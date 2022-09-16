# Buffers (2/2)

We have mentioned buffers and files and windows. Let's take a look at why there is actually a distinction here.

## Instructions

1. Run the motion `Ctrl+w, s` to create a new window in VIM split horizontally. You could also use the command `:split path/to/file` where the file is optional, to open a specific file.
2. Use the motion `Ctrl+w, w` to toggle between the windows.
3. Use `:bn` to change the current buffer of the currently active window (use `:e 1-navigating-files-folders/a-instructions.md` if you need another buffer).
4. Use the motion `Ctrl+w, v` to create a new window split vertically with the current window.
5. Use the motion `Ctrl+w, r` to move the current window to the right. You could also use the command `:vsplit path/to/file`.
6. Use motion `Ctrl+w, c` or `:close` on all open windows except this one (`:q` works too but `:close` command won't exit VIM if it is the last window).

> Tip: If you have multiple open windows instead of toggling you can use movement keys `h`, `j`, `k`, `l` with the window motion eg. `Ctrl+w, j` to move down. You can also use arrow keys if that is easier.

7. Navigate to *4-editing-files/a-instructions.md*