Week 2: Files, Directories & Editors 
📂 Key Topics Covered

Important directories:
/etc → configuration files
/bin → binaries/commands for normal users
/sbin → system binaries for root
/home → user home directories
/root → root user’s home directory (restricted)
/var → logs, ftp, webserver files (sticky bit: 1777)
/tmp → temp files (world writable, sticky bit)
/proc → kernel-related info (virtual, size=0)

Basic commands: cp, mv, mkdir, rm, rmdir

Vim editor:
Create file: vim file.txt → i → write → Esc :wq
Copy & paste (yank): yy + p
Search word: /word
Global replace: :%s/old/new/g
Split screen: vim -o f1 f2

Redirection:
cal | head -n 2 > f1 → redirect stdout (overwrite/create)
echo "Hello" >> f1 → append
ls 2> f1 → redirect stderr
random 2> /dev/null → discard stderr
(echo "hi"; cat nofile) &> result.txt → combine stdout+stderr

Search tools:
find . -name a123 → search in dir hierarchy
locate myfile → search prebuilt index

Links:
Hard link → same inode, files only, can’t cross FS → ln file new_hard
Soft link → new inode, stores path, works across FS → ln -s original symlink

Compression tools:
gzip - Fast compression, widely used for .gz files.
Commands:
gzip file → compress a file (file → file.gz)
zcat file.gz → read contents without extracting
gunzip file.gz → decompress

bzip2 - Slower than gzip, but better compression ratio. Produces .bz2 files.
Commands:
bzip2 file → compress a file (file → file.bz2)
bzcat file.bz2 → read contents without extracting
bunzip2 file.bz2 → decompress

xz - Very high compression ratio, often better than bzip2, but slowest. Produces .xz files.
Commands:
xz file → compress a file (file → file.xz)
xzcat file.xz → read contents without extracting
unxz file.xz → decompress

Remote copying:
rsync -av user@server:/path /dest → incremental, fast
scp file user@server:/dest → secure copy (no incremental)
