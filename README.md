fvscurl
=============

IIJ GIOストレージサービス FV/S に、メジャーなコマンドラインhttpクライアントであるcurlを使ってアクセスするときに便利なスクリプトです。
REST APIにリクエストを送るときに必要な、認証パラメータを計算してcurlから送るリクエストに付与します。

[Amazon S3 Authentication Tool for Curl](http://aws.amazon.com/code/128)をベースにしています。
同ソフトウェアと同様、Apache License, Version 2.0です。

必要なもの
-------

* Perl 5.6.0以降
* Curl (http://curl.haxx.se/)
* CPANモジュール Digest-HMAC, FindBin,  MIME-Base64,  Getopt-Long-2.38

私の手元の環境(Mac OS X 10.7.2)では、どれも新たにインストールする必要はありませんでした。

セットアップ
-------

ホームディレクトリに以下のような書式で、AccessKeyidとSecretAccessKeyを記述したファイルを .fvscurl として保存しておきます。


    %fvsSecretAccessKeys = (
        # personal account
        personal => {
            id => '1ME55KNV6SBTR7EXG0R2',
            key => 'zyMrlZUKeG9UcYpwzlPko/+Ciu0K2co0duRM3fhi',
        },
    
       # corporate account
       company => {
            id => '1ATXQ3HHA59CYF1CVS02',
            key => 'WQY4SrSS95pJUT95V6zWea01gBKBCL6PI0cdxeH8',
        },
    );


使い方の例
-------

[friendly-name]は、.fvscurlで指定したpersonalやcompanyといったものです。

Bucketのリストを表示

    ./fvscurl.pl --id=[friendly-name] -- http://gss.iijgio.com/[bucket-name]

Bucketを作成

    ./fvscurl.pl --id=[friendly-name] --createBucket  -- http://gss.iijgio.com/[bucket-name]

ObjectをPUTするとき

    ./fvscurl.pl --id=[friendly-name] --put=<file-name> -- http://gss.iijgio.com/[bucket-name]/[key-name]

ObjectをDELETEするとき

    ./fvscurl.pl --id=[friendly-name] --delete -- http://gss.iijgio.com/[bucket-name]/[key-name]

ObjectをCOPYするとき

    ./fvscurl.pl --id=[friendly-name] --copy=[source-bucket-name/source-key-name] -- http://gss.iijgio.com/[bucket-name]/[key-name]
