<!-- 人口迁出指数前10城市图 -->

<!-- <template>
    <div>
        <Echart
                id="speed20"
                :options="options"
                height="4rem"
        ></Echart>
    </div>
</template>
<script>
    import Echart from '@/common/echart';
    export default {
        name: "index",
        props:{type: {   //此处为接收父类传递的参数，进行点击切换数据，默认值为2019
            type: String,
            default:'2019',
            required: true,
        }
        },
        watch:{  //此处为关键，监听type值得变化，进行echarts渲染
            type:{    
                handler(newValue,oldValue){
                this.type=newValue;
                this.initChart(); }
            }
        },
        data() {
            return {
                options: {
                    tooltip: {
                        trigger: 'item',
                        formatter: '{b}{a}{c}'
                    },
                    series: [
                        {
                            name: '实际迁出指数',
                            type: 'pie',
                            roseType: 'radius',
                            radius: '100%',
                            center:['50%','50%'],
                            label: {
                                position: 'outside',
                                formatter: '{b}{c}',
                                fontSize: 14,
                                color:'#666'
                            },
                            data: [
                            {value:71.67, name: '广州'},
                            {value:60.82, name: '东莞'},
                            {value:53.4, name: '佛山'},
                            {value:50.36, name: '深圳'},
                            {value:44.16, name: '苏州'},
                            {value:32.27, name: '北京'},
                            {value:32.04, name: '上海'},
                            {value:30.13, name: '杭州'},
                            {value:29.84, name: '无锡'},
                            {value:28.8, name: '惠州'},
                            // {value:25.49, name: '成都'},
                            // {value:22.81, name: '廊坊'},
                            // {value:22.59, name: '南京'},
                            // {value:22.04, name: '郑州'},
                            // {value:21.71, name: '嘉兴'},
                            // {value:21.69, name: '天津'},
                            // {value:20.59, name: '西安'},
                            // {value:20.11, name: '中山'},
                            // {value:19.11, name: '常州'},
                            // {value:18.51, name: '济南'}
                            ]
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
            console.log(this.type);
            if (this.type == '2019'){
                this.options = {
                    tooltip: {
                        trigger: 'item',
                        formatter: '{b}{a}{c}'
                    },
                    series: [
                        {
                            name: '实际迁出指数',
                            type: 'pie',
                            roseType: 'radius',
                            radius: '100%',
                            center:['50%','50%'],
                            label: {
                                position: 'outside',
                                formatter: '{b}{c}',
                                fontSize: 14,
                                color:'#666'
                            },
                            data: [
                            {value:71.67, name: '广州'},
                            {value:60.82, name: '东莞'},
                            {value:53.4, name: '佛山'},
                            {value:50.36, name: '深圳'},
                            {value:44.16, name: '苏州'},
                            {value:32.27, name: '北京'},
                            {value:32.04, name: '上海'},
                            {value:30.13, name: '杭州'},
                            {value:29.84, name: '无锡'},
                            {value:28.8, name: '惠州'},
                            // {value:25.49, name: '成都'},
                            // {value:22.81, name: '廊坊'},
                            // {value:22.59, name: '南京'},
                            // {value:22.04, name: '郑州'},
                            // {value:21.71, name: '嘉兴'},
                            // {value:21.69, name: '天津'},
                            // {value:20.59, name: '西安'},
                            // {value:20.11, name: '中山'},
                            // {value:19.11, name: '常州'},
                            // {value:18.51, name: '济南'}
                            ]
                        }
                    ]
                }
            }
            else if(this.type==2020){
                this.options = {
                    tooltip: {
                        trigger: 'item',
                        formatter: '{b}{a}{c}%'
                    },
                    series: [
                        {
                            name: '实际迁出指数',
                            type: 'pie',
                            roseType: 'radius',
                            radius: '100%',
                            center:['50%','50%'],
                            label: {
                                position: 'outside',
                                formatter: '{b}{c}',
                                fontSize: 14,
                                color:'#666'
                            },
                            data: [
                            {value:80.03, name: '广州'},
                            {value:69.33, name: '东莞'},
                            {value:60.53, name: '佛山'},
                            {value:56.81, name: '深圳'},
                            {value:49.67, name: '苏州'},
                            {value:36.72, name: '杭州'},
                            {value:34.01, name: '上海'},
                            {value:33.93, name: '惠州'},
                            {value:33.86, name: '无锡'},
                            // {value:29.51, name: '成都'},
                            // {value:26.91, name: '北京'},
                            // {value:25.6, name: '南京'},
                            // {value:25.36, name: '郑州'},
                            // {value:25.29, name: '嘉兴'},
                            // {value:25.2, name: '西安'},
                            // {value:24.12, name: '天津'},
                            // {value:23.71, name: '廊坊'},
                            // {value:23.32, name: '中山'},
                            // {value:23.12, name: '济南'},
                            // {value:21.87, name: '常州'}
                            ]
                        }
                    ]
                }
            }
            else{
                this.options = {
                    tooltip: {
                        trigger: 'item',
                        formatter: '{b}{a}{c}%'
                    },
                    series: [
                        {
                            name: '实际迁出指数',
                            type: 'pie',
                            roseType: 'radius',
                            radius: '100%',
                            center:['50%','50%'],
                            label: {
                                position: 'outside',
                                formatter: '{b}{c}',
                                fontSize: 14,
                                color:'#666'
                            },
                            data: [
                            {value:76.9, name: '广州'},
                            {value:68.12, name: '东莞'},
                            {value:59.36, name: '佛山'},
                            {value:56.58, name: '深圳'},
                            {value:47.95, name: '苏州'},
                            {value:37.49, name: '杭州'},
                            {value:34.63, name: '惠州'},
                            {value:33.32, name: '上海'},
                            {value:32.41, name: '无锡'},
                            {value:31.46, name: '成都'},
                            // {value:26.25, name: '西安'},
                            // {value:25.96, name: '北京'},
                            // {value:25.27, name: '嘉兴'},
                            // {value:24.66, name: '郑州'},
                            // {value:24.13, name: '中山'},
                            // {value:23.39, name: '南京'},
                            // {value:22.99, name: '天津'},
                            // {value:22.75, name: '廊坊'},
                            // {value:22.61, name: '济南'},
                            // {value:21.44, name: '常州'}
                            ]
                        }
                    ]
                }
            }
            
        },
        },
        mounted() {
            this.initChart();
        },


    }

</script> -->