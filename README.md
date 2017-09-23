# WebIOPi Tutorial

## WebIOPi とは
ウェブブラウザのボタンからGPIOを操作したり、逆にGPIOから値を取得して表示したりが簡単に実現するソフトウェア.


## install
1. 環境
raspbian内で
```
$ cat /etc/debian_version
8.0

$ cat /etc/issue
Raspbian GNU/Linux 8 \n \l
```

---
2. WebIOPiのダウンロード
<http://sourceforge.net/projects/webiopi/files/WebIOPi-0.7.1.tar.gz/download>にアクセスすると、downloadが始まる.


---
3. インストール
```
$ cd	###上のファイルをダウンロードした場所に移動する
$ tar zxf WebIOPi-0.7.1.tar.gz
$ cd WebIOPi-0.7.1/
$ wget https://raw.githubusercontent.com/doublebind/raspi/master/webiopi-pi2bplus.patch
$ patch -p1 -i webiopi-pi2bplus.patch
$ sudo ./setup.sh
```

---
4. unit file のダウンロード
```
$ cd 
$ wget https://raw.githubusercontent.com/neuralassembly/raspi/master/webiopi.service
$ sudo mv webiopi.service /etc/systemd/system/
```

---
5. WebIOPiの起動
```
$ sudo /etc/init.d/webiopi start
```

---
6. 起動確認
```
$ ps ax |grep webiopi
### これでgrep以外のプロセスが見えれば良い.
```
ログファイルは、/var/log/webiopi


---
7. WebIOPiの停止
```
$ /etc/init.d/webiopi stop
```

---
8. 停止確認
```
$ ps ax |grep webiopi
### これでgrep以外のプロセスが見えれなければ良い.
```


## web browser から接続
web browser から "http://[raspberry pi の ip address]:8000/" にアクセス.
パスワードを要求されるが、デフォルトでは、
	- username
		- webiopi
	- password
		- raspberry



