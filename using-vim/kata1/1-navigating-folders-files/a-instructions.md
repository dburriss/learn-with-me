# Navigating folders and files (1/3)

Congratulations on your first steps to mastering Vim.  
An important part of understanding Vim is knowing that it has this concept of MODES. 
In total there are 7 modes at the time of writing this. 
We will not introduce all of these modes in the kata but each mode will be introduced the first time it is encountered.

> Tip: You can press ESC to get back to NORMAL mode if you mistakenly get into another MODE.

When Vim opens it is in NORMAL mode. Vim is about manipulating documents, not only about typing text. I don't want to get into this too much but it explains why NORMAL mode is the default. In normal mode you can navigate around and manipulate the document. This does not include INSERTING text character by character. We will get to that in another mode.

You opened this file by telling Vim to open it directly with the command `vim <file>`. We will now navigate while in Vim by using the built-in file explorer (netrw). This allowes us to use our arrow keys to navigate up and down files and folders and the ENTER key to go into a folder or open a file.

## Instructions

> Note: I am going to explain what to do before giving you the command since this command will launch a new window and you will no longer see the instructions.

After executing the command to launch netrw use **ENTER** to select a file or folder. 
Navigate: b-instructions.md

> Tip: In NORMAL mode press Ctrl-o to navigate back to a previous cursor's point in time.

Clear what to do once the command is executed? **Type the following in VIM**: `:Ex`

Navigate to *1-navigating-files-folders/b-instructions.md* and hit enter.
