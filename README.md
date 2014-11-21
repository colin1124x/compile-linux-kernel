# 編譯工作環境

## Fedora

[http://fedoraproject.org/zh_TW/](http://fedoraproject.org/zh_TW/)

## 編譯工具

- `hmaccalc` 用來處理 HMAC (hash-based message authentication code) [git](https://git.fedorahosted.org/cgit/hmaccalc.git)
- `xmlto` 主要用途是用任何手段將XML檔轉換成另外一種目的格式 [source](https://fedorahosted.org/xmlto/browser)
- `asciidoc` 用來寫文件,如man page
- `elfutils-devel` [git](http://git.fedorahosted.org/git/elfutils.git)
- `perl-ExtUtils-Embed` 將perl 嵌入 C/C++ 應用程序 [source](http://files1.directadmin.com/services/all/perl_modules/)1997年後沒任何修改
- `gcc` 
- `rpm-build`
    - `zlib-devel`
    - binutils-devel
    - newt-devel
    - python-devel
    - bison
    - audit-libs-devel
    - pciutils-devel
    - pesign //make menuconfig 時用作繪畫文字視窗的程式庫
    - ncurses-devel
    
## 編譯步驟

使用 yumdownloader 下載核心原始碼
```sh
$ yumdownloader --source kernel
```

```sh
$ rpm -ivh kernel-xxxx.src.rpm
```

解壓縮與套用更新檔
```sh
$ rpmbuild -bp rpmbuild/SPECS.kernel.spec
```

核心設定與編譯
```sh
$ cd rpmbuild/BUILD/kernel-xxxxx/linux-xxxxxx/
$ make menuconfig
$ make rpm
```

安裝與移除
```sh
$ rpm -ivh rpmbuild/RPMS/x86_64/kernel-xxxx.rpm 
$ sudo rpm -e kernel-xxxx
```


-------------------------------
#### 參考出處
- [linux-重編系統核心](http://darkranger.no-ip.org/content/how-to%EF%BC%9Alinux-%E9%87%8D%E7%B7%A8%E7%B3%BB%E7%B5%B1%E6%A0%B8%E5%BF%83)
- [編譯 Linux 核心](http://wiki.debian.org.hk/w/Compile_Linux_kernel)