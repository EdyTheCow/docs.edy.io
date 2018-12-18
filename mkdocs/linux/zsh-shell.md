# Installing zsh shell

TODO: format it nicely into sections

Installing package
sudo apt install zsh

Installing zsh basic configs
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

Setting zsh as default shell
Incase there's issue with above installation you can manually set shell using
sudo vi /etc/passwd
Change it from bash to zsh for specific user

Set a theme
Edit ~/.zshrc and change theme to agnoster
