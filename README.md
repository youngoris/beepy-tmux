# info "Local IP" local_ip
       # info "Public IP" public_ip
       # info "Users" users
       # info "Locale" locale  # This only works on glibc systems.
       info col
   }
   ```


   *The uncomment `info` should not exceed 12 lines, otherwise the beepy will not display a complete duck ascii image.


4. Change `image_sourc` value with our duck ascii file's path,a and replace `YOUR_NAME` with your username.


   ```bash
   image_source="/home/YOUR_NAME/.config/neofetch/sqfmi-duck-w24.ascii"
   ```


5. Give more screen space to system information text, toggle off color blocks, and change the `gap` value to `2` or `1`.


   ```bash
   color_blocks="off"
   gap=2
   ```


6. Other useful changes


   ```
   memory_percent="on"
   disk_percent="on"
   ```


7. Finnaly, run neofetch you will see our duck appears on your screen.


   ```$ neofetch
   $ neofetch
   ```





### Tmux Configuration
Follow these steps to configure tmux:


1. Edit the Configuration File


   ```bash
   nano ~/.tmux.conf
   ```


2. Add battery percent and CPU temprature inforamtion to the right of Tmux status bar, and session number to the left.


   ```bash
   set -g status-left "[#S] "
   set-option -g  status-right "#(cat /sys/firmware/beepy/battery_percent)% #(vcgencmd measure_temp | cut -c6-9|awk '{print int($1)}')C %H:%M %a %d/%b"
   ```


3. Set status bar refresh frequency to 30s


   ```bash
   set -g status-interval 30
   ```


4. Set keybinds


   ```bash
   bind-key b send-keys C-b
   bind-key C-b last-window
   bind-key \" choose-tree 
   bind-key r source-file ~/.tmux.conf \; display-message "~/.tmux.conf reloaded"
   ```


5. If you already running tmux, press the blackberry button + r to reload the configuration. If not, run Tmux in the terminal,  you'll see the battery and cpu info appear on the status bar. 


   ```bash
   $ tmux
   ```
6. Solving double prompts issue when quit tmux by using ctrl + d

   ```bash
   $ nano ~/bashrc
   ```
   Find PS1 setting under the line xterm*|rxvt*):

   PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
   replace it with:
   PS1="\[\e]0\a\]$PS1"


### Fbterm Configuration


1. Edit the Configuration File


   ```bash
   $ cd fbterm2
   $ nano ./src/fbdev.cpp  
   ```
   replace `/dev/fb0` with `/dev/fb1`.
2. Execute the below to compile and install fbterm.


   ```bash
   $ sudo apt-get install libfontconfig1-dev
   $ cd ~/fbterm2
   $ ./configure && make && sudo make install
   ```


3. Make sure you execute the below so fbterm can be run by non-root user and can capture shortcut keys


   ```bash
   $ sudo gpasswd -a YOUR_USERNAME video
   $ sudo setcap 'cap_sys_tty_config+ep' /usr/local/bin/fbterm
   ```


4. Run fbterm once which create the default fbterm configure file we need to edit# info "Local IP" local_ip
       # info "Public IP" public_ip
       # info "Users" users
       # info "Locale" locale  # This only works on glibc systems.
       info col
   }
   ```


   *The uncomment `info` should not exceed 12 lines, otherwise the beepy will not display a complete duck ascii image.


4. Change `image_sourc` value with our duck ascii file's path,a and replace `YOUR_NAME` with your username.


   ```bash
   image_source="/home/YOUR_NAME/.config/neofetch/sqfmi-duck-w24.ascii"
   ```


5. Give more screen space to system information text, toggle off color blocks, and change the `gap` value to `2` or `1`.


   ```bash
   color_blocks="off"
   gap=2
   ```


6. Other useful changes


   ```
   memory_percent="on"
   disk_percent="on"
   ```


7. Finnaly, run neofetch you will see our duck appears on your screen.


   ```$ neofetch
   $ neofetch
   ```





### Tmux Configuration
Follow these steps to configure tmux:


1. Edit the Configuration File


   ```bash
   nano ~/.tmux.conf
   ```


2. Add battery percent and CPU temprature inforamtion to the right of Tmux status bar, and session number to the left.


   ```bash
   set -g status-left "[#S] "
   set-option -g  status-right "#(cat /sys/firmware/beepy/battery_percent)% #(vcgencmd measure_temp | cut -c6-9|awk '{print int($1)}')C %H:%M %a %d/%b"
   ```


3. Set status bar refresh frequency to 30s


   ```bash
   set -g status-interval 30
   ```


4. Set keybinds


   ```bash
   bind-key b send-keys C-b
   bind-key C-b last-window
   bind-key \" choose-tree 
   bind-key r source-file ~/.tmux.conf \; display-message "~/.tmux.conf reloaded"
   ```


5. If you already running tmux, press the blackberry button + r to reload the configuration. If not, run Tmux in the terminal,  you'll see the battery and cpu info appear on the status bar. 


   ```bash
   $ tmux
   ```
6. Solving double prompts issue when quitting tmux with prefix key + d

   ```bash
   $ nano ~/bashrc
   ```
   Find PS1 setting under the line `xterm*|rxvt*)`:
   ```
   PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
   ```
   replace it with:
   ```
   PS1="\[\e]0\a\]$PS1"
   ```


### Fbterm Configuration


1. Edit the Configuration File


   ```bash
   $ cd fbterm2
   $ nano ./src/fbdev.cpp  
   ```
   replace `/dev/fb0` with `/dev/fb1`.
2. Execute the below to compile and install fbterm.


   ```bash
   $ sudo apt-get install libfontconfig1-dev
   $ cd ~/fbterm2
   $ ./configure && make && sudo make install
   ```


3. Make sure you execute the below so fbterm can be run by non-root user and can capture shortcut keys


   ```bash
   $ sudo gpasswd -a YOUR_USERNAME video
   $ sudo setcap 'cap_sys_tty_config+ep' /usr/local/bin/fbterm
   ```


1. Run fbterm once which create the default fbterm configure file we need to edit.

   ```bash
   $ fbterm
   ```

   `stdin isn't a interactive tty!` Ignore this output, it doesn't matter.

   change the following

   ```bash
   font-names=Terminus,WenQuanYi Bitmap Song,DotGothic16
   font-size=14
   font-width=8
   font-height=16
   text-encodings=utf-8
   term=xterm-mono
   ```

2. To autostart at system launch, add the following code to your shell configure file

   ```bash
   $ nano ~/.bashrc
   ```

   ```bash
   if [ -z "$SSH_CONNECTION" ]; then
    # if in virtual terminal, start fbterm
      if [[ "$(tty)" =~ /dev/tty ]] && type fbterm > /dev/null 2>&1; then
           fbterm 
     # otherwise, start/attach to tmux and start neofetch
      elif [ -z "$TMUX" ] && type tmux >/dev/null 2>&1; then
           tmux new -As "$(basename $(tty))" 'neofetch; bash'
      fi
   fi
   ```

   

### Optinal: Install fcitx and enable IMEs 

If you wish to use input methods, you can install and configure fcitx:

1.Install Fcitx

   ```
$ sudo apt install fcitx-frontend-fbterm
   ```

2. Run `fcitx-config-gtk3` under Xorg to enable IMEs or go to `~/.config/fcitx` and edit `profile` (example below enables google pinyin)

   ```
   EnabledIMList=fcitx-keyboard-us:True,googlepinyin:True,pinyin:False
   ```

3. Uncomment and change the following in `~/.fbtermrc`,

   ```
   input-method=fcitx-fbterm
   ```

4. Make `fcitx` start at system launch.

   Create a script to check if `fcitx` is running in each time we create a new terminal.

   ```bash
   $ nano ~/fcitx-start-check.sh
   ```

   fill with the following

   ```bash
   #!/bin/bash
   if ! pgrep -x "fcitx" > /dev/null; then
       echo "fcitx is not running. Starting fcitx..."
       nohup fcitx > /dev/null 2>&1 &
       sleep 1  # wait fcitx to start
   fi
   exit
   ```

   make this file excutable with the following code

   ```
   sudo chmod +x ~/fcitx-start-check.sh
   ```

   add the below code to your `tmux.conf `

   ```
   #Start fcitx 
   new-session -d -s default "~/fcitx-start-check.sh"
   ```

   

5. Reboot to your Tmux terminal, press ctrl(anwser call) + space, you will activate the input method( For example: Google Pinyin).

## Credites

[CJK support on Beepy ](https://gist.github.com/charlestsai1995/54ab65a87e2e063ea25eb3aec4193fe1) @charlestsai1995

[Beepy Package Repository](https://github.com/ardangelo/beepy-ppa) @ardangelo

[Getting Started](https://beepy.sqfmi.com/docs/getting-started) @SQFMI
