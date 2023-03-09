# Qt5-SignalsSlots
Repositorie created to help during the course 'Qt 5 C++ GUI Development For Beginners : The Fundamentals'.

We created a new project according to the [Qt5 C First Code](https://github.com/Rafaelatff/Qt5-C-First-Code).

## String notation

Let's start by adding a 'slider'. Open the 'Forms' -> 'widget.ui' and add an horizontal slider.

![image](https://user-images.githubusercontent.com/58916022/224121036-001c1547-caa5-4f4b-ab8c-ef80d03e20f6.png)

The 'objectName' of the slider is 'horizontalSlider'. We will change its range on 'QAbstractSlider', 'minimum' value will be 1 and 'maximum' will be 100.

Then let's add a progress bar.

![image](https://user-images.githubusercontent.com/58916022/224121218-3548c7b4-83e3-4713-bb82-72f6e2b1b5de.png)

The 'objectName' of the progress bar is 'progressBar'. We also need to set the values of 'minimum' to 1 and 'maximum' to 100 on 'QProgressBar' settings. We will also, on 'QProgressBar', set the 'value' to 1.

We will connect the progress bar value according to the value on the slider. For that, we will edit the 'widget.cpp' source file. It started that way:

```c++
#include "widget.h"
#include "ui_widget.h"

Widget::Widget(QWidget *parent)
    : QWidget(parent)
    , ui(new Ui::Widget)
{
    ui->setupUi(this);   
}

Widget::~Widget()
{
    delete ui;
}
```

Abd we added, just after the line 'ui->setupUi(this);', the following code:

```c++
    // String notation
    connect(ui->horizontalSlider,SIGNAL(valueChanged(int)),
            ui->progressBar,SLOT(setValue(int)));
```

Testing the code:

![Widget 2023-03-09 16-47-56](https://user-images.githubusercontent.com/58916022/224138168-b987da49-2fed-4286-a82d-1f7902f5d504.gif)

## Functor notation : Normal Slots

Now let's delete or comment the string notation and change for the following:

```c++
    // Functor notation : Normal Slots
    connect(ui->horizontalSlider,&QSlider::valueChanged,
            ui->progressBar,&QProgressBar::setValue);
```

Results will be the same. 

## Functor notation: Lambdas

Results will be the same, but code will look like:

```c++
    connect(ui->horizontalSlider,&QSlider::valueChanged,
            [=]() {
        ui->progressBar->setValue(ui->horizontalSlider->value());
```
