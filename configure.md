# Configure

## SSH Key
ssh-keygen -t rsa -C "liuchong12233@163.com"  
ssh-keygen -t rsa -C "liuchong12233@163.com"  

## Git
git config --global user.email "liuchong12233@163.com"  
git config --global user.name "liuchong"  
git config --global core.editor vim  
git config --global alias.st status  
git config --global alias.co checkout  
git config --global alias.ci commit  
git config --global alias.br branch  
git config --global color.ui auto    

## wsl 2.0 
使用管理员权限启动 powershell后安装 wsl  
wsl --install
wsl --update
wsl --set-version Ubuntu 2

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart  
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart  

