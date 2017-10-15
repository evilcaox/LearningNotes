# JavaScript 是脚本语言
* JavaScript 是一种轻量级编程语言。
* JavaScript 是可插入 HTML 页面的编程代码。
* JavaScript 插入 HTML 页面后，可由所有现代浏览器执行



# &lt;sprict> 标签
如需在 HTML 页面中插入 JavaScript，必须使用 &lt;script> 标签。&lt;/script> 和 &lt;script> 会告诉 JavaScript 在何处开始和结束。&lt;script> 和 &lt;/script> 之间的代码行包含了 JavaScript;

    <!DOCTYPE HTML>
    <html>
      <body>
        <h1>这是一张网页</>
        <p>这时我的第一张带 JavaScript 的网页</p>
        <script>
        alert("JavaScript!");
        </script>
      </body>
    </html>

# JavaScript 语法
JavaScript 的语法和 Java语言类似，每个语句以 `;` 结束，语句块用 `{……}`。但是，JavaScript 并不强制要求在每个语句的结尾加 `;`。但是让 JavaScript 引擎自动加分号在某些情况下会改变程序的语义，导致运行结果和预期不一致，故最好加上 `;`。

注释也是与 Java 相似，分为 `//` 与 `/*……*/`。

同样，JavaScript 严格区分大小写。

JavaScript 会忽略多余的空格。



# 操作 HTML 元素
若需要从 JavaScript 访问某个 HTML 元素，可以使用 `documet.getElementById(id)`。使用 “id” 属性来标识 HTML 元素.

    <!DOCTYPE HTML>
    <html>
      <body>
        <h1>这是一张网页</>
        <p id="demo">这时我的第一张带 JavaScript 的网页</p>
        <script>
        documet.getElementById("demo").innerHTML="修改段落后的段落！";
        </script>
      </body>
    </html>

# 写到文档输出
使用 `document.write()` 仅仅向文档输出写内容。如果在文档已完成加载后执行 `document.write()`，整个 HTML 页面将被覆盖。

    <!DOCTYPE HTML>
    <html>
      <body>
        <h1>标题1</h1>
        <script>
        document.write("使用write写内容");
        </script>
      </body>
    </html>
    <!--如下会覆盖网页-->
    <!DOCTYPE HTML>
    <html>
      <body>
        <h1>标题1</h1>
        <p>这是段落1</p>
        <button onclick="myFunction()">按钮</button>
        <script>
        function myFunction(){
          document.write("覆盖");
        }
        </script>
      </body>
    </html>
