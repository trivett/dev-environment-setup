# Setting up a good development environment on a Mac

### Install OSX
* Always best to clean install and transfer documents and stuff later imho.
* Pop in your bootable OSX USB stick.
* Wipe your hard drive by powering on your Mac while holding down the Option key, select the OSX USB drive, go to Utilities > Disk Utility, and format your hard disk in Mac OSX (Journaled) format.
* Don't sign in with your Apple ID right away.

### Important: If you are doing this with El Capitain, you need another step: 
* Restart your laptop and hold cmd+r
* Go to Utilities > Terminal
* Execute `csrutil disable`
* Now you can go into hardhat mode on your computer. Without this, anything relating to `root` will be impossible. 


### Xcode:
* Install all updates for your OS etc.
* Get Xcode's command line tools to get GCC, git and other goodies.
* Once it downloads do ````xcode-select --install```` to get the command line tools.


### System preferences:

* *Dock*: Shrink the dock. 
* *Mission Control*: Set up hot corners for mission control and show desktop.
* *Displays*: Arrangement-> uncheck mirror displays, arrange second monitor to your liking. 
* *Trackpad*: Tap to click, X scroll direction, X swipe between pages 
* *Keyboard*: Max speed Key Repeat and shortest Delay Until Repeat so you don't have to wait ages to move your cursor in the terminal. Under the Text tab here you can add keyboard shortcuts like  `¯\_(ツ)_/¯` which come in handy, amirite? Also set up your external pc keyboard and switch alt and cmd, and map the caps lock to an extra escape. 

### Fix (some) Privacy Intrusions
Apple is just going to send your data to Microsoft of all places if you don't do this.
* Follow the instructions at [Fix Mac OSX](https://fix-macosx.com) You can even do this automatically by running a Python script, but we aren't ready for that yet.

### Get Rid of Apple's stupid shit programs
In a Terminal window, enter: 

````sudo chflags hidden /Applications/Bullshit.app````

(Replace "Bullshit" with Maps, for example.)
 
This will hide Apple's perplexingly awful default programs that are inadvisable to delete outright.

I also deleted the stock alerts in the notifications panel.


### Dotfiles:
* I make my modifications in a fork of the [thoughtbot dot](https://github.com/thoughtbot/dotfiles) in [this repo](https://github.com/trivett/dotfiles)
* After that, I like to install [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) and [bash-it](https://github.com/Bash-it/bash-it) for no reason other than the nice themes so I don't have to edit my bash or zsh profiles too much. For some reason I like to change the colors of my terminal and stuff when I'm procrastinating.

### Dev friendly fonts

Install Powerline Fonts: https://github.com/powerline/fonts

###Homebrew
````
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

````

* Homebrew will ask you to download Xcode command line tools. When finished, run: 

````
brew doctor
brew update
````
### Rbenv, Ruby, and Rails
Much of this follows some of the instructions on [GoRails](https://gorails.com/setup/osx/10.10-yosemite).


If you have rvm installed: 
````
rvm implode
gem uninstall rvm
rm -rf .rvm
rm -rf .rvmrc

````
That gets rid of the competing ruby version manager. You will probably also have to remove references to rvm in your bash / zsh profile / rc. 


Rbenv

````
brew install rbenv ruby-build
````


````
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.zshrc
source ~/.zshrc
````

````
rbenv install 2.4.1
rbenv global 2.4.1
rbenv rehash

gem install rails --no-ri --no-rdoc 

rbenv rehash

````

#####Check thyself before thou wreckest thyself:

* Open a new terminal
* `ruby -v ` should give you 2.4.1 and `rails --version` should output 5.x.x


## Node

Install [nvm](https://github.com/creationix/nvm):
`curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash`

Then you should have the right version of node and npm


### Git and Github
* Git config:

````
git config --global color.ui true
git config --global user.name "First Last"
git config --global user.email "flast@yo.com"
````
Set up 2-factor authentication on github.

### Generate SSH keys:
* In Terminal:

````
cd ~/.ssh
ssh-keygen -t rsa -C "you@yo.com"
#don't enter a passphrase
pbcopy < ~/.ssh/id_rsa.pub
````
* Paste the entire resulting RSA key to [Github](https://github.com/settings/ssh).

````ssh -T git@github.com```` checks that this actually worked.

### Postgresql
````
brew install postgresql
ln -sfv /usr/local/opt/postgresql/*plist ~/Library/LaunchAgents

launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist


````


### VS Code
* [Download](https://code.visualstudio.com/)


* Some settings to get you started:

````
// Place your settings in this file to overwrite the default settings
{
    "editor.fontFamily": "Hack, Fira Mono for Powerline,Menlo, Monaco, 'Courier New', monospace",
    "editor.fontSize": 15,
    "editor.tabSize": 2,
    "editor.wordWrap": "on",
    "workbench.colorTheme": "Eagle Oceanic Next",
    "editor.wordWrap": "on",
    "window.zoomLevel": 0,
    "editor.renderIndentGuides": false,
    "editor.showFoldingControls": "always",
    "workbench.colorCustomizations": {
        "editorGutter.background": "#343D46"
    },

    "workbench.iconTheme": "material-theme-icons",
   "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/CVS": true,
        "**/tmp": true,
        "**/.DS_Store": true
    },   

}

}

````

Keybindings: 

```
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
    }
]

```

Extensions for VS Code:


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

### iTerm2:
* [Download](http://www.iterm2.com/#/section/home)
* I highly recommend a [heads-up terminal](http://totalterminal.binaryage.com/) for running servers and some color schemes such as [solarized](http://iterm2colorschemes.com/)
* On iTerm, turn off the annoying beep: Preferences>Profiles>Tab:Terminal>Notifications>Silence Bell
* Also nice to enable [option + arrow key navigation](https://coderwall.com/p/h6yfda/use-and-to-jump-forwards-backwards-words-in-iterm-2-on-os-x)


### Chrome:
Set up gmail, drive, and 2-factor authentication
Suggested Extensions:

* JSONView
* Pesticide
* Ghostery
* Rails Panel
* Postman Rest Client

### Python, pip and virtualenv

`````
brew install python # python comes with OSX but this installs pip and some other stuff
pip install virtualenv
`````

### Mongodb
* Installation with homebrew:

````	
brew install mongodb
````
* To start mongodb server, run ```` mongod ```` 
* For a shell, just type ```` mongo ```` 

### Other Apps:
* Dash
* Spectacle
* Skype
* Tor 
* OnionShare 
* Android Studio
* Pocket
* Mou
* Twitter
* Libre Office
* Slack
* Sip
