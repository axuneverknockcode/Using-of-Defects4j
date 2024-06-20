在安装Defects4j之前确保几件事情
1. JAVA的版本必须为8
2. 将Perl下载至自己的用户下（不知道有没有作用）`eval $(perl -I ~/perl5/lib/perl5/ -Mlocal::lib)`把这个加入到环境变量里
3. 安装cpamn

我在第一次使用Defects4j的时候遇到了一些问题，第一个是显示了Java 8 is required
解决方法就是安装JAVA8 

`sudo apt install openjdk-8-jdk`

在环境变量中配置JAVA路径

`export PATH=$PATH:/home/axu/HugFLearn/defects4j/framework/bin`
`export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre`

保存环境变量，然后`source ~/.bashrc`

如果重启之后发现JAVA还是原来的版本使用

`sudo update-alternatives --config java`选择JAVA8之后重启

当解决了Java8 is required的问题之后，初始化`./init.sh`仍然会出现一个下图的问题
```
Couldn't find project repositories! Did you (re)run 'defects4j/init.sh'?

Compilation failed in require at /home/axu/HugFLearn/defects4j/framework/bin/defects4j line 33.
BEGIN failed--compilation aborted at /home/axu/HugFLearn/defects4j/framework/bin/defects4j line 33.
```
后来去看官方文档，很多人都是重新下载了之后就成功了的，后来我反复看了下载的过程发现了，在安装第一个压缩包的时候会卡住
```
(base) axu@dell-t640:~/HugFLearn/defects4j$ ./init.sh
Setting up project repositories ... 
retrying curl https://defects4j.org/downloads/defects4j-repos.zip
Warning: Illegal date format for -z, --time-cond (and not a file name). 
Warning: Disabling time condition. See curl_getdate(3) for valid date syntax.
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  3  418M    3 13.2M    0     0  25130      0  4:51:22  0:09:10  4:42:12 31945
curl: (56) OpenSSL SSL_read: error:0A000126:SSL routines::unexpected eof while reading, errno 0

```
这个也是我看了别人说重新下载就好了的情况下，去尝试的然后发现这个包没下载的下来，所以可以根据里面的错误信息提供的网址去手都下载，然后解压好再放到`project_repos`文件当中。
所以我想那些重新下载就能好的人，大概率是在下载第一个包的时候就出问题了，那个包没有下载完所以导致在后面测试的时候找不到对应的文件。后面重新下载的时候把丢失的包又找回来了

之后去再设置环境变量`export PATH=$PATH:/home/axu/HugFLearn/defects4j/framework/bin`就ok了
测试一下
```
(base) axu@dell-t640:~/HugFLearn/defects4j$ defects4j info -p Lang
Summary of configuration for Project: Lang
--------------------------------------------------------------------------------
    Script dir: /home/axu/HugFLearn/defects4j/framework
      Base dir: /home/axu/HugFLearn/defects4j
    Major root: /home/axu/HugFLearn/defects4j/major
      Repo dir: /home/axu/HugFLearn/defects4j/project_repos
--------------------------------------------------------------------------------
    Project ID: Lang
       Program: commons-lang
    Build file: /home/axu/HugFLearn/defects4j/framework/projects/Lang/Lang.build.xml
--------------------------------------------------------------------------------
           Vcs: Vcs::Git
    Repository: /home/axu/HugFLearn/defects4j/project_repos/commons-lang.git
     Commit db: /home/axu/HugFLearn/defects4j/framework/projects/Lang/active-bugs.csv
Number of bugs: 64

```
Good Luck~!



