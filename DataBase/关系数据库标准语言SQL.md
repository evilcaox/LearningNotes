<h1>关系数据库标准语言SQL</h1>
<ol>
<li>SQL 的基本概念
  <p>
    <p>
      支持 SQL 的关系数据库管理系统同样支持数据库三级模式结构。如 图 1 SQL 对关系数据库模式的支持。其中外模式包括若干视图（view) 和部分基本表（base table），数据库模式包括若干基本表，内模式包括若干存储文件（stored file）。
    </p>
    <p>
      基本表是本身独立存在的表，在关系数据库管理系统中有个关系就对应一个基本表。一个或多个基本表对应一个存储文件，一个表可以带若干索引，索引也存放在存储文件中。
    </p>
    <p>
      存储文件的逻辑结构组成了关系数据库系统的内模式。存储文件的物理结构对最终用户是隐蔽的。
    </p>
    <p>
      视图是从一个或几个基本表导出的表。它本身不独立存储在数据库中，即数据库中只存放视图的定义而不存放视图对应的数据。这些数据仍存放在导出视图的基本表中，因此视图是一个虚表。视图的概念与基本表等同，用户可以在视图上再定义视图。
    </p>
  </p>
</li>
<li>学生-课程数据库
  <p>
    该数据库包含三个表：
    <blockquote >
      学生表：Student(<span style="border-bottom:1px solid white;">Sno</span>,Sname,Ssex,Sage,Sdept)<br>
      课程表：Course(<span style="border-bottom:1px solid white;">Cno</span>,Cname,Cpno,Ccredit)<br>
      学生选课表：SC(<span style="border-bottom:1px solid white;">Sno,Cno</span>,Grade)
    </blockquote>
  </p>
  <p>
    关系中主码加下划线表示。各表数据如下：
  </p>

  <table>
    <caption>学生表</caption>
    <tr>
      <td>学号(Sno)</td><td>姓名(Sname)</td><td>性别(Ssex)</td><td>年龄(Sage)</td><td>系(Sdept)</td>
    </tr>
    <tr>
      <td>140406001</td><td>张三</td><td>男</td><td>18</td><td>计算机</td>
    </tr>
    <tr>
      <td>140406002</td><td>李四</td><td>男</td><td>19</td><td>计算机</td>
    </tr>
    <tr>
      <td>140406003</td><td>王二</td><td>男</td><td>17</td><td>计算机</td>
    </tr>
    <tr>
      <td>140405001</td><td>韩六</td><td>男</td><td>18</td><td>网络</td>
    </tr>
    <tr>
      <td>140405002</td><td>赵红花</td><td>女</td><td>19</td><td>网络</td>
    </tr>
  </table>

  <table>
    <caption>课程表</caption>
    <tr>
      <td>课程号(Cno)</td><td>课程名(Cname)</td><td>先行课(Cpno)</td><td>学分(Ccredit)</td>
    </tr>
    <tr>
      <td>1</td><td>数据库</td><td>5</td><td>4</td>
    </tr>
    <tr>
      <td>2</td><td>数学</td><td></td><td>2</td>
    </tr>
    <tr>
      <td>3</td><td>信息系统</td><td>1</td><td>4</td>
    </tr>
    <tr>
      <td>4</td><td>操作系统</td><td>6</td><td>3</td>
    </tr>
    <tr>
      <td>5</td><td>数据结构</td><td>7</td><td>4</td>
    </tr>
    <tr>
      <td>6</td><td>数据处理</td><td></td><td>2</td>
    </tr>
    <tr>
      <td>7</td><td>Java</td><td>6</td><td>4</td>
    </tr>
  </table>

  <table>
    <caption>学生选课表</caption>
    <tr>
      <td>学号(Sno)</td><td>课程号(Cno)</td><td>成绩(Grade)</td>
    </tr>
    <tr>
      <td>140406001</td><td>1</td><td>84</td>
    </tr>
    <tr>
      <td>140406001</td><td>2</td><td>92</td>
    </tr>
    <tr>
      <td>140406001</td><td>3</td><td>88</td>
    </tr>
    <tr>
      <td>140405002</td><td>2</td><td>99</td>
    </tr>
    <tr>
      <td>140405002</td><td>3</td><td>98</td>
    </tr>
  </table>
</li>
<li> 数据定义
    <ol>
      <li>模式（数据库）的定义与删除
        <ul>
          <li>定义模式
            <p>
            <label>语法</label>
            <pre>
              CREATE SCHEMA <模式名> AUTHORIZATION <用户名>;
            </pre>
            <strong>注：</strong>若没有指定&#60;模式名&#62;,那么&#60;模式名&#62;隐含为&#60;用户名&#62;。<br>
            <p>要创建模式，调用该命令的用户必须拥有数据库管理员权限，或者获得了数据库管理员授予的 `CREATE SCHEMA` 的权限。</p>
            例如在 SQL Server 中创建一个模式：
            <pre>
              create database <数据库名>;
            </pre>
            </p>
          </li>
          <li>删除模式
            <p>
              <label>语法：</label>
              <pre>
                DROP SCHEMA <模式名><CASCADE|RESTRICT>;
              </pre>
              <p>其中 CASCADE 和 RESTRICT 必选一个。选择前一个表示级联，在删除模式的同时把该模式中所有的数据库对象全部删除；选择后一个表示限制，若该模式已经定义了下属的数据库对象（如表、视图等），则拒绝该删除语句的执行。</p>
              例如在 SQL Server 中：
              <pre>
                drop database <数据库名>;
              </pre>
            </p>
          </li>
        </ul>
      </li>
      <li>基本表的定义、删除与修改
        <ul>
          <li>定义基本表
            <p>
              创建了一个模式就建立了一个数据库的命名空间，一个框架。在这个空间首先要定义的是该模式包含的数据库基本表。</br>
              <label>语法：</label>
              <pre>
                CREATE TABLE <表名>(
                  <列名> <数据类型> [列级完整性约束]，
                  <表级完整性约束>
                  );
              </pre>
              建表的同时通常还可以定义与该表有关的完整性约束条件，这些完整性约束条件被存入系统的数据字典中，当用户操作表中数据时由关系数据库管理系统自动检查该操作是否违背这些完整性约束条件。若完整性约束条件涉及该表的多个属性列，则必须定义在表级上，否则既可以定义在列级也可以定义在表级。</br>

              例如在 SQL Server 中：
              <pre>
                create table Course(
                  Cno char(4) primary key,//列级完整性约束，设置为主码
                  Cname char(40) not null,//列级完整性约束条件，设置不能取空值
                  Cpno char(4) unique,//列级约束条件，取唯一值
                  Ccredit smallint,
                  foreign key (Cpno) references Course(Cno)//表级完整性约束条件，Cpno 是外码，被参照表是 Course,被参照的列是 Cno
                  );
              </pre>
            </p>
          </li>
          <li>模式与表
            <p>
              每一个基本表都属于某一个模式，一个模式包含多个基本表。当定义基本表时一般可以有三种方法定义它所属的模式：
              <ul>
                <li>在表名中明显地给出模式名：
                  <pre>
                    create table "数据库名".表名();
                  </pre>
                </li>
                <li>
                  在创建模式语句中同时创建表;
                </li>
                <li>设置所属的模式，这样在创建表时表名中不必给出模式名。
                </li>
              </ul>

              当用户创建表（其他数据库对象也一样）时若没有指定模式，系统根据搜索路径（serch path）来确定该对象所属的模式。<br>

              使用下面的语句可以显示当前的搜索路径：
              <pre>
                show serch_path;
              </pre>
              管理员也可以设置搜索路径：
              <pre>
                set serch_path to "模式名",public;
              </pre>
            </p>
          </li>
          <li>修改基本表
            <p>
              语法：
              <pre>
                alter tale <表名>
                [add [column] <新列名> <数据类型> [完整性约束]]
                [add <表级完整性约束>]
                [drop [column] <列名> [CASCADE|RESTRICT]]
                [drop constraint <完整性约束名> [RESTRICT|CASCADE]]
                [alter column <列名> <数据类型>];
              </pre>
              add 子句用于增加新列、新的列级完整性约束条件和新的表级完整性约束条件和新的表级完整性约束条件。drop column 子句用于删除表中的列;drop constraint 子句用于删除指定的完整性约束条件；alter column 子句用于修改原有的列定义，包括列名和数据类型。
            </p>
          </li>
          <li>删除基本表
            <p>
              语法：
              <pre>
                drop table <表名> [RESTRICT|CASCADE]
              </pre>
            </p>
          </li>
          <li>数据类型
            <p>
              关系模型中一个很重要的概念是域。每一个属性来自一个域，它的取值必须是域中的值。在 SQL 中域的概念用数据类型来实现，定义表的各个属性时需要指明其数据类型及长度。
            <table>
              <tr>
                <td>数据类型</td><td>含义</td>
              </tr>
              <tr>
                <td>char(n),character(n)</td><td>长度为 n 的字符串</td>
              </tr>
              <tr>
                <td>varchar(n),charactervarying(n)</td><td>最大长度为 n 的变长</td>
              </tr>
              <tr>
                <td>clob</td><td>字符串大对象</td>
              </tr>
              <tr>
                <td>blob</td><td>二进制大对象</td>
              </tr>
              <tr>
                <td>int,integer</td><td>长整数（4字节）</td>
              </tr>
              <tr>
                <td>smallint</td><td>短整数（2字节）</td>
              </tr>
              <tr>
                <td>bigint</td><td>大整数（8字节）</td>
              </tr>
              <tr>
                <td>numeric(p,d)</td><td>定点数，由 p 位数字（不包括符号、小数点）组成，小数点后面有 d 位数字</td>
              </tr>
              <tr>
                <td>decimal(p,d),dec(p,d)</td><td>同 numeric</td>
              </tr>
              <tr>
                <td>real</td><td>取决于机器精度的单精度浮点数</td>
              </tr>
              <tr>
                <td>double precision</td><td>取决于机器精度的双精度浮点数</td>
              </tr>
              <tr>
                <td>float(n)</td><td>可选精度的浮点数，精度至少为 n 位数字</td>
              </tr>
              <tr>
                <td>boolean</td><td>逻辑布尔量</td>
              </tr>
              <tr>
                <td>date</td><td>日期，包含年、月、日，格式为 YYYY-MM-DD,将输入日期时需要加单引号</td>
              </tr>
              <tr>
                <td>time</td><td>时间，包含一日的时、分、秒，格式为 HH:MM:SS</td>
              </tr>
              <tr>
                <td>timestamp</td><td>时间戳类型</td>
              </tr>
              <tr>
                <td>interval</td><td>时间间隔类型</td>
              </tr>
            </table>
            </p>
          </li>
        </ul>
      </li>
      <li>索引的建立与删除
        <p>
          当表的数据量比较大时，查询操作会比较耗时。建立索引是加快查询速度的有效手段。数据库索引类类似于图书后面的索引，能加快定位到需要查询的内容。用户可以根据应用环境的需要建立一个或多个索引，以提供多种存储路径，加快查找速度。<br>

          数据库索引由多种类型，常见索引包括顺序文件上的索引、B+ 数索引、散列索引、位图索引等。顺序文件上的索引是针对按指定属性值升序或降序存储的关系，在该属性上建立一个顺序索引文件，索引文件由属性值和相应的元组指针组成。B+ 索引树索引是将索引属性组织成 B+ 树形式，B+ 树的叶结点为属性值和相应的元组指针。B+ 树索引具有动态平衡的优点。散列索引是建立若干个桶，将索引属性按照其散列函数映射到相应桶中，桶中存放索引属性值和相应的元组指针。散列索引具有查找速度快的特点。位图索引是用位向量记录索引属性中可能出现的值，每个向量对应一个可能值。<br>

          索引虽然能够加速数据库查询，但需要占用一定的存储空间，当基本表更新时，索引要进行相应的维护，这些都会增加数据库的负担，因此要根据实际应用的需要有选择地创建索引。<br>

          一般来说，建立与删除索引由数据库管理员或表的属主，即建立表的人，负责完成。关系数据库管理系统在执行查询时会自动选择合适的索引作为存取路径，用户不必也不能显示地选择索引。索引是关系数据库管理系统的内部实现技术，属于内模式范围。<br>
          <ul>
            <li>建立索引<br>
                在 SQL 语言中，建立索引使用 create index 语句，其一般格式为
                <pre>
                  create [UNIQUE] [CLUSTER] index <索引名> on <表名>(<列名>[<次序>] [，<列名> <次序>]……)；
                </pre>
                其中，<表名> 是要建索引的基本表的名字。索引可以建立在该表的一列或多列上，各列名之间用逗号分隔。每个<列名>后面还可以用<次序>指定索引值的排列次序，可选 ASC （升序） 或 DESC （降序），默认值为 ASC。<br>

                UNIQUE 表明此索引的每一个索引值只对应唯一的数据记录。<br>

                CLUSTER 表示要建立的索引是聚族索引。<br>

            </li>
            <li>修改索引<br>
                语法：
                <pre>
                  alter index <> rename to <新索引名>;
                </pre>
            </li>
            <li>删除索引<br>
                语法：
                <pre>
                  drop index <索引名>;
                </pre>
            </li>
          </ul>
        </p>
      </li>
    </ol>
</li>
<li> 数据查询
  <p>
    数据查询时数据库的核心操作。SQL 提供 select 语句进行数据查询，该语句具有灵活的使用方式和丰富的功能。其一般语法为：
    <pre>
      select [ALL|DISTINCT] <目标列表达式>[,<目标表达式>]……
      from <表名或视图名>[,<表名或视图名>]|(<select 语句>)[AS]<别名>
      [where<条件表达式>]
      [group by<列名>[having<条件表达式>]]
      [order by<列名2>[ASC|DESC]];
    </pre>
    <ul>
      <li>单表查询
        <ul>
          <li>选择表中若干列
            <ul>
              <li>查询指定列<br/>
                <label>语法：</label>
                <pre>
                  select <目标表达式> from <表名>;//目标列表达式指定要查询的属性列,目标列表达式中各个列的先后顺序可以与表中的顺序不一致
                  例如查询全体学生的学号和姓名：
                  select Sno,Sname from Student;
                </pre>
              </li>
              <li>查询全部列（整张表）<br/>
                  <label>语法：</label>
                  <pre>
                    select * from <表名>;
                    例如查询全体学生的详细记录：
                    select * from Student;
                  </pre>
              </li>
              <li>查询经过计算的值<br/>
                <label>语法：</label>
                <pre>
                  select <目标列表表达式> from <表名>;//目标列表表达式可以为一个表达式,字符串常量、函数等。
                  例如查询学生的出生年：
                  select Sname,2017-Sage from Student;
                  查询所在系并用小写字母表示：
                  select lower(Sdept) from Student;
                  使用别名表示小写后的列：
                  select lower(Sdept) dept from Student;
                </pre>
              </li>
            </ul>
          </li>
          <li> 选择表中的若干元组
            <ul>
              <li>消除取值重复的行<br/>
                  在查询的列前面使用关键字 distinct 消除他们：
                  <pre>
                    例如查询选了课程并有成绩的人：
                    select distinct Sno from SC;
                  </pre>
              </li>
              <li>查询满足条件的元组<br/>
                  用于查询满足条件的元组可以通过 where 子句实现。
                  <ul>
                    <li>比较大小<br/>
                        用于进行比较大小的运算符一般包括 `=(等于)、>(大于)、<(小于)、>=(大于等于)、<=(小于等于)、!=或<>(不等于)、!>(不大于)、!<(不小于)` 以及 `not+上述运算比较符`。
                        <pre>
                          例如查询计算机系全体学生：
                          select Sname from Student where Sdept='CS';
                          例如查询年龄小于 20 的学生：
                          select Sname from Student where Sage<20;
                        </pre>
                    </li>
                    <li>确定范围<br/>
                        使用 `between……and……` 和 `not between……and……` 可以用来查找属性值在（或不在）指定范围内的元组，其中 between 后跟下限，and 后跟上限。
                        <pre>
                          查询年龄在 18~20 岁的学生名：
                          select Sname from Student where age between 18 and 20;
                          查询年龄不在 18~20 岁的学生名：
                          select Sname from Student where age not between 18 and 20;
                        </pre>
                    </li>
                    <li>确定集合<br/>
                        使用 `in` 可以用来查询属性值属于指定集合的元组。`not in` 查询属性值不属于指定集合的元组。
                        <pre>
                          查询计算机（CS)、数学（MA）、和信息系（IS）的学生姓名：
                          select Sname from Sdept in ('CS','MA','IS');
                          查询不是计算机（CS）、数学（MA）的学生姓名：
                          select Sname from Sdept not in ('CS','MA');
                        </pre>
                    </li>
                    <li>字符匹配<br/>
                        谓语 like 可以用来进行字符串匹配。一般语法如：`[not] like '<匹配串>' [escape '<换码字符>']`。含义是查找指定的属性列值与 <匹配串> 相匹配的元组。<匹配串> 可以是一个完整的字符串，也可以是含有通配符 % 和 _ 。 其中 `%` 代表任意长度（长度可为 0）的字符串，例如 a%b 表示以 a 开头，以 b 结尾的任意长度的字符串；`_` 表示代表任意单个字符,例如 a_b 表示以 a 开头 b 结尾的长度为 3 的任意字符串，注意当字符集为 GBK 时汉字只需一个 _ ,而为 ASCII 时一个汉字需要两个 _ 。若想要查询的字符串本身就含有通配符 % 或 _ ,这时需要使用 `escape '<换码字符>'`。
                        <pre>
                          查询所有姓李的同学：
                          select Sname from Student where Sname like '李%';
                        </pre>
                    </li>
                    <li>涉及空值的查询<br/>
                        使用 `is null` 查询空值记录。使用 `is not null` 查询不为空值的记录。
                        <pre>
                          查询选修课程而没有成绩的学号：
                          select Sno from SC where Grade is null;//不可以使用 Grade=null;
                          查询选修课程而有成绩的学号：
                          select Sno from SC where Grade is not null;
                        </pre>
                    </li>
                    <li>多重条件查询<br/>
                        逻辑运算符 AND 和 OR 可用来连接多个查询条件，AND 优先级高于 OR，可以使用括号改变优先级。
                        <pre>
                          查询计算机系且年龄小于 19 的同学学号：
                          select Sno from Student where Sdept='CS' and Sage<19;
                        </pre>
                    </li>
                  </ul>
              </li>
            </ul>
          </li>
          <li>ORDER BY 子句<br/>
              用户可以使用 ORDER BY 子句对查询的结果按照一个属性列升序（ASC）或者降序（DESC）排列，默认值为升序。
              <pre>
                查询选修 3 号课程的学生的学号及成绩，结果按成绩降序排列。
                select Sno,Grade from SC where Cno=3 order by Grade desc;
              </pre>
          </li>
          <li>聚集函数<br/>
              SQL 提供许多聚集函数，如下：
              <ul>
                <li>count(\*) 统计元组个数</li>
                <li>count([DISTINCT|ALL] <列名>) 统计一列中值的个数</li>
                <li>sum([DISTINCT|ALL] <列名>) 计算一列值的总和（此列必须为数值型）</li>
                <li>avg([DISTINCT|ALL] <列名>) 计算一列值的平均值（此列必须为数值型）</li>
                <li>max([DISTINCT|ALL] <列名>) 求一列中最大值</li>
                <li>min([DISTINCT|ALL] <列名>) 求一列中最小值</li>
              </ul>
              <strong>注意：</strong>where 子句中是不能用聚集函数作为条件表达式的。聚集函数只能用于 select 子句和 group by 中 having 子句。<br/>
              <pre>
                查询学号为 201215121 选修课程的总学分数。
                select sum(Ccredit) from SC,Course where Sno=201215121 and SC.Cno=Course.Cno;
              </pre>
          </li>
          <li>GROUP BY 子句<br/>
              GROUP BY 子句将查询结果按某一列或多列的值分组，值相等的为一组。对查询结果分组的目的是为了细化聚集函数的作用对象。如果未对查询结果进行分组，聚集函数将作用于整个查询结果。分组后聚集函数将作用于每一个组，即每一组都有一个函数值。<br/>
              <pre>
                查询选修了三门以上课程的学生学号：
                select Sno from SC group by Sno havin count(\*)>3;//这里先对 Sno 进行分组，再用聚集函数对每一组计数，having 短语给出了选择组的条件，只有满足条件的组才会被选出。
              </pre>
          </li>
        </ul>
      </li>
      <li>连接查询<br/>
        若一个表查询同时涉及两个以上的表，则称为连接查询。
        <ul>
          <li>等值与非等值查询<br/>
              查询的 where 子句中用来连接两个表的条件称为连接条件或连接谓语，其一般格式为：`[<表名1>.]<列名1> <比较运算符> [<表名2>.]<列名2>` 或 `[<表名1>.]<列名1> between [<表名2>.]<列名2> and [<表名2>.]<列名2>`。当运算符为 = 时，称为等值连接。使用其他运算符称为非等值连接。**一条 SQL 语句可以同时完成选择和连接查询，这时 WHERE 子句是由连接谓语和选择谓语组成的复合条件。**
              <pre>
                例如查询每个学生及其选修课程的情况：
                select Student.*,SC.* from Student,SC where Student.Sno=SC.Sno;
              </pre>
          </li>
          <li>自身连接<br/>
            连接操作不仅可以在两个表之间进行，也可以是一个表与其自己进行连接，称为表的自身连接。要进行表的自身连接，就要对表取别名。为 Course 取两个别名为 FIRST、SECOND。
            <pre>
              例如查询没一门课的先修课：
              select FIRST.Cno,SECOND.Cpno from Course FIRST,Course SECOND where FIRST.Cpo=SECOND.Cno;
            </pre>
          </li>
          <li>外连接<br/>
              有时想把 Student 表与 SC 表连接起来查看学生的选课成绩情况，可是部分学生没有选课，所以在连接时导致 Student 中这些元组在连接时被舍弃了。但我们仍想把 Student 的悬浮元组保存在结果关系中，而在 SC 表的属性上填空值 NULL，这时就需要外连接。<br/>
              <label>例如：</label>
              <pre>
                select Student.Sno,Sname,Ssex,Sage,Sdept,Cno,Grade from Student left join SC on (Student.Sno=SC.Sno);
              </pre>
          </li>
          <li>多表连接<br>
            在 where 子句中用 and 连接。例如：<br/>
            <pre>
              select Student.Sno,Sname,Cname,Grade from Student,SC,Course where Student.Sno=SC.Sno and SC.Cno=Course.Cno;
            </pre>
          </li>
        </ul>
      </li>
      <li>嵌套查询
        <p>
          在 SQL 语言里，一个 `select-from-where` 语句称为一个查询块。将一个查询块嵌套在另一个查询块的 `where` 子句或 `having` 短语的条件中的查询称为嵌套查询。例如：<br/>
          <code>  SELECT Sname From Student WHERE Sno IN(SELECT Sno FROM SC WHERE Cno='2');</code><br/>
          SQL 语言允许多层嵌套查询，即一个子查询中还可以嵌套其他子查询。需要特别指出的是，子查询的 `SELECT` 语句中不能使用 `ORDER BY` 子句，`ORDER BY` 子句只能对最终查询结果排序。
        </p>
        <ul>
          <li>带 IN 谓语的子查询<br/>
            <p>
              在嵌套查询中，子查询的结果往往是一个集合，所以谓词 IN 是嵌套查询中最常用的谓语。<br/>

              例如：查询选修了课程名为 “信息系统” 的学生学号和姓名。<br/>

              分析：该查询涉及学号、姓名和课程名三个属性。学号和姓名存放在 Student 表中，课程名存放在 Course 表中，但 Student 与 Course 两个表之间没有直接联系，必须通过 SC 表建立它们二者之间的关系，所以本表实际上涉及三个关系。
            </p>
            <pre>
              SELECT Sno,Sname FROM WHERE Sno IN(SELECT Sno FROM SC WHERE Cno IN(SELCET Cno FROM Course WHERE Cname='信息系统'))；
              //分析
              1. SELCET Cno FROM Course WHERE Cname='信息系统' 找出‘信息系统’的课程号，结果为3.
              2. SELECT Sno FROM SC WHERE Cno IN(SELCET Cno FROM Course WHERE Cname='信息系统') 在 SC 关系中找出选修了 3 号课程的学生学号。
              3. 最后在 Student 关系中取出 Sno 和 Sname。
            </pre>
            同样可以使用连接查询实现：
            <pre>
              SELECT Student.Sno,Snmae FROM Student,SC,Course WHERE Student.Sno=SC.Sno AND SC.Cno=Course.Cno AND Course.Cname='信息系统';
            </pre>
          </li>
          <li>带有比较运算符的子查询<br/>
            当用户能确切知道内层查询返回的是单个值时，可以用 <code>>、<、=、>=、<=、!=或 <>` </code>等比较运算符。<br/>
            例如：找出每个学生超过他自己选修课程平均成绩的课程号。
            <pre>
              SELECT Sno,Cno FROM SC x WHERE Grade>=(SELECT AVG(Grade) FROM SC y WHERE y.Sno=s.Sno);
            </pre>
          </li>
          <li>带有 ANY（SOME）或 ALL 谓语的子查询<br/>
            子查询返回单值时可以使用比较运算符，但返回多值时要用 ANY （有的系统用 SOME）或 ALL 谓词修饰符。而使用 ANY 或 ALL 谓词时则必须同时使用比较运算符。其语义如下：<br/>
            <ul>
                <li>
                  &#62;ANY
                  <p>大于子查询结果中的某个值</p>
                </li>
                <li>
                  &#62;ALL
                  <p>大于子查询结果中的所有值</p>
                </li>
                <li>
                  &#60;ANY
                  <p>小于子查询结果中的某个值</p>
                </li>
                <li>
                  &#60;ALL
                  <p>小于子查询结果中的所有值</p>
                </li>
                <li>
                  &#62;&#61;ANY
                  <p>大于等于子查询结果中的某个值</p>
                </li>
                <li>
                  &#62;&#61;ALL
                  <p>大于等于子查询结果中的所有值</p>
                </li>
                <li>
                  &#60;&#61;ANY
                  <p>小于等于子查询结果中的某个值</p>
                </li>
                <li>
                  &#60;&#61;ALL
                  <p>小于等于子查询结果中的所有值</p>
                </li>
                <li>
                  &#61;ANY
                  <p>等于子查询结果中的某个值</p>
                </li>
                <li>
                  &#61;ALL
                  <p>等于查询结果中的所有值</p>
                </li>
                <li>
                  &#33;&#61;(&#60;&#62;)ANY
                  <p>不等于子查询中的某个值</p>
                </li>
                <li>
                  &#33;&#61;(&#60;&#62;)ALL
                  <p>不等于子查询中的任何一个值</p>
                </li>
            </ul>
            例如查询非计算机科学系中比计算机科学系任意一个学生年龄小的学生姓名和年龄：
            <pre>
              SELECT Sname,Sage
              FROM Student
              WHERE Sage&#60;ANY(SELECT Sage
                                 FROM Student
                                 WHERE Sdept='CS')
              AND Sdept!='CS';
            </pre>
          </li>
          <li></li>
        </ul>
      </li>
    </ul>
</li>
</ol>
