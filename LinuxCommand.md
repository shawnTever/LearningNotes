# Linux指令

- [Linux指令](#linux指令)
  - [rm 删除](#rm-删除)
  - [touch 创建文件，修改文件时间](#touch-创建文件修改文件时间)
  - [dpkg 安装.deb软件](#dpkg-安装deb软件)
  - [wget 下载文件的工具](#wget-下载文件的工具)
  - [tar 压缩解压文件.gz格式](#tar-压缩解压文件gz格式)
  - [mv 移动文件](#mv-移动文件)
  - [mkdir 创建目录](#mkdir-创建目录)
  - [chown 改变拥有着](#chown-改变拥有着)
  - [cat 连接文件并打印到标准输出设备](#cat-连接文件并打印到标准输出设备)
  - [cp 复制](#cp-复制)
  - [ps 查看当前进程](#ps-查看当前进程)
  - [pwd 绝对路径](#pwd-绝对路径)
  - [echo 标准输出中显示输入的字符串](#echo-标准输出中显示输入的字符串)
  - [chmod 用户对文件的权限](#chmod-用户对文件的权限)
  - [stat 查看文件信息](#stat-查看文件信息)
  - [zip 压缩解压 zip格式](#zip-压缩解压-zip格式)
  - [free 内存的使用情况](#free-内存的使用情况)
  - [top 系统处理器状态监视](#top-系统处理器状态监视)

- [主页](README.md)

**sudo vim /etc/profile**

修改环境变量

**source /etc/profile**

重新加载环境变量

**查看端口是否被占用以及释放端口流程（以80端口为例）**

查找被占用的端口：netstat -tln | grep 80

查看端口被哪个进程占用：sudo lsof -i :80

杀掉占用端口的进程：sudo kill -9 进程id

## rm 删除

rm [options] name

-i 删除前逐一询问确认。-f 即使原档案属性设为唯读，亦直接删除，无需逐一确认。-r 将目录及以下之档案亦逐一删除。

eg：

rm test.txt：删除 一般文件 "test.txt"

rm -r homework ：删除目录 "homework"

## touch 创建文件，修改文件时间

touch [-acfm][-d<日期时间>][-r<参考文件或目录>] [-t<日期时间>][--help][--version][文件或目录…]

a 改变档案的读取时间记录。

m 改变档案的修改时间记录。

c 假如目的档案不存在，不会建立新的档案。与 --no-create 的效果一样。

f 不使用，是为了与其他 unix 系统的相容性而保留。

r 使用参考档的时间记录，与 --file 的效果一样。

d 设定时间与日期，可以使用各种不同的格式。

t 设定档案的时间记录，格式与 date 指令相同。

--no-create 不会建立新档案。

--help 列出指令格式。

--version 列出版本讯息。

eg：

touch testfile：修改文件"testfile"的时间属性为当前系统时间

touch file：在当前目录下，使用该指令创建一个空白文件"file"

## dpkg 安装.deb软件

dpkg -i <.deb file name>: 安装.deb软件

dpkg -R <目录>：安装目录下所有软件包

dpkg –unpack <.deb file name>: 释放软件包

dpkg –configure package_file：重新配置和释放软件包

dpkg -r：删除软件包（保留其配置信息）

## wget 下载文件的工具

## tar 压缩解压文件.gz格式

tar -czvf test.tar.gz a.c：压缩 a.c文件为test.tar.gz

tar -tzvf test.tar.gz：列出压缩文件内容

tar -xzvf test.tar.gz：解压文件

## mv 移动文件

mv source_file(文件) dest_file(文件)：源文件名 source_file 改为目标文件名 dest_file

mv source_file(文件) dest_directory(目录)：将文件 source_file 移动到目标目录 dest_directory 中

mv source_directory(目录) dest_directory(目录)：目录名 dest_directory 已存在，将 source_directory 移动到目录名 dest_directory 中；目录名 dest_directory 不存在则 source_directory 改名为目录名 dest_directory

## mkdir 创建目录

mkdir [-p] dirName

-p 确保目录名称存在，不存在的就建一个

eg：

mkdir runoob：在工作目录下，建立一个名为 runoob 的子目录

mkdir -p runoob2/test：在工作目录下的 runoob2 目录中，建立一个名为 test 的子目录。若 runoob2 目录原本不存在，则建立一个。

## chown 改变拥有着

chown [-cfhvR] [--help] [--version] user[:group] file...

user : 新的文件拥有者的使用者 IDgroup : 新的文件拥有者的使用者组(group)-c : 显示更改的部分的信息-f : 忽略错误信息-h :修复符号链接-v : 显示详细的处理信息-R : 处理指定目录以及其子目录下的所有文件--help : 显示辅助说明--version : 显示版本

eg：

chown root /var/run/httpd.pid：把 /var/run/httpd.pid 的所有者设置 root

chown runoob:runoobgroup file1.txt：将文件 file1.txt 的拥有者设为 runoob，群体的使用者 runoobgroup。

chown -R runoob:runoobgroup *：将当前前目录下的所有文件与子目录的拥有者皆设为 runoob，群体的使用者 runoobgroup。

## cat 连接文件并打印到标准输出设备

cat [-AbeEnstTuv] [--help] [--version] fileName 连接文件并打印到标准输出设备

-n 或 --number：由 1 开始对所有输出的行数编号。

-b 或 --number-nonblank：和 -n 相似，只不过对于空白行不编号。

-s 或 --squeeze-blank：当遇到有连续两行以上的空白行，就代换为一行的空白行。

-v 或 --show-nonprinting：使用 ^ 和 M- 符号，除了 LFD 和 TAB 之外。

-E 或 --show-ends : 在每行结束处显示 $。

-T 或 --show-tabs: 将 TAB 字符显示为 ^I。

-A, --show-all：等价于 -vET。

-e：等价于"-vE"选项；

-t：等价于"-vT"选项；

## cp 复制

cp [options] source dest

-a：此选项通常在复制目录时使用，它保留链接、文件属性，并复制目录下的所有内容。其作用等于dpR参数组合。
-d：复制时保留链接。这里所说的链接相当于 Windows 系统中的快捷方式。
-f：覆盖已经存在的目标文件而不给出提示。
-i：与 -f 选项相反，在覆盖目标文件之前给出提示，要求用户确认是否覆盖，回答 y 时目标文件将被覆盖。
-p：除复制文件的内容外，还把修改时间和访问权限也复制到新文件中。
-r：若给出的源文件是一个目录文件，此时将复制该目录下所有的子目录和文件。
-l：不复制文件，只是生成链接文件。

eg：

将当前目录 test/ 下的所有文件复制到新目录 newtest 下：cp –r test/ newtest

复制文件到某路径并重命名：cp -i 原文件 目的路径/重命名文件

复制源目录 为 dir1 ,目标目录为dir2，如果dir2目录不存在：cp -r dir1 dir2；如果dir2目录已存在：cp -r dir1/. dir2

## ps 查看当前进程

eg:

ps是显示当前状态处于running的进程，grep表示在这些里搜索，而ps aux是显示所有进程和其状态。

查到mongo的进程：ps aux | grep mongo

## pwd 绝对路径

立刻得知您目前所在的工作目录的绝对路径名称

pwd [--help][--version]

--help 在线帮助

--version 显示版本信息

## echo 标准输出中显示输入的字符串

echo 命令用来在标准输出中显示输入的字符串。

-n 不要在最后自动换行

-e 若字符串中出现以下字符，则特别加以处理，而不会将它当成一般文字输出：

\a 发出警告声；

b 删除前一个字符；

\c 最后不加上换行符号；

\f 换行但光标仍旧停留在原来的位置；

\n 换行且光标移至行首；

\r 光标移至行首，但不换行；

\t 插入tab；

\v 与\f相同；

\\\ 插入\字符；

\nnn 插入nnn（八进制）所代表的ASCII字符；

## chmod 用户对文件的权限

控制用户对文件的权限的命令

chmod [-cfvR] [--help] [--version] mode file...

u 表示该文件的拥有者，g 表示与该文件的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示这三者皆是。+ 表示增加权限、- 表示取消权限、= 表示唯一设定权限。r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该文件是个子目录或者该文件已经被设定过为可执行。

eg：

将文件 file1.txt 设为所有人皆可读取 :

chmod ugo+r file1.txt

chmod a+r file1.txt

## stat 查看文件信息

## zip 压缩解压 zip格式

将 /home/html/ 这个目录下所有文件和文件夹打包为当前目录下的 html.zip：zip -q -r html.zip /home/html

如果在我们在 /home/html 目录下，可以执行以下命令：zip -q -r html.zip *

从压缩文件 cp.zip 中删除文件 a.c：zip -dv cp.zip a.c

## free 内存的使用情况

用来显示内存的使用情况，使用权限是所有用户。

free ［－b－k－m］ ［－o］ ［－s delay］ ［－t］ ［－V］

参数：－b －k －m：分别以字节（KB、MB）为单位显示内存使用情况。－s delay：显示每隔多少秒数来显示一次内存使用情况。－t：显示内存总和列。－o：不显示缓冲区调节列

## top 系统处理器状态监视

实时地对系统处理器的状态进行监视。

命令格式：top [-] [d] [p] [q] [c] [C] [S]    [n]

参数说明：

d：  指定每两次屏幕信息刷新之间的时间间隔。当然用户可以使用s交互命令来改变之。

p：  通过指定监控进程ID来仅仅监控某个进程的状态。

q：该选项将使top没有任何延迟的进行刷新。如果调用程序有超级用户权限，那么top将以尽可能高的优先级运行。

S： 指定累计模式

s ： 使top命令在安全模式中运行。这将去除交互命令所带来的潜在危险。

i：  使top不显示任何闲置或者僵死进程。

c： 显示整个命令行而不只是显示命令名在top命令的显示窗口，我们还可以输入以下字母，进行一些交互：

h或者?  : 显示帮助画面，给出一些简短的命令总结说明。

k：终止一个进程。系统将提示用户输入需要终止的进程PID，以及需要发送给该进程什么样的信号。一般的终止进程可以使用15信号；如果不能正常结束那就使用信号9强制结束该进程。默认值是信号15。在安全模式中此命令被屏蔽。

i：忽略闲置和僵死进程。这是一个开关式命令。

q：  退出程序。

r：  重新安排一个进程的优先级别。系统提示用户输入需要改变的进程PID以及需要设置的进程优先级值。输入一个正值将使优先级降低，反之则可以使该进程拥有更高的优先权。默认值是10。

S：切换到累计模式。

s :  改变两次刷新之间的延迟时间。系统将提示用户输入新的时间，单位为s。如果有小数，就换算成ms。输入0值则系统将不断刷新，默认值是5。

f或者F :从当前显示中添加或者删除项目。

o或者O  :改变显示项目的顺序。

l: 切换显示平均负载和启动时间信息。即显示影藏第一行

m： 切换显示内存信息。即显示影藏内存行

t：切换显示进程和CPU状态信息。即显示影藏CPU行

c：  切换显示命令名称和完整命令行。 显示完整的命令。 这个功能很有用。

M ： 根据驻留内存大小进行排序。

P：根据CPU使用百分比大小进行排序。

T： 根据时间/累计时间进行排序。

W：  将当前设置写入~/.toprc文件中。这是写top配置文件的推荐方法。
