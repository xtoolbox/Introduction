# Introduction
XToolBox is Qt 4.8.5 based application framework, use the lua script to build the UI elements, 
can be used to make proto type of the application.

XToolBox是一个基于Qt 4.8.5开发的应用程序框架，使用lua脚本进行界面元素开发。可以用于应用程序的快速原型开发。

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
