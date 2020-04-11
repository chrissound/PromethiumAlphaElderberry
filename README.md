A shell/bash/cli implementation of the <https://github.com/bbatsov/projectile> emacs plugin.

```
p () {
  cd "$(tac ~/.config/projectilecli/dirs.txt | fzf)"
}

addToProjectile() {
  if git rev-parse --show-toplevel > /dev/null; then
    echo "$(git rev-parse --show-toplevel)" >> ~/.config/projectilecli/dirs.txt
    tac ~/.config/projectilecli/dirs.txt | awk '!seen[$0]++' | tac > ~/.config/projectilecli/dirs.txt.new
    cp ~/.config/projectilecli/dirs.txt.new ~/.config/projectilecli/dirs.txt

  fi
}
```

Then just call `addToProjectile` when ever you `cd` into a directory. Which with ZSH can be done automatically by:
```
chpwd() {
          $(addToProjectile > /dev/null 2> /dev/null &)
      }
```

Dependencies:
- tac 
- fzf
- awk
- git
