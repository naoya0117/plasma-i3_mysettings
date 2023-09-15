# plasma-i3_mysessions
- plasma-i3とplasma-kwin両方のセッションをデスクトップマネージャに表示させる
- plasma-i3セッションではplasmaセッション上でi3を操作するため、特有のウィンドウルールが必要である。
- ~/.coonfig/i3 への設定ファイルは
  [https://naoya0117/myi3settings/i3/config](https://github.com/naoya0117/myi3settings/blob/main/i3/config)
  または、https://github.com/heckelson/i3-and-kde-plasma を参照すること
## 使用方法
- 本環境ではsystemdサービスを使用している。（systemctlコマンド）
- 事前にsddm、または、同等の処理ができるDMをインストールしておくこと。
```
# pacman -S sddm
# systemctl enable sddm
```
plasmaとi3をインストールする
```
# pacman -S plasma i3 plasma
```
-  リポジトリのlocal-bin の中身を/usr/local/bin にコピーし、実行権限を付与する。
```
# cd /usr/local/bin/
# chmod a+x ./plasma-i3.sh
# chmod a+x ./plasma-kwin.sh
```
- 当リポジトリの xsessionsの中身を /usr/share/xsessions にコピーする（ファイル名は自由に変更してよいが、既存のsessionファイルを上書きしないこと。パッケージ更新時に自動で置き換わる可能性あり。）

## メモ
- plasma settingsのsplash screenはNoneにする ```systemsettings```
- /usr/share/xsessions 上の使わないセッションはbackupディレクトリでも作りその中に移動させておくと、SDDM上で表示されなくなる

例：
```.
├── backup
│   ├── i3.desktop
│   ├── i3-with-shmlog.desktop
│   └── plasma.desktop
├── plasma-i3.desktop
└── plasma-kwin.desktop

```

- kwin-sessionとi3-session間で環境を共有するためstartup-applicationは~/.config/i3/.configファイルではなくxdg-autostartを使用すべき。
- i3-sessionでは、各アプリケーションにおいてauthorization-errorが起こることがある。(vscodeなど)この場合、```path/to/application --password-store kwallet```としたものを/usr/local/binに保存しておくと良い。
  /usr/local/binの優先度を上げておく必要あり。)
