<template>
  <div id="waiting-ctn">
    <!--主体-->
    <div class="box am-center">
      <div class="qrcode am-round am-text-center"><img src="../../assets/images/qrcode.jpg" alt=""></div>
      <div class="info">
        <div class="driver am-fl">
          <div class="faces am-round am-text-center am-fl">
            <i class="am-icon-user"></i>
            <img class="am-round" src="images/p2.jpg" alt="">
          </div>
          <div class="tel am-fl">
            <h1>王师傅</h1>
            <div>153****5224</div>
          </div>
          <div class="am-cf"></div>
        </div>
        <div class="time am-text-center am-fl">
          <div>距离上车时间</div>
          <p>08:34</p>
        </div>
        <div class="car am-fr">
          <div>白色 雪弗兰</div>
          <p>川A29181G</p>
        </div>
        <div class="am-cf"></div>
      </div>
      <div class="button am-text-center">
        <a href="tel:15348115224" class="am-btn am-btn-success am-round">联系司机</a>
        <a href="index_cancel.html" class="am-btn am-btn-danger am-round">取消订单</a>
      </div>
    </div>
  </div>

</template>
<script>
export default {
  data() {
    return {};
  },
  mounted() {
    this.waiting();
  },
  methods: {
    waiting() {
      //百度地图
      //创建地图并设置中心点和当前城市
      var map = new BMap.Map("map", {
        enableMapClick: false //禁用地图默认的点击事件
      });
      var point = new BMap.Point(104.0818, 30.546564); //成都某地
      map.centerAndZoom(point, 7); //中心点及级数
      map.enableScrollWheelZoom(true);
      map.setCurrentCity("成都"); //当前城市
      //标注：起点
      point = new BMap.Point(104.0818, 30.546564);
      var icon = new BMap.Icon("images/marker1x.png", new BMap.Size(27, 48), {
        //标注大小
        anchor: new BMap.Size(13.5, 43.5) //标注的偏移量
      });
      var marker = new BMap.Marker(point, { icon: icon }); //创建标注对象并添加到地图
      map.addOverlay(marker);
      //标注：终点
      var point2 = new BMap.Point(104.790778, 29.318791); //自贡某地
      var icon2 = new BMap.Icon("images/marker2x.png", new BMap.Size(27, 48), {
        anchor: new BMap.Size(13.5, 43.5)
      });
      var marker2 = new BMap.Marker(point2, { icon: icon2 });
      map.addOverlay(marker2);
      map.centerAndZoom(point2, 7);

      //二维码
      //切换面板
      $(".qrcode").click(function() {
        $("#qrcode").toggleClass("active");
      });
      //关闭面板
      $("#qrcode").click(function(e) {
        var _con = $("#qrcode .img");
        if (!_con.is(e.target) && _con.has(e.target).length === 0) {
          $("#qrcode").removeClass("active");
        }
      });
    }
  }
};
</script>

<style scoped src="../../assets/css/waiting.css">
</style>
<style scoped>
#waiting-ctn {
  background: #fff;
}
/*
二维码
*/
#qrcode {
	position: absolute;
	top: 0;
	left: 0;
	z-index: 1;
	width: 100%;
	height: 100%;
	background-color: rgba(0,0,0,.5);
	-webkit-transform: translateY(100%);
	transform: translateY(100%);
	-webkit-transition: -webkit-transform .3s;
	transition: transform .3s;
}
#qrcode.active {
	-webkit-transform: none;
	transform: none;
}
.qrcodeCode {
	width: 100%;
	height: 100%;
	position: relative;
}
#qrcode .img {
	position: absolute;
	top: 50%;
	left: 50%;	
	width: 2.26rem;
	height: 2.26rem;
	background-color: #fff;
	margin: -1.8rem 0 0 -1.13rem;
}
#qrcode img {
	width: 1.56rem;
	height: 1.56rem;
	margin-top: .35rem;
	vertical-align: baseline;
}
</style>
