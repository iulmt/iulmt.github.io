# 安装Archlinux
```
# 切换源
reflector -c china -p https -l 10 --sort rate --save /etc/pacman.d/mirrorlist
# 开始安装
archinstall
```
# 安装必要的程序
```bash
# 编辑器
sudo pacman -S neovim
# 文件管理器
sudo pacman -S ranger
# 添加archlinuxcn源，文件位置： /etc/pacman.conf，在最后添加
[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
# 安装archlinuxcn证书
sudo pacman -Sy archlinuxcn-keyring
# 安装yay
sudo pacman -S yay
# 安装chrome
yay -S google-chrome
```
# 安装显示管理器（登录界面程序）
略
# 安装qtile窗口管理器
```python
sudo pacman -S xorg
# 安装qtile窗口管理器，安装lightdm显示管理器，
# 安装kitty终端，安装lightdm主题lightdm-webkit-theme-litarvan
sudo pacman -S qtile lightdm lightdm-gtk-greeter lightdm-webkit-theme-litarvan kitty
# 显示管理器开启服务自启动
sudo systemctl enable lightdm
# 编辑/etc/lightdm/lightdm.conf文件
[Seat:]
greeter-session=lightdm-webkit2-greeter
# 编辑/etc/lightdm/lightdm-webkit2-greeter.conf
[greeter]
webkit_theme        = litarvan
# 重启
```
# 安装open-vm-tools
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
# 时间同步
sudo vmware-toolbox-cmd timesync enable
# 窗口分辨率自动适配
sudo pacman -S xf86-video-vmware gtkmm gtkmm3 gtk2
# 编辑文件/etc/mkinitcpio.conf
MODULES=(vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx)
# 编辑文件后执行命令
sudo mkinitcpio -p linux
# 如果文件（/etc/xdg/autostart/vmware-user.desktop）不存在
cp /etc/vmware-tools/vmware-user.desktop /etc/xdg/autostart/vmware-user.desktop
# 重启系统
```
# 安装zsh
```
sudo pacman -S zsh
# 安装oh-my-zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# 安装插件
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# 编辑文件 /home/[user]/.zshrc
plugins=(git zsh-syntax-highlighting zsh-autosuggestions)
# 应用修改
source ~/.zshrc
```
# 安装rofi
```
yay -S rofi
# 编辑文件,添加快捷键 /home/[user]/.config/qtile/config.py
Key(["mod1"], "space", lazy.spawn("rofi -show drun"), desc="Launch Rofi")
# 重启
```
# 解决中文乱码
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
# 安装中文输入法
```
sudo pacman -S fcitx5-im fcitx5-chinese-addons fcitx5-rime
# 编辑文件/etc/environment
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
# 编辑文件 ~/.config/qitle/config.py
import os, subprocess

@hook.subscribe.startup_once
def autostart():
    home = os.path.expanduser("~")
    cmds = [home+"/.config/qtile/autorun.sh"]
    subprocess.call(cmds)
```
# 安装文件管理器
```
yay -S dolphin
```
# 安装图标主题
```
yay -S papirus-icon-theme
```
# 安装nvidia驱动
[看文章](https://www.littlezhang.com/2021/09/arch-linux-%E5%AE%89%E8%A3%85-nvidia-%E4%B8%93%E6%9C%89%E9%A9%B1%E5%8A%A8/)
```
sudo pamcan -S nvidia-dkms nvidia-prime
# 查看驱动是否安装成功
prime-run glxinfo | grep OpenGL
```
# 修复Discover不能正常使用的问题
```
sudo pacman -S packagekit-qt5
```
# pycharm激活
```
https://33tool.com/idea/
```