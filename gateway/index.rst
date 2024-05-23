网关
======
总览
---------
.. seealso:: https://github.com/OpenIoTHub/gateway-go

本节将介绍如何搭建一个网关

编译
---------
Build exe file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

    # Download golang then
    go build main.go

Build dynamic/static Library
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

    #build and push mobile lib
    #install gomobile(at system cli)
    go install golang.org/x/mobile/cmd/gobind@latest
    go install golang.org/x/mobile/cmd/gomobile@latest
    gomobile init
    gomobile version
    go get -u golang.org/x/mobile/...
    #then build
    export GO111MODULE="off"
    gomobile bind -target=android  -o gateway.aar
    gomobile bind -ldflags '-w -s -extldflags "-lresolve"' --target=ios,macos,iossimulator -o OpenIoTHubGateway.xcframework ./client
    #
    #https://gitee.com/OpenIoThub/mobile-lib-podspec
    #git tag -a 0.0.1 -m '0.0.1'
    #git pus --tags
    #pod trunk push ./OpenIoTHubGateway.podspec --skip-import-validation --allow-warnings
    #
    mvn gpg:sign-and-deploy-file -DrepositoryId=ossrh -Dfile=gateway.aar -DpomFile=gateway.pom -Durl=https://s01.oss.sonatype.org/service/local/staging/deploy/maven2/
    mvn deploy:deploy-file -Dfile=client.aar -DgroupId=cloud.iothub -DartifactId=gateway -Dversion=0.0.1 -Dpackaging=aar -DrepositoryId=github -Durl=https://maven.pkg.github.com/OpenIoTHub/gateway-go

::

    #for build windows dll
    echo "building windows dll"
    #brew install mingw-w64
    #sudo apt-get install binutils-mingw-w64
    # shellcheck disable=SC2034
    export CGO_ENABLED=1
    export CC=x86_64-w64-mingw32-gcc
    export CXX=x86_64-w64-mingw32-g++
    export GOOS=windows GOARCH=amd64
    go build -tags windows -ldflags=-w -trimpath -o ./build/windows/gateway_amd64.dll -buildmode=c-shared main.go

::

    #for build linux/android so file
    echo "building linux/android so file"
    #linux和Android共用动态链接库
    export CGO_ENABLED=1
    export GOARCH=amd64
    export GOOS=linux
    go build -tags linux -ldflags=-w -trimpath -o build/linux/libgateway_amd64.so -buildmode c-shared main.go
    # shellcheck disable=SC2034
    export CGO_ENABLED=1
    export GOARCH=arm64
    export GOOS=linux
    #sudo apt install gcc-aarch64-linux-gnu
    export CC=aarch64-linux-gnu-gcc
    ##sudo apt install g++-aarch64-linux-gnu
    #export CXX=aarch64-linux-gnu-g++
    ##sudo apt-get install binutils-aarch64-linux-gnu
    #export AR=aarch64-linux-gnu-ar
    go build -tags linux -ldflags=-w -trimpath -o build/linux/libgateway_arm64.so -buildmode c-shared main.go

安装
---------
Windows
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Windows app store搜索"openiothub"使用云亿连内置网关(推荐)或者从 `网关releases页 <https://github.com/OpenIoTHub/gateway-go/releases>`_ 下载终端版网关

Linux
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Ubuntu
"""""""""""""""""
Ubuntu App store 搜索"openiothub"使用内置网关（推荐）或者搜索"gateway-go"使用命令行网关，snapcraft:
 .. image:: ../statics/images/snap-store-white.png
  :target: https://snapcraft.io/gateway-go

或者 `网关releases页 <https://github.com/OpenIoTHub/gateway-go/releases>`_ 下载二进制程序

openwrt/entware/optware
""""""""""""""""""""""""""""""""""
use snapshot branch：https://downloads.openwrt.org/snapshots/
::

    opkg update
    opkg install gateway-go

Debian or CentOS
"""""""""""""""""
Download the `.deb` or `.rpm` from the `releases page <https://github.com/OpenIoTHub/gateway-go/releases>`_  and
install with `dpkg -i` and `rpm -i` respectively.  

macOS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Homebrew
"""""""""""""""""
::

    $ brew install gateway-go

homebrew pr `gateway-go <https://github.com/Homebrew/homebrew-core/blob/master/Formula/gateway-go.rb>`_

Android
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
安卓版云亿连内置云亿连网关，你可以打开云亿连网关以供另外一个云亿连添加

iOS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
iOS版云亿连内置云亿连网关，你可以打开云亿连网关以供另外一个云亿连添加

Docker
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
You can also use it within a Docker container. To do that, you'll need to
execute something more-or-less like the following:

::

$ docker run -it --net=host openiothub/gateway-go:latest -t <your Token>

Note that the image will almost always have the last stable Go version.

manually
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Download the pre-compiled binaries from the `releases page <https://github.com/OpenIoTHub/gateway-go/releases>`_ and
copy to the desired location.

配置
---------
默认情况下网关运行即会连接服务器，使用云亿连APP即可扫码添加(旧版的网关只有添加的时候才会连接服务器)
