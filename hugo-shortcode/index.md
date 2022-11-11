# 速查！Hugo Shortcodes 语法手册

<!--more-->

Markdown 的内容格式虽然简单，但是有时它也不尽如人意，在很多方面都无法很好地支持，这时内容编辑者就需要使用纯 HTML 来扩展可能性，这与 Markdown 语法的优美简洁相矛盾。

为了尽可能避免使用 HTML 以保持内容简洁，Hugo 创建了 Shortcodes 来规避这些限制。`Shortcodes` 是内容文件中的一个简单片段，可以生成合理的 HTML 代码，并且符合 Markdown 的设计哲学。在站点生成时，Hugo Shortcodes 将轻松合并到更改中，避免了可能复杂的搜索和替换操作。

通常无需记忆具体的语法，只要知道每个参数所代表的意义即可，你可以借助[搜狗拼音输入法](https://shurufa.sogou.com/?r=mac&t=pinyin)的自定义短语功能，将预设好参数的标签插件添加新短语，从而通过缩写实现快捷输入。

![自定义短语](LqA5LsZB4p.png)

![添加新短语](rto0sMWz5l.png)

## 内置简码

Hugo 附带了一组预定义的 Shortcodes，实现了一些常见的用法，以保持 Markdown 内容简洁。更具体的内容参数请阅读 [Hugo Shortcodes 文档](https://gohugo.io/content-management/shortcodes/)，下表仅为简单使用的短代码简表。

|   作用   | 语法                                                         |
| :------: | ------------------------------------------------------------ |
|   图片   | `{{</* figure src="图片地址" title="图片标题" */>}}`         |
|   gist   | `{{</* gist 用户名 gist-id */>}}`                            |
| 语法高亮 | `{{</* highlight html */>}}`……`{{</* /highlight */>}}`       |
| 前置参数 | `{{</* param Front-matter参数名称 */>}}`                     |
| 页面链接 | 用法1：`[文章标题]({{</* ref "文章文件的相对路径地址" */>}})`<br>用法2：`[文章标题]({{</* relref "文章标题的碎片链接地址" */>}})` |
|   推特   | `{{</* tweet user="用户名" id="文章ID" */>}}`                |
| YouTube  | 用法1：`{{</* vimeo 视频ID */>}}`<br>用法2：`{{</* youtube 视频ID */>}}` |



## 扩展简码

[DoIt](https://hugodoit.pages.dev/zh-cn/theme-documentation-extended-shortcodes/) 主题在 Hugo 内置的 Shortcodes 的基础上提供多个扩展的 Shortcodes，支持 Markdown 或 HTML 格式。更具体的内容参数请阅读 [DoIt 扩展 Shortcodes 使用文档](https://hugodoit.pages.dev/zh-cn/theme-documentation-extended-shortcodes/)，下表仅为简单使用的短代码简表。

|    作用    | 语法                                                         |
| :--------: | ------------------------------------------------------------ |
| 自定义样式 | `{{</* style "CSS样式" */>}}` ……`{{</* /style */>}}`         |
|    链接    | `{{</* link "链接地址" 链接的标题 "悬停在链接上显示的提示" */>}}` |
|    图片    | `{{</* image src="图片地址" caption="图片的标题" title="悬停在图片上显示的提示" */>}}` |
|  提示横幅  | `{{</* admonition 横幅类型 "标题" true或false */>}}`……`{{</* /admonition */>}}`<br>其中横幅类型可选：note、abstract、info、tip、success、question、warning、failure、danger、bug、example、quote |
|  数据图表  | 用法1：`{{</* mermaid */>}}`……`{{</* /mermaid */>}}`<br>用法2：`{{</* echarts */>}}`……`{{</* /echarts */>}}`<br>具体请参考 [mermaid](https://mermaidjs.github.io/) 和 [Echarts](https://echarts.apache.org/zh/index.html) |
|    地图    | `{{</* mapbox 经度值 纬度值 缩放比例 */>}}`                  |
|    音乐    | 用法1：`{{</* music url="本地音乐链接" name=音乐名字 artist=歌手 cover="音乐封面" */>}}`<br>用法2：`{{</* music "第三方音乐链接" */>}}`<br>用法3：`{{</* music 音乐平台 音乐类型 音乐ID */>}}`<br>其中音乐平台可选：netease、tecent、kugou、xiami、baidu；音乐类型可选：song、playlist、album、search、artist |
|  bilibili  | `{{</* bilibili BVid 分P数 */>}}`                            |
|  打字动画  | 简单打字动画：`{{</* typeit */>}}`……`{{</* /typeit */>}}`<br><br>代码打字动画：`{{</* typeit code=代码语言名称 */>}}`…… `{{</* /typeit */>}}`<br>段落打字动画：`{{</* typeit group=paragraph */>}}`…… `{{</* /typeit */>}}` |
| Javascript | `{{</* script */>}}`……`{{</* /script */>}}`                  |
|    友链    | `{{</* friend "名字" "友链" "头像" "简介" */>}}`             |
|  项目展示  | `{{</* showcase "项目标题" "项目简介" "项目封面图" "项目链接" */>}}` |
|  数学公式  | `{{</* math */>}}`……`{{</* /math */>}}`                      |

## 更多简码

这部分是我收集的自定义简码，需要在 `~/layouts/shortcodes/` 下创建 `name.html` 文件后使用，目前仅在 DoIt 主题使用过，不一定适用于全部主题，请视情况使用。

### 文字位置

这个简码的功能是设定文字的位置（居左、居中、居右、两端对齐等等），支持的样式基于 CSS 语法。你需要在 `~/layouts/shortcodes/` 下创建 `align.html` 文件，其内容如下：

```html
<p style="text-align:{{ index .Params 0 }}">{{ index .Params 1 | markdownify }}</p>
```

使用时只需要把需要改变位置的文字填在双引号处即可，示例源码如下。

```markdown
{{</* align left "文字居左" */*/>}}
{{</* align center "文字居中" */*/>}}
{{</* align right "文字居右" */*/>}}
```

## 参考内容


- [Hugo Shortcodes](https://gohugo.io/content-management/shortcodes/)
- [DoIt 扩展 Shortcodes](https://hugodoit.pages.dev/zh-cn/theme-documentation-extended-shortcodes/)
- [自定义 Hugo Shortcodes 简码](https://guanqr.com/tech/website/hugo-shortcodes-customization/)

