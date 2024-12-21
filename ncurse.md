* see http://jbwyatt.com/ncurses.html

* `addstr` is puts() in c;
* `addch` is putc() in c;
* `napms($ms)` for nap

```cc
init_pair(1, COLOR_WHITE, COLOR_RED);
init_pair(2, COLOR_BLUE, COLOR_CYAN);

attron(COLOR_PAIR(1));
printw("white text");

attron(COLOR_PAIR(2));
printw("blue text");
```

```cc
getyx(win, row, col) ;
move(row, col);
getmaxyx(win, row, col);
```

