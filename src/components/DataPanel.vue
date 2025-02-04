<template>
    <div class="head clearfix">
        <h1 class="pulll_left">数据监控平台</h1>
        <div class="menu pulll_left">
            <ul>
                <li><a href="">标题样式</a></li>
                <li><a href="">标题样式</a></li>
                <li><a href="">标题样式</a></li>
                <li><a href="">标题样式</a></li>
                <li><a href="">标题样式</a></li>
            </ul>
        </div>
        <div class="time">{{ currentTime }}</div>
    </div>
    <div class="mainbox clearfix">
        <div style="flex:22">
            <div class="box">
                <div class="tit">版块标题1</div>
                <div class="boxnav">
                    <table class="table1" width="100%" border="0" cellspacing="0" cellpadding="0">
                        <thead>
                            <tr>
                                <th>业务类型</th>
                                <th>计划完成</th>
                                <th>实际完成</th>
                                <th>增长率</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(item, index) in tableData1" :key="index">
                                <td>{{ item.type }}</td>
                                <td><span class="text-w">{{ item.planCompletion }}</span></td>
                                <td><span class="text-b">{{ item.actualCompletion }}</span></td>
                                <td>
                                    <div :class="item.growthDirection === '↑' ? 'text-d' : 'text-s'">{{
                                        item.growthDirection }}{{ item.growthRate }}</div>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <div class="box">
                <div class="tit">版块标题2</div>
                <div class="boxnav">
                    <div id="echart2" style="height:160px;"></div>
                    <div class="leidanav">
                        <ul class="clearfix" style="justify-content: space-between;">
                            <li v-for="(item, index) in tableData2" :key="index">
                                <span>{{ item.title }}</span>
                                <p>{{ item.value }}</p>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        <div style="flex:56">
            <div class="box">
                <div class="boxnav mapc" style="height: 412px; position: relative">
                    <div class="mapnav">
                        <div v-for="(item, index) in mapnavData" :key="index"><span>{{ item.title }}</span>
                            <p>{{ item.value }}</p>
                        </div>
                    </div>
                    <div class="mapnav2">
                        <div class="box" style="margin-bottom: 8px;">
                            <div class="tit">版块标题3</div>
                            <div class="boxnav" style="height: 100px;" id="echart3"></div>
                            <div class="leidanav" style="margin-bottom: 10px;">
                                <ul class="clearfix" style="justify-content: space-between;">
                                    <li v-for="(item, index) in tableData3_2" :key="index">
                                        <span>{{ item.title }}</span>
                                        <p>{{ item.value }}</p>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <div id="map" style="width:100%;height: 100%;"></div>
                </div>
            </div>
        </div>
        <div style="flex:22">
            <div class="box" style="width: 95%;">
                <div class="tit">版块标题4</div>
                <div class="boxnav" id="echart4" style="height: 140px;"></div>
            </div>
            <div class="box" style="width: 95%;">
                <div class="tit">版块标题5</div>
                <div class="boxnav" style="height: 175.5px;">
                    <div style="float: left; width: 30%; padding-left: 10px;">
                        <div class="tit02 text-b">热门话题榜</div>
                        <div class="huati">
                            <ul>
                                <li v-for="(item, index) in tableData5_1" :key="index">
                                    {{ index + 1. }}{{ item.title }}
                                    <span :class="item.growthDirection === '↑' ? 'text-d' : 'text-s'">{{
                                        item.growthDirection }}{{ item.growth }}</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <div style="float:right;width:65%;">
                        <div class="text-b tit02" style="text-align: center;">关键词 — 云</div>
                        <div class="tagcloud" style="margin-top: 70px;">
                            <!-- bo大小 co颜色 -->
                            <a v-for="(item, index) in tableData5_2" :key="index"
                                :class="['b0' + ((index % 4) + 1), 'co0' + ((index % 5) + 1)]">
                                {{ item }}
                            </a>
                        </div>
                    </div>

                </div>
            </div>
        </div>
    </div>
    <div class="box" style="padding:8px 0;margin-right: 8px;height:29%;">
        <ul class="clearfix nav2" style="margin:0;height:100%;">
            <li style="width:25%;">
                <div class="tit01">版块标题6</div>
                <div style="display: flex;margin-top: -10px;margin-bottom: 10px;">
                    <div style="width: 50%; height: 170px" id="echart61"></div>
                    <div style="width: 50%; height: 170px" id="echart62"></div>
                </div>
                <div class="leidanav">
                    <ul class="clearfix" style="display: flex; justify-content: space-around;">
                        <li v-for="(item, index) in tableData6_3" :key="index">
                            <span>{{ item.title }}</span>
                            <p>{{ item.value }}</p>
                        </li>
                    </ul>
                </div>


            </li>
            <li style="width:25%">
                <div class="tit01">版块标题7</div>
                <div style="height:180px;" id="echart7"></div>
            </li>
            <li style="width:25%">
                <div class="tit01">版块标题8</div>
                <div style="height:100%;display: flex; align-items: center;">
                    <div style="float: left; width: 50%; height: 100%" class="wancheng">
                        <div><span>已完成人数</span>
                            <h3>1835<i>人</i></h3>
                        </div>
                        <div class="yuan">
                            <span>19%</span>
                        </div>
                    </div>
                    <div style="float: left; width: 50%; height: 50%" id="echart8"></div>
                </div>
            </li>
            <li style="width:25%">
                <div class="tit01">版块标题9</div>
                <div style="display: flex;margin-top: -10px;margin-bottom: 10px;">
                    <div style="width: 50%; height: 170px" id="echart91"></div>
                    <div style="width: 50%; height: 170px" id="echart92"></div>
                </div>
            </li>
        </ul>
    </div>



</template>

<script>
import * as echarts from 'echarts';
import '@/assets/china.js'; // 导入中国地图 JSON 数据
import '../api/tagcloud.js';      /*3D标签云*/


export default {
    name: 'DataPanel',
    data() {
        return {
            currentTime: '',
            //版块标题1数据
            tableData1: [{
                type: "类型1",
                planCompletion: "1000万",
                actualCompletion: "900万",
                growthRate: "12%",
                growthDirection: "↑"
            },
            {
                type: "类型2",
                planCompletion: "1200万",
                actualCompletion: "1100万",
                growthRate: "8%",
                growthDirection: "↑"
            },
            {
                type: "类型3",
                planCompletion: "1500万",
                actualCompletion: "1400万",
                growthRate: "6%",
                growthDirection: "↓"
            },
            {
                type: "类型4",
                planCompletion: "1200万",
                actualCompletion: "1000万",
                growthRate: "10%",
                growthDirection: "↓"
            }],
            //版块标题2数据
            tableData2: [
                { title: "文本1", value: 43 },
                { title: "文本2", value: 100 },
                { title: "文本3", value: 28 },
                { title: "文本4", value: 3 },
                { title: "文本5", value: 150 },
            ],
            //方块数据
            mapnavData: [
                { title: "数据1", value: "40%" },
                { title: "数据2", value: "12%" },
                { title: "数据3", value: "8%" },
                { title: "数据4", value: "24%" },
                { title: "数据5", value: "26%" },
            ],
            //版块标题3 折线图数据
            tableData3_1: [
                { title: "1月", value: 2 },
                { title: "2月", value: 6 },
                { title: "3月", value: 3 },
                { title: "4月", value: 8 },
                { title: "5月", value: 5 },
                { title: "6月", value: 8 }
            ],
            //版块标题3 文字数据
            tableData3_2: [
                { title: "业务笔数", value: 128 },
                { title: "业务收益", value: 100 },
                { title: "业务笔数", value: 28 },
                { title: "业务收益", value: 28 },
            ],
            //版块标题4 条形图数据
            tableData4: [
                { title: '文本1', value: [2, 3, 3, 9, 15, 12, 6, 4, 6] },
                { title: "文本2", value: [1, 4, 5, 11, 12, 9, 5, 6, 5] },
            ],
            //版块标题5 话题榜数据
            tableData5_1: [{
                title: "数据分析",
                growth: "2167",
                growthDirection: "↑"
            },
            {
                title: "云存储",
                growth: "2167",
                growthDirection: "↑"
            },
            {
                title: "视觉分析",
                growth: "2167",
                growthDirection: "↓"
            },
            {
                title: "海量题库",
                growth: "2167",
                growthDirection: "↓"
            },
            {
                title: "云词典",
                growth: "2167",
                growthDirection: "↓"
            }],
            //版块标题5 tagcloud数据
            tableData5_2: [
                "大数据", "人工智能", "云计算", "区块链", "物联网",
            ],
            tableData6_1: [
                { name: '20-29岁', value: 4 },
                { name: '30-39岁', value: 2 },
                { name: '40-49岁', value: 2 },
                { name: '50岁以上', value: 1 },
            ],
            tableData6_2: [
                { name: '博士', value: 10 },
                { name: '硕士', value: 20 },
                { name: '本科', value: 30, },
                { name: '专科', value: 40 },
            ],
            tableData6_3: [
                { title: '总人数', value: 128 },
                { title: '男职员', value: 100 },
                { title: '女职员', value: 28 },
            ],
            tableData7: [
                { title: '2017年', value: [2, 6, 3, 8, 5, 8] },
                { title: "2018年", value: [5, 2, 6, 4, 5, 12] },
            ],

        };
    },
    methods: {
        /* eslint-disable */
        updateTime() {
            const dt = new Date();
            const y = dt.getFullYear();
            const mt = dt.getMonth() + 1;
            const day = dt.getDate();
            const h = dt.getHours();
            const m = dt.getMinutes();
            const s = dt.getSeconds();
            this.currentTime = y + "/" + mt + "/" + day + " " + h + ":" + m + ":" + s;
        },
        initChart2() {
            // 获取图表容器
            const myChart2 = echarts.init(document.getElementById('echart2'));
            //数据配置
            const data = [
                {
                    title: '**省'
                },
                this.tableData2.map(item => ({
                    name: item.title,
                    max: 150
                })),
                this.tableData2.map(item => item.value),
            ];
            // 配置项
            const option = {
                color: ['#9DD060', '#35C96E', '#4DCEF8'], //图表的颜色，依次为浅绿色、绿色和蓝色
                tooltip: {
                    backgroundColor: 'rgba(0,0,0,0.3)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 10, // 提示框文字大小
                        lineHeight: 0,
                    },
                },
                radar: { //雷达图
                    center: ['50%', '50%'], //中心位置，相对容器宽度和高度的 50%
                    radius: ['25%', '70%'], //半径范围，从内到外分别是 25% 和 70%
                    name: {
                        textStyle: {
                            fontSize: 9,
                            color: '#72ACD1' //各维度名称的字体颜色设置为淡蓝色
                        }
                    },
                    splitLine: { //分割线样式
                        lineStyle: {
                            color: 'rgba(255,255,255,.0)', //透明
                            width: 2
                        }
                    },
                    axisLine: { //轴线样式
                        lineStyle: {
                            color: 'rgba(255,255,255,0.2)',
                            width: 1,
                            type: 'dotted' //虚线
                        }
                    },
                    splitArea: { //分割区域背景色
                        areaStyle: {
                            color: ['rgba(255,255,255,.1)', 'rgba(255,255,255,0)'] //渐变色，内圈是半透明白色，外圈是完全透明。
                        }
                    },
                    indicator: data[1] //维度数据（即文本1-5数组）
                },
                series: [ //定义图表的数据系列
                    {
                        name: '总计',
                        type: 'radar',
                        data: [
                            {
                                areaStyle: {
                                    normal: {
                                        opacity: 0.3
                                    }
                                },
                                value: data[2]
                            }
                        ]
                    }
                ]
            };
            // 将配置项应用到图表中，显示图表
            myChart2.setOption(option);
            // 监听窗口尺寸变化，自动调整图表大小
            window.addEventListener('resize', function () {
                myChart2.resize();
            });
        },
        initChart3() {
            // 获取图表容器
            const myChart3 = echarts.init(document.getElementById('echart3'));
            // 配置项
            const option3 = {
                tooltip: {
                    backgroundColor: 'rgba(0,0,0,.3)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 10, // 提示框文字大小
                    },
                    trigger: 'axis', //鼠标悬停在坐标轴时，显示提示框
                    axisPointer: {
                        type: 'shadow' //悬停时显示阴影
                    }
                },
                grid: { //图表内容的位置和大小
                    left: '0',
                    top: '10px',
                    right: '0',
                    bottom: '0',
                    containLabel: true //包含标签
                },
                xAxis: [{ //X轴
                    type: 'category', //类别轴，离散标签
                    data: this.tableData3_1.map(item => item.title), //X轴标签数据
                    axisLine: { //坐标轴线
                        show: true,
                        lineStyle: {
                            color: "rgba(255,255,255,.1)", //白色透明
                            width: 1,
                            type: "solid" //实线
                        },
                    },
                    axisTick: { //坐标轴刻度线
                        show: false,
                    },
                    axisLabel: { //坐标轴标签
                        interval: 0, //每个刻度都显示标签
                        // rotate:50, //旋转度数
                        textStyle: {
                            color: "rgba(255,255,255,.6)",
                            fontSize: '11',
                        },
                    },
                }],
                yAxis: [{ //Y轴
                    type: 'value', //数值轴
                    axisLabel: {
                        textStyle: {
                            color: "rgba(255,255,255,.6)",
                            fontSize: '11',
                        },
                    },
                    axisTick: {
                        show: false,
                    },
                    axisLine: {
                        show: true,
                        lineStyle: {
                            color: "rgba(255,255,255,.1	)",
                            width: 1,
                            type: "solid"
                        },
                    },
                    splitLine: { //分割线
                        show: false,
                        lineStyle: {
                            color: "rgba(255,255,255,.1)",
                        }
                    }
                }],
                series: [{
                    name: '2024年',
                    type: 'line', //折线图
                    // smooth: true, //曲线
                    data: this.tableData3_1.map(item => item.value), //Y轴数值
                    itemStyle: {
                        normal: {
                            color: '#2f89cf',
                            opacity: 1, //透明度
                        }
                    }
                }]
            };
            // 将配置项应用到图表中，显示图表
            myChart3.setOption(option3);
            // 监听窗口尺寸变化，自动调整图表大小
            window.addEventListener('resize', function () {
                myChart3.resize();
            });
        },
        initMap() {
            const mapChart = echarts.init(document.getElementById('map'));
            const data = [
                { name: '海门', value: 9 },
                { name: '鄂尔多斯', value: 12 },
                { name: '招远', value: 12 },
                { name: '舟山', value: 12 },
                { name: '齐齐哈尔', value: 14 },
                { name: '盐城', value: 15 },
                { name: '赤峰', value: 16 },
                { name: '青岛', value: 18 },
                { name: '乳山', value: 18 },
                { name: '金昌', value: 19 },
                { name: '泉州', value: 21 },
                { name: '莱西', value: 21 },
                { name: '日照', value: 21 },
                { name: '胶南', value: 22 },
                { name: '南通', value: 23 },
                { name: '拉萨', value: 24 },
                { name: '云浮', value: 24 },
                { name: '梅州', value: 25 },
                { name: '文登', value: 25 },
                { name: '上海', value: 25 },
                { name: '攀枝花', value: 25 },
                { name: '威海', value: 25 },
                { name: '承德', value: 25 },
                { name: '厦门', value: 26 },
                { name: '汕尾', value: 26 },
                { name: '潮州', value: 26 },
                { name: '丹东', value: 27 },
                { name: '太仓', value: 27 },
                { name: '曲靖', value: 27 },
                { name: '烟台', value: 28 },
                { name: '福州', value: 29 },
                { name: '瓦房店', value: 30 },
                { name: '即墨', value: 30 },
                { name: '抚顺', value: 31 },
                { name: '玉溪', value: 31 },
                { name: '张家口', value: 31 },
                { name: '阳泉', value: 31 },
                { name: '莱州', value: 32 },
                { name: '湖州', value: 32 },
                { name: '汕头', value: 32 },
                { name: '昆山', value: 33 },
                { name: '宁波', value: 33 },
                { name: '湛江', value: 33 },
                { name: '揭阳', value: 34 },
                { name: '荣成', value: 34 },
                { name: '连云港', value: 35 },
                { name: '葫芦岛', value: 35 },
                { name: '常熟', value: 36 },
                { name: '东莞', value: 36 },
                { name: '河源', value: 36 },
                { name: '淮安', value: 36 },
                { name: '泰州', value: 36 },
                { name: '南宁', value: 37 },
                { name: '营口', value: 37 },
                { name: '惠州', value: 37 },
                { name: '江阴', value: 37 },
                { name: '蓬莱', value: 37 },
                { name: '韶关', value: 38 },
                { name: '嘉峪关', value: 38 },
                { name: '广州', value: 38 },
                { name: '延安', value: 38 },
                { name: '太原', value: 39 },
                { name: '清远', value: 39 },
                { name: '中山', value: 39 },
                { name: '昆明', value: 39 },
                { name: '寿光', value: 40 },
                { name: '盘锦', value: 40 },
                { name: '长治', value: 41 },
                { name: '深圳', value: 41 },
                { name: '珠海', value: 42 },
                { name: '宿迁', value: 43 },
                { name: '咸阳', value: 43 },
                { name: '铜川', value: 44 },
                { name: '平度', value: 44 },
                { name: '佛山', value: 44 },
                { name: '海口', value: 44 },
                { name: '江门', value: 45 },
                { name: '章丘', value: 45 },
                { name: '肇庆', value: 46 },
                { name: '大连', value: 47 },
                { name: '临汾', value: 47 },
                { name: '吴江', value: 47 },
                { name: '石嘴山', value: 49 },
                { name: '沈阳', value: 50 },
                { name: '苏州', value: 50 },
                { name: '茂名', value: 50 },
                { name: '嘉兴', value: 51 },
                { name: '长春', value: 51 },
                { name: '胶州', value: 52 },
                { name: '银川', value: 52 },
                { name: '张家港', value: 52 },
                { name: '三门峡', value: 53 },
                { name: '锦州', value: 54 },
                { name: '南昌', value: 54 },
                { name: '柳州', value: 54 },
                { name: '三亚', value: 54 },
                { name: '自贡', value: 56 },
                { name: '吉林', value: 56 },
                { name: '阳江', value: 57 },
                { name: '泸州', value: 57 },
                { name: '西宁', value: 57 },
                { name: '宜宾', value: 58 },
                { name: '呼和浩特', value: 58 },
                { name: '成都', value: 58 },
                { name: '大同', value: 58 },
                { name: '镇江', value: 59 },
                { name: '桂林', value: 59 },
                { name: '张家界', value: 59 },
                { name: '宜兴', value: 59 },
                { name: '北海', value: 60 },
                { name: '西安', value: 61 },
                { name: '金坛', value: 62 },
                { name: '东营', value: 62 },
                { name: '牡丹江', value: 63 },
                { name: '遵义', value: 63 },
                { name: '绍兴', value: 63 },
                { name: '扬州', value: 64 },
                { name: '常州', value: 64 },
                { name: '潍坊', value: 65 },
                { name: '重庆', value: 66 },
                { name: '台州', value: 67 },
                { name: '南京', value: 67 },
                { name: '滨州', value: 70 },
                { name: '贵阳', value: 71 },
                { name: '无锡', value: 71 },
                { name: '本溪', value: 71 },
                { name: '克拉玛依', value: 72 },
                { name: '渭南', value: 72 },
                { name: '马鞍山', value: 72 },
                { name: '宝鸡', value: 72 },
                { name: '焦作', value: 75 },
                { name: '句容', value: 75 },
                { name: '北京', value: 79 },
                { name: '徐州', value: 79 },
                { name: '衡水', value: 80 },
                { name: '包头', value: 80 },
                { name: '绵阳', value: 80 },
                { name: '乌鲁木齐', value: 84 },
                { name: '枣庄', value: 84 },
                { name: '杭州', value: 84 },
                { name: '淄博', value: 85 },
                { name: '鞍山', value: 86 },
                { name: '溧阳', value: 86 },
                { name: '库尔勒', value: 86 },
                { name: '安阳', value: 90 },
                { name: '开封', value: 90 },
                { name: '济南', value: 92 },
                { name: '德阳', value: 93 },
                { name: '温州', value: 95 },
                { name: '九江', value: 96 },
                { name: '邯郸', value: 98 },
                { name: '临安', value: 99 },
                { name: '兰州', value: 99 },
                { name: '沧州', value: 100 },
                { name: '临沂', value: 103 },
                { name: '南充', value: 104 },
                { name: '天津', value: 105 },
                { name: '富阳', value: 106 },
                { name: '泰安', value: 112 },
                { name: '诸暨', value: 112 },
                { name: '郑州', value: 113 },
                { name: '哈尔滨', value: 114 },
                { name: '聊城', value: 116 },
                { name: '芜湖', value: 117 },
                { name: '唐山', value: 119 },
                { name: '平顶山', value: 119 },
                { name: '邢台', value: 119 },
                { name: '德州', value: 120 },
                { name: '济宁', value: 120 },
                { name: '荆州', value: 127 },
                { name: '宜昌', value: 130 },
                { name: '义乌', value: 132 },
                { name: '丽水', value: 133 },
                { name: '洛阳', value: 134 },
                { name: '秦皇岛', value: 136 },
                { name: '株洲', value: 143 },
                { name: '石家庄', value: 147 },
                { name: '莱芜', value: 148 },
                { name: '常德', value: 152 },
                { name: '保定', value: 153 },
                { name: '湘潭', value: 154 },
                { name: '金华', value: 157 },
                { name: '岳阳', value: 169 },
                { name: '长沙', value: 175 },
                { name: '衢州', value: 177 },
                { name: '廊坊', value: 193 },
                { name: '菏泽', value: 194 },
                { name: '合肥', value: 229 },
                { name: '武汉', value: 273 },
                { name: '大庆', value: 279 }
            ];
            const geoCoordMap = {
                '海门': [121.15, 31.89],
                '鄂尔多斯': [109.781327, 39.608266],
                '招远': [120.38, 37.35],
                '舟山': [122.207216, 29.985295],
                '齐齐哈尔': [123.97, 47.33],
                '盐城': [120.13, 33.38],
                '赤峰': [118.87, 42.28],
                '青岛': [120.33, 36.07],
                '乳山': [121.52, 36.89],
                '金昌': [102.188043, 38.520089],
                '泉州': [118.58, 24.93],
                '莱西': [120.53, 36.86],
                '日照': [119.46, 35.42],
                '胶南': [119.97, 35.88],
                '南通': [121.05, 32.08],
                '拉萨': [91.11, 29.97],
                '云浮': [112.02, 22.93],
                '梅州': [116.1, 24.55],
                '文登': [122.05, 37.2],
                '上海': [121.48, 31.22],
                '攀枝花': [101.718637, 26.582347],
                '威海': [122.1, 37.5],
                '承德': [117.93, 40.97],
                '厦门': [118.1, 24.46],
                '汕尾': [115.375279, 22.786211],
                '潮州': [116.63, 23.68],
                '丹东': [124.37, 40.13],
                '太仓': [121.1, 31.45],
                '曲靖': [103.79, 25.51],
                '烟台': [121.39, 37.52],
                '福州': [119.3, 26.08],
                '瓦房店': [121.979603, 39.627114],
                '即墨': [120.45, 36.38],
                '抚顺': [123.97, 41.97],
                '玉溪': [102.52, 24.35],
                '张家口': [114.87, 40.82],
                '阳泉': [113.57, 37.85],
                '莱州': [119.942327, 37.177017],
                '湖州': [120.1, 30.86],
                '汕头': [116.69, 23.39],
                '昆山': [120.95, 31.39],
                '宁波': [121.56, 29.86],
                '湛江': [110.359377, 21.270708],
                '揭阳': [116.35, 23.55],
                '荣成': [122.41, 37.16],
                '连云港': [119.16, 34.59],
                '葫芦岛': [120.836932, 40.711052],
                '常熟': [120.74, 31.64],
                '东莞': [113.75, 23.04],
                '河源': [114.68, 23.73],
                '淮安': [119.15, 33.5],
                '泰州': [119.9, 32.49],
                '南宁': [108.33, 22.84],
                '营口': [122.18, 40.65],
                '惠州': [114.4, 23.09],
                '江阴': [120.26, 31.91],
                '蓬莱': [120.75, 37.8],
                '韶关': [113.62, 24.84],
                '嘉峪关': [98.289152, 39.77313],
                '广州': [113.23, 23.16],
                '延安': [109.47, 36.6],
                '太原': [112.53, 37.87],
                '清远': [113.01, 23.7],
                '中山': [113.38, 22.52],
                '昆明': [102.73, 25.04],
                '寿光': [118.73, 36.86],
                '盘锦': [122.070714, 41.119997],
                '长治': [113.08, 36.18],
                '深圳': [114.07, 22.62],
                '珠海': [113.52, 22.3],
                '宿迁': [118.3, 33.96],
                '咸阳': [108.72, 34.36],
                '铜川': [109.11, 35.09],
                '平度': [119.97, 36.77],
                '佛山': [113.11, 23.05],
                '海口': [110.35, 20.02],
                '江门': [113.06, 22.61],
                '章丘': [117.53, 36.72],
                '肇庆': [112.44, 23.05],
                '大连': [121.62, 38.92],
                '临汾': [111.5, 36.08],
                '吴江': [120.63, 31.16],
                '石嘴山': [106.39, 39.04],
                '沈阳': [123.38, 41.8],
                '苏州': [120.62, 31.32],
                '茂名': [110.88, 21.68],
                '嘉兴': [120.76, 30.77],
                '长春': [125.35, 43.88],
                '胶州': [120.03336, 36.264622],
                '银川': [106.27, 38.47],
                '张家港': [120.555821, 31.875428],
                '三门峡': [111.19, 34.76],
                '锦州': [121.15, 41.13],
                '南昌': [115.89, 28.68],
                '柳州': [109.4, 24.33],
                '三亚': [109.511909, 18.252847],
                '自贡': [104.778442, 29.33903],
                '吉林': [126.57, 43.87],
                '阳江': [111.95, 21.85],
                '泸州': [105.39, 28.91],
                '西宁': [101.74, 36.56],
                '宜宾': [104.56, 29.77],
                '呼和浩特': [111.65, 40.82],
                '成都': [104.06, 30.67],
                '大同': [113.3, 40.12],
                '镇江': [119.44, 32.2],
                '桂林': [110.28, 25.29],
                '张家界': [110.479191, 29.117096],
                '宜兴': [119.82, 31.36],
                '北海': [109.12, 21.49],
                '西安': [108.95, 34.27],
                '金坛': [119.56, 31.74],
                '东营': [118.49, 37.46],
                '牡丹江': [129.58, 44.6],
                '遵义': [106.9, 27.7],
                '绍兴': [120.58, 30.01],
                '扬州': [119.42, 32.39],
                '常州': [119.95, 31.79],
                '潍坊': [119.1, 36.62],
                '重庆': [106.54, 29.59],
                '台州': [121.420757, 28.656386],
                '南京': [118.78, 32.04],
                '滨州': [118.03, 37.36],
                '贵阳': [106.71, 26.57],
                '无锡': [120.29, 31.59],
                '本溪': [123.73, 41.3],
                '克拉玛依': [84.77, 45.59],
                '渭南': [109.5, 34.52],
                '马鞍山': [118.48, 31.56],
                '宝鸡': [107.15, 34.38],
                '焦作': [113.21, 35.24],
                '句容': [119.16, 31.95],
                '北京': [116.46, 39.92],
                '徐州': [117.2, 34.26],
                '衡水': [115.72, 37.72],
                '包头': [110, 40.58],
                '绵阳': [104.73, 31.48],
                '乌鲁木齐': [87.68, 43.77],
                '枣庄': [117.57, 34.86],
                '杭州': [120.19, 30.26],
                '淄博': [118.05, 36.78],
                '鞍山': [122.85, 41.12],
                '溧阳': [119.48, 31.43],
                '库尔勒': [86.06, 41.68],
                '安阳': [114.35, 36.1],
                '开封': [114.35, 34.79],
                '济南': [117, 36.65],
                '德阳': [104.37, 31.13],
                '温州': [120.65, 28.01],
                '九江': [115.97, 29.71],
                '邯郸': [114.47, 36.6],
                '临安': [119.72, 30.23],
                '兰州': [103.73, 36.03],
                '沧州': [116.83, 38.33],
                '临沂': [118.35, 35.05],
                '南充': [106.110698, 30.837793],
                '天津': [117.2, 39.13],
                '富阳': [119.95, 30.07],
                '泰安': [117.13, 36.18],
                '诸暨': [120.23, 29.71],
                '郑州': [113.65, 34.76],
                '哈尔滨': [126.63, 45.75],
                '聊城': [115.97, 36.45],
                '芜湖': [118.38, 31.33],
                '唐山': [118.02, 39.63],
                '平顶山': [113.29, 33.75],
                '邢台': [114.48, 37.05],
                '德州': [116.29, 37.45],
                '济宁': [116.59, 35.38],
                '荆州': [112.239741, 30.335165],
                '宜昌': [111.3, 30.7],
                '义乌': [120.06, 29.32],
                '丽水': [119.92, 28.45],
                '洛阳': [112.44, 34.7],
                '秦皇岛': [119.57, 39.95],
                '株洲': [113.16, 27.83],
                '石家庄': [114.48, 38.03],
                '莱芜': [117.67, 36.19],
                '常德': [111.69, 29.05],
                '保定': [115.48, 38.85],
                '湘潭': [112.91, 27.87],
                '金华': [119.64, 29.12],
                '岳阳': [113.09, 29.37],
                '长沙': [113, 28.21],
                '衢州': [118.88, 28.97],
                '廊坊': [116.7, 39.53],
                '菏泽': [115.480656, 35.23375],
                '合肥': [117.27, 31.86],
                '武汉': [114.31, 30.52],
                '大庆': [125.03, 46.58]
            };
            const convertData = function (data) {
                const res = [];
                for (var i = 0; i < data.length; i++) {
                    const geoCoord = geoCoordMap[data[i].name];
                    if (geoCoord) {
                        res.push({
                            name: data[i].name,
                            value: geoCoord.concat(data[i].value),
                        });
                    }
                }
                return res;
            };
            const option = {
                title: {
                    text: '实时工厂零件', //主标题
                    // subtext: '钢材', //副标题
                    left: 'right', //标题位置
                    textStyle: {
                        color: 'rgba(255,255,255,.8)',
                        fontSize: 16
                    }
                },
                tooltip: {
                    trigger: 'item',
                    backgroundColor: 'rgba(0,0,0,0.4)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 13, // 提示框文字大小
                        lineHeight: 0,
                    },
                    formatter: function (params) {
                        const value = params.value[2];  // 获取数据值（第三个元素）
                        const name = params.name; // 获取城市或地区的名称
                        // 返回自定义的 tooltip 格式
                        return `
            <div style="display: flex; align-items: center;">
                <div style="width: 8px; height: 8px; background-color: ${params.color}; border-radius: 50%; margin-right: 8px;"></div>
                <span>${name} :</span>
                <span style="margin-left: 8px;">${value}</span>
            </div>
             `;
                    }
                },
                geo: {
                    map: 'china', //中国地图
                    label: {
                        emphasis: {
                            show: false //禁用地图上区域的标签显示
                        }
                    },
                    roam: true, //允许地图的缩放和拖动
                    zoom: 1.2, //初始缩放级别为1.2
                    itemStyle: { //地图区域样式
                        normal: { //正常状态下
                            areaColor: 'rgba(2,37,101,.5)', //区域颜色
                            borderColor: 'rgba(112,187,252,.5)' //边界颜色
                        },
                        emphasis: { //选中状态下
                            areaColor: 'rgba(2,37,101,.8)'
                        }
                    }
                },
                series: [
                    {
                        // name: '位置',
                        type: 'scatter', //散点图
                        coordinateSystem: 'geo', //使用地理坐标系进行绘制
                        //symbol: 'image://D://MyWebProject//steels_defect//steels_defect_front//src//assets//position02.svg',  // 自定义图形（类似于菱形）
                        data: convertData(data), //将 data 转换为符合 ECharts 格式的地理数据
                        symbolSize: function (val) { //根据数据值调整散点的大小
                            return val[2] / 15;
                        },
                        // label: {
                        //     normal: {
                        //         show: false //正常状态下不显示标注文本
                        //     },
                        //     emphasis: {
                        //         formatter: '{b}', //格式化标注文本，{b} 代表城市名称。
                        //         position: 'right', //标注文本显示在点的右侧
                        //         show: true
                        //     }
                        // },
                        itemStyle: {
                            normal: {
                                color: '#ffeb7b' //散点颜色
                            }
                        }
                    }

                ]
            };
            mapChart.setOption(option);
            window.addEventListener("resize", function () {
                mapChart.resize();
            });
        },
        initChart4() {
            const myChart4 = echarts.init(document.getElementById('echart4'));
            const option4 = {
                tooltip: {
                    backgroundColor: 'rgba(0,0,0,.3)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 10, // 提示框文字大小
                    },
                    trigger: 'axis',
                    axisPointer: {
                        type: 'shadow'
                    }
                },
                legend: {
                    data: [this.tableData4[0].title, this.tableData4[1].title], //设置图例的名称
                    textStyle: {
                        color: "rgba(255,255,255,.5)",
                        fontSize: '10',

                    },
                    itemWidth: 10, //图例标记（小方块）的宽度
                    itemHeight: 10,
                    itemGap: 30, //图例项之间的间距
                },
                grid: { //图表的布局
                    left: '0%',
                    top: '30px',
                    right: '0%',
                    bottom: '0%',
                    containLabel: true, //包含坐标轴的刻度标签
                },
                xAxis: [{
                    type: 'category', //类别轴
                    data: ['1', '2', '3', '4', '5', '6', '7', '8', '9'],
                    axisLine: { //x轴线
                        show: true,
                        lineStyle: {
                            color: "rgba(255,255,255,.1)",
                        },
                    },
                    axisTick: { //轴刻度线
                        show: false,
                    },
                    axisLabel: { //轴刻度标签
                        interval: 0, //显示所有类别
                        textStyle: {
                            color: "rgba(255,255,255,.6)",
                            fontSize: '11',
                        },
                    },
                }],
                yAxis: [{
                    type: 'value',
                    axisLabel: {
                        textStyle: {
                            color: "rgba(255,255,255,.6)",
                            fontSize: '11',
                        },
                    },
                    axisTick: {
                        show: false,
                    },
                    axisLine: {
                        show: true,
                        lineStyle: {
                            color: "rgba(255,255,255,.1	)",
                        },
                    },
                    splitLine: {
                        lineStyle: {
                            color: "rgba(255,255,255,.1)",
                        }
                    }
                }],
                series: [{
                    name: this.tableData4[0].title,
                    type: 'bar',
                    data: this.tableData4[0].value,
                    barWidth: '20%', //柱子宽度
                    // barGap: 1, //柱子之间间距
                    itemStyle: {
                        normal: {
                            color: '#2f89cf',
                            barBorderRadius: 4,
                        }
                    }
                }, {
                    name: this.tableData4[1].title,
                    type: 'bar',
                    data: this.tableData4[1].value,
                    barWidth: '20%',
                    // barGap: 1,
                    itemStyle: {
                        normal: {
                            color: '#62c98d',
                            barBorderRadius: 4,
                        }
                    }
                },
                ]
            };
            myChart4.setOption(option4);
            window.addEventListener("resize", function () {
                myChart4.resize();
            });
        },
        initChart6() {
            const myChart61 = echarts.init(document.getElementById('echart61'));
            const myChart62 = echarts.init(document.getElementById('echart62'));
            const option61 = {
                tooltip: {
                    backgroundColor: 'rgba(0,0,0,.3)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 10, // 提示框文字大小
                    },
                    trigger: 'item',
                    formatter: "{a} <br/>{b}: {c} ({d}%)", //// 格式化提示框内容：{a}是系列名称，{b}是数据项名称，{c}是值，{d}是百分比。
                    position: function (p) {   //p为当前鼠标的位置
                        return [p[0] + 10, p[1] - 10]; // 提示框相对鼠标位置偏移 10px（右移10，向上移10）
                    }
                },
                legend: { //图例
                    orient: 'vertical', //显示方向：垂直排列
                    top: '25%', //距离容器顶部
                    right: 0,
                    itemWidth: 8,
                    itemHeight: 8,
                    textStyle: {
                        color: 'rgba(255,255,255,.5)',
                        fontSize: '10',
                    }
                },
                series: [
                    {
                        name: '年龄分布',
                        type: 'pie', //饼图
                        center: ['30%', '50%'], //中心位置，距容器左侧和顶部的百分比
                        radius: ['40%', '50%'], //半径范围，支持内外半径即环
                        color: ['#62c98d', '#2f89cf', '#4cb9cf', '#e0c828', '#e58c00', '#eb295b'], //每个扇形的颜色
                        label: { show: false }, //隐藏扇形区域的标签文字
                        labelLine: { show: false }, //隐藏扇形区域的引导线
                        data: this.tableData6_1,
                    }
                ]
            };
            const option62 = {
                tooltip: {
                    backgroundColor: 'rgba(0,0,0,.3)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 10, // 提示框文字大小
                    },
                    trigger: 'item',
                    formatter: "{a} <br/>{b}: {c} ({d}%)",
                    position: function (p) {   //其中p为当前鼠标的位置
                        return [p[0] + 10, p[1] - 10];
                    }
                },
                legend: {
                    orient: 'vertical',
                    top: '25%',
                    right: '8%',
                    itemWidth: 8,
                    itemHeight: 8,
                    textStyle: {
                        color: 'rgba(255,255,255,.5)',
                        fontSize: '10',
                    }
                },
                series: [
                    {
                        name: '学历构成',
                        type: 'pie',
                        center: ['40%', '50%'],
                        radius: ['40%', '50%'],
                        color: ['#62c98d', '#2f89cf', '#4cb9cf', '#e0c828', '#e58c00', '#eb295b'],
                        label: { show: false },
                        labelLine: { show: false },
                        data: this.tableData6_2,
                    }
                ]
            };
            myChart61.setOption(option61);
            myChart62.setOption(option62);
            window.addEventListener("resize", function () {
                myChart61.resize();
                myChart62.resize();
            });
        },
        initChart7() {
            const myChart7 = echarts.init(document.getElementById('echart7'));
            const option7 = {
                tooltip: {
                    backgroundColor: 'rgba(0,0,0,.3)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 10, // 提示框文字大小
                    },
                    trigger: 'axis',
                    axisPointer: {
                        type: 'shadow'
                    }
                },
                legend: {
                    data: this.tableData7.title,
                    top: '5%',
                    textStyle: {
                        color: "#fff",
                        fontSize: '10',
                    },
                    itemGap: 35
                },
                grid: {
                    left: '0%',
                    top: '22%',
                    right: '0%',
                    bottom: '0',
                    containLabel: true
                },
                xAxis: [{
                    type: 'category',
                    data: ['1月', '2月', '3月', '4月', '5月', '6月'],
                    axisLine: {
                        lineStyle: {
                            color: "rgba(255,255,255,.1)",
                        },
                    },
                    axisTick: {
                        show: false,
                    },
                    axisLabel: {
                        interval: 0,
                        textStyle: {
                            color: "rgba(255,255,255,.6)",
                            fontSize: '10',
                        },
                    },
                }],
                yAxis: [{
                    type: 'value',
                    axisLabel: {
                        textStyle: {
                            color: "rgba(255,255,255,.6)",
                            fontSize: '10',
                        },
                    },
                    axisTick: {
                        show: false,
                    },
                    axisLine: {
                        show: true,
                        lineStyle: {
                            color: "rgba(255,255,255,.1	)",
                        },
                    },
                    splitLine: {
                        lineStyle: {
                            color: "rgba(255,255,255,.1)",
                        }
                    }
                }],
                series: [{
                    name: this.tableData7[0].title,
                    type: 'line',
                    smooth: true,
                    data: this.tableData7[0].value,
                    itemStyle: {
                        normal: {
                            color: '#2f89cf',
                            barBorderRadius: 5,
                        }
                    }
                }, {
                    name: this.tableData7[1].title,
                    type: 'line',
                    smooth: true,
                    data: this.tableData7[1].value,
                    itemStyle: {
                        normal: {
                            color: '#62c98d',
                            barBorderRadius: 5,
                        }
                    }
                },
                ]
            };
            myChart7.setOption(option7);
            window.addEventListener("resize", function () {
                myChart7.resize();
            });
        },
        initChart8() {
            const myChart8 = echarts.init(document.getElementById('echart8'));
            const option8 = {
                grid: {
                    left: '0',
                    right: '0',
                    top: '10%',
                    bottom: '24%',
                },
                legend: {
                    data: ['等待', '已办人数', '已办业务'],
                    bottom: 0,
                    itemWidth: 8,
                    itemHeight: 8,
                    textStyle: {
                        color: "#fff",
                        fontSize: '9',
                    },
                    itemGap: 5
                },
                tooltip: {
                    backgroundColor: 'rgba(0,0,0,.3)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 10, // 提示框文字大小
                    },
                    show: "true",
                    trigger: 'item'
                },
                yAxis: {
                    type: 'value',
                    show: false,
                },
                xAxis: [{
                    type: 'category',
                    axisTick: {
                        show: false
                    },
                    axisLine: {
                        show: true,
                        lineStyle: {
                            color: '#363e83',
                        }
                    },
                    axisLabel: {
                        show: false,
                    },
                    data: ['业务办量统计']
                }],
                series: [
                    {
                        name: '等待',
                        type: 'bar',
                        barWidth: '16',
                        itemStyle: {
                            normal: {
                                show: true,
                                color: '#20aa92',
                                barBorderRadius: 40,
                                borderWidth: 0,
                            }
                        },
                        zlevel: 2,
                        barGap: '100%',
                        data: [20],
                        label: {
                            formatter: "{c}人",
                            show: true,
                            position: 'top',
                            textStyle: {
                                fontSize: 10,
                                color: 'rgba(255,255,255,.6)',
                            }
                        },
                    },
                    {
                        name: '已办人数',
                        type: 'bar',
                        itemStyle: {
                            normal: {
                                show: true,
                                color: '#f4664e',
                                barBorderRadius: 40,
                                borderWidth: 0,
                            }
                        },
                        zlevel: 2,
                        barWidth: '16',
                        data: [40],
                        label: {
                            formatter: "{c}人",
                            show: true,
                            position: 'top',
                            textStyle: {
                                fontSize: 10,
                                color: 'rgba(255,255,255,.6)',
                            }
                        },
                    },
                    {
                        name: '已办业务',
                        type: 'bar',
                        itemStyle: {
                            normal: {
                                show: true,
                                color: '#0c93dc',
                                barBorderRadius: 40,
                                borderWidth: 0,
                            }
                        },
                        zlevel: 2,
                        barWidth: '16',
                        data: [127],
                        label: {
                            formatter: "{c}份",
                            show: true,
                            position: 'top',
                            textStyle: {
                                fontSize: 10,
                                color: 'rgba(255,255,255,.6)',
                            }
                        },
                    },

                ]
            };
            myChart8.setOption(option8);
            window.addEventListener("resize", function () {
                myChart8.resize();
            });
        },
        initChart9() {
            const myChart91 = echarts.init(document.getElementById('echart91'));
            const myChart92 = echarts.init(document.getElementById('echart92'));
            const option91 = {
                tooltip: {
                    backgroundColor: 'rgba(0,0,0,.3)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 10, // 提示框文字大小
                    },
                    trigger: 'item',
                    formatter: "{a} <br/>{b}: {c} ({d}%)",
                    position: function (p) {   //其中p为当前鼠标的位置
                        return [p[0] + 10, p[1] - 10];
                    }
                },
                legend: {
                    orient: 'vertical',
                    top: 'center',
                    right: 0,
                    itemWidth: 8,
                    itemHeight: 8,
                    data: ['数据分门别类', '数据关系部门', '今日数据交易'],
                    textStyle: {
                        color: 'rgba(255,255,255,.5)',
                        fontSize: '10',
                    }
                },
                series: [
                    {
                        name: '数据',
                        type: 'pie',
                        center: ['30%', '50%'],
                        radius: ['40%', '50%'],
                        color: ['#62c98d', '#2f89cf', '#4cb9cf', '#e0c828', '#e58c00', '#eb295b'],
                        label: { show: false },
                        labelLine: { show: false },
                        data: [
                            { value: 4, name: '数据分门别类' },
                            { value: 2, name: '数据关系部门' },
                            { value: 2, name: '今日数据交易' },
                        ]
                    }
                ]
            };
            const option92 = {
                tooltip: {
                    backgroundColor: 'rgba(0,0,0,.3)', // 背景颜色，使用 rgba 格式设置透明背景
                    borderWidth: 0, // 边框宽度
                    textStyle: {
                        color: '#fff', // 提示框文字颜色
                        fontSize: 10, // 提示框文字大小
                    },
                    trigger: 'item',
                    formatter: "{a} <br/>{b}: {c} ({d}%)",
                    position: function (p) {   //其中p为当前鼠标的位置
                        return [p[0] + 10, p[1] - 10];
                    }
                },
                legend: {
                    orient: 'vertical',
                    top: 'center',
                    right: '8%',
                    itemWidth: 8,
                    itemHeight: 8,
                    data: ['零销类', '服务类', '销售类', '软件类', '硬件类', '其它类'],
                    textStyle: {
                        color: 'rgba(255,255,255,.5)',
                        fontSize: '10',
                    }
                },
                series: [
                    {
                        name: '业务分类', // 设置图表名称为“业务分类”
                        type: 'pie', // 指定图表类型为饼图
                        center: ['35%', '50%'], // 设置饼图中心位置
                        radius: ['40%', '50%'], // 设置饼图的内半径和外半径
                        color: ['#62c98d', '#2f89cf', '#4cb9cf', '#e0c828', '#e58c00', '#eb295b'], // 设置饼图颜色
                        label: { show: false }, // 隐藏饼图标签
                        labelLine: { show: false }, // 隐藏饼图标签连接线
                        data: [
                            { value: 10, name: '零销类' },
                            { value: 20, name: '服务类' },
                            { value: 30, name: '销售类' },
                            { value: 40, name: '软件类' },
                            { value: 50, name: '硬件类' },
                            { value: 60, name: '其它类' },
                        ]
                    }
                ]
            };
            myChart91.setOption(option91);
            myChart92.setOption(option92);
            window.addEventListener("resize", function () {
                myChart91.resize();
                myChart92.resize();
            });
        },

    },
    mounted() {
        tagcloud({
            selector: ".tagcloud",  //元素选择器
            radius: 30,         //滚动半径, 单位px 页面宽度和高度的五分之一
            mspeed: "slow",   //滚动最大速度, 取值: slow, normal(默认), fast
            ispeed: "slow",   //滚动初速度, 取值: slow, normal(默认), fast
            direction: 0,     //初始滚动方向, 取值角度(顺时针360): 0对应top, 90对应left, 135对应right-bottom(默认)...
            keep: false          //鼠标移出组件后是否继续随鼠标滚动, 取值: false, true(默认) 对应 减速至初速度滚动, 随鼠标滚动
        });
        this.updateTime();
        setInterval(this.updateTime, 1000);
        this.initChart2();
        this.initChart3();
        this.initMap();
        this.initChart4();
        this.initChart6();
        this.initChart7();
        this.initChart8();
        this.initChart9();

    }

};
</script>

<style>
.clearfix:after,
.clearfix:before {
    display: table;
    content: " "
}

.clearfix:after {
    clear: both
}

.clearfix {
    display: flex;
}

.head {
    position: relative;
    height: 50px;
    margin-left: 15px;
    margin-right: 15px;
    margin-top: 0px;
    margin-bottom: 8px;
}

.head h1 {
    font-size: 25px;
    /* letter-spacing: -2px; */
    /* text-align: center; */
    /* padding-left: 10px; */
    padding-right: 40px;
    line-height: 25px;
    color: #daf9ff;
}

.head .menu ul {
    font-size: 0;
}

.head .menu li {
    display: inline-block;
    position: relative;
    margin: 15px 15px;
}

.head .menu li a {
    display: block;
    font-size: 14px;
    color: #fff;
    line-height: 30px;
    padding: 0 15px;
    text-decoration: none;
}

.menu li:before,
.menu li:after {
    position: absolute;
    width: 10px;
    height: 5px;
    opacity: .4;
    content: "";
    border-top: 2px solid #02a6b5;
    top: -1px;
    border-radius: 2px;
}

.menu li:before,
.menu li a:before {
    border-left: 2px solid #02a6b5;
    left: -1px;
}

.menu li:after,
.menu li a:after {
    border-right: 2px solid #02a6b5;
    right: -1px;
}

.menu li a:before,
.menu li a:after {
    position: absolute;
    width: 10px;
    height: 5px;
    opacity: .4;
    content: "";
    border-bottom: 2px solid #02a6b5;
    bottom: -1px;
    border-radius: 2px;
}

.head .menu li a:hover {
    color: #f4e925;
}

.menu li a:hover:before,
.menu li a:hover:after,
.menu li:hover:before,
.menu li:hover:after {
    border-color: #f4e925;
    opacity: 1;
}

.head .time {
    position: absolute;
    right: 0;
    font-size: 13px;
    line-height: 60px;
}

.pulll_left {
    float: left;
}

.pulll_right {
    float: right;
}

.text-w {
    color: #ffe400
}

.text-d {
    color: #ff6316
}

.text-s {
    color: #14e144
}

.text-b {
    color: #07e5ff
}

ul {
    list-style-type: none;
    /* 去掉默认的列表符号 */
    padding: 0px;

}

.box {
    border: 1px solid rgba(7, 118, 181, .5);
    box-shadow: inset 0 0 8px rgba(7, 118, 181, .4);
    margin-bottom: 12px;
    position: relative;
    margin-left: 8px;
}

.tit {
    padding: 8px 8px 8px 20px;
    border-bottom: 1px solid rgba(7, 118, 181, .7);
    font-size: 13px;
    position: relative;
}

.tit:before,
.tit01:before {
    position: absolute;
    content: "";
    width: 5px;
    height: 5px;
    background: rgba(22, 214, 255, .9);
    box-shadow: 0 0 4px rgba(22, 214, 255, .9);
    border-radius: 8px;
    left: 8px;
    top: 14px;
}

.tit01 {
    font-size: 13px;
    /* font-weight: 500; */
    position: relative;
    padding-left: 15px;
}

.tit01:before {
    left: 3px;
    top: 8px;
}

.tit:after,
.box:before {
    width: 100%;
    height: 1px;
    content: "";
    position: absolute;
    left: 0;
    bottom: -1px;
    background: linear-gradient(to right, #076ead, #4ba6e0, #076ead);
    box-shadow: 0 0 5px rgba(131, 189, 227, 1);
    opacity: .6
}

.box:before {
    top: -1px;
}

.boxnav {
    padding: 8px;
}

.table1 th {
    border-bottom: 1px solid #407abd;
    font-size: 11px;
    text-align: center;
    padding: 5px 0;
    color: rgba(255, 255, 255, .8)
}

.table1 td {
    border-bottom: 1px dotted#407abd;
    font-size: 10px;
    padding: 5px 0;
    text-align: center;
    color: rgba(255, 255, 255, .6)
}

.table1 tr:last-child td {
    border: none;
}

.nav2>li:first-child {
    border: none;
}

.nav2>li {
    /* float: left; */
    border-left: 1px solid rgba(7, 118, 181, .2);
    /* height: 100%; */
    padding: 0 8px 8px 8px;
}


.mapc {
    background: url(../images/bg3.png) no-repeat center center;
    background-size: 100% 100%
}

/* .mapnav {
    position: absolute;
    z-index: 10;
} */

.mapnav div {
    background: url(../images/bg1.png) no-repeat;
    background-size: 100% auto;
    width: 90px;
    text-align: center;
    padding: 14px 0;
    line-height: 100%;
    float: left;
    margin-right: 5px;
}

.mapnav div span {
    font-size: 11px;
    opacity: .6
}

.mapnav div p {
    margin: 0;
    font-size: 15px;
    font-weight: bold;
    padding-top: 4px;
}


.mapnav2 {
    position: absolute;
    left: 0px;
    bottom: 0px;
    width: 40%;
    z-index: 10;
}

/* .ybp{width: 100%}
.ybp li{float: left; width: 50%; height: 120px; }
.duibi li{float: left; width: 25%; height: 200px; padding: 0; border: none;} */

.leidanav {
    margin-top: -25px;
    margin-bottom: -10px;
}

.leidanav li {
    float: left;
    width: 50%;
    text-align: center;
    border-left: 1px solid rgba(255, 255, 255, .1);
}

.leidanav p {
    font-size: 13.5px;
    color: #26a6ff;
    margin: 0;
}

.leidanav li:first-child {
    border-left: none;
}

.leidanav span {
    font-size: 10px;
    opacity: .6
}

.tit02 {
    font-size: 12px;
    padding: 8px 0;
}

.huati {
    padding-top: 0px;
}

.huati li {
    font-size: 10px;
    line-height: 200%;
}

.tagcloud a {
    display: block;
    border-radius: 50%;
    color: #fff;
    font-weight: bold;
    font-size: 11px;
    text-decoration: none;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
}

.b01 {
    width: 40px;
    height: 40px;
}

.b02 {
    width: 60px;
    height: 60px;
}

.b03 {
    width: 50px;
    height: 50px;

}

.b04 {
    width: 55px;
    height: 55px;

}

.co01 {
    border: 2px solid rgba(5, 118, 254, 1);
    box-shadow: inset 0 0 16px rgba(5, 118, 254, 1);
}

.co02 {
    border: 2px solid rgba(238, 255, 65, 1);
    box-shadow: inset 0 0 16px rgba(238, 255, 65, 1);
}

.co03 {
    border: 2px solid rgba(26, 121, 181, 1);
    box-shadow: inset 0 0 16px rgba(26, 121, 181, 1);
}

.co04 {
    border: 2px solid rgba(1, 187, 181, 1);
    box-shadow: inset 0 0 16px rgba(1, 187, 181, 1);
}

.co05 {
    border: 2px solid rgba(255, 138, 0, 1);
    box-shadow: inset 0 0 16px rgba(255, 138, 0, 1);
}

.wancheng {
    display: flex;
    align-items: center;
    justify-content: center;
}

.wancheng span {
    font-size: 11px;
    color: #fff;
}

.wancheng h3 {
    font-size: 16px;
    color: #00b4ff;
}

.wancheng h3 i {
    font-size: 10px;
    color: #fff;
}

.yuan {
    padding: 4px;
    border-radius: 100%;
    margin-left: 8px;
    border: 2px solid rgba(0, 99, 169, .8);
}

.yuan span {
    width: 50px;
    height: 50px;
    border-radius: 100%;
    background: rgba(0, 99, 169, .8);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
}

/* .btn{ position: absolute;  border-radius:2px; padding:4px 20px; opacity: .8;}
.btn1{border: 1px solid rgba(255,255,255,.5); background: #388665; left:35%; top: 30%;}
.btn2{ border: 1px solid rgba(255,255,255,.5); background: #297cc7;right:32%; top: 60%;}
.btn:hover{color: #fff; opacity:1;}
.btn1:before,.btn2:before{position: absolute; content: ''; width: 50px; height: 1px; background: #fff;}
.btn1:before{ transform: rotate(30deg); right: -65%; top: 100%}
.btn2:before{ transform: rotate(30deg); left: -65%; top: -10%}



 */



/* .box {
    transform: rotate(-30deg); 
} 

.box {
    transition: all 1s ease-in-out; 
}
.box:hover {
    background-color: red; 
}

.box {
    animation: move 2s infinite;
}
@keyframes move {
    0% { transform: translateX(0); }
    80% { transform: translateX(100px); }
}*/
</style>
