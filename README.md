# opniz

<div align="center"><img src="https://user-images.githubusercontent.com/22117028/274112294-10c9323f-14d3-4986-ac3e-c73c16b87f4b.png" alt="logo"></div>

> ❗ このプロジェクトは現在アルファ版です。

opnizとはM5StackデバイスをNode.js（JavaScript / TypeScript）からobnizライクに実装できるオープンソースフレームワークです。  
Node.js SDKおよびArduinoライブラリがあり、WebSocketで相互通信を行います。  

しくみとしてはM5StackデバイスおよびNode.js SDK間にてJSON形式のRPCメッセージをやりとりし、相互に定義されたメソッドを呼び合います。  

![overview](https://user-images.githubusercontent.com/22117028/274111780-1f1e22ec-66ac-4cd0-bee3-1a19ee2eb65c.png)



## 対応デバイス

* M5Stack BASIC
* M5Stack Core2
* M5StickC
* M5ATOM Matrix
* M5ATOM Lite
* M5ATOM Echo
* M5ATOM U
* M5ATOMS3
* M5ATOMS3 Lite
* M5Stamp Pico
* M5Stamp S3
* その他ESP32、ESP32-PICO-D4、ESP32-S3デバイス



## Node.js SDK

**[opniz SDK for Node.js](https://github.com/miso-develop/opniz-sdk-nodejs)**

デバイスのRead/Writeを実行したり（Pinも動的に指定可能です）、デバイス側からのイベント（たとえばM5Stack系デバイスのボタン等）を受け取って非同期に処理を実行したりできます。  
[M5Unified](https://github.com/m5stack/M5Unified)をベースにM5Stackデバイス固有のメソッドも備えています。  



## Arduinoライブラリ

**[opniz Arduino Library for M5Unified](https://github.com/miso-develop/opniz-arduino-m5unified)**  

Node.js SDKからのRPCリクエストを処理するハンドラと、M5StackデバイスからのRPCイベントを発火するエミッタを実装したデバイスクラスを提供します。  
Arduino IDEおよびPlatformIOに対応しています。  
[M5Unified](https://github.com/m5stack/M5Unified)を内部で使用しており、Node.js SDKより同じ書き味でメソッドを使用できます。  

opniz CLIにて簡単にM5Stackデバイスへ書き込むことができます。  



## opniz CLI

**[opniz CLI](https://github.com/miso-develop/opniz-cli)**

opniz CLIはM5Stackデバイスへopniz ArduinoライブラリのBasicスケッチをコマンドから簡単に書き込めるCLIツールです。  
[Arduino CLI](https://github.com/arduino/arduino-cli)のラッパーCLIです。  



## opniz Server

**[opniz-server](https://github.com/miso-develop/opniz-server)**

opniz Serverはopniz Node.js SDKやopnizデバイスからのJSON RPCメッセージを中継するWebSocketサーバです。  
opniz Serverを介すことでWebSocketクライアント同士の接続（opnizデバイス、ブラウザ、Node.js SDK等）を行えます。  

クラウド環境（PaaS、FaaS等）でも動作するため、たとえば手元のPCで動作させたopniz Node.js SDKからインターネット越しの環境にあるopnizデバイスを制御するといったことも可能です。  

![opniz-server](https://user-images.githubusercontent.com/22117028/274111777-8f17b07d-380e-4f9f-8064-06fa9eb8cbde.png)



## 利用可能な通信プロトコル

opniz Node.js SDKでは以下の通信プロトコルを実装しています。  
デフォルトでは`WebSocket (Server)`が使用されます。  

* WebSocket (Server)
* WebSocket (Client)
* TCP (Server/Client同居)

opniz Arduinoライブラリでは以下の通信プロトコルを実装しています。  
デフォルトでは`WebSocket (Client)`が使用されます。  

* WebSocket (Client)
* TCP (Server/Client同居)

使用するプロトコルによりopnizのコンストラクタパラメータが変わってきます。  

またクラウド（PaaS、FaaS）へデプロイして動作させたり、Node.js SDK同士の接続も可能です。  



## ライセンス

[MIT](./LICENSE)
