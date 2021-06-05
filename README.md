# GoDebug

[Delve](https://github.com/derekparker/delve) plugin for Sublime Text 3.

Based on ideas and sources:
* [SublimeGDB](https://github.com/quarnster/SublimeGDB)
* [go-debug](https://github.com/lloiser/go-debug)
* [jsonrpctcp](https://github.com/joshmarshall/jsonrpctcp)

This fork is based on [dishmaev v0.3.9](https://github.com/dishmaev/GoDebug) and has following improvements:
* adresses of all variables is showing; this includes the pointer adresses and adresses of the underlying value/object
* increase the default limit of DLV configuration, so more level of struct recursion and larger string will shown in the variable view
* if a string is cutted because of maxStringLen (current 128) is reached, a `@` will mark the end of the string
* underlying values of pointers wil also shown in the variable view
* `time.Time` objects will shown the timestamp in the format `YYYY-MM-DD HH:MM:SS`
* if a variable is currently not readable (by the process) a notification will shown as variable value
* shows `nil` on pointer, interfaces, channels, functions
* disable word_wrap for all debugger views
* use smaller font for all debugger views

## Installation
Only manually clone git repository [GoDebug](https://github.com/codeproducer198/GoDebug.git) in your package directory.
For a Linux system it can be `/home/<user-hone>/.config/sublime-text-3/Packages` and do a `git clone https://github.com/codeproducer198/GoDebug.git`.

## Enable plugin for your project
1. On active view of window right click mouse and choose from menu Delve/Enable (not recommended, if your project file contains necessary commented lines, after execution Sublime Text will remove all commented content)
2. Manually put specific setting in project file *\<YourGoProject\>.sublime-project*
```
"settings":
{
  ...
  "delve_enable": true
  ...
}
```

## Usage
See [the default key bindings](https://github.com/dishmaev/GoDebug/blob/master/Default.sublime-keymap), [the default mouse map](https://github.com/dishmaev/GoDebug/blob/master/Default.sublime-mousemap) and [the sample setting](https://github.com/dishmaev/GoDebug/blob/master/GoDebug.sublime-settings).

In short:
* If you have multiple projects, you most likely want to put project specific setting in your project file, with a prefixed "godebug_"
* If you have multiple executables in the same project, you can add a "godebug_executables" setting to your project settings, and add an entry for each executable's settings
* Toggle breakpoints with Alt+F9
* Launch with F5
* Next with F6
* Step into with F7
* Step out with Shift+F7
* Click on the appropriate line in the Delve Stacktrace view to go to that stack frame. Deactivated by default, see [the mouse map](https://github.com/dishmaev/GoDebug/blob/master/Default.sublime-mousemap) for details
* Click a variable in the Delve Variables view to show its children (if available).Deactivated by default, see [the mouse map](https://github.com/dishmaev/GoDebug/blob/master/Default.sublime-mousemap) for details
* You can also access some commands by right clicking in any view

## License
GoDebug are released under the MIT license. See [LICENSE](https://github.com/dishmaev/GoDebug/blob/master/LICENSE)

## Better layout

For a better layout of your code/variables you can change it in your `GoDebug.sublime-settings` with following overriding with 2 columns and 3 rows:

	,"panel_layout": {  "cols": [0.0, 0.50, 1.0],				// 2 spalten: links (0.50), rechts (0.50)
                        "rows": [0.0, 0.15, 0.80, 1.0],			// 3 zeilen: console (0.15), hauptfenster (0.80), breakpoints (0.20)
                        "cells":
                        [
                            [0, 0, 2, 1],	// 0: outline und dlv-console oben ueber ganze breite
                            [0, 1, 1, 3],	// 1: source code links
                            [1, 1, 2, 2],	// 2: rechts oben (variablen, watches, stack)
                            [1, 2, 2, 3] 	// 3: rechts unten (breakpoints, session, goroutine)
                        ] }
