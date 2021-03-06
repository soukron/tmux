# Tmux Environment

### Overview
This is my personal tmux configuration after a while using this manager.

It includes:
 - mouse integration to select/resize panes and text selection
 - status bar with hostname, system information and date (see Dependencies below)
 - xclip integration (see Dependencies below)
 - start numbering windows at 1 instead of 0
 - vi mode enabled
 - keybinds to:
   - split window h**o**rizontally (C-b o) in addition to default (C-b ")
   - split window v**e**rtically (C-b e) in addition to default (C-b %)
   - reload configuration file (C-b r)
   - automatically start a SSH connection (C-b R)
   - turn on/off pane synchronization (C-b S and C-b s respectively)
   - start text selection like in vi (v key when in copy-mode)
   - copy text selection to system clipboard (y key after begin-selection)
   - send prefix key to a nested tmux session (C-a) instead of (C-b C-b)
   
Also I include a launcher ([tmx]) which starts (or resumes if possible) a session based in a given name.

### Dependencies
Install **[tmux]** 2.2+:

```sh
$ sudo yum install tmux
```
Download, compile and install [tmux-mem-cpu-load] from Matt McCormick.

If you want to integrate [tmux] buffers with your system clipboard, install **xclip** package (and remove the comment in line #17 in __.tmux.conf__):
```sh
$ sudo yum install xclip
```

### Installation
Get the source code:

```sh
$ cd ~
$ git clone https://github.com/soukron/tmux.git
```
Copy (or symlink) the files:

```sh
$ ln -s ~/tmux/.tmux.conf ~/.tmux.conf
$ sudo ln -s ~/tmux/tmx /usr/local/bin/tmx
```

### Configuration
To get the pane title updated, add this code to your __.bashrc__, in all servers you connect:

```sh
if [ $TERM == "xterm" ] && [ $COLORTERM == "gnome-terminal" ]; 
then
        echo hello $TERM $COLORTERM
        export TERM=xterm-256color
fi
case $TERM in
    xterm*|rxvt)
        PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME}\007"'
        export PROMPT_COMMAND
        ;;
    screen)
        TITLE=$(hostname -s)                                                      
        PROMPT_COMMAND='/bin/echo -ne "\033k${TITLE}\033\\"'                      
        export PROMPT_COMMAND
        ;;
esac
```

### Contact
Reach me in [Twitter] or email in soukron _at_ gmbros.net

### References
 - http://tmux.sourceforge.net
 - https://github.com/thewtex/tmux-mem-cpu-load
 - http://opennomad.com/content/goodbye-screen-hello-tmux
 - https://justin.abrah.ms/dotfiles/tmux.html
 - https://github.com/brandur/tmux-extra

### License
Nothing to be licensed, but just in case, everything in this repo is licensed under GNU GPLv3 
license. You can read the document [here].

[tmux]:http://tmux.sourceforge.net
[tmux-mem-cpu-load]:https://github.com/thewtex/tmux-mem-cpu-load
[Twitter]:http://twitter.com/soukron
[here]:http://gnu.org/licenses/gpl.html
[tmx]:http://github.com/brandur/tmux-extra
