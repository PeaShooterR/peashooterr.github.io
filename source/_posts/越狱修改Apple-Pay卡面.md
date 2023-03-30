---
title: 越狱修改Apple Pay卡面
date: 2023-03-29 01:51:49
toc: true
---

## 修改卡面图片

替换`/var/mobile/Library/Passes/Cards/aaa.pkpass/cardBackgroundCombined*`**返回上一层目录，删掉`aaa.cache`文件夹**，呼出Apple Pay界面即可看到卡面变化。

<!--more-->

## 原始卡面图片

推荐使用Illustrator打开

* merpay: https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/c101d28967624f679a368c259bdeaa00

* LinePay Prepaid: https://pr-pod5-smp-device-asset.apple.com:443/broker/v1/assets/1bce5a713c5343ed8a47fd7b6a3392b7

* LinePay Credit: https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/a1dc6a5ef4d34a15ab97abcea9413676
* Suica: https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/ddcbbde0aa184031b5b9f19966162ce4
* SMBC Olive: https://pr-pod5-smp-device-asset.apple.com:443/broker/v1/assets/06e1a2c57613420e9be5394661616920
* 中国银行长城借记卡（png）:https://sh-pod2-smp-device-asset.apple.com:443/broker/v1/assets/9d437cf7b19d4280ae521659ebb3c26f 

## 我修改的卡面
点击图片下载
[<img src="LinePay_Credit.png" style="zoom:28%;" />](LinePay_Credit.pdf)			[<img src="LinePay_Prepaid.png" style="zoom:28%;" />](LinePay_Prepaid.pdf)			[<img src="SMBC_Olive.png" style="zoom:28%;" />](SMBC_Olive.pdf)



## 修改卡号颜色

同时修改以下两个文件里对应卡片的`label_color` 和`foreground_color`

`/var/mobile/Library/Passes/passes23.sqlite` （所有卡片信息都在`pass`表里）

`aaa.pkpass/pass.json`

删除`aaa.cache`**重启**手机即可生效。

如果你在没有重启的情况下直接打开了Wallet，你会发现所有卡片都消失了，不用担心，它们并没有被移除，重启后即可恢复。
