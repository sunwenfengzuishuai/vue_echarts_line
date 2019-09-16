# vue_echarts_line
#基于vue和echarts的折线图
#功能：
	可展示多条折现
	可自适应大小
#注意：
	x轴和y轴均为自己定义，请确保年份和数据一一对应
数据格式：
toLeftBottomLineData:{
lengendName:["总产量","养殖产品小计","海水养殖","淡水养殖"],
seriesData:[
{name:"总产量",type:"line",data:[1,2,3,4,5,6,7,8,9,10]},
{name:"养殖产品小计",type:"line",data:[1,2,3,4,5,6,7,8,9,10]},
{name:"海水养殖",type:"line",data:[1,2,3,4,5,6,7,8,9,10]},
{name:"淡水养殖",type:"line",data:[1,2,3,4,5,6,7,8,9,10]},
],
timeLineData:[2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017],
}
