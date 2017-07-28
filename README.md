## SteemData

This is fork of SteemData created by furion. The goal of the SteemData project is to make data from the STEEM blockchain more accessible to developers, researchers and 3rd party services.

SteemData is currently powered by MongoDB, the most used nosql, and [5th](http://db-engines.com/en/ranking) most popular database solution in the world.
MongoDB comes with a powerful query language, and it allows us to easily accommodate blockchain changes thanks to schema flexibility.

With SteemData, you can query for any kind of information living on the STEEM blockchain, such as Accounts, Posts, Transactions, Blocks or any kind of Operations.


### Getting Started
I highly recommend [RoboMongo](https://robomongo.org/) as a GUI utility for exploring SteemData.


## Deployment

Python 3.5+, pip3, mongodb-org 

`$ pip3 install -r requirements.txt` 

### MongoDB

```
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
$ echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
$ sudo apt-get update
$ sudo apt-get install -y mongodb-org
$ service mongod status
$ mongo

> db.createUser({user:'steem',pwd:'steem',roles:['readWrite']})
```
Create a read-only user from createUser.mongo from mongodb shell when mongo first starts.


#### Blockchain db requires first entry 

```
db.Blockchain.insert({previous:"0000000000000000000000000000000000000000",timestamp:"2016-03-24 16:05:00",witness:"initminer",transaction_merkle_root:"0000000000000000000000000000000000000000",extensions:[],witness_signature: "204f8ad56a8f5cf722a02b035a61b500aa59b9519b2c33c77a80c0a714680a5a5a7a340d909d19996613c5e4ae92146b9add8a7a663eef37d837ef881477313043",transactions:[],block_id:"0000000109833ce528d5bbfb3f6225b39ee10086",signing_key:"STM8GC13uCZbP44HzMLV6zPZGwVQ8Nt4Kji8PapsPiNq1BK153XTX",transaction_ids:[],block_num: 1 })
```

#### Allow external connection to mongodb

`$nano /etc/mongod.conf`

comment out bindip

`#bindIp 127.0.0.1`

Database name

`export DB_NAME="SteemData"`

#### Run scraper

`screen -dmSL scraper python3 runner.py`



