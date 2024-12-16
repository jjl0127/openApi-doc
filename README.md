# 接口文档
1、测试环境地址: http://ie-uocs-out.sit.sf-express.com:8000/	
2、生产环境地址：https://ie-uocs-lvs.sf-express.com/

-----------------------------------------------------------------------------------------------------------

#### 接口：外部用户鉴权接口 
*更新时间： 2024-12-13*
> ***对接平台的所有接口，首先应通过该接口进行身份鉴权认证，认证通过以后系统就返回接口token, 后续所有接口均需要带上在请求头上带上token***

- 接口地址：/apis-auth/login/auth
- 请求方法：POST
- 请求参数

    |字段名			|属性	    |类型	|是否必传	|说明                                            |
    |---------------|-----------|-------|-----------|------------------------------------------------|
    |appKey			|		    |String	|是			|appKey （固定值 IE-UOCS-OUT）                   |
    |appSecret		|		    |String	|是			|appKey 秘钥 （固定值fykj12345678）              |
    |deviceId		|		    |String	|是			|设备ID                                          |
    |hostName		|		    |String	|是			|设备名                                          |
    |requestId		|		    |String	|否			|请求ID                                          |
    |ip		  		|		    |String	|是			|IP地址                                          |
    |userId			|		    |String	|是			|用户账号（丰翼分配 xcy0001）                    |
    |password		|		    |String	|是			|密码（丰翼分配79323c441a34b5599aec5c1f56eda196）|
- 请求响应参数

    |字段名	 		|属性	    |类型	|是否必传	|说明	                                        |
    |---------------|-----------|-------|-----------|-----------------------------------------------|
    |requestId		|			|String	|是			|请求唯一标识                                   |
    |success		|			|Boolean|是			|true:成功 false:失败                           |
    |errorCode		|			|String	|否			|请求错误码                                     |
    |errorMessage	|			|String	|否			|请求错误信息                                   |
    |date		   	| 			|String	|是			|当前处理日期                                   |
    |version		|			|String	|否			|当前版本信息                                   |
    |obj			|			|Object	|否			|业务结果类                                     |
    |				|userId		|String	|是			|用户账号                                       |
    |				|token		|String	|是			|用户token 有效期7天                            |
		
- 请求示例
    ```json
    {
       "appKey":"IE-UOCS-OUT",
        "appSecret": "fykj12345678",
        "deviceId": "00:FF:16:4B:63:57",
        "hostName": "SF0001304522C",
        "requestId": "123456789",
        "ip": "192.168.255.10",
        "userId": "fc0001",
        "password": "8bb2423a0e1c4d0a"
    }
    ```
- 响应示例：
    ```json
    {
        "requestId":"xxxxxxx",
        "success":true,
        "business":null,
        "errorCode":null,
        "errorMessage":null,
        "date":null,
        "version":null,
        "obj":{
    		"userId":"fc0001",
            "token":"DEF_A3_537bc42380b6dafb5f480d9eaa4da0a91684302908599"
        }
    }
    ```



-----------------------------------------------------------------------------------------------------------

#### 接口：查询运力是否可用接口 
*更新时间： 2024-12-13*
> ***丰翼在该地区范围内是否有无人机承运运力***

- 接口地址：/uocs-tes/waybill/api/carrierWaybill
- 请求方法：POST
- 请求参数

    |字段名			|属性	    |类型	|是否必传	|说明                                            |
    |---------------|-----------|-------|-----------|------------------------------------------------|
	|devCode		|			|String	|是			|企业账号                                        |
	|gpsType		|			|Int	|是			|默认坐标系类型 1：WGS－84                       |
	|senderLon		|			|String	|是			|寄件人地址经度                                  |
	|senderLat		|			|String	|是			|寄件人地址纬度                                  |
	|goodsType		|			|Int	|是			|货物类型 默认传 10快递                          |
	|goodsWeight	|			|Int	|是			|货物重量(g) 默认传 2000                         |
	|receiverLon	|			|String	|是			|收件人地址经度                                  |
	|receiverLat	|			|String	|是			|收件人地址纬度                                  |

	
- 请求响应参数

    |字段名	 		|属性	    |类型	|是否必传	|说明	                                        |
    |---------------|-----------|-------|-----------|-----------------------------------------------|
	|requestId		|			|String	|是			|请求唯一标识                                   |
	|success		|			|Boolean|是			|true:成功 false:失败                           |
	|errorCode		|			|String	|否			|请求错误码                                     |
	|errorMessage	|			|String	|否			|请求错误信息(不可承运原因)                     |
	|date			|			|String	|是			|当前处理日期                                   |
	|version		|			|String	|否			|当前版本信息                                   |
	|obj			|			|T		|否			|业务结果类                                     |
	|				|gpsType	|Int	|是			|默认坐标系类型 1：WGS－84                      |
	|				|takeoffCode|String	|是			|起飞场航站代码                                 |
	|				|takeoffLon	|String	|是			|起飞场航站经度                                 |
	|				|takeoffLat	|String	|是			|起飞场航站纬度                                 |
	|				|takeoffName|String	|是			|起飞场航站名称                                 |
	|				|takeoffAddr|String	|是			|起飞场航站地址                                 |
	|				|takeoffTel	|String	|是			|起飞场航站手机                                 |
	|				|landingCode|String	|是			|降落场航站代码                                 |
	|				|landingLon	|String	|是			|降落场航站经度                                 |
	|				|landingLat	|String	|是			|降落场航站纬度                                 |
	|				|landingName|String	|是			|降落场航站名称                                 |
	|				|landingAddr|String	|是			|降落场航站地址                                 |
	|				|landingTel	|String	|是			|降落场航站手机                                 |
	|				|flightTime	|Int	|是			|预计飞行时长(min)                              |

		
- 请求示例
    ```json
    {
        "devCode": "tc123456",
    	"gpsType": 1,
    	"senderLon": "113.9311883",
    	"senderLat": "22.5616979",
    	"goodsType": 1,
    	"goodsWeight": 8000,
    	"receiverLon": "114.0267861",
    	"receiverLat": "22.5353805"
    }
    ```
- 响应示例：
    ```json
	{
    	"requestId": "123456789987",
    	"success": true,
    	"business": null,
    	"errorCode": null,
    	"errorMessage": null,
    	"params": null,
    	"date": "2022-11-23 16:32:58",
    	"version": "1.0",
    	"obj": {
    		"goodsType": 1,
            "takeoffCode":"CN001",
    		"takeoffLon":"114.1234567",
    		"takeoffLat":"26.1234567",
    		"takeoffName":"五和起降场A",
    		"takeoffAddr":"龙岗五和",
    		"landingCode":"CN001",
    		"landingLon":"114.1234567",
    		"landingLat":"26.1234567",
    		"landingName":"五和起降场A",
    		"landingAddr":"龙岗五和",
    		"flightTime":14
    	}
    }
    ```
	
-----------------------------------------------------------------------------------------------------------

#### 接口：创建运单的接口 
*更新时间： 2024-12-13*
> ***在查询到丰翼无人机有承运运力之后，通过该接口向丰翼无人机下订单***

- 接口地址：/uocs-tes/waybill/api/createWaybill
- 请求方法：POST
- 请求参数

    |字段名			|属性	    |类型	|是否必传	|说明                                            |
    |---------------|-----------|-------|-----------|------------------------------------------------|
	|devCode		|			|String	|是			|企业账号                                        |
	|pushTime		|			|String	|是			|推单时间 2024-10-21 17:00:00                    |
	|useCab		    |			|Int	|是			|是否使用接驳柜寄件 1：否；2：是  默认:1         |
	|boxCode		|			|String	|否			|接驳柜编码 useCab为2 必填                       |
	|bizCode		|			|String	|是			|客户单号                                        |
	|gpsType		|			|Int	|是			|默认坐标系 1：WGS－84                           |
	|senderCode		|			|String	|是			|寄件人航站编码                                  |
	|senderLon		|			|String	|是			|寄件人地址经度                                  |
	|senderLat		|			|String	|是			|寄件人地址纬度                                  |
	|senderAddr		|			|String	|是			|寄件人详细地址                                  |
	|senderTel		|			|String	|是			|寄件人电话                                      |
	|senderName		|			|String	|是			|寄件人姓名                                      |
	|goodsType		|			|Int	|是			|货物类型 默认传 10快递                          |
	|goodsWeight	|			|Int	|是			|货物重量(g) 默认传 2000                         |
	|receiverCode	|			|String	|是			|收件人航站编码                                  |
	|receiverLon	|			|String	|是			|收件人地址经度                                  |
	|receiverLat	|			|String	|是			|收件人地址纬度                                  |
	|receiverAddr	|			|String	|是			|收件人详细地址                                  |
	|receiverTel	|			|String	|是			|收件人电话                                      |
	|receiverName	|			|String	|是			|收件人姓名                                      |
	|amount			|			|Double	|否			|订单金额(元)                                    |
	|goodsCode		|			|String	|否			|货物编码 多个，隔开                             |
	|remark			|			|String	|否			|备注                                            |

	
- 请求响应参数

    |字段名	 		|属性	    |类型	|是否必传	|说明	                                        |
    |---------------|-----------|-------|-----------|-----------------------------------------------|
	|requestId		|			|String	|是			|请求唯一标识                                   |
	|success		|			|Boolean|是			|true:成功 false:失败                           |
	|errorCode		|			|String	|否			|请求错误码                                     |
	|errorMessage	|			|String	|否			|请求错误信息(不可承运原因)                     |
	|date			|			|String	|是			|当前处理日期                                   |
	|version		|			|String	|否			|当前版本信息                                   |
	|obj			|			|T		|否			|业务结果类                                     |
	|				|fyCode		|String	|是			|丰翼编号	                     				|
	|				|sendCode	|String	|是			|寄件码(起飞场为丰巢柜时                        |

		
- 请求示例
    ```json
    {
        "devCode": "tc123456",
        "pushTime": "2024-10-08 14:07:11",
        "useCab": 1,
        "bizCode": "tc123456899",
        "senderCode": "CN001",
        "receiverCode": "CN0023",
        "gpsType": 1,
        "senderLon": "114.1234567",
        "senderLat": "26.1234567",
        "senderAddr": "深圳市",
        "senderTel": "13699847593",
        "senderName": "jacky",
        "goodsType": 1,
        "goodsWeight": 2000,
        "receiverLon": "114.1234567",
        "receiverLat": "26.1234567",
        "receiverAddr": "深圳市",
        "receiverTel": "13699847593",
        "receiverName": "jacky",
        "amount": 20.5,
        "remark": null
	}
    ```
- 响应示例：
    ```json
    {
		"requestId": "123456789987",
		"success": true,
		"business": null,
		"errorCode": null,
		"errorMessage": null,
		"params": null,
		"date": "2022-11-23 16:32:58",
		"version": "1.0",
		"obj": {
			"fyCode":"C123456",
			"sendCode":"65875"
		}
	}
    ```