---
title: 【Python】RPCライブラリ・フレームワークまとめ
tags:
  - Python
  - RPC
  - gRPC
private: false
updated_at: '2025-12-02T00:09:48+09:00'
id: a027f2f18f926d975683
organization_url_name: null
slide: false
ignorePublish: false
---
RPCフレームワークとしてまず挙げられるのは [gRPC](https://grpc.io/) であるかと思いますが、そもそもなぜgRPCが注目されているのか、他にライブラリやフレームワークがあるのかといったことが気になったのでこの機会にまとめます。

# REST vs RPC
RPCはRESTと同じくWeb APIを実現するための手法です。各サービス間の連携方法として広く採用されているのはRESTですが、RESTは一定の原則こそあるものの、複雑で自由度が高くベストプラクティス的なものがほぼ存在しません。

一方、RPCは仕様がすでに決まっていることが多く、開発者は考慮するべき点が絞られるため本来集中すべき開発に時間を割くことができます。

例えば、RPCのフレームワークであるgRPCは、 `.proto` という拡張子ファイルにインターフェース定義を作成することで、これに準拠するサーバ・クライアントのソースコードのひな型が自動生成されます。`.proto` は言語に依存しないIDLであるため、インターフェース定義のドキュメントとしての効果もあるといえます。

以下のスライドが詳しいです。

[マイクロサービスバックエンドAPIのためのRESTとgRPC](https://www.slideshare.net/disc99_/apirestgrpc)

# PythonのRPCライブラリ・フレームワークまとめ
| RPC | プロトコル | QuickStart |
|:-:|:-:|:-:|
| [xmlrpc](https://docs.python.jp/3/library/xmlrpc.html) | [XML-RPC](https://ja.wikipedia.org/wiki/XML-RPC) |  |
| [json-rpc](http://json-rpc.readthedocs.io/en/latest/quickstart.html) | [JSON-RPC](http://www.jsonrpc.org/specification) | http://json-rpc.readthedocs.io/en/latest/quickstart.html |
| [Mprpc](http://mprpc.readthedocs.io/en/latest/intro.html) | [MessagePack](https://msgpack.org/) | http://mprpc.readthedocs.io/en/latest/intro.html　|
| [gRPC](https://grpc.io/) | [Protocol Buffers](https://developers.google.com/protocol-buffers/) | https://grpc.io/docs/quickstart/python.html |

Pythonで実装できるRPCは調べてみたところ、4種類ありました。それぞれ採用しているプロトコルが大きな違いで、これによってデータ形式が異なります。それぞれ公式のQuickStartを試してみることで違いがわかるかと思います。それぞれの特徴をまとめてみます。

# [xmlrpc](https://docs.python.jp/3/library/xmlrpc.html)
> XML-RPC は HTTP 経由の XML を使って遠隔手続き呼び出し (Remote Procedure Call) を実現する方法です。XML-RPC を使うと、クライアントはリモートサーバー (サーバーは URI で名前付けられます) 上のメソッドを引数付きで呼び出して、構造化されたデータを受け取る事ができます。

Python3の標準ライブラリ（Python2では[xmlrpclib](http://docs.python.jp/2/library/xmlrpclib.html)）で、プロトコルは[XML-RPC](https://ja.wikipedia.org/wiki/XML-RPC)。
データ形式はXMLです。

# [json-rpc](http://json-rpc.readthedocs.io/en/latest/quickstart.html)
> 　This implementation does not have any transport functionality realization, only protocol. Any client or server implementation is easy based on current code, but requires transport libraries, such as requests, gevent or zmq, see examples.

> ・Vanilla Python, no dependencies.
・200+ tests for multiple edge cases.
・Optional backend support for Django, Flask.
・json-rpc 1.1 and 2.0 support.

プロトコルは[JSON-RPC](http://www.jsonrpc.org/specification)で、データ形式はJSONです。

# [Mprpc](http://mprpc.readthedocs.io/en/latest/intro.html)
> mprpc is a lightweight MessagePack RPC library. It enables you to easily build a distributed server-side system by writing a small amount of code. It is built on top of gevent and MessagePack.


プロトコルは[MessagePack](https://msgpack.org/)。

MessagePackとは、
> It's like JSON. but fast and small.

と謳っており、バイナリ形式のシリアライズ方式のため、JSONに比べ高速かつデータが小さいのが特徴です。

参考記事: [MessagePackをPythonで使ってみる](http://wapa5pow.hatenablog.com/entry/2015/04/18/120333)


# [gRPC](https://grpc.io/)
> gRPC is a modern open source high performance RPC framework that can run in any environment. It can efficiently connect services in and across data centers with pluggable support for load balancing, tracing, health checking and authentication. It is also applicable in last mile of distributed computing to connect devices, mobile applications and browsers to backend services.


Googleが開発したOSSのRPCフレームワークで、プロトコルは[Protocol Buffers](https://developers.google.com/protocol-buffers/)。

Protocol Buffersとは
> think XML, but smaller, faster, and simpler. 

らしく、下記のようなデータ構造になります。バイナリ形式のシリアライズ方式のため、XMLより高速かつデータが小さいのが特徴です。

```
message Person {
  required string name = 1;
  required int32 id = 2;
  optional string email = 3;
}
```

参考記事: [ProtocolBuffersについて調べてみた](https://qiita.com/aiueo4u/items/54dc5dd8c4772253634c)

# 所感
全てのQuickStartを試してみましたが、gRPCがもっともドキュメントが豊富で初心者にはありがたかったです。QuickStartが簡潔で学習コストが一番低かったのはMprpcだったので、PythonでRPCをサクッと実装してみたい時はオススメかもしれません。

# さいごに
データ形式によって様々なプロトコルが存在し、それごとにRPCのライブラリやフレームワークがあることがわかりました。これだけ種類があると使い分けはどうするという話になるかと思いますが、 ドキュメントが充実していて参考文献も豊富な `gRPC` を使っておけば問題ないと思います。また、Docker, Netflix、メルカリなどで採用実績があり、採用する理由としては十分そうです。Google様様ですね。
