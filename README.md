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
为保证最佳体验,设备分辨率建议在1080P及以上,并且已登录哔哩哔哩账户.
## 新样式
改变顶栏的样式,并有一些界面微调.
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
- 搜索
- 直播间
- 相簿查看
- 新番时间表

之后会陆续添加其他页面,不支持推广板块(会被`删除广告`功能去除的部分).
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

(只对旧版播放器生效,新版播放器已经默认外置)
#### 放大按钮
增大控制栏的按钮间距,使触摸操作更准确.
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
## 隐藏热搜词
将搜索框的热搜词替换为`搜索`.
## 全屏修复
修复点击全屏按钮无响应的问题.

点击全屏时, b站的源代码中会检查浏览器是否为`Chrome XX.X.XXX5.1`和`window.Element`是否包含`ALLOW_KEYBOARD_INPUT`属性, 然后向`requsetFullscreen`传递不同的参数. 而部分浏览器不允许向此API传参数, 全屏操作就会失败.

附:视频全屏代码
```js
request: function(c) {
    var f = d.requestFullscreen;
    c = c || document.documentElement;
    if (/5\.1[\.\d]* Safari/.test(navigator.userAgent))
        c[f]();
    else
        try {
            var b = Element;
            c[f](g && b.ALLOW_KEYBOARD_INPUT)
        } catch (e) {
            c[f]()
        }
},
```
直播间全屏代码
```js
b.request = function(b) {
    var a = c.requestFullscreen;
    b = b || document.documentElement;
    if (/5\.1[\.\d]* Safari/.test(window.navigator.userAgent))
        b[a]();
    else {
        var g = Element
            , d = !1;
        g && "ALLOW_KEYBOARD_INPUT"in g && g.ALLOW_KEYBOARD_INPUT && (d = !0);
        b[a](d)
    }
}
```
## 直播间
### 缩放看板娘
根据屏幕DPI缩放看板娘的大小以提高像素的清晰度.
### 删除直播水印
删除观看直播时角落的水印.

# 设置
脚本启用后,在网页左侧中央会有一个齿轮图标,点击即可打开设置.

**设置保存后,需要刷新网页才能生效.**
![设置](images/gui-settings.png)
## 默认值
### 样式
- 新样式: `开启`
    - 自定义颜色: `浅蓝色(#00A0D8)`
    - 顶栏(对横幅)不透明度: `0.382`
    - 夜间模式: `关闭`
    - 搜索栏位置调整: `开启`
        - 显示顶部横幅: `开启`
### 工具
- 自动展开弹幕列表: `开启`
- 删除广告: `开启`
- 稍后再看重定向: `开启`
- 隐藏热搜词: `关闭`
- 全屏修复: `关闭`
### 直播间
- 缩放看板娘: `开启`
- 删除直播水印: `开启`
### 触摸
- 顶栏触摸优化: `关闭`
- 播放器触摸支持: `关闭`
    - 启用实验性动画效果: `关闭`
    > 因为部分浏览器对包含实验性效果的动画没有优化会很卡, 所以开放此选项.

# 关于新版播放器
目前新版播放器不是默认开启的,可在旧版播放页面右侧找到入口.

如果没有找到入口,也可以手动在浏览器开发者工具(快捷键通常为`F12`)中的控制台运行[脚本](utils/enable-new-player.js)开启.

# 兼容性
## ![Chrome:兼容](https://img.shields.io/badge/Chrome-兼容-brightgreen.svg?style=flat-square&colorB=009688)
- 触摸调整框的背景模糊效果(`backdrop-filter`)需要手动在`chrome://flags/#enable-experimental-web-platform-features`中开启.
## ![Firfox:部分兼容](https://img.shields.io/badge/FireFox-部分兼容-yellow.svg?style=flat-square&colorB=1976D2)
- 滚动条样式无效.
- 触摸调整框的背景模糊效果无效.
- 触摸调整的进度预览有弹跳现象.(来自`transition: all 0.2s;`. 短时间内总是从原数值开始变化,而不是当前数值)
## ![Edge:部分兼容](https://img.shields.io/badge/Edge-部分兼容-yellow.svg?style=flat-square&colorB=1976D2)
- 滚动条样式无效.
- 由于Edge的CSS渲染bug(主要集中在`filter`和`color`), 部分自定义颜色错乱.
- 顶栏触摸体验不佳.
- 触摸功能需要手动在`about:flags`中开启.
## ![Safari:未知](https://img.shields.io/badge/Safari-未知-lightgrey.svg?style=flat-square&colorB=323232)
尚未在Safari中测试.
