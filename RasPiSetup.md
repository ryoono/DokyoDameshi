# Raspberry Pi セットアップ手順  

多分何回かセットアップしなくてはならないため，手順をメモっておく  
[ここ](https://101010.fun/iot/raspi-samba.html)を参考にしているが，リンクが切れているといけないので一応下に記載する  

### やりたいこと  

Sambaをインストールする  
共有ファイル設定する  

## RasPi側の設定  
### Sambaインストール  

```sh
$ sudo apt-get install samba
```  

### Sambaの設定  

```sh
$ sudo nano /etc/samba/smb.conf
```

以下のように修正する  

```sh
# +++変更前+++

# By default, the home directories are exported read-only. Change the
# next parameter to 'no' if you want to be able to write to them.
   read only = yes

# File creation mask is set to 0700 for security reasons. If you want to
# create files with group=rw permissions, set next parameter to 0775.
   create mask = 0700

# Directory creation mask is set to 0700 for security reasons. If you want to
# create dirs. with group=rw permissions, set next parameter to 0775.
   directory mask = 0700

# +++変更後+++

# By default, the home directories are exported read-only. Change the
# next parameter to 'no' if you want to be able to write to them.
   read only = no 

# File creation mask is set to 0700 for security reasons. If you want to
# create files with group=rw permissions, set next parameter to 0775.
   create mask = 0644

# Directory creation mask is set to 0700 for security reasons. If you want to
# create dirs. with group=rw permissions, set next parameter to 0775.
   directory mask = 0755
```

### Sambaへユーザ追加  

```sh
# ユーザ名がpinお場合
$ sudo smbpasswd -a pi
```

### Sambaの再起動  

設定の反映をしてRasPi側の設定は完了  

```sh
$ sudo service smbd restart
```

## Mac側の設定  

### 共有フォルダアクセス  

Finder → 移動 → サーバへ移動...  

```
smb://raspberrypi.local
```

あとは成り行きで上手く接続してくだしい(飽きた)  