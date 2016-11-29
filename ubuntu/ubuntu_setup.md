# Ubuntu setup

Making a nice developer environment on a PC. [Mac version](https://github.com/trivett/dev-environment-setup/blob/master/README.md) 

## Update all the things

First run Software Updater from the Dash and do as it commands.

Then run a nice `sudo apt-get update`

While that runs, download the Chrome browser and log in and half of your life is already on the machine.

## Fix Ubuntu

Inspired by [https://fixubuntu.com/.](https://fixubuntu.com/.) 

To fix some of Canonical's puzzlingly bad privacy no-nos, first download Unity Tweak Tool from the Software Center, and uncheck Search Online Sources and Show More Suggestions in the search panel. This prevents you from getting results for bras on Amazon when you are looking for Brasero in Dash.

## Visual tweaks

Now that we have tweak tool, lets make Ubuntu look nice.

Get a nice GTK theme. I kind of like Papirus Icons and the Adapta GTK theme. 

Adapta

```shell
sudo apt-add-repository ppa:tista/adapta -y
sudo apt-get update
sudo apt-get install adapta-gtk-theme
```

I also install the GNOME tweak tool (`sudo apt-get install gnome-tweak-tool`) to
make the caps lock an extra escape (vim ftw) and choose global dark theme, which
looks great with Adapta GTK. You can also switch the alt and ctrl keys to make
it feel more Mac like but I get confused doing that.


Papirus

```shell
sudo add-apt-repository ppa:varlesh-l/papirus-pack

sudo apt-get update && sudo apt-get install papirus-gtk-icon-theme
```

Select them under Theme and Icons respectively in Unity tweak tool

Put the Launcher on the bottom like in Windows and Mac if you like

`gsettings set com.canonical.Unity.Launcher launcher-position Bottom`

In Appearance in the system preferences, check menu visibility to always be visible rather than only showing when you hover

Enable hot corners to spread windows and show desktop.

Install Variety to get a new pretty wallpaper like the Astronomy Photo of the Day.

```
sudo add-apt-repository ppa:peterlevi/ppa
sudo apt-get update
sudo apt-get install variety variety-slideshow
```

Dash size

I prefer the Unity dash to not take up the whole screen. Put it in desktop form-factor to make it more like a windows start button.

`gsettings set com.canonical.Unity form-factor Desktop`


## Applications



Mail Client for Gmail: [wmail](https://thomas101.github.io/wmail/download)

Markdown editor: [Typora](www.typora.io)

Compiz config settings `sudo apt-get install compizconfig-settings-manager`

Compiz plugins 'sudo apt-get install compiz-plugins'

You can import my settings from the compiz-settings file in this folder.

Gimp (Software Center app)

Pick ([color picker](http://kryogenix.org/code/pick/))

VLC (Software Center app)

Shutter (Software Center app)

Spotify (Note that the spotify web player is finicky and the regular Linux desktop client is no longer maintained. [Spotiweb](https://github.com/tomasmcm/SpotiWeb/releases) is your best bet)

Bleach bit (Software center app)

Guake

[Franz] (http://meetfranz.com/) This [script](https://gist.github.com/ruebenramirez/22234da93f08be65125cc45fc386c1cd) is helpful for installing

Gloobus (space to open preview like in osx)

```shell
sudo add-apt-repository ppa:gloobus-dev/gloobus-preview 
sudo apt-get update 
sudo apt-get install gloobus-preview gloobus-sushi 
sudo apt-get install unoconv 

```


## Fonts

I always use [Mononoki](https://github.com/madmalik/mononoki) for my terminal  and [Source Code Pro](https://github.com/adobe-fonts/source-code-pro) in Sublime Text

# Just developer stuff


##Set up Git
```shell
sudo apt install git
git config --global color.ui true
git config --global user.name "First Last"
git config --global user.email "flast@yo.com"

mkdir ~/.ssh
ssh-keygen -t rsa -C "you@yo.com"
#don't enter a passphrase
cat  ~.ssh/id_rsa.pub

#copy that and paste the entire resulting RSA key to [Github](https://github.com/settings/ssh).

ssh -T git@github.com #checks that this actually worked.
```




## Dotfiles

Clone my [dotfiles](https://github.com/trivett/dotfiles) (which are forked from Thoughtbot's)

`sudo apt install zsh`

`sudo apt install vim`

RCM

```shell
sudo add-apt-repository ppa:martin-frost/thoughtbot-rcm
sudo apt-get update
sudo apt-get install rcm
env RCRC=$HOME/dotfiles/rcrc rcup
```

Oh my zsh

`sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

Then go into your `.zshrc` and change the theme on line 10 to `agnoster`

## Text editor

Download [Sublime Text](https://www.sublimetext.com/3)

Install package control:

```python
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```



Packages you need: 

* Advanced new file

* color highlighter

* sidebar enhancements

* All autocomplete

* babel

* colorsublime

* emmet

* git gutter

* htmlbeautify

* json reindent

* jsx

* numix theme

* oceanic next color scheme

* react js

* sass

* sidebar enhancements

* sublime linter

  ​

User preferences 



```json
{
	"auto_complete": true,
	"auto_complete_commit_on_tab": false,
	"bold_folder_labels": true,
	"color_scheme": "Packages/User/SublimeLinter/Oceanic Next (SL).tmTheme",
	"copy_with_empty_selection": true,
	"ensure_newline_at_eof_on_save": true,
	"fade_fold_buttons": false,
	"folder_exclude_patterns":
	[
		"bower_components",
		"tmp",
		".git"
	],
	"font_face": "Mononoki",
	"font_size": 13,
	"highlight_line": true,
	"highlight_modified_tabs": true,
	"ignored_packages":
	[
		"Color Highlighter",
		"Vintage"
	],
	"index_files": true,
	"line_padding_bottom": 1,
	"line_padding_top": 1,
	"numix_folder_icons": false,
	"tab_size": 2,
	"theme": "Numix Dark.sublime-theme",
	"translate_tabs_to_spaces": true,
	"trim_trailing_white_space_on_save": true,
	"word_separators": "./\\()\"'-:,.;<>~@#$%^&*|+=[]{}`~",
	"word_wrap": true
}

```



# Installing ruby and such



###Dependencies

```shell

sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
```

###Rbenv
```
cd ~
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
cd ~/.rbenv && src/configure && make -C src

echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(rbenv init -)"' >> ~/.zshrc
exec $SHELL

```

###ruby-build

```
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.zshrc
exec $SHELL

```

###ruby

```

rbenv install 2.3.1
rbenv global 2.3.1
ruby -v
gem install bundler
rbenv rehash

```

###node

```
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
```


###rails

```
gem install rails -v 4.2.6 --no-ri --no-rdoc
rbenv rehash
```

###postgresql

```
sudo sh -c "echo 'deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-common
sudo apt-get install postgresql-9.5 libpq-dev

sudo -u postgres createuser vincent -s

```

### Heroku toolbelt

```shell
wget -O- https://toolbelt.heroku.com/install-ubuntu.sh | sh
heroku login
```

