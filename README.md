#Setting up a good development environment on a Mac


#Step One
* Pop in your bootable OSX Yosemite USB stick.
* Wipe your harddrive by starting OSX while holding down option, go to Utilities > Disk Utility and format your hard disk in Mac OSX (Journaled) format.
* Don't sign in with your Apple ID right away.


###Xcode:
* Download Xcode from the App store. It will take a while so do this first.
* Install all updates for your OS etc.
* Get Xcode's command line tools to get GCC, git and other goodies.
* Once it downloads do ````xcode-select --install```` to get the command line tools.



###System preferences:
While Xcode takes forever to download

* *Dock*: Shrink the dock. 
* *Mission Control*: Set up hot corners for mission control and show desktop.
* *Displays*: Arrangement-> uncheck mirror displays, arrange second monitor to your liking. 
* *Trackpad*: Tap to click, X scroll direction, X swipe between pages 

###Fix (some) Privacy Intrusions
Apple is just going to send your data to fucking Microsoft of all places if you don't do this.
* Follow the instructions at [Fix Mac OSX](https://fix-macosx.com) You can even do this automatically by running a Python script, but we aren't ready for that yet.

### Get Rid of Apple's stupid shit programs
In a Terminal window, hit 

````sudo chflags hidden /Applications/Bullshit.app````

replacing "Bullshit" with Maps for example.
 
This will hide Apple's perplexingly awful default programs that are inavisable to delete straight away.

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
Much of this follows some of the instructions on [GoRails](https://gorails.com/setup/osx/10.10-yosemite)

````
brew install rbenv ruby-build
````

````
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
source ~/.bash_profile
````

````
rbenv install 2.1.3
rbenv global 2.1.3
gem install rails
rbenv rehash
````

#####Check thyself before you wreck thyself:
```` ruby -v ```` should give you 2.1.3 and ````rails --version```` should output 4.1.6


###Git and Github
* Git config:

````
git config --global color.ui true
git config --global user.name "First Last"
git config --global user.email "flast@yo.com"
````
Set up 2-factor authentication on github.

###Generate SSH keys:
* Instructions:

````
cd ~/.ssh
ssh-keygen -t rsa -C "you@yo.com"
#don't enter a passphrase
pbcopy < ~/.ssh/id_rsa.pub
````
* Paste the resulting RSA key to [Github](https://github.com/settings/ssh).

````ssh -T git@github.com```` checks that this actually worked.

###Postgresql
````
brew install postgresql
ln -sfv /usr/local/opt/postgresql/*plist ~/Library/LaunchAgents

launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist


````

###Chrome
yep.

###Firefox
uh huh.


###Sublime Text 3:
* [Download](http://www.sublimetext.com/)
* [Package control](https://sublime.wbond.net/installation)
* Emmet
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
	"font_size": 18
}
````
###iTerm2:
* [Download](http://www.iterm2.com/#/section/home)
* I highly recommend a [heads-up terminal](http://ivanvillareal.com/osx/setup-iterm2-to-behave-like-guake/) for running servers and some color schemes such as [solarized](http://iterm2colorschemes.com/)

###Chrome:
Set up gmail, drive, and 2-factor authentication
Suggested Extensions:

*JSONView
*Pesticide
*Live Reload

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

###Vim
* get yourself a nice vim distro like spf13 

````curl https://j.mp/spf13-vim3 -L > spf13-vim.sh && sh spf13-vim.sh)````


###Other Apps:
* Dash
* Spectacle
* Skype
* Spider Oak (fuck Dropbox for hiring Condoleeza Rice. Seriously, anyone without the war in Iraq and warrantless wiretapping on their resume would have been better.)
* Tor 
* OnionShare 
* Android Studio
* Pocket
* Mou
* Twitter
* Libre Office
* 
