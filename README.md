# convert-markdown-to-git

「vscodeでphpのセットアップ」からはサンプルです。
自分がQiitaに投稿した内容はこちらです。
https://qiita.com/_wow_/items/6f7d3bb722cc3286f7c5

---

# vscodeでphpのセットアップ  

## メインセットアップ  

下記サイトをもとに拡張機能のインストールまで進めていきます。  
※デバッグ実行やComposerなどは後述の手順でセットアップをします。  
　Gitはすでに入っているため飛ばします。  

https://qiita.com/tfukumori/items/97a8f1ac6532612b004f  

## サブセットアップ  

### デバッグ実行  

デバッグ実行時になぜかブレークポイントで止まらなかったので、正常に動いた設定を下記に記載しています。  

setting.json  
・何もしない  

``` launch.json  
{  
  "version": "0.2.0",  
  "configurations": [  
    {  
      "name": "Listen for XDebug",  
      "type": "php",  
      "request": "launch",  
      "port": 9000  
    },  
    {  
      "name": "Launch currently open script",  
      "type": "php",  
      "request": "launch",  
      "program": "${file}",  
      "cwd": "${fileDirname}",  
      "port": 9000  
    }  
  ]  
}  
```  

``` php.ini  
[XDebug]  
zend_extension = xdebug  
xdebug.mode=debug  
xdebug.start_with_request=yes  
xdebug.client_port=9000  
```  

上記設定をしたあとに、XAMPPのApacheを再起動します。  
hello.phpにブレークポイントを設定して、「Listen for XDebug」でデバッグを実行します。  
確認用URL: http://localhost/hello/index.html  

「submit」ボタンを押すことで、ブレークポイントで止まるのを確認できます。  

### Composer、Laravel  

下記サイトをもとにComposerとLaravelのセットアップをします。  

https://www.sejuku.net/blog/106106  

#### Laravel追記  

Laravelのプロジェクトを作成したい場所でプロンプトを開き、下記コマンドを実行します。  

``` cmd  
composer create-project laravel/laravel --prefer-dist Sample  
```  

E:\xampp\htdocsでコマンドを実行すると下記のようになります。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/604560/a5027c8a-4abb-2870-e5e0-109904e42e03.png)  

下記ファイルの任意の箇所にブレークポイントを設定します。  
E:\xampp\htdocs\Sample\routes\web.php  

作成したプロジェクトのlaunch.jsonを下記内容で更新し、「Listen for Xdebug」でデバッグを実行します。  
``` launch.json  
    {  
      "name": "Listen for Xdebug",  
      "type": "php",  
      "request": "launch",  
      "port": 9000  
    },  
```  

XAMPP(ザンプ)のApacheを再起動します。  
※下記の「apache_start.bat」でapacheを再起動できます。  
　apacheが起動中に「apache_stop.bat」を実行しても停止しないです。  
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/604560/953e3e89-d2e2-5b33-c301-dc6f3f4cb852.png)  


下記URLにアクセスすると、ブレークポイントで止まります。  
処理を続行すると下図画面が表示されます。  
確認用URL: http://localhost/Sample/public/  

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/604560/15525f84-9f9f-2d01-9235-bdf41197785b.png)  

### ルートパス変更  

下記記事の設定をするとhttp://localhost/Sample/public/ をhttp://localhost に省略できます。  
設定パス: /xampp/htdocs/Sample/public  

https://webstyle.work/xampp-document-root/  



