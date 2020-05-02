# Cookie 及其应用
Cookie 是客户访问 Web服务器时，服务器在客户硬盘上存放的信息。Cookie 管理包括两个方面：将 Cookie对象发送到客户端和从客户端读取 Cookie。

## 1.1 Cookie API
对 Cookie 的管理需要使用 <code>javax.servlet.http.Cookie</code> 类，构造方法为 <code>public Cookie(String name,String value)</code>，参数 name 为 Cookie 名，value 为 Cookie 的值。

常用方法如下：
<ol>
<li><code>public String getName()</code>
<p>返回 Cookie 的名称，名称一旦创建不能改变。
</p>
</li>
<li><code>public String getValue</code>
<p>返回 Cookie 的值。
</p>
</li>
<li><code>public void setValue(String newValue)</code>
<p>在 Cookie 创建后为它指定一个新值。
</p>
</li>
<li><code>public void setMaxAge(int expiry)</code>
<p>设置 Cookie 在浏览器中的最长存活时间，单位为秒。如果参数值为负，表示 Cookie 并不永久存储，如果是 0 表示删除该 Cookie。
</p>
</li>
<li><code>public int getMaxAge()</code>
<p>返回 Cookie 在浏览器上最大存活时间。
</p>
</li>
<li><code>public void setDomain(String pattern)</code>
<p>设置该 Cookie 所在的域。域名以 <code>.</code> 开头。默认情况下只有发送 Cookie 的服务器才能得到它。
</p>
</li>
<li><code>public String getDomain()</code>
<p>返回该 Cookie 设置的域名。
</p>
</li>
</ol>

## 1.2 向客户端发送 Cookie
要把 Cookie 发送到客户端，Servlet 先要使用 Cookie 类的构造方法创建一个 Cookie 对象，通过 setXxx() 设置各种属性，再通过响应对象的 <code>addCookie(Cookie)</code> 把 Cookie 加入响应头。具体步骤如下：
<ol>
<li>创建 Cookie 对象
</li>
<p>调用 Cookie 类的构造方法可以创建 Cookie 对象。例如：<code>Cookie userCookie=new Cookie("username","hacker")</code>。
<li>设置 Cookie 的最大存活时间
</li>
<p>在默认情况下，发送到客户端的 Cookie 对象只是一个会话级别的 Cookie，它存储在浏览器内存中，用户关闭浏览器后 Cookie 对象将被删除。如果希望浏览器将 Cookie 对象存在磁盘上，需要使用 Cookie 类的 <code>setMaxAge()</code> 设置 Cookie 的最大存活时间。单位为秒。
</p>
<li>向客户发送 Cookie 对象
</li>
<p>要将 Cookie 对象发送到客户端，需要调用响应对象的 <code>addCookie()</code> 将 Cookie 添加到 SetCookie 响应头，代码如下：<code>response.addCookie(userCookie)</code>。
</p>
</ol>

## 1.3 从客户端读取 Cookie
要从客户端读入 Cookie,Servlet 应该调用请求对象的 <code>getCookies()</code>，该方法返回一个 Cookie 对象数组。大多数情况下，只需要用循环访问该数组的各个元素寻找指定名字的 Cookie，然后对该 Cookie 调用 <code>getValue()</code>  取得与指定名字关联的值。具体步骤如下：
<ol>
<li>调用请求对象的 getCookies 方法
</li>
<p>该方法返回一个 Cookie 对象数组。如果请求中不含 Cookie，返回 null。例如：<code>Cookie[] cookies=request.getCookies();</code>
</p>
<li>对 Cookie 数组循环
</li>
<p>有了 Cookie 对象数组后，就可以通过访问它的每个元素，然后调用每个 Cookie 的 <code>getName()</code>，直到找到一个与希望的名称相同的对象为止。找到所需要的 Cookie 对象后，一般调用它的 <code>getValue()</code>，并根据得到的值做进一步处理。
</p>
</ol>
