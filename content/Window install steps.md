- Tải Ubuntu, zsh,
- https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH
- https://ohmyz.sh/
### Install ZSH
- zsh autocomplete: 
```
sudo git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
- Thêm vào plugin
```
plugins=(
	...
	zsh-autosuggestions
)
```

- zsh hightlight:
```
sudo git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

``` bash
plugins=(
  ... 
  zsh-syntax-highlighting
)
```

- Oh-my-posh (tải cho window trước)
	- https://ohmyposh.dev/docs/installation/linux
	- nerd font
	- Tạo folder, tải themes, add dòng sau vào .zshrc
	``` bash
	eval "$(oh-my-posh init zsh --config ~/themes/jandedobbeleer.omp.json)"
	```
- Cách add alias
	``` bash
	alias cdD='cd ../../../../mnt/d'
	```
### Oh-my-posh powershell
- Chạy trong powershell admin:
	``` bash
	Set-ExecutionPolicy -ExecutionPolicy Unrestricted
	Install-Module PsReadLine -Force
	```
- Làm như doc: https://ohmyposh.dev/docs/installation/windows
	``` bash
	oh-my-posh init pwsh --config '"C:\Users\HoangHiep\AppData\Local\Programs\oh-my-posh\themes\velvet.omp.json"' | Invoke-Expression
	```

#### Powershell autocomplete
- Bật powershell, ấn f2
- add 2 dòng sau vào $PROFILE
	``` bash
	Set-PSReadlineKeyHandler -Key Tab -Function Complete
	Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete
	```
	