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
ログファイルは、/var/log/webiopi 。起動しなかったり動作がおかしかったらこのファイルをtail -fしてみると良い。


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


## web browser から WebIOPi への接続方法
web browser から "http://[raspberry pi の ip address]:8000/" にアクセス.
パスワードを要求されるが、デフォルトでは、
- username : webiopi  
- password : raspberry


## Programing Tutorial
1. WebIOPi の処理フロー
- 参考 : <http://webiopi.trouch.com/Tutorial_Basis.html>

WebIOPiには、HTMLリソースとREST APIの両方を提供するHTTPサーバーが含まれている。  
ウェブブラウザは、まずHTMLファイルをロードし、そこに含まれているJavascriptがUIを制御および更新するためにREST APIへの非同期呼び出しを行う。
```
[Web browser]                                                                     [WebIOPi]
http://<raspberryPi's ip>:8000/ にアクセス   ---- GET index.html ------------->   
                                             <--- index.html     --------------

index.html の読み込み                        ---- GET script.js  ------------->
                                             <--- script.js      --------------

script.js が動作                             ---- GET or POST , REST API ----->  
                                             <--- Some Response from WebIOPi --
```
