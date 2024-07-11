IoA 安装
#############################

🚀 快速开始
=============================================

仅需几个步骤即可启动并运行IoA：

1. 📋 首要条件
--------------------
* 确保您的本地环境已安装Docker。如果未安装Docker，请访问 `Docker官方网站 <https://docs.docker.com/desktop/>`_ 获取下载详情.

1. 🛳️ 克隆仓库
---------------------------

.. code-block:: bash

   git clone git@github.com:OpenBMB/IoA.git
   cd IoA

3. 🏗️ 构建Docker镜像
--------------------------

核心组件
^^^^^^^^^^^^^^^

你可以直接从docker hub拉取预构建的docker镜像：

.. code-block:: bash

   # Server
   docker pull weize/ioa-server:latest

   # Client
   docker pull weize/ioa-client:latest

   # Server Frontend
   docker pull weize/ioa-server-frontend:latest

   # Rename the images
   docker tag weize/ioa-server:latest ioa-server:latest
   docker tag weize/ioa-client:latest ioa-client:latest
   docker tag weize/ioa-server-frontend:latest ioa-server-frontend:latest

或者你可以从源代码构建

.. code-block:: bash

   # Server
   docker build -f dockerfiles/server.Dockerfile -t ioa-server:latest .

   # Client
   docker build -f dockerfiles/client.Dockerfile -t ioa-client:latest .

   # Server Frontend
   docker build -f dockerfiles/server_frontend.Dockerfile -t ioa-server-frontend:latest .

智能体镜像（按需构建）
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

   # ReAct Agent
   docker pull weize/react-agent:latest
   docker tag weize/react-agent:latest react-agent:latest

   # AutoGPT (we have fixed some bugs in AutoGPT's original docker image)
   docker pull weize/autogpt:latest
   docker tag weize/autogpt:latest autogpt:latest

   # Open Interpreter
   docker pull weize/open-interpreter:latest
   docker tag weize/open-interpreter:latest open-interpreter:latest

或者您可以从源代码构建

.. code-block:: bash

   # ReAct Agent
   docker build -f dockerfiles/tool_agents/react.Dockerfile -t react-agent:latest .   

   # AutoGPT (我们修复了AutoGPT原始docker镜像中的一些错误)
   docker build -f dockerfiles/tool_agents/autogpt.Dockerfile -t autogpt:latest .   

   # Open Interpreter
   docker build -f dockerfiles/tool_agents/open_interpreter.Dockerfile -t open-interpreter:latest .

4. 🌐 启动Milvus服务
------------------------------
.. code-block:: bash

   docker network create agent_network
   docker-compose -f dockerfiles/compose/milvus.yaml up


5. 🎬 启动IoA
----------------

.. code-block:: bash

   cd dockerfiles/compose/
   cp .env_template .env

在 :code:`.env` 文件中，填写您的OpenAI API密钥和其他可选的环境变量。然后，对于包含AutoGPT和Open Interpreter的快速演示：

.. code-block:: bash

   cd ../../
   docker-compose -f dockerfiles/compose/open_instruction.yaml up

这样，您将建立一个包含AutoGPT和Open Interpreter的小规模智能体互联网！


6. 🧪 测试
---------------------
您可以使用以下脚本在我们的Open Instruction数据集上测试IoA。

.. code-block:: bash

   python scripts/open_instruction/test_open_instruction.py

或者简单地发送一个post请求，如下所示：

.. code-block:: python

   import requests

   goal = "I want to know the annual revenue of Microsoft from 2014 to 2020. Please generate a figure in text format showing the trend of the annual revenue, and give me a analysis report."

   response = requests.post(
    "http://127.0.0.1:5050/launch_goal",
    json={
        "goal": goal,
        "max_turns": 20,
        "team_member_names": ["AutoGPT", "Open Interpreter"],   # 当为 "None" 时，智能体将自主决定是否组建团队
    },
   )

   print(response)
   
