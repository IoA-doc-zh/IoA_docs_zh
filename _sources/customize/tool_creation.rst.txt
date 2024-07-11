工具创建
#######################
如果您没有自己的智能体，但想要提供一个自定义工具，让 ReAct 智能体或其他现有智能体可以利用该工具解决问题，则需要创建工具。当您拥有专门的工具或功能，可以增强智能体的功能而无需开发成熟的新智能体时，就会产生这种需求。通过集成这些工具，ReAct 智能体可以利用它们执行特定任务，从而扩展其解决问题的能力，使其在处理更广泛的场景时更加灵活和有效。在介绍工具配置之前，需要为工具配置创建一个 yaml 文件和相应工具的 Python 文件。

* 在 :code:`im_client/agents/tools` 中创建并完成相应工具的 Python 实现。例如： :code:`im_client/agents/tools/code_executor.py`
  
* 将完成的工具导入并添加到：:code:`im_client/agents/tools/__init__.py` 中的 :code:`TOOL_MAPPING`，确保工具调用成功。例如：

  .. code-block:: python

      from . import arxiv_tools
      TOOL_MAPPING = {
      "arxiv_search": arxiv_tools.arxiv_search
      }

* 创建一个名为 :code:`tools_name.yaml` 的文件，作为工具智能体调用该工具的配置文件。YAML文件内所有工具的格式应遵循OpenAI函数调用格式。例如：:code:`im_client/agents/react/tools_code_executor.yaml`。
  
以下是 YAML 配置的示例：

具有必需参数的工具
=====================================

.. code-block:: yaml

    - function:
        description: 函数描述
        name: 函数名称
        parameters:
          properties:
            parameters_1:
              description:  参数1的描述
              type: string / number / boolean 
              enum: ["如果您的参数由 Literal 类型或指定参数设置，则必须包含该参数"] 
            parameters_2:  # 如果函数中有多个参数，则必须包含该参数
              description:  参数2的描述
              type: string / number / boolean 
          required:
          - 参数1
          - 参数2
          type: object
      type: function

|

Tool without required parameters
=========================================

.. code-block:: yaml

    - function:
        description: 函数描述
        name: 函数名称
        parameters:
          properties: {} 
          required: [] 
          type: object
      type: function
