
# Installing Mac

## Contents

* [AppStore](#appstore)
* [3rd party](#3rdparty)
* [Copy Files](#files)
* [Preferences](#preferences)
* [All Desktops Apps](#alldesktopapps)
* [Xcode](#commandlinetools)
* [Homebrew](#homebrew)
* [/etc git](#etc)
* [ZSH](#zsh)
* [Fonts](#fonts)
* [Dot files](#dotfiles)
* [gitconfig](#gitconfig)
* [ssh](#ssh)
* [Dotvim](#dotvim)
* [RVM](#rvm)
* [Heroku](#heroku)
* [Nodejs](#nodejs)
* [MySQL](#mysql)



<a name=appstore></a>
## AppStore

Login into the AppStore, go to "Purchases" and download all relevant apps.

<a name=3rdparty></a>
## 3rd party

* [Dropbox](https://www.dropbox.com)

* [Disk Inventory X](http://www.derlien.com/)

* [FireFox](http://www.firefox.com/)

* [Google Chrome](http://www.google.com/chrome/)

  sign into your gmail account to sync prefs.

  visit [http://www.google.com/ncr](http://www.google.com/ncr) in every browser
  you use so that Google will stop redirecting to the stupid local site.

* [iTerm2](http://www.iterm2.com)

  in Settings/Terminal set 'Unlimited scrollback'

* [SequelPro](http://www.sequelpro.com)
* [Transmission](http://www.transmissionbt.com)
* [VLC](http://www.videolan.org/)

* simplenote (https://simplenote.com)

[top](#top)<a name=files></a>
## Copy Files

Copy the following files over:

* `~/Documents/`
* `~/Downloads`
* `~/Desktop/`
* `~/bin/`

  add `~/bin` to the path:

        echo ~/bin | sudo tee /etc/paths.d/home-bin

[top](#top)<a name=preferences></a>
## Preferences

Go to system preferences and adjust the following:

* Dock
  * check "Automatically hide and show the Dock"
  * add spaces:
  
  	defaults write **com.apple.dock persistent-apps -array-add '{"tile-type"="spacer-tile";}'** to add a space 
  	
  	then
  	
  	**killall Dock** to restart dock

* Mission Control

  uncheck "Automatically rearrange spaces based on most recent use"

  uncheck "When switching to an application, switch to a space with open windows for the application"

* TimeMachine

  Exclude directories from TimeMachine backup

       sudo tmutil addexclusion -p ~/.dropbox
       sudo tmutil addexclusion -p ~/Dropbox
       sudo tmutil addexclusion -p ~/Google\ Drive/
       sudo tmutil addexclusion -p ~/Downloads/
       sudo tmutil addexclusion -p /usr/local/Cellar
       sudo tmutil addexclusion -p /usr/local/rvm

* Language & Text

  select required input sources

* Security & Privacy

  disable password reset through Apple ID

  turn on "File Vault"

  turn on Firewall

* Sharing

  Choose computer name

* Accessability

  Enable dragging with Drag Lock on "Mouse & Trackpad/Trackpad Options"

[top](#top)<a name=alldesktopapps></a>
## All Desktops Apps

Change the following apps to be on all desktops:
	
	(right click on the dock options->all desktops. need to be two desktops for the option to show)

* Preferences
* Activity Monitor

[top](#top)<a name=commandlinetools></a>
## XCODE
install xcode

## Homebrew

* Install [Homebrew](http://mxcl.github.com/homebrew/).
* brew install macvim git wget imagemagick dos2unix watch tree pstree
* brew install tmux mtr iftop htop-osx gpg2 ctags
* brew install md5deep ack s3cmd unrar
* brew install tig

[top](#top)<a name=etc></a>
## /etc git

    sudo su -
    cd /etc/
    git init
    chmod 700 .git
    git add .
    git commit -m initial

[top](#top)<a name=zsh></a>
## ZSH

    brew install zsh zsh-completions

    git clone https://github.com/ofridagan/dotzsh.git .zsh
    ln -sfn .zsh/zshrc .zshrc

    echo /usr/local/bin/zsh | sudo tee -a /etc/shells
    chsh -s /usr/local/bin/zsh

    # edit /etc/paths and move /usr/local/bin to the 1st line
    # also add /usr/local/sbin just as the 2nd line
    vim /etc/paths

[top](#top)<a name=inconsolata></a>
## [Fonts](#fonts)

- wget http://www.levien.com/type/myfonts/Inconsolata.otf -O /Library/Fonts/Inconsolata.otf
- wget https://gist.github.com/raw/1595572/Inconsolata-dz-Powerline.otf -O /Library/Fonts/Inconsolata-dz-Powerline.otf
- wget https://gist.github.com/raw/1595572/Menlo-Powerline.otf -O /Library/Fonts/Menlo-Powerline.otf
- wget https://gist.github.com/raw/1595572/mensch-Powerline.otf -O /Library/Fonts/mensch-Powerline.otf
- vim fonts (from my gmail)


[top](#top)<a name=dotfiles></a>
## Dot files

    cd ~
    git clone https://github.com/ofridagan/dotfiles .dot
    cd .dot
    make install

This will install the following:

* ~/.local-after.vim
* ~/.zsh/local
* /etc/gitconfig
* ~/.gitconfig

[top](#top)<a name=gitconfig></a>
### Gitconfig

Homebrew's git system file is not quite properly set. it points to version
install dir and not to /usr/local/etc. we will need to link it every git install/upgrade:

First note the path of the system gitconfig file:

    git config --system -l

Link to /etc (use the path from previous command). e.g.:

    # for older versions of git this will be something like
    sudo ln -sfn /etc/gitconfig /usr/local/Cellar/git/1.7.11.4/etc/

    # for the newer ones:
    sudo ln -sfn /etc/gitconfig /usr/local/etc/


Verify it works:

    git lga

> NOTE: in older versions of brew git system config directory was inside the
> brew's Cellar, so you had to re-do this every time you installed a new
> version of git. The latest versions though, use /usr/local/etc/gitconfig
> instead, so you only need to do it once.

[top](#top)<a name=ssh></a>
## SSH

Copy your `~/.ssh` directory over from the old system or backup.

## SSH (new system / user)

Generate ssh keys:

    ssh-keygen -t dsa

[top](#top)<a name=dotvim></a>
## Dotvim

    cd ~
    git clone git@github.com:ofridagan/dotvim.git .vim
    ln -sfn .vim/vimrc .vimrc

    cd .vim
    make install

This is my ~/.vimrc.after

	set guifont=Sauce\ Code\ Powerline\ Light:h14
	let g:Powerline_symbols = 'fancy'

	set cul
	set foldcolumn=4

	if has('gui_running')
	  set background=dark
	else
	  set background=dark
	end
	colorscheme solarized

	let g:nerdtree_tabs_open_on_gui_startup = 0

	map ` :Switch<cr>
	nnoremap <leader>W :retab<cr>:%s/\s\+$//<cr>:let @/=''<cr>

	set shiftwidth=2

	" defines that a .ctrlp (empty) file marks the root of searches for ctlp (in
	" addition to .git folder)
	let g:ctrlp_root_markers = ['.xxx']

[top](#top)<a name=rvm></a>
## RVM

    curl -L https://get.rvm.io | sudo bash -s stable

After the install go to Preferences and add your user to the rvm group. Logout
and re-login. now you are able to run rvm commands.

    brew install libksba

    rvm install ruby

    brew tap homebrew/dupes
    brew install apple-gcc42

    rvm install 1.9.2

    CFLAGS="-I/opt/X11/include" rvm install 1.8.7


[top](#top)<a name=heroku></a>
## Heroku

Copy `~/.heroku/accounts` from the old machine.

Then:

    gem install heroku
    heroku plugins:install git://github.com/ddollar/heroku-accounts.git

Verify by running

    heroku accounts

[top](#top)<a name=nodejs></a>
## Nodejs
	brew install node
	
[top](#top)<a name=mysql></a>
## MySQL

* Download 64bit Community Server DMG archive from [MySQL](http://mysql.com).
* Mount it
* install 3 components:
  * mysql
  * MySQL.prefpane
  * MySQLStartupItem
* setup paths:

        echo /usr/local/mysql/bin | sudo tee /etc/paths.d/mysql
        echo /usr/local/mysql/man | sudo tee /etc/manpaths.d/mysql

### Library not loaded: libmysqlclient.18.dylib

If you get this error the magic incantation to fix it is this:

    sudo install_name_tool -change libmysqlclient.18.dylib /usr/local/mysql/lib/libmysqlclient.18.dylib /usr/local/rvm/gems/ruby-1.9.3-p286-falcon/gems/mysql2-0.2.13/lib/mysql2/mysql2.bundle

> NOTE: you need to use your real mysql2.bundle path. to find it out do:

    gem which mysql2

[top](#top)
## Copyright

© 2012 Vitaly Kushner, Astrails Ltd.
