# 以下コマンドでインストール

$ModuleName = "AddComma"
$GitHubName = "MuraAtVwnet"
Invoke-WebRequest -Uri https://raw.githubusercontent.com/$GitHubName/$ModuleName/master/OnlineInstall.ps1 -OutFile ~/OnlineInstall.ps1
& ~/OnlineInstall.ps1


<#
このリポジトリは、以下コンテンツで使用しているリポジトリです

[後で書く]
#>

<#
Uninstall 方法
& ~/UnInstallAddComma.ps1
#>

