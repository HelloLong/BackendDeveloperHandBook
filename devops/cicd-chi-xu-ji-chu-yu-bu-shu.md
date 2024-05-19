# CICD 持续基础与部署

## CI - 持续集成 (Continuous integration)

持续集成指的是，频繁地（一天多次）将代码集成到主干。

## CD - 持续交付 (**Continuous delivery**)

持续交付指的是，频繁地将软件的新版本，交付给质量团队或者用户，以供评审。如果评审通过，代码就进入生产阶段。

## CD - 持续部署 (**Continuous deployment**)

持续部署是持续交付的下一步，指的是代码通过评审以后，自动部署到生产环境。

## 流程

提交 -> 测试 -> 构建 -> 测试 -> 部署 -> 回滚

测试：单元测试、集成测试、端到端测试。

构建常见工具：Jenkings、Trabvis、Codeship、strider。

## References

[持续集成是什么？](https://www.ruanyifeng.com/blog/2015/09/continuous-integration.html)

\
\
