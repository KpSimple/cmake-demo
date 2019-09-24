CMake-Demo
=====

[CMake 入门实战](http://hahack.com/codes/cmake) 的源代码。

### cmake 采用toolchain.cmake 文件进行arm-linux跨平台编译  
cmake -DCMAKE_TOOLCHAIN_FILE=../toolchain/Toolchain-arm-linux-gnueabihf.cmake ..  

### 生成对应平台toolchain
编译android库我们同样可以引入一个toolchain文件，这里我是从android-cmake里面下载的。 在使用这个toolchain文件之前，我们先要使用ndk自带的make-standalone-toolchain.sh脚本来生成对应平台的toolchain.这个脚本位于你的NDK的路径下面的buil/tools目录下。  

比如要生成arm平台的toolchain，我们可以使用下列命令:  
`  
sh $ANDROID_NDK/build/tools/make-standalone-toolchain.sh --platform=android-$ANDROID_API_LEVEL --install-dir=./android-toolchain --system=darwin-x86_64 --ndk-dir=/Users/guanghui/AndroidDev/android-ndk-r9d/ --toolchain=arm-linux-androideabi-4.8
`  
这里的$ANDROID_NDK为你的NDK的安装路径。这段命令可以生成arm的toolchain，最终可以编译出armeabi和armeabi-v7a静态库。 如果想生成x86的toolchain，指需要使用下列命令:  
`
sh $ANDROID_NDK/build/tools/make-standalone-toolchain.sh --platform=android-$ANDROID_API_LEVEL --install-dir=./android-toolchain-x86 --system=darwin-x86_64 --ndk-dir=/Users/guanghui/AndroidDev/android-ndk-r9d/ --toolchain=x86-4.8
`  
`
export PATH=$PATH:./android-toolchain/bin
`  
`  
export ANDROID_STANDALONE_TOOLCHAIN=./android-toolchain  
`  
`  
cmake -DCMAKE_TOOLCHAIN_FILE=../android.toolchain.cmake -DANDROID_ABI="armeabi" ..  
`  
