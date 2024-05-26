服务器
======
总览
---------
.. seealso:: https://github.com/OpenIoTHub/server-go

编译(可选)
---------
* 1.安装golang
* 2.执行:

::

    go build main.go

安装
---------
下载二进制运行
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. seealso:: https://github.com/OpenIoTHub/server-go/releases
Linux
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
使用snap安装:
::

          sudo snap install server-go

配置
使用默认生成的配置文件`server-go.yaml`再更改秘钥：

.. code-block::

    server_uuid: 你的UUID-随机生成就行
    my_public_ip_or_domian: ""
    logconfig:
        enablestdout: true
        logfilepath: ./mylog.log
    common:
        bind_addr: 0.0.0.0
        tcp_port: 34320
        kcp_port: 34320
        udp_p2p_port: 34321
        kcp_p2p_port: 34322
        tls_port: 34321
        grpc_port: 34322
        http_port: 80
        https_port: 443
    security:
        login_key: 你的秘钥建议修改
        tls_Cert_file_path: ""
        tls_key_file_path: ""
        https_cert_file_path: ""
        https_key_file_path: ""
    redisconfig:
        enabled: false
        network: tcp
        address: 127.0.0.1:6379
        database: 0
        needAuth: false
        password: ""

---------
