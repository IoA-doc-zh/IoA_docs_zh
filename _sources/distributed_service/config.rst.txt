.. Running IoA on Different Devices
.. --------------------------------
.. This guide explains how to configure the IoA framework to run on distributed devices.

.. 🗄️ Server
.. +++++++++++++++++++++++
.. 1. Open TCP & UDP ports
..    Open two ports for network access. By default, you should open port 7788 for the server (denoted as <SERVER_PORT>), and 80 for the webpage frontend (denoted as <FRONTEND_PORT>), but in case where these ports are occupied on your server, you can open other ports.

.. 2. Pull or build necessary docker images:

.. .. code-block:: bash

..    # Server
..    docker pull weize/ioa-server:latest

..    # Server Frontend
..    docker pull weize/ioa-server-frontend:latest

..    # Rename the images
..    docker tag weize/ioa-server:latest ioa-server:latest
..    docker tag weize/ioa-server-frontend:latest ioa-server-frontend:latest

.. 3. Launch Milvus service:

.. .. code-block:: bash

..    docker-compose -f dockerfiles/compose/milvus.yaml up

.. 4. Launch IoA's server:

.. .. code-block:: bash

..    docker-compose -f dockerfiles/compose/server_only.yaml up

.. .. note:: If port `7788` or `80` has already been occupied on your server, revise the port mapping in the yaml file. For example:

..    .. code-block:: yaml

..       Server:
..          ...
..          ports:
..             - <SERVER_PORT>:7788 # Fill <SERVER_PORT> with an opened port on your server
      
..       ...
..       ServerFrontend:
..          ...
..          ports:
..             - <FRONTEND_PORT>:80  # Fill <FRONTEND_PORT> with an opened port on your server

.. You can then access `<SERVER_IP>:<FRONTEND_PORT>` for the server's frontend showing the agents' communication.

.. 💻 Client
.. +++++++++
.. 1. Pull or build necessary docker images:

.. .. code-block:: bash

..    docker pull weize/ioa-client:latest
..    docker tag weize/ioa-client:latest ioa-client:latest

..    # Pull or Build Your Agent Docker, for example, to pull a react agent docker:
..    # docker pull weize/react-agent:latest
..    # docker tag weize/react-agent:latest react-agent:latest 

.. 2. In client's config file, properly config the server:

.. .. code-block:: yaml

..    server:
..       port: <SERVER_PORT>    # e.g., 7788
..       hostname: <SERVER_IP>  # e.g., 43.163.221.23

.. 3. Launch Milvus service:

.. .. code-block:: bash

..    docker-compose -f dockerfiles/compose/milvus.yaml up

.. 4. Launch your client with your agent. 

.. For example, in `configs/client_configs/case/example/bob.yaml` you can replace the `<SERVER_PORT>` and `<SERVER_IP>` with the opened port and ip of your server, and launch an example:

.. .. code-block:: bash

..    docker-compose -f dockerfiles/compose/example.yaml up


.. ❓ Troubleshooting
.. +++++++++++++++++++++++++++++++++++
.. - If connections fail, check firewall settings and ensure ports are correctly forwarded.
.. - Verify that all IP addresses and hostnames are correctly set in the configuration files.
.. - Check network connectivity between devices using ping or traceroute.

.. For additional help, you can raise an issue in our `Github repo <https://github.com/OpenBMB/IoA/issues>`_.






在分布式设备上运行IoA
==================================

本指南解释了如何在多个设备上配置和运行IoA框架。

🗄️ 服务端设置
----------------

1. 配置网络访问
^^^^^^^^^^^^^^^^^^^^^^^^^^^
在您的服务器上打开两个端口：

- :code:`<SERVER_PORT>` (默认: 7788) 用于IoA服务器
- :code:`<FRONTEND_PORT>` (默认: 80) 用于前端


.. note:: 如果默认端口被占用，请选择其他可用端口。

2. 准备Docker镜像
^^^^^^^^^^^^^^^^^^^^^^^^
拉取并重命名必要的镜像：

.. code-block:: bash

   docker pull weize/ioa-server:latest
   docker pull weize/ioa-server-frontend:latest
   docker tag weize/ioa-server:latest ioa-server:latest
   docker tag weize/ioa-server-frontend:latest ioa-server-frontend:latest

3. 启动服务
^^^^^^^^^^^^^^^^^^
启动Milvus服务：

.. code-block:: bash

   docker-compose -f dockerfiles/compose/milvus.yaml up

启动IoA服务器：

.. code-block:: bash

   docker-compose -f dockerfiles/compose/server_only.yaml up

.. note:: 如果使用自定义端口，请修改 :code:`server_only.yaml` 文件：

   .. code-block:: yaml

      Server:
         ports:
            - <SERVER_PORT>:7788
      
      ServerFrontend:
         ports:
            - <FRONTEND_PORT>:80

4. 访问前端
^^^^^^^^^^^^^^^^^^^^^^
在浏览器中打开 `http://<SERVER_IP>:<FRONTEND_PORT>` 查看智能体的通信界面。

💻 客户端设置
---------------

1. 准备Docker镜像
^^^^^^^^^^^^^^^^^^^^^^^^
拉取IoA客户端镜像和您选择的智能体镜像：

.. code-block:: bash

   docker pull weize/ioa-client:latest
   docker tag weize/ioa-client:latest ioa-client:latest

   # Example for React agent:
   # docker pull weize/react-agent:latest
   # docker tag weize/react-agent:latest react-agent:latest 

2. 配置客户端
^^^^^^^^^^^^^^^^^^^
更新客户端的配置文件：

.. code-block:: yaml

   server:
      port: <SERVER_PORT>    # e.g., 7788
      hostname: <SERVER_IP>  # e.g., 43.163.221.23

3. 启动Milvus服务
^^^^^^^^^^^^^^^^^^^^^^^^
在客户端设备上启动Milvus服务：

.. code-block:: bash

   docker-compose -f dockerfiles/compose/milvus.yaml up

4. 启动客户端
^^^^^^^^^^^^^^^^
使用配置好的智能体启动您的客户端。例如：

.. code-block:: bash

   docker-compose -f dockerfiles/compose/example.yaml up

.. note:: 请确保您已更新 :code:`configs/client_configs/case/example/bob.yaml` 中的 <SERVER_PORT> 和 <SERVER_IP>。

❓ 故障排除
-------------------

- 验证防火墙设置和端口转发。
- 仔细检查所有配置文件中的IP地址和主机名。
- 使用ping或traceroute测试网络连接。

如需进一步帮助，请在我们的GitHub仓库中 `提出问题 <https://github.com/OpenBMB/IoA/issues>`_.