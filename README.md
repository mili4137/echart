最近又在做关于echart的项目，在做的时候很多属性的配置都忘了，为了下次用的方面，在此把一些配置记录下来。


index.html文件
为一个简单的演示页面。包含了Echarts所必须的链接文件，图表的使用方法，但不包含配置方法。

<!DOCTYPE html>
<html style="height: 100%">
<head>
    <meta charset="utf-8">
</head>
<body style="height: 100%; margin: 0">
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="container" style="height: 100%"></div>
<!--所需js文件-->
<script type="text/javascript" src="js/echarts-all-3.js"></script>
<script type="text/javascript" src="js/extension/dataTool.min.js"></script>
<script type="text/javascript" src="js/extension/jquery-2.2.4.js"></script>
<script type="text/javascript" src="js/map/js/china.js"></script>
<script type="text/javascript" src="js/map/js/world.js"></script>
<script type="text/javascript" src="js/api.js"></script>
<script type="text/javascript" src="js/extension/bmap.min.js"></script>
<script type="text/javascript" src="bar.js"></script>    <!--  自定义图表配置option对象，只需要学习这个  -->

<!--代码-->
<script type="text/javascript">
var dom = document.getElementById("container");
var myChart = echarts.init(dom);               /*  使用dom初始化echarts*/
myChart.hideLoading();                           /* 加载缓冲图  */
option={                                         /*  对应需要设置配置  */
    title:title,

};
myChart.showLoading();                          /*  去除加载缓冲图 */
myChart.setOption(option);                      /*  应用配置选项  */
if (option && typeof option === "object") {
    myChart.setOption(option, true);
}

</script>
</body>
</html>


coordinate-geo.js文件
为地理坐标系的配置参数

mytextStyle={
    color:"#333",                //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                 //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                //颜色
    borderColor:"#000",        //边框颜色
    borderWidth:0,              //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,              //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};

geo=[{
    show:true,                                  //是否显示
    map:"china",                                //地图类型。world世界地图，china中国地图
    roam:false,                                 //是否开启鼠标缩放和平移漫游。默认不开启。如果只想要开启缩放或者平移，可以设置成 'scale' 或者 'move'。设置成 true 为都开启
    center:[115.97, 29.71],                     //当前视角的中心点，用经纬度表示
    aspectScale:0.75,                           //这个参数用于 scale 地图的长宽比。
    boundingCoords: [[-180, 90], [180, -90]],  //二维数组，定义定位的左上角以及右下角分别所对应的经纬度
    zoom:1,                                     //当前视角的缩放比例
    scaleLimit:{                                //所属组件的z分层，z值小的图形会被z值大的图形覆盖
        min:1,                                  //最小的缩放值
        max:1,                                  //最大的缩放值
    },
    nameMap:{                                   //自定义地区的名称映射
        'China' : '中国'
    },
    selectedMode: false ,                      //选中模式，表示是否支持多个选中，默认关闭，支持布尔值和字符串，字符串取值可选'single'表示单选，或者'multiple'表示多选。
    label:{                                     //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等
        normal:{
            show:false,                          //是否在普通状态下显示标签。
            textStyle:mytextStyle,              //普通状态下的标签文本样式。
        },
        emphasis:{
            show:false,                         //是否在高亮状态下显示标签。
            textStyle:mytextStyle              //高亮状态下的标签文本样式。
        }
    },
    itemStyle:{                                 //地图区域的多边形 图形样式
        normal:myitemStyle,
        emphasis:myitemStyle
    },
    zlevel:0,                                   //所属图形的 zlevel 值。
    z:2,                                        //所属图形的 z 值。
    left:"10%",                                 //组件离容器左侧的距离,百分比字符串或整型数字
    top:60,                                     //组件离容器上侧的距离，百分比字符串或整型数字
    right:"auto",                               //组件离容器右侧的距离,百分比字符串或整型数字
    bottom:"auto",                              //组件离容器下侧的距离,百分比字符串或整型数字
    layoutCenter:['30%', '30%'],                //地图中心在屏幕中的位置
    layoutSize:100,                             //地图的大小,支持相对于屏幕宽高的百分比或者绝对的像素大小。
    regions:[{                                  //在地图中对特定的区域配置样式。
        name: '广东',
        itemStyle: {
            normal: {
                areaColor: 'red',
                color: 'red'
            }
        }
    }],
    silent:false,                               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
}];



coordinate-grid.js文件
为直角坐标系的配置参数

mytextStyle={
    color:"#333",                //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                 //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};


grid=[{
    show:true,                       //是否显示
    zlevel:0,                        //所属图形的Canvas分层，zlevel 大的 Canvas 会放在 zlevel 小的 Canvas 的上面
    z:2,                              //所属组件的z分层，z值小的图形会被z值大的图形覆盖
    left:"10%",                      //组件离容器左侧的距离,百分比字符串或整型数字
    top:60,                          //组件离容器上侧的距离，百分比字符串或整型数字
    right:"auto",                    //组件离容器右侧的距离,百分比字符串或整型数字
    bottom:"auto",                   //组件离容器下侧的距离,百分比字符串或整型数字
    width:"auto",                    //图例宽度
    height:"auto",                   //图例高度
    containLabel: true,               //grid 区域是否包含坐标轴的刻度标签，
    backgroundColor:"transparent", //标题背景色
    borderColor:"#ccc",              //边框颜色
    borderWidth:0,                    //边框线宽
    shadowColor:"red",               //阴影颜色
    shadowOffsetX:0,                 //阴影水平方向上的偏移距离
    shadowOffsetY:0,                 //阴影垂直方向上的偏移距离
    shadowBlur:10,                    //阴影的模糊大小
    tooltip:{                        //坐标系特定的 tooltip 设定
        show:true,                   //是否显示提示框组件，包括提示框浮层和 axisPointer
        trigger:"axis",              //触发类型 none不触发  'item' 数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。  'axis'  坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用。
        position: ['50%', '50%'],    //提示框浮层的位置，默认不设置时位置会跟随鼠标的位置,[10, 10],回掉函数，inside鼠标所在图形的内部中心位置，top、left、bottom、right鼠标所在图形上侧，左侧，下侧，右侧，
        formatter:"{b0}: {c0}<br />{b1}: {c1}", //提示框浮层内容格式器，支持字符串模板和回调函数两种形式,模板变量有 {a}, {b}，{c}，{d}，{e}，分别表示系列名，数据名，数据值等
        backgroundColor:"transparent",        //标题背景色
        borderColor:"#ccc",         //边框颜色
        borderWidth:0,               //边框线宽
        padding:5,                    //图例内边距，单位px  5  [5, 10]  [5,10,5,10]
        textStyle:mytextStyle,      //文本样式
    },
}];
xAxis=[
    {
        show:true,                //是否显示 x 轴
        gridIndex:0,              //x 轴所在的 grid 的索引，默认位于第一个 grid
        position:"bottom",       //x 轴的位置。"top"，"bottom"，默认 grid 中的第一个 x 轴在 grid 的下方（'bottom'），第二个 x 轴视第一个 x 轴的位置放在另一侧
        offset:0,                 //X 轴相对于默认位置的偏移，在相同的 position 上有多个 X 轴的时候有用
        type:"category",         //坐标轴类型。'value' 数值轴，适用于连续数据。'category' 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据。
                                   // 'time' 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。'log' 对数轴。适用于对数数据
        name:'时间',               //坐标轴名称
        nameLocation:"end",       //坐标轴名称显示位置。可选：'start','middle','end'
        nameTextStyle:mytextStyle,  //坐标轴名称的文字样式
        nameGap:15,                  //坐标轴名称与轴线之间的距离
        nameRotate:0,                //坐标轴名字旋转，角度值
        inverse:false,              //是否是反向坐标轴
        boundaryGap:true,           //类目轴中 boundaryGap 可以配置为 true 和 false。非类目轴，包括时间，数值，对数轴，boundaryGap是一个两个值的数组，分别表示数据最小值和最大值的延伸范围，可以直接设置数值或者相对的百分比，在设置 min 和 max 后无效['20%', '20%']
        min:null,                    //坐标轴刻度最小值。可以设置成特殊值 'dataMin'，此时取数据在该轴上的最小值作为最小刻度。不设置时会自动计算最小值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
        max:null,                   //坐标轴刻度最大值。可以设置成特殊值 'dataMax'，此时取数据在该轴上的最大值作为最大刻度。不设置时会自动计算最大值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
        scale:false,                //只在数值轴中（type: 'value'）有效。是否是脱离 0 值比例。设置成 true 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。在设置 min 和 max 之后该配置项无效。
        splitNumber:5,             //坐标轴的分割段数，需要注意的是这个分割段数只是个预估值，最后实际显示的段数会在这个基础上根据分割后坐标轴刻度显示的易读程度作调整
        minInterval:0,             //自动计算的坐标轴最小间隔大小,例如可以设置成1保证坐标轴分割刻度显示成整数。只在数值轴中（type: 'value'）有效。
        logBase:10,                 //对数轴的底数，只在对数轴中（type: 'log'）有效
        silent:false,              //坐标轴是否是静态无法交互
        triggerEvent:false,       //坐标轴的标签是否响应和触发鼠标事件
        axisLine:{                 //坐标 轴线
            show:true,             //是否显示坐标轴轴线
            onZero:true,           //X 轴或者 Y 轴的轴线是否在另一个轴的 0 刻度上，只有在另一个轴为数值轴且包含 0 刻度时有效
            lineStyle:mylineStyle
        },
        axisTick :{                 //坐标轴刻度相关设置
            show:true,              //是否显示坐标轴刻度。
            alignWithLabel:false,  //类目轴中在 boundaryGap 为 true 的时候有效，可以保证刻度线和标签对齐
            interval:auto,          //坐标轴刻度的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
            inside:false,           //坐标轴刻度是否朝内，默认朝外。
            length:5,                //坐标轴刻度的长度。
            lineStyle:mylineStyle
        },
        axisLabel:{                 //坐标轴刻度标签的相关设置
            show:true,              //是否显示
            interval:"auto",        //坐标轴刻度标签的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
            inside:false,           //刻度标签是否朝内，默认朝外
            rotate:0,               //刻度标签旋转的角度，在类目轴的类目标签显示不下的时候可以通过旋转防止标签之间重叠。旋转的角度从 -90 度到 90 度
            margin:8,               //刻度标签与轴线之间的距离
            formatter: function (value, index) {            //使用函数模板，函数参数分别为刻度数值（类目），刻度的索引
                return value+"kg";
            },
            showMinLabel:null,      //是否显示最小 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最小 tick 的 label）
            showMaxLabel:null,      //是否显示最大 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最大 tick 的 label）
            textStyle:mytextStyle
        },
        splitLine:{                 //坐标轴在 grid 区域中的分隔线。
            show:true,              //是否显示分隔线。默认数值轴显示，类目轴不显示。
            interval:"auto",        //坐标轴分隔线的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，可以用数值表示间隔的数据，也可以通过回调函数控制。回调函数格式如下：
            lineStyle:mylineStyle
        },
        splitArea:{                 //坐标轴在 grid 区域中的分隔区域，默认不显示。
            interval:"auto",
            show:false,             //是否显示分隔区域
            areaStyle:myareaStyle
        },
        data : ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],             //类目数据，在类目轴（type: 'category'）中有效。
        zlevel:0,                   //X 轴所有图形的 zlevel 值。
        z:0,                        //X 轴组件的所有图形的z值
    }
];
yAxis=xAxis;                        //y轴配置内容同x轴



coordinate-parallel.js文件
为平行坐标系的配置参数

mytextStyle={
    color:"#333",                //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                 //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};

parallel=[{
    show:true,                        //是否显示
    zlevel:0,                         //所属图形的Canvas分层，zlevel 大的 Canvas 会放在 zlevel 小的 Canvas 的上面
    z:2,                               //所属组件的z分层，z值小的图形会被z值大的图形覆盖
    left:"10%",                       //组件离容器左侧的距离,百分比字符串或整型数字
    top:60,                           //组件离容器上侧的距离，百分比字符串或整型数字
    right:"auto",                     //组件离容器右侧的距离,百分比字符串或整型数字
    bottom:"auto",                    //组件离容器下侧的距离,百分比字符串或整型数字
    width:"auto",                     //图例宽度
    height:"auto",                    //图例高度
    layout: "horizontal",             //布局方式，可选值为：'horizontal'：水平排布各个坐标轴。'vertical'：竖直排布各个坐标轴。
    axisExpandable:false,             //是否允许点击展开折叠 axis。
    axisExpandCenter:null,            //初始时，以哪个轴为中心展开，这里给出轴的 index。没有默认值，需要手动指定。
    axisExpandCount:0,                 //初始时，有多少个轴会处于展开状态。建议根据你的维度个数而手动指定。
    axisExpandWidth:50,                //在展开状态，轴的间距是多少，单位为像素。
    axisExpandTriggerOn:"click",      //'click'：鼠标点击的时候 expand。'mousemove'：鼠标悬浮的时候 expand。
    parallelAxisDefault:{             //配置多个 parallelAxis 时，有些值一样的属性，如果书写多遍则比较繁琐，那么可以放置在 parallel.parallelAxisDefault 里
        type:"category",               //坐标轴类型。'value' 数值轴，适用于连续数据。'category' 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据。
                                         // 'time' 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。'log' 对数轴。适用于对数数据
        name:'时间',                    //坐标轴名称
        nameLocation:"end",           //坐标轴名称显示位置。可选：'start','middle','end'
        nameTextStyle:mytextStyle,    //坐标轴名称的文字样式
        nameGap:15,                       //坐标轴名称与轴线之间的距离
        nameRotate:0,                     //坐标轴名字旋转，角度值
        inverse:false,                    //是否是反向坐标轴
        boundaryGap:true,                 //类目轴中 boundaryGap 可以配置为 true 和 false。非类目轴，包括时间，数值，对数轴，boundaryGap是一个两个值的数组，分别表示数据最小值和最大值的延伸范围，可以直接设置数值或者相对的百分比，在设置 min 和 max 后无效['20%', '20%']
        min:null,                         //坐标轴刻度最小值。可以设置成特殊值 'dataMin'，此时取数据在该轴上的最小值作为最小刻度。不设置时会自动计算最小值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
        max:null,                         //坐标轴刻度最大值。可以设置成特殊值 'dataMax'，此时取数据在该轴上的最大值作为最大刻度。不设置时会自动计算最大值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
        scale:false,                      //只在数值轴中（type: 'value'）有效。是否是脱离 0 值比例。设置成 true 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。在设置 min 和 max 之后该配置项无效。
        splitNumber:5,                    //坐标轴的分割段数，需要注意的是这个分割段数只是个预估值，最后实际显示的段数会在这个基础上根据分割后坐标轴刻度显示的易读程度作调整
        minInterval:0,                    //自动计算的坐标轴最小间隔大小,例如可以设置成1保证坐标轴分割刻度显示成整数。只在数值轴中（type: 'value'）有效。
        logBase:10,                       //对数轴的底数，只在对数轴中（type: 'log'）有效
        silent:false,                     //坐标轴是否是静态无法交互
        triggerEvent:false,              //坐标轴的标签是否响应和触发鼠标事件
        axisLine:{                        //坐标 轴线
            show:true,                    //是否显示坐标轴轴线
            onZero:true,                  //X 轴或者 Y 轴的轴线是否在另一个轴的 0 刻度上，只有在另一个轴为数值轴且包含 0 刻度时有效
            lineStyle:mylineStyle
        },
        axisTick :{                       //坐标轴刻度相关设置
            show:true,                    //是否显示坐标轴刻度。
            alignWithLabel:false,         //类目轴中在 boundaryGap 为 true 的时候有效，可以保证刻度线和标签对齐
            interval:auto,                //坐标轴刻度的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
            inside:false,                 //坐标轴刻度是否朝内，默认朝外。
            length:5,                     //坐标轴刻度的长度。
            lineStyle:mylineStyle //
        },
        axisLabel:{                     //坐标轴刻度标签的相关设置
            show:true,                  //是否显示
            interval:"auto",           //坐标轴刻度标签的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
            inside:false,               //刻度标签是否朝内，默认朝外
            rotate:0,                   //刻度标签旋转的角度，在类目轴的类目标签显示不下的时候可以通过旋转防止标签之间重叠。旋转的角度从 -90 度到 90 度
            margin:8,                   //刻度标签与轴线之间的距离
            formatter: function (value, index) { //使用函数模板，函数参数分别为刻度数值（类目），刻度的索引
                return value+"kg";
            },
            showMinLabel:null,        //是否显示最小 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最小 tick 的 label）
            showMaxLabel:null,        //是否显示最大 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最大 tick 的 label）
            textStyle:mytextStyle
        },
        data : ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],  //类目数据，在类目轴（type: 'category'）中有效。
    },

}];

parallelAxis=[
    {
        dim:0,                         //坐标轴的维度序号。
        parallelIndex:0,              //用于定义『坐标轴』对应到哪个『坐标系』中。
        realtime:true,                //是否坐标轴刷选的时候，实时刷新视图。如果设为 false，则在刷选动作结束时候，才刷新视图。大数据量时，建议设置成 false，从而避免卡顿。
        areaSelectStyle:{             //在坐标轴上可以进行框选，这里是一些框选的设置。
            width:20,                  //框选范围的宽度。
            borderWidth:1,            //选框的边框宽度。
            borderColor:'rgba(160,197,232)',  //选框的边框颜色。
            color: 'rgba(160,197,232)',         //选框的填充色。
            opacity:0.3,              //选框的透明度。
        },
        type:"category",              //坐标轴类型。'value' 数值轴，适用于连续数据。'category' 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据。
                                       // 'time' 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。'log' 对数轴。适用于对数数据
        name:'时间',                  //坐标轴名称
        nameLocation:"end",           //坐标轴名称显示位置。可选：'start','middle','end'
        nameTextStyle:mytextStyle,    //坐标轴名称的文字样式
        nameGap:15,                     //坐标轴名称与轴线之间的距离
        nameRotate:0,                  //坐标轴名字旋转，角度值
        inverse:false,                //是否是反向坐标轴
        boundaryGap:true,             //类目轴中 boundaryGap 可以配置为 true 和 false。非类目轴，包括时间，数值，对数轴，boundaryGap是一个两个值的数组，分别表示数据最小值和最大值的延伸范围，可以直接设置数值或者相对的百分比，在设置 min 和 max 后无效['20%', '20%']
        min:null,                      //坐标轴刻度最小值。可以设置成特殊值 'dataMin'，此时取数据在该轴上的最小值作为最小刻度。不设置时会自动计算最小值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
        max:null,                      //坐标轴刻度最大值。可以设置成特殊值 'dataMax'，此时取数据在该轴上的最大值作为最大刻度。不设置时会自动计算最大值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
        scale:false,                   //只在数值轴中（type: 'value'）有效。是否是脱离 0 值比例。设置成 true 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。在设置 min 和 max 之后该配置项无效。
        splitNumber:5,                 //坐标轴的分割段数，需要注意的是这个分割段数只是个预估值，最后实际显示的段数会在这个基础上根据分割后坐标轴刻度显示的易读程度作调整
        minInterval:0,                 //自动计算的坐标轴最小间隔大小,例如可以设置成1保证坐标轴分割刻度显示成整数。只在数值轴中（type: 'value'）有效。
        logBase:10,                    //对数轴的底数，只在对数轴中（type: 'log'）有效
        silent:false,                 //坐标轴是否是静态无法交互
        triggerEvent:false,           //坐标轴的标签是否响应和触发鼠标事件
        axisLine:{                     //坐标 轴线
            show:true,                 //是否显示坐标轴轴线
            onZero:true,               //X 轴或者 Y 轴的轴线是否在另一个轴的 0 刻度上，只有在另一个轴为数值轴且包含 0 刻度时有效
            lineStyle:mylineStyle
        },
        axisTick :{                   //坐标轴刻度相关设置
            show:true,                //是否显示坐标轴刻度。
            alignWithLabel:false,     //类目轴中在 boundaryGap 为 true 的时候有效，可以保证刻度线和标签对齐
            interval:auto,            //坐标轴刻度的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
            inside:false,             //坐标轴刻度是否朝内，默认朝外。
            length:5,                 //坐标轴刻度的长度。
            lineStyle:mylineStyle //
        },
        axisLabel:{                   //坐标轴刻度标签的相关设置
            show:true,                //是否显示
            interval:"auto",         //坐标轴刻度标签的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
            inside:false,             //刻度标签是否朝内，默认朝外
            rotate:0,                 //刻度标签旋转的角度，在类目轴的类目标签显示不下的时候可以通过旋转防止标签之间重叠。旋转的角度从 -90 度到 90 度
            margin:8,                 //刻度标签与轴线之间的距离
            formatter: function (value, index) { //使用函数模板，函数参数分别为刻度数值（类目），刻度的索引
                return value+"kg";
            },
            showMinLabel:null,        //是否显示最小 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最小 tick 的 label）
            showMaxLabel:null,        //是否显示最大 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最大 tick 的 label）
            textStyle:mytextStyle
        },
        data : ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],  //类目数据，在类目轴（type: 'category'）中有效。
    }
];



coordinate-polar.js文件
为极坐标系的配置参数

mytextStyle={
    color:"#333",                //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                 //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};

polar=[{
    show:true,                                  //是否显示
    zlevel:0,                                   //所属图形的Canvas分层，zlevel 大的 Canvas 会放在 zlevel 小的 Canvas 的上面
    z:2,                                         //所属组件的z分层，z值小的图形会被z值大的图形覆盖
    center:['50%', '50%'],                      //极坐标系的中心（圆心）坐标，像素值或百分比均可。设置成百分比，设置成百分比时第一项是相对于容器宽度，第二项是相对于容器高度
    radius:['20%', '70%'],                      //数组的第一项是内半径，第二项是外半径。支持设置成百分比，相对于容器高宽中较小的一项的一半。
    tooltip:{                                   //坐标系特定的 tooltip 设定
        show:true,                              //是否显示提示框组件，包括提示框浮层和 axisPointer
        trigger:"axis",                         //触发类型 none不触发  'item' 数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。  'axis'  坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用。
        position: ['50%', '50%'],               //提示框浮层的位置，默认不设置时位置会跟随鼠标的位置,[10, 10],回掉函数，inside鼠标所在图形的内部中心位置，top、left、bottom、right鼠标所在图形上侧，左侧，下侧，右侧，
        formatter:"{b0}: {c0}<br />{b1}: {c1}", //提示框浮层内容格式器，支持字符串模板和回调函数两种形式,模板变量有 {a}, {b}，{c}，{d}，{e}，分别表示系列名，数据名，数据值等
        backgroundColor:"transparent",        //标题背景色
        borderColor:"#ccc",                    //边框颜色
        borderWidth:0,                          //边框线宽
        padding:5,                               //图例内边距，单位px  5  [5, 10]  [5,10,5,10]
        textStyle:mytextStyle,                 //文本样式
    },
}];
radiusAxis=[
    {
        show:true,                     //是否显示 x 轴
        polarIndex :0,                 //x 轴所在的 grid 的索引，默认位于第一个 grid
        type:"category",              //坐标轴类型。'value' 数值轴，适用于连续数据。'category' 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据。
                                        // 'time' 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。'log' 对数轴。适用于对数数据
        name:'时间',                   //坐标轴名称
        nameLocation:"end",           //坐标轴名称显示位置。可选：'start','middle','end'
        nameTextStyle:mytextStyle,   //坐标轴名称的文字样式
        nameGap:15,                    //坐标轴名称与轴线之间的距离
        nameRotate:0,                  //坐标轴名字旋转，角度值
        inverse:false,                 //是否是反向坐标轴
        boundaryGap:true,             //类目轴中 boundaryGap 可以配置为 true 和 false。非类目轴，包括时间，数值，对数轴，boundaryGap是一个两个值的数组，分别表示数据最小值和最大值的延伸范围，可以直接设置数值或者相对的百分比，在设置 min 和 max 后无效['20%', '20%']
        min:null,                      //坐标轴刻度最小值。可以设置成特殊值 'dataMin'，此时取数据在该轴上的最小值作为最小刻度。不设置时会自动计算最小值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
        max:null,                       //坐标轴刻度最大值。可以设置成特殊值 'dataMax'，此时取数据在该轴上的最大值作为最大刻度。不设置时会自动计算最大值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
        scale:false,                    //只在数值轴中（type: 'value'）有效。是否是脱离 0 值比例。设置成 true 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。在设置 min 和 max 之后该配置项无效。
        splitNumber:5,                  //坐标轴的分割段数，需要注意的是这个分割段数只是个预估值，最后实际显示的段数会在这个基础上根据分割后坐标轴刻度显示的易读程度作调整
        minInterval:0,                  //自动计算的坐标轴最小间隔大小,例如可以设置成1保证坐标轴分割刻度显示成整数。只在数值轴中（type: 'value'）有效。
        logBase:10,                     //对数轴的底数，只在对数轴中（type: 'log'）有效
        silent:false,                   //坐标轴是否是静态无法交互
        triggerEvent:false,             //坐标轴的标签是否响应和触发鼠标事件
        axisLine:{                      //坐标 轴线
            show:true,                  //是否显示坐标轴轴线
            onZero:true,                //X 轴或者 Y 轴的轴线是否在另一个轴的 0 刻度上，只有在另一个轴为数值轴且包含 0 刻度时有效
            lineStyle:mylineStyle
        },
        axisTick :{                     //坐标轴刻度相关设置
            show:true,                  //是否显示坐标轴刻度。
            alignWithLabel:false,       //类目轴中在 boundaryGap 为 true 的时候有效，可以保证刻度线和标签对齐
            interval:auto,              //坐标轴刻度的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
            inside:false,               //坐标轴刻度是否朝内，默认朝外。
            length:5,                   //坐标轴刻度的长度。
            lineStyle:mylineStyle //
        },
        axisLabel:{                     //坐标轴刻度标签的相关设置
            show:true,                  //是否显示
            interval:"auto",            //坐标轴刻度标签的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
            inside:false,               //刻度标签是否朝内，默认朝外
            rotate:0,                   //刻度标签旋转的角度，在类目轴的类目标签显示不下的时候可以通过旋转防止标签之间重叠。旋转的角度从 -90 度到 90 度
            margin:8,                   //刻度标签与轴线之间的距离
            formatter: function (value, index) { //使用函数模板，函数参数分别为刻度数值（类目），刻度的索引
                return value+"kg";
            },
            showMinLabel:null,          //是否显示最小 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最小 tick 的 label）
            showMaxLabel:null,          //是否显示最大 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最大 tick 的 label）
            textStyle:mytextStyle
        },
        splitLine:{                     //坐标轴在 grid 区域中的分隔线。
            show:true,                  //是否显示分隔线。默认数值轴显示，类目轴不显示。
            interval:"auto",            //坐标轴分隔线的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，可以用数值表示间隔的数据，也可以通过回调函数控制。回调函数格式如下：
            lineStyle:mylineStyle
        },
        splitArea:{                     //坐标轴在 grid 区域中的分隔区域，默认不显示。
            interval:"auto",
            show:false,                 //是否显示分隔区域
            areaStyle:myareaStyle
        },
        data : ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],  //类目数据，在类目轴（type: 'category'）中有效。
        zlevel:0,                       //X 轴所有图形的 zlevel 值。
        z:0,                            //X 轴组件的所有图形的z值
    }
];
angleAxis=[{                            //y轴配置内容同x轴
    polarIndex:0,                       //角度轴所在的极坐标系的索引，默认使用第一个极坐标系
    startAngle:90,                      //起始刻度的角度，默认为 90 度，即圆心的正上方。0 度为圆心的正右方。
    clockwise:true,                     //刻度增长是否按顺时针，默认顺时针。
    type:"category",                    //坐标轴类型。'value' 数值轴，适用于连续数据。'category' 类目轴，适用于离散的类目数据，为该类型时必须通过 data 设置类目数据。
                                          // 'time' 时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。'log' 对数轴。适用于对数数据
    inverse:false,                      //是否是反向坐标轴
    boundaryGap:true,                   //类目轴中 boundaryGap 可以配置为 true 和 false。非类目轴，包括时间，数值，对数轴，boundaryGap是一个两个值的数组，分别表示数据最小值和最大值的延伸范围，可以直接设置数值或者相对的百分比，在设置 min 和 max 后无效['20%', '20%']
    min:null,                            //坐标轴刻度最小值。可以设置成特殊值 'dataMin'，此时取数据在该轴上的最小值作为最小刻度。不设置时会自动计算最小值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
    max:null,                           //坐标轴刻度最大值。可以设置成特殊值 'dataMax'，此时取数据在该轴上的最大值作为最大刻度。不设置时会自动计算最大值保证坐标轴刻度的均匀分布。在类目轴中，也可以设置为类目的序数
    scale:false,                        //只在数值轴中（type: 'value'）有效。是否是脱离 0 值比例。设置成 true 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。在设置 min 和 max 之后该配置项无效。
    splitNumber:5,                      //坐标轴的分割段数，需要注意的是这个分割段数只是个预估值，最后实际显示的段数会在这个基础上根据分割后坐标轴刻度显示的易读程度作调整
    minInterval:0,                      //自动计算的坐标轴最小间隔大小,例如可以设置成1保证坐标轴分割刻度显示成整数。只在数值轴中（type: 'value'）有效。
    logBase:10,                         //对数轴的底数，只在对数轴中（type: 'log'）有效
    silent:false,                       //坐标轴是否是静态无法交互
    triggerEvent:false,                 //坐标轴的标签是否响应和触发鼠标事件
    axisLine:{                           //坐标 轴线
        show:true,                       //是否显示坐标轴轴线
        onZero:true,                     //X 轴或者 Y 轴的轴线是否在另一个轴的 0 刻度上，只有在另一个轴为数值轴且包含 0 刻度时有效
        lineStyle:mylineStyle
    },
    axisTick :{                         //坐标轴刻度相关设置
        show:true,                      //是否显示坐标轴刻度。
        alignWithLabel:false,           //类目轴中在 boundaryGap 为 true 的时候有效，可以保证刻度线和标签对齐
        interval:auto,                  //坐标轴刻度的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
        inside:false,                   //坐标轴刻度是否朝内，默认朝外。
        length:5,                       //坐标轴刻度的长度。
        lineStyle:mylineStyle //
    },
    axisLabel:{                         //坐标轴刻度标签的相关设置
        show:true,                      //是否显示
        interval:"auto",                //坐标轴刻度标签的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
        inside:false,                   //刻度标签是否朝内，默认朝外
        rotate:0,                       //刻度标签旋转的角度，在类目轴的类目标签显示不下的时候可以通过旋转防止标签之间重叠。旋转的角度从 -90 度到 90 度
        margin:8,                       //刻度标签与轴线之间的距离
        formatter: function (value, index) { //使用函数模板，函数参数分别为刻度数值（类目），刻度的索引
            return value+"kg";
        },
        showMinLabel:null,          //是否显示最小 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最小 tick 的 label）
        showMaxLabel:null,          //是否显示最大 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最大 tick 的 label）
        textStyle:mytextStyle
    },
    splitLine:{                     //坐标轴在 grid 区域中的分隔线。
        show:true,                  //是否显示分隔线。默认数值轴显示，类目轴不显示。
        interval:"auto",            //坐标轴分隔线的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，可以用数值表示间隔的数据，也可以通过回调函数控制。回调函数格式如下：
        lineStyle:mylineStyle
    },
    splitArea:{                     //坐标轴在 grid 区域中的分隔区域，默认不显示。
        interval:"auto",
        show:false,                 //是否显示分隔区域
        areaStyle:myareaStyle
    },
    data : ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],  //类目数据，在类目轴（type: 'category'）中有效。
    zlevel:0,                       //所属图形的 zlevel 值。
    z:0,                            //组件的所属图形的z值
}];



coordinate-radar.js文件
为雷达坐标系的配置参数

mytextStyle={
    color:"#333",                //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                 //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};


radar=[{
    center:['50%', '50%'],      //中心（圆心）坐标，数组的第一项是横坐标，第二项是纵坐标。支持设置成百分比，设置成百分比时第一项是相对于容器宽度，第二项是相对于容器高度。
    radius:"75%",               //数组的第一项是内半径，第二项是外半径。支持设置成百分比，相对于容器高宽中较小的一项的一半。
    startAngle:90,              //起始刻度的角度，默认为 90 度，即圆心的正上方。0 度为圆心的正右方。
    name:{                      //雷达图每个指示器名称的配置项。
        show:true,              //是否显示指示器名称。
        formatter:function (value, indicator) {  //用回调函数，第一个参数是指示器名称，第二个参数是指示器配置项
            return '【' + value + '】';
        },
        textStyle:mytextStyle
    },
    nameGap:15,                 //指示器名称和指示器轴的距离
    splitNumber:5,              //指示器轴的分割段数
    scale:false,                //只在数值轴中（type: 'value'）有效。是否是脱离 0 值比例。设置成 true 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。在设置 min 和 max 之后该配置项无效。
    shape:"polygon",            //雷达图绘制类型，支持 'polygon' 和 'circle'。
    silent:false,               //坐标轴是否是静态无法交互
    triggerEvent:false,         //坐标轴的标签是否响应和触发鼠标事件
    axisLine:{                   //坐标 轴线
        show:true,               //是否显示坐标轴轴线
        onZero:true,            //X 轴或者 Y 轴的轴线是否在另一个轴的 0 刻度上，只有在另一个轴为数值轴且包含 0 刻度时有效
        lineStyle:mylineStyle
    },
    axisTick :{                 //坐标轴刻度相关设置
        show:true,              //是否显示坐标轴刻度。
        alignWithLabel:false,   //类目轴中在 boundaryGap 为 true 的时候有效，可以保证刻度线和标签对齐
        interval:auto,          //坐标轴刻度的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
        inside:false,           //坐标轴刻度是否朝内，默认朝外。
        length:5,               //坐标轴刻度的长度。
        lineStyle:mylineStyle //
    },
    axisLabel:{                 //坐标轴刻度标签的相关设置
        show:true,              //是否显示
        interval:"auto",        //坐标轴刻度标签的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，如果值为 2，表示隔两个标签显示一个标签，以此类推
        inside:false,           //刻度标签是否朝内，默认朝外
        rotate:0,               //刻度标签旋转的角度，在类目轴的类目标签显示不下的时候可以通过旋转防止标签之间重叠。旋转的角度从 -90 度到 90 度
        margin:8,               //刻度标签与轴线之间的距离
        formatter: function (value, index) { //使用函数模板，函数参数分别为刻度数值（类目），刻度的索引
            return value+"kg";
        },
        showMinLabel:null,      //是否显示最小 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最小 tick 的 label）
        showMaxLabel:null,      //是否显示最大 tick 的 label。可取值 true, false, null。默认自动判定（即如果标签重叠，不会显示最大 tick 的 label）
        textStyle:mytextStyle
    },
    splitLine:{                 //坐标轴在 grid 区域中的分隔线。
        show:true,               //是否显示分隔线。默认数值轴显示，类目轴不显示。
        interval:"auto",        //坐标轴分隔线的显示间隔，在类目轴中有效。默认会采用标签不重叠的策略间隔显示标签。可以设置成 0 强制显示所有标签。如果设置为 1，表示『隔一个标签显示一个标签』，可以用数值表示间隔的数据，也可以通过回调函数控制。回调函数格式如下：
        lineStyle:mylineStyle
    },
    splitArea:{                 //坐标轴在 grid 区域中的分隔区域，默认不显示。
        interval:"auto",
        show:false,             //是否显示分隔区域
        areaStyle:myareaStyle
    },
    indicator: [                //雷达图的指示器，用来指定雷达图中的多个变量（维度）
        { name: '销售（sales）', max: 6500},
        { name: '管理（Administration）', max: 16000},
        { name: '信息技术（Information Techology）', max: 30000},
        { name: '客服（Customer Support）', max: 38000},
        { name: '研发（Development）', max: 52000},
        { name: '市场（Marketing）', max: 25000}
    ],
    zlevel:0,                   //所属图形的 zlevel 值。
    z:0,                        //组件的所属图形的z值
}];



index.js文件
为图表颜色、背景、标题、提示框、工具框、图例、缩放设置、视觉映射等内容

/*chart       是指一个完整的图表，如折线图，饼图等“基本”图表类型或由基本图表组合而成的“混搭”图表，可能包括坐标轴、图例等
 axis        直角坐标系中的一个坐标轴，坐标轴可分为类目轴和数值轴
 xAxis       直角坐标系中的横轴，通常并默认为类目轴
 yAxis       直角坐标系中的纵轴，通常并默认为数值轴
 grid        直角坐标系中除坐标轴外的绘图网格
 legend      图例，表述数据和图形的关联
 dataRange   值域选择，常用于展现地域数据时选择值域范围
 dataZoom    数据区域缩放，常用于展现大数据时选择可视范围
 toolbox     辅助工具箱，辅助功能，如添加标线，框选缩放等
 tooltip     气泡提示框，常用于展现更详细的数据
 timeline    时间轴，常用于展现同一组数据在时间维度上的多份数据
 series      数据系列，一个图表可能包含多个系列，每一个系列可能包含多个数据


 line        折线图，堆积折线图，区域图，堆积区域图。
 bar         柱形图（纵向），堆积柱形图，条形图（横向），堆积条形图。
 scatter     散点图，气泡图。散点图至少需要横纵两个数据，更高维度数据加入时可以映射为颜色或大小，当映射到大小时则为气泡图
 k           K线图，蜡烛图。常用于展现股票交易数据。
 pie         饼图，圆环图。饼图支持两种（半径、面积）南丁格尔玫瑰图模式。
 radar       雷达图，填充雷达图。高维度数据展现的常用图表。
 chord       和弦图。常用于展现关系数据，外层为圆环图，可体现数据占比关系，内层为各个扇形间相互连接的弦，可体现关系数据
 force       力导布局图。常用于展现复杂关系网络聚类布局。
 map         地图。内置世界地图、中国及中国34个省市自治区地图数据、可通过标准GeoJson扩展地图类型。支持svg扩展类地图应用，如室内地图、运动场、物件构造等。*/
color=['#c23531','#2f4554', '#61a0a8', '#d48265', '#91c7ae','#749f83',  '#ca8622', '#bda29a','#6e7074', '#546570', '#c4ccd3'];//调色盘颜色列表。如果系列没有设置颜色，则会依次循环从该列表中取颜色作为系列颜色
backgroundColor="#000000";   //背景色，默认无背景。 'rgb(128, 128, 128)'， 'rgba(128, 128, 128, 0.5)'，除了纯色之外颜色也支持渐变色和纹理填充
mytextStyle={
    color:"#333",                           //文字颜色
    fontStyle:"normal",                     //italic斜体  oblique倾斜
    fontWeight:"normal",                    //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",                //字体系列
    fontSize:18,                              //字体大小
};

title={
    show:true,                                 //是否显示
    text:"大标题",                             //大标题
    subtext:"小标题",                          //小标题
    sublink:"http://www.baidu.com",          //小标题链接
    target:"blank",                            //'self' 当前窗口打开，'blank' 新窗口打开
    subtarget:"blank",                        //小标题打开链接的窗口
    textAlign:"center",                       //文本水平对齐
    textBaseline:"top",                       //文本垂直对齐
    textStyle:mytextStyle,                     //标题样式
    subtextStyle:mytextStyle,                 //小标题样式
    padding:5,                                  //标题内边距 5  [5, 10]  [5,10,5,10]
    itemGap:10,                                 //大小标题间距
    zlevel:0,                                   //所属图形的Canvas分层，zlevel 大的 Canvas 会放在 zlevel 小的 Canvas 的上面
    z:2,                                         //所属组件的z分层，z值小的图形会被z值大的图形覆盖
    left:"center",                              //组件离容器左侧的距离,'left', 'center', 'right','20%'
    top:"top",                                   //组件离容器上侧的距离,'top', 'middle', 'bottom','20%'
    right:"auto",                               //组件离容器右侧的距离,'20%'
    bottom:"auto",                              //组件离容器下侧的距离,'20%'
    backgroundColor:"transparent",            //标题背景色
    borderColor:"#ccc",                         //边框颜色
    borderWidth:0,                               //边框线宽
    shadowColor:"red",                          //阴影颜色
    shadowOffsetX:0,                            //阴影水平方向上的偏移距离
    shadowOffsetY:0,                            //阴影垂直方向上的偏移距离
    shadowBlur:10,                               //阴影的模糊大小
};

tooltip ={                                      //提示框组件
    trigger: 'item',                            //触发类型,'item'数据项图形触发，主要在散点图，饼图等无类目轴的图表中使用。 'axis'坐标轴触发，主要在柱状图，折线图等会使用类目轴的图表中使用。
    triggerOn:"mousemove",                      //提示框触发的条件,'mousemove'鼠标移动时触发。'click'鼠标点击时触发。'mousemove|click'同时鼠标移动和点击时触发。'none'不在 'mousemove' 或 'click' 时触发
    showContent:true,                           //是否显示提示框浮层
    alwaysShowContent:true,                     //是否永远显示提示框内容
    showDelay:0,                                  //浮层显示的延迟，单位为 ms
    hideDelay:100,                                //浮层隐藏的延迟，单位为 ms
    enterable:false,                             //鼠标是否可进入提示框浮层中
    confine:false,                               //是否将 tooltip 框限制在图表的区域内
    transitionDuration:0.4,                      //提示框浮层的移动动画过渡时间，单位是 s,设置为 0 的时候会紧跟着鼠标移动
    position:['50%', '50%'],                    //提示框浮层的位置，默认不设置时位置会跟随鼠标的位置,[10, 10],回掉函数，inside鼠标所在图形的内部中心位置，top、left、bottom、right鼠标所在图形上侧，左侧，下侧，右侧，
    formatter:"{b0}: {c0}<br />{b1}: {c1}",     //提示框浮层内容格式器，支持字符串模板和回调函数两种形式,模板变量有 {a}, {b}，{c}，{d}，{e}，分别表示系列名，数据名，数据值等
    backgroundColor:"transparent",            //标题背景色
    borderColor:"#ccc",                        //边框颜色
    borderWidth:0,                              //边框线宽
    padding:5,                                  //图例内边距，单位px  5  [5, 10]  [5,10,5,10]
    textStyle:mytextStyle,                     //文本样式
};

toolbox={
    show : true,                                 //是否显示工具栏组件
    orient:"horizontal",                        //工具栏 icon 的布局朝向'horizontal' 'vertical'
    itemSize:15,                                 //工具栏 icon 的大小
    itemGap:10,                                  //工具栏 icon 每项之间的间隔
    showTitle:true,                             //是否在鼠标 hover 的时候显示每个工具 icon 的标题
    feature : {
        mark : {                                 // '辅助线开关'
            show: true
        },
        dataView : {                            //数据视图工具，可以展现当前图表所用的数据，编辑后可以动态更新
            show: true,                         //是否显示该工具。
            title:"数据视图",
            readOnly: false,                    //是否不可编辑（只读）
            lang: ['数据视图', '关闭', '刷新'],  //数据视图上有三个话术，默认是['数据视图', '关闭', '刷新']
            backgroundColor:"#fff",             //数据视图浮层背景色。
            textareaColor:"#fff",               //数据视图浮层文本输入区背景色
            textareaBorderColor:"#333",         //数据视图浮层文本输入区边框颜色
            textColor:"#000",                    //文本颜色。
            buttonColor:"#c23531",              //按钮颜色。
            buttonTextColor:"#fff",             //按钮文本颜色。
        },
        magicType: {                            //动态类型切换
            show: true,
            title:"切换",                       //各个类型的标题文本，可以分别配置。
            type: ['line', 'bar'],              //启用的动态类型，包括'line'（切换为折线图）, 'bar'（切换为柱状图）, 'stack'（切换为堆叠模式）, 'tiled'（切换为平铺模式）
        },
        restore : {                             //配置项还原。
            show: true,                         //是否显示该工具。
            title:"还原",
        },
        saveAsImage : {                         //保存为图片。
            show: true,                         //是否显示该工具。
            type:"png",                         //保存的图片格式。支持 'png' 和 'jpeg'。
            name:"pic1",                        //保存的文件名称，默认使用 title.text 作为名称
            backgroundColor:"#ffffff",        //保存的图片背景色，默认使用 backgroundColor，如果backgroundColor不存在的话会取白色
            title:"保存为图片",
            pixelRatio:1                        //保存图片的分辨率比例，默认跟容器相同大小，如果需要保存更高分辨率的，可以设置为大于 1 的值，例如 2
        },
        dataZoom :{                             //数据区域缩放。目前只支持直角坐标系的缩放
            show: true,                         //是否显示该工具。
            title:"缩放",                       //缩放和还原的标题文本
            xAxisIndex:0,                       //指定哪些 xAxis 被控制。如果缺省则控制所有的x轴。如果设置为 false 则不控制任何x轴。如果设置成 3 则控制 axisIndex 为 3 的x轴。如果设置为 [0, 3] 则控制 axisIndex 为 0 和 3 的x轴
            yAxisIndex:false,                   //指定哪些 yAxis 被控制。如果缺省则控制所有的y轴。如果设置为 false 则不控制任何y轴。如果设置成 3 则控制 axisIndex 为 3 的y轴。如果设置为 [0, 3] 则控制 axisIndex 为 0 和 3 的y轴
        },
    },
    zlevel:0,                                   //所属图形的Canvas分层，zlevel 大的 Canvas 会放在 zlevel 小的 Canvas 的上面
    z:2,                                         //所属组件的z分层，z值小的图形会被z值大的图形覆盖
    left:"center",                              //组件离容器左侧的距离,'left', 'center', 'right','20%'
    top:"top",                                   //组件离容器上侧的距离,'top', 'middle', 'bottom','20%'
    right:"auto",                               //组件离容器右侧的距离,'20%'
    bottom:"auto",                              //组件离容器下侧的距离,'20%'
    width:"auto",                               //图例宽度
    height:"auto",                              //图例高度
};



legend={
    show:true,                                  //是否显示
    zlevel:0,                                   //所属图形的Canvas分层，zlevel 大的 Canvas 会放在 zlevel 小的 Canvas 的上面
    z:2,                                         //所属组件的z分层，z值小的图形会被z值大的图形覆盖
    left:"center",                              //组件离容器左侧的距离,'left', 'center', 'right','20%'
    top:"top",                                   //组件离容器上侧的距离,'top', 'middle', 'bottom','20%'
    right:"auto",                               //组件离容器右侧的距离,'20%'
    bottom:"auto",                              //组件离容器下侧的距离,'20%'
    width:"auto",                               //图例宽度
    height:"auto",                              //图例高度
    orient:"horizontal",                        //图例排列方向
    align:"auto",                               //图例标记和文本的对齐,left,right
    padding:5,                                   //图例内边距，单位px  5  [5, 10]  [5,10,5,10]
    itemGap:10,                                  //图例每项之间的间隔
    itemWidth:25,                               //图例标记的图形宽度
    itemHeight:14,                              //图例标记的图形高度
    formatter:function (name) {                 //用来格式化图例文本，支持字符串模板和回调函数两种形式。模板变量为图例名称 {name}
        return 'Legend ' + name;
    },
    selectedMode:"single",                    //图例选择的模式,true开启,false关闭,single单选,multiple多选
    inactiveColor:"#ccc",                     //图例关闭时的颜色
    textStyle:mytextStyle,                    //文本样式
    data:['类别1', '类别2', '类别3'],          //series中根据名称区分
    backgroundColor:"transparent",            //标题背景色
    borderColor:"#ccc",                         //边框颜色
    borderWidth:0,                               //边框线宽
    shadowColor:"red",                          //阴影颜色
    shadowOffsetX:0,                            //阴影水平方向上的偏移距离
    shadowOffsetY:0,                            //阴影垂直方向上的偏移距离
    shadowBlur:10,                               //阴影的模糊大小
};

dataZoom=[                                      //区域缩放
    {
        id: 'dataZoomX',
        show:true,                              //是否显示 组件。如果设置为 false，不会显示，但是数据过滤的功能还存在。
        backgroundColor:"rgba(47,69,84,0)",  //组件的背景颜色
        type: 'slider',                         //slider表示有滑动块的，inside表示内置的
        dataBackground:{                        //数据阴影的样式。
            lineStyle:mylineStyle,              //阴影的线条样式
            areaStyle:myareaStyle,              //阴影的填充样式
        },
        fillerColor:"rgba(167,183,204,0.4)",  //选中范围的填充颜色。
        borderColor:"#ddd",                     //边框颜色。
        filterMode: 'filter',                   //'filter'：当前数据窗口外的数据，被 过滤掉。即 会 影响其他轴的数据范围。每个数据项，只要有一个维度在数据窗口外，整个数据项就会被过滤掉。
                                                  //'weakFilter'：当前数据窗口外的数据，被 过滤掉。即 会 影响其他轴的数据范围。每个数据项，只有当全部维度都在数据窗口同侧外部，整个数据项才会被过滤掉。
                                                  //'empty'：当前数据窗口外的数据，被 设置为空。即 不会 影响其他轴的数据范围。
                                                  //'none': 不过滤数据，只改变数轴范围。
        xAxisIndex:0,                            //设置 dataZoom-inside 组件控制的 x轴,可以用数组表示多个轴
        yAxisIndex:[0,2],                        //设置 dataZoom-inside 组件控制的 y轴,可以用数组表示多个轴
        radiusAxisIndex:3,                       //设置 dataZoom-inside 组件控制的 radius 轴,可以用数组表示多个轴
        angleAxisIndex:[0,2],                    //设置 dataZoom-inside 组件控制的 angle 轴,可以用数组表示多个轴
        start: 30,                                //数据窗口范围的起始百分比,表示30%
        end: 70,                                  //数据窗口范围的结束百分比,表示70%
        startValue:10,                           //数据窗口范围的起始数值
        endValue:100,                            //数据窗口范围的结束数值。
        orient:"horizontal",                    //布局方式是横还是竖。不仅是布局方式，对于直角坐标系而言，也决定了，缺省情况控制横向数轴还是纵向数轴。'horizontal'：水平。'vertical'：竖直。
        zoomLock:false,                          //是否锁定选择区域（或叫做数据窗口）的大小。如果设置为 true 则锁定选择区域的大小，也就是说，只能平移，不能缩放。
        throttle:100,                             //设置触发视图刷新的频率。单位为毫秒（ms）。
        zoomOnMouseWheel:true,                  //如何触发缩放。可选值为：true：表示不按任何功能键，鼠标滚轮能触发缩放。false：表示鼠标滚轮不能触发缩放。'shift'：表示按住 shift 和鼠标滚轮能触发缩放。'ctrl'：表示按住 ctrl 和鼠标滚轮能触发缩放。'alt'：表示按住 alt 和鼠标滚轮能触发缩放。
        moveOnMouseMove:true,                   //如何触发数据窗口平移。true：表示不按任何功能键，鼠标移动能触发数据窗口平移。false：表示鼠标滚轮不能触发缩放。'shift'：表示按住 shift 和鼠标移动能触发数据窗口平移。'ctrl'：表示按住 ctrl 和鼠标移动能触发数据窗口平移。'alt'：表示按住 alt 和鼠标移动能触发数据窗口平移。
        left:"center",                           //组件离容器左侧的距离,'left', 'center', 'right','20%'
        top:"top",                                //组件离容器上侧的距离,'top', 'middle', 'bottom','20%'
        right:"auto",                             //组件离容器右侧的距离,'20%'
        bottom:"auto",                            //组件离容器下侧的距离,'20%'

    },
    {
        id: 'dataZoomY',
        type: 'inside',
        filterMode: 'empty',
        disabled:false,                         //是否停止组件的功能。
        xAxisIndex:0,                           //设置 dataZoom-inside 组件控制的 x轴,可以用数组表示多个轴
        yAxisIndex:[0,2],                       //设置 dataZoom-inside 组件控制的 y轴,可以用数组表示多个轴
        radiusAxisIndex:3,                      //设置 dataZoom-inside 组件控制的 radius 轴,可以用数组表示多个轴
        angleAxisIndex:[0,2],                   //设置 dataZoom-inside 组件控制的 angle 轴,可以用数组表示多个轴
        start: 30,                               //数据窗口范围的起始百分比,表示30%
        end: 70,                                  //数据窗口范围的结束百分比,表示70%
        startValue:10,                           //数据窗口范围的起始数值
        endValue:100,                            //数据窗口范围的结束数值。
        orient:"horizontal",                    //布局方式是横还是竖。不仅是布局方式，对于直角坐标系而言，也决定了，缺省情况控制横向数轴还是纵向数轴。'horizontal'：水平。'vertical'：竖直。
        zoomLock:false,                          //是否锁定选择区域（或叫做数据窗口）的大小。如果设置为 true 则锁定选择区域的大小，也就是说，只能平移，不能缩放。
        throttle:100,                             //设置触发视图刷新的频率。单位为毫秒（ms）。
        zoomOnMouseWheel:true,                   //如何触发缩放。可选值为：true：表示不按任何功能键，鼠标滚轮能触发缩放。false：表示鼠标滚轮不能触发缩放。'shift'：表示按住 shift 和鼠标滚轮能触发缩放。'ctrl'：表示按住 ctrl 和鼠标滚轮能触发缩放。'alt'：表示按住 alt 和鼠标滚轮能触发缩放。
        moveOnMouseMove:true,                    //如何触发数据窗口平移。true：表示不按任何功能键，鼠标移动能触发数据窗口平移。false：表示鼠标滚轮不能触发缩放。'shift'：表示按住 shift 和鼠标移动能触发数据窗口平移。'ctrl'：表示按住 ctrl 和鼠标移动能触发数据窗口平移。'alt'：表示按住 alt 和鼠标移动能触发数据窗口平移。
    }
];

visualMap=[                                     //视觉映射组件，用于进行『视觉编码』，也就是将数据映射到视觉元素。视觉元素可以是：symbol: 图元的图形类别。symbolSize: 图元的大小。color: 图元的颜色。
                                                 // colorAlpha: 图元的颜色的透明度。opacity: 图元以及其附属物（如文字标签）的透明度。colorLightness: 颜色的明暗度。colorSaturation: 颜色的饱和度。colorHue: 颜色的色调。
    {
        show:true,                              //是否显示 visualMap-continuous 组件。如果设置为 false，不会显示，但是数据映射的功能还存在
        type: 'continuous',                     // 定义为连续型 viusalMap
        min:10,                                  //指定 visualMapContinuous 组件的允许的最小值
        max:100,                                 //指定 visualMapContinuous 组件的允许的最大值
        range:[15, 40],                          //指定手柄对应数值的位置。range 应在 min max 范围内
        calculable:true,                        //是否显示拖拽用的手柄（手柄能拖拽调整选中范围）
        realtime:true,                          //拖拽时，是否实时更新
        inverse:false,                          //是否反转 visualMap 组件
        precision:0,                            //数据展示的小数精度，默认为0，无小数点
        itemWidth:20,                           //图形的宽度，即长条的宽度。
        itemHeight:140,                         //图形的高度，即长条的高度。
        align:"auto",                           //指定组件中手柄和文字的摆放位置.可选值为：'auto' 自动决定。'left' 手柄和label在右。'right' 手柄和label在左。'top' 手柄和label在下。'bottom' 手柄和label在上。
        text:['High', 'Low'],                   //两端的文本
        textGap:10,                              //两端文字主体之间的距离，单位为px
        dimension:2,                            //指定用数据的『哪个维度』，映射到视觉元素上。『数据』即 series.data。 可以把 series.data 理解成一个二维数组,其中每个列是一个维度,默认取 data 中最后一个维度
        seriesIndex:1,                          //指定取哪个系列的数据，即哪个系列的 series.data,默认取所有系列
        hoverLink:true,                         //鼠标悬浮到 visualMap 组件上时，鼠标位置对应的数值 在 图表中对应的图形元素，会高亮
        inRange:{                               //定义 在选中范围中 的视觉元素
            color: ['#121122', 'rgba(3,4,5,0.4)', 'red'],
            symbolSize: [30, 100]
        },
        outOfRange:{  //定义 在选中范围外 的视觉元素。
            color: ['#121122', 'rgba(3,4,5,0.4)', 'red'],
            symbolSize: [30, 100]
        },
        zlevel:0,                                   //所属图形的Canvas分层，zlevel 大的 Canvas 会放在 zlevel 小的 Canvas 的上面
        z:2,                                         //所属组件的z分层，z值小的图形会被z值大的图形覆盖
        left:"center",                              //组件离容器左侧的距离,'left', 'center', 'right','20%'
        top:"top",                                   //组件离容器上侧的距离,'top', 'middle', 'bottom','20%'
        right:"auto",                               //组件离容器右侧的距离,'20%'
        bottom:"auto",                              //组件离容器下侧的距离,'20%'
        orient:"vertical",                         //图例排列方向
        padding:5,                                   //图例内边距，单位px  5  [5, 10]  [5,10,5,10]
        backgroundColor:"transparent",            //标题背景色
        borderColor:"#ccc",                         //边框颜色
        borderWidth:0,                               //边框线宽
        textStyle:mytextStyle,                      //文本样式
        formatter: function (value) {                 //标签的格式化工具。
            return 'aaaa' + value;                    // 范围标签显示内容。
        }
    },
    {
        show:true,                          //是否显示 visualMap-continuous 组件。如果设置为 false，不会显示，但是数据映射的功能还存在
        type: 'piecewise',                  // 定义为分段型 visualMap
        splitNumber:5,                      //对于连续型数据，自动平均切分成几段。默认为5段
        pieces: [                           //自定义『分段式视觉映射组件（visualMapPiecewise）』的每一段的范围，以及每一段的文字，以及每一段的特别的样式
            {min: 1500},                     // 不指定 max，表示 max 为无限大（Infinity）。
            {min: 900, max: 1500},
            {min: 310, max: 1000},
            {min: 200, max: 300},
            {min: 10, max: 200, label: '10 到 200（自定义label）'},
            {value: 123, label: '123（自定义特殊颜色）', color: 'grey'}, // 表示 value 等于 123 的情况。
            {max: 5}                        // 不指定 min，表示 min 为无限大（-Infinity）。
        ],
        categories:['严重污染', '重度污染', '中度污染', '轻度污染', '良', '优'],  //用于表示离散型数据（或可以称为类别型数据、枚举型数据）的全集
        min:10,                             //指定 visualMapContinuous 组件的允许的最小值
        max:100,                             //指定 visualMapContinuous 组件的允许的最大值
        minOpen:true,                       //界面上会额外多出一个『< min』的选块
        maxOpen:true,                       //界面上会额外多出一个『> max』的选块。
        selectedMode:"multiple",           //选择模式，可以是：'multiple'（多选）。'single'（单选）。
        inverse:false,                      //是否反转 visualMap 组件
        precision:0,                        //数据展示的小数精度，默认为0，无小数点
        itemWidth:20,                       //图形的宽度，即长条的宽度。
        itemHeight:140,                     //图形的高度，即长条的高度。
        align:"auto",                       //指定组件中手柄和文字的摆放位置.可选值为：'auto' 自动决定。'left' 手柄和label在右。'right' 手柄和label在左。'top' 手柄和label在下。'bottom' 手柄和label在上。
        text:['High', 'Low'],               //两端的文本
        textGap:10,                          //两端文字主体之间的距离，单位为px
        showLabel:true,                     //是否显示每项的文本标签
        itemGap:10,                          //每两个图元之间的间隔距离，单位为px
        itemSymbol:"roundRect",             //默认的图形。可选值为： 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
        dimension:2,                          //指定用数据的『哪个维度』，映射到视觉元素上。『数据』即 series.data。 可以把 series.data 理解成一个二维数组,其中每个列是一个维度,默认取 data 中最后一个维度
        seriesIndex:1,                        //指定取哪个系列的数据，即哪个系列的 series.data,默认取所有系列
        hoverLink:true,                      //鼠标悬浮到 visualMap 组件上时，鼠标位置对应的数值 在 图表中对应的图形元素，会高亮
        inRange:{                             //定义 在选中范围中 的视觉元素
            color: ['#121122', 'rgba(3,4,5,0.4)', 'red'],
            symbolSize: [30, 100]
        },
        outOfRange:{                            //定义 在选中范围外 的视觉元素。
            color: ['#121122', 'rgba(3,4,5,0.4)', 'red'],
            symbolSize: [30, 100]
        },
        zlevel:0,                                   //所属图形的Canvas分层，zlevel 大的 Canvas 会放在 zlevel 小的 Canvas 的上面
        z:2,                                         //所属组件的z分层，z值小的图形会被z值大的图形覆盖
        left:"center",                              //组件离容器左侧的距离,'left', 'center', 'right','20%'
        top:"top",                                   //组件离容器上侧的距离,'top', 'middle', 'bottom','20%'
        right:"auto",                               //组件离容器右侧的距离,'20%'
        bottom:"auto",                              //组件离容器下侧的距离,'20%'
        orient:"vertical",                        //图例排列方向
        padding:5,                                   //图例内边距，单位px  5  [5, 10]  [5,10,5,10]
        backgroundColor:"transparent",            //标题背景色
        borderColor:"#ccc",                         //边框颜色
        borderWidth:0,                               //边框线宽
        textStyle:mytextStyle,                      //文本样式
        formatter: function (value) {                //标签的格式化工具。
            return 'aaaa' + value;                   // 范围标签显示内容。
        }
    }
];




series-bar.js文件
为柱形图的参数配置

mytextStyle={
    color:"#333",               //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                  //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                 //颜色
    borderColor:"#000",         //边框颜色
    borderWidth:0,              //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,              //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};
mylabel={
    show:false,                  //是否显示标签。
    position:"inside",          //标签的位置。// 绝对的像素值[10, 10],// 相对的百分比['50%', '50%'].'top','left','right','bottom','inside','insideLeft','insideRight','insideTop','insideBottom','insideTopLeft','insideBottomLeft','insideTopRight','insideBottomRight'
    offset:[30, 40],             //是否对文字进行偏移。默认不偏移。例如：[30, 40] 表示文字在横向上偏移 30，纵向上偏移 40。
    formatter:'{b}: {c}',       //标签内容格式器。模板变量有 {a}、{b}、{c}，分别表示系列名，数据名，数据值。
    textStyle:mytextStyle
};
mypoint={
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
myline={
    symbol:["pin","circle"],    //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    precision:2,                //标线数值的精度，在显示平均值线的时候有用。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle
    }
};
myarea={
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
series=[
{
    type:"bar",                 //柱形
    zlevel:0,                   //柱状图所有图形的 zlevel 值。
    z:2,                         //柱状图组件的所有图形的z值。控制图形的前后顺序。z值小的图形会被z值大的图形覆盖。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    name:"数据名称",            //系列名称，用于tooltip的显示，legend 的图例筛选，在 setOption 更新数据和配置项时用于指定对应的系列。
    legendHoverLink:true,      //是否启用图例 hover 时的联动高亮。
    coordinateSystem:"cartesian2d",////'cartesian2d'使用二维的直角坐标系。'geo'使用地理坐标系
    xAxisIndex:0,               //使用的 x 轴的 index，在单个图表实例中存在多个 x 轴的时候有用。
    yAxisIndex:0,               //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用。
    label:{                     //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等，
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{                 //图形样式，normal 是图形在默认状态下的样式；emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
        normal:myitemStyle,
        emphasis:myitemStyle,
    },
    stack:null,                  //数据堆叠，同个类目轴上系列配置相同的stack值可以堆叠放置。
    cursor:"pointer",           //鼠标悬浮时在图形元素上时鼠标的样式是什么。同 CSS 的 cursor。
    barGap:"30%",                //柱间距离，可设固定值（如 20）或者百分比（如 '30%'，表示柱子宽度的 30%）。
    barCategoryGap:"20%",       //类目间柱形距离，默认为类目间距的20%，可设固定值
    encode: {                     //可以定义 data 的哪个维度被编码成什么
        x: [3, 1, 5],              // 表示维度 3、1、5 映射到 x 轴。
        y: 2,                       // 表示维度 2 映射到 y 轴。
        tooltip: [3, 2, 4],         // 表示维度 3、2、4 会在 tooltip 中显示。
        label: 3                    // 表示 label 使用维度 3。
    },
    data: [                         //每一列称为一个『维度』。维度下标从0开始
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
    ],
    markPoint:mypoint.data=[
        {name: '最大值', type: 'max'},
        {name: '某个坐标', coord: [10, 20]},
        {name: '固定 x 像素位置', yAxis: 10, x: '90%'},
        {name: '某个屏幕坐标', x: 100, y: 100}],
    markLine:myline.data=[
        {name: '平均线',type: 'average'},                  // 支持 'average', 'min', 'max'
        {name: 'Y 轴值为 100 的水平线',yAxis: 100},
        [
            {name: '最小值到最大值', type: 'min'},         // 起点和终点的项会共用一个 name
            {type: 'max'}
        ],
        [
            {name: '两个坐标之间的标线',coord: [10, 20]},
            {coord: [20, 30]}
        ],
        [
            {yAxis: 'max',x: '90%'},                        // 固定起点的 x 像素位置，用于模拟一条指向最大值的水平线
            {type: 'max'}
        ],
        [
            { name: '两个屏幕坐标之间的标线',x: 100,y: 100},
            {x: 500,y: 200}
        ]
    ],
    markArea:myarea.data=[
        [
            {name: '平均值到最大值',type: 'average'},
            {type: 'max'}
        ],

        [
            {name: '两个坐标之间的标域',coord: [10, 20]},
            {coord: [20, 30]}
        ],
        [
            {name: '60分到80分',yAxis: 60},
            {yAxis: 80}
        ],
        [
            {name: '所有数据范围区间',coord: ['min', 'min']},
            {coord: ['max', 'max']}
        ],
        [
            {name: '两个屏幕坐标之间的标域',x: 100,y: 100},
            {x: '90%',y: '10%'}
        ]
    ],
    tooltip:tooltip,   //index.js中定义的
},
];



series-effectscatter.js文件
为特效散点图的参数配置

mytextStyle={
    color:"#333",               //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                  //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                 //颜色
    borderColor:"#000",         //边框颜色
    borderWidth:0,              //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,              //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};
mylabel={
    show:false,                  //是否显示标签。
    position:"inside",          //标签的位置。// 绝对的像素值[10, 10],// 相对的百分比['50%', '50%'].'top','left','right','bottom','inside','insideLeft','insideRight','insideTop','insideBottom','insideTopLeft','insideBottomLeft','insideTopRight','insideBottomRight'
    offset:[30, 40],             //是否对文字进行偏移。默认不偏移。例如：[30, 40] 表示文字在横向上偏移 30，纵向上偏移 40。
    formatter:'{b}: {c}',       //标签内容格式器。模板变量有 {a}、{b}、{c}，分别表示系列名，数据名，数据值。
    textStyle:mytextStyle
};
mypoint={
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
myline={
    symbol:["pin","circle"],    //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    precision:2,                //标线数值的精度，在显示平均值线的时候有用。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle
    }
};
myarea={
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
series=[
{
    type:"effectScatter",       //特效散点图
    zlevel:0,                    //柱状图所有图形的 zlevel 值。
    z:2,                          //柱状图组件的所有图形的z值。控制图形的前后顺序。z值小的图形会被z值大的图形覆盖。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    name:"数据名称",             //系列名称，用于tooltip的显示，legend 的图例筛选，在 setOption 更新数据和配置项时用于指定对应的系列。
    legendHoverLink:true,       //是否启用图例 hover 时的联动高亮。
    hoverAnimation:true,        //是否开启鼠标 hover 的提示动画效果。
    effectType:"ripple",        //特效类型，目前只支持涟漪特效'ripple'。
    showEffectOn:"render",      //配置何时显示特效。可选：'render' 绘制完成后显示特效。'emphasis' 高亮（hover）的时候显示特效。
    rippleEffect:{              //涟漪特效相关配置。
        period:4,               //动画的时间。
        scale:2.5,              //动画中波纹的最大缩放比例。
        brushType:'fill',      //波纹的绘制方式，可选 'stroke' 和 'fill'。
    },
    coordinateSystem:"geo",   //'cartesian2d'使用二维的直角坐标系。'geo'使用地理坐标系
    xAxisIndex:0,               //使用的 x 轴的 index，在单个图表实例中存在多个 x 轴的时候有用。
    yAxisIndex:0,               //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用。
    polarIndex:0,               //使用的极坐标系的 index，在单个图表实例中存在多个极坐标系的时候有用。
    geoIndex:0,                 //使用的地理坐标系的 index，在单个图表实例中存在多个地理坐标系的时候有用。
    calendarIndex:0,            //使用的日历坐标系的 index，在单个图表实例中存在多个日历坐标系的时候有用。
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    large:false,                //是否开启大规模散点图的优化，在数据图形特别多的时候（>=5k）可以开启。开启后配合 largeThreshold 在数据量大于指定阈值的时候对绘制进行优化。缺点：优化后不能自定义设置单个数据项的样式。
    largeThreshold:2000,        //开启绘制优化的阈值。
    cursor:"pointer",           //鼠标悬浮时在图形元素上时鼠标的样式是什么。同 CSS 的 cursor。
    label:{                      //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等，
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{                 //图形样式，normal 是图形在默认状态下的样式；emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
        normal:myitemStyle,
        emphasis:myitemStyle,
    },
    encode: {                   //可以定义 data 的哪个维度被编码成什么
        x: [3, 1, 5],           // 表示维度 3、1、5 映射到 x 轴。
        y: 2,                   // 表示维度 2 映射到 y 轴。
        tooltip: [3, 2, 4],     // 表示维度 3、2、4 会在 tooltip 中显示。
        label: 3                // 表示 label 使用维度 3。
    },
    data: [                     //每一列称为一个『维度』。维度下标从0开始
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
    ],
    //markPoint:同bar
    //markLine:同bar
    //markArea:同bar
    tooltip:tooltip  //index.js
},

];



series-graph.js文件
为关系图的参数配置

mytextStyle={
    color:"#333",               //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                  //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                 //颜色
    borderColor:"#000",         //边框颜色
    borderWidth:0,              //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,              //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};
mylabel={
    show:false,                  //是否显示标签。
    position:"inside",          //标签的位置。// 绝对的像素值[10, 10],// 相对的百分比['50%', '50%'].'top','left','right','bottom','inside','insideLeft','insideRight','insideTop','insideBottom','insideTopLeft','insideBottomLeft','insideTopRight','insideBottomRight'
    offset:[30, 40],             //是否对文字进行偏移。默认不偏移。例如：[30, 40] 表示文字在横向上偏移 30，纵向上偏移 40。
    formatter:'{b}: {c}',       //标签内容格式器。模板变量有 {a}、{b}、{c}，分别表示系列名，数据名，数据值。
    textStyle:mytextStyle
};
mypoint={
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
myline={
    symbol:["pin","circle"],    //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    precision:2,                //标线数值的精度，在显示平均值线的时候有用。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle
    }
};
myarea={
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
series=[
{
    type:"graph",               //关系图
    zlevel:0,                   //柱状图所有图形的 zlevel 值。
    z:2,                         //柱状图组件的所有图形的z值。控制图形的前后顺序。z值小的图形会被z值大的图形覆盖。
    left:"10%",                 //组件离容器左侧的距离,百分比字符串或整型数字
    top:60,                      //组件离容器上侧的距离，百分比字符串或整型数字
    right:"auto",               //组件离容器右侧的距离,百分比字符串或整型数字
    bottom:"auto",              //组件离容器下侧的距离,百分比字符串或整型数字
    width:"auto",               //图例宽度
    height:"auto",              //图例高度
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    name:"数据名称",            //系列名称，用于tooltip的显示，legend 的图例筛选，在 setOption 更新数据和配置项时用于指定对应的系列。
    legendHoverLink:true,       //是否启用图例 hover 时的联动高亮。
    hoverAnimation:true,        //是否开启鼠标 hover 节点的提示动画效果。
    coordinateSystem:null,      //null无坐标系，'cartesian2d'使用二维的直角坐标系。'geo'使用地理坐标系，'polar'使用极坐标系
    xAxisIndex:0,                //使用的 x 轴的 index，在单个图表实例中存在多个 x 轴的时候有用。
    yAxisIndex:0,                //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用。
    polarIndex:0,                //使用的极坐标系的 index，在单个图表实例中存在多个极坐标系的时候有用。
    geoIndex:0,                  //使用的地理坐标系的 index，在单个图表实例中存在多个地理坐标系的时候有用。
    calendarIndex:0,            //使用的日历坐标系的 index，在单个图表实例中存在多个日历坐标系的时候有用。
    layout:'none',              //'none' 不采用任何布局，使用节点中提供的 x， y 作为节点的位置.'circular' 采用环形布局，'force' 采用力引导布局。
    //circular:{},               //环形布局相关配置
    //force:{},                  //力引导布局相关的配置项
    roam:false,                 //是否开启鼠标缩放和平移漫游。默认不开启。如果只想要开启缩放或者平移，可以设置成 'scale' 或者 'move'。设置成 true 为都开启
    nodeScaleRatio:0.6,         //鼠标漫游缩放时节点的相应缩放比例，当设为0时节点不随着鼠标的缩放而缩放
    draggable:false,            //节点是否可拖拽，只在使用力引导布局的时候有用。
    focusNodeAdjacency:true,   //是否在鼠标移到节点上的时候突出显示节点以及节点的边和邻接节点。
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    edgeSymbol:['circle', 'arrow'],//边两端的标记类型，可以是一个数组分别指定两端，也可以是单个统一指定。默认不显示标记，常见的可以设置为箭头
    edgeSymbolSize:[5,2],       //边两端的标记大小，可以是一个数组分别指定两端，也可以是单个统一指定。
    cursor:"pointer",           //鼠标悬浮时在图形元素上时鼠标的样式是什么。同 CSS 的 cursor。
    label:{                      //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等，
        normal:mylabel,
        emphasis:mylabel
    },
    edgeLabel:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{                 //图形样式，normal 是图形在默认状态下的样式；emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
        normal:myitemStyle,
        emphasis:myitemStyle,
    },
    lineStyle:{                 //图形样式，normal 是图形在默认状态下的样式；emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
        normal:mylineStyle,
        emphasis:mylineStyle,
    },
    categories:[                //节点分类的类目，可选。
        {
            name:"类目名称",    //类目名称
            symbol:"pin",       //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
            symbolSize:50,      //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
            symbolRotate:0,     //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
            symbolOffset:[0,0], //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
            label:{              //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等，
                normal:mylabel,
                emphasis:mylabel
            },
            itemStyle:{         //图形样式，normal 是图形在默认状态下的样式；emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
                normal:myitemStyle,
                emphasis:myitemStyle,
            },
        }
    ],
    data: [                     //data就是node
        {
        name: '1',
        x: 10,
        y: 10,
        value: 10
    }, {
        name: '2',
        x: 100,
        y: 100,
        value: 20,
        symbolSize: 20,
        itemStyle: {
            normal: {
                color: 'red'
            }
        }
        }
    ],
    links:[                 //links就是edges
        {
            source: 'n1',
            target: 'n2'
        }, {
            source: 'n2',
            target: 'n3'
        }
    ],
    //markPoint:同bar
    //markLine:同bar
    //markArea:同bar
    tooltip:tooltip  //index.js
},

];


series-heatmap.js文件
为热力图的参数配置

mytextStyle={
    color:"#333",               //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                  //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                 //颜色
    borderColor:"#000",         //边框颜色
    borderWidth:0,              //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,              //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};
mylabel={
    show:false,                  //是否显示标签。
    position:"inside",          //标签的位置。// 绝对的像素值[10, 10],// 相对的百分比['50%', '50%'].'top','left','right','bottom','inside','insideLeft','insideRight','insideTop','insideBottom','insideTopLeft','insideBottomLeft','insideTopRight','insideBottomRight'
    offset:[30, 40],             //是否对文字进行偏移。默认不偏移。例如：[30, 40] 表示文字在横向上偏移 30，纵向上偏移 40。
    formatter:'{b}: {c}',       //标签内容格式器。模板变量有 {a}、{b}、{c}，分别表示系列名，数据名，数据值。
    textStyle:mytextStyle
};
mypoint={
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
myline={
    symbol:["pin","circle"],    //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    precision:2,                //标线数值的精度，在显示平均值线的时候有用。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle
    }
};
myarea={
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
series=[
{
    type:"heatmap",             //热力图
    zlevel:0,                   //柱状图所有图形的 zlevel 值。
    z:2,                         //柱状图组件的所有图形的z值。控制图形的前后顺序。z值小的图形会被z值大的图形覆盖。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    name:"数据名称",            //系列名称，用于tooltip的显示，legend 的图例筛选，在 setOption 更新数据和配置项时用于指定对应的系列。
    coordinateSystem:"geo",    //'cartesian2d'使用二维的直角坐标系。'geo'使用地理坐标系
    xAxisIndex:0,               //使用的 x 轴的 index，在单个图表实例中存在多个 x 轴的时候有用。
    yAxisIndex:0,               //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用。
    polarIndex:0,               //使用的极坐标系的 index，在单个图表实例中存在多个极坐标系的时候有用。
    geoIndex:0,                 //使用的地理坐标系的 index，在单个图表实例中存在多个地理坐标系的时候有用。
    calendarIndex:0,            //使用的日历坐标系的 index，在单个图表实例中存在多个日历坐标系的时候有用。
    blurSize:20,                //每个点模糊的大小，在地理坐标系(coordinateSystem: 'geo')上有效。
    minOpacity:0,               //最小的透明度，在地理坐标系(coordinateSystem: 'geo')上有效。
    maxOpacity:1,               //最大的透明度，在地理坐标系(coordinateSystem: 'geo')上有效。
    cursor:"pointer",           //鼠标悬浮时在图形元素上时鼠标的样式是什么。同 CSS 的 cursor。
    data: [                      //每一列称为一个『维度』。维度下标从0开始
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
    ],
    //markPoint:同bar
    //markLine:同bar
    //markArea:同bar
    tooltip:tooltip  //index.js
},


];


series-lines.js文件
为线图的参数配置

mytextStyle={
    color:"#333",               //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                  //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                     //坐标轴线线宽
    opacity:1,                   //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                 //颜色
    borderColor:"#000",         //边框颜色
    borderWidth:0,               //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,               //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,             //阴影水平方向上的偏移距离。
    shadowOffsetY:0,             //阴影垂直方向上的偏移距离。
    opacity:1,                    //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};
mylabel={
    show:false,                  //是否显示标签。
    position:"inside",          //标签的位置。// 绝对的像素值[10, 10],// 相对的百分比['50%', '50%'].'top','left','right','bottom','inside','insideLeft','insideRight','insideTop','insideBottom','insideTopLeft','insideBottomLeft','insideTopRight','insideBottomRight'
    offset:[30, 40],              //是否对文字进行偏移。默认不偏移。例如：[30, 40] 表示文字在横向上偏移 30，纵向上偏移 40。
    formatter:'{b}: {c}',       //标签内容格式器。模板变量有 {a}、{b}、{c}，分别表示系列名，数据名，数据值。
    textStyle:mytextStyle
};
mypoint={
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
myline={
    symbol:["pin","circle"],    //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    precision:2,                //标线数值的精度，在显示平均值线的时候有用。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle
    }
};
myarea={
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
series=[
{
    type:"lines",               //线图
    zlevel:0,                   //柱状图所有图形的 zlevel 值。
    z:2,                        //柱状图组件的所有图形的z值。控制图形的前后顺序。z值小的图形会被z值大的图形覆盖。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    name:"数据名称",            //系列名称，用于tooltip的显示，legend 的图例筛选，在 setOption 更新数据和配置项时用于指定对应的系列。
    coordinateSystem:"geo",    //'cartesian2d'使用二维的直角坐标系。'geo'使用地理坐标系
    xAxisIndex:0,               //使用的 x 轴的 index，在单个图表实例中存在多个 x 轴的时候有用。
    yAxisIndex:0,               //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用。
    geoIndex:0,                 //使用的地理坐标系的 index，在单个图表实例中存在多个地理坐标系的时候有用。
    polyline:false,             //是否是多段线。默认为 false，只能用于绘制只有两个端点的线段，线段可以通过 lineStyle.normal.curveness 配置为曲线。
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    large:false,                //是否开启大规模散点图的优化，在数据图形特别多的时候（>=5k）可以开启。开启后配合 largeThreshold 在数据量大于指定阈值的时候对绘制进行优化。缺点：优化后不能自定义设置单个数据项的样式。
    largeThreshold:2000,        //开启绘制优化的阈值。
    cursor:"pointer",           //鼠标悬浮时在图形元素上时鼠标的样式是什么。同 CSS 的 cursor。
    label:{                      //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等，
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{                 //图形样式，normal 是图形在默认状态下的样式；emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
        normal:mylineStyle,
        emphasis:mylineStyle,
    },
    data: [
        {
            coords: [[120, 66], [122, 67]],
            lineStyle: {normal: {}}
        }
    ],
    //markPoint:同bar
    //markLine:同bar
    //markArea:同bar
    tooltip:tooltip  //index.js
},
];


series-map.js文件
为地图的参数配置

mytextStyle={
    color:"#333",                //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                  //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                 //颜色
    borderColor:"#000",         //边框颜色
    borderWidth:0,               //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,               //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离。
    opacity:1,                   //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};
mylabel={
    show:false,                  //是否显示标签。
    position:"inside",          //标签的位置。// 绝对的像素值[10, 10],// 相对的百分比['50%', '50%'].'top','left','right','bottom','inside','insideLeft','insideRight','insideTop','insideBottom','insideTopLeft','insideBottomLeft','insideTopRight','insideBottomRight'
    offset:[30, 40],             //是否对文字进行偏移。默认不偏移。例如：[30, 40] 表示文字在横向上偏移 30，纵向上偏移 40。
    formatter:'{b}: {c}',       //标签内容格式器。模板变量有 {a}、{b}、{c}，分别表示系列名，数据名，数据值。
    textStyle:mytextStyle
};
mypoint={
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
myline={
    symbol:["pin","circle"],    //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    precision:2,                //标线数值的精度，在显示平均值线的时候有用。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle
    }
};
myarea={
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
series=[
{
    type:"map",                                 //地图数据表
    map:"china",                                //地图类型。world世界地图，china中国地图
    roam:false,                                 //是否开启鼠标缩放和平移漫游。默认不开启。如果只想要开启缩放或者平移，可以设置成 'scale' 或者 'move'。设置成 true 为都开启
    center:[115.97, 29.71],                     //当前视角的中心点，用经纬度表示
    aspectScale:0.75,                           //这个参数用于 scale 地图的长宽比。
    boundingCoords: [[-180, 90], [180, -90]],  //二维数组，定义定位的左上角以及右下角分别所对应的经纬度
    zoom:1,                                     //当前视角的缩放比例
    scaleLimit:{                                //所属组件的z分层，z值小的图形会被z值大的图形覆盖
        min:1,                                  //最小的缩放值
        max:1,                                  //最大的缩放值
    },
    nameMap:{                                   //自定义地区的名称映射
        'China' : '中国'
    },
    selectedMode: false ,                      //选中模式，表示是否支持多个选中，默认关闭，支持布尔值和字符串，字符串取值可选'single'表示单选，或者'multiple'表示多选。
    label:{                                     //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等
        normal:{
            show:false,                          //是否在普通状态下显示标签。
            textStyle:mytextStyle,              //普通状态下的标签文本样式。
        },
        emphasis:{
            show:false,                         //是否在高亮状态下显示标签。
            textStyle:mytextStyle              //高亮状态下的标签文本样式。
        }
    },
    itemStyle:{                                 //地图区域的多边形 图形样式
        normal:myitemStyle,
        emphasis:myitemStyle
    },
    zlevel:0,                                   //所属图形的 zlevel 值。
    z:2,                                         //所属图形的 z 值。
    left:"10%",                                 //组件离容器左侧的距离,百分比字符串或整型数字
    top:60,                                      //组件离容器上侧的距离，百分比字符串或整型数字
    right:"auto",                               //组件离容器右侧的距离,百分比字符串或整型数字
    bottom:"auto",                              //组件离容器下侧的距离,百分比字符串或整型数字
    layoutCenter:['30%', '30%'],                //地图中心在屏幕中的位置
    layoutSize:100,                              //地图的大小,支持相对于屏幕宽高的百分比或者绝对的像素大小。
    mapValueCalculation:"sum",                  //多个拥有相同地图类型的系列会使用同一个地图展现，如果多个系列都在同一个区域有值，目前有：'sum' 取和。'average' 取平均值。'max' 取最大值。'min' 取最小值。
    showLegendSymbol:true,                      //在图例相应区域显示图例的颜色标识（系列标识的小圆点），存在 legend 组件时生效。
    silent:false,                                //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    data: [
        {name: '数据1',value: 10},
        {name: '数据2',value: 20}
    ],
    //markPoint:同bar
    //markLine:同bar
    //markArea:同bar
    tooltip:tooltip  //index,js
},

];


series-pie.js文件
为饼图的参数配置

mytextStyle={
    color:"#333",               //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                  //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                 //颜色
    borderColor:"#000",         //边框颜色
    borderWidth:0,               //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,              //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离。
    opacity:1,                   //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};
mylabel={
    show:false,                  //是否显示标签。
    position:"inside",          //标签的位置。// 绝对的像素值[10, 10],// 相对的百分比['50%', '50%'].'top','left','right','bottom','inside','insideLeft','insideRight','insideTop','insideBottom','insideTopLeft','insideBottomLeft','insideTopRight','insideBottomRight'
    offset:[30, 40],             //是否对文字进行偏移。默认不偏移。例如：[30, 40] 表示文字在横向上偏移 30，纵向上偏移 40。
    formatter:'{b}: {c}',       //标签内容格式器。模板变量有 {a}、{b}、{c}，分别表示系列名，数据名，数据值。
    textStyle:mytextStyle
};
mypoint={
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
myline={
    symbol:["pin","circle"],    //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    precision:2,                //标线数值的精度，在显示平均值线的时候有用。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle
    }
};
myarea={
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
series=[
{
    type:"pie",                 //饼图
    zlevel:0,                   //柱状图所有图形的 zlevel 值。
    z:2,                         //柱状图组件的所有图形的z值。控制图形的前后顺序。z值小的图形会被z值大的图形覆盖。
    center:['50%', '50%'],      //饼图的中心（圆心）坐标，数组的第一项是横坐标，第二项是纵坐标。支持设置成百分比，设置成百分比时第一项是相对于容器宽度，第二项是相对于容器高度。
    radius:[0, '75%'],          //饼图的半径，数组的第一项是内半径，第二项是外半径。支持设置成百分比，相对于容器高宽中较小的一项的一半。可以将内半径设大显示成圆环图（Donut chart）。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    name:"数据名称",            //系列名称，用于tooltip的显示，legend 的图例筛选，在 setOption 更新数据和配置项时用于指定对应的系列。
    legendHoverLink:true,       //是否启用图例 hover 时的联动高亮。
    hoverAnimation:true,        //是否开启 hover 在扇区上的放大动画效果。
    selectedMode:false,         //选中模式，表示是否支持多个选中，默认关闭，支持布尔值和字符串，字符串取值可选'single'，'multiple'，分别表示单选还是多选。
    selectedOffset:10,          //选中扇区的偏移距离。
    clockwise:true,             //饼图的扇区是否是顺时针排布。
    startAngle:90,              //起始角度，支持范围[0, 360]。
    minAngle:0,                 //最小的扇区角度（0 ~ 360），用于防止某个值过小导致扇区太小影响交互。
    roseType:false,             //是否展示成南丁格尔图，通过半径区分数据大小。可选择两种模式：'radius' 扇区圆心角展现数据的百分比，半径展现数据的大小。'area' 所有扇区圆心角相同，仅通过半径展现数据大小。
    cursor:"pointer",           //鼠标悬浮时在图形元素上时鼠标的样式是什么。同 CSS 的 cursor。
    label:{                      //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等，
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{                  //图形样式，normal 是图形在默认状态下的样式；emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
        normal:myitemStyle,
        emphasis:myitemStyle,
    },
    data:[
        {name: '数据1', value: 10},
        {name: '数据2', value: 20}
    ],
    //markPoint:同bar
    //markLine:同bar
    //markArea:同bar
    tooltip:tooltip  //index,js
},

];


series-radar.js文件
为雷达图的参数配置

mytextStyle={
    color:"#333",                //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",   //字体系列
    fontSize:18,                //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                //颜色
    borderColor:"#000",         //边框颜色
    borderWidth:0,              //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,              //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离。
    opacity:1,                   //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};
mylabel={
    show:false,                  //是否显示标签。
    position:"inside",          //标签的位置。// 绝对的像素值[10, 10],// 相对的百分比['50%', '50%'].'top','left','right','bottom','inside','insideLeft','insideRight','insideTop','insideBottom','insideTopLeft','insideBottomLeft','insideTopRight','insideBottomRight'
    offset:[30, 40],             //是否对文字进行偏移。默认不偏移。例如：[30, 40] 表示文字在横向上偏移 30，纵向上偏移 40。
    formatter:'{b}: {c}',       //标签内容格式器。模板变量有 {a}、{b}、{c}，分别表示系列名，数据名，数据值。
    textStyle:mytextStyle
};
mypoint={
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
myline={
    symbol:["pin","circle"],    //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    precision:2,                //标线数值的精度，在显示平均值线的时候有用。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle
    }
};
myarea={
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
series=[
{
    type:"radar",               //雷达图
    zlevel:0,                   //柱状图所有图形的 zlevel 值。
    z:2,                        //柱状图组件的所有图形的z值。控制图形的前后顺序。z值小的图形会被z值大的图形覆盖。
    silent:false,              //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    name:"数据名称",            //系列名称，用于tooltip的显示，legend 的图例筛选，在 setOption 更新数据和配置项时用于指定对应的系列。
    radarIndex:0,               //雷达图所使用的 radar 组件的 index。
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    cursor:"pointer",           //鼠标悬浮时在图形元素上时鼠标的样式是什么。同 CSS 的 cursor。
    label:{                      //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等，
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{                 //图形样式，normal 是图形在默认状态下的样式；emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
        normal:myitemStyle,
        emphasis:myitemStyle,
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle,
    },
    areaStyle:{
        normal:myareaStyle,
        emphasis:myareaStyle,
    },
    data: [                     //每一列称为一个『维度』。维度下标从0开始
        {
            value : [4300, 10000, 28000, 35000, 50000, 19000],
            name : '预算分配（Allocated Budget）'
        },
        {
            value : [5000, 14000, 28000, 31000, 42000, 21000],
            name : '实际开销（Actual Spending）'
        }
    ],
    tooltip:tooltip
},

]
series-scatter.js文件
为散点图的参数配置

mytextStyle={
    color:"#333",               //文字颜色
    fontStyle:"normal",         //italic斜体  oblique倾斜
    fontWeight:"normal",        //文字粗细bold   bolder   lighter  100 | 200 | 300 | 400...
    fontFamily:"sans-serif",    //字体系列
    fontSize:18,                  //字体大小
};
mylineStyle={
    color:"#333",               //颜色，'rgb(128, 128, 128)'，'rgba(128, 128, 128, 0.5)'，支持线性渐变，径向渐变，纹理填充
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    type:"solid",               //坐标轴线线的类型，solid，dashed，dotted
    width:1,                    //坐标轴线线宽
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myareaStyle={
    color:['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)'],//分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。
    shadowColor:"red",          //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离
    shadowBlur:10,              //图形阴影的模糊大小。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形
};
myitemStyle={
    color:"red",                 //颜色
    borderColor:"#000",         //边框颜色
    borderWidth:0,              //柱条的描边宽度，默认不描边。
    borderType:"solid",         //柱条的描边类型，默认为实线，支持 'dashed', 'dotted'。
    barBorderRadius:0,          //柱形边框圆角半径，单位px，支持传入数组分别指定柱形4个圆角半径。
    shadowBlur:10,              //图形阴影的模糊大小。
    shadowColor:"#000",         //阴影颜色
    shadowOffsetX:0,            //阴影水平方向上的偏移距离。
    shadowOffsetY:0,            //阴影垂直方向上的偏移距离。
    opacity:1,                  //图形透明度。支持从 0 到 1 的数字，为 0 时不绘制该图形。
};
mylabel={
    show:false,                  //是否显示标签。
    position:"inside",          //标签的位置。// 绝对的像素值[10, 10],// 相对的百分比['50%', '50%'].'top','left','right','bottom','inside','insideLeft','insideRight','insideTop','insideBottom','insideTopLeft','insideBottomLeft','insideTopRight','insideBottomRight'
    offset:[30, 40],             //是否对文字进行偏移。默认不偏移。例如：[30, 40] 表示文字在横向上偏移 30，纵向上偏移 40。
    formatter:'{b}: {c}',       //标签内容格式器。模板变量有 {a}、{b}、{c}，分别表示系列名，数据名，数据值。
    textStyle:mytextStyle
};
mypoint={
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
myline={
    symbol:["pin","circle"],    //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    precision:2,                //标线数值的精度，在显示平均值线的时候有用。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    lineStyle:{
        normal:mylineStyle,
        emphasis:mylineStyle
    }
};
myarea={
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    label:{
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{
        normal:myitemStyle,
        emphasis:myitemStyle
    }
};
series=[
{
    type:"scatter",             //散点图
    zlevel:0,                   //柱状图所有图形的 zlevel 值。
    z:2,                         //柱状图组件的所有图形的z值。控制图形的前后顺序。z值小的图形会被z值大的图形覆盖。
    silent:false,               //图形是否不响应和触发鼠标事件，默认为 false，即响应和触发鼠标事件。
    name:"数据名称",             //系列名称，用于tooltip的显示，legend 的图例筛选，在 setOption 更新数据和配置项时用于指定对应的系列。
    legendHoverLink:true,       //是否启用图例 hover 时的联动高亮。
    hoverAnimation:true,        //是否开启鼠标 hover 的提示动画效果。
    coordinateSystem:"geo",     //'cartesian2d'使用二维的直角坐标系。'geo'使用地理坐标系
    xAxisIndex:0,                //使用的 x 轴的 index，在单个图表实例中存在多个 x 轴的时候有用。
    yAxisIndex:0,                //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用。
    polarIndex:0,                //使用的极坐标系的 index，在单个图表实例中存在多个极坐标系的时候有用。
    geoIndex:0,                  //使用的地理坐标系的 index，在单个图表实例中存在多个地理坐标系的时候有用。
    calendarIndex:0,            //使用的日历坐标系的 index，在单个图表实例中存在多个日历坐标系的时候有用。
    symbol:"pin",               //图形 'circle', 'rect', 'roundRect', 'triangle', 'diamond', 'pin', 'arrow'
    symbolSize:50,              //标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，例如 [20, 10] 表示标记宽为20，高为10。
    symbolRotate:0,             //标记的旋转角度。注意在 markLine 中当 symbol 为 'arrow' 时会忽略 symbolRotate 强制设置为切线的角度。
    symbolOffset:[0,0],         //标记相对于原本位置的偏移。默认情况下，标记会居中置放在数据对应的位置
    large:false,                //是否开启大规模散点图的优化，在数据图形特别多的时候（>=5k）可以开启。开启后配合 largeThreshold 在数据量大于指定阈值的时候对绘制进行优化。缺点：优化后不能自定义设置单个数据项的样式。
    largeThreshold:2000,        //开启绘制优化的阈值。
    cursor:"pointer",           //鼠标悬浮时在图形元素上时鼠标的样式是什么。同 CSS 的 cursor。
    label:{                      //图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等，
        normal:mylabel,
        emphasis:mylabel
    },
    itemStyle:{                 //图形样式，normal 是图形在默认状态下的样式；emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
        normal:myitemStyle,
        emphasis:myitemStyle,
    },
    encode: {                    //可以定义 data 的哪个维度被编码成什么
        x: [3, 1, 5],             // 表示维度 3、1、5 映射到 x 轴。
        y: 2,                     // 表示维度 2 映射到 y 轴。
        tooltip: [3, 2, 4],      // 表示维度 3、2、4 会在 tooltip 中显示。
        label: 3                 // 表示 label 使用维度 3。
    },
    data: [                      //每一列称为一个『维度』。维度下标从0开始
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
        [12, 44, 55, 66, 2],
        [23, 6, 16, 23, 1],
    ],
    //markPoint:同bar
    //markLine:同bar
    //markArea:同bar
    tooltip:tooltip  //index.js
},

];