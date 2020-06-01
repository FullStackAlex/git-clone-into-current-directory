Clone a repository into current directory without creating a new parent folder.

Just put the following function into your bash config file in ~/.bash_profile or ~/.bashrc and source the config file or restart terminal (tab)
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

# Usage example:
```bash
cd /Users/you/path/to/repo
git-clone-into-current-directory git@github.com:Tech-Nomad/git-clone-into-current-directory.git
```

# Autocompletion:
To avoid writing out the whole function name just type `git_clone` and then press the Tab key twice to print the full function name (or a list of bash functions/commands starting with "git_clone"). 
