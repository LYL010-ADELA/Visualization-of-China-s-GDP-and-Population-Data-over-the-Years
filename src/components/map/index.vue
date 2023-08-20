<template>
    <div class="echart" ref="mapRef" id="map"></div>
</template>

<script>
    import chinaJson from './china.json'
    import resizeMixins from '@/utils/resizeMixins'
    import 'echarts/lib/chart/scatter'
    import gdp2020 from './gdp_2020.json'
    import lines_data from './lines_data.json'
    import link_coordinate from './link_coordinate_new.json'

    var cityName = '北京市'
    export default {
        name: "index",
        mixins: [resizeMixins],
        data(){
            return{
                data: gdp2020,
                chart:null,
            }
        },
        watch: {
            options: {
                handler (options) {
                    // 设置true清空echart缓存
                    this.chart.setOption(options, true)
                },
                deep: true
            }
        },
        mounted() {
            this.initChart();
            // this.handleMapRandomSelect(); //随机选中区域
        },
        beforeDestroy() {
            if (this.timer) {clearInterval(this.intervalId);}
        },
        methods: {
            initChart() {
                let that = this;
                this.chart = this.$echarts.init(document.getElementById('map'), 'shine');
                this.$echarts.registerMap("china", chinaJson);
                var lineseries = [];
                lineseries.push({
                    name: cityName,
                    type: 'lines',
                    zlevel: 1,
                    show: true,
                    effect: {
                        show: true,
                        period: 4, // 特效动画的时间
                        symbol: 'arrow',
                        trailLength: 0.6, // 特效尾迹的长度。取从 0 到 1 的值，默认为 0.2，数值越大尾迹越长
                        color: '#fff',
                        // symbol: planePath, // 特效图形的标记
                        symbolSize: 6
                    },
                    tooltip: {
                        show: true, // 是否显示
                        trigger: 'item', // 触发类型  'item'图形触发：散点图，饼图等无类目轴的图表中使用； 'axis'坐标轴触发；'none'：什么都不触发。
                        // backgroundColor: 'rgba(50,50,50,0.7)', // 提示框浮层的背景颜色。
                        // borderColor: '#fff', // 提示框浮层的边框颜色。
                        borderWidth: 0, // 提示框浮层的边框宽。
                        // padding: 5, // 提示框浮层内边距，
                        // textStyle: { // 提示框浮层的文本样式。
                        //     color: '#fff',
                        //     fontStyle: 'normal',
                        //     fontWeight: 'normal',
                        //     fontFamily: 'sans-serif',
                        //     fontSize: 14,
                        // },
                        // extraCssText: 'box-shadow: 0 0 3px rgba(0, 0, 0, 0.3);', // 额外附加到浮层的 css 样式
                        confine: false, // 是否将 tooltip 框限制在图表的区域内。
                        // formatter: '{b} 的成绩是 {c}'
                        formatter: function(arg) {
                            return '从'+arg.data.fromName + '到' + arg.data.toName + '<br/>的迁徙指数为:<br/>'+ arg.data.value
                        }
                    },
                    lineStyle: {
                        normal: {
                            color: function(arg){
                                var fromName = arg.data.fromName
                                if (fromName == cityName){
                                    return '#CD5C5C'
                                }
                                return '#3f4b51'},
                            width:  2.5,
                            opacity: 0.2,
                            curveness: 0.2
                        }
                    },
                    data: lines_data[cityName]
                },
                {
                    name: cityName+'2',
                    type: 'effectScatter',      // 带有涟漪特效的散点图，起到视觉突出的效果
                    coordinateSystem: 'geo',    // 该系列使用的坐标系指定为地理坐标系
                    zlevel: 2,
                    rippleEffect: {
                        brushType: 'stroke'     // 波纹的绘制方式
                    },
                    label: {
                        normal: {
                            show: true,
                            position: 'left',  // 地区名称标签显示位置
                            formatter: '{b}'    // 格式化显示标签，b指的是系列的名称
                        }
                    },
                    symbolSize: function (data) {
                        if(data[2]==1){
                            return 6
                        }
                        return 3;      // 目的地涟漪特效的大小
                    },
                    itemStyle: {
                        normal: {
                            color: function (val) {
                                if(val.data.name == cityName){
                                    return '#FFA500'
                                }
                                return 'MidnightBlue'}
                        }
                    },
                    // 解析：item[1] ==> BJData：[[{name:'北京'}, {name:'上海',value:95}],...]
                    data: link_coordinate[cityName]
                },
                );
                // 指定图表的配置项和数据
                let options = {
                    title: {
                        text: '2020年中国省级GDP总量及热门迁徙路线图',
                        subtext: '国家统计局、高德地图',
                        textStyle:{
                            color:'#377ee5'
                        },
                        subtextStyle:{
                            color:'#c7d5d9'
                        }
                    },
                    tooltip: {
                        textStyle: {
                            fontSize: '14px',
                        },
                        formatter: function(data){
                            if(!isNaN(data.value)){
                                return data.name+"<br/>"+data.value+"亿元";
                            }else{
                                return data.name
                            }
                        }
                    },
                    geo:{
                        type: "map",
                        roam: false, //设置能否移动和缩放
                        map: "china",
                        itemStyle: {
                            areaColor: "LightGrey",
                            borderColor: "#739af5",
                            borderWidth: 1
                        },
                        emphasis: {
                            label: {
                                show: false
                            },
                            itemStyle: {
                                areaColor: "#f59a05"
                            }
                        }
                    },
                    layoutCenter: ['50%', '50%'],//位置
	                layoutSize:'100%',//大小
                    visualMap: [
                    {
                        orient: 'horizontal',
                        min: 1900,
                        max: 120000,
                        text: ['GDP总量(亿元)'],
                        realtime: false,
                        calculable: true,
                        bottom:"0%",                              //组件离容器下侧的距离,'20%'
                        inRange: {
                            color: ['Azure', '#1f8bcb']
                        },
                        textStyle:{
                            color:'#000000'
                        },
                    }],
                    series: [
                        {
                            name:'2020年中国城市GDP百强榜',
                            type: "map",
                            // roam: true,
                            map: "china",   
                            geoIndex: 0,
                            itemStyle: {
                                areaColor: "#1f8bcb",
                                borderColor: "#739af5",
                                borderWidth: 1
                            },
                            emphasis: {
                                label: {
                                    show: false
                                },
                                itemStyle: {
                                    areaColor: "#f59a05"
                                }
                            },
                            data:[...this.data]
                        },
                        lineseries[0],
                        lineseries[1]
                    ]
                };
                this.chart.setOption(options, true);
                this.chart.on('click', (param)=>{
                    cityName = param.name;
                    this.$emit('showCityName',cityName);
                    var lineseries = [];
                    lineseries.push({
                    name: cityName,
                    type: 'lines',
                    zlevel: 1,
                    show: true,
                    effect: {
                        show: true,
                        period: 4, // 特效动画的时间
                        symbol: 'arrow',
                        trailLength: 0.6, // 特效尾迹的长度。取从 0 到 1 的值，默认为 0.2，数值越大尾迹越长
                        color: '#fff',
                        // symbol: planePath, // 特效图形的标记
                        symbolSize: 6
                    },
                    tooltip: {
                        show: true, // 是否显示
                        trigger: 'item', // 触发类型  'item'图形触发：散点图，饼图等无类目轴的图表中使用； 'axis'坐标轴触发；'none'：什么都不触发。
                        // backgroundColor: 'rgba(50,50,50,0.7)', // 提示框浮层的背景颜色。
                        // borderColor: '#fff', // 提示框浮层的边框颜色。
                        borderWidth: 0, // 提示框浮层的边框宽。
                        // padding: 5, // 提示框浮层内边距，
                        // textStyle: { // 提示框浮层的文本样式。
                        //     color: '#fff',
                        //     fontStyle: 'normal',
                        //     fontWeight: 'normal',
                        //     fontFamily: 'sans-serif',
                        //     fontSize: 14,
                        // },
                        // extraCssText: 'box-shadow: 0 0 3px rgba(0, 0, 0, 0.3);', // 额外附加到浮层的 css 样式
                        confine: false, // 是否将 tooltip 框限制在图表的区域内。
                        // formatter: '{b} 的成绩是 {c}'
                        formatter: function(arg) {
                            return '从'+arg.data.fromName + '到' + arg.data.toName + '<br/>的迁徙指数为:<br/>'+ arg.data.value
                        }
                    },
                    lineStyle: {
                        normal: {
                            color: function(arg){
                                var fromName = arg.data.fromName
                                if (fromName == cityName){
                                    return '#CD5C5C'
                                }
                                return '#3f4b51'},
                            width:  2.5,
                            opacity: 0.2,
                            curveness: 0.2
                        }
                    },
                    data: lines_data[cityName]
                },
                {
                    name: cityName+'2',
                    type: 'effectScatter',      // 带有涟漪特效的散点图，起到视觉突出的效果
                    coordinateSystem: 'geo',    // 该系列使用的坐标系指定为地理坐标系
                    zlevel: 2,
                    rippleEffect: {
                        brushType: 'stroke'     // 波纹的绘制方式
                    },
                    label: {
                        normal: {
                            show: true,
                            position: 'left',  // 地区名称标签显示位置
                            
                            textStyle:{
                                fontSize:12,
                            },
                            formatter: '{b}'    // 格式化显示标签，b指的是系列的名称
                        }
                    },
                    symbolSize: function (data) {
                        if(data[2]==1){
                            return 6
                        }
                        return 3;      // 目的地涟漪特效的大小
                    },
                    itemStyle: {
                        normal: {
                            color: function (val) {
                                if(val.data.name == cityName){
                                    return '#FFA500'
                                }
                                return 'MidnightBlue'}
                        }
                    },
                    // 解析：item[1] ==> BJData：[[{name:'北京'}, {name:'上海',value:95}],...]
                    data: link_coordinate[cityName]
                },
                );
                // 指定图表的配置项和数据
                let options = {
                    title: {
                        text: '2020年中国省级GDP总量及热门迁徙路线图',
                        subtext: '国家统计局、高德地图',
                        textStyle:{
                            color:'#377ee5'
                        },
                        subtextStyle:{
                            color:'#c7d5d9'
                        }
                    },
                    tooltip: {
                        textStyle: {
                            fontSize: '14px',
                        },
                        formatter: function(data){
                            if(!isNaN(data.value)){
                                return data.name+"<br/>"+data.value+"亿元";
                            }else{
                                return data.name
                            }
                        }
                    },
                    geo:{
                        type: "map",
                        roam: false, //设置能否移动和缩放
                        map: "china",
                        itemStyle: {
                            areaColor: "LightGrey",
                            borderColor: "#739af5",
                            borderWidth: 1
                        },
                        emphasis: {
                            label: {
                                show: false
                            },
                            itemStyle: {
                                areaColor: "#f59a05"
                            }
                        }
                    },
                    layoutCenter: ['50%', '50%'],//位置
	                layoutSize:'100%',//大小
                    visualMap: [
                    {
                        orient: 'horizontal',
                        min: 1900,
                        max: 120000,
                        text: ['GDP总量(亿元)'],
                        realtime: false,
                        calculable: true,
                        bottom:"0%",                              //组件离容器下侧的距离,'20%'
                        inRange: {
                            color: ['Azure', '#1f8bcb']
                        },
                        textStyle:{
                            color:'#000000'
                        },
                    }],
                    series: [
                        {
                            name:'2020年中国城市GDP百强榜',
                            type: "map",
                            // roam: true,
                            map: "china",   
                            geoIndex: 0,
                            itemStyle: {
                                areaColor: "#1f8bcb",
                                borderColor: "#739af5",
                                borderWidth: 1
                            },
                            emphasis: {
                                label: {
                                    show: false
                                },
                                itemStyle: {
                                    areaColor: "#f59a05"
                                }
                            },
                            data:[...this.data]
                        },
                        lineseries[0],
                        lineseries[1],
                        lineseries[2]
                    ]
                };
                    this.chart.clear();
                    this.chart.setOption(options)
                });
            },
            // 开启定时器
            startInterval() {
                if (this.intervalId !== null) {
                    clearInterval(this.intervalId);
                }
                this.intervalId = setInterval(() => {
                    this.reSelectMapRandomArea();
                }, 2000);
            },
            // 重新随机选中地图区域
            reSelectMapRandomArea() {
                this.$nextTick(() => {
                    let index = Math.floor(Math.random() * this.data.length);
                    this.chart.dispatchAction({
                        type: 'showTip',
                        seriesIndex: 0,
                        dataIndex: index,
                    });
                    this.chart.dispatchAction({
                        type: 'select',
                        seriesIndex: 0,
                        dataIndex: index,
                    });
                });
            },
            handleMapRandomSelect() {
                this.$nextTick(() => {
                    setTimeout(() => {
                        this.reSelectMapRandomArea();
                    }, 0);
                    // 移入区域，清除定时器、取消之前选中并选中当前
                    this.chart.on('mouseover', (params)=> {
                        clearInterval(this.intervalId);
                    });
                    // 移出区域重新随机选中地图区域，并开启定时器
                    this.chart.on('globalout', ()=> {
                        this.reSelectMapRandomArea();
                        this.startInterval();
                    });
                    this.startInterval();
                });
            },
        }
    }
</script>

<style scoped>
    .echart {
        height: 12rem;
    }
</style>
