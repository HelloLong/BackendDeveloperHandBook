# Login 登录

## session认证

众所周知，http协议本身是无状态的协议，那就意味着当有用户向系统使用账户名称和密码进行用户认证之后，下一次请求还要再一次用户认证才行。因为我们不能通过http协议知道是哪个用户发出的请求，所以如果要知道是哪个用户发出的请求，那就需要在服务器保存一份用户信息(保存至session)，然后在认证成功后返回cookie值传递给浏览器，那么用户在下一次请求时就可以带上cookie值，服务器就可以识别是哪个用户发送的请求，是否已认证，是否登录过期等等。这就是传统的session认证方式。

session认证的缺点其实很明显，由于session是保存在服务器里，所以如果分布式部署应用的话，会出现session不能共享的问题，很难扩展。于是乎为了解决session共享的问题，又引入了redis，接着往下看。

## token认证

这种方式跟session的方式流程差不多，不同的地方在于保存的是一个token值到redis，token一般是一串随机的字符(比如UUID)，value一般是用户ID，并且设置一个过期时间。每次请求服务的时候带上token在请求头，后端接收到token则根据token查一下redis是否存在，如果存在则表示用户已认证，如果token不存在则跳到登录界面让用户重新登录，登录成功后返回一个token值给客户端。

优点是多台服务器都是使用redis来存取token，不存在不共享的问题，所以容易扩展。缺点是每次请求都需要查一下redis，会造成redis的压力，还有增加了请求的耗时，每个已登录的用户都要保存一个token在redis，也会消耗redis的存储空间。

有没有更好的方式呢？接着往下看。

## JWT

Jwt 全称 Json web token, 是为了在网络应用环境间传递声明而执行的一种基于 `JSON` 的开放标准（RFC 7519）。该 token 被设计为紧凑且安全的，特别适用于分布式站点的单点登录（SSO）场景。

<figure><img src="../../.gitbook/assets/f84b0a914d9077c432db25010a3ca013.png" alt=""><figcaption><p>jwt 流程图</p></figcaption></figure>

流程描述一下：

1. 用户使用账号、密码登录应用，登录的请求发送到Authentication Server。
2. Authentication Server进行用户验证，然后创建JWT字符串返回给客户端。
3. 客户端请求接口时，在请求头带上JWT。
4. Application Server验证JWT合法性，如果合法则继续调用应用接口返回结果。

### JWT 组成

JWT 由三个部分组成：头部（Header）、载荷（Payload）和签名（Signature）。每个部分都使用 Base64 编码，并使用句点（.）连接起来。具体结构如下：

* **头部（Header）**：包含 JWT 的类型（例如，"typ": "JWT"）和所使用的算法（例如，"alg": "HS256"）。这些字段提供了关于 JWT 的元数据。
* **载荷（Payload）**：存储实际的用户数据或声明。它包含一组称为声明（Claims）的属性，可以自定义添加一些标准声明（如过期时间、发行人等）或自定义声明。载荷中的声明可以被加密，但通常是以明文形式存在。
* **签名（Signature）**：用于验证消息的完整性和真实性。签名是通过将头部和载荷与一个秘密密钥进行加密生成的，确保 JWT 没有被篡改过。

### 实现示例

<pre class="language-python"><code class="lang-python"><strong># pip install pyJWT
</strong># JwtProject/api/views.py

import uuid
import jwt
import datetime
from jwt import exceptions
from django.http import JsonResponse
from django.views import View
from django.conf import settings
from .models import UserInfo

class JwtLoginView(View):

   def post(self, request):
       user_name = request.POST.get("username")
       pwd = request.POST.get("password")

       # 校验用户是否存在
       user = UserInfo.objects.filter(username=user_name, password=pwd).first()

       if not user:
           return JsonResponse({"code": 1001, "error": "用户名或密码不正确"})

       # 头部信息
       header = {
           "typ": "jwt",
           "alg": "HS256"
      }

       # 载荷信息
       payload = {
           "name": user.username,
           "exp": datetime.datetime.utcnow() + datetime.timedelta(minutes=5)
      }

       token = jwt.encode(payload=payload, key=settings.SECRET_KEY, algorithm="HS256", headers=header).decode("utf-8")

       return JsonResponse({"code": 1000, "token": token})


class JwtOrderView(View):

   def get(self, request):
       # 获取token，校验用户身份
       token = request.GET.get("token")

       # 第一步，切割 jwt
       # 第二步，解密第二段，校验是否过期
       # 第三步，校验第三段是否正确

       payload = None
       msg = None

       try:
           payload = jwt.decode(token, settings.SECRET_KEY, True)
           print(payload)
       except exceptions.ExpiredSignatureError:
           msg = "签证已失效"
       except exceptions.DecodeError:
           msg = "token认证失败"
       except exceptions.InvalidTokenError:
           msg = "非法token"

       if not payload:
           return JsonResponse({"code": 1001, "message": msg})

       return JsonResponse({"code": 1000, "message": "订单列表"})
</code></pre>



## References

JWT 技术介绍 [https://mp.weixin.qq.com/s/YL8kU3csDFXAk3ac5j2VVg](https://mp.weixin.qq.com/s/YL8kU3csDFXAk3ac5j2VVg)&#x20;

不懂就学，什么是JWT？[https://mp.weixin.qq.com/s/Q4rO3ycGtBLGlnPdlcHh2g](https://mp.weixin.qq.com/s/Q4rO3ycGtBLGlnPdlcHh2g)

\


