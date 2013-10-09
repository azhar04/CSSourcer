CSSourcer
=========

CSSourcer is a program that will simplify the process of bundling and minification.

The steps it takes to create a single CSS file is as follows:

Given a folder, it will read the folder and all subfolders and then

- Delete all files ending with `.less.css` (if any)
- Compile all LESS files (if any) generating `.less.css` files
- Read all CSS files and resolve references (if any), bundling as needed
- If the config is set as `Release` it will be minified, otherwise it will
  generate a single CSS file without minification other than newline removal
  
Usage syntax:

    <Mode> <StyleFolder-1> <OutputPath-1> [<StyleFolder-N> <OutputPath-N>]
  
Example (the project is configured to do this when you run in Debug/Release):

    Debug   "..\..\Example\Input\\" "..\..\Example\Output\all.css"
    Release "..\..\Example\Input\\" "..\..\Example\Output\all.css"

In the example:

    000-test.less            -> references -> subfolder\002-test.less
    subfolder\002-test.less  -> references -> ..\001-test.less
    001-test.less            -> references -> null
    normal.css               -> references -> null
  
When bundling, instead of the order of the files in the folder, the output will be:

    001-test.less contents
    002-test.less contents
    000-test.less contents
    normal.css    contents

To add references, put at the top of the file

    /// <reference path="path.less" />


You don't need to use LESS if you don't want to, you can use purely CSS.
