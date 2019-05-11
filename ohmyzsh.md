install zsh - this is more powerful than regular bash
```
sudo apt-get update && sudo apt-get -y install zsh .
#Check version to verify installation zsh --version .
#Make Zsh your default shell chsh -s /bin/zsh . You will be prompted to enter your password.
chsh -s /bin/zsh
#Logout exit .
exit
#Log back into the system ssh <newuser>@[vultr-ip-address] .
```
install ohmyzsh brings in templates
```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
