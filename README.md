3dfsb
=====

3D File System Browser - improved, cleaned up and maintained fork of the old tdfsb

This runs on GNU/Linux, and might run on BeOS and FreeBSD (although this has not been tested recently).

Homepage: https://github.com/tomvanbraeckel/3dfsb

Maintained and improved by Tom Van Braeckel
Originally written by Leander Seige

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA



Dependencies
============

(a better installation (autoconf) is planned for future releases)

Needed Libraries:

You may need to install 'devel' packages of these
libraries in order to get the necessary .h files
and the sdl-config script.

SDL             (http://www.libsdl.org)
SDL_image       (http://www.libsdl.org/projects/SDL_image/index.html)
OpenGL/GLU/glut (       Linux/FreeBSD:  look at your distribution
                                        if that fails:
                                        http://www.rpmfind.net/
                                        http://freshmeat.net/
                        BeOS:           OpenGL (including GLU) should come 
                                        with BeOS,
                                        for glut look at http://www.bebits.com
                )
libmagic-dev	For mimetype identification

On Ubuntu, you can install all build-time dependencies with:

sudo apt-get install build-essential freeglut3-dev libsdl-image1.2-dev libsdl1.2-dev libsmpeg-dev libxi-dev libxmu-dev

This list of dependencies was made using: apt-rdepends --build-depends --follow=DEPENDS 3dfsb

+ for GStreamer, you need:
sudo apt-get install libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libgstreamer-plugins-bad0.10-dev

and also perhaps:

sudo apt-get install gstreamer0.10-plugins-*
sudo apt-get install gstinterfaces

and for pulseaudio:

sudo apt-get install gstreamer1.0-pulseaudio

Compilation
===========

There is a small shell script which contains a standard compile
string for every OS (Linux, BeOS and BSD). So please try

./compile.sh

If something goes wrong error messages will appear. If
you don't know how to solve them don't hesitate and
report the error messages to me.

If ./compile.sh was successful you can call the 3dfsb

./3dfsb

or copy the 3dfsb binary to your path, e.g. /usr/bin/

Once you have a working 3dfsb binary you may try to
edit the compile.sh for a more optimized version.
You could change the -O2 argument (opimization) to a
higher value (e.g. -O6) or add machine specific
optimizations (e.g.  -march=i686 -mcpu=i686).
Read 'man gcc' for additional arguments.


ADDITIONAL NOTES


FreeBSD:

If you have problems with SDL_image try:
cd /usr/ports/graphics/sdl_image/
make install


BeOS:

This package does not contain a BeOS binary, because i don't 
have BeOS installed on my computer anymore, sorry :/
The source should compile anyway.

I noticed that the SMPEG library could be hard to find,
especially the development package so i made that package
available from my own page:
http://www.determinate.net/webdata/data/SDLGameLibs-1.2.2-devel-beos.zip

NVidia Cards under Linux (+FreeBSD?):

NVidia users who have problems compiling the 3dfsb
--------------------------------------------------
In most cases they are linking
against the wrong libraries, especially the libGLU.so.
In this case please read the instructions that came
with your drivers.
The following often helped but of course i can give no
guarantee, try it on your own risk!
    There are two libGLU.so's. Move the original libGLU.so
    to a safe place (libGLU.so.my.original or something).
    Make a link libGLU.so->libGLU.so.the.right.one.
    libGLU.so.the.right.one is often >500kByte while
    the wrong libGLU.so is much smaller.




********CREDITS********

Thanks to:

Marc Berhault for some additional code (see ChangeLog)

Nico 'aMadMan' Toerl for extensive beta testing

Kyle 'greenfly' Rankin for some additional code (see ChangeLog)

Benjamin Burke for help and testing of the compile.sh

Rafal Zawadzki for creating man pages and debian packages

all the people who sent me additional compile strings and new ideas




*********USAGE*********

3dfsb
  or
3dfsb -V
  or
3dfsb --version
  or
3dfsb -D /path/to/dir
  or
3dfsb --dir /path/to/dir

- the config file is $HOME/.3dfsb (e.g. /home/user/.3dfsb). if it does not
  exist tdsfb will generate one with all available options. this is strongly
  recommended.

- if you start the 3dfsb the first time, press 'h' for the help menu
  (will also be printed to the terminal)

- simply walk into the spheres for cd'ing into another directory

- select an object by pointing at it with the crosshair and press the left
  mouse button. or hold the left mouse button and press any key to select
  the first object that begins with that character (case sensitive).
    -   while an object is selected press the right mouse button simultaneously to
        automatic approach the object
        [unfortunately doesn't work on BeOS as well as resizing the window, afaik
        these are issues of the SDL implementation, use the right CTRL for now].
    -   if an mp3 or mpeg1 video file is selected press the RETURN key to start
        the playback

- some of the displays are not visible while the help display is active

- it is possible to execute a custom command from within 3dfsb. configure
  your command in the config file! the command can be called by pressing
  the tabulator key. put a "%s" in the command line, this will be replaced
  by the current directory or selected file.
  for instance if you set the command to
    xmms "%s" &
  and press tab from a directory, xmms will be started with the directory
  given as argument. 
  if you select an audio file and press the tab key xmms will play the file.
  the default command is
    cd "%s"; xterm&
  it will open a xterm in the current directory.
  this command is always present by pressing shift+tab!
  so you have two commands: 
  - one by configuring your custom command for the tab key
  - one by pressing shift+tab, it will execute the built in xterm call  
  but dont forget the quotation marks!
  you are free to not add "%s" to your custom command if you just
  want to launch any program. but if you do so, you can customize
  3dfsb for your needs, choose a certain kind of files and than launch
  emacs for editing text files, mplayer for playing avis or whatever...

Here is a print out of the default keyboard settings.
You may change these by editing ~/.3dfsb

=======================================
Esc           quit   F1/F2    speed +/-
Mouse move    look   F3/F4      rot +/-
UP         forward   F5/F6  ball detail
DOWN      backward   HOME     start pos
L/R     step aside   LMB  select object
END    ground zero   +RMB|CTRL appr.obj
F7/F8  max fps +/-   +ENTER ply mpg/mp3
"t"      filenames   "g"   ground cross
"c"      crosshair   "d"        display
"."      dot files   "p"      print FPS
"r" rel./get mouse   "f"     fullscreen
"l"     reload dir   "b"   image bricks
"u"           cd..   "a"      alphasort
"m"        shading   " "         flying
"h"      show help   "i"  print GL info
"0"      jump home   "o"    classic nav
"s"    save config   "#"   fps throttle
 
"1|3|q|e"            Up|Down|Left|Right
"2|w"                  Forward|Backward
PgUp/Down or MMB+Mouse move up/downward
=======================================

22/06/2007:
ps. TDFSB is 6 years old now and I havent done anything on it for a long time.
Today I would code a lot of things very different - better i hope - than years
ago. But, so what, it still works and I got very less bug reports on 3dfsb.
Some days ago I installed Gentoo for the first time and I heared that someone
(thank you!) build a package for Gentoo so I tried emerge 3dfsb and it worked :)
Besides that it has problems with freeglut which I quickly fixed now.
So I hope some people, YOU,  still like it. Have fun!

25/12/2014:
Tom here; I've picked up where Leander left off.
I'm cleaning up the code and adding features, see CHANGELOG!