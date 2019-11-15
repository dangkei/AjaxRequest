# AjaxRequest
写这个javascript对象的目的主要是为了封装一下前端js调用webservice的方法
##方法：
	###javascript 调用domino代理的方法。
	this.ajaxCallAgent = function(agentParam)；
	###javascript 调用Webservice的方法。
	this.CallWebService =function (serviceParam)

	return this;
}

/*
* 打包为参数，目的是在重复调用时，一次初始化固定的数据
* 变化的参数在调用前初始化不变的默认初始化就可以了
*/
var serviceParam ={}

/*
* 调用代理参数少， 没有action
* 传递参数
*/
var agentParam ={}




