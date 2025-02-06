---
title: ElasticSearch
published: 2025-02-06
description: 'ElasticSearch Tutorial'
image: ''
tags: ["ElasticSearch"]
category: 'Tool'
draft: false 
lang: 'zh_CN'
---

## 简介

对于 ElasticSearch，其两个重要的概念即为文档和词条，其中词条是通过分词实现的，是实现倒排索引的重要字段；

**创建倒排索引**是对正向索引的一种特殊处理和应用，流程如下：

- 将每一个文档的数据利用**分词算法**根据语义拆分，得到一个个词条；
- 创建表，每行数据包括词条、词条所在文档id、位置等信息；
- 因为词条唯一性，可以给词条创建**正向**索引。

## 查询

对于 ES 而言，其查询方式主要有叶子查询和复合查询，对于模糊的查询可以使用 match 来匹配对应字段中所有出现该词的文档，并基于score 进行排序展示；对于精确查询则使用 term 对对应字段的值进行精确查询匹配；

对于复合查询，支持 bool 查询条件，包括 must、should、must_not、filter 等条件进行筛选；

此外，对于 ES 中文档的查询，还支持排序、分页、高亮等查询选项；

对于 ES 而言，还支持对应的聚合，如桶聚合、条件聚合、metric 聚合；
