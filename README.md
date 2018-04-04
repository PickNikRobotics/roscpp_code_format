# ROSCpp Code Format

Why waste your valuable development time formatting code manually when we are trying to build amazing robots?

The repo contains an auto formatting script for the [ROS C++ Style Guidelines](http://wiki.ros.org/CppStyleGuide).

## Setup

 * Install **clang_format**:

   ``sudo apt-get install -y clang-format-3.8``

 * Then symlink or copy in the root of your catkin workspace the file ``.clang-format``, located in this repo. You can save this file from [this link](https://raw.githubusercontent.com/davetcoleman/roscpp_code_format/master/.clang-format). For example, place it on your computer here:

   ``~/catkin_ws/.clang-format``

 * If you are interested in improving this configuration file, we recommend you checkout the git repo and symlink, e.g.:

   ``ln -s ~/roscpp_code_format/.clang-format ~/catkin_ws/.clang-format``

 * Now any file inside your catkin workspace will be formatted with the ROS style guidelines described in this config file

## Usage

You can run **clang_format** in several ways:

### Command Line

Format single file:

    clang-format-3.8 -i -style=file MY_ROS_NODE.cpp

Format entire directory recursively including subfolders:

    find . -name '*.h' -or -name '*.hpp' -or -name '*.cpp' | xargs clang-format-3.8 -i -style=file $1

### Emacs Editor Configuration

In your ``~/.emacs`` config file, add the following:

Format your source code if its in some directory such as the ``catkin_ws`` (feel free to change keywords catkin_ws):

```
(defun run-ros-clang-format ()
  "Runs clang-format on cpp,h files in catkin_ws/ and reverts buffer."
  (interactive)
  (and
   (string-match "/catkin_ws/.*\\.\\(h\\|cpp\\)$" buffer-file-name)
   (save-some-buffers 'no-confirm)
   (shell-command (concat "clang-format-3.8 -style=file -i " buffer-file-name))
   (message (concat "Saved and ran clang-format on " buffer-file-name))
   (revert-buffer t t t)
))
```

Set a keyboard shortcut to run, such as F12

    (global-set-key [f12] 'run-ros-clang-format)

### Atom Editor Configuration

Install the [clang-format](https://atom.io/packages/clang-format) package via the Atom package manager or ``apm install clang-format``.

In the package settings set ``clang-format-3.8`` as your executable and point 'Style' to your ``.clang_format`` file.

### Usage with Qt

To set up Qt Creator to use this clang formatting follow the instructions [here](http://doc.qt.io/qtcreator/creator-beautifier.html).

On the **Clang Format** Panel change the **Clang Format command** to 'clang-format-4.0'. After this, choose **Use predefined style: File**, and then create a soft link on the root of your files workspace (where all your code is) pointing to this file and with the same name (.clang-format).

It is recomended to deactivate the **Enable auto format on file save** option and create a [keyboard shortcut](http://doc.qt.io/qtcreator/creator-keyboard-shortcuts.html)

### Usage with Sublime

Installation Package Control in Sublime:

https://packagecontrol.io/installation

Configuration Clang format in Sublime:

https://github.com/rosshemsley/SublimeClangFormat/blob/master/README.md

### Usage with Visual Studio Code

Install the [c/c++ extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools).

Put the ``.clang-format`` file in your workspace.

Select ``Format Document`` in the right-click context menu, or use the shortcut ``Ctrl+Shift+I``.

This explanation and more [here](https://code.visualstudio.com/docs/languages/cpp#_code-formatting).

## Exceptions to clang-format

Occationally the auto formatting used by clang-format might not make sense e.g. for lists of items that are easier to read on separate lines. It can be overwritten with the commands:

```
// clang-format off
... some untouched code
// clang-format on
```

Use this sparingly though.
