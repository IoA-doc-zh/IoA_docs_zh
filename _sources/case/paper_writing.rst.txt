协作论文写作
##########################################

让我们尝试一个有趣而简单的 IoA 工作示例：起草 IoA 研究论文的引言。

✍️ 使用 IoA 撰写论文
=========================

想象一下：四个 AI 助手围坐在虚拟桌子旁，集思广益，为关于 IoA 本身的论文撰写完美的引言。这是我们的梦之队：

1. Weize Chen's Assistant
2. Chen Qian's Assistant
3. Cheng Yang's Assistant
4. ArxivAssistant (我们的研究大师)

ArxivAssistant 是团队中的书虫。它基于 ReAct 代理框架构建，擅长从 Arxiv 中挖掘相关论文来支持我们的写作。

⚙️ 试着去启动
--------------------------------

准备好看看这些代理的实际作用了吗？按照以下简单步骤操作：

1. 启动 Milvus 服务：

首先，我们需要启动 Milvus 服务。它就像我们 AI 团队的图书管理员，帮助快速组织和检索信息。

.. code-block:: bash

    docker-compose -f dockerfiles/compose/milvus.yaml up

2. 创建 ReAct Agent 镜像：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash
  
  docker pull weize/react-agent:latest
  docker tag weize/react-agent:latest react-agent:latest

    # or 
    # docker build -f dockerfiles/tool_agents/react.Dockerfile -t react-agent:latest . 

3. 设置您的凭证：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   
将您的 OpenAI API 密钥和其他环境变量添加到 :code:`dockerfiles/compose/.env`. 

.. note:: 如果您已将这些设置为系统环境变量，则可以跳过此步骤！

4. 启动 IoA 写作小组：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  docker-compose -f dockerfiles/compose/paper_writing.yml up --build

5. 启动写作过程：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

在新的命令行窗口中，运行：

.. code-block:: bash

  python scripts/test_paper_writing.py

就这样！您刚刚发起了一项由 AI 驱动的写作协作。

.. |

.. Paper Writing with Printer
.. ====================================
.. IOA Paper Writing with Printer builds on the Paper Writing scenario, introducing the FormatCraft Printer which can print out the result of the IOA paper introduction completed in the Paper Writing scenario. Here’s how to start and use it:

.. 1. First, create the ReAct Agent image.

..    .. code-block:: bash

..      docker build -f dockerfiles/tool_agents/latex_printer_react.Dockerfile  -t latex_printer_react:latest .


.. |

.. 2. Create a network that allows docker containers to communicate with each other.

..    .. code-block:: bash

..      docker network create agent_network


.. |

.. 3. Start the containers specified in the docker-compose configuration file.

..    .. code-block:: bash

..      docker-compose -f dockerfiles/compose/paper_writing_with_printer.yml up --build


.. |

.. 4. After starting, execute a command in another window command line, which will initiate a goal.

..    .. code-block:: bash

..      python tests/test_paper_writing_with_printer.py
