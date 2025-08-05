計算結果を PowerShell でカンマ付きにしてクリップボードに格納する

計算結果をカンマ編集してクリップボードに格納する「AddComma」フィルタ書きました

2025-08-05_00007.png


■ コマンド実行結果を表示しつつクリップボードに格納する
コマンド実行結果をクリップボードにセットする方法として clip.exe を使う方法が良く知られています

例えば、dir の結果をクリップボードにセットのであれば「dir | clip」とします

2025-08-05_00001.png

この場合は、コマンド結果が clip.exe にリダイレクトされてしまい、dir 結果を確認するには、クリップボードに格納されている内容を何かにペーストしなくてはなりません

コマンド実行結果のクリップボード格納格納と、実行結果表示を両立させるのには、PowerShell の「Set-Clipboard -PassThru」を使うと実現できます

Set-Clipboard は「scb」とエリアスがセットされているので、「scb -PassThru」とすれば OK です
(-PassThru オプションは -p[TAB]　で補完できます)

2025-08-05_00002.png

■ 計算結果をカンマ編集してクリップボードに格納する

PowerShell は計算式を入力すると、計算結果を表示できるので、電卓アプリより便利だったりします

2025-08-05_00004.png

そのままだと、計算結果がカンマ編集されないので、桁数が大きいと結果確認に難があります
とはいえ、柔軟に対応できるのも PowerShell の利点なので、ToString を使ってカンマ編集させるとこんな感じになります

2025-08-05_00005.png

これを「scb -PassThru」にリダイレクトしてクリップボードに格納に格納すれば良いですが、この呪文を都度入力するのは現実的はありませんね

■ フィルタとして実装する
PowerShell でリダイレクトを受け取る方法としてフィルタを書く手があります

コードにするとこんな感じです

filter AddComma{
    $_.ToString("#,0.##########") | Set-Clipboard -PassThru
}

こいつを組み込んでしまえば、面倒な呪文を書かなくでも「AddComma」にリダイレクトすれば、カンマ編集とクリップボード格納が出来ます
(addc[TAB]でAddCommaに補完できます)

2025-08-05_00006.png


■ コマンドの組み込み
以下を PowerShell にコピペすれば「AddComma」がオンラインインストールされます

$ModuleName = "AddComma"
$GitHubName = "MuraAtVwnet"
Invoke-WebRequest -Uri https://raw.githubusercontent.com/$GitHubName/$ModuleName/master/OnlineInstall.ps1 -OutFile ~/OnlineInstall.ps1
& ~/OnlineInstall.ps1

■ コマンドの Uninstall
以下コマンドを入力すると「AddComma」は Uninstall されます

& ~/UnInstallAddComma.ps1

■ コード一式は、以下リポジトリで公開しているます
https://github.com/MuraAtVwnet/AddComma
git@github.com:MuraAtVwnet/AddComma.git

■ Web サイト
以下で Web コンテンツにしています

計算結果を PowerShell でカンマ付きにしてクリップボードに格納する
https://www.vwnet.jp/windows/PowerShell/2025080501/AddComma.htm
