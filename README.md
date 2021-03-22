# Toefl-Scanner-Pro

TOEFL NEEA 托福空余考位自动扫描脚本，支持自定义城市。



## 🤖️使用方法

- 登录NEEA TOEFL界面

- 点击「考位查询」

![search](image/search.png)

- 打开检查界面，点击Console界面

![check](image/check.png)

- 在Console栏中粘贴以下代码，空余考位将直接显示在Console栏
![console](image/code.png)

🚀**Scanner()默认搜索全部城市，如果需要搜索选定城市，请将最下方Scanner()中的【true】改为【false】**

```javascript
//在这里加入你需要选择的城市。
var city_choose = ["武汉","郑州","长沙"]

function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms))
}

async function Scanner(city_choose, all) {
	//定位所需要的元素
	city = document.getElementById('centerProvinceCity')
	day = document.getElementById("testDays")
	btn_query = document.getElementById("btnQuerySeat")
	num_city = 0

	//循环查找
	for (i = 1; i < city.options.length; ++i) {
		for(n = 0; n < city_choose.length; n++){
			if(city_choose[n]==city.options[i].text||all==true){ //如果找到了指定的城市
				city.options[i].selected = true
    			for (j = 1; j < 18; ++j) {
        			day.options[j].selected = true
        			btn_query.click()
        			await sleep(1000)
        			tables = document.getElementsByClassName("table table-bordered table-striped")
        			if (tables.length == 1) {
        		    	tb = tables[0]
        		    	for (row = 2; row < tb.rows.length; ++row) {
        		        	if (tb.rows[row].cells[3].innerText == "有名额") {
        		            	console.log(
        		                	city.options[i].innerText,
        		                	day.options[j].innerText,
        		                	tb.rows[row].cells[1].innerText)
}}}}}}}}

//搜索指定城市
//Scanner(city_choose, false)

//搜索全部城市
Scanner(city_choose, true)

```

- 输出结果

![console](image/result.png)

## 🎉鸣谢

感谢[NEEA_TOEFL_AUTOMATOR](https://github.com/Augustpan/NEEA_TOEFL_AUTOMATOR)的启发，本项目在此基础上新增了城市选择功能。

