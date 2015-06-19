# 相关度

**相关度(Relevance)** 是一个查询响应满足用户搜索信息的程度。

查询响应的相关度依赖于查询被执行的上下文。
单个搜索应用根据用户的需要和期待可能有不同的使用上下文。
例如，气候数据的搜索引擎对大学研究员可用来学习长期的气候趋势，
农民可能感兴趣的是计算春天最后一次霜冻的日期，
公务的工程师可能对降水模式和洪水频率感兴趣，
而大学生可能计划假期去某个地区，想知道何时可以出行。
因为这些用户不同的动机，对一个查询的特定响应的相关度也会不同。

查询响应应该有多详尽？
通常像相关度一样，这个问题也依赖于搜索的上下文。
在某个查询的响应中 *没有* 找到一个特定文档的成本在某些上下文中非常高，
比如对某个传票的响应中的一个合法的电子取证的搜索；
有的成本就不高，如 Web 网站上数十上百个的蛋糕菜谱中的其中一个。
当配置 Solr 时，你需要衡量详尽性和其它像时间线和易用性等因子。

上面的电子取证和菜谱的示例演示了和相关度有关的两个重要概念：

* **查准率(Precision)** 是返回的结果中的文档是相关文档的比例
* **查全率(Recall)** 是返回的相关结果占系统中所有相关结果的比例。
要取得完美的查全率很简单：对每次查询简单地返回集合中的所有文档既可

回到上面的示例，对电子取证搜索应用，拥有 100% 的查全率以返回和某个传票相关的所有文档是很重要的。
然而但对菜谱应用，相对而言查准率更重要一些。
某些情况下，在非正式的上下文中返回过多的结果可能会淹没用户。
某些上下文中，返回更少但相关度更高的结果可能是最好的方式。

有了查准率和查全率的概念，就有可能量化对不同的用户和不同的对集合文档的查询的相关度。
一个完美的系统对每个用户和每次查询都将会有 100% 的查准率和 100% 的查全率。
或者说，它都将查出而且只查出所有相关的文档。
特别地，当我们讨论真实系统中的查准率和查全率时，通常关注于某个特定数量的结果的查准率和查全率，
最常见(也最有用)的是十个结果。

通过 faceting 、查询过滤器和其他搜索组件， Solr 可以非常灵活地配置以帮助用户
细粒度地调整他们的搜索以给用户返回最相关的结果。
也就是说， Solr 可被配置来权衡查准率和查全率以满足某个特定用户社区的需要。

一个 Solr 应用的配置应当考虑：

* 应用的多种用户的需求(包含易用性、响应速度以及其它限制信息等需求)
* 针对这些用户的多种不同上下文有意义的分类(如日期、产品分类或地区等)
* 任何文档固有的相关度(如确保有一个官方的产品描述或 FAQ 总是在接近搜索结果的顶部返回可能很有用)
* 文档的年龄是否重要(某些上下文中，最新的文档总是最重要的)

铭记这些因素，在 Solr 部署的计划阶段去草拟你能想到的是搜索应用针对示例查询应该返回的响应的类型
常常会很有帮助。
一旦应用上线运行了，你可以采用一系列测试方法，如关注分组、内部测试、
[TREC](http://trec.nist.gov) 测试和 A/B 测试等
来调整应用配置以更好地满足用户需求。

更多有关相关度的信息，可以查看 Grant Ingersoll 在 SearchHub.org 上的技术文档
[Debugging Search Application Relevance Issues](http://searchhub.org/2009/09/02/debugging-search-application-relevance-issues/)