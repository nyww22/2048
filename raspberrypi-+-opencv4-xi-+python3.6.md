# RaspberryPi + OpenCV4系+Python3.6

通常のインストールではインストールできない

{% embed url="https://qiita.com/ysdyt/items/3c29271a8b8ef38b9893" %}



{% hint style="info" %}
buildフォルダは削除してmakeを実行しないといけない。
{% endhint %}

```text
(base) pi@raspberrypi:~ $ sudo apt-get install git
(base) pi@raspberrypi:~ $ git clone https://github.com/opencv/opencv.git
(base) pi@raspberrypi:~ $ acmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/home/pi/out -D OPENCV_EXTRA_MODULES_PATH=/home/pi/opencv4/opencv_contrib/modules -D PYTHON3_EXECUTABLE=/home/pi/berryconda3/bin/python -D PYTHON3_INCLUDE_DIR=/home/pi/berryconda3/include/python3.6m -D PYTHON3_LIBRARY=/home/pi/berryconda3/lib/libpython3.6m.so -D PYTHON3_NUMPY_INCLUDE_DIRS=/usr/lib/python3/dist-packages/numpy/core/include -S /home/pi/opencv4/opencv
(base) pi@raspberrypi:~ $ make -j9





```



### PiCameraで画像認識

{% embed url="https://qiita.com/KMiura95/items/41a24d7639cffc629227" %}

{% embed url="https://qiita.com/FukuharaYohei/items/ec6dce7cc5ea21a51a82" %}





### JupyterNoteBookにカーネル環境を追加（Conda環境の追加）

{% embed url="https://qiita.com/smiler5617/items/e0d9b3034d79457cc253" %}



