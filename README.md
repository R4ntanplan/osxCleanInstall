OS X ENV (re)Install
====================

This is my personal guide to restore my configuration and setup my system for a fresh install (original by m4dz). I use it and keep it updated frequently. Hope it will inspire you on your own way =].

Backup
------

Before a fresh reinstall, don't forget to backup many things. A regular ghost made with CarbonCopyCloner is a good solution, but if you can't, you should save the following :

- MySQL databases (use the script bellow)
- User preferences
	- ~/Library/Application Support
	- ~/Library/ColorSync/Profiles
	- ~/Library/Fonts	
	- ~/Library/Keychains
	- ~/Library/LaunchAgents
	- ~/Library/Preferences
	- ~/Library/QuickLook
- Configs
	- ~/.gitconfig
	- ~/.glacier-cmd
	- ~/.gnupg
	- ~/.pow
	- ~/.powconfig
	- ~/.s3cfg
	- ~/.ssh

Installation
------------

After a clean fresh install (format disk and reinstall the base OS and updates), let's install xtras.

### Base

You can restore the previously backuped files. If you do so, don't forget to restore permissions : restart in Restore mode with `⌘+R`, open the `terminal` and launch `resetpassword2`.

### Homebrew

Homebrew is a package manager for OS X. I use to manage my developer tools, and my desktop apps using its submanager : cask.

	ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
	brew tap josegonzalez/php
	brew tap homebrew/dupes
	brew tap phinze/cask
	brew tap caskroom/versions
	brew install brew-cask 


### Shell

I use ZSH instead of the legacy bash shell. To do so :

!https://s3.amazonaws.com/ohmyzsh/oh-my-zsh-logo.png!

oh-my-zsh is an open source, community-driven framework for managing your ZSH configuration. It comes bundled with a ton of helpful functions, helpers, plugins, themes, and few things that make you shout...

bq. "OH MY ZSHELL!"

h2. Setup

@oh-my-zsh@ should work with any recent release of "zsh":http://www.zsh.org/, the minimum recommended version is 4.3.9.

h3. The automatic installer... (do you trust me?)

You can install this via the command line with either @curl@ or @wget@.

h4. via @curl@

@curl -L http://install.ohmyz.sh | sh@

h4. via @wget@

@wget --no-check-certificate http://install.ohmyz.sh -O - | sh@
	git clone https://github.com/madsgraphics/oh-my-zsh.git ~/.oh-my-zsh
	ln -sfv ~/.oh-my-zsh/custom/zshenv .zshenv
	ln -sfv ~/.oh-my-zsh/custom/zshrc .zshrc
	chsh -s /bin/zsh
	
### Pow

Pow is a tools that combines a local host names resolver (based on the `.dev` tld) and a rack server for ruby (and others) apps.

	echo 'export POW_DST_PORT=88' >> ~/.powconfig
	curl get.pow.cx | sh


### Commons tools

My basic tools for everyday use.

	brew cask install dropbox
# gestion des fichiers ds_store
	brew cask install asepsis
	brew cask install little-snitch
	brew cask install trim-enabler
	brew cask install alfred
	brew cask install bartender
	brew cask install iterm2
	brew cask install istat-menus
	brew cask install hyperdock
	brew cask install appcleaner
	brew cask install cocktail
	brew cask install gpgtools

- Appstore
	- 1password
	- Evernote
 	- Moom
	- Mouseposé
	- DaisyDisk
	- Growl


### Development Environment

My development envrionment is a little bit complex due to many languages and apps I use everyday. You can simplify it to adapt it to your requirements.

Do not forget to add `launch plist` files for daemons. You can add the `plist` for your servers (http, PHP-FPM, Mysql,Memcached…) directly to `/Library/LaunchDaemons` to start it at boot with root permissions. Use `brew info <package>` to view extras informations. For Nginx and PHP-FPM, configure user / group to `_www` in config files ; for Memcache, configure plist file with UserName / GroupName `daemon`.

#### Base

	brew install git
	brew install ack aria2 autojump apple-gcc42 bash-completion gettext pidof curl ssh-copy-id s3cmd

	brew install imagemagick --use-cms --with-freetype --use-rsvg --use-tiff
	brew install optipng
	
	sudo gem install --no-ri --no-rdoc lunchy powder 
	
	brew install nginx
	mkdir -p /usr/local/var/log/nginx
	chown _www /usr/local/var/log/nginx
	
	brew cask install vagrant

#### DB

	brew install mariadb postgresql memcached mongodb sqlite zeromq
	
#### Python

	brew install python pyenv pyenv-virtualenv
	
#### Ruby

	brew install ruby-build rbenv
	rbenv install 2.1.0
	gem install --no-ri --no-rdoc bundler mime-types rails rake sass sinatra sqlite3 thin tzinfo uglifier
	
#### NodeJS

	brew install node --without-npm
	curl http://npmjs.org/install.sh | sh
	npm -g install bower coffee-script csslint docco grunt-cli jade jsbin jscs jshint yo
	brew install phantomjs

#### PHP

	brew install php55 --with-fpm --without-apache
	brew install php55-apcu php55-intl php55-memcached php55-xdebug php55-yaml php55-zmq
	brew install drush
	
	chmod -R ug+w /usr/local/Cellar/php55/5.5.10/lib/php
    	pear config-set php_ini /usr/local/etc/php/5.5/php.ini
	pear config-set auto_discover 1
	
	pear channel-discover pear.phpunit.de
	pear install pear.phpunit.de/PHPUnit
	pear channel-discover pear.phpdoc.org
	pear install phpdoc/phpDocumentor-alpha
	
#### Apps

	brew cask install diffmerge
	brew cask install mongoHub
	brew cask install virtualbox
	brew cask install genymotion
	brew cask install sequel-pro
	brew cask install versions

- Appstore
	- Base
	- xScope
	- JPEGmini Lite
	- Dash
	- XCode

#### Editor

I use sublime text and store the config in a [git repository](https://github.com/madsgraphics/ST3-User-package).
	
	brew cask install sublime-text3
	git clone https://github.com/madsgraphics/ST3-User-package ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/User

### Apps

#### Web tools.

	brew cask install google-chrome
	brew cask install firefox
	brew cask install adium
	brew cask install cyberduck
	brew cask install skype
	
- Appstore
	- tweetbot

#### Photos

	brew cask install imagealpha
	brew cask install imageoptim

- Suites
 	- Adobe CreativeCloud
	- Nik SilverFX Pro
- Appstore
	- Aperture

#### Music & Videos
	
	brew cask install musicmanager
	brew cask install spotify
	brew cask install xld
	brew cask install handbrake
	brew cask install vlc

- Appstore
	- imovie
	
#### Productivity

	brew cask install libreoffice
	brew cask install nvalt
	brew cask install calibre

- Suites
	- MS Office
- Appstore
	- Airmail
	- ReadKit
	- Pages
	- Keynote
	- Marked
	- MultiMarkdown Composer
	- Glui
	- Mindnode Pro
