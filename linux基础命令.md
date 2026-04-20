# linux的基础命令

## 文件操作

### 1. pwd - Print Working Directory
显示当前命令行进程的工作目录的绝对路径
```bash
➜  ~ pwd
/home/a3165
```


### 2. ls - List
列出目录的 索引节点（inode） 内容及元数据
```bash
➜  nano-vllm git:(main) ls
LICENSE  README.md  assets  bench.py  example.py  nanovllm  pyproject.toml
```

#### `ls -l` (Long format)：

显示文件的详细属性，包括 权限位（Permissions）、硬链接数、所有者（Owner）、所属组（Group）、文件大小及最后修改时间（mtime）。

```bash
➜  nano-vllm git:(main) ls -l
total 28
-rw-r--r-- 1 a3165 a3165 1067 Apr 20 23:47 LICENSE
-rw-r--r-- 1 a3165 a3165 2185 Apr 20 23:47 README.md
drwxr-xr-x 2 a3165 a3165 4096 Apr 20 23:47 assets
-rw-r--r-- 1 a3165 a3165 1121 Apr 20 23:47 bench.py
-rw-r--r-- 1 a3165 a3165  916 Apr 20 23:47 example.py
drwxr-xr-x 6 a3165 a3165 4096 Apr 20 23:47 nanovllm
-rw-r--r-- 1 a3165 a3165  598 Apr 20 23:47 pyproject.toml
```

`ls -l`  默认不显示`.`开头的隐藏文件，如需显示隐藏文件，应使用`ls -la`

```bash
➜  nano-vllm git:(main) ls -la
total 48
drwxr-xr-x  5 a3165 a3165 4096 Apr 20 23:47 .
drwxr-x--- 51 a3165 a3165 4096 Apr 20 23:53 ..
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

推荐使用`ls -lah`表示人类可读
```bash
➜  nano-vllm git:(main) ls -lah
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

#### `ls -i` (inode)：
显示文件在磁盘上的唯一标识符 inode 编号。
```bash
➜  nano-vllm git:(main) ls -i
433379 LICENSE    433381 assets    433384 example.py  433410 pyproject.toml
433380 README.md  433383 bench.py  433385 nanovllm
``` 
- `ls -d` (Directory)：仅列出目录本身的信息，而非其子内容。