# Bilibili-Evolved
增强哔哩哔哩Web端体验的油猴脚本.

# 安装
需要浏览器拥有[Tampermonkey](https://tampermonkey.net/)或同类插件.

[![正式版](https://img.shields.io/badge/正式版-🌸-green.svg?style=flat-square&colorB=009688)](https://github.com/the1812/Bilibili-Evolved/raw/master/bilibili-evolved.user.js)

正式发布的版本,最稳定,更新频率较慢.

[![预览版](https://img.shields.io/badge/预览版-🍺-yellow.svg?style=flat-square&colorB=607D8B)](https://github.com/the1812/Bilibili-Evolved/raw/preview/bilibili-evolved.preview.user.js)

新增内容测试的地方,更新频率快,但功能不稳定.

[![离线版](https://img.shields.io/badge/离线版-👻-blue.svg?style=flat-square)](https://github.com/the1812/Bilibili-Evolved/raw/master/bilibili-evolved.offline.user.js)

内置所有依赖项以提高加载速度,体积较大,可以不受GitHub服务器不稳定的影响. 由于任何依赖项更新后此脚本也需更新,所以更新频率会高于正式版.

# 功能概览
## 新样式
改变顶栏的样式,并有一些界面微调,适用于主站和新版播放器.暂不支持直播,相簿.

设备分辨率建议在1080P及以上.
### 效果
![主站](images/new-navbar.png)
![播放](images/new-navbar-stardust.png)
### 自定义颜色
![粉色](images/new-navbar-stardust.png)
![紫色](images/new-navbar-purple.png)
![蓝色](images/new-navbar-lightBlue.png)
![绿色](images/new-navbar-teal.png)
![暗蓝色](images/new-navbar-blueGrey.png)
### 夜间模式(实验性)
夜间模式更适合光线暗的环境,并会大量应用自定义颜色.

目前支持的页面有:
- 主站
- 动态
- 新版视频
- 稍后再看
- 观看历史
- 专栏阅读
- 个人空间
- 消息中心

之后会陆续添加其他页面.
#### 启用前
![日间](images/light-style.png)
#### 启用后
![夜间](images/dark-style.png)
### 搜索框位置调整
在主站(非新版播放器)中,总是把搜索框置于顶栏.
#### 启用前
![不调整](images/original-navbar.png)
#### 启用后
![调整](images/override-navbar.png)
### 移除横幅
在搜索框位置调整启用的时候,还可以使用此功能移除顶部横幅.
#### 启用前
![不移除](images/override-navbar.png)
#### 启用后
![移除](images/no-banner.png)
## 触摸支持
### 顶栏
删除顶栏右侧的一级链接(从`大会员`到`历史`),以方便触屏设备快速预览信息.被删除的链接可从各预览中的`查看更多`进入.
### 播放器
#### 启用触摸控制
- 左右滑动可调整进度
- 上下滑动可调整音量
- 进度调整可在左上角和右上角取消
- 在不同位置滑动,可以使用3档不同的灵敏度.

![进度调整](images/adjust-playback.png)
![音量调整](images/adjust-volume.png)

已知问题: 滑动调整的音量不会保存,下次打开视频将恢复原音量.
#### 外置网页全屏
因为触屏设备很难做出"鼠标悬停",`网页全屏`将从`全屏`的鼠标悬停菜单中移动到外部.
#### 放大按钮
放大控制栏的按钮及间距,使触摸操作更准确.
##### 启用前
![放大前](images/player-buttons-original.png)
##### 启用后
![放大后](images/player-buttons-large.png)
## 自动展开弹幕列表
新版播放页面中,弹幕列表默认收起以显示推荐的其他视频.启用此功能可在每次加载视频时自动展开弹幕列表.
## 删除广告
删除嵌于页面中的推广横幅.
### 删除前
![删除前](images/remove-ads-before.png)
### 删除后
![删除后](images/remove-ads-after.png)
## 稍后再看重定向
将稍后再看的链接重定向为普通播放网址,以使用新版播放页面.

# 设置
脚本启用后,在网页左侧中央会有一个齿轮图标,点击即可打开设置.

**设置保存后,需要刷新网页才能生效.**

![设置](images/gui-settings.png)

# 兼容性
## ![Chrome](https://img.shields.io/badge/Chrome-兼容-brightgreen.svg?style=flat-square&colorB=009688)
- 触摸调整框的背景模糊效果(`backdrop-filter`)需要手动在`chrome://flags/#enable-experimental-web-platform-features`中开启.
## ![Firfox](https://img.shields.io/badge/FireFox-部分兼容-yellow.svg?style=flat-square&colorB=FF6F00)
- 滚动条样式无效.
- 滤镜效果不仅无抗锯齿,还会使部分布局错位.
- 触摸调整框的背景模糊效果无效.
## ![Edge](https://img.shields.io/badge/Edge-部分兼容-yellow.svg?style=flat-square&colorB=FF6F00)
- 自定义颜色与滚动条样式无效.
- 滤镜效果无抗锯齿.
- 半透明颜色(`#rrggbbaa`)无效*.
- 顶栏触摸体验不佳.
- 触摸功能需要手动在`about:flags`中开启.

*Edge将考虑用rgba()实现半透明颜色.
## ![Safari](https://img.shields.io/badge/Safari-未知-lightgrey.svg?style=flat-square&colorB=323232)
尚未在Safari中测试.
