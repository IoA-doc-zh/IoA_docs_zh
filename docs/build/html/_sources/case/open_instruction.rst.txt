开放指令数据集
========================

让我们探索我们精心策划的开放指令数据集 - 旨在测试 AI 智能体多功能性的多样化任务集合！

🤔 什么是开放指令数据集？
---------------------------------------
该数据集包含广泛的开放式指令，挑战 AI 系统执行各种领域的任务，例如信息检索、编码、数学问题解决和一般协助。

🚀 让我们开始吧！
---------------------

0. 准备 docker 镜像：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

我们假设您已按照 `安装说明 <../getting_started/installation.html>`_ 为服务器客户端、**AutoGPT 和 Open Interpreter** 准备 docker 镜像.

1. 启动 Milvus 服务：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

首先，我们需要启动 Milvus 服务来帮助高效地管理和检索信息：

.. code-block:: bash

    docker-compose -f dockerfiles/compose/milvus.yaml up

2. 启动服务器和客户端：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

现在，让我们将服务器和客户端智能体联机，包括 AutoGPT 和 Open Interpreter：

.. code-block:: bash

    docker-compose -f dockerfiles/compose/open_instruction.yaml up

1. 启动开放指令数据集测试：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

一切设置完毕后，就可以运行开放指令数据集了：

.. code-block:: bash

    python scripts/open_instruction/test_open_instruction.py

此脚本会将我们精选数据集中的指令发送到 IoA 框架，让您观察 AutoGPT 和 Open Interpreter 如何协作处理各种开放式任务。

🎭 观看合作展开
---------------------------------
在测试运行时，您将看到 AutoGPT 和 Open Interpreter 协同工作，利用其独特功能来处理各种指令。这展示了 IoA 在集成不同 AI 智能体以解决各种开放式问题方面的强大功能。

请随意检查输出并查看智能体在处理各种类型的任务时如何相互补充。本次测试展示了IoA框架在真实场景中的灵活性和适应性！