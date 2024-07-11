客户端配置
#######################

要将您的智能体（或我们提供的智能体）成功集成到您的IoA服务器中，必须配置客户端设置以确保在IoA生态系统中正确注册。这涉及设置服务器详细信息、定义智能体规范和调整通信设置，具体如下：

* 在 :code:`configs/client_configs/cases` 目录下为您的案例创建一个名为 your_case_name 的文件夹。例如：:code:`configs/client_configs/cases/example`

* 创建一个名为 :code:`agent_name.yaml` 的文件作为智能体的配置文件，根据需要的智能体数量，创建相应数量的YAML文件。例如：:code:`configs/client_configs/cases/example/bob.yaml`

以下是参数配置的示例。配置文件分为三个部分： **服务端** , **工具智能体**, **通信服务客户端**.

服务器
===========================
服务器部分负责设置基本的服务器配置

.. code-block:: yaml

   server:  
      port: SERVER_PORT    # e.g. default 7788
      hostname: SERVER_IP  # e.g. default ioa-server

|

工具智能体
===========================
工具智能体部分定义了工具智能体本身的配置，并表示集成到IoA平台中的各种智能体，如ReAct、OpenInterpreter等。工具智能体的包含是可选的，具体取决于给定用例所需的特定智能体。



.. code-block:: yaml

   tool_agent: 
      agent_type: ReAct
      agent_name: 工具智能体名称
      desc: |- 
         工具智能体能力的描述。
      tool_config: 工具的配置文件  # e.g tools_code_executor.yaml
      image_name: react-agent
      container_name: docker 容器名称
      port: 智能体的Docker容器将暴露的端口号。
      model: 智能体使用的模型  # e.g. gpt-4-1106-preview
      max_num_steps: 智能体在其过程中可以执行的最大步骤数。




|

通信服务客户端
===================================
通信服务客户端部分用于与其他客户端通信和交互，并为工具智能体分配任务。

.. code-block:: yaml

   comm:  
      name: 客户端的名称。
      desc: 通信智能体能力的描述。
      type: 通信智能体的类型。  # Thing Assistant or Human Assistant
      support_nested teams: 指示智能体是否支持嵌套团队。  # true or false
      max_team_up_attempts: 与其他智能体组队的最大尝试次数。
      llm:  
         llm_type: 定义大语言模型的类型 # e.g. openai-chat
         model: 指定大语言模型的模型，表示使用的AI模型的版本和类型  # e.g., gpt-4-1106-preview 
         temperature: 控制大语言模型响应的随机性  # default value is 0.1

   