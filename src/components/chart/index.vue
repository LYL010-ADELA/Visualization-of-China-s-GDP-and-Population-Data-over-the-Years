<template>
    <div>
        <Echart id="chart" :options="option" height="6.5rem"></Echart>
    </div>
</template>
<script>
import Echart from '@/common/echart';


// GDP、增速、人口、名称、序号
import data from './chart.json';

const years = []
for (var i = 0; i < 21; i++) {
    years.push(i + 2000)
}

// 用于鼠标移动显示的提示信息
const schema = [
    { name: "city", index: 0, text: '省份' },
    { name: "amount", index: 1, text: 'GDP总量（亿元）' },
    { name: "speed", index: 2, text: 'GDP增速（%）' },
    { name: "population", index: 3, text: '人口（万人）' }

]

// 这里颜色是写死了的，也可以随机生成
const COLOR_ALL = [
    '#551A8B',
    '#483d8b',
    '#e06343',
    '#37a354',
    '#b55dba',
    '#b5bd48',
    '#8378EA',
    '#96BFFF',
    '#8696a7',
    '#656565',
    'rgb(144,59,28)',
]
for (var c = 0; c < 31 - 10; c++) {
    let R = Math.floor(Math.random() * 255);
    let G = Math.floor(Math.random() * 255);
    let B = Math.floor(Math.random() * 255);
    COLOR_ALL.push('rgb(' + R + ',' + G + ',' + B + ')')
}

var city_num = 31
var cities = []
for (var i = 0; i < city_num; i++) {
    cities.push(data[0][i][3])
}

var pieces = []
for (var i = 0; i < city_num; i++) {
    pieces.push({
        value: i,
        label: cities[i],
        color: COLOR_ALL[i]
    });
}

export default {
    name: "index",
    data() {
        var option = {
            baseOption: {
                timeline: {
                    axisType: 'category',
                    orient: 'vertical',
                    autoPlay: true,
                    inverse: true,
                    playInterval: 1000,
                    left: 30,
                    top: 20,
                    bottom: "26%",
                    width: 55,
                    height: null,
                    symbol: 'none',
                    checkpointStyle: {
                        borderWidth: 2
                    },
                    controlStyle: {
                        showNextBtn: false,
                        showPrevBtn: false
                    },
                    data: []
                },
                title: [
                    {
                        text: years[0],
                        textAlign: 'center',
                        left: '63%',
                        top: '55%',
                        textStyle: {
                            fontSize: 20
                        }
                    },
                ],
                tooltip: {
                    trigger: 'axis',
                    axisPointer: {
                        type: 'cross'
                    }
                },
                grid: {
                    left: '18%',
                    right: '10%',
                    top: "10%",
                    bottom: '30%'
                },
                xAxis: [
                    {
                        scale: true,
                        name: 'GDP总量\n（亿元）',
                        min: 100,
                        max: 120000,
                    }
                ],
                yAxis: [
                    {
                        scale: true,
                        name: 'GDP增速',
                        min: -6,
                        max: 30
                    }
                ],
                visualMap: [
                {
                    type: 'piecewise',
                    bottom: '18%',
                    left:"center",
                    show: true,
                    orient:"horizontal", //图例排列方向
                    right: 0,
                    dimension: -1, // dimension是最后一个维度被映射，即 index序号
                    seriesIndex: "0",
                    outRange: {
                        color: '#656565',
                    },
                    pieces: pieces.slice(0, 8)
                },
                {
                    type: 'piecewise',
                    bottom: "12%",
                    show: true,
                    orient:"horizontal", //图例排列方向
                    left:"center",
                    dimension: -1, // dimension是最后一个维度被映射，即 index序号
                    seriesIndex: "0",
                    outRange: {
                        color: '#656565',
                    },
                    pieces: pieces.slice(8,17)
                },
                {
                    type: 'piecewise',
                    bottom: "6%",
                    show: true,
                    orient:"horizontal", //图例排列方向
                    left:"center",
                    dimension: -1, // dimension是最后一个维度被映射，即 index序号
                    seriesIndex: "0",
                    outRange: {
                        color: '#656565',
                    },
                    pieces: pieces.slice(17,25)
                },
                {
                    type: 'piecewise',
                    bottom: "0%",
                    show: true,
                    orient:"horizontal", //图例排列方向
                    left:"center",
                    dimension: -1, // dimension是最后一个维度被映射，即 index序号
                    seriesIndex: "0",
                    outRange: {
                        color: '#656565',
                    },
                    pieces: pieces.slice(25,31)
                },
                {
                    type: 'piecewise',
                    top: 'middle',
                    show: false,
                    orient:"vertical", //图例排列方向
                    right: "20%",
                    dimension: -1, // dimension是最后一个维度被映射，即 index序号
                    seriesIndex: "0",
                    outRange: {
                        color: '#656565',
                    },
                    pieces: pieces
                },
                ],
                // 以下是鼠标移到圈圈显示的内容，注意序号
                tooltip: {
                    backgroundColor: 'rgba(255,255,255,0.7)',
                    formatter: function (param) {
                        var value = param.value;
                        return schema[0].text + '：' + value[3] + '<br>'
                            + schema[1].text + '：' + value[0] + '<br>'
                            + schema[2].text + '：' + value[1] + '<br>'
                            + schema[3].text + '：' + value[2] + '<br>';
                    }
                },
                series: [
                    {
                        type: 'scatter',
                        symbolSize: function (data) {
                            return data[2] / 100 // 这里返回圆圈大小
                        },
                        itemStyle: { // 圈圈的颜色
                            opacity: 0.8,
                            color: function (COLOR_ALL) {
                                return COLOR_ALL
                            }
                        },
                        data: data[0],
                    }
                ],
                animationDurationUpdate: 1000,
                animationEasingUpdate: 'quinticInOut'
            },
            options: []
        };

        for (var n = 0; n < data.length; n++) {
            option.baseOption.timeline.data.push(years[n]);
            option.options.push({
                title: {
                    show: true,
                    text: years[n] + ' '
                },
                series: {
                    name: years[n],
                    type: 'scatter',
                    itemStyle: {
                        opacity: 0.8,
                        color: function (COLOR_ALL) {
                            return COLOR_ALL
                        }
                    },
                    data: data[n],
                    symbolSize: function (data) {
                        // return 10
                        if (data[2] / 120<10){
                            return 10
                        }
                        return data[2] / 120 // 这里返回圆圈大小
                    },
                }
            });
        }
        return { option };
    },
    components: {
        Echart,
    },
    methods: {
    }
}
</script>