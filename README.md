#Setting up a good development environment on a Mac

###Install OSX
* Always best to clean install and transfer documents and stuff later imho.
* Pop in your bootable OSX USB stick.
* Wipe your hard drive by powering on your Mac while holding down the Option key, select the OSX USB drive, go to Utilities > Disk Utility, and format your hard disk in Mac OSX (Journaled) format.
* Don't sign in with your Apple ID right away.

### Important: If you are doing this with El Capitain, you need another step: 
* Restart your laptop and hold cmd+r
* Go to Utilities > Terminal
* Execute `csrutil disable`
* Now you can go into hardhat mode on your computer. Without this, anything relating to `root` will be impossible. 


###Xcode:
* Download Xcode from the App Store. It will take a while so do this first.
* Install all updates for your OS etc.
* Get Xcode's command line tools to get GCC, git and other goodies.
* Once it downloads do ````xcode-select --install```` to get the command line tools.


###System preferences:
While Xcode takes forever to download

* *Dock*: Shrink the dock. 
* *Mission Control*: Set up hot corners for mission control and show desktop.
* *Displays*: Arrangement-> uncheck mirror displays, arrange second monitor to your liking. 
* *Trackpad*: Tap to click, X scroll direction, X swipe between pages 
* *Keyboard*: Max speed Key Repeat and shortest Delay Until Repeat so you don't have to wait ages to move your cursor in the terminal. Under the Text tab here you can add keyboard shortcuts like  `¯\_(ツ)_/¯` which come in handy, amirite?

###Fix (some) Privacy Intrusions
Apple is just going to send your data to Microsoft of all places if you don't do this.
* Follow the instructions at [Fix Mac OSX](https://fix-macosx.com) You can even do this automatically by running a Python script, but we aren't ready for that yet.

### Get Rid of Apple's stupid shit programs
In a Terminal window, enter: 

````sudo chflags hidden /Applications/Bullshit.app````

(Replace "Bullshit" with Maps, for example.)
 
This will hide Apple's perplexingly awful default programs that are inadvisable to delete outright.

I also deleted the stock alerts in the notifications panel.


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

````
brew install rbenv ruby-build
````

````
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
source ~/.bash_profile
````

````
rbenv install 2.2.3
rbenv global 2.2.3
gem install rails # you might have to chown or adjust path so you don't have to install gems as root
rbenv rehash
````

#####Check thyself before thou wreckest thyself:
```` ruby -v ```` should give you 2.2.3 and ````rails --version```` should output 4.2.4


###Git and Github
* Git config:

````
git config --global color.ui true
git config --global user.name "First Last"
git config --global user.email "flast@yo.com"
````
Set up 2-factor authentication on github.

###Generate SSH keys:
* In Terminal:

````
cd ~/.ssh
ssh-keygen -t rsa -C "you@yo.com"
#don't enter a passphrase
pbcopy < ~/.ssh/id_rsa.pub
````
* Paste the entire resulting RSA key to [Github](https://github.com/settings/ssh).

````ssh -T git@github.com```` checks that this actually worked.

###Postgresql
````
brew install postgresql
ln -sfv /usr/local/opt/postgresql/*plist ~/Library/LaunchAgents

launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist


````
###Firefox
* Get the [developer edition!](https://www.mozilla.org/en-US/firefox/developer/)


###Sublime Text 3:
* [Download](http://www.sublimetext.com/)
* [Package control](https://sublime.wbond.net/installation)
* Emmet
* Colorsublime
* Sublime Linter
* Set up subl command line shortcut: 

````ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl````


* Some settings to get you started:

````
{
	"bold_folder_labels": true,
	"color_scheme": "Packages/Color Scheme - Default/Solarized (Light).tmTheme",
	"fade_fold_buttons": false,
	"highlight_line": true,
	"highlight_modified_tabs": true,
	"ignored_packages":
	[
		"Vintage"
	],
	"line_padding_bottom": 1,
	"line_padding_top": 1,
	"word_wrap": true,
	"font_face": "AnonymousPro",
	"font_size": 13
}
````
###iTerm2:
* [Download](http://www.iterm2.com/#/section/home)
* I highly recommend a [heads-up terminal](http://totalterminal.binaryage.com/) for running servers and some color schemes such as [solarized](http://iterm2colorschemes.com/)
* On iTerm, turn off the annoying beep: Preferences>Profiles>Tab:Terminal>Notifications>Silence Bell
* Also nice to enable [option + arrow key navigation](https://coderwall.com/p/h6yfda/use-and-to-jump-forwards-backwards-words-in-iterm-2-on-os-x)


###Chrome:
Set up gmail, drive, and 2-factor authentication
Suggested Extensions:

* JSONView
* Pesticide
* Ghostery
* Rails Panel
* Postman Rest Client

###Python, pip and virtualenv

`````
brew install python # python comes with OSX but this installs pip and some other stuff
pip install virtualenv
`````

###Mongodb
* Installation with homebrew:

````	
brew install mongodb
````
* To start mongodb server, run ```` mongod ```` 
* For a shell, just type ```` mongo ```` 

###Dotfiles:
* I make my modifications in a fork of the [thoughtbot dot](https://github.com/thoughtbot/dotfiles) in [this repo](https://github.com/trivett/dotfiles)
* After that, I like to install [oh-my-zsh] for no reason other than the nice themes so I don't have to edit my bash or zsh profiles too much. For some reason I like to change the colors of my terminal and stuff when I'm procrastinating.

###Other Apps:
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
