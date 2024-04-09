# Vi Commands

## 1. Opening a file

To open a file in the vi editor, use the following command:

**_vim filename_**

This command opens the specified file in the vi editor. If the file does not exist, a new file with that name will be created.

This command opens the specified file in the vi editor. If the file does not exist, a new file with that name will be created.

## 2. Switching to command mode

When you open a file in vi, you start in command mode. In this mode, you can issue commands to navigate and edit the file. To switch to command mode from insert mode (explained later), press the `Esc` key.

## 3. Saving and quitting

- **:w**: Save the changes made to the file (write). This command writes the changes to disk but does not quit vi. You can continue editing the file.
- **:q**: Quit the vi editor. If there are no unsaved changes, vi will exit immediately. If there are unsaved changes, vi will display an error message and refuse to quit.
- **:wq**: Save the changes and quit. This command combines the `:w` (write) and `:q` (quit) commands, allowing you to save the changes made to the file and exit vi simultaneously.
- **:q!**: Quit vi without saving changes.

It's important to note that in vi, you need to be in command mode (press `Esc`) before using these commands. Also, if you're in insert mode, you can switch back to command mode by pressing `Esc`.

## 4. Inserting and editing text

- **i**: Switch to insert mode. This allows you to start entering text at the current cursor position.
- **a**: Switch to insert mode and move the cursor one character to the right.
- **o**: Open a new line below the current line and switch to insert mode.
- **O**: Open a new line above the current line and switch to insert mode.
- **x**: Delete the character at the current cursor position.
- **dd**: Delete the current line.

## 5. Moving the cursor

- **h**: Move the cursor one character to the left.
- **j**: Move the cursor one line down.
- **k**: Move the cursor one line up.
- **l**: Move the cursor one character to the right.
- **0**: Move the cursor to the beginning of the current line.
- **$**: Move the cursor to the end of the current line.
- **gg**: Move the cursor to the first line of the file.
- **G**: Move the cursor to the last line of the file.

These commands should give you a good starting point for using vi. As you become more familiar with the editor, you can explore additional commands and features.
