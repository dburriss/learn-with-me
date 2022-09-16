# Editing files (3/3)

In this last section we are going to look at searching for text and replacing.

## Instructions

### Searching

1. Switch to text.md using `Ctrl+w,w`
2. Press `gg` to send the cursor to the start of line 1.
3. Type `/4` like you would execute a command. Then press `n` to cycle to next occurance. You can use `N` to cycle to previous occurance. The reason we went to the start of the file is because `/` searches for the pattern from the cursor. You can use `?` to search backward from the cursor.

### Replacing

4. Run the command `:%s/Hydro/Hydroelectric`. The `%` indicates the range is the whole file.
5. Run `:w` to save your changes.

> Tip: :[range]s/{pattern}/{string}/[flags] [count] 

### Cleaning up

6. Close text.md by running `:close`.
7. Run `:Ex` and navigate to text.md but do not open it.
8. Press `D` (`Shift+d`) and when asked if you want to delete the file type `y`.

Thats it! You finished the 1st kata.