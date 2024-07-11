Docker Compose 设置
#######################

自定义 Docker Compose YAML 文件对于设置环境以包含各种智能体的 Docker 容器以及配置每个容器的所有必要变量至关重要。此设置允许在 IoA 平台内无缝集成和编排多个智能体和工具，确保它们能够有效且高效地协同工作。Docker Compose 配置简化了部署过程，提供了一种集中的方式来管理依赖项、环境设置和网络配置。

Docker Compose 配置
=====================================
在 :code:`dockerfiles/compose` 目录中创建特定于实例的 :code:`your_case.yml` 文件. 例如：:code:`dockerfiles/compose/IOT_Party.yml`。

.. code-block:: yaml

      version: "3" 

      service:
      Name:  # e.g. WeizeChen 
         image: 指定用于此服务的 Docker 映像  # e.g. ioa-client:latest
         build: 
            context: ../../
            dockerfile: dockerfiles/client.Dockerfile
         container_name: Docker 容器的名称
         env_file:
            - .env
         volumes:
            - /var/run/docker.sock:/var/run/docker.sock
            - ${DOCKER_VOLUME_DIRECTORY:-.}/volumes/sqlite:/app/database
            - ./volumes/openai_response_log:${OPENAI_RESPONSE_LOG_PATH}
            - ../../configs/client_configs:/app/configs
         environment:
            - OPENAI_API_KEY
            - CUSTOM_CONFIG=agent 配置文件路径  # e.g. configs/cases/paper_writing/weizechen.yaml
         ports:
            - 将 host_port 映射到 container_port，允许访问服务  # e.g. 5050:5050
         depends_on:
            - Server
         stdin_open: true
         tty: true

