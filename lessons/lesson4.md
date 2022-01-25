# Lesson 4

## 加速度感應器

加速度感應器是用於檢測**速度的改變**。我們可以透過**搖晃**或**傾斜**加速度感應器讀取加速度數據。

### 加速度與地心引力
當Studuino:bit 在平面上保持不動，加速度感應器仍然會在Z方向軸量度到一些加速度。這實際上是由於地球引致的拉力，你的加速度感應器並沒有設計到能區分地心吸力以及其他類型的加速。所以，Studuino:bit 內置的加速度感應器**無法測出重力加速度**。

### 搖晃的加速度

如圖示所示。

![Accelerator](../public/3-2_4_e.png)

### 傾斜的加速度
- 如果 X 軸的值小於-5 ➡ Studuino:bit 向左傾
- 如果 X 軸的值大於5 ➡ Studuino:bit 向右傾
- 如果 Y 軸的值小於-5 ➡ Studuino:bit 向外傾
- 如果 Y 軸的值大於5 ➡ Studuino:bit 向內傾

### 製作數碼水平儀
```python
from pystubit.sensor import StuduinoBitAccelerometer
from pystubit.board import display
import time

ac = StuduinoBitAccelerometer()
while True:
    values = ac.get_values()
    x = values[0]

    if x < -5:
        display.set_pixel(0, 2, (15, 0, 0))
    elif x > 5:
        display.set_pixel(4, 2, (15, 0, 0))
    else:
        display.set_pixel(2, 2, (15, 0, 0))

    time.sleep_ms(100)
    display.clear()
```

## 陀螺儀

陀螺儀是用於測量物件**轉動速度**的感應器。角速度的量度單位為**角度每秒**。我們只能透過**旋轉**陀螺儀讀取旋轉軸及方向。

### 使用陀螺儀

如圖示所示。

![Gyro](../public/3-2_21_e.png)

### 製作電子螢光棒

```python
from pystubit.sensor import StuduinoBitGyro
from pystubit.board import display, Image
import time

gyro = StuduinoBitGyro()
image = Image('11111:11111:11111:11111:11111:') 
while True:
    values = gyro.get_values()
    z = values[2]
    if z < -200:
        display.show(image, delay=100, color=(0, 0, 31))
    elif z > 200:
        display.show(image, delay=100, color=(0, 31, 0))
    else:
        display.show(image, delay=100, color=(31, 31, 31))

    time.sleep_ms(100)
```
