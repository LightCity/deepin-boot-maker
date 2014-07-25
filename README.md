
**The backend is fork from unetbootin just now. however, it will rewrite sooner or later, maybe.**

Deepin Boot Maker is help for user to create a boot usb stick quick and easy, it designed to support only deepin install iso, but it can can work for all ubuntu live install iso too.

深度启动器制作工具是用来帮助用户简单便捷的制作启动U盘的工具. 设计上只支持深度系统安装镜像,但实际上Ubuntu Live系列的镜像都是可以支持的.

![duc](https://cloud.githubusercontent.com/assets/1117694/3170269/8cfbd364-ebb4-11e3-811e-39da9026f4c7.png)

系统支持:
====

**Windows平台：**

Windows XP/Windows 7/ Windows 8

**Linux平台：**

Ubuntu12.04/Ubuntu14.04/Deepin 14.04

安装以下软件包
```
sudo apt-get install p7zip mtools 
```

**Mac：**

app打包文件不支持Mac OS 10.10, 但是可以使用命令行直接运行MacOS目录下的二进制文件.

开发指南
================
开发环境：Qt5.3
请注意以下事项：
1. 现有阶段代码主要为静态编译准备，qt5.3中的qtquick qml文件是直接打包在qrc文件中发布的，使用其他版本的qt可能导致兼容性问题。
2. 如需要动态编译版本，请注意修改代码相应位置，以后会做出相应支持。

**Windows平台：**

开发环境：
Windows 7 64bit + msvc2010 + WinSDK 8.1+Qt5.3

1.静态编译参数：
```
set DXSDK_DIR="C:\Program Files (x86)\Windows Kits\8.0\Include\um"
configure -prefix "C:\Qt\QtStatic\5.3\vs2010" -release -platform win32-msvc2010 \
-no-qml-debug -confirm-license -opensource -static -qt-pcre -no-icu -no-sql-sqlite \
-no-nis -no-cups -no-iconv -no-dbus -nomake examples -no-sql-odbc -no-compile-examples \
-skip qtwebkit -skip qtwebkit-examples -skip qtactiveqt -no-openssl -qt-zlib \
-qt-libpng -qt-freetype -qt-libjpeg
```

注意：
1.不要编译icu，不然发布时会附带30M左右的icu支持的dll


**Mac平台:**

Macx 10.9 + Qt5.3

1.设置Qt路径
```
export QtInstallPath=/User/yourhome/Qt5.3/5.3/clang_64
export PATH=$QtInstallPath/bin:$PATH
```
2.编译
```
cd src
qmake -r deepin-boot-maker.pro
make
macdeployqt ../build/release/deepin-boot-maker.app
```
3.附加qml运行库
```
cp $QtInstallPath/qml/QtQuick/Dialogs/libdialogplugin.dylib ../build/release/deepin-boot-maker.app/Contents/MacOS/
cp $QtInstallPath/qml/QtQuick/Controls/libqtquickcontrolsplugin.dylib  ../build/release/deepin-boot-maker.app/Contents/MacOS/
cp $QtInstallPath/qml/QtQuick/Window.2/libwindowplugin.dylib ../build/release/deepin-boot-maker.app/Contents/MacOS/
cp $QtInstallPath/qml/QtQuick.2/libqtquick2plugin.dylib ../build/release/deepin-boot-maker.app/Contents/MacOS/
cp $QtInstallPath/qml/Qt/labs/folderlistmodel/libqmlfolderlistmodelp
```

**Linux平台**
```
cd src
qmake
make
sudo ../build/release/deepin-boot-maker
```
