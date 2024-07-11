目标提交
#######################
在设置好服务器和客户端后，你可以将目标发送给IoA。在启动目标之前，你需要创建一个Python脚本。

* 在 :code:`scripts` 目录中创建 :code:`test_your_case.py` 。例如 :code:`scripts/test_paper_writing.py`

目标
===========================
在goal变量中填写你的任务目标描述，并向 :code:`url: "http://127.0.0.1:5050/launch_goal"` 发送POST请求，将 :code:`team_member_names` 设置为None，将 :code:`team_up_depth` 设置为你想要的嵌套团队深度。
完整 URL :code:`url: "http://127.0.0.1:5050/launch_goal"` 用于向本地服务器发送 POST 请求以启动目标。此请求包含一个 JSON 负载，指定目标的详细信息，例如目标描述、最大回合数和团队成员姓名等。此端点的服务器处理请求并设置 IoA 要实现的指定目标。

.. code-block:: python

   import requests 
   goal = "任务描述" 
   # e.g. goal = I want to know the annual revenue of Microsoft from 2014 to 2020. Please generate a figure in text format showing the trend of the annual revenue, and give me a analysis report.
   response = requests.post(
      "http://127.0.0.1:5050/launch_goal",
      json={
         "goal": goal,
         "max_turns": 20,
         "team_member_names": [agent_1, agent_2]  # 如果您没有特定的团队成员，请将其设置为 None
      },
   )