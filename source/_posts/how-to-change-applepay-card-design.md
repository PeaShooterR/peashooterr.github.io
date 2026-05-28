---
title: 越狱修改Apple Pay卡面
date: 2023-03-29 01:51:49
toc: true
---

## 修改卡面图片

替换`/var/mobile/Library/Passes/Cards/aaa.pkpass/cardBackgroundCombined*`**返回上一层目录，删掉`aaa.cache`文件夹**，呼出Apple Pay界面即可看到卡面变化。

<!--more-->

## 原始卡面图片

PDF卡面推荐使用Illustrator打开

| Card Name | Resource Name | URL |
| :--- | :--- | :--- |
| JALカード | cardBackgroundCombined.pdf | https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/65e35a6b4bac418d8047bd4a402151cd |
| JCBカードWplusL | cardBackgroundCombined.pdf | https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/15fd74b8a7fa4313bf72df6101bd3345 |
| LinePay Credit | cardBackgroundCombined.pdf | https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/a1dc6a5ef4d34a15ab97abcea9413676 |
| LinePay Prepaid | cardBackgroundCombined.pdf | https://pr-pod5-smp-device-asset.apple.com:443/broker/v1/assets/1bce5a713c5343ed8a47fd7b6a3392b7 |
| PASMO | cardBackgroundCombined.pdf | https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/545c264d20a84c6394650f7bd68fc894 |
| Suica | cardBackgroundCombined.pdf | https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/570d9e16c9a84a029160db32330a1f35 |
| メルペイ電子マネー | cardBackgroundCombined.pdf | https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/c101d28967624f679a368c259bdeaa00 |
| 三井住友カードOliveフレキシブルペイ | cardBackgroundCombined@2x.png | https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/0da16003ac0c45829028c9e00f1cc633 |
| 三井住友カードOliveフレキシブルペイ Credit Mode Only | cardBackgroundCombined@2x.png | https://pr-pod8-smp-device-asset.apple.com:443/broker/v1/assets/31e7c52a8bf44ff7a5fee79611412dca |
| 三井住友カードOliveフレキシブルペイ（初版PDF卡面） | cardBackgroundCombined.pdf | https://pr-pod5-smp-device-asset.apple.com:443/broker/v1/assets/06e1a2c57613420e9be5394661616920 |
| 中国银行长城借记卡 | cardBackgroundCombined@3x.png | https://sh-pod2-smp-device-asset.apple.com:443/broker/v1/assets/8089fecd7b6b4a91a80b1498f0f888c1 |
| 中国银行长城洛天依联名借记卡 | cardBackgroundCombined@2x.png | https://sh-pod2-smp-device-asset.apple.com:443/broker/v1/assets/1b8b55c14fa142e59c3cd86fefec1a00 |

## 我修改的卡面
点击图片下载
[<img src="LinePay_Credit.png" style="zoom:28%;" />](LinePay_Credit.pdf)			[<img src="LinePay_Prepaid.png" style="zoom:28%;" />](LinePay_Prepaid.pdf)			[<img src="SMBC_Olive.png" style="zoom:28%;" />](SMBC_Olive.pdf)



## 修改卡号颜色

同时修改以下两个文件里对应卡片的`label_color` 和`foreground_color`

`/var/mobile/Library/Passes/passes23.sqlite` （所有卡片信息都在`pass`表里）

`aaa.pkpass/pass.json`

删除`aaa.cache`**重启**手机即可生效。

如果你在没有重启的情况下直接打开了Wallet，你会发现所有卡片都消失了，不用担心，它们并没有被移除，重启后即可恢复。
