# This is my personal homelab code that I use for fun and to learn

This is run on a lenovo laptop on my local network and is not connected to the
internet at large. Is designed to be fun a a space to hack around. I strive to
use best practices all around

# Setup

- Install `direnv` on you local machine
``` bash
    brew install direnv 
    
    # add this to your .zshrc
    eval "$(direnv hook zsh)"
    plugins=(direnv)
```

- Set up end vars
``` bash
    cp .envrc.example .envrc
    # update the values of the variables
```

- Install `talosctl` on you local machine
``` bash
    brew install siderolabs/tap/talosctl
```
