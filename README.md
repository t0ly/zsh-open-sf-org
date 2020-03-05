# zsh-open-sf-org
Alias and tab completion to open Salesforce orgs from the command line in zsh
==


Preprequisites
===

- Z-shell (default on macOS from Catalina)
- [Salesforce CLI `sfdx`](/forcedotcom/cli)
- Orgs registered (`sfdx force:org:list` shows the orgs you've logged in)

Install
===

#### 1. Add this to your `.zshrc`

```
# zsh Function to call sfdx force:org:open command
sfopen () {
if (( $# == 0 ))
        then grep "\": \"" ~/.sfdx/alias.json |  cut -s -d\" -f2 | sort && echo \\nUsage: sfopen myorgname\\nTab key completes org alias;
fi
        for i; do
        date && sfdx force:org:open -p /setup/forcecomHomepage.apexp -u $i;
        done
}

autoload _sfopen                # do not forget BEFORE the next cmd!
compdef _sfopen sfopen  # binds the completion function to a command

# enable the default zsh completions!
autoload -Uz compinit && compinit

# add custom completion scripts in .zsh directory
fpath=(~/.zsh $fpath)



```

#### 2. Save the [`_sfopen`](.zsh/_sfopen) completion file somewhere in your path (.zsh/ directory in the example above)

#### 3. Restart zsh
```
zsh -l

```
