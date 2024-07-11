GAIA 基准
=======================================

让我们深入了解 GAIA 基准 - 一项旨在挑战 AI 智能体解决问题能力的严格测试！

🤔 什么是 GAIA?
-----------------
`GAIA <https://arxiv.org/abs/2311.12983>`_ 是一项基准，用于测试 AI 系统在各种现实世界任务中的表现，这些任务需要一系列基本能力，例如推理、多模态处理、网页浏览以及一般的工具使用能力

🚀 让我们开始吧！
----------------------

0. 准备 docker 镜像：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

我们假设您已按照 `说明 <../getting_started/installation.html>`_ 为服务器、客户端和 ReAct 智能体准备 docker 镜像。

1. 启动 Milvus 服务：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

首先，我们需要启动 Milvus 服务。它就像我们 AI 团队的图书管理员，帮助快速组织和检索信息。

.. code-block:: bash

    docker-compose -f dockerfiles/compose/milvus.yaml up

2. 启动服务端和客户端：
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   
现在，让我们将服务器和客户端智能体联机。此命令设置协作环境。

.. code-block:: bash

    docker-compose -f dockerfiles/compose/gaia.yaml up

3. 游戏开始！
^^^^^^^^^^^^^^^^^^^^^^^

一切就绪后，是时候启动 GAIA 基准测试了。

.. code-block:: bash

    python scripts/gaia/test_gaia.py --level <level_in_gaia> --max_workers <thread_number>

- 将 :code:`<level_in_gaia>` 替换为您选择的难度（1、2 或 3）。
- 设置 :code:`<thread_number>` 以决定团队同时处理的任务数。
