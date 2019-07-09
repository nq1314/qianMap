<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
<meta name="keywords" content="百度地图,百度地图API，百度地图自定义工具，百度地图所见即所得工具" />
<meta name="description" content="百度地图API自定义地图，帮助用户在可视化操作下生成百度地图" />
<title>百度地图API自定义地图</title>
<!--引用百度地图API-->
<style type="text/css">
    html,body{margin:0;padding:0;}
/*地图标题*/
.BMap_bubble_title {
    color: #e48812;
    padding-left: 5px;
    font-weight: 600;
    font-size: 15px;
    background: #fff;
    padding-top: 5px;
    padding-left: 10px;
}
/* 消息内容 */
.BMap_bubble_content {
    background: #fff;
    padding-left:10px;
    padding-top:5px;
    padding-bottom:10px;
    font-size: 14px;
    line-height: 22px;
    color: #523926c7;
    font-weight: 600;
}
/* 内容 */
.BMap_pop div:nth-child(9) {
    top:35px !important;
    border-radius:7px;
}
/* 左上角删除按键 */
.BMap_pop img {
    top:43px !important;
    left:215px !important;
}
.BMap_top {
    display:none;
}
.BMap_bottom {
    display:none;
}
.BMap_center {
    display:none;
}
.BMap_center+div{
    display: none;
}
/* 隐藏边角 */
.BMap_pop div:nth-child(1) div {
    display:none;
}
.BMap_pop div:nth-child(3) {
    display:none;
}
.BMap_pop div:nth-child(7) {
    display:none;
}
.head{
    position: fixed;
    top: 10px;
    left: 0;
    right: 0;
    margin: auto;
    text-align: center;
    color: #9a5c2cc7;
    font-weight: 600;
    font-size: 24px;
    background: #ffffff94;
    width: 400px;
}
</style>
<script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=wqBXfIN3HkpM1AHKWujjCdsi"></script>
<script type="text/javascript" src="https://cdn.bootcss.com/jquery/3.4.1/jquery.js"></script>
</head>

<body>
    <div class="map">
        <div style="width:100%;height:100%" id="map"></div>
        <span class="head">千城千舍（小茶姑娘民宿）</span>
    </div>
   <script type="text/javascript">
       //创建和初始化地图函数：
       function initMap() {
           createMap();//创建地图
           setMapEvent();//设置地图事件
           addMapControl();//向地图添加控件
           addMapOverlay();//向地图添加覆盖物
           
       }
       function createMap() {
           map = new BMap.Map("map");       //经度      //纬度    //缩放比例
           map.centerAndZoom(new BMap.Point(120.1617445782,30.2799186759), 9); 
           
       }
       function setMapEvent() {
            // map.setMapStyleV2({     
            //  styleId: '83da37f91ccc52632fecc80c4cf34f90'
            // });
           map.enableScrollWheelZoom();
           map.enableKeyboard();
           map.enableDragging();
           map.enableDoubleClickZoom();
          
    //        map.setMapStyle({ styleJson:[   {
    //         "featureType": "road",
    //         "elementType": "geometry.stroke",
    //         "stylers": {
    //         "color": "#ff0000"
    //         }
    //    }   ]  });
       }
       function addClickHandler(target, window) {
           target.addEventListener("click", function () {
               target.openInfoWindow(window);
           });
       }
       function addMapOverlay() {
           var markers = [
             { content: "余杭塘栖古镇",phone: "18057122334",wechat: "hz-teahostel",storeHref:"http://www.baidu.com", title: "余杭塘栖小茶姑娘", position: { lat: 30.4821216619 , lng:120.1907563263 } }, // 纬度  经度
             { content: "浙江丽水松阳",phone: "18057122334",wechat: "hz-teahostel",storeHref:"http://www.baidu.com", title: "松阳小茶姑娘", position: { lat: 28.5360950061 , lng:119.3888653686 } }, // 纬度  经度
             { content: "浙江湖州溧阳天目湖",phone: "18057122334",wechat: "hz-teahostel",storeHref:"http://www.baidu.com", title: "隐湖居", position: { lat: 30.8691241310 , lng:120.0995194598 } } // 纬度  经度
           ];
           for (var index = 0; index < markers.length; index++) {
               var point = new BMap.Point(markers[index].position.lng, markers[index].position.lat);
               var marker = new BMap.Marker(point);
               var label = new BMap.Label(markers[index].title, { offset: new BMap.Size(25, 0) });
               label.setStyle({ 
                    color : "#e8683f", 
                    fontSize : "14px", 
                    backgroundColor :"rgba(255,255,255,0.85)",
                    padding:"5px",
                    border :"0", 
                    fontWeight :"bold" ,
                    borderRadius:"5px"
                });
                var opts = {
                   width: 210,
                   title: markers[index].title,
                   enableMessage: false
               };
               /* var infoWindow = new BMap.InfoWindow(markers[index].content, opts); */
               
              var infoWindow = new BMap.InfoWindow("地址：" + markers[index].content + "<br>咨询电话：" + markers[index].phone + "<br>掌柜微信：" + markers[index].wechat+"<br> 逛 一 逛 ：<a href="+markers[index].storeHref+">点击查看店铺</a>", opts);
               marker.setLabel(label);
               addClickHandler(marker, infoWindow);
               map.addOverlay(marker);
           };
           
        
           var labels = [];
           for (var index = 0; index < labels.length; index++) {
               var opt = { position: new BMap.Point(labels[index].position.lng, labels[index].position.lat) };
               var label = new BMap.Label(labels[index].content, opt);
               map.addOverlay(label);
           };
       }
       //向地图添加控件
       function addMapControl() {
           var scaleControl = new BMap.ScaleControl({ anchor: BMAP_ANCHOR_BOTTOM_LEFT });
           scaleControl.setUnit(BMAP_UNIT_IMPERIAL);
           map.addControl(scaleControl);
           var navControl = new BMap.NavigationControl({ anchor: BMAP_ANCHOR_TOP_LEFT, type: BMAP_NAVIGATION_CONTROL_LARGE });
           map.addControl(navControl);
           var overviewControl = new BMap.OverviewMapControl({ anchor: BMAP_ANCHOR_BOTTOM_RIGHT, isOpen: true });
           map.addControl(overviewControl);
       }
       var map;
       initMap();
       
   </script>
   
   </body>
   </html>
