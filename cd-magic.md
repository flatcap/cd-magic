# CD Magic

Change directory (etc)

## CD - Change Directory

| Command                  | Equivalent to        | Description                                                |
| :----------------------- | :------------------- | :--------------------------------------------------------- |
| cd                       | cd "$HOME"           | Change to home directory (unless a saved directory exists) |
| cd DIR                   | cd DIR               | Change directory                                           |
| cd "DIR WITH SPACES"     | cd "DIR WITH SPACES" | Change directory                                           |
| cd .                     |                      | No operation                                               |
| cd PATH/TO/FILE          | cd PATH/TO           | Change to file's directory                                 |
| cd FILE                  |                      | No operation                                               |
| cd LINK -> PATH/TO/DIR   | cd LINK              | Change directory following symlink                         |
| cd LINK -> .             |                      | No operation                                               |
| cd LINK -> PATH/TO/FILE  | cd PATH/TO           | Change to directory of symlinked file                      |
| cd LINK -> ./FILE        |                      | No operation                                               |

## Fake Directories

| Command | Equivalent to | Description                            |
| :------ | :------------ | :------------------------------------- |
| cd ..   | cd ..         | Change to parent directory             |
| cd ...  | cd ../..      | Change to grand-parent directory       |
| cd .... | cd ../../..   | Change to great-grand-parent directory |
| etc     |               | and so on...                           |

## History

| Command | Description                       |
| :------ | :-------------------------------- |
| cd -l   | List cd history                   |
| cd -    | Change to previous directory      |
| cd -1   | Change to previous directory      |
| cd -2   | Change to directory 2 changes ago |
| cd -3   | Change to directory 3 changes ago |
| etc     | and so on...                      |

History is de-duplicated

## List

| Command               | Description                                                |
| :-------------------- | :--------------------------------------------------------- |
| cd DIR1 DIR2 DIR3 ... | Set the cd list to these directories (and cd to the first) |
| cd -l                 | Show cd list                                               |
| cd +                  | Change to next directory                                   |
| cd +1                 | Change to next directory                                   |
| cd +2                 | Change to directory 2 ahead in the list                    |
| cd +3                 | Change to directory 3 ahead in the list                    |
| etc                   | and so on...                                               |
| cd -n                 | Change to next directiory                                  |
| cd -p                 | Change to previous directiory                              |
| cd -x                 | Exit the cd list                                           |

alias n='cd -n'
alias p='cd -p'

List is fixed and loops around

## Save Place

| Command    | Description                               |
| :--------- | :---------------------------------------- |
| cd -s      | Save my place, here                       |
| cd -s .    | Save my place, here                       |
| cd -s DIR  | Change directory and save my place, there |
| cd -s ~    | Unset my saved place                      |

## Git

| Command       | Description          |
| :------------ | :------------------- |
| cd GIT_BRANCH | Checkout git branch  |

## Misc

| Command  | Equivalent to | Description                      |
| :------- | :------------ | :------------------------------- |
| cd DIRls | cd DIR; ls    | cd then ls (typo workaround)     |
| cd -d    | cd $(pwd -P)  | Dereference symlinks in the path |

## Aliases

| Alias  | Command     |
| :----- | :---------- |
| /      | cd /        |
| ~      | cd ~        |
| . FILE | source FILE |
| .      | cd .        |
| ..     | cd ..       |
| ...    | cd ../..    |
| ....   | cd ../../.. |

## Environment

| Variable       | Description                                        |
| :------------- | :------------------------------------------------- |
| CD_DIR_LIST    | Current directory list                             |
| CD_HISTORY     | Directory history                                  |
| CD_HISTORY_MAX | Maximum number of entries in the directory history |
| CD_LS_COMMAND  | Command to run after "cd DIRls"                    |
| CD_SAVE_DIR    | Current "saved" directory                          |

