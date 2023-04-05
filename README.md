
# Linux Hacks on Ubuntu 22.10

## Creating a linux bootable cd on linux

Several tools exist but many either dont work or have poor documention. 
GUI tool [`gnome-multi-writer`](https://linuxconfig.org/how-to-make-a-bootable-usb-from-an-iso-in-linux) 
is easy and direct to use. Install as 

```bash
$ sudo apt install gnome-multi-writer
```

## Two-line kali linux prompt 

To have the kali linux prompt, across 2 lines;

1. create this file in the home folder
2. modify the bashrc file


###  ~/.bashrc_kali_linux_prompt

```bash
# The following block is surrounded by two delimiters.
# These delimiters must not be modified. Thanks.
# START KALI CONFIG VARIABLES
PROMPT_ALTERNATIVE=twoline
NEWLINE_BEFORE_PROMPT=yes
# STOP KALI CONFIG VARIABLES

# override default virtualenv indicator in prompt
VIRTUAL_ENV_DISABLE_PROMPT=1

prompt_color='\[\033[;32m\]'
info_color='\[\033[1;34m\]'
prompt_symbol=㉿
if [ "$EUID" -eq 0 ]; then # Change prompt colors for root user
    prompt_color='\[\033[;94m\]'
    info_color='\[\033[1;31m\]'
    # Skull emoji for root terminal
    #prompt_symbol=💀
fi
case "$PROMPT_ALTERNATIVE" in
    twoline)
        PS1=$prompt_color'┌──${debian_chroot:+($debian_chroot)──}${VIRTUAL_ENV:+(\[\033[0;1m\]$(basename $VIRTUAL_ENV)'$prompt_color')}('$info_color'\u'$prompt_symbol'\h'$prompt_color')-[\[\033[0;1m\]\w'$prompt_color']\n'$prompt_color'└─'$info_color'\$\[\033[0m\] ';;
    oneline)
        PS1='${VIRTUAL_ENV:+($(basename $VIRTUAL_ENV)) }${debian_chroot:+($debian_chroot)}'$info_color'\u@\h\[\033[00m\]:'$prompt_color'\[\033[01m\]\w\[\033[00m\]\$ ';;
    backtrack)
        PS1='${VIRTUAL_ENV:+($(basename $VIRTUAL_ENV)) }${debian_chroot:+($debian_chroot)}\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ ';;
esac
unset prompt_color
unset info_color
unset prompt_symbol    
```

###  ~/.bashrc

```bash
if [ "$color_prompt" = yes ]; then
    if [ -f ~/.bashrc_kali_linux_prompt ]; then
        . ~/.bashrc_kali_linux_prompt
    else
        PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
    fi
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
```

## Working with pdf documents

Three useful programs to work with pdf docs; `pdfsam`, `pdfarranger` and `pdftk`.

### Installation

```bash
$ sudo apt -y install  pdfsam pdfarranger pdftk
```

### `pdfsam` 

GUI tool to combine pdf documents into 1.

### `pdfarranger` 

GUI tool to change the order of pages in a pdf file

### `pdftk`

CLI tool to password protect a pdf file `pdftk pdf_file.pdf output output_pdf_file.pdf user_pw PROMPT`

