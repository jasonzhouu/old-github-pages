---
layout: post
title: '命令行工具的配置'
---

Mac上默认的shell是bash，并自带vim，自带终端工具terminal。

shell负责接收用户命令，比如`git add .`，然后调用相应的应用程序，它是我们控制操作系统的接口。terminal是shell的包装程序，引用[What is the difference between shell, console, and terminal?](http://superuser.com/questions/144666/what-is-the-difference-between-shell-console-and-terminal)的回答：

> The **shell** is the program which actually processes commands and returns output. Most shells also manage foreground and background processes, command history and command line editing. These features (and many more) are standard in `bash`, the most common shell in modern linux systems.
>
> A **terminal** refers to a wrapper program which runs a shell. Decades ago, this was a physical device consisting of little more than a monitor and keyboard. As unix/linux systems added better multiprocessing and windowing systems, this terminal concept was abstracted into software. Now you have programs such as [Gnome Terminal](http://directory.fsf.org/project/gnome-terminal/) which launches a window in a Gnome windowing environment which will run a *shell* into which you can enter commands.

## zsh

但是有人开发出了zsh，zsh拥有强大的自动补全功能，而且有大量的插件支持。安装[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)后会安装好很多插件，~/.zshrc的plugin参数用于管理这些插件，ZSH_THEME参数用于管理界面主题，oh-my-zsh[自带了很多主题](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)，默认的主题是robbyrussell，这个主题我用了很长时间。

另外我尝试了agnoster, [powerline](http://powerline.readthedocs.io/en/latest/index.html), [powerlevel9k](https://github.com/bhilburn/powerlevel9k)，这三种主题很类似，它的命令行有很多提示，而且命令行因为有彩色背景，辨识度很高，robbyrussell主题则容易使命令行和输出结果混在一起，命令多的时候让人很难分辨输出结果对应的是哪一条命令行。agnoster是oh-my-zsh自带的，将ZSH_THEME参数设置为agnoster就可以，另外两种需要下载到~/.oh-my-zsh/themes目录，然后也同样需要设置ZSH_THEME参数。经过比较，最后我选择了agnoster主题，如下配图所示。

![]({{ site.ur }}/images/Snip20170208_1.png)

这三种主题需要终端工具安装特定的字体，我用的是Meslo LG M DZ Regular for Powerline，他可以正确的显示powerline上特殊的符号。

最后还需要将终端工具的显示颜色设置一下，以便让洁面显示效果更清晰，[Solarized Dark colorscheme](http://ethanschoonover.com/solarized)是很受欢迎的一种颜色搭配。

界面颜色和字体是在终端工具的preference里设置，将在Solarized官网下载文件，在preference里倒入相应版本的配置文件，之后可以自己对颜色进行调整；字体也是先下载Meslo字体，打开字体文件，点击安装，然后在终端工具的preference里选择Meslo。我用Mac自带的terminal和另外安装的iTerm都设置了一下，iTerm的显示效果更好。

BTW：shelll和终端工具是分离的，我在iTerm上安装了zsh，terminal上的命令行工具也会由默认的bash变成zsh。在iTerm上安装oh-my-zsh，terminal也能用oh-my-zsh上的插件。但是终端工具的显示颜色和字体是需要在各自的preference里设置的。


## vim

vim由当初Unix系统上的vi发展而来，vim的最大特点是跨终端，mac, windows, linux系统上都能运行，而且非常稳定。配置云服务器的时候，少不了要用到。

vim也有很多插件和主题，[spf13-vim](http://vim.spf13.com/)将很多受欢迎的插件和主题集成在了一起，安装好之后，可以直接通过～/.vimrc.local的colorscheme参数设置主题，最常见的solarized, onedark都有，但是solarized在mac上有点问题。

spf13-vim带有vundle插件，vundle是vim的插件管理工具，相当于node的npm，可以用它下载最新版本的vim插件，和用来升级插件。

spf13-vim安装的插件具有比如以下一些功能：

- 自动补全功能，编辑html的标签，也能像atom/sublime一样自动补全了，比如输入h2然后按Tab键就能自动生成`<h2></h2>`，而且支持很多种语言。
- 可以用鼠标控制光标的位置，默认的vim只能用上下左右键控制。
- indent（锯齿），可以直观地分辨初始标签对应的结束标签。

和atom/sublime一样，vim的快捷键也非常。但不同的是，vim的大多数操作只能用快捷键完成。这两种IDE的学习成本都很高，要同时掌握必然需要很多时间，我目前而言只需要掌握好atom就行了，atom的功能也是很强大的，我现在还没有熟练掌握。atom和sublime差不多，但atom好像更好用一些，就是启动稍微慢一点，而vim等以后有精力或者有需要再学习，否则可能两种都学不成。

BTW：vim和zsh一样，在iTerm上安装好之后，terminal上也能用。

![]({{ site.ur }}/images/Snip20170208_2.png)