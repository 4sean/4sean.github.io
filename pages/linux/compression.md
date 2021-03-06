## 打包压缩相关指令<br/>

**bzip2(选项)(参数)命令用于创建和管理（包括解压缩）**<br/>
  ```
  -c或——stdout：将压缩与解压缩的结果送到标准输出；
  -d或——decompress：执行解压缩；
  -f或-force：bzip2在压缩或解压缩时，若输出文件与现有文件同名，预设不会覆盖现有文件。若要覆盖。请使用此参数；
  -h或——help：在线帮助；
  -k或——keep：bzip2在压缩或解压缩后，会删除原始文件。若要保留原始文件，请使用此参数；
  -s或——small：降低程序执行时内存的使用量；
  -t或——test：测试.bz2压缩文件的完整性；
  -v或——verbose：压缩或解压缩文件时，显示详细的信息；
  -z或——compress：强制执行压缩；
  -V或——version：显示版本信息；
  --repetitive-best：若文件中有重复出现的资料时，可利用此参数提高压缩效果；
  --repetitive-fast：若文件中有重复出现的资料时，可利用此参数加快执行效果。
  ```

**gunzip(选项)(参数)命令用来解压缩文件**<br/>
  ```
  -a或——ascii：使用ASCII文字模式；
  -c或--stdout或--to-stdout：把解压后的文件输出到标准输出设备；
  -f或-force：强行解开压缩文件，不理会文件名称或硬连接是否存在以及该文件是否为符号连接；
  -h或——help：在线帮助；
  -l或——list：列出压缩文件的相关信息；
  -L或——license：显示版本与版权信息；
  -n或--no-name：解压缩时，若压缩文件内含有原来的文件名称及时间戳记，则将其忽略不予处理；
  -N或——name：解压缩时，若压缩文件内含有原来的文件名称及时间戳记，则将其回存到解开的文件上；
  -q或——quiet：不显示警告信息；
  -r或——recursive：递归处理，将指定目录下的所有文件及子目录一并处理；
  -S或<压缩字尾字符串>或----suffix<压缩字尾字符串>：更改压缩字尾字符串；
  -t或——test：测试压缩文件是否正确无误；
  -v或——verbose：显示指令执行过程；
  -V或——version：显示版本信息；
  ```

**gzip(选项)(参数)命令用来压缩文件**<br/>
  ```
  -a或——ascii：使用ASCII文字模式；
  -d或--decompress或----uncompress：解开压缩文件；
  -f或——force：强行压缩文件。不理会文件名称或硬连接是否存在以及该文件是否为符号连接；
  -h或——help：在线帮助；
  -l或——list：列出压缩文件的相关信息；
  -L或——license：显示版本与版权信息；
  -n或--no-name：压缩文件时，不保存原来的文件名称及时间戳记；
  -N或——name：压缩文件时，保存原来的文件名称及时间戳记；
  -q或——quiet：不显示警告信息；
  -r或——recursive：递归处理，将指定目录下的所有文件及子目录一并处理；
  -S或<压缩字尾字符串>或----suffix<压缩字尾字符串>：更改压缩字尾字符串；
  -t或——test：测试压缩文件是否正确无误；
  -v或——verbose：显示指令执行过程；
  -V或——version：显示版本信息；
  -<压缩效率>：压缩效率是一个介于1~9的数值，预设值为“6”，指定愈大的数值，压缩效率就会愈高；
  --best：此参数的效果和指定“-9”参数相同；
  --fast：此参数的效果和指定“-1”参数相同。
  ```

**tar(选项)(参数)命令用来解压压缩文件**<br/>
  ```
  -A或--catenate：新增文件到以存在的备份文件；
  -B：设置区块大小；
  -c或--create：建立新的备份文件；
  -C <目录>：这个选项用在解压缩，若要在特定目录解压缩，可以使用这个选项。
  -d：记录文件的差别；
  -x或--extract或--get：从备份文件中还原文件；
  -t或--list：列出备份文件的内容；
  -z或--gzip或--ungzip：通过gzip指令处理备份文件；
  -Z或--compress或--uncompress：通过compress指令处理备份文件；
  -f<备份文件>或--file=<备份文件>：指定备份文件；
  -v或--verbose：显示指令执行过程；
  -r：添加文件到已经压缩的文件；
  -u：添加改变了和现有的文件到已经存在的压缩文件；
  -j：支持bzip2解压文件；
  -v：显示操作过程；
  -l：文件系统边界设置；
  -k：保留原有文件不覆盖；
  -m：保留文件不被覆盖；
  -w：确认压缩文件的正确性；
  -p或--same-permissions：用原来的文件权限还原文件；
  -P或--absolute-names：文件名使用绝对名称，不移除文件名称前的“/”号；
  -N <日期格式> 或 --newer=<日期时间>：只将较指定日期更新的文件保存到备份文件里；
  --exclude=<范本样式>：排除符合范本样式的文件。
  ```
  实例<br/>
  ```
  tar -cvf log.tar log2012.log    仅打包，不压缩！ 
  tar -zcvf log.tar.gz log2012.log   打包后，以 gzip 压缩 
  tar -jcvf log.tar.bz2 log2012.log  打包后，以 bzip2 压缩 
  ```

**zip(选项)(参数)命令可以用来解压缩文件**<br/>
  ```
  -A：调整可执行的自动解压缩文件；
  -b<工作目录>：指定暂时存放文件的目录；
  -c：替每个被压缩的文件加上注释；
  -d：从压缩文件内删除指定的文件；
  -D：压缩文件内不建立目录名称；
  -f：此参数的效果和指定“-u”参数类似，但不仅更新既有文件，如果某些文件原本不存在于压缩文件内，使用本参数会一并将其加入压缩文件中；
  -F：尝试修复已损坏的压缩文件；
  -g：将文件压缩后附加在已有的压缩文件之后，而非另行建立新的压缩文件；
  -h：在线帮助；
  -i<范本样式>：只压缩符合条件的文件；
  -j：只保存文件名称及其内容，而不存放任何目录名称；
  -J：删除压缩文件前面不必要的数据；
  -k：使用MS-DOS兼容格式的文件名称；
  -l：压缩文件时，把LF字符置换成LF+CR字符；
  -ll：压缩文件时，把LF+cp字符置换成LF字符；
  -L：显示版权信息；
  -m：将文件压缩并加入压缩文件后，删除原始文件，即把文件移到压缩文件中；
  -n<字尾字符串>：不压缩具有特定字尾字符串的文件；
  -o：以压缩文件内拥有最新更改时间的文件为准，将压缩文件的更改时间设成和该文件相同；
  -q：不显示指令执行过程；
  -r：递归处理，将指定目录下的所有文件和子目录一并处理；
  -S：包含系统和隐藏文件；
  -t<日期时间>：把压缩文件的日期设成指定的日期；
  -T：检查备份文件内的每个文件是否正确无误；
  -u：更换较新的文件到压缩文件内；
  -v：显示指令执行过程或显示版本信息；
  -V：保存VMS操作系统的文件属性；
  -w：在文件名称里假如版本编号，本参数仅在VMS操作系统下有效；
  -x<范本样式>：压缩时排除符合条件的文件；
  -X：不保存额外的文件属性；
  -y：直接保存符号连接，而非该链接所指向的文件，本参数仅在UNIX之类的系统下有效；
  -z：替压缩文件加上注释；
  -$：保存第一个被压缩文件所在磁盘的卷册名称；
  -<压缩效率>：压缩效率是一个介于1~9的数值。
  ```
  实例<br/>
  ```
  zip file1.zip file1 创建一个zip格式的压缩包 
  zip -r file1.zip file1 file2 dir1 将几个文件和目录同时压缩成一个zip格式的压缩包 
  unzip file1.zip 解压一个zip格式压缩包 
  ```



<!-- ## 下一篇文章
<a href='https://github.com/MarsPen/-notes-summary/blob/master/linux/package.md'>linux基础系列之-软件包管理</a>

## linux基础命令系列目录
<a href='https://github.com/MarsPen/-notes-summary/blob/master/linux/index.md'>linux基础命令系列</a> -->

