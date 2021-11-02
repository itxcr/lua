## UI设置

### 函数：UINew 创建 UI

UINew(pagination,titles,okname,cancelname,config,orient,timer,width,height,bgcolor,btnbkcolor,bg,pagenumtype,selpage,titlesize, titlealign)

|    参数     |  类型  | 必填 | 说明                                                         |     默认值     |
| :---------: | :----: | :--: | :----------------------------------------------------------- | :------------: |
| pagination  | number |  否  | 显示的脚本配置页数                                           |       1        |
|   titles    | string |  否  | 标题，多页多标题之间用英文半角逗号分割                       |   "脚本配置"   |
|   okname    | string |  否  | 确定文字，UI 底部右侧文字                                    |     "开始"     |
| cancelname  | string |  否  | 取消文字，UI 底部左侧文字                                    |     "取消"     |
|   config    | string |  否  | 配置文件，保存配置到该文件                                   | "uiconfig.dat" |
|   orient    | number |  否  | UI 方向，仅支持 iOS， 0 - 向下；1 - 向右；2 - 向左           |       0        |
|    timer    | number |  否  | 倒计时时间，单位：秒。倒计时完成自动开始                     |      120       |
|    width    | number |  否  | 脚本配置显示宽度                                             |    屏幕宽度    |
|   height    | number |  否  | 脚本配置显示高度                                             |    屏幕高度    |
|   bgcolor   | string |  否  | 背景颜色，使用 RGB 十进制数值 以英文半角逗号分割             |    "0,0,0"     |
| btnbkcolor  | string |  否  | 按钮背景色，使用 RGB 十进制数值 以英文半角逗号分割           |    "0,0,0"     |
|     bg      | string |  否  | 背景图片，相对路径为 res 目录 可填写绝对路径                 |       -        |
| pagenumtype | string |  否  | 分页指示样式，dot - 小圆点 number - 数字；default - 不显示； tab - 底部不显示页码样式， 在顶部将分页标题显示为二级标签， 仅支持 Android**v3.2.0**、iOSv**3.1.5** 及其以上版本 |   "default"    |
|   selpage   | number |  否  | 默认停留页面                                                 |       1        |
|  titlesize  | number |  否  | titles 字体大小， 仅支持 Androidv3.2.1、iOSv3.1.6 及其以上版本， 仅支持 v1.3.4 及其以上版本 TSLib |       15       |
| titlealign  | string |  否  | titles 对齐方式，默认左对齐。可取值为：左对齐 left，右对齐 right，居中 center， 仅支持 Androidv3.2.1、iOSv3.1.6 及其以上版本， 仅支持 v1.3.4 及其以上版本 TSLib |     “left”     |

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
w,h = getScreenSize()
UINew("我的脚本","运行脚本","退出脚本","uiconfig.dat",0,120,w*0.9,h*0.9,"255,231,186","255,231,186") --方式一，宽高为屏幕的 90%
UIShow()
```

```lua
--titlealign、titlesize 仅支持 Androidv3.2.1、iOSv3.1.6 及其以上版本，仅支持 v1.3.4 及其以上版本 TSLib
--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
require "TSLib"
w,h = getScreenSize()
UINew("我的脚本1,我的脚本2","运行脚本","退出脚本","uiconfig.dat",0,120,w*0.9,h*0.9,"255,231,186","255,231,186","","tab",1,15,"right") --方式一，宽高为屏幕的 90%
UIShow()
```

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
w,h = getScreenSize()
UINew({titles="我的脚本",okname="运行脚本",cancelname="退出脚本"}) --方式二
UIShow()
```

- 默认配置文件路径：
  -  触动精灵 iOS 配置文件目录：/var/mobile/Media/TouchSprite/config/
  -  触动精灵安卓配置文件目录：/mnt/sdcard/TouchSprite/config/
  -  iOS 小精灵配置文件目录：/var/mobile/Media/小精灵包名/config/
  - 安卓小精灵配置文件目录：/mnt/sdcard/

- 可选参数如果写部分的话，该参数前的所有参数都必须需要填写，否则会报错。其他控件也一样
- 标题 titles，如果每页标题显示不一样该项请用逗号隔开，如："标题1,标题2,标题3"
- 函数有两种传入方式，普通和 table 方式，table 方式可选择性写入
- 函数方法内没有的参数，可以用 table 方式实现
- 使用 pagenumtype 参数中的 tab 会在顶部将 titles 内容显示为二级分页标签，非 tab 会将 titles 内容显示为顶部分页标题。

### 函数：UIShow 显示 UI

ret = UIShow(num)

| 参数 |  类型  | 必填 | 说明                                             |
| :--: | :----: | :--: | :----------------------------------------------- |
| num  | number |  否  | 是否判断返回值，0 - 判断返回值，默认为不进行判断 |

| 返回值 |  类型  |            说明            |
| :----: | :----: | :------------------------: |
|  ret   | number | 0 - 点击取消，1 - 点击开始 |

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UIShow() --显示 UI,UI 设置完成记得加上该函数，不然不能创建显示
```

```lua
--判断是否运行脚本
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
ret=UIShow(0) 
if ret == 1 then
    dialog("开始运行")
elseif  ret == 0 then
dialog("取消运行")
end
```

- UI 设置完成记得加上该函数，不然不能创建显示
- 选择退出默认自动退出脚本，如果需要自己处理，参数填 0，点取消返回值为 0，确定返回 1

### 函数：UILabel 文本标签

UILabel(num,text,size,align,color,width,nowrap,valign);

|  参数  |  类型  | 必填 | 说明                                                         |  默认值   |
| :----: | :----: | :--: | :----------------------------------------------------------- | :-------: |
|  num   | number |  否  | 控件所在页面页数，不能超过 UINew 的 pagination 参数          |     1     |
|  text  | string |  否  | 文字内容，需要显示的文字                                     |     -     |
|  size  | number |  否  | 字号，字体大小                                               |    15     |
| align  | string |  否  | 对齐方式 ，左对齐 left，右对齐 right，居中 center            |  "left"   |
| color  | string |  否  | 文字颜色，使用 RGB 十进制数值，以英文半角逗号分割            | "0,0,255" |
| width  | number |  否  | 控件宽度，默认 0 为一行，自定义宽度可写其他数值 Android 设备仅支持整数否则会提示 UI 格式错误； -1 为自适应屏幕，0 为占用整行， 大于等于 1 按照数字设置宽度，不填默认占整行， -1、0、及大于等于 1 的参数仅支持 Android**v3.2.0**、iOSv**3.1.5** 以及以上版本 |     0     |
| nowrap | number |  否  | 指定下一个控件是否换行，当此属性为 1 时 将指定下一个控件不换行 |     0     |
| valign | string |  否  | 垂直对齐方式，顶端对齐 top， 垂直居中 center，底部对齐 bottom，默认垂直居中， 仅支持 Androidv3.2.0、iOSv3.1.5 以及以上版本， 仅支持 v1.3.4 及其以上版本 TSLib | "center"  |

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UILabel("我的第一个脚本",15,"left","255,0,0",-1,0) --宽度写 -1 为一行，自定义宽度可写其他数值
UIShow()
--可选参数如果写部分的话，该参数前的所有参数都必须需要填写，否则会报错
```

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
w,h = getScreenSize()
UINew(2,"第一页,第二页","运行脚本","退出脚本","uiconfig.dat",0,120,w*0.9,h*0.9,"255,231,186","255,231,186","","tab",1,15,"right") --方式一，宽高为屏幕的 90%
UILabel("我的第一个脚本",15,"left","255,0,0",-1,0,"center")
UILabel("我的第二个脚本",15,"left","255,0,0",-1,0,"bottom")
UIShow()
```

```
--控件在一行
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UILabel("第一个",15,"left","0,0,0",100,1,"top") 
UILabel("第二个",15,"left","255,0,0",100,1,"center") 
UIShow()
```

- 本函数无返回值，只作文字显示

- 标签支持多行显示，在字符串中插入 \n 可以进行换行，例如：\"测试\n测试 1\n测试 2"

### 函数：UITextArea 多行文本框

UITextArea(num,id,prompt,text,size,align,color,kbtype,width,nowrap,height)

|  参数  |  类型  | 必填 | 说明                                                         |  默认值   |
| :----: | :----: | :--: | :----------------------------------------------------------- | :-------: |
|  num   | number |  否  | 控件所在页面页数，不能超过 UINew 的 pagination 参数          |     1     |
|   id   | string |  是  | 控件 ID                                                      |     -     |
| prompt | string |  是  | 提示文字（仅支持 Android）                                   |     -     |
|  text  | string |  是  | 默认文字，编辑框默认内容                                     |     -     |
|  size  | number |  否  | 字号，字体大小                                               |    15     |
| align  | string |  否  | 对齐方式，左对齐 - left，右对齐 - right，居中 - center       |  "left"   |
| color  | string |  否  | 文字颜色，使用 RGB 十进制数值，以英文半角逗号分割            | "0,0,255" |
| kbtype | string |  否  | 键盘类型，类型有 `number` `ascii` `default` 三种             | "default" |
| width  | number |  否  | 控件宽度，默认 -1 为一行， 自定义宽度可写其他数值， Android 设备仅支持整数否则会提示 UI 格式错误 |    -1     |
| nowrap | number |  否  | 指定下一个控件是否换行，当此属性为 1 时， 将指定下一个控件不换行 |     0     |
| height | number |  否  | 控件高度，支持 iOS v2.4.5-3、 Android v2.3.3.2 及其以上版本， Android 为默认高度，此参数 Android 写入数值不生效 |     -     |

```lua
--控件在一行
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UITextArea("选项1","1","测试1",30,"center","0,0,255","",200,1)
UITextArea("选项2","2","测试2",15,"left","0,0,255","",200,1)
UIShow()
dialog(选项1.."\r\n"..选项2)
--可选参数如果写部分的话，该参数前的所有参数都必须需要填写，否则会报错
```

### 函数：UIEdit 单行文本框

UIEdit(num,id,prompt,text,size,align,color,kbtype,width,nowrap,secure);

|  参数  |  类型   | 必填 | 说明                                                         |  默认值   |
| :----: | :-----: | :--: | :----------------------------------------------------------- | :-------: |
|  num   | number  |  否  | 控件所在页面页数，不能超过 UINew 的 pagination 参数          |     1     |
|   id   | string  |  是  | 控件 ID                                                      |     -     |
| prompt | string  |  是  | 提示文字，默认显示的文字                                     |     -     |
|  text  | string  |  是  | 默认文字，编辑框默认内容                                     |     -     |
|  size  | number  |  否  | 字号，字号大小                                               |    15     |
| align  | string  |  否  | 对齐方式，左对齐 left，右对齐 right，居中 center             |  "left"   |
| color  | string  |  否  | 文字颜色，使用 RGB 十进制数值 以英文半角逗号分割             | "0,0,255" |
| kbtype | string  |  否  | 键盘类型，`number` `ascii` `default`三种                     | "default" |
| width  | number  |  否  | 控件宽度，默认0 为占用一整行 自定义宽度可写其他数值， Android 设备仅支持整数否则会提示 UI 格式错误 -1 为自适应屏幕，0 为占用整行， 大于等于 1 按照数字设置宽度，不填默认占整行， -1、0、及大于等于1参数仅支持 Android**v3.2.0**、iOSv**3.1.5** 以及以上版本 |     0     |
| nowrap | number  |  否  | 指定下一个控件是否换行，当此属性为 1 时， 将指定下一个控件不换行 |     0     |
| secure | boolean |  否  | 是否明文显示，仅支持 v1.3.2 及其以上版本 TSLib， 默认是 false - 明文显示，true - 加密显示 |   false   |

```lua
--控件在一行
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UIEdit("edt1","测试","test1",15,"center","0,0,0","default",200,1,true)--返回值为字符串，若文本框内容为：测试，则返回 edt == "测试"
UIEdit("edt2","测试","test2",15,"left","255,0,0","default",200,1)
UIShow()
dialog("edt1 的选择值："..edt1.."\r\n".."edt2 的选择值："..edt2)
```

### 函数：UIRadio 单选组合

UIRadio(num,id,list,sel,width,nowrap,images,scale,countperline)

|     参数     |  类型  | 必填 | 说明                                                         | 默认值 |
| :----------: | :----: | :--: | :----------------------------------------------------------- | :----: |
|     num      | number |  否  | 控件所在页面页数 不能超过 UINew 的 pagination 参数           |   1    |
|      id      | string |  是  | 控件 ID                                                      |   -    |
|     list     | string |  是  | 文字选项，多个可选项目之间用英文半角逗号分割                 |   -    |
|     sel      | string |  否  | 默认选项编号，需填写选项编号，选项1编号为 0， 选项2为 1，依次类推，写为空为不选中 |  "0"   |
|    width     | number |  否  | 控件宽度，默认 -1 为一行， 自定义宽度可写其他数值， Android 设备仅支持整数否则会提示 UI 格式错误 |   -1   |
|    nowrap    | number |  否  | 指定下一个控件是否换行，当此属性为 1 时 将指定下一个控件不换行 |   0    |
|    images    | string |  否  | 图片选项，可以和 list 属性同时使用， 多个图片资源用英文半角逗号分割 |   -    |
|    scale     | number |  否  | 图片缩放范围 0 - 1                                           |   1    |
| countperline | number |  否  | 单行控件显示数量，Android 默认 1 行显示 1 个， iOS 控件总宽度超过屏幕宽度则堆积在一起， 引擎版本支持 iOS v3.00-157 及 Android v2.3.6 及其以上版本， 仅支持 TSLib 函数库 v1.2.4 及其以上版本 |   -    |

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UIRadio("rdo","选项1,选项2,选项3","1",-1,0,"",1,1)--3 个单选选项，默认选择选项 2
UIShow()
if rdo == "选项1" then--返回值为字符型
toast("选项1")
elseif rdo == "选项2" then
toast("选项2")
elseif rdo == "选项3" then
end
```

```lua
--控件在一行
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UIRadio("rdo1","测试1,测试2","1",200,1)--2 个单选选项，默认选择选项 2
UIRadio("rdo2","选项1,选项2","1",200,1)--2 个单选选项，默认选择选项 2
UIShow()
```

- 可选参数如果写部分的话，该参数前的所有参数都必须需要填写，否则会报错
- 返回值为选项名，选中第一个的话，返回 rdo == "选项1"，依此类推
- 选中项 sel 需填写选项编号，选项1 编号为 0，选项2 为 1，依次类推
- 由于单选为非此即彼的选择，返回值判断需要用到 if...then...elseif...then...else...then...end 判断语句
- iOS 设备 width 参数不能写的过小，否则可能出现无法选择参数的问题，出现此问题请调整 width 参数

### 函数：UICheck 多选组合

UICheck(num,id,list,sel,width,nowrap,images,scale,countperline)

|     参数     |  类型  | 必填 | 说明                                                         | 默认值 |
| :----------: | :----: | :--: | :----------------------------------------------------------- | :----: |
|     num      | number |  否  | 控件所在页面页数，不能超过 UINew 的 pagination 参数          |   1    |
|      id      | string |  是  | 多个可选项目之间用英文半角逗号分割                           |   -    |
|     list     | string |  是  | 文字选项，确定与变量名的项目数相同                           |   -    |
|     sel      | string |  否  | 默认选项编号，需填写选项编号，选项 1 编号为 0， 选项 2 为 1，依次类推；填写多个时以 @ 分割； 默认不选填空"" |  "0"   |
|    width     | number |  否  | 控件宽度，默认 -1 为一行， 自定义宽度可写其他数值， Android 设备仅支持整数否则会提示 UI 格式错误 |   -1   |
|    nowrap    | number |  否  | 指定下一个控件是否换行， 当此属性为 1 时将指定下一个控件不换行 |   0    |
|    images    | string |  否  | 图片选项，可以和 list 属性同时使用， 多个图片资源用英文半角逗号分割 |   ""   |
|    scale     | number |  否  | 图片缩放范围 0 - 1                                           |   1    |
| countperline | number |  否  | 单行控件显示数量，Android 默认 1 行显示 1 个， iOS 控件总宽度超过屏幕宽度则堆积在一起， 引擎版本支持 iOS v3.00-157 及 Android v2.3.6 及其以上版本， 仅支持 TSLib 函数库 v1.2.4 及其以上版本 |   -    |

**函数用例**

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UICheck("check1,check2,check3","选项1,选项2,选项3","0@1",-1,0,"",1,1)--默认选项：选项1 和选项2
UIShow()
if check1 == "选项1" then
    dialog("您选择了选项1",3)
end 
if check2 == "选项2" then
    dialog("您选择了选项2",3)
end
if check3 == "选项3" then
    dialog("您选择了选项3",3)
end
```

```lua
--控件不在一行
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UICheck("check1,check2,check3","选项1,选项2,选项3","0@1",200,1)--默认选项：选项1 和选项2
UICheck("check4,check5,check6","选项4,选项5,选项6","0@1",200,1)--默认选项：选项4 和选项5
UIShow()
```

**注意事项**

1. 可选参数如果写部分的话，该参数前的所有参数都必须需要填写，否则会报错。
2. 返回值为字符串，选中第一个和第二个的话，则：check1 == "选项1",check2 == "选项2"，依此类推。
3. 有多少个选项需要创建多少个变量来赋值，没有选中的变量为 nil。
4. 由于多选组合为允许并存的选择，判断返回值需要用到多个 if...then..end 判断语句
5. iOS 设备 width 参数不能写的过小，否则可能出现无法选择参数的问题，出现此问题请调整 width 参数。

### 函数：UICombo 下拉框

UICombo(num,id,list,sel,width,nowrap,prompt)

|  参数  |  类型   | 必填 | 说明                                                         | 默认值 |
| :----: | :-----: | :--: | :----------------------------------------------------------- | :----: |
|  num   | number  |  否  | 控件所在页面页数，不能超过 UINew 的 pagination 参数          |   1    |
|   id   | string  |  是  | 控件 ID                                                      |   -    |
|  list  | string  |  是  | 文字选项，多个可选项目之间用英文半角逗号分割                 |   -    |
|  sel   | string  |  否  | 默认选项编号，需填写选项编号，选项 1 编号为 0， 选项 2 为 1，依次类推 |  "0"   |
| width  | number  |  否  | 控件宽度，默认 0 占用一行，自定义宽度可写其他数值， Android 设备仅支持整数否则会提示 UI 格式错误， -1 为自适应屏幕，0 为占用整行， 大于等于 1 按照数字设置宽度，不填默认占整行， -1、0、及大于等于1参数仅支持 Android**v3.2.0**、iOSv**3.1.5** 以及以上版本 |   0    |
| nowrap | number  |  否  | 指定下一个控件是否换行，当此属性为 1 时， 将指定下一个控件不换行 |   0    |
| prompt | boolean |  否  | 点击提示，仅支持引擎版本 Android v3.1.3 及 iOS v3.0.6 及其以上版本， TLSib 仅支持 v1.2.9 及其以上版本， 默认为 false - 不弹点击提示，true - 弹点击提示 | false  |

**函数用例**

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UICombo("name","下拉框1,下拉框2,下拉框3","1",400,1,true)--默认选择：下拉框1
UIShow()
if name == "下拉框1" then--返回值为字符型
    toast("选择下拉框1")
elseif name == "下拉框2" then
    toast("选择下拉框2")
else
    toast("选择下拉框3")
end
```

1. 返回值为字符串，选中第一个的话，返回 name == "下拉框1"
2. 由于下拉框为非此即彼的选择，返回值判断需要用到 if...then...elseif...then...else...then...end 判断语句

### 函数：UIComboRlt 联动下拉框

UIComboRlt(num,id,list,data,source,sel,width,nowrap,prompt)

|  参数  |  类型   | 必填 | 说明                                                         | 默认值 |
| :----: | :-----: | :--: | :----------------------------------------------------------- | :----: |
|  num   | number  |  否  | 控件所在页面页数，不能超过 UINew 的 pagination 参数          |   1    |
|   id   | string  |  是  | 控件 ID                                                      |   -    |
|  list  | string  |  是  | 文字选项，多个可选项目之间用英文半角逗号分割                 |   -    |
|  data  | string  |  是  | 联动关联框选项，选择项有几项，需要用 # 号分割成几项          |   -    |
| source | string  |  是  | 标志名，与 UIComboRlts 的 dataSource 通过一致的字符串保证匹配 |   -    |
|  sel   | string  |  否  | 默认选项编号，需填写选项编号，选项 1 编号为 0， 选项 2 为 1，依次类推 |  "0"   |
| width  | number  |  否  | 控件宽度，默认 -1 为一行，自定义宽度可写其他数值， Android 设备仅支持整数否则会提示 UI 格式错误； -1 为自适应屏幕，0 为占用整行， 大于等于 1 按照数字设置宽度，不填默认占整行， -1、0、及大于等于1参数仅支持 Android**v3.2.0**、iOSv**3.1.5** 以及以上版本 |   0    |
| nowrap | number  |  否  | 指定下一个控件是否换行，当此属性为 1 时， 将指定下一个控件不换行 |   0    |
| prompt | boolean |  否  | 点击提示，仅支持引擎版本 Android v3.1.3 及 iOS v3.0.6 及其以上版本， TLSib 仅支持 v1.2.9 及其以上版本， 默认为 false - 不弹点击提示，true - 弹点击提示 | false  |

**函数用例**

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UIComboRlt("name1,name2","河北省,黑龙江省","石家庄市,承德市#哈尔滨市,齐齐哈尔市","test","0",400,0,true)
UIComboRlts("name2","test","0",500,1,true)--请保证变量名与标志项与联动框一致，返回值已通过联动框获取
UIShow()
if name1 == "河北省" and name2 == "石家庄市" then
    toast("河北省石家庄市")
elseif name1 == "河北省" and name2 == "承德市" then
    toast("河北省承德市")
elseif name1 == "黑龙江省" and name2 == "哈尔滨市" then
    toast("黑龙江省哈尔滨市")
elseif name1 == "黑龙江省" and name2 == "齐齐哈尔市" then
    toast("黑龙江省齐齐哈尔市")
end
--table 格式
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
w,h = getScreenSize()
UINew({titles="我的脚本",okname="运行脚本",cancelname="退出脚本"}) 
UIComboRlt({id="comborle,comborles",list="选项1,选项2,选项3",data="子选项1,子选项2,子选项3,子选项4#子选项5,子选项6,子选项7#子选项8,子选项9",source="test"})
UIComboRlts({id="comborles",dataSource="test"})
UIShow()
if  comborle =="选项1" then
    dialog("选项1".."\r\n选项"..comborles+1)
elseif comborle =="选项2" then
    dialog("选项2".."\r\n选项"..comborles+5)
elseif comborle =="选项3" then
    dialog("选项3".."\r\n选项"..comborles+8)
end
```

**注意事项**

1. 联动框第一个变量名请填写两个变量名，第二个变量名与关联框的变量名一致。否则会出现取值不对的问题
2. 返回值为字符串，联动框选择第二个，关联框选择第一个，则返回 name1 == "选项 2",name2 == "子选项 5"。

### 函数：UIComboRlts 联动关联框

**函数名称：关联框**

**函数功能：可作为 UIComboRlt 的子对象，通过标志项 dataSource 与 UIComboRlt**

**函数方法**

UIComboRlts(num,id,dataSource,sel,width,nowrap,prompt)

|    参数    |  类型   | 必填 | 说明                                                         | 默认值 |
| :--------: | :-----: | :--: | :----------------------------------------------------------- | :----: |
|    num     | number  |  否  | 控件所在页面页数，不能超过 UINew 的 pagination 参数          |   1    |
|     id     | string  |  是  | 控件 ID                                                      |   -    |
| dataSource | string  |  是  | 标志项，与 UIComboRlts 的 source 通过一致的字符串保证匹配    |   -    |
|    sel     | string  |  是  | 默认选项编号，需填写选项编号，选项 1 编号为 0， 选项 2 为 1，依次类推 |  "0"   |
|   width    | number  |  否  | 控件宽度，默认 0 为一行， 自定义宽度可写其他数值， Android 设备仅支持整数否则会提示 UI 格式错误； -1 为自适应屏幕，0 为占用整行， 大于等于 1 按照数字设置宽度，不填默认占整行， -1、0、及大于等于1参数仅支持 Android**v3.2.0**、iOSv**3.1.5** 以及以上版本 |   0    |
|   nowrap   | number  |  否  | 指定下一个控件是否换行，当此属性为 1 时， 将指定下一个控件不换行 |   0    |
|   prompt   | boolean |  否  | 点击提示，仅支持引擎版本 Android v3.1.3 及 iOS v3.0.6 及其以上版本， TLSib 仅支持 v1.2.9 及其以上版本， 默认为 false - 不弹点击提示，true - 弹点击提示 | false  |

**函数用例**

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UIComboRlt("name1,name2","河北省,黑龙江省","石家庄市,承德市#哈尔滨市,齐齐哈尔市,","test","0",400,0,true)
UIComboRlts("name2","test","0",500,1,true)--请保证变量名与标志项与联动框一致，返回值已通过联动框获取
UIShow()
if name1 == "河北省" and name2 == "石家庄市" then
    toast("河北省石家庄市")
elseif name1 == "河北省" and name2 == "承德市" then
    toast("河北省承德市")
elseif name1 == "黑龙江省" and name2 == "哈尔滨市" then
    toast("黑龙江省哈尔滨市")
elseif name1 == "黑龙江省" and name2 == "齐齐哈尔市" then
    toast("黑龙江省齐齐哈尔市")
end
```

**注意事项**

- 请保证变量名与标志项与联动框一致
- 返回值已通过联动框获取

### 函数：UIImage 图片

**函数名称：图片框**

**函数功能：图片显示**

**函数方法**

UIImage(num,way,align,scale,width,nowrap);

|  参数  |  类型  | 必填 | 说明                                                         |  默认值  |
| :----: | :----: | :--: | :----------------------------------------------------------- | :------: |
|  num   | number |  否  | 控件所在页面页数，不能超过 UINew 的 pagination 参数          |    1     |
|  way   | string |  是  | 图片路径，可以是本地路径或者网络路径                         |    -     |
| align  | string |  否  | 对齐方式，左对齐 left，右对齐 right，居中 center             | "center" |
| scale  | number |  否  | 缩放比例 范围 0 - 1                                          |    1     |
| width  | number |  否  | 控件宽度，默认 -1 为一行， 自定义宽度可写其他数值， Android 设备仅支持整数否则会提示 UI 格式错误； -1 为自适应屏幕，0 为占用整行， 大于等于 1 按照数字设置宽度，不填默认占整行， -1、0、及大于等于1参数仅支持 Android**v3.2.0**、iOSv**3.1.5** 以及以上版本 |    0     |
| nowrap | number |  否  | 指定下一个控件是否换行，当此属性为 1 时， 将指定下一个控件不换行 |    0     |

**函数用例**

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UIImage("http://www.baidu.com/img/bdlogo.png") --创建一个图片框，默认居中对齐，图片不缩放，宽度默认一行，下一控件不换行
--可选参数如果写部分的话，该参数前的所有参数都必须需要填写，否则会报错
UIShow()
```

**注意事项**

- 无返回值，只做图片显示
- 触动精灵 iOS 默认图片资源路径为 /var/mobile/Media/TouchSprite/res，触动精灵安卓默认路径为 sdcard/TouchSprite/res
- 小精灵 iOS 默认图片资源路径为 /var/mobile/Media/ 程序唯一标识 /res，触动精灵安卓默认路径为 sdcard/ 程序唯一标识 /res

### 函数：UILine 分割线

**函数名称：分割线**

**引擎版本：仅支持 Android v3.1.3,iOS v3.0.6 及其以上版本**

**其他版本要求：仅支持 TSLib v1.2.9 及其以上版本**

**函数方法**

UILine(num,align,width,height,color)

|  参数  |  类型  | 必填 | 说明                                                         |    默认值     |
| :----: | :----: | :--: | :----------------------------------------------------------- | :-----------: |
|  num   | number |  否  | 控件所在页面页数， 不能超过 UINew 的 pagination 参数         |       1       |
| align  | string |  否  | 对齐方式，默认左对齐，左对齐 - left， 右对齐 - right，居中 - center |    "left"     |
| width  | number |  否  | 控件宽度，默认全屏， Android 设备仅支持整数否则会提示 UI 格式错误 |   屏幕宽度    |
| height | number |  否  | 控件高度，默认 0.5 像素， Android 设备仅支持整数否则会提示 UI 格式错误 |      0.5      |
| color  | string |  否  | 线条颜色，默认灰色，使用 RGB 十进制数值， 以英文半角逗号分割 | "208,208,208" |

**函数用例**

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
UILabel("分割线1",15,"center","255,0,0",-1,0) 
--引擎版本：仅支持 Android v3.1.3、专业版 iOS v3.0.6 及其以上版本
--版本：仅支持 TSLib  v1.2.9 及其以上版本
UILine("center",600,5,"255,0,0")
UILabel("分割线2",15,"center")
UILine("center",600,5)
UIShow()
```

### 函数：UIWeb 网页

**函数名称：网页**

**函数功能：显示网页**

**引擎版本：仅支持 Android v3.1.3,iOS v3.0.6 及其以上版本**

**其他版本要求：仅支持 TSLib v1.2.9 及其以上版本**

**函数方法**

UIWeb(num,url,width,height)

|  参数  |  类型  | 必填 | 说明                                                | 默认值                                               |
| :----: | :----: | :--: | :-------------------------------------------------- | :--------------------------------------------------- |
|  num   | number |  否  | 控件所在页面页数， 不能超过 UINew 的pagination 参数 | 1                                                    |
|  url   | string |  是  | 浏览器地址                                          | -                                                    |
| width  | number |  否  | 控件宽度                                            | 屏幕宽度                                             |
| height | number |  否  | 控件高度                                            | iOS 不写默认为 144 像素， Android 不写默认为 70 像素 |

**函数用例**

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
UINew()
--引擎版本：仅支持 Android v3.1.3、专业版 iOS v3.0.6 及其以上版本
--版本：仅支持 TSLib  v1.2.9 及其以上版本
UILabel("显示触动官网",15,"center","255,0,0",-1,0) 
UIWeb("http://www.touchsprite.com/",600,600)
UIShow()
```

### 函数：UISwitch 开关

UISwitch(num,id,state,size,align,width,nowrap)

|  参数  |  类型  | 必填 | 说明                                                         | 默认值 |
| :----: | :----: | :--: | :----------------------------------------------------------- | :----: |
|  num   | number |  否  | 控件所在页面页数， 不能超过 UINew 的 pagination 参数         |   1    |
|   id   | string |  是  | 控件指定 ID                                                  |   -    |
| state  | string |  否  | 开关状态，默认关闭，on 打开，off 关闭， disable 禁用，disable-on 打开并禁用 | "off"  |
|  size  | string |  否  | 为控件指定大小，默认中号，s 小号，m 中号，l 大号             |  "m"   |
| align  | string |  否  | 为控件指定对齐方式，默认居左， 居中 center，居左 left，居右 right | "left" |
| width  | number |  否  | 控件宽度， 自定义宽度可写其他数值， Android 设备仅支持整数否则会提示 UI 格式错误； -1 为自适应屏幕，0 为占用整行， 大于等于 1 按照数字设置宽度，不填默认占整行， -1、0、及大于等于1参数仅支持 Android**v3.2.0**、iOSv**3.1.5** 以及以上版本 |   0    |
| nowrap | number |  否  | 指定下一个控件是否换行，当此属性为 1 时， 将指定下一个控件不换行， 仅支持 v1.3.4 及其以上版本 TSLib |   0    |

**函数示例**

```lua
require "TSLib"--使用本函数库必须在脚本开头引用并将文件放到设备 lua 目录下
local m = TSVersions()
if m <= "1.3.1" then
    dialog("请使用 v1.3.2 及其以上版本 TSLib")
    luaExit()
end
--仅支持 v1.3.2 及其以上版本 TSLib
UINew()
UILabel("开关打开",15,"left","255,0,0")
UISwitch("switch1","on","s","right")
UILabel("开关关闭",15,"left","255,0,0")
UISwitch("switch2","off","m","center")
UILabel("开关关闭并禁用",15,"left","255,0,0")
UISwitch("switch3","disable","l","left")
UILabel("开关打开并禁用",15,"left","255,0,0")
UISwitch("switch4","disable-on")
UIShow()
dialog(switch1,2)
dialog(switch2,2)
dialog(switch3,2)
dialog(switch4,2)
```

### UI 完整实例

使用了 table 格式和一般格式两种，可根据自己需要使用哪一种或者两种同时使用，多页 UI 只需在前面写数字页数，不写默认布局到第一页。

```lua
require "TSLib"--使用函数库一定要在最前面调用并将函数库文件发送到手机 lua 目录
w,h = getScreenSize()
UINew(2,"第一页,第二页","开始","取消","uiconfig.dat",0,120,w*0.8,h*0.8,"221,240,237","88,210,232")
UIImage(2,"http://www.baidu.com/img/bdlogo.png")
UILabel({text="单选组合设置："})
UIRadio({id="radio",list="单选1,单选2,单选3,单选4,单选5,单选6"})
UILabel(2,"下拉框设置：")
UICombo({num=2,id="combo",list="下拉框1,下拉框2,下拉框3,下拉框4,下拉框5,下拉框6"})
UILabel("多选组合设置：")
UICheck("check1,check2,check3,check4,check5,check6","多选1,多选2,多选3,多选4,多选5,多选6")
UILabel("联动框设置：")
UIComboRlt("comborle,comborles","选项1,选项2,选项3","子选项1,子选项2,子选项3,子选项4#子选项5,子选项6,子选项7#子选项8,子选项9","test")
UILabel("关联框设置：")
UIComboRlts("comborles","test")
UIShow()
dialog("单选组合选择："..radio.."\n".."下拉框选择："..combo.."\n".."联动框选择："..comborle.."\n".."关联框选择："..comborles, 0)
dialog("多选组合结果:".."\ncheck1="..tostring(check1).."\ncheck2="..tostring(check2).."\ncheck3="..tostring(check3).."\ncheck4="..tostring(check4).."\ncheck5="..tostring(check5).."\ncheck6="..tostring(check6), 0)
```

### showUI

**显示一个自定义的界面，用来接收用户相关的自定义配置**

ret, input_1, input_2, ... = showUI(ui_json)

返回值：ret,input_(*)

|  参数   |  类型  | 说明                                                   |
| :-----: | :----: | :----------------------------------------------------- |
| ui_json | string | 自定义界面 json 格式字符串调用时字符串需经过压缩与转义 |

|  返回值   |  类型  | 说明                       |
| :-------: | :----: | :------------------------- |
|    ret    | number | 1 - 确认输入；0 - 取消输入 |
| input_(*) | string | 返回用户输入的多项数据     |

### 全局属性

|    参数     |  类型  | 必填 |                             说明                             | 默认值        |
| :---------: | :----: | :--: | :----------------------------------------------------------: | ------------- |
|    style    | string |  否  | 指定界面样式 default 为默认样式，所有控件自动排列，每个控件占据一行。 custom 为自定义样式，当界面样式被指定为这种， 则必须指定每个控件的 rect 属性以调整控件的尺寸以及位置。 | "default"     |
|    width    | number |  否  |          界面的宽度（像素 pixels），不得低于 400。           | -             |
|   height    | number |  否  |          界面的高度（像素 pixels），不得低于 120。           | -             |
|     bg      | string |  否  | 指定界面的背景图片， 相对路径为 res 资源目录，可填写绝对路径。 | -             |
|   okname    | string |  否  |         确认文字，指定底部右侧确认按钮上显示的文字。         | “确定”        |
| cancelname  | string |  否  |         取消文字，指定底部左侧取消按钮上显示的文字。         | “取消”        |
|    title    | string |  否  | 标题，用于指定 UI 顶部标题栏文字， 仅 iOS **v2.2.5**, Android **v1.2.4** 以上版本支持 | “脚本配置”    |
| titlealign  | string |  否  | title 对齐方式，默认左对齐。 可取值为：左对齐 left，右对齐 right，居中 center， 仅支持 Android**v3.2.0**、iOSv**3.1.5** 及其以上版本 | “left”        |
|  titlesize  | number |  否  | title 字体大小，仅支持 Android**v3.2.0**、iOSv**3.1.5** 及其以上版本 | 15            |
|   titles    | string |  否  | 多页标题，用于指定 UI 顶部标题栏文字在多页模式下 可以设置多个标题对应多个页面， 以逗号分隔， 仅 iOS v2.3.2, Android v2.2.7 以上版本支持。 | -             |
|  pagetype   | string |  否  | 多页模式，当指定该属性值为 `multi` 时，UI 可分页显示， 左右滑动进行翻页，如不指定该属性，将使用默认的单页模式， 仅 iOS**v2.2.5**, Android**v2.1.5** 以上版本支持。 | -             |
|   selpage   | number |  否  | 多页模式下指定默认停留的页面， iOS 仅支持 **v2.2.7** 及其以上版本， Android 支持所有引擎版本。 | 1             |
|   orient    | number |  否  | 指定 UI 界面显示方向， 0 - Home 键在设备下方， 1 - Home 键在设备右侧， 2 - Home 键在设备左侧， 仅支持 iOS **v2.2.5** 及其以上版本 | 0             |
| btnbkcolor  | string |  否  | 底部按钮背景色，使用 RGB 十进制数值，以英文半角逗号分割， 仅支持 iOS**v2.3.5** 及其以上版本， Android 暂不支持。 | “248,248,248” |
|   bgcolor   | string |  否  | 界面背景色，使用 RGB 十进制数值，以英文半角逗号分割， 仅支持 iOS**v2.3.5** 及其以上版本， Android 暂不支持。 | “248,248,248” |
| pagenumtype | string |  否  | 页码样式，dot - 小圆点， number - 数字， default - 不显示， 仅支持 iOS**v2.3.5** 及其以上版本，Android 暂不支持； tab - 底部不显示页码样式， 在顶部将分页标题显示为二级标签， 仅支持 Android**v3.2.0**、iOSv**3.1.5** 及其以上版本 | “default”     |
|   config    | string |  否  |              配置保存文件名，保存配置到该文件。              | -             |
|    timer    | number |  否  | 自动确认时间，倒计时完成自动开始， 专业版 iOS**v3.0.6**、 Android**v3.2.0** 及其以上版本客户端 此参数最高只能显示 999 秒； Android**v3.2.0**、iOSv**3.1.5** 及以上版本将倒计时图标挪到数字右侧， 数字和图标均为右对齐，文字修改为只有数字不显示单位， 调整位置为右对齐 | -             |
|   rettype   | string |  否  | 指定返回值类型，default - 默认模式，保持旧版格式，可使用此属性兼容旧版 UI； array - 数组模式，将所有控件返回值按添加顺序放入一个 table 中返回； table - table 模式，将所有控件返回值以 key, values 形式的 table 返回， key 为控件 id 属性所指定的值，仅支持 iOS**v2.2.6**, Android**v1.2.7** 及以上版本。 | “default”     |

### 指定控件尺寸与位置

界面的样式 style 为 default 时，即默认样式，这个样式下的控件将会自动排列，不需要指定其坐标。 另一种界面样式为 custom，当界面样式被指定为这种，则必须指定每个控件的 rect 属性以调整控件的尺寸以及位置，例如：

```lua
{
"type": "Edit", "size": 15, "align": "left",
"prompt": "提示文字",
"text": "默认文字",
"color": "255,0,0",
"rect": "0,0,100,40"
}
```

| 参数 |  类型  | 说明                                                         |
| :--: | :----: | :----------------------------------------------------------- |
| rect | string | 尺寸与位置，该属性适用于全部五种控件， 将控件的左上角顶点横坐标、纵坐标， 控件宽度、高度分别以英文半角逗号分割 |

**注意事项**

- 默认配置文件路径：

   触动精灵 iOS 配置文件目录：/var/mobile/Media/TouchSprite/config/

   触动精灵安卓配置文件目录：/mnt/sdcard/TouchSprite/config/

   iOS 小精灵配置文件目录：/var/mobile/Media/小精灵包名/config/

   安卓小精灵配置文件目录：/mnt/sdcard/

- 当在 `iOS 9` 以上版本的 iPad 设备上使用 showUI 界面时，务必使用 **orient** 属性指定正确的屏幕方向，否则将可能出现确定、取消按钮无法点击的情况。

- 如果配置文件已存在，调用该界面会自动载入该文件中的配置，如果更新了 UI 代码，必须要删除旧的配置文件才会正常显示。

- 使用 **timer** 属性必须要设定 **config** 属性，第一次存储配置文件不存在时，此属性不生效，当配置文件存在时，此属性会在生成 UI 上进行倒计时。

- 在脚本 UI 界面点击闹钟标志则取消倒计时功能。

- 在引擎版本 iOS v2.2.6 以上版本中，自定义模式坐标计算方式由原来的分辨率(pt)改为分辨率（px），开发者使用自定义模式时需要做对应修改，新的方式只需将原自定义模式坐标乘以 Render 屏对应的倍数即可。

- 引擎版本 Android v3.1.7、iOS v3.1.1 及其以上版本修改了脚本配置文件的存储方式同时增加了自动还原脚本配置数据的功能。

- 使用 pagenumtype 参数中的 tab 会在顶部将 titles 内容显示为二级标签，title 为空顶部标题显示为脚本配置，有内容将内容显示为顶部标题。

### 实例代码 - 一行显示多个控件

该代码中的部分新参数最低支持`安卓 v3.2.0`, `iOS v3.1.5` 版本。

```lua
local ts = require("ts")
local cjson = ts.json
w,h = getScreenSize();
MyTable = {
    ["style"]  = "default",    
    ["width"] = w,          
    ["height"] = h,            
    ["cancelname"] = "取消",  
    ["okname"] = "开始", 
    ["title"] = "居中自定义字号",
    ["titlealign"] = "center",
    ["align"] = "center",
    ["titlesize"] = 12,  
    ["titles"] = "第一页,标签页,新增属性,左右滑动,切换页面", 
    ["pagetype"]= "multi",  
    ["selpage"] = 1,   
    ["orient"] = 0, 
    ["btnbkcolor"] = "255,255,255",         
    ["bgcolor"] = "255,255,255",
    ["pagenumtype"] = "tab", 
    ["config"] = "showuiTest1.txt",  
    ["timer"] = 99,  
    ["rettype"] = "table",   
    pages            =
    {
        {
            {
                ["type"] = "Label", 
                ["text"] = "上线日期：",        
                ["size"] = 12, 
                ["align"] = "left",          
                ["valign"] = "top", 
                ["color"] = "0,0,0",           
                ["width"] = -1,
                ["nowrap"] = 1,--下个控件不换行
            },
            {
                ["type"] = "Edit",               
                ["id"] = "year",                  
                ["prompt"] = "年",  
                ["text"] = "2014",     
                ["kbtype"] = "number",  
                ["color"] = "0,0,0",   
                ["size"] = 12,           
                ["align"] = "center",           
                ["valign"] = "top",   
                ["width"] = 180,
                ["nowrap"] = 1,--下个控件不换行
            },
            {
                ["type"] = "Label", 
                ["text"] = "年",        
                ["size"] = 12, 
                ["align"] = "left",          
                ["valign"] = "top", 
                ["color"] = "0,0,0",           
                ["width"] = -1,
                ["nowrap"] = 1,--下个控件不换行
            },
            {
                ["type"] = "Edit",               
                ["id"] = "month",                  
                ["prompt"] = "月",  
                ["text"] = "5",     
                ["kbtype"] = "number",  
                ["color"] = "0,0,0",   
                ["size"] = 12,           
                ["align"] = "center",--输入框文字水平对齐方式           
                ["valign"] = "top", --输入框垂直对齐方式  
                ["width"] = 120,
                ["nowrap"] = 1,--下个控件不换行
            },
            {
                ["type"] = "Label",            
                ["text"] = "月",        
                ["size"] = 12,                 
                ["align"] = "left",           
                ["valign"] = "top", 
                ["color"] = "0,0,0",    
                ["width"] = -1,
                ["nowrap"] = 1,--下个控件不换行
            },
            {
                ["type"] = "Edit",               
                ["id"] = "day",                  
                ["prompt"] = "日",  
                ["text"] = "1",     
                ["kbtype"] = "number",  
                ["color"] = "0,0,0",   
                ["size"] = 12,           
                ["align"] = "center",           
                ["valign"] = "top",   
                ["width"] = 120,
                ["nowrap"] = 1,--下个控件不换行
            },
            {
                ["type"] = "Label",        
                ["text"] = "日",        
                ["size"] = 12,                  
                ["align"] = "left",           
                ["valign"] = "top", 
                ["color"] = "0,0,0",           
                ["width"] = -1,
                --["nowrap"] = 1,
            },      
        }
    }   
}
local MyJsonString = cjson.encode(MyTable);
UIret,values = showUI(MyJsonString)
if UIret == 1 then
    local year =  values.year
    local month =  values.month
    local day =  values.day
    dialog("上线日期："..year.." 年 "..month.."  月"..day.." 日")
end
```

**注意事项**

- 默认配置文件路径：

   触动精灵 iOS 配置文件目录：/var/mobile/Media/TouchSprite/config/

   触动精灵安卓配置文件目录：/mnt/sdcard/TouchSprite/config/

```lua
local ts = require("ts")
local cjson = ts.json
w,h = getScreenSize();
MyTable = {
    ["style"]  = "default",            --  选填，默认样式，控件排列类型
    ["rettype"] = "table",              
    --  选填，旧版，showUI 返回值格式
    ["width"] = w,          
    --  选填，安卓默认全屏，iOS 默认，showUI 宽度
    ["height"] = h,             --  选填，安卓默认全屏，iOS 默认，showUI 高度
    ["config"] = "showuiTest1.txt",  --  选填，无，配置文件保存文件
    ["timer"] = 99,                 --  选填，无，自动执行倒计时
    ["orient"] = 0,                 --  选填，竖屏，显示方向(仅支持 iOS)
    ["pagetype"]= "multi",                  
    --  选填，单页，单页/多页 (多页显示时必填，否则无法正确显示 showUI)
    ["title"] = "触动精灵脚本 UI 演示",--  选填，脚本配置，showUI 标题
    ["titles"] = "第一页,第二页,第三页", 
    --  选填，无，多页 showUI 标题(仅在多页下有效)
    ["cancelname"] = "取消",      --  选填，取消，左下角按钮名称
    ["okname"] = "开始",          --  选填，确认，右下角按钮名称
    ["selpage"] = 1,              --  选填，无，多页模式下指定默认停留的页面
    ["btnbkcolor"] = "255,255,255",         
    --  选填，255,255,255，底部按钮背景色(仅支持 iOS)
    ["bgcolor"] = "255,255,255",  --  选填，255,255,255，界面背景色(仅支持 iOS)
    ["pagenumtype"] = "number",  --  选填，无，分页指示样式    
    pages            =
    {
        {
            {
                ["type"] = "Label",
                ["text"] = "点击右上角闹钟关闭倒计时↗",
                ["size"] = 20,
                ["align"] = "center",
                ["color"] = "255,0,0",
            },
            {
                ["type"] = "Label",             -- 必填，控件类型，标签
                ["text"] = "第一页设置",        
                -- 选填，无，显示内容(内容为空,仍然占用一行)
                ["size"] = 25,                  -- 选填，15，字号
                ["align"] = "center",           -- 选填，居左，对齐样式
                ["color"] = "0,0,0",            -- 选填 ，0,0,0，字体颜色
            },
            {
                ["type"] = "Label",
                ["align"] = "center",
                ["text"] = "单选组合-RadioGroup",
                ["size"] = 20,
            },
            {
                ["type"] = "RadioGroup",            
                -- 必填，控件类型，单选组合
                ["id"] = "rg",                      
                -- 选填，无，控件 ID，以 table 格式返回返回值时必填,否则无法获取返回值
                ["list"] = "小学,初中,高中,大学",     -- 必填，无，单选组合内容
                ["select"] = "1",                   -- 选填，0，默认选中项 id
                ["images"] = "showui_test_a.png,showui_test_b.png,showui_test_c.png,showui_test_d.png", 
                -- 选填，无， 单选组合选项显示图片
                ["scale"] = "0.4",                  -- 选填，1，图片缩放比例
            },
            {
                ["type"] = "Label",
                ["align"] = "center",
                ["text"] = "输入框-Edit",
                ["size"] = 20,
            },
            {
                ["type"] = "Edit",               
                -- 必填，控件类型，输入框
                ["id"] = "edit",                  
                -- 选填，无，控件 ID 以table格式返回返回值时必填，否则无法获取返回值
                ["prompt"] = "年",                -- 选填，无，提示文字
                ["text"] = "1989",                -- 选填，无，默认文字
                ["kbtype"] = "number",            -- 选填，标准键盘，键盘类型
                ["color"] = "0,0,0",              -- 选填，黑色，字体颜色
                ["size"] = 15,                    -- 选填，15，字体大小
                ["align"] = "center",             -- 选填，居左，对齐方式
            },
            {
                ["type"] = "Label",
                ["align"] = "center",
                ["text"] = "单级下拉框-ComboBox",
                ["size"] = 20,
            },
            {
                ["type"] = "ComboBox",                             
                -- 必填，控件类型，下拉框
                ["id"] = "cb1",                                     
                -- 选填，无，控件 ID 以 table 格式返回返回值时必填，否则无法获取返回值
                ["list"] = "鼠,牛,虎,兔,龙,蛇,马,羊,猴,鸡,狗,猪",
                -- 必填，无，下拉框内容
                ["select"] = "1",                                   
                -- 选填，0，默认选中项 ID
            },
            {
                ["type"] = "Label",
                ["text"] = "二级下拉框-ComboBox",
                ["size"] = 20,
            },
            {
                ["type"] = "ComboBox",          -- 必填，控件类型，下拉框
                ["id"] = "cb2",                             
                -- 选填，无，控件ID 以 table 格式返回返回值时必填，否则无法获取返回值
                ["list"] = "北京,上海,广州,深圳",-- 必填，无，下拉框内容
                ["select"] = "0",               -- 选填，0，默认选中项 ID
                ["data"] = "北京1,北京2,北京3,北京4#"..
                "上海1,上海2,上海3,上海4#"..
                "广州1,广州2,广州3,广州4#"..
                "深圳1,深圳2,深圳3,深圳4",   --必填，无，下拉框子选项内容
                ["source"] = "这里必须一致"                      
                --  必填，无，主选项下拉框控件 source 属性必须与子选项下拉框的 dataSource 属性一致
            },
            {
                ["type"] = "ComboBox",                      -- 必填，控件类型，下拉框
                ["id"] = "cb3",                             
                -- 选填，无控件 ID，以 table 格式返回返回值时必填，否则无法获取返回值
                ["select"] = "0",                           
                -- 选填，无，子选项下拉框默认选中项
                ["dataSource"] = "这里必须一致"             
                --必填，无，主选项下拉框控件 source 属性必须与子选项下拉框的 dataSource 属性一致
            },
            },{
            {
                ["type"] = "Label",
                ["text"] = "第二页设置",
                ["size"] = 25,
                ["align"] = "center",
                ["color"] = "0,0,0",
            },
            {
                ["type"] = "Label",
                ["align"] = "center",
                ["text"] = "多行文本框-TextArea",
                ["size"] = 20,
            },
            {   -- 必填，控件类型，输入框
                ["type"] =  "TextArea",         
                ["id"] = "ta",                  
                -- 选填，无，控件ID 以 table 格式返回返回值时必填，否则无法获取返回值
                ["text"] = "触动精灵"..
                "官方工作人员都是使用 288 开头的企业 QQ\r\n"..
                "交易需谨慎,谨防上当受骗!",       -- 选填，无，默认文字
                ["prompt"] =  "我是hint",       -- 选填，无，提示文字
                ["size"] =  15,                 -- 选填，15，字体大小
                ["align"] =  "center",          -- 选填，居左，对齐方式
                ["height"] =  250,              -- 选填，75，空间高度(仅支持 iOS)
                ["color"] =  "255,0,0",         -- 选填，黑色，字体颜色
                ["kbtype"] = "number",          -- 选填，标准键盘，键盘类型
            },
            {
                ["type"] = "Label",
                ["align"] = "center",
                ["text"] = "多选组合-CheckBoxGroup",
                ["size"] = 20,
            },
            {   --必填，控件类型，单选组合
                ["type"] = "CheckBoxGroup",     
                -- 选填，无，控件 ID  以 table 格式返回返回值时必填，否则无法获取返回值
                ["id"] = "cbg",                             

                -- 必填，无 ，单选组合内容
                ["list"] = "电影,读书,跑步,吃饭,"..
                "运动,睡觉,旅行,打豆豆,听歌,电影",   
                -- 选填，0，默认选中项 ID
                ["select"] = "3@5@7",           
                -- 选填，无，单选组合选项显示图片
                ["images"] = "showui_test_a.png,showui_test_b.png,"..
                "showui_test_c.png,showui_test_d.png,showui_test_e.png,"..
                "showui_test_f.png,showui_test_g.png,showui_test_h.png,"..
                "showui_test_i.png,showui_test_j.png",
                -- 选填，1，图片缩放比例
                ["scale"] = "0.3",         
            },
            },{
            {
                ["type"] = "Label",
                ["text"] = "第三页设置",
                ["size"] = 25,
                ["align"] = "center",
                ["color"] = "0,0,0",
            },
            {
                ["type"] = "Label",
                ["align"] = "center",
                ["text"] = "图片-Image",
                ["size"] = 20,
            },
            {   -- 必填，控件类型，图片
                ["type"] = "Image",    
                --- 必填，无，图片路径(可填写资源目录下相对路径，绝对路，,网址)
                ["src"] = "http://mrw.so/4wbrDw",   
                -- 选填，无，图片缩放比例
                ["scale"] = 0.4,                     
            },
            {
                ["type"] = "Image",
                ["src"] = "http://mrw.so/4wbrDw",
                -- 选填，无，图片缩放比例
                ["scale"] = 0.6,                     
                -- 选填，默认居左，对齐方式
                ["align"] = "left"                   
            },
            {
                ["type"] = "Image",
                ["src"] = "http://mrw.so/4wbrDw",
                -- 选填，无，图片缩放比例
                ["scale"] = 0.8,       
                -- 选填，默认居左，对齐方式
                ["align"] = "center"                
            },
            {
                ["type"] = "Image",
                ["src"] = "http://mrw.so/4wbrDw",
                -- 选填，无，图片缩放比例
                ["scale"] = 1,      
                -- 选填，默认居左，对齐方式
                ["align"] = "right"               
            },
        }
    }   
}
local MyJsonString = cjson.encode(MyTable);
UIret,values = showUI(MyJsonString)
if UIret == 1 then
    local rg =  values.rg
    local edit =  values.edit
    local cb1 =  values.cb1
    local cb2 =  values.cb2
    local cb3 =  values.cb3
    local ta =  values.ta
    local cbg =  values.cbg
    dialog("单选组合:"..rg..",\r\n单行输入框:"..edit..",\r\n一级下拉框:"..cb1..",\r\n二级下拉框主选项:"..cb2..",\r\n二级下拉框子选项:"..cb3..",\r\n多行文本框:"..ta..",\r\n多选组合:"..cbg..",")
end
```

### WebUI示例

```lua
local html = [[
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Hello 触动精灵 ShowUI</title>
    <meta name="viewport" content="width=device-width, initial-scale=1,maximum-scale=1,user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black">
    <!--标准mui.css-->
    <link rel="stylesheet" href="css/tsShowUI.css">
        <link rel="stylesheet" href="css/icons-extra.css">
    <!--App自定义的css-->

</head>
<body>
    <header class="mui-bar mui-bar-nav">
        <button id="ts-cancle" class="mui-action-back mui-btn mui-btn-blue mui-btn-link mui-btn-nav mui-pull-left"><span class="mui-icon mui-icon-left-nav"></span><span class=" mui-tscancel">返回</span></button>
        <button id="ts-timer" class="mui-action-back mui-btn mui-btn-blue mui-btn-link mui-btn-nav mui-pull-right"></button>
        <h1 class="mui-title mui-tstitle"></h1>
    </header>
    <footer class="mui-bar mui-bar-footer mui-bar-tsfooter">
        <button id="ts-post-btn" class="mui-ts-footerbth btn mui-btn-block mui-btn-blue mui-tsaction" data-loading-text="执行中" type="button">开始</button>
    </footer>
    <div class="mui-content">
        <form class="mui-tsform">
            <div class="mui-card" id="renderbox">
            </div>
        </form>
    </div>
    <script src="js/tsShowUI.js"></script>
    <script>
    (function($, doc) {
        var uiVersion=$.getVersion();//获取ui版本
        //json兼容原showui 格式
        var showui_json = {//通过$.renderUI方法来添加组件（页面只需添加一次）
            "title": "触动精灵脚本配置", 
            "cancelname": "取消", 
            "config": "8888.txt",
            "okname": "开始",
            "titles" : "项目名称1,项目名称2,项目名称3,项目名称4,项目名称5,项目名称6", 
            "pagenumtype" : "tab",
            "style": "default",
            "align":'center',
            "titlesize":15,
            "timer": 30,
            "orient": 0,
            "pagetype": "multi",
            "pages": [
            [
                {   "type":"Label",
                    "size":20,
                    "align":"center",
                    "color":"100,255,100",
                    "width":20,
                    "text":"分割线"
                },
                {
                    "type":"Line",
                    "align":"center",
                    "color":"0,0,0",
                    "width":600,
                    "height":"5"
                },        
                {   "type":"Label",
                    "size":20,
                    "align":"center",
                    "color":"100,255,100",
                    "text":"滑块"
                },
                {   "type":"Slide",
                     "id":"huakuai",
                    "default":"20",
                    "min":"5",
                    "max":"50",
                    "span":"2"
                },
                {   
                    "type":"Label",
                    "size":20,
                    "align":"center",
                    "color":"100,255,100",
                    "text":"单选组合"
                },
                {  
                    "type":"RadioGroup",
                    "id":"danxuan",
                    "select":"2",
                    "list":"单选1,单选2,单选3,单选4"
                },
                {   
                    "type":"Label",
                    "size":20,
                    "align":"center",
                    "color":"100,255,100",
                    "text":"多选组合"
                },
                {
                    "type":"CheckBoxGroup",
                    "id":"duoxuan",
                    "select":"1@3@5",
                    "list":"电影,读书,跑步,吃饭,运动,睡觉,旅行,打豆豆,听歌"  
                },
                {
                    "type":"Label",
                    "size":20,
                    "align":"left",
                    "color":"100,255,100",
                    "text":"数字单行文本框"
                },
                {  
                    "type": "Edit",
                    "id": "shuzi",
                    "prompt": "请输入一个数字",
                    "text": "1234",
                    "kbtype": "number",
                    "secure": true
                },
                {
                    "type":"Label",
                    "size":20,
                    "align":"left",
                    "color":"100,255,100",
                    "text":"普通单行文本框"
                },
                {
                    "type": "Edit",
                    "id": "putong",
                    "prompt": "请输入一个字母",
                    "text": "默认值",
                    "row": "5",
                    "kbtype": "ascii"
               },
               {
                    "type":"Label",
                    "size":20,
                    "align":"left",
                    "color":"100,255,100",
                    "text":"密码单行文本框"
                },
                {   "type": "Edit",
                    "id": "mima",
                    "prompt": "请输入密码",
                    "text": "hhkjkjh",
                    "kbtype": "password"
                },
                {
                    "type":"Label",
                    "size":20,
                    "align":"left",
                    "color":"100,255,100",
                    "text":"多行文本框"
                },   
                {
                    "type":"TextArea",
                    "id":"duohang",
                    "size":15,
                    "height":250,
                    "color":"255,0,0",
                    "prompt":"我是hint",
                    "align":"center",
                    "kbtype":"number",
                    "text":"1\r\n2\n3"
                },
                {
                    "type":"Label",
                    "size":20,
                    "align":"left",
                    "color":"100,255,100",
                    "text":"下拉框"
                },
                {
                    "type":"ComboBox",
                    "id":"xiala1",
                    "select":"0",
                    "list":"北京,上海"
                },
                {
                    "type":"Label",
                    "size":20,
                    "align":"left",
                    "color":"100,255,100",
                    "text":"联动下拉框"
                },
                {
                    "type":"ComboBox",
                    "id":"xiala2",
                    "select":"1#1",
                    "list":"北京,上海",
                    "data":"北京1,北京2#上海1,上海2"
                },
                {
                    "type":"Label",
                    "size":20,
                    "align":"left",
                    "color":"100,255,100",
                    "text":"开关"
                },
                {
                    "type":"Switch",
                    "id":"kaiguan1",
                    "size":"s",
                    "align":"center",
                    "state":"on"
                },
                {
                    "type":"Switch",
                    "id":"kaiguan2",
                    "size":"s",
                    "align":"right",
                    "state":"off"
                },
                ],[
                {
                    "type":"Label",
                    "size":20,
                    "align":"center",
                    "color":"100,255,100",
                    "text":"图片"
                },
                {
                    "type":"Image",
                    "src":"http:\/\/www.baidu.com\/img\/bdlogo.png",
                    "scale":1
                },
                {
                    "type":"Label",
                    "size":20,
                    "align":"center",
                    "color":"100,255,100",
                    "text":"网页"
                },
                {
                    "type":"Web",
                    "height":500,
                    "url":"https://www.touchsprite.com"
                },
                ],[
                {
                    "type":"Label",
                    "size":20,
                    "align":"center",
                    "color":"100,255,100",
                    "text":"开关"
                },
                {
                    "type":"switches",
                    "id":"kaiguan3",
                    "list":"开关1,开关2,开关3,开关4",
                    "select": "0@2"
                }
            ]
            ]
        };
        $.renderUI(showui_json);
    })(mui, document)
    </script>
</body>
</html>
]]
local thread = require('thread')
local event = require('event')
local ts = require('ts')
local cjson = ts.json
--创建webview
local showui_view,err = require('webview').new("myshowui",
    {html=html})
assert(showui_view,err)
event.register("showUI_commit",function(value)
        showui_view.close()
        dialog(cjson.encode(value))
    end)
event.register("showUI_cancel",function(value)
        showui_view.close()
    end)
showui_view.show()
thread.waitAllThreadExit()
```

