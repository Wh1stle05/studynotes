# Linux 基础命令

---

## 1. 当前目录

### `pwd`

显示当前工作目录的绝对路径。

```bash
$ pwd
/home/a3165
```

---

## 2. 目录查看

### `ls`

列出目录内容。

```bash
$ ls
LICENSE  README.md  assets  bench.py  example.py  nanovllm  pyproject.toml
```

### `ls -l`

显示文件详细信息。

```bash
$ ls -l
total 28
-rw-r--r-- 1 a3165 a3165 1067 Apr 20 23:47 LICENSE
-rw-r--r-- 1 a3165 a3165 2185 Apr 20 23:47 README.md
drwxr-xr-x 2 a3165 a3165 4096 Apr 20 23:47 assets
-rw-r--r-- 1 a3165 a3165 1121 Apr 20 23:47 bench.py
-rw-r--r-- 1 a3165 a3165  916 Apr 20 23:47 example.py
drwxr-xr-x 6 a3165 a3165 4096 Apr 20 23:47 nanovllm
-rw-r--r-- 1 a3165 a3165  598 Apr 20 23:47 pyproject.toml
```

### `ls -la`

显示隐藏文件。

```bash
$ ls -la
total 48
drwxr-xr-x  5 a3165 a3165 4096 Apr 20 23:47 .
drwxr-x--- 51 a3165 a3165 4096 Apr 20 23:55 ..
drwxr-xr-x  8 a3165 a3165 4096 Apr 20 23:47 .git
-rw-r--r--  1 a3165 a3165 4329 Apr 20 23:47 .gitignore
-rw-r--r--  1 a3165 a3165 1067 Apr 20 23:47 LICENSE
-rw-r--r--  1 a3165 a3165 2185 Apr 20 23:47 README.md
drwxr-xr-x  2 a3165 a3165 4096 Apr 20 23:47 assets
-rw-r--r--  1 a3165 a3165 1121 Apr 20 23:47 bench.py
-rw-r--r--  1 a3165 a3165  916 Apr 20 23:47 example.py
drwxr-xr-x  6 a3165 a3165 4096 Apr 20 23:47 nanovllm
-rw-r--r--  1 a3165 a3165  598 Apr 20 23:47 pyproject.toml
```

### `ls -lah`

以更适合阅读的单位显示文件大小。

```bash
$ ls -lah
total 48K
drwxr-xr-x  5 a3165 a3165 4.0K Apr 20 23:47 .
drwxr-x--- 51 a3165 a3165 4.0K Apr 20 23:55 ..
drwxr-xr-x  8 a3165 a3165 4.0K Apr 20 23:47 .git
-rw-r--r--  1 a3165 a3165 4.3K Apr 20 23:47 .gitignore
-rw-r--r--  1 a3165 a3165 1.1K Apr 20 23:47 LICENSE
-rw-r--r--  1 a3165 a3165 2.2K Apr 20 23:47 README.md
drwxr-xr-x  2 a3165 a3165 4.0K Apr 20 23:47 assets
-rw-r--r--  1 a3165 a3165 1.1K Apr 20 23:47 bench.py
-rw-r--r--  1 a3165 a3165  916 Apr 20 23:47 example.py
drwxr-xr-x  6 a3165 a3165 4.0K Apr 20 23:47 nanovllm
-rw-r--r--  1 a3165 a3165  598 Apr 20 23:47 pyproject.toml
```

### `ls -i`

显示 inode 编号。

```bash
$ ls -i
433379 LICENSE    433381 assets    433384 example.py  433410 pyproject.toml
433380 README.md  433383 bench.py  433385 nanovllm
```

---

## 3. 创建、复制、移动、删除



### `mkdir`

创建目录。

```bash
$ mkdir ./demo
```
递归创建，如果父目录不存在则一并创建。
```bash
$ mkdir -p ./demo/a/b
```


### `touch`

创建空文件。

```bash
$ touch demo/a/file1.txt
```

修改文件时间戳,可用于测试定时任务或备份系统逻辑。

```bash
$ touch -t 202612251200.00 document.txt
# touch -t CCYYMMDDHHMM.SS filename
```
### `cp`

复制文件。

```bash
#同名备份
$ cp demo/a/file2.txt demo/backup/   
#异名备份
$ cp demo/a/file2.txt demo/backup/file3.txt
```
递归复制。
```bash
$ cp -r nginx
```
`cp -r` (**Recursive**)复制将会导致子目录和文件的**权限**，**时间戳**，**所有者**发生变化，会改为执行命令的用户
```bash
$ cp -a nginx
```
`cp -a`(**Archive**)等同于`cp -dR --preserve=all`<br>

该复制尽力使目标文件与源文件一模一样

**保留链接 (`-d`)**： 如果源文件里有一个符号链接（快捷方式），`-a` 会复制这个链接本身；而 `-r` 可能会把链接指向的实际内容复制一遍。

**保留属性 (`--preserve=all`)**： 强制保留原始的**所有者（Owner）**、**所属组（Group）**、**权限（Permissions）**以及**时间戳（Timestamps）**。

**递归复制 (`-R`)**： 包含所有子目录。

### `mv`

移动或重命名文件。

```bash
$ mv demo/a/file3.txt demo/a/file3-renamed.txt
```



### `rm`

删除文件。

```bash
$ rm demo/x/delete.txt
```



---

## 4. 文件内容查看

### `cat`

查看文件全部内容。

```bash
$ cat demo/a/file2.txt
alpha
beta
gamma
```

### `head`

查看前几行。

```bash
$ head -n 2 demo/a/file2.txt
alpha
beta
```

### `tail`

查看后几行。

```bash
$ tail -n 1 demo/a/file2.txt
gamma
```

### `tail -f`

适合持续查看日志文件。

---

## 5. 文本搜索

### `grep`

搜索指定内容。

```bash
$ grep -n 'beta' demo/a/file2.txt
2:beta
```

### `find`

按条件查找文件。

```bash
$ find demo -type f | sort
demo/a/file1.txt
demo/a/file2.txt
demo/a/file3-renamed.txt
```

---

## 6. 权限管理

### `chmod`

修改文件权限。

```bash
$ chmod 755 run.sh
$ ls -l run.sh
-rwxr-xr-x 1 a3165 a3165 8 Apr 21 10:34 run.sh
```

### `chown`

修改文件所有者和所属组。

```bash
$ chown user:group test.txt
```

---

## 7. 进程管理

### `ps`

查看当前进程。

```bash
$ ps aux | head -n 5
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.1  0.0  21760 12140 ?        Ss   10:24   0:00 /sbin/init
root         2  0.0  0.0   3120  1920 ?        Sl   10:24   0:00 /init
root        10  0.0  0.0   3164  1968 ?        Sl   10:24   0:00 plan9 --control-socket 7 --log-level 4 --server-fd 8 --pipe-fd 10 --log-truncate
root        46  0.0  0.1  66816 18656 ?        S<s  10:24   0:00 /usr/lib/systemd/systemd-journald
```

### `top`

实时查看系统资源和进程占用。

```bash
$ top -b -n 1 | head -n 10
top - 10:34:37 up 9 min,  2 users,  load average: 0.09, 0.10, 0.08
Tasks:  61 total,   1 running,  60 sleeping,   0 stopped,   0 zombie
%Cpu(s):  1.5 us,  2.3 sy,  3.1 ni, 90.8 id,  0.8 wa,  0.0 hi,  1.5 si,  0.0 st 
MiB Mem :  15963.2 total,  11107.6 free,   1654.5 used,   3448.5 buff/cache     
MiB Swap:   4096.0 total,   4096.0 free,      0.0 used.  14308.7 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
    1 root      20   0   21760  12140   9068 S   0.0   0.1   0:00.64 systemd
    2 root      20   0    3120   1920   1920 S   0.0   0.0   0:00.00 init-syst+
   10 root      20   0    3164   1968   1920 S   0.0   0.0   0:00.08 init
```

### `kill`

结束进程。

```bash
$ kill 1234
$ kill -9 1234
```

---

## 8. 网络排查

### `ss`

查看端口监听状态。

```bash
$ ss -lnt | head -n 5
State  Recv-Q Send-Q Local Address:Port  Peer Address:PortProcess
LISTEN 0      4096   127.0.0.53%lo:53         0.0.0.0:*
LISTEN 0      511        127.0.0.1:46451      0.0.0.0:*
LISTEN 0      4096      127.0.0.54:53         0.0.0.0:*
```

### `curl`

请求 HTTP 接口并查看返回。

```bash
$ curl -I http://127.0.0.1:1
HTTP/1.1 502 Bad Gateway
Content-Length: 0
```

### `curl -I`

查看响应头。

```bash
$ curl -I http://127.0.0.1:1
HTTP/1.1 502 Bad Gateway
Content-Length: 0
```

### `ping`

测试网络连通性。

```bash
$ ping -c 1 127.0.0.1
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.022 ms

--- 127.0.0.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.022/0.022/0.022/0.000 ms
```

---

## 9. 磁盘与内存

### `df`

查看磁盘使用情况。

```bash
$ df -h | head -n 5
Filesystem                                Size  Used Avail Use% Mounted on
none                                      7.8G     0  7.8G   0% /usr/lib/modules/6.6.87.2-microsoft-standard-WSL2
none                                      7.8G  4.0K  7.8G   1% /mnt/wsl
drivers                                   450G  312G  138G  70% /usr/lib/wsl/drivers
/dev/sdd                                 1007G   53G  904G   6% /
```

### `du`

查看目录占用大小。

```bash
$ du -sh /home/a3165/studynotes
212K	/home/a3165/studynotes
```

### `free`

查看内存情况。

```bash
$ free -h | head -n 5
               total        used        free      shared  buff/cache   available
Mem:            15Gi       1.6Gi        10Gi       4.5Mi       3.4Gi        13Gi
Swap:          4.0Gi          0B       4.0Gi
```

---

## 10. 压缩与归档

### `tar`

打包或解包文件。

```bash
$ tar -czvf pkg.tar.gz pkg
```

查看归档内容：

```bash
$ tar -tzvf pkg.tar.gz
drwxr-xr-x a3165/a3165       0 2026-04-21 10:34 pkg/
drwxr-xr-x a3165/a3165       0 2026-04-21 10:34 pkg/inner/
-rw-r--r-- a3165/a3165      12 2026-04-21 10:34 pkg/inner/readme.txt
```

---

## 11. 命令路径

### `which`

查看命令位置。

```bash
$ which zsh
/usr/bin/zsh
$ which curl
/usr/bin/curl
$ which tar
/usr/bin/tar
```

---

## 12. 小结

Linux 基础命令的学习重点不是背参数，而是能够在实际场景中完成以下操作：

- 找到当前目录
- 看懂目录结构
- 创建、复制、移动、删除文件
- 查看文件内容和日志
- 查找文本
- 修改权限
- 查看进程和端口
- 判断磁盘和内存状态
- 打包和解包文件
- 确认命令所在路径

如果进一步用于实习准备，重点应当放在“命令执行后如何验证结果”和“排障顺序如何形成”上。
