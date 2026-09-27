# Column Relative Paths

When editing with Anvil, sometimes you may have many files open in different directories, perhaps on different hosts. In those situations the long pathnames in the window tags combined with the high number of windows makes it difficult to distinguish between files at a glance. To help unclutter the view, Anvil allows you to set directory path in a column tag, after which you can use relative paths as the paths of the windows in that column. The relative window paths are relative to the column path and so much shorter and tidier.

In more detail, to set a column relative path do the following:

1. Click the leftmost position in the column tag so that your cursor is left of the word 'New'
2. Type or paste an absolute path to a directory, followed by space so that there is a space between the column path and 'New'.

Once you've set a column path, you can open new windows that are relative to that directory by typing or pasting a path relative to that directory at the end of the column tag or at the end of any window tag in that column and then acquiring it. If you open the path '.' (the current directory) it opens the column's directory.

If you already have windows in the column before you set the relative path, they are not automatically made relative to the column path. Instead, you can run the command `Rel` in the column and it will make the window paths relative to the column path. Alternately, if you Get a window in the path (using the Get command or CTRL-G), the path is made relative. If you drag a window from the column to another column that does not have a path set, or has a different path set, that window's path is made absolute or relative to the new directory respectively.

## Demo Video

This video demonstrates the use of column-relative paths. We start with a file open on a remote host with a very long path name. We cut the directory part of the file including the remote host information, and paste it into the initial part of the column tag followed by a space. Then we Get the window to note that Anvil does in fact load the window using the relative path. Next we open the directory `.` which is relative to the column's path, showing the contents of the directory and open a few more files. Finally we create a new column and drag a window to that column and back, showing the window's path changing to absolute and back to relative.

![type:video](../../img/anvil-tut-col-rel-paths.mp4)

