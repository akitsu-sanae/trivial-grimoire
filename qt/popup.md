## ポップアップウィンドウをだす
出そうとして色々四苦八苦したのでここにまとめる

### ポップアップウィンドウを出すだけ
ただ単にポップアップウィンドウを出すには, QWidgetを継承したクラスのコンストラクタで  
```cpp
    setWindowFlags(Qt::Window | Qt::FramelessWindowHint);
```
とすればいい

## ぷらすあるふぁ
上だけだとポップアップウィンドウをドラッグしても当然移動してくれないので
```cpp
void SomeOreOreWidget::mousePressEvent(QMouseEvent* e) {
    m_pos = e->pos();
}

void SomeOreOreWidget::mouseMoveEvent(Qmouseevent* e) {
    if (!(e->buttons() && Qt::LeftButton))
        return;
    QPoint newPos = pos() + e->pos() - m_pos;
    move(newpos);
}
```
などとするといい



