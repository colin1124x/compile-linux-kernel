# 編譯工作環境

## Fedora

[http://fedoraproject.org/zh_TW/](http://fedoraproject.org/zh_TW/)

## 編譯工具

使用 yum install package.name 安裝

- `hmaccalc` 用來處理 HMAC (hash-based message authentication code)
- `xmlto` 主要用途是用任何手段將XML檔轉換成另外一種目的格式
- `asciidoc` 用來寫文件,如man page
- `elfutils-devel`
- `perl-ExtUtils-Embed` 將perl 嵌入 C/C++ 應用程序
- `gcc` 
- `rpm-build`
    - `zlib-devel`
    - `binutils-devel`
    - `newt-devel`
    - `python-devel`
    - `bison` 上下文無關語法剖析器
    - `audit-libs-devel`
    - `pciutils-devel` 處理PCI
    - `ncurses-devel`
- `pesign` make menuconfig 時用作繪畫文字視窗的程式庫

### rpmbuild 說明
- 建立目錄
    - BUILD 放置rpmbuild 建立的軟體檔案
    - RPMS 放置2進位檔
    - SOURCE 放置原始檔
    - SPECS 放置每個要建立的 RPM spec檔
    - SRPMS 
- `rpmbuild --showrc` 查看內部變數
- `vim xxx.spec` 會自動產生該填寫的變數欄位
- spec檔內常用變數
    - `RPM_BUILD_DIR` /$HOME/rpmbuild/BUILD
    - `RPM_BUILD_ROOT` /$HOME/rpmbuild/BUILDROOT
    - `%{_sysconfdir}` /etc
    - `%{_sbindir}` /usr/sbin
    - `%{_bindir}` /usr/bin
    - `%{_datadir}` /usr/share
    - `%{_mandir}` /usr/share/man
    - `%{_libdir}` /usr/lib64
    - `%{_prefix}` /usr
    - `%{_localstatedir}` /usr/var
    
- spec檔內的腳本鉤子
    - `%prep` 預處理腳本
    - `%setup`
    - `%build` 編譯連接腳本
    - `make`
    - `%install` 安裝腳本程序
    - `make install`
    - `%clean` 清理腳本
    - `%pre` 安裝前
    - `%post` 安裝後
    - `%preun` 卸載前
    - `%postun` 卸載後
    - `%verifyscript` 驗證腳本
    - `%triggerin`
    - `%triggerun`
    - `%triggerpostun`
    
## 編譯步驟

使用 yumdownloader 下載核心原始碼
```sh
$ yumdownloader --source kernel
```

```sh
$ sudo yum install mock
$ sudo useradd mockbuild
```

解壓縮與套用更新檔
```sh
# -i|--install
# -v Print verbose information
# -h|--hash 用50個#作為解壓縮進度顯示
$ rpm -ivh kernel-xxxx.src.rpm

# -b if a spec file is being used to build the package
# -bp Executes the "%prep" stage from the spec file. Normally this involves unpacking the sources and applying any patches.
$ rpmbuild -bp rpmbuild/SPECS/kernel.spec
```

核心設定與編譯
```sh
$ cd rpmbuild/BUILD/kernel-xxxxx/linux-xxxxxx/

# 操作說明 
# <Y> includes, <N> excludes, <M> modularizes features
# <Esc><Esc> exit, <?> for Help, </> for Search
$ make menuconfig

# 在 RPMS/x86_64/ 下產生kernel-xxxx-rpm檔 
# 注意,有可能會出現 No space left on device (inode用盡)
# 使用指令 sysctl kernel.msgmni  查看inode數
# 使用指令 sudo sysctl -w kernel.msgmni=xxx 重新設定
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
- [Linux Rpmbuild 包制作](http://kling.blog.51cto.com/3320545/1239571)
- [fedora Packaging:ScriptletSnippets](http://fedoraproject.org/wiki/Packaging:ScriptletSnippets)
