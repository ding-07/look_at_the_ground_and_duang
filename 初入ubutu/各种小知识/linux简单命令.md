# 本文档总结一下目前常用的linux命令

> 2023.1.5

### 1.列出所有安装的软件包（两种方式）

1. `sudo apt list --installed`
2. `dpkg --get-selections`  

### 2.更新、删除或安装我们不需要的软件

#### 更新：

- `sudo apt update` 用于从你的软件源更新软件目录
- `sudo apt upgrade` 用于根据软件目录更新软件

#### 删除：

1. 方法一：

- `sudo apt list --installed | grep 软件名 `
- `sudo apt purge 软件包名`
- `sudo apt autopurge`

> 注意：文件名，软件名均可用正则表达式

2. 方法二：

- `dpkg --get-selections | grep 软件名`
- `sudo apt purge 软件包名`
- `sudo apt autopurge`

#### 安装：

1. 方法一：

- `sudo apt install 软件名 `

> 直接从互联网搜索安装

2. 方法二：

- `sudo dpkg -i 软件包名`

> 对已下载好的软件包进行软件安装

3. 方法三：
- 1. `pip3 install 包名`
- 2. `pip3 install -r requirements.txt`
> 使用pip3安装python3的包,`-r`选项作用为`install from the given requirements file`，可以根据txt文件中的内容同时安装多个包（将包名分别写在txt文件中即可，分隔符为`换行`）


### 3.在当前目录下查找文件

- `ls | grep 文件名   `

### 4.有规律的创建文件（以用于测试）

1. `touch {1..10}.txt`

> 同时创建1.txt 2.txt ..... 10.txt 共十个文件

2. `touch {a..z}.txt`

> 同时创建a.txt b.txt ..... z.txt 共26个文件

### 5.find 命令的使用

1. `基本格式 find 路径 -name(按文件名查找) 文件名`   功能：在该路径下查找该文件名的文件  -iname不区分文件名大小写
2. `find` 单个命令默认打印当前目录下的所有文件名到标准输出
3. `-print` 为默认选项，会在标准输出中查找文件名，当前目录为默认路径，故如果是查找当前目录下的文件，直接  `find 文件名`   即可

### 6.xargs 命令的使用

1. `xargs`作用是将输入作为下一个命令的参数
2. `find 路径 -name 文件名 | xargs rm`   删除该路径下该文件名的文件

> **注意**：`xargs`是按空格区分单词的，故如果文件名中含有空格，则 `2`中命令无法将其删除。例如文件为 `'1 2.txt'`则xargs读取时会读取成 `'1 `和 `2.txt'`两个参数并送给 `rm`命令，则此时 `rm`命令无法正确删除文件

### 7.管道命令|的使用

- 管道命令 `|`的作用是将前一个命令的输出转化为后一个命令的输入
- 有时后一个命令可以直接操作输入，则用管道命令 `|`即可，有时后一个命令不能直接操作输入，则需要用 `| xargs`(管道+xargs)将输入转化为参数才能使用（如 `rm`命令就需要使用 `管道+xargs` 例子: `ls | grep nihao* | xargs rm`）

### 8.新建和删除文件

- `touch 文件名`    功能：新建文件
- `mkdir 文件夹名`  功能：新建文件夹
- `rm 文件名 `      功能：删除文件但是不能删除文件夹
- `rmdir 文件夹名 ` 功能：删除文件夹但是不能删除文件
- `rm -r`文件名或文件夹名   功能：文件和文件夹都能删除

### 9.复制/剪切文件

1. cp命令(copy)
2. mv命令(move)
   用法：`cp/mv 源文件 目标目录`  功能：将源文件复制到目标目录

### 10.查看文件大小

- wc命令(word count)
  用法： `wc 选项 文件名`
  选项： `-bytes` 显示文件字节数  `-l` 显示文件行数  `-w` 显示文件字数

### 11.source 命令

- 用途：用于重新载入一遍配置文件，常用来刷新当前shell的环境。
  ros中每次更改代码，重新使用catkin_make编译完后，由于配置文件发生了改变，所以需要重新source一遍以更新环境

### 12.watch命令
`watch -n 2 其他命令`  
这行命令的用途是每隔2s运行一次`其他命令`，watch命令常用于以固定时间间隔运行某个命令。我常用它来监视显卡使用情况，命令如下  
`watch -n 2 nvidia-smi`




