# Install brew

```sh
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

# .bashrc
```sh
export PS1="\e[01;36m\][\t] ${debian_chroot:+($debian_chroot)}\u@\h\[\e[01;35m\]:\w\n\[\e[01;33m\]$\[\e[00m\] "

export HF_ENDPOINT=https://hf-mirror.com

alias n='nvidia-smi'
alias nvi='watch -n 0.1 nvidia-smi'
alias nvfind='fuser -v /dev/nvidia*'

alias sdi='sudo dpkg -i'
alias l='ls -alF -h'
alias d='du -h --max-depth 1'
alias cb='cat ~/.bashrc'
alias vb='vi ~/.bashrc'
alias sb='source ~/.bashrc'
alias sc='screen'
alias cc='/home/user/opt/clash/clash -d /home/user/opt/clash'
alias tat='tmux a -t'
alias tl='tmux ls'
alias jfu='journalctl -f -u'

function psfind() {
        ps aux | head -n 1
        ps aux | grep -E $1 | grep -v grep
}
function sp() {
        export http_proxy=http://127.0.0.1:7891
        export HTTP_PROXY=http://127.0.0.1:7891
        export https_proxy=http://127.0.0.1:7891
        export HTTPS_PROXY=http://127.0.0.1:7891
        export all_proxy=socks://127.0.0.1:7891
        export ALL_PROXY=socks://127.0.0.1:7891
        echo 'set proxy'
}
function usp() {
        unset http_proxy
        unset HTTP_PROXY
        unset https_proxy
        unset HTTPS_PROXY
        unset all_proxy
        unset ALL_PROXY
        echo 'unset proxy'
}

# >>> conda initialize >>>
CONDA_PATH=/home/**/opt/miniconda3
BIN_PATH=$CONDA_PATH/bin/conda
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$($BIN_PATH 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "$CONDA_PATH/etc/profile.d/conda.sh" ]; then
        . "$CONDA_PATH/etc/profile.d/conda.sh"
    else
        export PATH="$CONDA_PATH/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```