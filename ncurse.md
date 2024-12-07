  * see http://jbwyatt.com/ncurses.html

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<!-- saved from url=(0031)http://jbwyatt.com/ncurses.html -->
<html><head><meta http-equiv="Content-Type" content="text/html; charset=windows-1252"><title>Ncurses programming guide</title>


<style type="text/css">
   body {
         color: #000; background: #FFF; margin-left: 3%; margin-right: 3%;
   }
   H1, H2 {color: #00F;}
   code {color: #095D0F;}
   #code {color: #000099;}
   #ptype {color: #995D99;}
   #vim {color: #095D0F;}
   </style>

<meta content="Microsoft FrontPage 4.0" name="GENERATOR"><style type="text/css">#_copy{align-items:center;background:#4494d5;border-radius:3px;color:#fff;cursor:pointer;display:flex;font-size:13px;height:30px;justify-content:center;position:absolute;width:60px;z-index:1000}#select-tooltip,#sfModal,.modal-backdrop,div[id^=reader-helper]{display:none!important}.modal-open{overflow:auto!important}._sf_adjust_body{padding-right:0!important}.enable_copy_btns_div{position:fixed;width:154px;left:10px;top:45%;background:#e7f1ff;border:2px solid #4595d5;font-weight:600;border-radius:2px;font-family:-apple-system,BlinkMacSystemFont,Segoe UI,PingFang SC,Hiragino Sans GB,Microsoft YaHei,Helvetica Neue,Helvetica,Arial,sans-serif,Apple Color Emoji,Segoe UI Emoji,Segoe UI Symbol;z-index:5000}.enable_copy_btns_logo{width:100%;background:#4595d5;text-align:center;font-size:12px;color:#e7f1ff;line-height:30px;height:30px}.enable_copy_btns_btn{display:block;width:128px;height:28px;background:#7f5711;border-radius:4px;color:#fff;font-size:12px;border:0;outline:0;margin:8px auto;font-weight:700;cursor:pointer;opacity:.9}.enable_copy_btns_btn:hover{opacity:.8}.enable_copy_btns_btn:active{opacity:1}</style></head><body inmaintabuse="1">
<h1>Ncurses Programming Guide</h1>
<p>If you have some beginning experience in Unix programming, you may have felt 
the need of some text user interface operations, such as moving the cursor on 
the screen, editing user input, using colors, ... Such terminal IO related 
operations are not portable and not defined in C language. You need to either 
use the low-level termcap library or the curses library. Using curses/ncurses 
library is much easier and more portable. 
</p><h2>Contents</h2>
<dl>
  <dt>
  </dt><h4><a href="http://jbwyatt.com/ncurses.html#using">Using the library</a></h4>
  <dd>Installations, header inclusions and link options. 
  </dd><dt>
  </dt><h4><a href="http://jbwyatt.com/ncurses.html#init">Before and after using ncurses function</a></h4>
  <dd>Thing you need to do before calling curses functions 
  </dd><dt>
  </dt><h4><a href="http://jbwyatt.com/ncurses.html#window">Creating windows</a></h4>
  <dd>Creating windows 
  </dd><dt>
  </dt><h4><a href="http://jbwyatt.com/ncurses.html#cursor">Moving the cursor</a></h4>
  <dd>Move the cursor around the window 
  </dd><dt>
  </dt><h4><a href="http://jbwyatt.com/ncurses.html#input">Input</a></h4>
  <dd>Read user input from keyboard 
  </dd><dt>
  </dt><h4><a href="http://jbwyatt.com/ncurses.html#output">Output</a></h4>
  <dd>Write text to the window 
  </dd><dt>
  </dt><h4><a href="http://jbwyatt.com/ncurses.html#attribute">Using colors and other text attributes</a></h4>
  <dd>Text colors, highlighting, blinking, ... 
  </dd><dt>
  </dt><h4><a href="http://jbwyatt.com/ncurses.html#xterm">Using curses in Xterm</a></h4>
  <dd>How to cope window resizing by user 
  </dd><dt>
  </dt><h4><a href="http://jbwyatt.com/ncurses.html#example">An example of complete programs</a></h4>
  <dd>A typing speed test program by me </dd></dl>
<p align="center"></p><hr> <p></p><a name="using">
</a><h2><a name="using">Using ncurses library</a></h2><a name="using">To compile your C/C++ programs using  
ncurses/curses library you need to include the curses header file  
<tt>&lt;curses.h&gt;</tt>. For ncurses, you may include either  
<tt>&lt;curses.h&gt; or &lt;ncurses.h&gt;</tt>. In some systems, you must  
include <tt>&lt;ncurses.h&gt;</tt>.  
</a><blockquote><code id="code"><a name="using">#include &lt;curses.h&gt;</a></code><a name="using"> </a></blockquote><a name="using">To link  
the programs you need to use the <tt><b>-lcurses</b></tt> or  
<tt><b>-lncurses</b></tt> option, like  
</a><blockquote><code id="code"><a name="using">gcc -lncurses prog.c</a></code><a name="using"> </a></blockquote><a name="using">This way the  
program is dynamically linked to the ncurses library. To run it in another  
computer, the system must have the ncurses library installed. If you want to  
avoid the trouble, you may have it statically linked. To do that, find the file  
<tt><b>libncurses.a</b></tt> in <tt><b>/usr/lib</b></tt> and do  
</a><blockquote><code id="code"><a name="using"><b>gcc prog.c libncurses.a</b></a></code><a name="using"> </a></blockquote><a name="using"> 
</a><p><a name="using">Most Unix systems have curses or ncurses installed as a default option. To  
find out if it's installed, you can try man ncurses man curses or go to /usr/lib  
and /usr/include to list the files.  
</a></p><p><a name="using">If you're installing Linux or FreeBSD on your own machine, be sure to install  
the <tt><b>ncurses-development</b></tt> package in order to do ncurses  
programming.  
</a></p><p align="center"><a name="using"></a></p><hr><a name="using"> </a><p></p><a name="init"> 
</a><h2><a name="init">Initialization</a></h2><a name="init"><b>The very first thing to do:</b> Before you use any  
other <i><b>curses</b></i> routines, the <tt>initscr()</tt> routine must be  
called first.  
</a><blockquote><code id="code"><a name="init"><b>initscr();</b></a></code><a name="init"> </a></blockquote><a name="init">If your program  
is going to write to several terminals, you should call <tt>newterm</tt> instead,  
which is another story.  
</a><p><a name="init"><b>One-character-a-time.</b> To disable the buffering of typed characters by  
the TTY driver and get a character-at-a-time input, you need to call  
</a></p><blockquote><code id="code"><a name="init"><b>cbreak();</b></a></code><a name="init"> </a></blockquote><a name="init"> 
</a><p><a name="init"><b>No echo.</b> To suppress the automatic echoing of typed characters, you  
need to call  
</a></p><blockquote><code id="code"><a name="init"><b>noecho();</b></a></code><a name="init"> </a></blockquote><a name="init"> 
</a><p><a name="init"><b>Special keys.</b> In order to capture special keystrokes like  
<tt><b>Backspace</b></tt>, <tt><b>Delete</b></tt> and the four arrow keys by  
<code><b>getch()</b></code>, you need to call  
</a></p><blockquote><code id="code"><a name="init"><b>keypad(stdscr, TRUE);</b></a></code><a name="init"> </a></blockquote><a name="init"> 
</a><p><a name="init"><b>Before exiting.</b> Before the program is terminated,  
<tt><b>endwin()</b></tt> must be called to restore the terminal settings.  
</a></p><p align="center"><a name="init"></a></p><hr><a name="init"> </a><p></p><a name="window"> 
</a><h2><a name="window">Windows</a></h2><a name="window">A window is a 2-dimensional array of characters representing all  
or part of a CRT screen. Character input and output should pertain to a specific  
window.  
</a><p><a name="window"><b>The default window.</b> A default window called <tt><b>stdscr</b></tt>,  
which is the size of the terminal screen, is supplied. To use the  
<tt><b>stdscr</b></tt> window, you don't need to do any initializations. You can  
also divide the screen to several parts and create a window to represent each  
part.  
</a></p><p><a name="window"><b>Create a new window.</b> The data structure of window is WINDOW, defined  
in ncurses.h. To declare and create a new window, do  
</a></p><blockquote><code id="code"><a name="window"><b>WINDOW * win = newwin(nlines, ncols, y0,  
  x0);</b></a></code><a name="window"> </a></blockquote><pre><a name="window">                        The screen (stdscr)
        (0,0)*----------------------------------* (0, COLUMNS-1)
             |                                  |
             |                                  |
             |    (y0,x0)                       |
             |      ---------------             |
             |      |             |             |
             |      |             |             |
             |      |     win     |nlines       |
             |      |             |             |
             |      |             |             |
             |      |             |             |
             |      ---------------             |
             |          ncols                   |
             |                                  |
             *----------------------------------*
       (LINES-1, 0)                              (LINES-1, COLUMNS-1) 
</a></pre><a name="window">All the 4 parameters are <tt id="code"><b>int</b></tt>s. Here nline is the  
height of the window -- number of lines, ncols is the width -- number of columns  
of the window. y0 and x0 are the coordinates of the upper left corner of win on  
the screen -- line y0 and columns x0. You should make sure that the area of the  
new window is inside the screen.  
</a><p><a name="window"><b>Height and width of the window.</b> The size of the whole screen can be  
determined by the two global variables <tt><b>COLUMNS</b></tt> and  
<tt><b>LINES</b></tt>. <tt><b>y0</b></tt> and <tt><b>x0</b></tt> should satisfy </a></p><pre><code id="code"><a name="window"><b>
   0 &lt;= y0 &lt; LINES;
   0 &lt;= x0 &lt; COLUMNS;
</b></a></code>
</pre><a name="window"> 
</a><p><a name="window">In X window system, the actual xterm size might be changed leaving these two  
variables obslete. In this case you should use the macro <tt id="ptype">void  
getmaxyx(WINDOW *, int y, int x)</tt> to get the size of the screen. </a></p><pre><code id="code"><a name="window"><b>
   int h, w;
   getmaxyx(stdscr, h, w);
</b></a></code>
</pre><a name="window"> 
</a><p><a name="window"><b>No overlapping.</b> Windows cannot overlap with each other. Therefore you  
have two options: only use stdscr and no other windows, or create several  
non-overlapping windows but do not use stdscr.  
</a></p><p><a name="window"><b>Refresh.</b> If you make some change to a window, such as printing  
something or moving the cursor, the effect is not shown on the screen until you  
call the wrefresh() function </a></p><pre><code id="code"><a name="window"><b>
   wrefresh(win);
</b></a></code>
</pre><a name="window"> 
</a><p><a name="window"><b>Clear window.</b> To erase everything written in the window  
<tt><b>win</b></tt>, call <tt><b>wrefresh(win)</b></tt>.  
<tt><b>refresh()</b></tt> is equivalent to <tt><b>wrefresh(stdscr)</b></tt>.  
</a></p><p><a name="window"><b>Delete window.</b> If a window <tt><b>win</b></tt> is no longer needed,  
and you're going to create new windows to overlap it, you should call  
<tt><b>delwin(win)</b></tt> to delete the window (release the memory it is  
using).  
</a></p><p align="center"><a name="window"></a></p><hr><a name="window"> </a><p></p><a name="cursor"> 
</a><h2><a name="cursor">Moving the cursor</a></h2><a name="cursor">The position of the cursor on the screen is important  
because it is default beginning place for most output functions. The cursor also  
shows the user where the input is expected.  
</a><p><a name="cursor">To move the cursor to a new position on a window, use the function <code id="code"><b>int wmove(WINDOW *win, int y, int x)</b></code>  
</a></p><blockquote><code id="code"><a name="cursor"><b>wmove(win, y, x);</b></a></code><a name="cursor"> </a></blockquote><a name="cursor">where  
<tt><b>(x, y)</b></tt> are the coordinates of the new position in the window. If  
the window has <tt><b>nlines</b></tt> lines and <tt><b>ncolumns</b></tt>  
columns, then </a><pre><a name="cursor"><b>
      0 &lt;= y &lt; nlines
      0 &lt;= x &lt; ncolumns
</b></a></pre><a name="cursor"> 
</a><p><a name="cursor"><b>Refresh.</b> The actual cursor motion is not shown on the screen untill  
you do a <tt><b>wrefresh(win)</b></tt>.  
</a></p><p><a name="cursor"><tt><b>move(y, x)</b></tt> is equivalent to the <tt><b>wmove(stdscr, y,  
x)</b></tt>.  
</a></p><p align="center"><a name="cursor"><img src="./Ncurses programming guide_files/slim.gif" height="7" width="100%"> </a></p><a name="input"> 
</a><h2><a name="input">Input</a></h2><a name="input">To read a character from stdscr, use the function <code id="code"><b>int getch(void)</b></code>. </a><pre id="code"><a name="input"><b>
    int ch = getch();
</b></a></pre><a name="input"><b>No echoing.</b> If you have called <code id="code"><b>noecho()</b></code>, the character <code id="code"><b>ch</b></code>  
will not be printed on the screen, otherwise it will. Disabling automatic  
echoing gives you more control over the user interface.  
</a><p><a name="input"><b>No buffering.</b> If you have called <code id="code"><b>cbreak(void)</b></code> each key the user hits is returned  
immediately by <code id="code"><b>getch()</b></code>. Otherwise the keys hit by  
the user are queued until a newline is read. Then calls to <code id="code"><b>getch()</b></code> take characters from the queue in FIFO manner until 
the queue is empty and the next whole line is read.  
</a></p><p><a name="input"><b>No delaying.</b> Usually a call to <code id="code"><b>getch()</b></code>  
waits until a key is hit. If you have called <code id="code"><b>nodelay(stdscr,  
TRUE)</b></code>, then <code id="code"><b>getch()</b></code> will work in a  
non-blocking manner -- it will return <tt><b>ERR</b></tt> if the key input is  
not ready. This is usually useful for writing game-like programs, where the  
promptness of user response matters. For example </a></p><pre id="code"><a name="input"><b>
     int ch;
     nodelay(stdscr, TRUE);
     for (;;) {
          if ((ch = getch()) == ERR) {
              /* user hasn't responded
               ...
              */
          }
          else {
              /* user has pressed a key ch
               ...
              */
          }
     }
</b></a></pre><a name="input"> 
</a><p><a name="input"><b>Special keys.</b> If you have called <code id="code"><b>keypad(stdstr,  
TRUE)</b></code>, then if the user hits a special key such as the <tt><b id="spk">Delete</b></tt> key, the arrow keys, <tt><b>Ctrl</b></tt> combined keys  
and function keys, a single int value will be returned. Here is the definition  
of several special keys </a></p><pre><a name="input"><b id="code">
           key code        description

           KEY_DOWN        The four arrow keys ...
           KEY_UP
           KEY_LEFT
           KEY_RIGHT
           KEY_HOME        Home key 
           KEY_BACKSPACE   Backspace
           KEY_F(n)        Function keys, for 0 &lt;= n &gt;= 63
           KEY_DC          Delete character
           KEY_IC          Insert char or enter insert mode
           KEY_ENTER       Enter or send
</b></a></pre><a name="input">For a complete list read the man page of <code><b>getch()</b></code>.  
</a><p><a name="input"><b>Catch special keys.</b> To use these keys, you need to check the return  
value of <code><b>getch()</b></code>. For example </a></p><pre><a name="input"><b id="code">
     int ch = getch();
     switch (ch) {
          case KEY_BACKSPACE: /* user pressed backspace */ 
             ...
          case KEY_UP:  /* user pressed up arrow key */
             ...
          case KEY_DOWN:  /* user pressed up arrow key */
             ...
          case 'A' ....   /* user pressed key 'A' */
             ...
     }
</b></a></pre><a name="input"><b>Read character from a window.</b> The function <code id="code"><b>int  
wgetch(WINDOW *win)</b></code>. reads a key from a window. The user input of  
course comes from the keyboard and not the screen window. But the different  
windows on the screen might have different delay modes and other properties,  
therefore affect the behavior of <code id="code"><b>wgetch()</b></code>.  
</a><p><a name="input"><b>Moving the cursor and read a character.</b> There are also functions which  
combine cursor moving and character reading together </a></p><pre><a name="input"><b id="code">
       int mvgetch(int y, int x);
       int mvwgetch(WINDOW *win, int y, int x);
</b></a></pre><a name="input"> 
</a><p align="center"><a name="input"><img src="./Ncurses programming guide_files/slim.gif" height="7" width="100%"> </a></p><a name="output"> 
</a><h2><a name="output">Output</a></h2><a name="output">The function <code id="code"><b>int waddch(WINDOW * win, chtype  
ch)</b></code> adds a character on the window at the current cursor position,  
and the cursor position is advanced then.  
</a><p><a name="output"><b>Wrap.</b> If the new position of the cursor is out of the window, it wraps  
to the beginning of the next line.  
</a></p><p><a name="output"><b>Scroll.</b> If the next line is out of the window, and you have called  
<code id="code"><b>scrollok(win, TRUE)</b></code> when the window was created, the  
stuff in the window is scrolled up one line.  
</a></p><p><a name="output"><b>Character attribute.</b> The parameter <code id="code"><b>ch</b></code> is  
of type <code id="code"><b>chtype()</b></code>, which is the ASCII value of the  
character combined with some video attributes such as colors. The combination is  
through the logical <tt><b>OR</b></tt> of the character value and the attribute,  
which I will talk about in the section.  
</a></p><p><a name="output"><b>Refresh.</b> After a call to <code id="code"><b>waddch</b></code>, the  
screen is not updated until you call <code id="code"><b>wrefresh(win)</b></code>.  
 
</a></p><h4><a name="output">Ohter output functions</a></h4><a name="output"> 
</a><p><code id="code"><a name="output"><b>mvwaddch(win, y, x, ch);</b></a></code><a name="output"> is equivalent to <code id="code"><b>wmove(win, y, x); waddch(win, ch);</b></code>  
</a></p><p><code id="code"><a name="output"><b>addch(ch);</b></a></code><a name="output"> is equivalent to <code id="code"><b>waddch(stdscr, ch);</b></code>.  
</a></p><p><code><a name="output"><b id="code">wechochar(win, ch);</b></a></code><a name="output"> function and <code><b id="code">echochar(ch)</b></code> are equivalent to <code id="code"><b>waddch(win,  
ch); wrefresh(win);</b></code> and <code id="code"><b>addch(ch);  
refresh();</b></code> respectively. But <code id="code"><b>echochar</b></code> and  
<code id="code"><b>wechochar</b></code> may be more efficient.  
</a></p><p><code id="code"><a name="output"><b>int waddstr(WINDOW *win, const char *str)</b></a></code><a name="output"> and  
<code id="code"><b>int addstr(const char *str)</b></code> prints a null-terminated  
string at the cursor position of the window, and advance the cursor position  
accordingly.  
</a></p><p><a name="output">The functions <code id="code"><b>int wprintw(WINDOW *win, char *fmt  
...)</b></code> and <code id="code"><b>int printw(char *fmt ...)</b></code> do  
formatted output in the same fashion as the analogous standard library function  
<code id="code"><b>printf</b></code>.  
</a></p><p align="center"><a name="output"><img src="./Ncurses programming guide_files/slim.gif" height="7" width="100%"> </a></p><a name="attribute"> 
</a><h2><a name="attribute">Attribute</a></h2><a name="attribute">When characters are drawn on the screen some special video  
effects, like <i>foreground and background </i><i>color</i>, <i>highlight</i>,  
<i>underline</i>, <i>blinking</i>, ..., can be shown. Such video effects are  
represented by integers called text attributes. Each significant bit of the  
attribute corresponds to one video effect.  
</a><h4><a name="attribute">Using attribute</a></h4><a name="attribute">There are two ways to use attribute. One is by passing  
<code id="code"><b>waddch(win, ch)</b></code> a character value combined with  
attribute. The other is setting the global window attribute.  
</a><p><a name="attribute"><b>Character type.</b> When calling <code id="code"><b>waddch(win,  
ch)</b></code> or <code id="code"><b>addch(ch)</b></code>, logical  
<tt><b>OR</b></tt> the character value with the attribute. For example, <code id="code"><b>A_UNDERLINE</b></code> is the predefined attribute for underlining.  
To print the character <b>'X'</b> with underlining, do </a></p><pre><a name="attribute"><b id="code">
     waddch(win, 'X' | A_UNDERLINE);
</b></a></pre><a name="attribute">Using several attributes is of course possible. For example, to To  
print the character <b>'X'</b> with highlight in color pair 3 </a><pre><a name="attribute"><b id="code">
     waddch(win, 'X' | A_UNDERLINE | COLOR_PAIR(3));
</b></a></pre><a name="attribute"> 
</a><p><a name="attribute"><b>Setting window attribute.</b> <code id="code"><b>int wattron(WINDOW *win,  
int attr)</b></code> function to turn on an attribute <code id="code"><b>attr</b></code>. Then anything printed by subsequent calls to <code id="code"><b>waddch</b></code>, <code id="code"><b>addstr</b></code> and <code id="code"><b>waddstr</b></code> will have the attribute <code id="code"><b>attr</b></code>, For example, to print a highlighted message on the  
screen </a></p><pre><a name="attribute"><b id="code">
     attron(A_STANDOUT);
     addstr("I am highlighted!\n");
</b></a></pre><a name="attribute"><b>Predefined attributes.</b> Here is some attributes defined in  
ncurses.h </a><pre><a name="attribute"><b id="code">
        A_NORMAL        Normal display (no highlight)
        A_STANDOUT      Best highlighting mode of the terminal.
        A_UNDERLINE     Underlining
        A_REVERSE       Reverse video
        A_BLINK         Blinking
        A_DIM           Half bright
        A_BOLD          Extra bright or bold
        A_PROTECT       Protected mode
        A_INVIS         Invisible or blank mode
        A_ALTCHARSET    Alternate character set
        A_CHARTEXT      Bit-mask to extract a character
        COLOR_PAIR(n)   Color-pair number n
</b></a></pre><a name="attribute"> 
</a><h4><a name="attribute">Using colors</a></h4><a name="attribute">The combination of foreground and background color is an  
attribute. Unlike other attributes, before using colors, you must call <code id="code"><b>start_color()</b></code>.  
</a><p><a name="attribute">When <code id="code"><b>start_color()</b></code> is called, a set of  
<i>colors</i> and <i>color pairs</i> are created which you can use. The number  
of available colors and the number of the color pairs are stored in two global  
variables <code id="code"><b>COLORS</b></code> and <code id="code"><b>COLOR_PAIRS</b></code>. To use an predefined color pair as an  
attribute, you need to cal the macro <code id="code"><b>COLOR_PAIR(n)</b></code>,  
where <tt><b>n</b></tt> must satisfy </a></p><pre><a name="attribute"><b>
     0 &lt;= n &lt; COLORS
</b></a></pre><a name="attribute"><b>Example.</b> To give a window the color attribute defined by color  
pair #2, so that each subsequent character printed in this window has the foreground 
and background color defined by color pair #2 </a><pre><a name="attribute"><b id="code">
    wattron(win, COLOR_PAIR(2));
</b></a></pre><a name="attribute">The meaning of a color pair can be redefined. For example </a><pre><a name="attribute"><b id="code">
     init_pair(1,2,0);
</b></a></pre><a name="attribute">redefine the color pair #1 with foreground color #2 and background  
color #0. In the function <code><b id="code">int init_pair(short n, short f, short  
b)</b></code> the parameters must satisfy </a><pre><a name="attribute"><b id="code">
    0 &lt;= n &lt; COLORS  
    0 &lt;= f &lt; COLOR_PAIRS  
    0 &lt;= b &lt; COLOR_PAIRS  
</b></a></pre><a name="attribute"> 
</a><p><a name="attribute">When <code><b id="code">start_color()</b></code> is called, 8 basic colors are  
initialized </a></p><pre><a name="attribute"><b id="code">
        COLOR_BLACK
        COLOR_RED
        COLOR_GREEN
        COLOR_YELLOW
        COLOR_BLUE
        COLOR_MAGENTA
        COLOR_CYAN
        COLOR_WHITE
</b></a></pre><a name="attribute">You can use these names in <code><b id="code">init_pair()</b></code> for  
specifying foreground and background color.  
</a><p><a name="attribute">To find out what foreground color and background color is used by a color  
pair, use the function <code><b id="code">int pair_content(short pair, short *f,  
short *b)</b></code>. To find out the definition of a color use the function  
<code><b id="code">int color_content(short color, short *r, short *g, short  
*b)</b></code>  
</a></p><p><a name="attribute">Color can also be redefined by <code><b id="code">int init_color(short n, short  
r, short g, short b)</b></code>, where n is the index of color, must be less  
than COLORS. r, g, and b represent the intensity of red, green and blue. Each  
value of r, g and b must be less than 1000.  
</a></p><h4><a name="attribute">Line graphics</a></h4><a name="attribute">Line graphics. Here are some special characters which can  
be used in addch and addstr routines as the chtype. </a><pre><a name="attribute">       ACS_BLOCK               solid square block
       ACS_BOARD               board of squares
       ACS_BTEE                bottom tee
       ACS_BULLET              bullet
       ACS_CKBOARD             checker board (stipple)
       ACS_DARROW              arrow pointing down
       ACS_DEGREE              degree symbol
       ACS_DIAMOND             diamond
       ACS_GEQUAL              greater-than-or-equal-to
       ACS_HLINE               horizontal line
       ACS_LANTERN             lantern symbol
       ACS_LARROW              arrow pointing left
       ACS_LEQUAL              less-than-or-equal-to
       ACS_LLCORNER            lower left-hand corner
       ACS_LRCORNER            lower right-hand corner
       ACS_LTEE                left tee
       ACS_NEQUAL              not-equal
       ACS_PI                  greek pi
       ACS_PLMINUS             plus/minus
       ACS_PLUS                plus
       ACS_RARROW              arrow pointing right
       ACS_RTEE                right tee
       ACS_S1                  scan line 1
       ACS_S3                  scan line 3
       ACS_S7                  scan line 7
       ACS_S9                  scan line 9
       ACS_STERLING            pound-sterling symbol
       ACS_TTEE                top tee
       ACS_UARROW              arrow pointing up
       ACS_ULCORNER            upper left-hand corner
       ACS_URCORNER            upper right-hand corner
       ACS_VLINE               vertical line
</a></pre><a name="attribute">Usually on terminals using these symbols can draw pretty windows and  
shapes. One place to use this is the <code><b id="code">wborder</b></code>  
function, which draws borders for a window. See the man page for details about  
the parameters, but usually do it the following way </a><pre><a name="attribute"><b id="code">
     wborder(win, 0, 0, 0, 0, 0, 0, 0, 0);
</b></a></pre><a name="attribute">will make a good looking window.  
</a><p><a name="attribute">To draw a horizontal line across the window, do </a></p><pre><a name="attribute"><b id="code">
     whline(win, ACS_HLINE, ncolumns);
</b></a></pre><a name="attribute"> 
</a><p align="center"><a name="attribute"></a></p><hr><a name="attribute"> </a><p></p><a name="xterm"> 
<h2>X window</h2>If an xterm is resized the contents on your text windows might  
be messed up. To handle this gracefully you should redraw all the stuff based on  
the new height and width of the screen. When resizing happens, your program is  
sent a <tt><b>SIGWINCH</b></tt> signal. You should catch this signal and do  
redrawing accordingly. Here is some hint. <pre><b><code>
     #include &lt;signal.h&gt;
     void* resizeHandler(int);

     int main(void) {
          ...
          signal(SIGWINCH, resizeHandler);
          ...
     }

     void* resizeHandler(int sig)
     {
          int nh, nw;
          getmaxyx(stdscr, nh, nw);  /* get the new screen size */
          ...
     }
</code></b></pre> 
<p align="center"></p><hr> <p></p></a><a name="example"> 
<h1>Examples</h1></a><a href="http://jbwyatt.com/ncursesCode/">This</a> is a program for testing typing speed,  
which was never finished. It's usable but may need some refinement.  
<p align="center"></p><hr> <p></p> 
<p align="center"><a href="http://publish.uwo.ca/">from uwo.ca
</a></p> 

```
