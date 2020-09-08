## 2020-9-8 Install Python

centos 安装 python3.7.9，发现 pip install 运行不了，是因为 openssl 版本问题，搞了很久发现没有可行的方式，后来才发现正确的升级 openssl 的方法

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

./configure --prefix=/usr/local/python37 --with-openssl=/usr/local/openssl
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
