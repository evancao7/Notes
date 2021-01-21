命令行中 {必填}  [选填] 之间用空格隔开
cd / 回到根目录，/代表根
-la 等价于 -l -a,即两个参数公用一个-   
ls是list的缩写

touch 新建
access最近被访问的时间
modify文件内容被修改的时间
change关于此文件发生任何改变的时间
rm  remove

mv
文件夹的改名和移动
~/D/g/A/N/Linux ❯❯❯ mkdir a
~/D/g/A/N/Linux ❯❯❯ ls
a/       day1.md
~/D/g/A/N/Linux ❯❯❯ mv a b
~/D/g/A/N/Linux ❯❯❯ ls
b/       day1.md
将day1.md移动到b/中
~/D/g/A/N/Linux ❯❯❯ ls
b/       day1.md
~/D/g/A/N/Linux ❯❯❯ mv day1.md b/
~/D/g/A/N/Linux ❯❯❯ ls
b/


ls 



mkdir  建立目录
命令语法
      mkdir [选项] 目录
命令选项
  -v   显示信息
  -p   递归创建

~/D/g/A/N/Linux ❯❯❯ mkdir -v a
mkdir: created directory 'a'

递归创建文件夹 -p
~/D/g/A/N/Linux ❯❯❯ mkdir -p a/b/c
~/D/g/A/N/Linux ❯❯❯ mkdir -pv a/b/c/d
~/D/g/A/N/Linux ❯❯❯ ls
a/       day1.md
~/D/g/A/N/Linux ❯❯❯ cd a/b/c/d/

rmdir 删除空目录
命令语法
  rmdir  [options]  directory
命令选项
  -p   递归删除空目录
删除
~/D/g/A/N/Linux ❯❯❯ rmdir a
rmdir: a: Directory not empty
~/D/g/A/N/Linux ❯❯❯ rmdir -p a
rmdir: a: Directory not empty
~/D/g/A/N/Linux ❯❯❯ rmdir -p a/b/c/d/
~/D/g/A/N/Linux ❯❯❯ ls
day1.md


~/D/g/A/N/Linux ❯❯❯ mkdir -pv a/b/c/d
~/D/g/A/N/Linux ❯❯❯ ls
a/       day1.md
强制删除文件夹a，以及其所包含的所有
~/D/g/A/N/Linux ❯❯❯ rm -rf a
~/D/g/A/N/Linux ❯❯❯ ls
day1.md