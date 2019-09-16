
<style>
</style>

<template>
    <div class="pro-year-cont">
        <div id="proyeaelin"  ref="line"></div>
    </div>
</template>

<style scoped>
    .pro-year-cont {
        width: 100%;
        height: 100%;
        position: relative;
    }

    #proyeaelin {
        width: 100%;
        height: 100%;
        z-index:10;
    }
</style>

<script>
    import echarts from "echarts";

    export default {
        props: {
            toLeftBottomLineData: {
                type: Object,
                default: function() {
                    return {};
                }
            }
        },
        data() {
            return {
                timerId: 0
            };
        },
        watch: {
            toLeftBottomLineData: {
                handler(newval, oldval) {
                    this.drawLine();
                },
                deep: true
            }
        },
        mounted() {
            //this.drawLine()
        },
        methods: {
            handleResize() {
                echarts.init(this.$refs.line).resize();
            },
            async drawLine() {
                var chart = echarts.init(this.$refs.line);
                let _this = this;
                var option = {
                    // title: {
                    //   text: "发展趋势图",
                    //   textStyle: {
                    //     color: "#fff"
                    //   }
                    // },
                    tooltip: {
                        trigger: "axis"
                    },
                    legend: {
                        data: this.toLeftBottomLineData.lengendName,
                        top: 56,
                        textStyle: {
                            color: "#fff"
                        }
                    },
                    dataZoom: [
                        {
                            type: "slider",
                            show: false,
                            start: 1,
                            end: 100,
                            handleSize: 8
                        },
                        {
                            type: "inside",
                            start: 1,
                            end: 100
                        }
                        // {
                        //     type: 'slider',
                        //     show: true,
                        //     yAxisIndex: 0,
                        //     filterMode: 'empty',
                        //     width: 12,
                        //     height: '70%',
                        //     handleSize: 8,
                        //     showDataShadow: false,
                        //     left: '93%'
                        // }
                    ],
                    grid: {
                        top: "36%",
                        left: "3%",
                        right: "4%",
                        bottom: "6%",
                        containLabel: true
                    },
                    toolbox: {
                        right: 10,
                        feature: {
                            saveAsImage: {
                                title:'Save as a picture',
                                pixelRatio: 2,
                                backgroundColor: "transparent",
                                iconStyle:{
                                    // color:'#052C52',
                                    borderColor:'#052C52'
                                },
                            },
                            dataView: {
                                lang: ['DataView','Close'],
                                title:"DataView",
                                readOnly: true,
                                textColor: '#fff',
                                backgroundColor: '#09132B',
                                buttonColor: '#fff',
                                buttonTextColor: '#000',
                                iconStyle:{
                                    color:'#409EFF',
                                },
                                optionToContent: function(opt) {
                                    let tdHeads =
                                        '<td  style="padding: 0 10px ;font-Size:18px">年份</td>'; //表头
                                    let tdBodys = ""; //数据
                                    opt.series.forEach(ele => {
                                        tdHeads +=
                                            '<td  style="padding: 0 10px;font-Size:18px">' +
                                            ele.name +
                                            "</td>";
                                    });
                                    let table = `<table width='100%' border="1" style="border-collapse:collapse;text-align:center;color:#ccc; border:solid"><tbody><tr>${tdHeads} </tr>`;
                                    for (let j = 0; j < opt.series[0].data.length; j++) {
                                        tdBodys = `<td style="border:solid 1px">${
                                            opt.xAxis[0].data[j]
                                            }</td>`;
                                        for (let i = 0; i < opt.series.length; i++) {
                                            tdBodys += `<td style="border:solid 1px">${
                                                opt.series[i].data[j]
                                                }</td>`;
                                        }
                                        table += `<tr>${tdBodys}</tr>`;
                                    }
                                    table += "</tbody></table>";
                                    return table;
                                },
                                magicType: {title:{line:'Toggle to polyline graph',bar:'Switch to histogram'},type: ['line', 'bar']},
                            }
                        }
                    },
                    xAxis: {
                        type: "category",
                        boundaryGap: false,
                        data: this.toLeftBottomLineData.timeLineData,
                        splitLine: {
                            show: false
                        },
                        axisLine: {
                            lineStyle: {
                                color: "#fff"
                            }
                        }
                    },
                    yAxis: {
                        type: "value",
                        splitLine: {
                            show: false
                        },
                        axisLine: {
                            lineStyle: {
                                color: "#fff"
                            }
                        }
                    },
                    series: this.toLeftBottomLineData.seriesData
                };
                //清空画布
                chart.clear();
                // 使用刚指定的配置项和数据显示图表。
                chart.setOption(option);
                // 屏幕自适应
                this.timerId = setTimeout(function() {
                    window.addEventListener("resize", _this.handleResize);
                }, 200);
            }
        },

        beforeDestroy() {
            clearTimeout(this.timerId);
            window.removeEventListener("resize", this.handleResize);
        }
    };
</script>


