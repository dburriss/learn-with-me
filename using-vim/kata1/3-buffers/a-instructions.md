# Buffers (1/2)

When we have a VIM open it is showing us the contents of a buffer. A buffer is an in-memory representation of a text file. What do we mean by in-memory? As you change a file (which we will do in the next sequence of the kata), it is changed in the buffer but is not yet written to disk until you give the command to write the bufer to the file.

## Instructions

1. We can see the list of currently open buffers with the command `:ls`. This will list the files open. A #a marks the currently active buffer. The number allows us to refer to that buffer. `:files` gives the same result if that is easier to remember.
2. You can cycle through open buffers using `:bn` (buffer next) and `:bp` (buffer previous).
3. You can jump to a specific buffer using the number `b<number>` eg. `:b5`
4. You can also jump to a buffer by partially matching on filename eg. `:b nav`
5. Navigate to a buffer that is not this file and type `:bdelete` or you can use the number eg. `bdelete 5`
6. Run `:ls` again to see the deleted buffer is no longer listed. Note that this does not delete the file but rather the in-memory buffer. Changes will be lost though if not wrtten to the file.
7. Navigate to *3-buffers/b-instructions.md*