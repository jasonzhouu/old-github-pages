---
layout: post
title: '命令行工具的配置'
---

Mac上默认的命令行工具是bash，自带vim。

## zsh

但是有人开发出了zsh，zsh拥有强大的自动补全功能，而且有大量的插件支持。安装[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)后会安装好很多插件，通过~/.zshrc的plugin参数用于管理这些插件，ZSH_THEME参数用于管理界面主题，oh-my-zsh[自带了很多主题](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)，默认的主题是robbyrussell，这个主题我用了很长时间。另外我尝试了的agnoster, [powerline](http://powerline.readthedocs.io/en/latest/index.html), [powerlevel9k](https://github.com/bhilburn/powerlevel9k)，这三种主题很类似，它们给终端的界面提供了很多提示。agnoster是oh-my-zsh自带的，将ZSH_THEME参数设置为agnoster就可以，另外两种需要下载到themes目录，然后也同样的需要设置ZSH_THEME参数。

这三种主题需要终端工具安装特定的字体，我用的是Meslo LG M DZ Regular for Powerline，他可以正确的显示powerline上特殊的符号。

最后还需要将终端工具的显示颜色设置一下，以便让洁面显示效果更清晰，[Solarized Dark colorscheme](http://ethanschoonover.com/solarized)是很受欢迎的一种颜色搭配。

界面颜色和字体是在终端工具的preference里设置，将在Solarized官网下载文件，在preference里倒入相应版本的配置文件，之后可以自己对颜色进行调整；字体也是先下载Meslo字体，打开字体文件，点击安装，然后在终端工具的preference里选择Meslo。我用Mac自带的terminal和另外安装的iTerm都设置了一下，iTerm的显示效果更好。

BTW, 命令行工具和终端工具是分离的，我在iTerm上安装zsh的同时，打开terminal用的也会是zsh。在iTerm上安装oh-my-zsh，terminal也一样能用它oh-my-zsh上的插件。但是终端工具的显示颜色和字体是需要在各自的preference里设置的。

![]({{ site.ur }}/images/Snip20170208_1.png)

## vim

vim由当初Unix系统上的vi发展而来，vim的最大特点是跨终端，mac, windows, linux系统上都能运行，而且非常稳定。配置云服务器的时候，少不了要用到。

vim也有很多插件和主题，[spf13-vim](http://vim.spf13.com/)将很多受欢迎的插件和主题集成在了一起，安装好之后，可以直接通过～/.vimrc.local的colorscheme参数设置主题，最常见的solarized, onedark都有，但是solarized在mac上有点问题。spf13-vim带有vundle插件，vundle是vim的插件管理工具，相当于node的npm，可以用它下载最新版本的vim插件，和用来升级插件。

![]({{ site.ur }}/images/Snip20170208_2.png)