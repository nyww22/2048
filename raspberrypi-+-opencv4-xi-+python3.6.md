# RaspberryPi + OpenCV4系+Python3.6

通常のインストールではインストールできない

{% embed url="https://qiita.com/ysdyt/items/3c29271a8b8ef38b9893" %}



{% hint style="info" %}
buildフォルダは削除してmakeを実行しないといけない。
{% endhint %}

```text
(base) pi@raspberrypi:~ $ cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/home/pi/out -D OPENCV_EXTRA_MODULES_PATH=/home/pi/opencv4/opencv_contrib/modules -D PYTHON3_EXECUTABLE=/home/pi/berryconda3/bin/python -D PYTHON3_INCLUDE_DIR=/home/pi/berryconda3/include/python3.6m -D PYTHON3_LIBRARY=/home/pi/berryconda3/lib/libpython3.6m.so -D PYTHON3_NUMPY_INCLUDE_DIRS=/usr/lib/python3/dist-packages/numpy/core/include -S /home/pi/opencv4/opencv
(base) pi@raspberrypi:~ $ make -j9





```

