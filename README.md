# Python-Library-API




## 安装准备




## 安装Graphene的Python库

Dangdang-chain 建立依据的是 Graphene 基础设施，所以为 Graphene 设计的API接口在Dangdang-chain 仍然可以运行。

### 方法1 （手动安装）

下载Graphene的python库代码：

```bash
git clone https://github.com/xeroc/python-graphenelib/
```

安装python-graphenelib库：

```bash
cd python-graphenelib
python3 setup.py install
```

### 方法2 （`pip`安装）

```bash
sudo apt-get install libffi-dev libssl-dev python-dev
pip3 install graphenelib
```

## 测试脚本


假设当前私链的区块生产间隔是1s，cli_wallet命令行钱包的开启的rpc监听端口是`30892`，则通过每个区块从账户nathan给账户gamma转账1000次的测试脚本如下：

```Python


import time
import json
from grapheneapi.grapheneapi import GrapheneAPI


blockinterval    = 1
numbertxperblock = 1000
rounds = 5


log = open("stress_test.log","a");


if __name__ == '__main__':
	client = GrapheneAPI("47.91.22.22", 38092, "", "")
	k = 0
	while k < rounds :
		for i in range(0,numbertxperblock) :
			print(i)
			log.write(str(i))
			res = client.transfer("dang-dang","apitestkn01","0.1", "DANG", "injectTest", True);
			#print(json.dumps(res,indent=4))
			log.write(json.dumps(res,indent=4))
		k = k + 1
		time.sleep(blockinterval)




log.close()




```



```json
root@iZ6wee92clbvvf28j9oojzZ:/home/cTnode/python-graphenelib# more stress_test.log
0{
    "ref_block_prefix": 2113389145,
    "operations": [
        [
            0,
            {
                "to": "1.2.21",
                "amount": {
                    "asset_id": "1.3.0",
                    "amount": 100
                },
                "fee": {
                    "asset_id": "1.3.0",
                    "amount": 200000
                },
                "from": "1.2.17",
                "extensions": []
            }
        ]
    ],
    "signatures": [
        "2007a68d9d3fcc1b0b27f2c00c98b5bd72a19f172a431f8c22da074d7270b470d5680b7beddaea3c85e10b4157b
5addac4626d08959760e98dabd9e64d39ce5c75"
    ],
    "ref_block_num": 48911,
    "extensions": [],
    "expiration": "2018-08-27T20:44:25"
}1{
    "ref_block_prefix": 2113389145,
    "operations": [
        [
            0,
            {
                "to": "1.2.21",
                "amount": {
                    "asset_id": "1.3.0",
                    "amount": 100
                },
                "fee": {
                    "asset_id": "1.3.0",
                    "amount": 200000
                },
                "from": "1.2.17",
                "extensions": []
            }
        ]
    ],
    "signatures": [
        "1f3bc986e8269e34b759213f8a39d92917cfff193083fec7897e0fef47506268c47f975816f5d0691e090a81ae5
b96978e880368cf9b37ab92ad10d6cc975e77b8"
    ],
    "ref_block_num": 48911,
    "extensions": [],
    "expiration": "2018-08-27T20:44:26"
}2{
    "ref_block_prefix": 2113389145,
    "operations": [
        [
            0,
            {
                "to": "1.2.21",
                "amount": {
                    ...
```


## Reference

+ [Python Graphene Doc](https://python-graphenelib.readthedocs.io/en/latest/)






