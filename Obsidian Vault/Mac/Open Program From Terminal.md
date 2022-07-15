# Open Program From Terminal
#mac #terminal

https://apple.stackexchange.com/questions/25844/can-i-open-files-in-textedit-from-the-terminal-in-mac-os-x

`open -a TextEdit filename` should do the trick.

The `-a` flag specifies any application you want, so it's applicable to any number of situations, including ones where TextEdit isn't the default editor.

### Other relevant options

-   `-t` opens in the default editor (i.e. if you use BBEdit, TextMate, etc.)
-   `-e` will open the file specifically in TextEdit