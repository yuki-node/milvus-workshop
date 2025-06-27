# 使用 Zilliz Cloud 快速体验 Milvus

在学习 Milvus 向量数据库时，除了本地 Milvus Lite、单机版 Milvus Standalone 或 Milvus on K8s 之外，还可以选择 **Zilliz Cloud** —— 一种无需部署服务器、零成本上手的托管方案。下面将演示如何申请 Zilliz Cloud 中国区免费套餐并运行官方示例代码。

------

## 一、注册并创建免费集群

1. 打开官网

   - 国内站点：https://zilliz.com.cn/
   - 海外站点：https://zilliz.com/

   ![a508309b90c710ffd1d9e998626c47f9](https://raw.githubusercontent.com/cloudsmithy/picgo-imh/master/a508309b90c710ffd1d9e998626c47f9.png)

2. 选择 **手机号码** 或 **邮箱** 登录/注册。

   ![image-20250626212403361](https://raw.githubusercontent.com/cloudsmithy/picgo-imh/master/image-20250626212403361.png)

3. 进入控制台首页后，点击 **Create Cluster** 按钮。
    ![起始页面](https://raw.githubusercontent.com/cloudsmithy/picgo-imh/master/d712d4c4fd8f2546dab4426c68bf806f.png)

4. 在弹窗中选择 **Free Tier**（免费套餐），数据中心默认为 **阿里云 · 杭州**。
    ![选择免费集群](https://raw.githubusercontent.com/cloudsmithy/picgo-imh/master/25626960ddcd05d12117aff485eb2487.png)

5. 等待几分钟，集群创建完成后会显示 **Endpoint URI、API Token、Cluster ID** 等信息，请妥善保存。
    ![集群信息](https://raw.githubusercontent.com/cloudsmithy/picgo-imh/master/3d606a5a0a797d7332bbb3efd86fd8c4.png)

6. 运行中

![395f581c7dbbeb8b4940afa0bcab025a](https://raw.githubusercontent.com/cloudsmithy/picgo-imh/master/395f581c7dbbeb8b4940afa0bcab025a.png)

------

## 二、准备本地 Python 环境



新建虚拟机环境

```bash
conda create -n milvus-py python==3.12 -y
conda activate milvus-py
```

## 

1. **克隆仓库**

```bash
git clone https://github.com/zilliztech/cloud-vectordb-examples.git
```

1. **安装 PyMilvus**

```bash
pip3 install pymilvus==2.5.3
```

1. **进入 Python 示例目录**

```bash
cd cloud-vectordb-examples/python
```

------

## 四、配置连接信息

在 `config.ini` 中填入你的集群信息（务必保持格式）：

```ini
uri = https://<your-endpoint>
token = <your-api-key>
```

------

## 五、运行示例脚本

```bash
python3 hello_zilliz_vectordb.py
```

运行后可见类似输出：

```
Connected to DB: https://in03-d7b5690fee7bcbf.serverless.ali-cn-hangzhou.cloud.zilliz.com.cn successfully
Start to create the collection schema
Start to prepare index parameters with default AUTOINDEX
Start to create example collection: book
Collection details: {'collection_name': 'book', 'auto_id': False, 'num_shards': 1, 'description': '', 'fields': [{'field_id': 100, 'name': 'book_id', 'description': 'customized primary id', 'type': <DataType.INT64: 5>, 'params': {}, 'is_primary': True}, {'field_id': 101, 'name': 'word_count', 'description': 'word count', 'type': <DataType.INT64: 5>, 'params': {}}, {'field_id': 102, 'name': 'book_intro', 'description': 'book introduction', 'type': <DataType.FLOAT_VECTOR: 101>, 'params': {'dim': 64}}], 'functions': [], 'aliases': [], 'collection_id': 457861707686138665, 'consistency_level': 2, 'properties': {}, 'num_partitions': 1, 'enable_dynamic_field': False}
Start to insert 2000 entities into example collection: book
Insert completed in 0.692 seconds
Start to flush
Flush completed in 3.0984 seconds
Search 0 results: data: ["[{'id': 0, 'distance': 10.547525405883789, 'entity': {}}, {'id': 1, 'distance': 10.547525405883789, 'entity': {}}]", "[{'id': 0, 'distance': 8.913854598999023, 'entity': {}}, {'id': 1, 'distance': 8.913854598999023, 'entity': {}}]", "[{'id': 1000, 'distance': 9.11572551727295, 'entity': {}}, {'id': 1001, 'distance': 9.11572551727295, 'entity': {}}]"] , extra_info: {'cost': 6}
Search 0 latency: 3.4933 seconds
Search 1 results: data: ["[{'id': 0, 'distance': 8.898500442504883, 'entity': {}}, {'id': 1, 'distance': 8.898500442504883, 'entity': {}}]", "[{'id': 0, 'distance': 9.7216157913208, 'entity': {}}, {'id': 1, 'distance': 9.7216157913208, 'entity': {}}]", "[{'id': 1000, 'distance': 8.997819900512695, 'entity': {}}, {'id': 1001, 'distance': 8.997819900512695, 'entity': {}}]"] , extra_info: {'cost': 6}
Search 1 latency: 0.099 seconds
Search 2 results: data: ["[{'id': 0, 'distance': 7.597465515136719, 'entity': {}}, {'id': 1, 'distance': 7.597465515136719, 'entity': {}}]", "[{'id': 0, 'distance': 9.255533218383789, 'entity': {}}, {'id': 1, 'distance': 9.255533218383789, 'entity': {}}]", "[{'id': 0, 'distance': 9.471370697021484, 'entity': {}}, {'id': 1, 'distance': 9.471370697021484, 'entity': {}}]"] , extra_info: {'cost': 6}
Search 2 latency: 0.0677 seconds
Search 3 results: data: ["[{'id': 1000, 'distance': 8.828998565673828, 'entity': {}}, {'id': 1001, 'distance': 8.828998565673828, 'entity': {}}]", "[{'id': 1000, 'distance': 8.66336441040039, 'entity': {}}, {'id': 1001, 'distance': 8.66336441040039, 'entity': {}}]", "[{'id': 0, 'distance': 9.222965240478516, 'entity': {}}, {'id': 1, 'distance': 9.222965240478516, 'entity': {}}]"] , extra_info: {'cost': 6}
Search 3 latency: 0.0722 seconds
Search 4 results: data: ["[{'id': 0, 'distance': 9.342487335205078, 'entity': {}}, {'id': 1, 'distance': 9.342487335205078, 'entity': {}}]", "[{'id': 0, 'distance': 6.45243501663208, 'entity': {}}, {'id': 1, 'distance': 6.45243501663208, 'entity': {}}]", "[{'id': 0, 'distance': 8.369773864746094, 'entity': {}}, {'id': 1, 'distance': 8.369773864746094, 'entity': {}}]"] , extra_info: {'cost': 6}
Search 4 latency: 0.0687 seconds
```

如果控制台显示如上日志，即表明已成功连接集群、创建 collection 并完成简单的向量检索。

------

![image-20250626211850476](https://raw.githubusercontent.com/cloudsmithy/picgo-imh/master/image-20250626211850476.png)

------

> 通过 Zilliz Cloud，我们可以在几分钟内获得一套托管版 Milvus 服务，免去本地运维与资源成本，非常适合作为学习、原型开发或小型应用的向量数据库后端。祝大家玩得开心！
