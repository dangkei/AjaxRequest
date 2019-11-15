# AjaxRequest
写这个javascript对象的目的主要是为了封装一下前端js调用webservice的方法

##
var AjaxRequest = function(){
	//返回处理结果的回调函数
	this.agentCallBack = {};
	//javascript 调用domino代理的方法。
	this.ajaxCallAgent = function(url, jsondata,callBack){
		me.agentCallBack = callBack;
		$.ajax({
	　　　　type: "POST",
	　　　　url: url ,
	　　　　data: jsondata,
	　　　　beforeSend: function(request) {
			 //request.setRequestHeader("User-Agent","Apache-HttpClient/4.1.1 (java 1.5)");
	　　　　},
	　　　　success: this.agentCallBack,
	　　　　error: function(request, errorInfo) {
	　　　　　　alert("agent call failed, please contact your administrator.",errorInfo); // alert("errorInfo = "+errorInfo);
	　　　　} 
	　　});
	};

	//返回处理结果的回调函数
	this.serviceCallBack = {};
	//调用WebService方法
	//url：请求的url
	//soapdata：提交的xml数据
	//soapation webservice里的方法
	this.CallWebService =function (serviceParam){
		this.serviceCallBack = serviceParam.callBack;
	　　$.ajax({
	　　　　type: "POST",
	　　　　url: serviceParam.url ,
	　　　　data: serviceParam.soapdata,
	　　　　beforeSend: function(request) {
	　　　　　　request.setRequestHeader("Content-Type", "text/xml; charset=gbk"); //
	　　　　　　request.setRequestHeader("SOAPAction", serviceParam.soapaction);
	　　　　},
	　　　　success: this.serviceCallBack,
	　　　　error: function(request, errorInfo) {
	　　　　　　alert("invoke webservice failed, please contact your administrator."); 
	　　　　} 
	　　});
	}

	return this;
}

/*
* 打包为参数，目的是在重复调用时，一次初始化固定的数据
* 变化的参数在调用前初始化不变的默认初始化就可以了
*/
var serviceParam =function(){
	this.dbPath = $("[name=dbPath]").val();
	this.url = "/"+this.dbPath+ "/wsPurchaseOrder?OpenWebService";			//默认初始化参数
	this.ordernumber = $("[name=fldCgddbh]").val();
	this.soapaction = {};								//调用前初始化， 需要new 一个参数对象
	this.callback = {};
	this.soapdata = '<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:DefaultNamespace">'+
   			'<soapenv:Header/><soapenv:Body><urn:orderNumber>'+this.ordernumber+'</urn:orderNumber></soapenv:Body></soapenv:Envelope>';
	return this;
};

/*
* 调用代理参数少， 没有action
* 传递参数
*/
var agentParam =function(){
	this.dbPath = $("[name=dbPath]").val();
	this.url = "/"+this.dbPath+ "/agent?openagent";							//默认初始化参数		
	this.callback = {};										//调用前初始化， 需要new 一个参数对象
	this.jsondata = {};										//{ordernumber：ordernumber}
	return this;
};




