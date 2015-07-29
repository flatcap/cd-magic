# CD Magic

Change directory (etc)

## CD - Change Directory

| Command          | Equivalent to | Description                |
| :--------------- | :------------ | :------------------------- |
| cd DIR           | cd DIR        | Change directory           |
| cd /PATH/TO/FILE | cd /PATH/TO   | Change to file's directory |

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

## Save Place

| Command    | Description                               |
| :--------- | :---------------------------------------- |
| cd -s      | Save my place, here                       |
| cd -s .    | Save my place, here                       |
| cd -s DIR  | Change directory and save my place, there |
| cd -s ~    | Unset my saved place                      |

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

## Configuration

CD_DIR_LIST
CD_HISTORY
CD_HISTORY_MAX
CD_LS_COMMAND
CD_SAVE_DIR

OPERATIONS
	cd
	list
	saved dir
	fake-dirs/redirection

--------------------------------------------------------------------------------
MAGIC CD

cd			cd "$HOME"
cd			cd "$CDDIR"

cd DIRECTORY		cd 'DIRECTORY'
cd DIR WITH SPACES	cd 'DIR WITH SPACES'

cd PATH/FILE		cd 'PATH'
cd ./FILE		cd .

cd LINK -> DIR		cd 'LINK'			prompt shows LINK
cd LINK -> .		NO-OP

cd LINK -> PATH/FILE	cd 'PATH'
cd LINK -> ./FILE	NO-OP

cd DIRls		cd 'DIR'; ls

cd .			cd $(pwd -P)			prompt shows REAL PATH

cd GIT_BRANCH		git checkout GIT_BRANCH
cd .			git checkout master


--------------------------------------------------------------------------------
cd ..ls -> cd ..; ls;
any "cd EXISTING_DIRls" -> cd EXISTING_DIR; ls
cd X -- automatically ls?

function cd()
{
	if [[ "$1" =~ "^\.\.+$" ]]; then
		builtin cd "$(echo $1 | sed -e 's/\.//' -e 's/\./..\//g')"
	else
		builtin cd "$@"
	fi
}

cd {git-branch}
	should cddir too
	git checkout branch

magic cd
	H = hikes
	W = work
	T = todo / torrent?
	P = public_html
	autocomplete on each dir

magic cd
	newly spawned dirs: should they inherit [H|W]?
	would have to descend dir hierarchy looking for a marker
	look for .cddir ?

what happens to duplicate entries?
what happens to list (a, b, c, d) after cd -; cd -; ?
	option to de-dupe or keep all

magic cd
in work mode, replace ~/docs with $WORKDIR/docs

bash complete cd
	check CDPATH
	fix to allow cd ./<tab> etc

fix cd autocomplete for cd ~/X/...

magic dirs
	"cd ~/docs" to mean "cd $WORK_DIR/docs"
	=> substitution before cd
	=> auto-completion needs to be work_dir aware

_cd_complete ()
{
	local cur
	_get_comp_words_by_ref cur
	DIR=${cur:-.}
	[ -d "$DIR" ] || DIR=${DIR%/*}
	echo
	echo DIR=$DIR
	find $DIR -maxdepth 1 ! -name . ! -name .git -type d | cut -b3- | sort -u
	# COMPREPLY=(
	# 	$(compgen -W "$(
	# 		git branch 2> /dev/null;
	# 		find . -maxdepth 1 ! -name . ! -name .git -type d | cut -b3- | sort -u
	# 	)" -- "$cur")
	# )
}
complete -F _cd_complete cd

cddir -n DIR
	set CDDIR, but don't change dir

cddir doesn't respect symlinks (as cd() does)

change CDPATH to include /mnt/space

cd with multiple args activates first/last behaviour