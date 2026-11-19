---
title: 提取/修改Apple Pay卡面图片的方法
date: 2023-03-29 01:51:49
toc: true
---
## 卡面图片保存路径
#### ①第三方App内添加的卡片
在第三方App内调用苹果钱包接口添加卡片后，资源文件会缓存文件至：
`/private/var/mobile/Containers/Data/Application/com.apple.PassbookUIService/Library/Caches/com.apple.PassbookUIService/fsCachedData/`

1. 文件夹中约4～6KB大小的文件，重命名为.zip并解压
2. `cardBackgroundCombined*.urls`里面是卡面资源URL

#### ②备份到iCloud的卡片
在设置中添加卡片时，曾经添加过并备份到iCloud的卡片会临时下载到：
`/private/var/mobile/Containers/Data/Application/com.apple.Passbook/tmp/TemporaryItems/com.apple.Passbook/{unique_id}.pkpass/`

1. 开启iCloud中的Wallet备份，然后删除卡片
2. 打开Wallet App中的添加卡片界面，选择 "为你找到的卡片 - 来自其他设备"（Cards Found For You - From other devices），等待卡面图片加载完毕
3. 保持Wallet App处于上述界面不动，打开`{unique_id}.pkpass/cardBackgorundCombined*.urls`，里面是卡面图片URL

#### ③钱包内的卡片
钱包内的卡片路径位于
`/var/mobile/Library/Passes/Cards/{unique_id}.pkpass/`

- `{unique_id}.pkpass/cardBackgorundCombined*.urls`里面是卡面图片URL

- 修改图片文件`{unique_id}.pkpass/cardBackgroundCombined*`，**返回上一层目录，删掉`{UUID}.cache`文件夹**，即可修改Wallet中显示的卡面图片

- 修改 `/var/mobile/Library/Passes/passes23.sqlite`（passes表）和 `{unique_id}.pkpass/pass.json` 中对应卡片的`label_color` 和`foreground_color`，可以修改Wallet中显示的卡号颜色等，注意修改此文件后必须重启手机Wallet才能正常显示卡片

  <img src="database.png">

## 访问上述路径的方法
#### FilzaSlop / 3105 (iOS 18, iOS 26, iOS 27 beta 1–4)
这个漏洞可以提供上述①②路径的读取权限

闲鱼购买P12开发者证书，使用”全能签“等工具签名并安装 [FilzaSlop](https://github.com/0xjohnnydev/FilzaSlop)

应用数据目录位于`FilzaSlopeHome/[HMA-C2] App Data`

#### AirLift漏洞 (iOS18.0–27.0.1, iOS 27.2 beta 1–2)
这个漏洞可以提供上述①②③路径的**读写**权限
具体实现有 [AirCard](https://github.com/Mak5er/AirCard)

#### 越狱
越狱后可以获得上述①②③路径的读写权限

使用Filza等文件管理器参照上述路径保存/修改文件即可



## 我提取的卡面
PDF卡面推荐使用Illustrator打开

| Card Name | Resource Name |
| :--- | :--- |
| JALカード | [cardBackgroundCombined.pdf](https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/65e35a6b4bac418d8047bd4a402151cd) |
| JCBカードWplusL | [cardBackgroundCombined.pdf](https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/15fd74b8a7fa4313bf72df6101bd3345) |
| LinePay Credit | [cardBackgroundCombined.pdf](https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/a1dc6a5ef4d34a15ab97abcea9413676) |
| LinePay Prepaid | [cardBackgroundCombined.pdf](https://pr-pod5-smp-device-asset.apple.com:443/broker/v1/assets/1bce5a713c5343ed8a47fd7b6a3392b7) |
| merpay電子マネー（初版） | [cardBackgroundCombined.pdf](https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/c101d28967624f679a368c259bdeaa00) |
| merpay電子マネー（第三版） | [cardBackgroundCombined.pdf](https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/26c5d22654944bce8c2d4dc59257c958) |
| PASMO | [cardBackgroundCombined.pdf](https://nc-pod5-smp-device-asset.apple.com:443/broker/v1/assets/545c264d20a84c6394650f7bd68fc894) |
| Revolut (Blue) | [cardBackgroundCombined@2x.png](https://pr-pod8-smp-device-asset.apple.com:443/broker/v1/assets/3a74988d788a4fe1881fd11d0ee10902) |
| Revolut (Lilac) | [cardBackgroundCombined@2x.png](https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/d466a912c0c74a2297d79560ee5a229f) |
| Suica (Penguin) | [cardBackgroundCombined.pdf](https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/570d9e16c9a84a029160db32330a1f35) |
| Suica (No Penguin) | [cardBackgroundCombined.pdf](https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/E4kYwaAy41Gsyaut7k7GnvyCAqA8h449UNNB3ibgtNcK) |
| VポイントPay | [cardBackgroundCombined.pdf](https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/7d3b5510d96a4c0e80e0fe5b58f742a1) |
| 上海公共交通卡 | [cardBackgroundCombined@2x.png](https://tj-pod2-smp-device-asset.apple.com/broker/v1/assets/08a0a13df96c4261ace41638616db85a) |
| 上海公共交通卡-支付宝 | [cardBackgroundCombined@2x.png](https://tj-pod2-smp-device-asset.apple.com:443/broker/v1/assets/eea508f166674421bf4d1165ad5ea1ed) |
| 三井住友カードOliveフレキシブルペイ | [cardBackgroundCombined@2x.png](https://nc-pod8-smp-device-asset.apple.com:443/broker/v1/assets/0da16003ac0c45829028c9e00f1cc633) |
| 三井住友カードOliveフレキシブルペイ Credit Mode Only | [cardBackgroundCombined@2x.png](https://pr-pod8-smp-device-asset.apple.com:443/broker/v1/assets/31e7c52a8bf44ff7a5fee79611412dca) |
| 三井住友カードOliveフレキシブルペイ（旧版PDF卡面） | [cardBackgroundCombined.pdf](https://pr-pod5-smp-device-asset.apple.com:443/broker/v1/assets/06e1a2c57613420e9be5394661616920) |
| どこでもmajica | [cardBackgroundCombined.pdf](https://pr-pod8-smp-device-asset.apple.com:443/broker/v1/assets/57486ed788ef46138c3bb0e5ac970552) |
| 中国银行长城借记卡 | [cardBackgroundCombined@3x.png](https://sh-pod2-smp-device-asset.apple.com:443/broker/v1/assets/8089fecd7b6b4a91a80b1498f0f888c1) |
| 中国银行长城洛天依联名借记卡 | [cardBackgroundCombined@2x.png](https://sh-pod2-smp-device-asset.apple.com:443/broker/v1/assets/1b8b55c14fa142e59c3cd86fefec1a00) |
