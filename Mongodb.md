# MongoDB

使用update对表中的orderNo为1字段下的userInfo数组对象下的cardNo等于123456789这个对象中的timeline字段进行日志更新

```javascript
{
	"_id" : ObjectId("59546c5051eb690367d457fa"),
	"orderNo" : "o111111"
	"userInfo" : [
		{
			"name" : "o1111",
			"cardNo" : "123456789",
			"logs" : [
				"2017-08-09 timeline ...",
        			"2017-08-10 timeline1 ...",
			]
		},
		{
			"name" : "o1111",
			"cardNo": "987654321",
			"logs": [
				"2017-08-09 timeline ...",
			]
		},
		...
	]
},
...
}
```
在Nodejs中操作，可以使用$push在找到logs数组后依次添加日志信息
```javascript
let condition = {"orderNo":"o111111","passengers.passengerIds":"123456789"}

let update = {
	$push: {
		"passengers.$.logs": "2017-08-10 timeline1 ..."
	}
}
db.collections.findOneAndUpdate(condition, update, { returnOriginal: false })
```
也可以使用$set 对某个字段进行更新
```javascript
let condition = {"orderNo":"o111111","passengers.passengerIds":"123456789"}

let update = {
	$set: {"passengers.$.status": "已更新"}
}

DB.orderColl.updateOne({condition},update)
```