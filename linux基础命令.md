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
### 3.1 `mkdir`

创建目录。

```bash
$ mkdir demo
$ mkdir -p demo/a/b
```

- `-p`：递归创建多级目录
- 父目录不存在时，自动创建完整路径

常见场景：

- 创建项目目录
- 创建日志目录
- 创建临时测试目录

### 3.2 `touch`

创建空文件，或更新文件时间戳。

```bash
$ touch demo/a/file1.txt
```

```bash
$ touch -t 202612251200.00 document.txt
```

- `-t`：手动指定修改时间
- 常用于测试定时任务、备份任务、文件监听逻辑

### 3.3 `cp`

复制文件或目录。

```bash
$ cp demo/a/file2.txt demo/backup/
$ cp demo/a/file2.txt demo/backup/file3.txt
```

第一种写法表示复制到目标目录，文件名保持不变。  
第二种写法表示复制到目标路径，并使用新文件名。

递归复制目录时使用 `-r`。

```bash
$ cp -r nginx nginx-copy
```

归档式复制使用 `-a`。

```bash
$ cp -a nginx nginx-archive
```

- `-r`：递归复制目录
- `-a`：尽量保留原始属性，包括权限、时间戳、链接等

常见使用场景：

- 备份配置文件
- 复制代码目录
- 保留目录结构迁移文件

### 3.4 `mv`

移动文件或重命名文件。

```bash
$ mv demo/a/file3.txt demo/a/file3-renamed.txt
```

常见使用场景：

- 文件重命名
- 目录迁移
- 临时文件整理

### 3.5 `rm`

删除文件或目录。

```bash
$ rm demo/x/delete.txt
$ rm -r demo/x
```

- `-r`：递归删除目录
- `-f`：强制删除，不提示确认

删除命令属于高风险命令，执行前需要再次确认目标路径。

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

- 适合查看小文件
- 如果文件较大，通常改用 `less`、`head` 或 `tail`

### `head`

查看前几行。

```bash
$ head -n 2 demo/a/file2.txt
alpha
beta
```

- 默认输出前 10 行
- `-n` 可以指定行数

### `tail`

查看后几行。

```bash
$ tail -n 1 demo/a/file2.txt
gamma
```

- 默认输出最后 10 行
- 常用于查看日志文件末尾内容
- `-f` 可以持续跟踪新增内容

### `tail -f`

适合持续查看日志文件。

```bash
$ tail -f app.log
```

- 适合观察运行中的日志输出
- 常用于调试接口、服务启动和报错信息

---

## 5. 文本搜索

### `grep`

搜索指定内容。

```bash
$ grep -n 'beta' demo/a/file2.txt
2:beta
```

- `-n`：显示行号
- `-i`：忽略大小写
- `-r`：递归搜索目录
- `-v`：反向匹配

常见场景：

- 从日志中找错误关键词
- 从配置文件中找某个变量
- 从代码里找某个函数名

### `find`

按条件查找文件。

```bash
$ find demo -type f | sort
demo/a/file1.txt
demo/a/file2.txt
demo/a/file3-renamed.txt
```

- `-name`：按文件名查找
- `-type f`：查找普通文件
- `-type d`：查找目录
- `-maxdepth`：限制搜索层级

示例：

```bash
$ find . -name "*.log"
$ find /var/log -type f
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

- `644`：常见普通文件权限
- `755`：常见脚本文件权限
- `chmod +x`：添加可执行权限

常见写法：

```bash
$ chmod 644 config.yaml
$ chmod 755 start.sh
$ chmod +x start.sh
```

### `chown`

修改文件所有者和所属组。

```bash
$ chown user:group test.txt
```

- 用于切换文件所有者
- 常见于部署、数据目录和服务账号场景

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

- `ps aux`：常见写法，显示所有进程
- `ps -ef`：另一种常用格式
- `head -n 5`：只看前几行，避免输出过长

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

- `top` 适合快速查看 CPU、内存、负载
- 常用于排查机器卡顿、服务占用高、系统资源异常

### `kill`

结束进程。

```bash
$ kill 1234
$ kill -9 1234
```

- `kill`：发送终止信号
- `kill -9`：强制结束
- 优先使用普通 `kill`，无效时再考虑 `-9`

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

- `-l`：只看监听状态
- `-n`：数字形式显示
- `-t`：TCP
- `-p`：显示进程信息

常见用途：

- 查看服务是否真的监听端口
- 判断端口是否被占用

### `curl`

请求 HTTP 接口并查看返回。

```bash
$ curl -I http://127.0.0.1:1
HTTP/1.1 502 Bad Gateway
Content-Length: 0
```

- `-I`：只查看响应头
- 常用于验证接口连通性
- 也可以配合 `-v` 看详细请求过程

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

- `ping` 适合检查网络是否可达
- 常用于先判断主机层面连通性

---

## 9. 磁盘与内存

### `df`

查看磁盘使用情况。

```bash
$ df -h
```

- `-h`：以人类可读单位显示
- 常用于判断磁盘是否快满

### `du`

查看目录或文件占用大小。

```bash
$ du -sh /home/a3165/studynotes
```

- `-s`：只显示总大小
- `-h`：以人类可读单位显示

### `free`

查看内存使用情况。

```bash
$ free -h
```

- 常用于判断系统内存是否紧张
- 也可结合 `top` 一起看

---

## 10. 压缩与归档

### `tar`

打包或解包文件。

```bash
$ tar -czvf pkg.tar.gz pkg
$ tar -xzvf pkg.tar.gz
```

- `-c`：创建归档
- `-x`：解包
- `-z`：使用 gzip
- `-v`：显示过程
- `-f`：指定文件名

常见场景：

- 打包代码目录
- 备份配置文件
- 传输服务文件

---

## 11. 实用补充

### `which`

查看命令所在路径。

```bash
$ which zsh
$ which curl
$ which tar
```

### `history`

查看历史命令。

```bash
$ history
```

### `clear`

清屏。

```bash
$ clear
```

---

## 12. 小结

Linux 基础命令的重点不在于死记参数，而在于能够快速完成以下事情：

- 创建和管理文件
- 查看文件内容
- 搜索文本
- 管理权限
- 查看进程
- 判断端口和网络
- 查看磁盘和内存
- 打包和解包文件

后续学习中，建议把这些命令和排障场景结合起来理解，而不是单独背诵。
