# binbin03
<!DOCTYPE>
<html>
  <head>
    <meta charset="utf-8">
    <title>IFE JavaScript Task 01</title>
  </head>
<body>

  <ul id="source">
    <li>北京空气质量：<b>90</b></li>
    <li>上海空气质量：<b>70</b></li>
    <li>天津空气质量：<b>80</b></li>
    <li>广州空气质量：<b>50</b></li>
    <li>深圳空气质量：<b>40</b></li>
    <li>福州空气质量：<b>32</b></li>
    <li>成都空气质量：<b>90</b></li>
  </ul>

  <ul id="resort">
    <!-- 
    <li>第一名：北京空气质量：<b>90</b></li>
    <li>第二名：北京空气质量：<b>90</b></li>
    <li>第三名：北京空气质量：<b>90</b></li>
     -->

  </ul>

  <button id="sort-btn">排序</button>

<script type="text/javascript">

/**
 * getData方法
 * 读取id为source的列表，获取其中城市名字及城市对应的空气质量
 * 返回一个数组，格式见函数中示例
 */
function getData() {
  /*
  coding here
  */

  /*
  data = [
    ["北京", 90],
    ["北京", 90]
    ……
  ]
  */
var data = new Array();
var a =document.getElementById("source").getElementsByTagName("li");
for (var i = 0; i < a.length; i++) {
data[i]=a[i].innerHTML;
}
for (i = 0; i < a.length; i++) {

data[i]=[data[i].substring(0,2),data[i].replace(/[^0-9]/ig,"")];
}
  return data;
}


/**
 * sortAqiData
 * 按空气质量对data进行从小到大的排序
 * 返回一个排序后的数组
 */
function sortAqiData(data) {
function compare(value1, value2)
{
if (value1[1]<value2[1]) {
  return -1;
} else return 1;
}

return data.sort(compare);
}

/**
 * render
 * 将排好序的城市及空气质量指数，输出显示到id位resort的列表中
 * 格式见ul中的注释的部分
 */
function render(data) {
for (var i = 0; i < data.length; i++) {
var li = document.createElement("li");
document.getElementById("resort").appendChild(li);
li.innerHTML = "第" + i + "名：" + data[i][0] +"空气质量：" +data[i][1];
}
}

function btnHandle() {
  var aqiData = getData();
aqiData = sortAqiData(aqiData);
render(aqiData);
}

function init() {

  // 在这下面给sort-btn绑定一个点击事件，点击时触发btnHandle函数
  var EventUtil={
  
   addHandler:function(element,type,handler){ 
      if(element.addEventListener){ 
         element.addEventListener(type,handler,false);  
      }else if(element.attachEvent){                   
         element.attachEvent("on"+type,handler);
      }else{
         element["on"+type]=handler;       
      }
   },
    getEvent:function(event){ 
      return event?event:window.event;
   }
 };

EventUtil.addHandler(document.getElementById("sort-btn"),"click",function(event){
event = EventUtil.getEvent(event);
btnHandle();
 });
}

init();

</script>
</body>
</html>
