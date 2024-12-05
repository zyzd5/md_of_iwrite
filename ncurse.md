```cc
WINDOW *initscr();
int endwin();

keypad(WINDOW *window, bool);
// KEY_UP ... 

SCREEN *newterm();

cbreak();                 // 1 or 0
nocbreak();               // 1 or 0

echo();                 // 1 or 0
noecho();               // 1 or 0

// color 
int start_color();      // 1 or 0
bool has_colors();       // true or false

int init_pair(short pair_number, short foreground, short background);
// pair_number: 1-32767
/*
    foreground
    background
    COLOR_BLACK
    COLOR_RED ... 
*/ 

attron(int COLOR_PAIR);
attroff(int COLOR_PAIR);

int init_color(short COLOR, short r, short g, short b);
```
