% Get powerline working with bash, vim and git integration
% 21/08/2018

Based on  
<https://fedoramagazine.org/add-power-terminal-powerline/> (initial setup)  
<https://leifmadsen.wordpress.com/2015/09/09/configuring-powerline-to-show-working-git-branch/> (for git integration)

Intended for/tested on Fedora (28)


## Installation

### for powerline
~~~
dnf install powerline powerline-fonts
~~~

### for vim 
~~~
dnf install vim-powerline
~~~

### for git integration (pip and python is obviously needed)
~~~
pip install powerline-gitstatus
~~~

## configuration

### for the bash prompt, add this snippet to your .bashrc
~~~
if [ -f `which powerline-daemon` ]; then
  powerline-daemon -q
  POWERLINE_BASH_CONTINUATION=1
  POWERLINE_BASH_SELECT=1
  . /usr/share/powerline/bash/powerline.sh
fi
~~~

### for powerline in vim, add this snippet to your .vimrc
~~~
"" For powerline
python3 from powerline.vim import setup as powerline_setup
python3 powerline_setup()
python3 del powerline_setup
set laststatus=2 " Always display the statusline in all windows
set showtabline=2 " Always display the tabline, even if there is only one tab
set noshowmode " Hide the default mode text (e.g. -- INSERT -- below the statusline)
set t_Co=256
~~~

### for git integration (show current branch in the bash prompt) 

#### first create a powerline config directory
~~~
mkdir -p ~/.config/powerline
~~~

#### next copy your systemwide powerline config file over to your local
~~~
cp /etc/xdg/powerline/config.json ~/.config/powerline/config.json
~~~

#### modify the local file (~/.config/powerline/config.json) - change *"theme": "default"* to *"theme": "default_leftonly"* under the "shell" part. As follows ("---" and "+++" should not actually be there, it's just indicating what to change):
~~~
}
"shell": {
"colorscheme": "default",
--- "theme": "default",
+++ "theme": "default_leftonly",
"local_themes": {
"continuation": "continuation",
"select": "select"
~~~
