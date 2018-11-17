# Introduction
XToolBox is Qt 4.8.5 based application framework, use the lua script to build the UI elements, 
can be used to make proto type of the application.

XToolBox是一个基于Qt 4.8.5开发的应用程序框架，使用lua脚本进行界面元素开发。可以用于应用程序的快速原型开发。

Source code is available [here][xtoolbox_source]. 源代码在[这里][xtoolbox_source]。

Pre Build Binary is [here][xtoolbox_donwload]. 编译好的可执行程序在这里[xtoolbox_donwload]。 

# Qt feature in lua
## signal/slot
In Qt, we connect the signal and slot use this way
```C++
connect(btn1, SIGNAL(clicked()), this, SLOT(btn1_clicked()));
```
In XToolBox, we do it in this way
```lua
btn1.clicked = function()
   -- button clicked action
end
connect
```

## layout
In Qt, we can setup the UI element by code or the UI designer. If we use code setup the layout, it looks like below
```C++
 frame->addWidget(btn1, ...);
 frame->addWidget(btn2, ...);
```
In XToolbox, we can use this complex way
```lua
 frame:addWidget(btn1, ...);
 frame:addWidget(btn2, ...);
```
But there is also a brand new way to setup the layout
```lua
   frame.layout = QVBoxLayout{
       btn1,
       btn2,
       text1,
       strech = "0,0,1"
   }
```
## Example
copy follow code in "script.lua", and put it into the same directory of [XToolBox.exe][exe_path], then run [XToolBox.exe][exe_path], you will get a lua edit box and a [run] button. 

Click the run button, the log window will show the result " test(10,20) = 30"

复制下面的代码到一个名为script.lua文件中，并把script.lua放在[XToolBox.exe][exe_path]的相同目录下，然后运行[XToolBox.exe][exe_path]，可以看到一个lua编辑框和一个按键。点击按键可以看到日志框中的运行结果，" test(10,20) = 30"。
```lua
class "SampleFrame"(QFrame)
function SampleFrame:__init()
   QFrame.__init(self)
   self.btnRun = QPushButton("Run")
   self.luaEdit = QLuaEdit()
   self.luaEdit.plainText = [[
function test(a ,b)
  return a+b
end
logEdit:append(" test(10,20) = " .. test(10,20))
]]
   
   self.layout = QHBoxLayout{
     self.luaEdit,
     self.btnRun
   }
   
   self.btnRun.clicked = function()
      loadstring(self.luaEdit.plainText)()
   end
end

mdiArea:addSubWindow(SampleFrame()):show()
```
上面代码运行效果如下：

![Alt text](/image/sample.png)

[exe_path]: https://github.com/xtoolbox/Introduction/releases

[xtoolbox_source]: https://github.com/xtoolbox/qtlua

[xtoolbox_donwload]: https://github.com/xtoolbox/Introduction/releases
