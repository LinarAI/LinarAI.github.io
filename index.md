## PostgreSQL 数据类型

数值数据类型
数字数据类型用于指定表中的数字数据。

名称 描述 存储大小 范围
smallint 存储整数，小范围 2 字节 -32768 至 +32767
integer 存储整数。使用这个类型可存储典型的整数 4 字节 -2147483648 至 +2147483647
bigint 存储整数，大范围。 8 字节 -9223372036854775808 至 9223372036854775807
decimal 用户指定的精度，精确 变量 小数点前最多为 131072 个数字; 小数点后最多为 16383 个数字。
numeric 用户指定的精度，精确 变量 小数点前最多为 131072 个数字; 小数点后最多为 16383 个数字。
real 可变精度，不精确 4 字节 6 位数字精度
double 可变精度，不精确 8 字节 15 位数字精度
serial 自动递增整数 4 字节 1 至 2147483647
bigserial 大的自动递增整数 8 字节 1 至 9223372036854775807
字符串数据类型
String 数据类型用于表示字符串类型值。

数据类型 描述
char(size) 这里 size 是要存储的字符数。固定长度字符串，右边的空格填充到相等大小的字符。
character(size) 这里 size 是要存储的字符数。 固定长度字符串。 右边的空格填充到相等大小的字符。
varchar(size) 这里 size 是要存储的字符数。 可变长度字符串。
character varying(size) 这里 size 是要存储的字符数。 可变长度字符串。
text 可变长度字符串。
日期/时间数据类型
日期/时间数据类型用于表示使用日期和时间值的列。

名称 描述 存储大小 最小值 最大值 解析度
timestamp [(p)]不带时区 日期和时间(无时区) 8 字节 4713 bc 294276 ad 1 微秒/14 位数
timestamp [(p)]带时区 包括日期和时间，带时区 8 字节 4713 bc 294276 ad
date 日期(没有时间) 4 字节 4713 bc 5874897 ad 1 微秒/14 位数
time [(p)]不带时区 时间(无日期) 8 字节 00:00:00 24:00:00 1 微秒/14 位数
time [(p)] 带时区 仅限时间，带时区 12 字节 00:00:00+1459 24:00:00-1459 1 微秒/14 位数
interval [fields ][p] 时间间隔 12 字节 -178000000 年 178000000 年 1 微秒/14 位数
一些其他数据类型
布尔类型：
名称 描述 存储大小
boolean 它指定 true 或 false 的状态。 1 字节
货币类型：
名称 描述 存储大小 范围
money 货币金额 8 字节 -92233720368547758.08 至 +92233720368547758.07
几何类型：
几何数据类型表示二维空间对象。最根本的类型：点 - 形成所有其他类型的基础。

名称 存储大小 表示 描述
point 16 字节 在一个平面上的点 (x,y)
line 32 字节 无限线(未完全实现) ((x1,y1),(x2,y2))
lseg 32 字节 有限线段 ((x1,y1),(x2,y2))
box 32 字节 矩形框 ((x1,y1),(x2,y2))
path 16+16n 字节 封闭路径(类似于多边形) ((x1,y1),…)
polygon 40+16n 字节 多边形(类似于封闭路径) ((x1,y1),…)
circle 24 字节 圆 <(x，y)，r>(中心点和半径)

## 2020-9-18 React Native Web Socket INVALID_STATE_ERR

发现只能在 ws.onopen 里面调用 ws.send, 在外面的话会报 INVALID_STATE_ERR
原来建立 web socket 是需要时间的，需要等连接建好了再调 ws.send
另外可以加上:
if (instance && instance.readyState === WebSocket.OPEN) {
instance.send("Lancelot");
}

## 2020-9-8 Install Python

centos 安装 python3.7.9，发现 pip install 运行不了，SSLError("Can't connect to HTTPS URL because the SSL module is not available")
发现是因为 openssl 版本问题，搞了很久发现网上很难找到直接可行的方式解决，后来才发现正确的升级 openssl 的方法：

```markdown
升级步骤：

1、去官网下载最新版本，或 wget 下载也行 http://www.openssl.org

wget https://www.openssl.org/source/openssl-1.1.1.tar.gz

2、解压并进入解压目录后执行：

./config --prefix=/usr/local/openssl shared zlib
make
make && make install

3、备份当前 openssl：

mv /usr/local/openssl /usr/local/openssl.bak

mv /usr/include/openssl /usr/include/openssl.bak

4、配置使用新版本：

ln -s /usr/local/openssl/bin/openssl /usr/bin/openssl

ln -s /usr/local/openssl/include/openssl /usr/include/openssl

5、更新动态链接库数据：

echo "/usr/local/ssl/lib" >> /etc/ld.so.conf

重新加载动态链接库
ldconfig -v

6、重新查看版本号：

openssl version

如果在更新完后执行 openssl version 命令报错

这是由于 openssl 库的位置不正确造成的。
可以做一个软连接：

ln -s /usr/local/openssl/lib/libssl.so.1.1 /usr/lib/

ln -s /usr/local/openssl/lib/libcrypto.so.1.1 /usr/lib/

然后执行 openssl version 命令即可

重新安装 python
注意：需要指定 openssl 的安装路径，--with-openssl

./configure --prefix=/usr/local/python3 --with-openssl=/usr/local/openssl
make
make install
```

## Welcome to LinarAI Pages

You can use the [editor on GitHub](https://github.com/LinarAI/LinarAI.github.io/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1

## Header 2

### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/LinarAI/LinarAI.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

```
thank you

```
