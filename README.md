# 編譯工作環境

## Fedora

[http://fedoraproject.org/zh_TW/](http://fedoraproject.org/zh_TW/)

## 編譯工具

- hmaccalc
- xmlto
- asciidoc
- elfutils-devel
- perl-ExtUtils-Embed
- gcc
- rpm-build
    - zlib-devel
    - binutils-devel
    - newt-devel
    - python-devel
    - bison
    - audit-libs-devel
    - pciutils-devel
    - pesign
    
## 編譯步驟

1. 使用 yumdownloader 下載核心原始碼
```
$ yumdownloader --source kernel
```

2. 
```
$ rpm -ivh kernel-xxxx.src.rpm
```

3. 解壓縮與套用更新檔
```
$ rpmbuild -bp rpmbuild/SPECS.kernel.spec
```

4. 核心設定與編譯
```
$ cd rpmbuild/BUILD/kernel-xxxxx/linux-xxxxxx/
$ make menuconfig
$ make rpm
```

5. 安裝與移除
```
$ rpm -ivh rpmbuild/RPMS/x86_64/kernel-xxxx.rpm 
$ sudo rpm -e kernel-xxxx
```


