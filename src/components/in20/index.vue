<!-- 人口迁入指数前10城市图 -->

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
                            name: '实际迁入指数',
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
                            {value:67.43, name: '广州'},
                            {value:58.68, name: '东莞'},
                            {value:54.53, name: '深圳'},
                            {value:48.67, name: '佛山'},
                            {value:41.75, name: '苏州'},
                            {value:35.44, name: '上海'},
                            {value:31.97, name: '北京'},
                            {value:29.2, name: '杭州'},
                            {value:26.16, name: '无锡'},
                            {value:25.74, name: '成都'},
                            // {value:25.47, name: '惠州'},
                            // {value:22.64, name: '廊坊'},
                            // {value:22.49, name: '郑州'},
                            // {value:20.46, name: '西安'},
                            // {value:20.17, name: '中山'},
                            // {value:19.98, name: '南京'},
                            // {value:19.26, name: '天津'},
                            // {value:18.37, name: '嘉兴'},
                            // {value:16.19, name: '常州'},
                            // {value:15.99, name: '长沙'}
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
                            name: '实际迁入指数',
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
                            {value:67.43, name: '广州'},
                            {value:58.68, name: '东莞'},
                            {value:54.53, name: '深圳'},
                            {value:48.67, name: '佛山'},
                            {value:41.75, name: '苏州'},
                            {value:35.44, name: '上海'},
                            {value:31.97, name: '北京'},
                            {value:29.2, name: '杭州'},
                            {value:26.16, name: '无锡'},
                            {value:25.74, name: '成都'},
                            // {value:25.47, name: '惠州'},
                            // {value:22.64, name: '廊坊'},
                            // {value:22.49, name: '郑州'},
                            // {value:20.46, name: '西安'},
                            // {value:20.17, name: '中山'},
                            // {value:19.98, name: '南京'},
                            // {value:19.26, name: '天津'},
                            // {value:18.37, name: '嘉兴'},
                            // {value:16.19, name: '常州'},
                            // {value:15.99, name: '长沙'}
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
                            name: '实际迁入指数',
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
                            {value:74.44, name: '广州'},
                            {value:67.23, name: '东莞'},
                            {value:60.11, name: '深圳'},
                            {value:55.84, name: '佛山'},
                            {value:46.24, name: '苏州'},
                            {value:37.75, name: '上海'},
                            {value:35.02, name: '杭州'},
                            {value:29.82, name: '惠州'},
                            {value:29.59, name: '无锡'},
                            {value:29.33, name: '成都'},
                            // {value:26.96, name: '北京'},
                            // {value:25.59, name: '郑州'},
                            // {value:24.81, name: '西安'},
                            // {value:23.51, name: '中山'},
                            // {value:23.44, name: '廊坊'},
                            // {value:22.29, name: '南京'},
                            // {value:21.45, name: '嘉兴'},
                            // {value:20.99, name: '天津'},
                            // {value:19.61, name: '济南'},
                            // {value:19.46, name: '长沙'},
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
                            name: '实际迁入指数',
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
                            {value:73.24, name: '广州'},
                            {value:66.89, name: '东莞'},
                            {value:59.97, name: '深圳'},
                            {value:56.35, name: '佛山'},
                            {value:45.69, name: '苏州'},
                            {value:37.13, name: '上海'},
                            {value:35.97, name: '杭州'},
                            {value:31.98, name: '成都'},
                            {value:31.13, name: '惠州'},
                            {value:29.13, name: '无锡'},
                            // {value:26.24, name: '北京'},
                            // {value:26.19, name: '西安'},
                            // {value:24.82, name: '郑州'},
                            // {value:24.35, name: '中山'},
                            // {value:22.86, name: '廊坊'},
                            // {value:22.33, name: '嘉兴'},
                            // {value:20.49, name: '南京'},
                            // {value:20.31, name: '天津'},
                            // {value:20.19, name: '济南'},
                            // {value:19.37, name: '长沙'},
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