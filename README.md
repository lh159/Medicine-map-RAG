# Medicine-map-RAG
个性化知识图谱
一、项目概述
本项目旨在构建一个基于中医药领域的医疗智能问答系统，通过整合 Neo4j 图数据库、RAG（Retrieval-Augmented Generation）技术和通义千问的 API 接口，并使用 Django 框架实现一个简单的查询问答系统，为用户提供准确、高效的中医药相关问题的解答服务。
二、功能需求
（一）Neo4j 图数据库模块

1. 节点和边关系
  - 参考build_medicalgraph.py文件，图数据库包含以下节点和边关系：
    - 节点类型：共 7 类节点（具体节点信息在read_nodes方法中），包含疾病节点（在create_diseases_nodes方法中创建）等。
    - 边关系：实体关系边（在create_graphrels方法中创建）和实体关联边（在create_relationship方法中创建）。
  - 提供 Neo4j 图数据库的接口调用功能，实现对图数据库的查询操作，以便获取与用户问题相关的中医药知识信息。
2. 配置信息
  - 使用以下配置连接 Neo4j 数据库：

NEO4J_GRAPH = Graph("xxxxxxxx",
    auth=("xxxx", "xxxxxx"))
（二）RAG 技术优化搜索模块

1. 信息检索
  - 对用户输入的问题进行分析和处理，利用 RAG 技术从 Neo4j 图数据库中检索与问题相关的中医药知识信息。
  - 设计有效的检索策略，提高检索的准确性和效率，例如采用关键词匹配、语义分析等方法。
2. 信息整合
  - 将检索到的相关信息进行整合和筛选，去除冗余和无关信息，提取关键信息作为生成回答的依据。
（三）通义千问 API 接口模块

1. 配置信息
  - 使用以下通义千问 API 的配置信息：


DASHSCOPE_API_KEY = "xxxxxxxxx"

2. 问答生成
  - 将 RAG 技术整合的相关信息作为上下文，调用通义千问的 API 接口，生成针对用户问题的准确、自然的回答。
  - 处理 API 接口的返回结果，对回答进行适当的格式化和处理，以提高用户体验。
（四）Django 框架模块

1. 用户界面
  - 实现一个简单的 Web 界面，用户可以在界面上输入中医药相关的问题，并提交查询请求。
  - 界面设计应简洁、易用，提供良好的用户交互体验。
2. 请求处理
  - 接收用户的查询请求，将请求转发给相应的处理模块（如 RAG 技术模块、通义千问 API 接口模块）进行处理。
  - 对处理结果进行展示，将生成的回答返回给用户，并在界面上显示。
三、非功能需求
（一）性能要求

1. 系统应具备良好的响应性能，对于用户的查询请求，应在合理的时间内返回结果，避免用户长时间等待。
2. 优化 RAG 技术的检索和通义千问 API 接口的调用过程，提高系统的整体性能。
（二）安全性要求
1. 对用户输入的信息进行安全过滤，防止 SQL 注入、XSS 攻击等安全问题。
2. 妥善保管通义千问的 API 密钥和 Neo4j 数据库的认证信息，避免信息泄露。
（三）可扩展性要求
1. 系统应具备良好的可扩展性，便于后续添加新的功能模块或扩展中医药知识信息。
2. 代码结构应清晰、模块化，易于维护和扩展。
四、接口设计
（一）Neo4j 图数据库接口

1. 查询接口
  - 设计用于查询节点和边关系的接口，根据用户问题中的关键词和语义信息，从图数据库中检索相关信息。
  - 接口应支持灵活的查询条件，如节点类型、边关系类型等。
（二）通义千问 API 接口

1. 问答生成接口
  - 封装通义千问的 API 接口，将 RAG 技术整合的相关信息作为输入，调用 API 生成回答。
  - 处理 API 接口的返回结果，将回答进行格式化和处理后返回给 Django 框架。
五、数据库设计

本项目主要使用 Neo4j 图数据库，其节点和边关系的设计参考build_medicalgraph.py文件。
六、测试需求
1. 单元测试
  - 对各个功能模块（如 Neo4j 图数据库接口、RAG 技术模块、通义千问 API 接口模块）进行单元测试，确保每个模块的功能正常。
2. 集成测试
  - 对整个系统进行集成测试，测试各个模块之间的交互和数据传递是否正常，确保系统的整体功能符合需求。
3. 性能测试
  - 对系统的性能进行测试，包括响应时间、吞吐量等指标，确保系统在高并发情况下仍能稳定运行。
七、部署需求
1. 选择本地环境进行系统部署
2. 配置服务器的网络环境，确保系统能够正常访问 Neo4j 图数据库和通义千问的 API 接口。
3. 部署 Django 应用，配置 Web 服务器（如 Nginx、Apache 等），实现系统的对外服务。

