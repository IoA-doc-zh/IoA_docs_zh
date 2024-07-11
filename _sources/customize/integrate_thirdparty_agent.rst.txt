集成第三方智能体
################################

以下是集成第三方智能体的简要指南。如果您想集成来自第三方仓库的智能体，主要有两点需要考虑：


* **构建和公开 Docker 容器**:
  
  * **容器化**: 将第三方智能体打包在 Docker 容器中。这可确保智能体运行的环境一致且隔离


* **开发集成适配器**:
  
  * **公开 API 接口**: 利用 FastAPI 或其他合适的 Web 框架向外部公开运行接口。该接口应具有以下规范：
  
    * **run(task_desc)**: 从头开始执行 :code:`task_desc` 任务并以字符串形式返回结果。

您可以查看具体实例Open Interpreter位于 :code:`im_client/agents/open_interpreter` 的实现逻辑。此示例的详细说明在以下部分中给出。

|

Open Interpreter 集成
===============================
* **为 Open Interpreter 构建HTTP服务**: 
  
  * 位于 :code:`im_client/agents/open_interpreter/open_interpreter_agent.py` 脚本中的 Open Interpreter 将被 docker 化。此脚本包含 FastAPI POST 端点，在使用 Uvicorn 启动时，这些端点将作为 HTTP 服务公开。使用 Docker 部署后，可以从外部访问这些端点。

* **为 Open Interpreter 创建 Dockerfile**: 
  
  * 接下来，在 :code:`dockerfiles/tool_agents` 目录中创建一个 Dockerfile。此 Dockerfile 确保可以使用 Docker 启动Open Interpreter等工具智能体，从而防止与 IoA 发生潜在的环境冲突。

* **构建 Open Interpreter 适配器**: 
  
  * Open Interpreter 适配器也位于 :code:`im_client/agents/open_interpreter/open_interpreter_agent.py`，有助于弥合 IoA 协议与 Open Interpreter 之间的差距。它将请求转换并转发到 Open Interpreter Docker 容器。
  
*  **构建 Open Interpreter 配置文件**: 
    
   * Open Interpreter 的示例配置文件位于 :code:`configs/client_configs/cases/example/open_interpreter.yaml`。有关配置参数的说明，请参阅 `客户端配置部分 <client_configuration.html>`_ 。

|

Open Interpreter Docker 启动
=======================================
* 环境变量配置:
  
  * 在 :code:`dockerfiles/compose/open_interpreter.yaml` 中设置环境变量 :code:`CUSTOM_CONFIG`，用于指定工具智能体的配置文件。在 :code:`CUSTOM_CONFIG` 引用的文件中定义工具智能体相关参数。例如，Open Interpreter 的配置文件为：
  
    .. code-block:: yaml

      CUSTOM_CONFIG=configs/cases/open_interpreter.yaml
  
  * 在 :code:`dockerfiles/compose/.env` 中，确保设置必要的环境变量，例如 :code:`OPENAI_API_KEY` 和 :code:`OPENAI_RESPONSE_LOG_PATH`。

* 构建并运行 Docker 容器：
  
  * 通过在终端中运行以下命令来构建先前创建的 Dockerfile：
   
    .. code-block:: bash

      docker build -f dockerfiles/tool_agents/open_interpreter.Dockerfile -t open_interpreter:latest .
  
  * 然后，通过运行以下命令启动服务器和通信智能体：
  
    .. code-block:: bash

      docker-compose -f dockerfiles/open_interpreter.yml up






