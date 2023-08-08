# Archlinux And Kde
## 安装Archlinux和kde桌面
略
## 切换国内源
```
reflector -c china -p https -l 10 --sort rate --save /etc/pacman.d/mirrorlist
```
## 安装Discover后台程序
```
sudo pacman -S packagekit-qt5
```
## 安装yay帮助程序
```
# 添加archlinuxcn源，文件位置： /etc/pacman.conf，在最后添加
[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
# 安装archlinuxcn证书
sudo pacman -Sy archlinuxcn-keyring
# 安装yay
sudo pacman -S yay
```
## 安装yakuake
```
sudo pacman -S yakuake
```
## 安装open-vm-tools
```
# 安装open-vm-tools
sudo pacman -S open-vm-tools
# 启动服务
sudo systemctl start vmtoolsd.service
sudo systemctl start vmware-vmblock-fuse.service
# 设置开机启动
sudo systemctl enable vmtoolsd.service
sudo systemctl enable vmware-vmblock-fuse.service
# 查看服务状态
sudo systemctl status vmtoolsd.service
sudo systemctl status vmware-vmblock-fuse.service
# 编辑文件/etc/mkinitcpio.conf
MODULES=(vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx)
# 编辑文件后执行命令
sudo mkinitcpio -p linux
# 如果文件（/etc/xdg/autostart/vmware-user.desktop）不存在
cp /etc/vmware-tools/vmware-user.desktop /etc/xdg/autostart/vmware-user.desktop
# 重启系统
```
# 虚拟机和物理机相互复制
```
sudo pacman -S gtkmm gtkmm3 gtk2
```
## 安装chrome
```
yay -S google-chrome
```
## 解决中文乱码
```
# 编辑文件 /etc/locale.gen 解除注释
zh_CN.GB18030 GB18030
zh_CN.GBK GBK
zh_CN.UTF-8 UTF-8
# 生成语言包
sudo locale-gen
# 安装支持中文的字体，任选其一
sudo pacman -S wqy-zenhei 
sudo pacman -S ttf-ubraille
sudo pacman -S ttf-symbola
sudo pacman -S texlive-core
sudo pacman -S noto-fonts-emoji
sudo pacman -S ttf-cm-unicode
sudo pacman -S otf-latin-modern
sudo pacman -S otf-xits
sudo pacman -S ttf-joypixels
sudo pacman -S ttf-twemoji-color
sudo pacman -S adobe-source-han-sans-otc-fonts
sudo pacman -S adobe-source-han-serif-otc-fonts
sudo pacman -S noto-fonts-cjk
sudo pacman -S wqy-microhei
sudo pacman -S wqy-microhei-lite
sudo pacman -S ttf-i.bming
sudo pacman -S adobe-source-han-serif-cn-fonts
sudo pacman -S adobe-source-han-serif-tw-fonts
sudo pacman -S adobe-source-han-sans-cn-fonts
sudo pacman -S adobe-source-han-sans-tw-fonts
sudo pacman -S noto-fonts-sc
sudo pacman -S noto-fonts-tc
sudo pacman -S wqy-zenhei
sudo pacman -S wqy-bitmapfont
sudo pacman -S ttf-arphic-ukai
sudo pacman -S ttf-arphic-uming
sudo pacman -S opendesktop-fonts
sudo pacman -S ttf-hannom
sudo pacman -S ttf-tw
sudo pacman -S ttf-twcns-fonts
sudo pacman -S ttf-ms-win8-zh_cn
sudo pacman -S ttf-ms-win8-zh_tw
sudo pacman -S ttf-ms-win10-zh_cn
sudo pacman -S ttf-ms-win10-zh_tw
sudo pacman -S fonts-cjk
sudo pacman -S fonts-cjk-sc-yrdzst
```
## 安装中文输入法
```
sudo pacman -S fcitx5-im fcitx5-chinese-addons fcitx5-rime fcitx5-configtool
# 编辑文件/etc/environment
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
```