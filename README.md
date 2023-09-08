# beepy-tmux
This is a tmux configuration for Beepy made by SQFMI.

A configuration let Tumx start at systeml lauch and neofetch output system status before the prompt string.

## Prequisition

You have to install the screen and keyboard driver through the official doc page.

https://beepy.sqfmi.com/docs/getting-started

## Installation

1. Install Tmux and Neofetch

   ```bash
   $ sudo apt install tmux neofetch
   ```

2. Install Fbterm and CJK fonts

   Download fbterm

   ```bash
   $ git clone https://github.com/onokatio/fbterm2.git
   ```

## Configuration

### Neofetch Configuration

1. Download SQFMI duck ascii file to your directory

   ```bash
   $ mkdir -p ~/.config/neofetch/
   $ wget https://raw.githubusercontent.com/youngoris/beepy-tmux/main/neofetch/sqfmi-duck-w24.ascii -O ~/.config/neofetch/sqfmi-duck-w24.ascii
   ```

2. Edit `config.conf` under the `~/.config/neofetch/` directory

   ```bash
   $ nano ~/.config/neofetch/config.conf
   ```

3. Replace the function `print_info()` with the following code:

   ```bash
   print_info() {
       prin "------------------- "
       prin "BEEPY made by SQFMI "
       info underline
       
       info "OS" distro
       info "Host" model
       info "Kernel" kernel
       info "Uptime" uptime
       info "Packages" packages
       # info "Shell" shell
       info "Resolution" resolution
       info "DE" de
       info "WM" wm
       info "WM Theme" wm_theme
       info "Theme" theme
       info "Icons" icons
       info "Terminal" term
       info "Terminal Font" term_font
       info "CPU" cpu
       # info "GPU" gpu
       info "Memory" memory
   
       # info "GPU Driver" gpu_driver  # Linux/macOS only
       # info "CPU Usage" cpu_usage
       info "Disk" disk
       # info "Battery" battery
       # info "Font" font
       # info "Song" song
       # [[ "$player" ]] && prin "Music Player" "$player"
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

Finnaly, run neofetch you will see our duck appears on your screen.

```bash
$ neofetch
```



### Tmux Configuration

1. Create or Open config file

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

### Fbterm Configuration

1. Change  `/dev/fb0`  to  `/dev/fb1`  in /src/fbdev.cpp

   ```bash
   $ cd fbterm2
   $ nano ./src/fbdev.cpp  
   ```

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

   
