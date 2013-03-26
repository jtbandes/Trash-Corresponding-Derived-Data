Trash-Corresponding-Derived-Data
================================

A Folder Action which automatically trashes derived data (build products) when you move an Xcode project to the Trash.

If the items you move to the Trash contain any `.xcodeproj` files, then any folders in DerivedData that have the same name will also be moved to the Trash. 

### To download:
Click on either the `.zip` file or the `.xip` file (a signed archive for Mountain Lion and up)!

## Demo

![demo](http://i.imgur.com/chEig.gif)

## The script

For the paranoid, here is the script used to find the derived data folders (you can also open the folder action in Automator to see how it works):

    DATADIR=~/Library/Developer/Xcode/DerivedData
    
    # bail early if there is no DerivedData directory
    if [ ! -d "$DATADIR" ]; then exit 0; fi
    
    # find any Xcode projects
    for PROJ in $(find "$@" -name "*.xcodeproj")
    do
      # find corresponding build output folders
      find "$DATADIR" -maxdepth 1 -type d -name "$(basename "$PROJ" .xcodeproj)-*" -print
    done
