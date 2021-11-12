# opniz

![logo](./extras/images/logo.png)

`❗ このプロジェクトは現在アルファ版です。`

opnizとはM5StackといったESP32デバイスをNode.jsからobnizライクに遠隔制御するための、**Node.js SDK**および**Arduinoライブラリ**です。  
しくみとしてはESP32デバイスおよびNode.js SDK間にて**JSON形式のRPCメッセージ**をやりとりし、相互に定義されたメソッドを呼び合います。  

![overview](./extras/images/overview.png)

現在Node.js SDK、Arduinoライブラリともに**ESP32**および**M5ATOM**クラスを実装しています。  
M5ATOMクラスで**M5Stack、M5StickC、M5ATOM Lite、M5ATOM Matrixでの動作を確認しています。**  

新たなデバイスクラスや独自のメソッドを簡単に拡張できる設計となっています。  
また**クラウド環境（PaaS、FaaS等）でも動作**させることができます。  



## Node.js SDK

アルファ版をGitHubにて公開しています。  

**[opniz-sdk-nodejs](https://github.com/miso-develop/opniz-sdk-nodejs)**

デバイスのRead/Writeを実行したり（Pinも動的に指定可能です）、デバイス側からのイベント（たとえばM5Stack系デバイスのボタン等）を受け取って非同期に処理を実行したりできます。  



## Arduinoライブラリ

アルファ版をGitHubにて公開しています。  
現在M5ATOM向けとESP32向けのライブラリをそれぞれ公開しています。  

**[opniz-arduino-m5atom](https://github.com/miso-develop/opniz-arduino-m5atom)**  
**[opniz-arduino-esp32](https://github.com/miso-develop/opniz-arduino-esp32)**  

Node.js SDKからのRPCリクエストを処理するハンドラと、ESP32デバイスからのRPCイベントを発火するエミッタを実装したデバイスクラスを提供します。  
Arduino IDEおよびPlatformIOに対応しています。  


## 実装状況

現在M5ATOM、ESP32クラスを実装しています。  
これらのクラスはそれぞれ対応するArduinoライブラリを模しています。  
これらのクラスを継承して簡単に新たなデバイスクラスを拡張できる設計となっています。  

ESP32クラスを継承したM5ATOMクラスの実装を参照すると拡張のヒントになると思います。  

たとえば[Node.js SDKのM5ATOMクラス](https://github.com/miso-develop/opniz-sdk-nodejs/blob/main/src/devices/M5Atom.ts)ではLEDを制御する`dis.drawpix`メソッドと、デバイスのボタンを押したときの`onbutton`メソッドを実装しています。  
これらメソッドはそれぞれ、デバイスに対する命令と、デバイスからのイベント処理の実装です。  
opnizの拡張はこの2種類の動作を定義していくだけです。  

[ArduinoライブラリのM5ATOMクラス](https://github.com/miso-develop/opniz-arduino-m5atom/blob/main/src/opniz/M5Atom.cpp)では、Node.js SDKからの制御メッセージを受け取るハンドラと、デバイスのボタンを押したときにNode.js SDKへイベントを発火するエミッタをそれぞれ実装しています。  
必要に応じて同様にハンドラ、エミッタを継承実装することで拡張が行えます。  



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
