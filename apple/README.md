# Setting up a good development environment on a Mac

## Install OSX
Always best to clean install and transfer documents and stuff later imho.

Pop in your bootable OSX USB stick.

Wipe your hard drive by powering on your Mac while holding down the Option key, select the OSX USB drive, go to Utilities > Disk Utility, and format your hard disk in Mac OSX (Journaled) format.

Don't sign in with your Apple ID right away.

## Xcode:
Unless you plan on doing iOS or native Mac coding, you don't need xcode. Just run `code-select —install` to get GCC, git and other goodies.

## System preferences:

Dock*: Shrink the dock. 

*Mission Control*: Set up hot corners for mission control and show desktop.

*Displays*: Arrangement-> uncheck mirror displays, arrange second monitor to your liking. 

*Trackpad*: Tap to click, X scroll direction, X swipe between pages 

*Keyboard*: Max speed Key Repeat and shortest Delay Until Repeat so you don't have to wait ages to move your cursor in the terminal. Under the Text tab here you can add keyboard shortcuts like  `¯\_(ツ)_/¯` which come in handy, amirite? Also set up your external pc keyboard and switch alt and cmd, and map the caps lock to an extra escape. 

In the finder go to Preferences and change the sidebar so to include the directories such as `~` so you can easily get to them.

## Fix (some) Privacy Intrusions
Apple is just going to send your data to Microsoft of all places if you don't do this.

Follow the instructions at [Fix Mac OSX](https://fix-macosx.com). 

## Get Rid of Apple's stupid shit programs
In a Terminal window, enter: 

````sudo chflags hidden /Applications/Bullshit.app````

(Replace "Bullshit" with Maps, for example.)

This will hide Apple's perplexingly awful default programs that are inadvisable to delete outright.

I also deleted the stock alerts in the notifications panel.

## Dotfiles:
I make my modifications in a fork of the [thoughtbot dot](https://github.com/thoughtbot/dotfiles) in [this repo](https://github.com/trivett/dotfiles)

After that, I like to install [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh). I usually go for Agnoster as my theme.

## Dev friendly fonts

Install Powerline Fonts: https://github.com/powerline/fonts

## Homebrew

In the default Mac terminal for now:

````shell
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
````

Homebrew will ask you to download Xcode command line tools if you haven't already. When finished, run: 

````shell
brew doctor
brew update
````

## Programming languages

### Rbenv, Ruby, and Rails

If you have rvm installed: 

````shell
rvm implode
gem uninstall rvm
rm -rf .rvm
rm -rf .rvmrc
````
That gets rid of the competing ruby version manager. You will probably also have to remove references to rvm in your bash / zsh profile / rc. 

Install rbenv and ruby-build:

````shell
brew install rbenv ruby-build
````

````shell
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.zshrc
source ~/.zshrc
````

````shell
rbenv install 2.4.1
rbenv global 2.4.1
rbenv rehash

gem install rails --no-ri --no-rdoc 

rbenv rehash
````

Check ruby installation in a new terminal window. `ruby -v ` should give you 2.4.1 and `rails --version` should output 5.x.x.

### Node

Install [nvm](https://github.com/creationix/nvm):
`curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash`

Then you should have the latest version of node and npm

### Golang

Download from the official golang site: [https://golang.org/dl/](https://golang.org/dl/)

### Python

`````shell
brew install python3
`````

## Git and Github
Git config:

````shell
git config --global color.ui true
git config --global user.name "First Last"
git config --global user.email "flast@yo.com"
````
Set up 2-factor authentication on github.

## Generate SSH keys:
In Terminal:

````Shell
mkdir ~/.ssh && cd ~/.ssh
ssh-keygen -t rsa -C "you@example.com"
#don't enter a passphrase
pbcopy < ~/.ssh/id_rsa.pub
````
Paste the entire resulting RSA key to [Github](https://github.com/settings/ssh).

````ssh -T git@github.com```` checks that this actually worked.

## Heroku

If you plan on deploying to Heroku first install the heroku CLI with `brew install heroku/brew/heroku`

You will need to log in with your credentials with `heroku login`

If you have more than one set of creds, you can set up a personal and work account with the [heroku-accounts](https://github.com/heroku/heroku-accounts) plugin.

I highly recommend the [parity](https://github.com/thoughtbot/parity) gem, which simplifies the work of dealing with staging and production environments on Heroku, provides an easier to type interface, makes it next to impossible to nuke production, and makes it really easy to sync databases between prod, dev, and staging.

## Postgresql
````Shell
brew install postgresql
ln -sfv /usr/local/opt/postgresql/*plist ~/Library/LaunchAgents
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
````

## VS Code
Download](https://code.visualstudio.com/)

Some settings to get you started:

````json
{
  "prettier.ignorePath": ".eslintignore",
  "editor.fontSize": 16,
  "files.autoSaveDelay": 5000,
  "editor.fontFamily": "Cousine for Powerline, Anonymous Pro for Powerline",
  "editor.tabSize": 2,
  "editor.wordWrap": "on",
  "workbench.editor.enablePreview": false,
  "window.zoomLevel": 0,
  "editor.renderIndentGuides": false,
  "editor.showFoldingControls": "always",
  "workbench.colorCustomizations": {
  
      "terminal.foreground": "#839496",
      "terminal.background": "#002833",
      "terminal.ansiBlack": "#003541",
      "terminal.ansiBlue": "#268bd2",
      "terminal.ansiCyan": "#2aa198",
      "terminal.ansiGreen": "#859901",
      "terminal.ansiMagenta": "#d33682",
      "terminal.ansiRed": "#dc322f",
      "terminal.ansiWhite": "#eee8d5",
      "terminal.ansiYellow": "#b58901",
      "terminal.ansiBrightBlack": "#586e75",
      "terminal.ansiBrightBlue": "#839496",
      "terminal.ansiBrightCyan": "#93a1a1",
      "terminal.ansiBrightGreen": "#586e75",
      "terminal.ansiBrightMagenta": "#6c6ec6",
      "terminal.ansiBrightRed": "#cb4b16",
      "terminal.ansiBrightWhite": "#fdf6e3",
      "terminal.ansiBrightYellow": "#657b83",
      "terminalCursor.foreground": "#839496",
      "terminalCursor.background": "#003541"
  
      // "editorGutter.background": "#eee8d5" //light
    },
    "editorGutter.background": "#343D46", //dark
  "files.exclude": {
    "**/.git": true,
    "**/.svn": true,
    "**/.hg": true,
    "**/CVS": true,
    "**/tmp": true,
    "**/.DS_Store": true
  },
"files.defaultLanguage": "javascript",
"terminal.integrated.rendererType": "dom",
"editor.minimap.enabled": false,
"editor.minimap.maxColumn": 80,
"java.configuration.checkProjectSettingsExclusions": false,
"editor.suggestSelection": "first",
"vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
"workbench.startupEditor": "newUntitledFile",

"workbench.colorTheme": "Eagle Oceanic Next",
// "workbench.colorTheme": "Glance (rainglow)",
"[typescript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[json]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[javascript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"editor.fontLigatures": true,
"[html]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},

}

````

Keybindings: 

```json
[
  {
     "key": "ctrl+shift+up",
     "command": "editor.action.moveLinesUpAction",
     "when": "editorTextFocus"
   },
   {
     "key": "ctrl+shift+down",
     "command": "editor.action.moveLinesDownAction",
     "when": "editorTextFocus"
   },
   {
      "key": "cmd+shift+d",
      "command": "editor.action.copyLinesDownAction",
      "when": "editorTextFocus"
    },
    {
      "key": "ctrl+pagedown",
      "command": "workbench.action.nextEditor",
      "when": "editorTextFocus"
    },
   {
      "key": "ctrl+pageup",
      "command": "workbench.action.previousEditor",
      "when": "editorTextFocus"
    }
]
```

### Extensions for VS Code:

* Eagle oceanic next
* Beautify
* docker
* editorconfig
* erb
* eslint
* File utils
* Go
* higlight matching tag
* material theme
* open in browser
* path intellisense
* python
* vscode-icons

## iTerm2:
[Download](http://www.iterm2.com/#/section/home)

I highly recommend a [heads-up terminal](http://totalterminal.binaryage.com/) for running servers and some color schemes such as [solarized](http://iterm2colorschemes.com/)

On iTerm, turn off the annoying beep: Preferences>Profiles>Tab:Terminal>Notifications>Silence Bell

Also nice to enable [option + arrow key navigation](https://coderwall.com/p/h6yfda/use-and-to-jump-forwards-backwards-words-in-iterm-2-on-os-x)

You can use the `.plist` file in this directory to import settings.

## Chrome:
Set up gmail, drive, and 2-factor authentication
Suggested Extensions:

* JSONViewer
* Pesticide
* Ghostery
* Rails Panel
* Postman Rest Client
* Form Filler
* GMT/UTC Clock
* Google Keep
* HTTPS Everywhere
* OneTab
* Papier
* Save to Pocket
* Privacy Badger
* React Developer Tools
* Redux Dev Tools
* Rikaikun
* Track Me Not
* uBlock Origin
* Wappalyzer

## Other Apps:

* Caffeine
* Dash
* Deco
* Docker
* Dr Cleaner
* Enpass
* Firefox
* Flux
* Franz
* Gimp
* GimPs Gimp Theme
* Chrome
* iTerm
* Keybase
* Kap
* Keynote
* Kindle
* Libre Office
* Mailplane
* Pocket
* [Pocketcasts](https://github.com/mortenjust/PocketCastsOSX)
* Postman
* Private Internet Access
* Psequel
* Screenhero
* Simplenote
* Sip
* Skype
* Spectacle
* Spotify
* Table Plus
* Tor
* Typora
* Virtualbox
* Visual Studio Code
* Trello
* Xcode
* VLC
* [Epson film scanner software](https://epson.com/Support/Scanners/Perfection-Series/Epson-Perfection-V300-Photo/s/SPT_B11B193081)
