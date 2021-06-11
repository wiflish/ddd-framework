## DDD脚手架
基于DDD的项目脚手架，基于DDD的一种落地实践。

理念: 采用以业务为微内核的理念、结合SPI，以领域模型为中心，基于领域模型定义各种接口，把实现放到外围，类似于以扩展点的形式加载到领域模型中。


各模块职责如下:

| 模块名称 | 服务描述 |基本约定|
|:--------:|:------ |:------|
|ddd-framework-archetype-api|外部依赖的接口层，提供给外部调用的接口定义，不依赖其他模块。| <li>接口定义统一以ApiService结尾</li> <li>内部自洽，尽量少的依赖其他组件</li>|
|ddd-framework-archetype-application|应用服务层，服务启动的入口。对外暴露的接口服务处理，不处理业务逻辑，仅做各种领域的组装和拼接，依赖ddd-framework-archetype-infra模块。| <li>实现统一以ApiServiceImpl结尾</li><li>不处理实际业务，只做分发和数据组装</li><li>Http接口也放到这一层</li>|
|ddd-framework-archetype-infra|基础设施层，处理DB、Message等基础设施相关的逻辑实现，依赖ddd-framework-archetype-domain模块|<li>数据库的实现，通过依赖倒置将实现注入到domain层</li><li>消息的处理</li><li>表的映射对象以PO结尾，表示是持久化对象</li>|
|ddd-framework-archetype-domain|核心领域层，处理业务的核心逻辑，不依赖其他模块|<li>关注业务逻辑的实现</li><li>有且仅有领域模型相关的对象</li><li>vo包下的是值对象</li>|

