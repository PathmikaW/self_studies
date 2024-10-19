# This is a heading

**This text is bold** and *this text is italic*.

- This is a list item.

# install screen copy on mac(scrcpy)

- brew install scrcpy
- brew install android-platform-tools
- Once installed, run from a terminal:
            scrcpy
- or with arguments (here to disable audio and record to file.mkv):
        scrcpy --no-audio --record=file.mkv
- man scrcpy
- scrcpy --help
https://github.com/Genymobile/scrcpy/blob/master/doc/macos.md


# cd /Applications
Absolute Path: The / at the beginning indicates the root directory of the system.
This command navigates to the /Applications folder, which is a system-wide directory that contains applications installed on your Mac.
It works no matter where you are in the file system, as it specifies the full path.

# cd Applications
Relative Path: Without the /, this command refers to a directory named "Applications" relative to your current working directory.
This only works if there’s an Applications folder in the current directory you're in. For example, if you are in /Users/yourusername/, this will navigate to /Users/yourusername/Applications, if such a folder exists.
If there’s no "Applications" folder in your current directory, you'll get an error

# /Applications is the absolute path to the system-wide applications folder.
# Applications is a relative path and depends on where you currently are in the file system.

# open the mac terminal 

    - Right-click in Finder: Select "New Terminal at Folder".
    - Drag folder into Terminal: Opens that folder in Terminal.
    - Custom Keyboard Shortcut: Use Automator to create a shortcut for opening Terminal.
    - Use Go2Shell App: Adds a button in Finder to open Terminal directly.



