# QLayoutItemでQWidgetを扱う注意点

```cpp
QLayout layout;
layout.addWidget(new QCheckBox());
dynamic_cast<QWidget*>(layout.itemAt(0)) // nullptr
```
となるので `layout.itemAt`の返り値の`QLayoutItem` を`dynamic_cast` しても駄目  

こうする

```cpp
QLayout layout;
layout.addWidget(new QWidget());
auto widget_item = dynamic_cast<QWidgetItem*>(layout.itemat(0));
auto check_box = dynamic_cast<QCheckBox*>(widget_item->widget());
```
つまり、`QLayoutItem` を `QWidgetItem` に `dynamic_cast` して`QWidgetItem::widge` から `QWidget*` を取得し、それを目的の型にキャストする

