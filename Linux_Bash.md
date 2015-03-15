=== readline ===
  * `set -o`
  * `emacs || vi`

### 符号 ###

  1. 魔法数字 `#!` sha-bang
  1. 特殊字符
    * ```# ; ;; . "" '' , \ / `` : ! * ? $ ${} $* $@ $? $$ () {} [] [[]] (())```
    * `> &> >& >> <> << <<< > < \< \> | >| || && & - = + % ~ ~+ =~ ^`

### 命令 ###

  * 内建命令/内部命令 builtin

  * I/O: echo printf read
  * 文件系统: cd pushd popd dirs
  * 变量: let eval set unset export declare typeset
    * readonly getopts
  * 脚本行为: source/. exit exec shopt caller
  * 命令: true false type hash hind help
  * 作业控制命令: jobs disown fg bg wait suspend logout
    * times kill killall command builtin enable autoload
  * 外部工具

  * 寻求帮组: --help man info
  * 时间日期: `[#date date]` zdump time cal sleep usleep hwclock
  * 文件目录: touch ls vdir cp mv rm mkdir rmdir ln readlink pwd
  * 权限管理: chown chmod chattr
  * 文件查找: which type file whatis whereis locate look find
  * 文本处理: cat tac head tail sort tsort uniq rev wc tr
    * expand unexpand cut paste join
    * fold fmt col column colrm nl pr
    * gettext msgfmt iconv recode tex gs enscript groff tbl eqn
    * lex(flex) yacc(bison)
    * strings diff diff3 sdiff cmp comm patch
    * grep sed awk
  * `> >> < |` xargs expr at batch
  * 归档工具: tar shar ar rpm cpio rpm2cpio gzip bzip2
    * compress uncompress sq zip unzip unarc unarj unrar
  * basename dirname
  * split csplit
  * sum cksum md5sum shalsum
  * shred
  * uuencode uudecode mimencode mmencode
  * crypt
  * mktemp make install dos2unix ptx more less
  * host ipcalc nslookup dig traceroute ping whois finger chfn vrfy

```
    which $cmdname
    whatis $cmdname
    whereis $cmdname
    type $cmdname
    locate $cmdname
    ll $cmdname
    file $patch/$cmdname
    pacman -Qo $patch/$cmdname
    pacman -Qi $pkgname
    pacman -Ql $pkgname
```

### 例程 ###

```
    kill -9 `ps ax | grep firefox | grep -v grep | awk '{ print $1 }'`
    WORKDIR=`dirname $0`
```



### date ###
[回到顶部](http://code.google.com/p/footearthtest/wiki/Bash#)
```
$>date
Mon Dec  7 15:43:39 CST 2009

#格式化输出
$> date +"%Y-%m-%d"
2009-12-07

#时间游走 当前时间 2009-12-07
# year , month , day ,hour , minute,second  - ago
#昨天输出
$> date  -d "1 day ago" +"%Y-%m-%d"
2009-12-06

#2秒后输出
$> date  -d "2 second" +"%Y-%m-%d %H:%M.%S"
2009-12-07 15:50.04

#传说中的 1234567890 秒
$>date -d "1970-01-01  1234567890 seconds"  +"%Y-%m-%d %H:%m:%S"
2009-02-13 23:02:30

#其他格式的转换
date -d "$(echo "03/Nov/2009 11:04:28" |perl -ne 'print "$2 $1 $3 $4\n" if /(.*?)"/(.*?)"/(.*?) (.*)/;') " +%Y-%m-%d
2009-11-03

#普通 转格式
$> date -d "2009-12-12" +"%Y/%m/%d %H:%M.%S"
2009/12/12 00:00.00

#apache 格式转换
$>date  -d "Dec 5, 2009 12:00:37 AM" +"%Y-%m-%d %H:%M.%S"
2009-12-05 00:00.37

#格式转换 后时间 游走
$>date  -d "Dec 5, 2009 12:00:37 AM 2 year ago" +"%Y-%m-%d %H:%M.%S"
2007-12-05 00:00.37


#时间差
#一小时 3600
#一天 86400 秒
$>st=$(date  -d "Dec 5, 2009 12:00:37 AM 1 day ago 1 hour ago " +"%s")
$>et=$(date  -d "Dec 5, 2009 12:00:37 AM" +"%s")
$>echo "时间差$[($et-$st)/86400]天，$[($et-$st)/3600%24]小时"
时间差1天，1小时
```