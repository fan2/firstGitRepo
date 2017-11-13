# cd
cd（change directory）：切换文件目录。

- `cd` / `cd ~`：进入当前用户的家目录（$HOME）；  
- `cd ..`：返回上级目录；  
- `cd -`：返回上次访问目录。  

切换到带有空格的路径，需要加转义字符（反斜杠<kbd>\\</kbd>）来标识空格。

以下示例从 `~/` 目录切换到 `/Library/Application Support/Sublime Text 3/Packages/User`：

```Shell
faner@THOMASFAN-MB0:~|⇒  cd /Users/faner/Library/Application\ Support/Sublime\ Text\ 3/Packages/User/
faner@THOMASFAN-MB0:~/Library/Application Support/Sublime Text 3/Packages/User|
⇒  
```

另外一种做法是定义 shell 字符串变量，然后使用 <kbd>$</kbd> 符号解引用变量作为 cd 的参数：

```Shell
faner@THOMASFAN-MB0:~|⇒  dir="/Users/faner/Library/Application Support/Sublime Text 3/Packages/User/"                    
faner@THOMASFAN-MB0:~|⇒  cd $dir
faner@THOMASFAN-MB0:~/Library/Application Support/Sublime Text 3/Packages/User|
```

# [bc](https://en.wikipedia.org/wiki/Bc_(programming_language))
[bc](https://www.gnu.org/software/bc/manual/html_mono/bc.html)(basic calculator) - An arbitrary precision calculator language  

bc is typically used as either a `mathematical scripting language` or as an `interactive mathematical shell`.  

There are four special variables, `scale`, `ibase`, `obase`, and `last`.  

支持输入数学表达式的解释型计算语言  

在终端输入 `bc` 即可进入 bc 命令行解释器；输入 `quit` 或者 `<C-d>` 发送 EOF 结束退出 bc。

> [COMMAND LINE CALCULATOR, BC](http://linux.byexamples.com/archives/42/command-line-calculator-bc/)  
> [How to Use the "bc" Calculator in Scripts](https://www.lifewire.com/use-the-bc-calculator-in-scripts-2200588)  
> [Linux下的计算器(bc、expr、dc、echo、awk)知多少？](http://blog.csdn.net/linco_gp/article/details/4517945)  
> [Linux中的super pi(bc 命令总结)](http://www.linuxidc.com/Linux/2012-06/63684.htm)  
> [我使用过的Linux命令之bc - 浮点计算器、进制转换](http://codingstandards.iteye.com/blog/793734)  

## basic
1. 在 bash shell 终端输入 `bc` 即可启动 bc 计算器：

```Shell
pi@raspberrypi:~ $ bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
56.8 + 77.7
134.5
```

可书写代数表达式，用变量承载计算结果，作为进一步计算的操作数：

```Shell
a=2+3;
a
5
b=a*4;
b
20
```

2. 在 bash shell 终端可基于[数据流重定向或管道](https://www.cnblogs.com/mingcaoyouxin/p/4077264.html)作为 `bc` 的输入表达式：

```Shell
pi@raspberrypi:~ $ bc <<< "56.8 + 77.7"
134.5

pi@raspberrypi:~ $ echo "56.8 + 77.7" | bc
134.5
```

3. `scale` 变量可指定浮点数计算输出精度：

```Shell
scale=2; 5 * 7 /3
11.66
```

4. 以下为在 shell scripts 调用 bc 做计算的示例:

```Shell
pi@raspberrypi:~ $ result=$(echo "scale=2; 5 * 7 /3;" | bc)
pi@raspberrypi:~ $ echo $result
11.66
```

## last
**`last`**  (an  extension)  is a variable that has the value of the *last* printed number.

 last 变量代表上个表达式的计算结果，可将 last 变量作为后续表达式的操作数，进行二次计算：

```
2+3
5
last*4
20
```

## ibase/obase
在 bc 命令解释器中输入 `ibase=10;obase=16;2017`，转换输出2017（十进制）的十六进制：

```Shell
ibase=10;obase=16;2017
7E1
```

或者 echo 分号相隔的表达式重定向作为 bc 的输入进行解释运行：

```Shell
pi@raspberrypi:~ $ echo "ibase=10;obase=16;2017" | bc
7E1
```

# python

> [python格式化输出](http://blog.csdn.net/wchoclate/article/details/42297173)  
> [Python print函数用法](http://blog.csdn.net/zanfeng/article/details/52164124)  

## 进制转换
python 内置的 `bin()`、`oct()`、`hex()` 函数支持将十进制数转换为对应的二进制、八进制、十六进制字符串。

```Shell
>>> bin(2017)
'0b11111100001'
>>> oct(2017)
'0o3741'
>>> print(hex(2017))
0x7e1
>>> print(0x7e1)
2017
```

或者通过 `print()` 函数的占位符 `%o`、`%x` 格式化输出十进制数对应的八进制和十六进制格式：

```Shell
>>> x=2017
>>> print('oct=%o' %(x))
oct=3741
>>> print('hex=%x' %(2017))
hex=7e1
```

# Checksum
## cksum
cksum, sum -- display file checksums and block counts
     
## CRC32
crc32 - Perform a 32bit Cyclic Redundancy Check

## MD5 
md5 -- calculate a message-digest fingerprint (checksum) for a file

md5 命令后的默认输入参数为文件名，也可通过 `-s` 选项指定计算字符串参数的MD5。

```
     -s string
             Print a checksum of the given string.
```

## SHA1
shasum - Print or Check SHA Checksums

```Shell
SYNOPSIS
        Usage: shasum [OPTION]... [FILE]...
        Print or check SHA checksums.
        With no FILE, or when FILE is -, read standard input.

          -a, --algorithm   1 (default), 224, 256, 384, 512, 512224, 512256
          -b, --binary      read in binary mode
          -c, --check       read SHA sums from the FILEs and check them
          -t, --text        read in text mode (default)
```

When verifying SHA-512/224 or SHA-512/256 checksums, indicate the **algorithm** explicitly using the `-a` option, e.g.

`shasum -a 512224 -c checksumfile`

# pipe
how count all lines in all files in current dir and omit empty lines with wc, grep, cut and bc commands

```Shell
echo `wc -l * | grep total | cut -f2 -d’ ‘` – `grep -in “^$” * | wc -l ` | bc
```