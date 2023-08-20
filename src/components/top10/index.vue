<template>
    <div>
        <Echart
                id="top10"
                :options="options"
                height="5rem"
        ></Echart>
    </div>
</template>
<script>
    import Echart from '@/common/echart';
    import gdp_data from './gdp.json';
    import pop_data from './pop.json';
    import rate_data from './gdp_rate.json';
    export default {
        name: "index",
        props:{country: {   //此处为接收父类传递的参数，进行点击切换数据，默认值为北京
            type: String,
            default:'北京市',
            required: true,
        }
        },
        watch:{  //监听country值的变化
            country:{    
                handler(newValue,oldValue){
                this.country=newValue;
                this.initChart(); }
            }
        },
        data() {
            return {
                options: {
                    color:[
                        '#67a1e5','#50e3c2','#D0648A'
                    ],
                    grid: {
                        left: '18%',
                        bottom:'10%'
                    },
                    tooltip: {
                        trigger: 'axis',
                        axisPointer: {
                            type: 'cross'
                        }
                    },
                    xAxis: [
                        {   
                            type: 'category',
                            axisTick: {
                                alignWithLabel: true,
                            },
                            axisLabel:{
                                textStyle:{
                                    color:'#00000'
                                }
                            },
                            data: ['2000', '2001', '2002', '2003', '2004', '2005', '2006', '2007', '2008', '2009',
                                   '2010', '2011', '2012', '2013', '2014', '2015', '2016', '2017', '2018', '2019',
                                   '2020']
                        }
                    ],
                    yAxis: [
                        {
                            type: 'value',
                            name: 'GDP总量\n（亿元）',
                            min: 0,
                            max: 38000,
                            position: 'left',
                            axisLine: {
                                show: true,
                                lineStyle: {
                                    color: '#67a1e5'
                                }
                            },
                            axisLabel: {
                                formatter: '{value}'
                            },
                            splitLine: {
                                show: false
                            }
                        },
                        {
                            type: 'value',
                            name: '常住人口\n（万人）',
                            min: 0,
                            max: 9000,
                            position: 'left',
                            offset: 80,
                            axisLine: {
                                show: true,
                                lineStyle: {
                                    color: '#50e3c2'
                                }
                            },
                            axisLabel: {
                                formatter: '{value}'
                            },
                            splitLine: {
                                show: false
                            }
                        },
                        {
                            type: 'value',
                            name: 'GDP增速',
                            min: -20,
                            max: 70,
                            position: 'right',
                            axisLine: {
                                show: true,
                                lineStyle: {
                                    color: '#D0648A'
                                }
                            },
                            axisLabel: {
                                formatter: '{value}%'
                            },
                            splitLine: {
                                show: false
                            }
                        }
                    ],
                    series: [
                        {
                            name: 'GDP总量（亿元）',
                            type: 'bar',
                            data: [3277.8, 3861.5, 4525.7, 5267.2, 4283.3, 7149.8, 8387.0,
                                   10425.5, 11813.1, 12900.9, 14964.0, 16000.4, 17879.4, 19800.8,
                                   21330.8, 23014.59, 24899.26, 28000.3, 30320.0, 35371.28, 36102.6]
                        },
                        {
                            name: '常住人口（万人）',
                            type: 'bar',
                            yAxisIndex: 1,
                            data: [1207,1217,1223,1404,1417,1426,1434,1442,1451,1461,1451,1459,
                                   1976,1985,1994,2012,2021,2029,2037,2044,2052]
                        },
                        {
                            name: 'GDP增速',
                            type: 'line',
                            yAxisIndex: 2,
                            data: [18.77,17.81,17.2,16.38,-18.68,66.92,17.3,24.31,13.31,9.21,15.99,6.93,
                                   11.74,10.75,7.73,7.89,8.19,12.45,8.28,16.66,2.07]
                        }
                    ]
                },
            };
        },
        components: {
            Echart,
        },
        methods: {
            initChart(){
                Array.prototype.max = function(){ 
                return Math.max.apply({},this) 
                } 
                Array.prototype.min = function(){ 
                return Math.min.apply({},this) 
                } 
                
                    this.options =  {
                        color:[
                            '#67a1e5','#50e3c2','#D0648A'
                        ],
                        grid: {
                            left: '18%',
                            bottom:'10%'
                        },
                        tooltip: {
                            trigger: 'axis',
                            axisPointer: {
                                type: 'cross'
                            }
                        },
                        xAxis: [
                            {
                                type: 'category',
                                axisTick: {
                                    alignWithLabel: true,
                                },
                                axisLabel:{
                                    textStyle:{
                                        color:'#00000'
                                    }
                                },
                                data: ['2000', '2001', '2002', '2003', '2004', '2005', '2006', '2007', '2008', '2009',
                                    '2010', '2011', '2012', '2013', '2014', '2015', '2016', '2017', '2018', '2019',
                                    '2020']
                            }
                        ],
                        yAxis: [
                            {
                                type: 'value',
                                name: 'GDP总量\n（亿元）',
                                min: 0,
                                max: Math.ceil(gdp_data[this.country].max()/10000)*10000,
                                position: 'left',
                                axisLine: {
                                    show: true,
                                    lineStyle: {
                                        color: '#67a1e5'
                                    }
                                },
                                axisLabel: {
                                    formatter: '{value}'
                                },
                                splitLine: {
                                    show: false
                                }
                            },
                            {
                                type: 'value',
                                name: '常住人口\n（万人）',
                                min: Math.floor(pop_data[this.country].min()/1000)*1000,
                                max: Math.ceil(pop_data[this.country].max()/1000)*1000,
                                position: 'left',
                                offset: 80,
                                axisLine: {
                                    show: true,
                                    lineStyle: {
                                        color: '#50e3c2'
                                    }
                                },
                                axisLabel: {
                                    formatter: '{value}'
                                },
                                splitLine: {
                                    show: false
                                }
                            },
                            {
                                type: 'value',
                                name: 'GDP增速',
                                min: Math.floor(rate_data[this.country].min()/10)*10,
                                max: Math.ceil(rate_data[this.country].max()/10)*10,
                                position: 'right',
                                axisLine: {
                                    show: true,
                                    lineStyle: {
                                        color: '#D0648A'
                                    }
                                },
                                axisLabel: {
                                    formatter: '{value}%'
                                },
                                splitLine: {
                                    show: false
                                }
                            }
                        ],
                        series: [
                            {
                                name: 'GDP总量（亿元）',
                                type: 'bar',
                                data: gdp_data[this.country]
                                // [3277.8, 3861.5, 4525.7, 5267.2, 4283.3, 7149.8, 8387.0,
                                //     10425.5, 11813.1, 12900.9, 14964.0, 16000.4, 17879.4, 19800.8,
                                //     21330.8, 23014.59, 24899.26, 28000.3, 30320.0, 35371.28, 36102.6]
                            },
                            {
                                name: '常住人口（万人）',
                                type: 'bar',
                                yAxisIndex: 1,
                                data: pop_data[this.country]
                            },
                            {
                                name: 'GDP增速',
                                type: 'line',
                                yAxisIndex: 2,
                                data: rate_data[this.country]
                            }
                        ]

                }
                

        }
        },
        mounted() {
            this.initChart();
        },
    }
</script>