# 如何更改 SQL Server 的身份验证方式
在默认情况下，SQL Server 2012 Express 是采用集成的 Windows 安全验证且禁用了 sa 登录名。有时不方便使用 Windows 集成安全验证，我们就需要启用 SQL Server 2012 Express 的混合安全验证，也就是说由 SQL Server 来验证用户而不是由 Windows 来验证用户。

启动页面的服务器名称组成为：机器名\\实例名。第一次使用默认为 Windows 身份验证，是安装时默认决定的。

## 设置 SQL Server 的身份验证
在通过 Windows 身份验证后的页面左侧，鼠标右键点击连接的服务器，选择属性。接着选择安全性，勾选 SQL Server 和 Windows 身份验证模式。最后点击确定。

## 设置 sa 的密码并启用 sa 登录名
点击展开连接的服务器，选择并打开安全性，选择并打开登录名，鼠标右键点击 sa 并选择属性。点击状态，登录处勾选启用。继续选择常规，更改密码后点击确定。重启后生效。
