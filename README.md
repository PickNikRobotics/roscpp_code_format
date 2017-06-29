# ROS cpp format for PAL robotics

This repo contains an auto formatting script for the [ROS C++ Style Guidelines](http://wiki.ros.org/CppStyleGuide) with some
minor adjustments for our style guidelines.

## Clang dependency

This clang format file uses clang-format-4.0
`sudo apt-get install clang-format-4.0`

## Usage with Qt

To set up Qt Creator to use this clang formatting follow the instructions [here](http://doc.qt.io/qtcreator/creator-beautifier.html).

On the **Clang Format** Panel choose **Use predefined style: File**, then create a soft link on the root of your workspace pointing to this
file. It is recomended to deactivate the **Enable auto format on file save** option and create a [keyboard shortcut](http://doc.qt.io/qtcreator/creator-keyboard-shortcuts.html)
to format the files.


## Usage with Sublime
Installation Package Control in Sublime:

https://packagecontrol.io/installation

Configuration Clang format in Sublime:

https://github.com/rosshemsley/SublimeClangFormat/blob/master/README.md
