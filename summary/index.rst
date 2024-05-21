总览
=====
.. seealso:: https://github.com/OpenIoTHub
本软件功能
---------
本软件提供以下功能:
 * 智能家居设备远程控制
 * 私有云
 * 内网穿透

本系统的架构图
----------
 .. image:: ../statics/images/OpenIoTHub-architecture.png

本系统的组成
----------
 * `网关 <https://github.com/OpenIoTHub/gateway-go>`_:作为家庭和内网中心，所有服务通过网关进行跨网访问
 * `转发服务器 <https://github.com/OpenIoTHub/server-go>`_:作为访问客户端到内网设备、服务的桥梁，作为中间人的角色
 * `访问客户端 <https://github.com/OpenIoTHub/OpenIoTHub>`_:用户访问设备、服务的总入口，通过该软件访问所有的设备和服务
 * APP服务器:保存用户数据和配置
 * 受访的设备、服务:用户自己的设备、服务、私有云
本系统的使用
----------
 * 内网穿透、私有云：打开云亿连->添加网关->添加主机->添加端口
 * 智能家居：打开云亿连->添加网关->添加智能设备->控制设备