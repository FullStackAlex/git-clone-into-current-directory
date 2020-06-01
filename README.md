# git-clone-into-current-directory

Clone a repository into current directory without creating a new parent folder.

#Usage:
```bash
cd /Users/you/path/to/repo
git-clone-into-current-directory git@github.com:Tech-Nomad/git-clone-into-current-directory.git
```
#Code

Put the following function into your bash config file in ~/.bash_profile or ~/.bashrc
```bash
git_clone_into_current_directory() {

  #seconds to wait before processing
  timeout=5
  #Number of expected characters (y/n + Enter)
  number=2
  url=$1
  prompt="this will move anything in this directory into the bin. Proceed anyway? y/n   "
  read -p $prompt -n $number -t $timeout -a entered_key_sequence
  if [[ $entered_key_sequence =~ ^[Yy]$ ]]; then
    if [ -n "$1" ]; then
      #move everything in the current directory into the bin inside a folder named by the current date and time
      mkdir ~/.Trash/$( date +'%Y-%m-%d_%H-%M-%S')
      printf "\nMOVING FILES TO BIN:\n"
      mv -v ./* ~/.Trash/$( date +'%Y-%m-%d_%H-%M-%S')
      printf "\nCLONING REPOSITORY:\n"
      git clone $url .
      else
        printf "No URL provided\n"
    fi
  else
    printf "\nAborting...\n\n"
  fi
}
```
