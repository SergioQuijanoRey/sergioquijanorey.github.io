---
layout: post
title: Mi configuración de i3
---

# Mi configuración de i3

Este verano he estado experimentando con unos cuantos entornos de escritorios distintos. Siempre he usado *gnome* dado que es el entorno de escritorio que trae por defecto *Ubuntu*, y hasta que no sales de esa primera configuración no entiendes los problemas que trae una configuración linux alternativa que no tiene todas las cosas preparadas.

Entre estos entornos de escritorio, lo he intentado con *kde plasma* que no me terminó de convencer por necesitar una excesiva configuración en todos los elementos del escritorio para tener algo bien mínimamente funcional o bien mínimamente bonito. Otro entorno de escritorio, *xfce*, me pareció basntante potente, pero había algo que no me terminaba de convencer, y por otro lado, *lxde* me pareció simplemente anticuado.

Así que, cuando ya lo había dado por perdido y estaba a punto de volver a *gnome* por su cierta versatilidad y funcionalidad sin complicaciones, se cruzó en mi camino *i3*, que no es exactamente un entorno de escritorio, sino un gestor de ventanas (*window manager*). No tenía muchas esperanzas en esta alternativa, dado que *i3* tiene una fama (muy desmerecida) de ser extremadamente díficil de usar. Sin embargo, tras unas horas de uso, me enamoró por completo la potencia, versatilidad, grado de configuración y estética limpia y simple de este gestor de ventanas.

# Entorno de Escritorio vs Gestor de ventanas

La primera pregunta que se os puede venir a la mente es,qué es un gestor de ventanas y en qué se diferencia de un entorno de escritorio? 

Saber esto es fundamental a la hora de elegir una alternativa, dependiendo de una serie de factores fundamentales:

* Nuestra experiencia: si eres un usuario que acaba de empezar en el mundo de *linux* lo mejor que puedes es usar un entorno de escritorio que te de los menos problemas posibles
* Nuestro uso: si 

# Mi configuración

Tenéis mi configuración en mi página de *github*: [dotfiles](https://github.com/SergioQuijanoRey/dotfiles). Aquí tenéis mis archivos de configuración, con la estructura de árbol lista para clonar, actualizada al día en el que leáis esto. Incluso si queréis proponer algún cambio al código. De todas formas, los archivos de configuración que uso son los siguientes:

**.i3/config**:

~~~conf
# i3wm config file
# Autor:
#       Sergio Quijano Rey
#       sergiquijano@gmail.com
#       https://github.com/SergioQuijanoRey
# Version:
#       v1.0: 04/09/2018 - First little rice. The config file is uncleaned
#       v1.1: 04/09/2018 - Cleaning the config file

# Windows modkey
set $mod Mod4

# Fonts
font pango:System San Francisco Display 8
 
# Use Mouse+$mod to drag floating windows to their wanted position
floating_modifier $mod

# Launch terminal
bindsym $mod+Return exec i3-sensible-terminal

# kill focused window
bindsym $mod+Shift+q kill

# Rofi menu launcher
set $rofi_theme "/home/sergio/.i3/rofithemes/flat-blue.rasi"
bindsym $mod+d exec rofi -show run -config $rofi_theme
bindsym $mod+Shift+d exec rofi -show window -config $rofi_theme

# change focus
bindsym $mod+j focus left
bindsym $mod+k focus down
bindsym $mod+l focus up
bindsym $mod+ntilde focus right
bindsym $mod+Left focus left
bindsym $mod+Down focus down
bindsym $mod+Up focus up
bindsym $mod+Right focus right

# move focused window
bindsym $mod+Shift+j move left
bindsym $mod+Shift+k move down
bindsym $mod+Shift+l move up
bindsym $mod+Shift+ntilde move right
bindsym $mod+Shift+Left move left
bindsym $mod+Shift+Down move down
bindsym $mod+Shift+Up move up
bindsym $mod+Shift+Right move right

# Split horizontal and vertical orientation
bindsym $mod+h split h
bindsym $mod+v split v

# Fullscreen mode
bindsym $mod+f fullscreen toggle

# change container layout (stacked, tabbed, toggle split)
bindsym $mod+s layout stacking
bindsym $mod+w layout tabbed
bindsym $mod+e layout toggle split

# toggle tiling / floating
bindsym $mod+Shift+space floating toggle

# change focus between tiling / floating windows
bindsym $mod+space focus mode_toggle

# focus the parent container
bindsym $mod+a focus parent

# Workspace naming
set $workspace1 "1: Terminal "
set $workspace2 "2: Navigation "
set $workspace3 "3: Code Editing "
set $workspace4 "4: Folders "
set $workspace5 "5: Texting "
set $workspace6 "6"
set $workspace7 "7"
set $workspace8 "8"
set $workspace9 "9"
set $workspace10 "10: Music "

# switch to workspace
bindsym $mod+1 workspace $workspace1
bindsym $mod+2 workspace $workspace2
bindsym $mod+3 workspace $workspace3
bindsym $mod+4 workspace $workspace4
bindsym $mod+5 workspace $workspace5
bindsym $mod+6 workspace $workspace6
bindsym $mod+7 workspace $workspace7
bindsym $mod+8 workspace $workspace8
bindsym $mod+9 workspace $workspace9
bindsym $mod+0 workspace $workspace10

# move focused container to workspace
bindsym $mod+Shift+1 move container to workspace $workspace1
bindsym $mod+Shift+2 move container to workspace $workspace2
bindsym $mod+Shift+3 move container to workspace $workspace3
bindsym $mod+Shift+4 move container to workspace $workspace4
bindsym $mod+Shift+5 move container to workspace $workspace5
bindsym $mod+Shift+6 move container to workspace $workspace6
bindsym $mod+Shift+7 move container to workspace $workspace7
bindsym $mod+Shift+8 move container to workspace $workspace8
bindsym $mod+Shift+9 move container to workspace $workspace9
bindsym $mod+Shift+0 move container to workspace $workspace10

# Forcing apps on workspaces
# Web apps
assign [class="Firefox"] $workspace2
assign [class="Google-chrome"] $workspace2
# Coding apps
assign [class="Atom"] $workspace3
assign [class="Code"] $workspace3
assign [class="Gedit"] $workspace3
# File apps
assign [class="Nautilus"] $workspace4
# Texting apps
assign [class="TelegramDesktop"] $workspace5
assign [class="whatsapp-desktop"] $workspace5
# Music apps
#assign [class="Spotify"] $workspace10
for_window [class="Spotify"] move to workspace $workspace10

# reload the configuration file
bindsym $mod+Shift+c reload

# restart i3 inplace (preserves your layout/session, can be used to upgrade i3)
bindsym $mod+Shift+r restart

# exit i3 (logs you out of your X session)
bindsym $mod+Shift+e exec "i3-nagbar -t warning -m 'You pressed the exit shortcut. Do you really want to exit i3? This will end your X session.' -b 'Yes, exit i3' 'i3-msg exit'"

# Resize windows
mode "resize" {
        # Vim bindings
        bindsym j resize shrink width 10 px or 10 ppt
        bindsym k resize grow height 10 px or 10 ppt
        bindsym l resize shrink height 10 px or 10 ppt
        bindsym ntilde resize grow width 10 px or 10 ppt

        # Arrow bindings
        bindsym Left resize shrink width 10 px or 10 ppt
        bindsym Down resize grow height 10 px or 10 ppt
        bindsym Up resize shrink height 10 px or 10 ppt
        bindsym Right resize grow width 10 px or 10 ppt

        # back to normal: Enter or Escape
        bindsym Return mode "default"
        bindsym Escape mode "default"
}

# Resize binding
bindsym $mod+r mode "resize"

# Color config
set $bg-color 	         #2f343f
set $inactive-bg-color   #2f343f
set $text-color          #f3f4f5
set $inactive-text-color #676E7D
set $urgent-bg-color     #E53935
set $blue-color          #5DA8F4

# Window colors
client.focused          $bg-color           $bg-color          $text-color          #00ff00
client.unfocused        $inactive-bg-color $inactive-bg-color $inactive-text-color #00ff00
client.focused_inactive $inactive-bg-color $inactive-bg-color $inactive-text-color #00ff00
client.urgent           $blue-color    $blue-color   $text-color          #00ff00

# i3wm bar
bar {
        # Bar program
        status_command i3blocks -c ~/.i3/i3blocks.conf
        
        # Position of the bar
        position top
        
        # Bar colors
        colors {
		background $bg-color
	    	separator #757575
		#                  border             background         text
		focused_workspace  $bg-color          $bg-color          $text-color
		inactive_workspace $inactive-bg-color $inactive-bg-color $inactive-text-color
	        urgent_workspace   $blue-color   $blue-color   $text-color
        }
}

# Pulse Audio controls
bindsym XF86AudioRaiseVolume exec --no-startup-id pactl set-sink-volume 0 +5% #increase sound volume
bindsym XF86AudioLowerVolume exec --no-startup-id pactl set-sink-volume 0 -5% #decrease sound volume
bindsym XF86AudioMute exec --no-startup-id pactl set-sink-mute 0 toggle # mute sound

# Sreen brightness controls
bindsym XF86MonBrightnessUp exec xbacklight -inc 20 # increase screen brightness
bindsym XF86MonBrightnessDown exec xbacklight -dec 20 # decrease screen brightness

# Touchpad controls
bindsym XF86TouchpadToggle exec /home/sergio/bin/toggletouchpad # toggle touchpad

# Music song controls
bindsym XF86AudioPlay exec play_pause
bindsym XF86AudioPause exec play_pause
bindsym XF86AudioNext exec playerctl next
bindsym XF86AudioPrev exec playerctl previous

# Personal KeyBindings
bindsym $mod+x exec i3lock --color "$bg-color"
bindsym $mod+Shift+f exec firefox
bindym exec google-chrome
bindsym $mod+Shift+n exec google-chrome --incognito
bindsm $mod+Shift+x exec shutdown -h now
bindsym $mod+Shift+v exec code
bindsym $mod+Shift+b exec blueman-manager

# Invert scrolling
exec_always --no-startup-id synclient NaturalScrolling=1 VertScrollDelta=-113 

# Disable tap while typing
exec syndaemon -i 0.3 -t -K -R

# Remove green border on the left
for_window [class="^.*"] border pixel 0

# Apps on start
exec_always choose_wallpaper
exec_always compton
exec blueman
exec whatsapp
exec telegram
~~~

**.i3/3blocks.conf**

~~~conf
# i3blocks config file
#
# Please see man i3blocks for a complete reference!
# The man page is also hosted at http://vivien.github.io/i3blocks
#
# List of valid properties:
#
# align
# color
# command
# full_text
# instance
# interval
# label
# min_width
# name
# separator
# separator_block_width
# short_text
# signal
# urgent

# Global properties
#
# The top properties below are applied to every block, but can be overridden.
# Each block command defaults to the script name to avoid boilerplate.
command=/usr/share/i3blocks/$BLOCK_NAME
separator_block_width=15
markup=none

# Volume indicator
#
# The first parameter sets the step (and units to display)
# The second parameter overrides the mixer selection
# See the script for details.
[volume]
label=
instance=Master
#instance=PCM
interval=1
signal=10
command=/usr/share/i3blocks/volume 5 pulse

# Generic media player support
#
# This displays "ARTIST - SONG" if a music is playing.
# Supported players are: spotify, vlc, audacious, xmms2, mplayer, and others.
[mediaplayer]
label=
instance=spotify
interval=5
signal=10


# Memory usage
#
# The type defaults to "mem" if the instance is not specified.
# [memory]
# label=MEM
# separator=false
# interval=30

# [memory]
# label=SWAP
# instance=swap
# separator=false
# interval=30

# Disk usage
#
# The directory defaults to $HOME if the instance is not specified.
# The script may be called with a optional argument to set the alert
# (defaults to 10 for 10%).
[disk]
label=
#instance=/mnt/data
interval=30

# Network interface monitoring
#
# If the instance is not specified, use the interface used for default route.
# The address can be forced to IPv4 or IPv6 with -4 or -6 switches.
[iface]
#instance=wlan0
label=
interval=10
separator=false

[wifi]
#instance=wlp3s0
label=
interval=10
separator=false

# [bandwidth]
# #instance=eth0
# interval=5

# CPU usage
#
# The script may be called with -w and -c switches to specify thresholds,
# see the script for details.
# [cpu_usage]
# label=CPU
# interval=10
# min_width=CPU: 100.00%
#separator=false

[load_average]
label=
interval=10

# Battery indicator
#
# The battery instance defaults to 0.
[battery]
label=
#label=⚡
#instance=1
interval=30

# Date Time
#
[time]
label=
command=date '+%d-%m-%Y | %H:%M:%S'
interval=1

# OpenVPN support
#
# Support multiple VPN, with colors.
#[openvpn]
#interval=20

# Temperature
#
# Support multiple chips, though lm-sensors.
# The script may be called with -w and -c switches to specify thresholds,
# see the script for details.
#[temperature]
#label=TEMP
#interval=10

# Key indicators
#
# Add the following bindings to i3 config file:
#
# bindsym --release Caps_Lock exec pkill -SIGRTMIN+11 i3blocks
# bindsym --release Num_Lock  exec pkill -SIGRTMIN+11 i3blocks
#[keyindicator]
#instance=CAPS
#interval=once
#signal=11

#[keyindicator]
#instance=NUM
#interval=once
#signal=11
~~~

**.i3/rofithemes/flat-blue.rasi**:

~~~conf
/**
 * ROFI Color theme
 * User: mbfraga
 * Copyright: Martin B. Fraga
 */

/* global settings and color variables */
* {
   maincolor:        #5da8f4;
   highlight:        bold #5da8f4;
   urgentcolor:      #E53935;

   fgwhite:          #cfcfcf;
   blackdarkest:     #1d1d1d;
   blackwidget:      #262626;
   blackentry:       #292929;
   blackselect:      #303030;
   darkgray:         #848484;
   scrollbarcolor:   #505050;
   font: "DejaVu Sans Mono Regular 14";
   background-color: @blackdarkest;
}

window {
   background-color: @blackdarkest;
   anchor: north;
   location: north;
   y-offset: 20%;
}

mainbox {
   background-color: @blackdarkest;
   spacing:0px;
   children: [inputbar, message, sidebar, listview];
}

message {
   padding: 6px 10px;
   background-color:@blackwidget;
}

textbox {
   text-color:@darkgray;
   background-color:@blackwidget;
}

listview {
   fixed-height: false;
   dynamic: true;
   scrollbar: true;
   spacing: 0px;
   padding: 1px 0px 0px 0px;
   margin: 0px 0px 1px 0px;
   background: @blackdarkest;
}

element {
   padding: 2px 15px;
}

element normal.normal {
   padding: 0px 15px;
   background-color: @blackentry;
   text-color: @fgwhite;
}

element normal.urgent {
   background-color: @blackentry;
   text-color: @urgentcolor;
}

element normal.active {
   background-color: @blackentry;
   text-color: @maincolor;
}

element selected.normal {
    background-color: @blackselect;
    text-color:       @fgwhite;
}

element selected.urgent {
    background-color: @urgentcolor;
    text-color:       @blackdarkest;
}

element selected.active {
    background-color: @maincolor;
    text-color:       @blackdarkest;
}

element alternate.normal {
    background-color: @blackentry;
    text-color:       @fgwhite;
}

element alternate.urgent {
    background-color: @blackentry;
    text-color:       @urgentcolor;
}

element alternate.active {
    background-color: @blackentry;
    text-color:       @maincolor;
}

scrollbar {
   background-color: @blackwidget;
   handle-color: @darkgray;
   handle-width: 15px;
}

sidebar {
   background-color: @blackwidget;
}

button {
   background-color: @blackwidget;
   text-color:       @darkgray;
}

button selected {
    text-color:       @maincolor;
}

inputbar {
   background-color: @blackdarkest;
   spacing: 0px;
}

prompt {
   padding:6px 9px;
   background-color: @maincolor;
   text-color:@blackwidget;
}

entry {
   padding:6px 10px;
   background-color:@blackwidget;
   text-color:@fgwhite;
}

case-indicator {
   padding:6px 10px;
   text-color:@maincolor;
   background-color:@blackwidget;
}
~~~

**.i3/scripts/choose_wallpaper**:

~~~python
#!/usr/bin/python3.6
# A simple program to make a slide wallpaper on i3-wm

import time
import random
import os

# Some functions
def choose_random_wallpaper(dir, opts, last_img = None):
    # The wallpaper img is chosen
    opt = random.choice(opts)
    img = dir + "/" + opt

    # The same wallpaper is discarded
    if img == last_img:
        return choose_random_wallpaper(dir, opts, last_img)
    else:
        # The i3-wm command is launch
        os.system("feh --bg-scale {}".format(img))
        return img

# The data of the wallpaper images
img_dir = "/home/sergio/GitProjects/misArchivos/Fondos_pantalla/LowPoly"
opts = [
    "low_poly_bird.png",
    "low_poly_cat_1.png",
    "low_poly_cat_2.png",
    "low_poly_colors.jpg"
]

minute_change = 3   # Change the wallpaper every 3 mins
seconds_change = minute_change * 60

# The actual algorithm --> Daemon
prev_img = choose_random_wallpaper(img_dir, opts)  # First time a wallpaper has to be chosen
last_time = time.time()

while True:
    now = time.time()
    key = input()

    if now - last_time > seconds_change:
        prev_img = choose_random_wallpaper(img_dir, opts, prev_img)
        last_time = now
~~~

**.i3/scripts/play_pause**:

~~~python
#!/usr/bin/python3
# Program made for some improvements

import os

config_file = "/home/sergio/.i3/scripts/play_pause.config"

with open(config_file, "r") as fileobj:
    # State 0 --> esta pausado, hay que reproducir
    # State 1 --> se esta reproduciendo, hay que pausar

    state = fileobj.read()

    if state == "0":
        os.system("playerctl play")
        new_state = 1
    elif state == "1":
        os.system("playerctl pause")        
        new_state = 0
    else:
        os.system("playerctl play")
        new_state = 1
        print("ERROR!")
    
with open(config_file, "w") as fileobj:
    fileobj.write(str(new_state))
~~~

**.i3/scripts/telegram**:

~~~bash
#!/bin/bash

# Executes telegram desktop app
/home/sergio/.telegram/Telegram
~~~

**.i3/scripts/whatsapp**:

~~~bash
#!/bin/bash

/opt/whatsapp-desktop/WhatsApp
~~~

**.i3/scripts/toggletouchpad**:

~~~bash
#!/bin/bash
if synclient -l | grep "TouchpadOff .*=.*0" ; then
    synclient TouchpadOff=1 ;
else
    synclient TouchpadOff=0 ;
fi
~~~
