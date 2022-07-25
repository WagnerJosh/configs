# Oh my Posh Terminal Configuration file

Snippet to add to `.zprofile`

```bash

## Ohmyposh 

## may have to change --config path. Points to location of ohmyposh config file.
## IF statment is to stop oh my posh from rendering in default Apple Terminal since 
## it is unable to correctly display colours.

if [ $TERM_PROGRAM != "Apple_Terminal" ]; then
  eval "$(oh-my-posh init zsh --config ~/code/configs/ohmyposh/jw-ohmyposh.json)"
fi

```

## Issues

Documentation of issues encountered setting up Ohmyposh

**Problem:**  
Terminal not rendering colours correctly. Github Issue [#61 Background colors on segments not rendering in MacOS during manual execution](https://github.com/JanDeDobbeleer/oh-my-posh/issues/61)

**Solution:**
Use iterm2 and wrap `.zprofile` config line in if statement exclude `Apple Terminal`  

```bash 
if [ $TERM_PROGRAM != "Apple_Terminal" ]; then
    # eval statment
fi
```
