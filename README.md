# robosys_DevieDriver_2020
ロボットシステム学の課題１で作成したLEDをコントロールするデバイスドライバです。
## 目次
- 概要
- 動作環境
- 回路
- 実行コマンド
- ライセンス

## 概要
- 1~4の入力で数字に対応したLEDが点灯
- 0の入力で全LEDを消灯
- tの入力で16秒までのタイマー(時間は点灯・消灯をそれぞれ1・0とした2進数で表される)

[実際に動かした動画:YouTube](https://www.youtube.com/watch?v=cMpp3_HkJ5c)

## 動作環境
- Raspberry Pi 3 Model B
  - Ubuntu 20.04 LTS
- ブレッドボード
- LED × 4
- 抵抗 330Ω × 4
- ジャンパ線 × 8

## 回路
回路図と実際に組み立てたものは以下の通りです。
![circuit diagram](https://github.com/katsuharuogata/hoge/blob/main/kairo.png)  
回路図
![real thing](https://github.com/katsuharuogata/hoge/blob/main/jitubutu.jpg)  
実物

## 実行コマンド
### ビルド
動作させるためにまずこのリポジトリをクローンしビルドします。  
カーネルモジュールをインストールして、権限を変更します。
```
$ git clone https://github.com/katsuharuogata/robosys_DevieDriver_2020.git
$ cd robosys_DviceDriver_2020/myled
$ make
$ sudo insmod myled.ko
$ sudo chmod 666 /dev/myled0
```
### 入力:0~4
入力文字とGPIOは以下のように対応しています。入力するとそれぞれに繋げたLEDが点灯します。
1. GPIO18
2. GPIO23
3. GPIO24
4. GPIO25

0を入力するとすべてのLEDが消灯します。
```
$ echo 1 > /dev/myled0
```
### 入力:t
tと入力すると16秒まで測れるタイマがスタートします。  
左から順にGPIO 18,23,24,25に繋いだLEDを設置することで、点灯が1、消灯が0として、2進数で時間が表現されます。
```
$ echo t > /dev/myled0
```
### 後始末
カーネルモジュールをアンインストールします。
```
$ sudo rmmod myled
$ make clean
```

## ライセンス
[GNU General Public License v3.0](https://github.com/katsuharuogata/robosys_DevieDriver_2020/blob/main/LICENSE)
