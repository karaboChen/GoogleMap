<script setup>
import {  onMounted } from 'vue';
import { GoogleMap, Marker, InfoWindow, Polyline } from "vue3-google-map";
import { useRouter } from 'vue-router';
const router = useRouter()

//初始化地圖設定---------
const center = { lat: 22.544214, lng: 120.355484 };
const key = import.meta.env.VITE_key
const u_id = import.meta.env.VITE_id
//--------------------------FFFF00


//藍線
//==煉焦東路到南門， ( 煉焦BFG儲槽lat: 22.5395310, lng: 120.3534600)， 南門路口(lat: 22.5319833, lng: 120.3597917 )
const BluePath = {
  path: [
    { lat: 22.5395310, lng: 120.3534600 },
    { lat: 22.5319833, lng: 120.3597917 }
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==中興二路， ( 二道門22.5364167_N120.3629583_E ) ,(中興二路與河北路 22.5514778_N120.3502278_E      )
const BluePath2 = {
  path: [
    { lat: 22.5364167, lng: 120.3629583 },
    { lat: 22.5514778, lng: 120.3502278 }
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==動力東路與高爐西路(碼頭路UDC路口22.5487167_N120.3505917_E)， (電動鼓風機_北端22.5463583_N120.3524306_E)，
//==                (電動鼓風機_南端22.5454361_N120.3527361_)，(高爐西路_南端22.5370222_N120.3598500_E)
const BluePath3 = {
  path: [
    { lat: 22.5487167, lng: 120.3505917 },
    { lat: 22.5463583, lng: 120.3524306 },
    { lat: 22.5454361, lng: 120.3527361 },
    { lat: 22.5370222, lng: 120.3598500 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==高橫五路(22.5409800, lng: 120.3602700)， (22.5383570, lng: 120.3565440)，  (22.5365800, lng: 120.3560056)
const BluePath4 = {
  path: [
    { lat: 22.5409800, lng: 120.3602700 },
    { lat: 22.5383570, lng: 120.3565440 },
    { lat: 22.5365800, lng: 120.3560056 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==運河北一路。(運河北一路與中興二路口lat: 22.5363680, lng: 120.3629680)， (運河北一路與煉焦東路口22.5331980, lng: 120.3588220)
const BluePath5 = {
  path: [
    { lat: 22.5409800, lng: 120.3602700 },
    { lat: 22.5383570, lng: 120.3565440 },
    { lat: 22.5365800, lng: 120.3560056 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==運河北二路。(運河北二路東側 水源新直路口lat: 22.539435, lng: 120.367062) (運河北二路與中興二路口lat: 22.5363680, lng: 120.3629680)， 
const BluePath6 = {
  path: [
    { lat: 22.539435, lng: 120.367062 },
    { lat: 22.5363680, lng: 120.3629680 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==碼頭路。 (碼頭路與中興二路口lat: 22.5495610, lng: 120.3518940)， ( 石灰場A點 22.5460240, lng: 120.3469910)
//==          ( 石灰場B點 22.5454890, lng: 120.3465610)(碼頭路W1大樓22.5433300, lng: 120.3436000)
const BluePath7 = {
  path: [
    { lat: 22.5495610, lng: 120.3518940 },
    { lat: 22.5460240, lng: 120.3469910 },
    { lat: 22.5454890, lng: 120.3465610 },
    { lat: 22.5433300, lng: 120.3436000 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==生鐵南路。 (生鐵南路與高爐西路口lat: 22.542016, lng: 120.355593)， ( 動力二中路口 lat: 22.541879, lng: 120.355019 )
//==          ( 副產東路口 lat: 22.541660, lng: 120.353803 ) (生鐵南路_西端lat: 22.541546, lng: 120.353372)
const BluePath8 = {
  path: [
    { lat: 22.542016, lng: 120.355593 },
    { lat: 22.541879, lng: 120.355019 },
    { lat: 22.541660, lng: 120.353803 },
    { lat: 22.541546, lng: 120.353372 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==煉焦一南路。 ( 煉焦一南路與生鐵南路口   lat: 22.541546, lng: 120.353372)， 
//==            ( 煉焦一南路與煉焦一東路口 lat: 22.540584, lng: 120.252048)
//==            ( 煉焦一南路與 爐石東路口  lat: 22.540467, lng: 120.351924 )
//==            ( 爐石東路與 油槽南路口    lat: 22.539166, lng: 120.352903 )
//==            ( 油槽南路東側            lat: 22.539856, lng: 120.353967 )
//==            ( 煤焦化學廠              lat: 22.540813, lng: 120.353247 )
//==comment=====( 原料一東路口 lat: 22.540111, lng: 120.351442  ) 
//==comment=====(煉焦一南路_西端碼頭 lat: 22.541546, lng: 120.353372)
const BluePath9 = {
  path: [
    { lat: 22.541546, lng: 120.353372 },
    { lat: 22.540578, lng: 120.352037 },
    { lat: 22.540467, lng: 120.351924 },
    { lat: 22.539166, lng: 120.352903 },
    { lat: 22.539856, lng: 120.353967 },
    { lat: 22.540813, lng: 120.353247 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==煤焦化學廠路。( 煤焦化學廠與副產二東路  lat: 22.541546, lng: 120.353372)
//==            ( 煤焦化學廠路西側管制口   lat: 22.540157, lng: 120.352190)
const BluePath10 = {
  path: [
    { lat: 22.541376, lng: 120.354018 },
    { lat: 22.540146, lng: 120.352190 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==副產二東路。 (副產二東路北端與生鐵南路   lat: 22.541661, lng: 120.353800)， 
//==            (副產二東路南端與高爐橫五路 lat: 22.538356, lng: 120.356544 )
const BluePath11 = {
  path: [
    { lat: 22.541661, lng: 120.353800 },
    { lat: 22.538356, lng: 120.356544 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==原料一東路口。 (原料一東路北端lat: 22.541546, lng: 120.353372)， ( 原料一東路南端 lat: 22.540111, lng: 120.351442 )
const BluePath12 = {
  path: [
    { lat: 22.544667, lng: 120.345545 },
    { lat: 22.540111, lng: 120.351442 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==水橫一路。 (水橫一路與中興二路 lat: 22.548670, lng: 120.352643 ) 
//==          (水橫一路與動力東路 lat: 22.547756, lng: 120.351320 )
const BluePath13 = {
  path: [
    { lat: 22.548670, lng: 120.352643 },
    { lat: 22.547756, lng: 120.351320 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==水橫二路。 (水橫二路與中興二路 lat: 22.547984, lng: 120.353230 ) 
//==          (水橫二路與動力東路 lat: 22.547042, lng: 120.351939 )
const BluePath14 = {
  path: [
    { lat: 22.547984, lng: 120.353230 },
    { lat: 22.547042, lng: 120.351939 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==生鐵北路。 (生鐵北路與高爐西路   lat: 22.544373, lng: 120.353705) 
//==          (生鐵北路與副產一東路 lat: 22.543172, lng: 120.352074 )
const BluePath15 = {
  path: [
    { lat: 22.544373, lng: 120.353705 },
    { lat: 22.543172, lng: 120.352074 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==副產一東路。 (副產一東路與二號燒結廠 lat: 22.545141, lng: 120.350489 ) 
//==       or   (副產一東路與二號燒結廠 lat: 22.545104, lng: 120.350383  ) 
//==          (副產一東路與生鐵南路     lat: 22.541568, lng: 120.353394 )
const BluePath16 = {
  path: [
    { lat: 22.545104, lng: 120.350383 },
    { lat: 22.541568, lng: 120.353394 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==運河北三路。(運河北三路東側 lat: 22.5418710, lng: 120.3700800)(河北二路東側 水源新直路口 lat: 22.539435, lng: 120.367062)
const BluePath17 = {
  path: [
    { lat: 22.5418710, lng: 120.3700800 },
    { lat: 22.5394350, lng: 120.3670620 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==燒結二南路路。(燒結二南路東側 lat: 22.536462, lng: 120.361864)(燒結二南路與煉焦二東路 lat: 22.533862, lng: 120.358256)
const BluePath18 = {
  path: [
    { lat: 22.536462, lng: 120.361864 },
    { lat: 22.533862, lng: 120.358256 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==高爐南路。(高爐南路東側與中興二路 lat: 22.538091, lng: 120.361481)
//==         (高爐南路與高爐西二路A  lat: 22.537043, lng: 120.359954)
//==         (高爐南路與高爐西二路B  lat: 22.537089, lng: 120.359700)
//==         (高爐南路與煉焦二東路   lat: 22.535238, lng: 120.357119)
const BluePath19 = {
  path: [
    { lat: 22.538091, lng: 120.361481 },
    { lat: 22.537043, lng: 120.359954 },
    { lat: 22.537089, lng: 120.359700 },
    { lat: 22.535238, lng: 120.357119 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==高橫四路。(高橫四路與高橫西路口 lat: 22.541775, lng: 120.355860)
//==         (高橫四路 A          lat: 22.542082, lng: 120.356737)
//==         (高橫四路 B          lat: 22.542156, lng: 120.357136)
//==         (高橫四路 C          lat: 22.542017, lng: 120.357353)
//==         (控制室大樓 A        lat: 22.541812, lng: 120.357708)
//==         (控制室大樓 B        lat: 22.541725, lng: 120.357640)
//==         (HS廢熱回收          lat: 22.542045, lng: 120.357022)
const BluePath20 = {
  path: [
    { lat: 22.541775, lng: 120.355860 },
    { lat: 22.542082, lng: 120.356737 },
    { lat: 22.542156, lng: 120.357136 },
    { lat: 22.542017, lng: 120.357353 },
    { lat: 22.541812, lng: 120.357708 },
    { lat: 22.541725, lng: 120.357640 },
    { lat: 22.542045, lng: 120.357022 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==青年路西段。(青年路上下班鐵門  lat: 22.549585, lng: 120.348030)
//==           (青年路西側鐵門    lat: 22.548304, lng: 120.346241)
const BluePath21 = {
  path: [
    { lat: 22.549585, lng: 120.348030 },
    { lat: 22.548304, lng: 120.346241 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==研究東路  。(研究東路北端    lat: 22.549370, lng: 120.347758)
//==           (研究東路南端    lat: 22.547650, lng: 120.349211)
const BluePath22 = {
  path: [
    { lat: 22.549370, lng: 120.347758 },
    { lat: 22.547650, lng: 120.349211 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};

//==研究中路  。(研究中路北端    lat: 22.548906, lng: 120.347121)
//==           (研究中路南端    lat: 22.547196, lng: 120.348574)
const BluePath23 = {
  path: [
    { lat: 22.548906, lng: 120.347121 },
    { lat: 22.547196, lng: 120.348574 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==研究西路  。(研究西路北端    lat: 22.548470, lng: 120.346484)
//==           (研究西路南端    lat: 22.546737, lng: 120.347952)
const BluePath24 = {
  path: [
    { lat: 22.548470, lng: 120.346484 },
    { lat: 22.546737, lng: 120.347952 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==原料一東路口。 (原料一東路北端lat: 22.541546, lng: 120.353372)， ( 原料一東路南端 lat: 22.540111, lng: 120.351442 )
const BluePath25 = {
  path: [
    { lat: 22.544667, lng: 120.345545 },
    { lat: 22.540111, lng: 120.351442 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
//==警防南路  。(警防南東端    lat: 22.550598, lng: 120.351068)
//==           (警防南西端    lat: 22.548633, lng: 120.348389)
const BluePath26 = {
  path: [
    { lat: 22.550598, lng: 120.351068 },
    { lat: 22.548633, lng: 120.348389 },
  ],
  geodesic: true,
  clickable: true,
  strokeColor: "#04BADE",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 6,
};
onMounted(() => {
  console.log('成功執行')
})



//外層紅框 
const red = [
  { lat: 22.554450, lng: 120.347810 },  //==中鋼大門
  { lat: 22.561130, lng: 120.356975 },  //==中鋼路與沿海路口
  { lat: 22.541017, lng: 120.371999 },  //==沿海路與中林路口
  { lat: 22.527451, lng: 120.354088 },  //==中林路中油廠
  { lat: 22.532268, lng: 120.347436 },  //==中鋼巨蛋
  { lat: 22.532939, lng: 120.347927 },  //==中鋼巨蛋
  { lat: 22.535211, lng: 120.345019 },  //==中鋼巨蛋
  { lat: 22.536046, lng: 120.345995 },
  { lat: 22.538164, lng: 120.343252 },  //==佑泰清潔公司 
  { lat: 22.538571, lng: 120.343534 },  //==佑泰清潔公司
  { lat: 22.541223, lng: 120.340231 },  //==中油104碼頭
  { lat: 22.546447, lng: 120.347465 },  //==碼頭路鋼捲儲區廠
  { lat: 22.548181, lng: 120.346051 },  //==青年路西側
  { lat: 22.550947, lng: 120.349867 },  //==診療所旁
  { lat: 22.554083, lng: 120.347267 },  //==明邦聽西北角
  { lat: 22.554450, lng: 120.347810 },  //==中鋼大門
];
const RedPath = {
  path: red,
  geodesic: true,
  clickable: true,
  strokeColor: "#FF0000",  // 折線的顏色（紅色#FF0000） (綠色#008000)(藍色#04BADE)(黃色#FFFF00)
  strokeOpacity: 1.0,      // 折線的透明度
  strokeWeight: 2,         // 折線的粗細度
};

function road(e) {
  let N = e.latLng.lat()
  let E = e.latLng.lat()
  const { href } = router.resolve({
    name: 'about',
    query: {
      latitude: N,
      longitude: E,
    },
  });
  // 使用 window.open 打開新的分頁
  window.open(href, '_blank');


}

</script>

<template>
  <GoogleMap :tilt="1.5" :heading="322.25" :streetViewControl="false" :api-key="key" class="googleMap" :center="center"
    :zoom="15" :mapTypeId="'satellite'" :mapId="u_id">
    <Marker :options="{ position: center }">
      <InfoWindow>
        <div id="content">
          <div id="siteNotice"></div>
          <h1 id="firstHeading" class="firstHeading">Uluru</h1>
          <div id="bodyContent">
            <p>
              <b>Uluru</b>, also referred to as <b>Ayers Rock</b>, is a large sandstone rock formation in the southern
              part of the Northern Territory, central Australia. It lies 335&#160;km (208&#160;mi) south west of the
              nearest large town, Alice Springs; 450&#160;km (280&#160;mi) by road. Kata Tjuta and Uluru are the two
              major features of the Uluru - Kata Tjuta National Park. Uluru is sacred to the Pitjantjatjara and
              Yankunytjatjara, the Aboriginal people of the area. It has many springs, waterholes, rock caves and
              ancient paintings. Uluru is listed as a World Heritage Site.
            </p>
            <p>
              Attribution: Uluru,
              <a href="https://en.wikipedia.org/w/index.php?title=Uluru&oldid=297882194">
                https://en.wikipedia.org/w/index.php?title=Uluru</a>
              (last visited June 22, 2009).
            </p>
          </div>
        </div>
      </InfoWindow>
    </Marker>
    <Polyline :options="RedPath" />
    <Polyline :options="BluePath" @click="road" />
    <Polyline :options="BluePath2" @click="road"/>
    <Polyline :options="BluePath3" @click="road"/>
    <Polyline :options="BluePath4" @click="road"/>
    <Polyline :options="BluePath5" @click="road"/>
    <Polyline :options="BluePath6" @click="road"/>
    <Polyline :options="BluePath7" @click="road"/>
    <Polyline :options="BluePath8" @click="road"/>
    <Polyline :options="BluePath9" @click="road"/>
    <Polyline :options="BluePath10" @click="road"/>
    <Polyline :options="BluePath11" @click="road"/>
    <Polyline :options="BluePath12" @click="road"/>
    <Polyline :options="BluePath13" @click="road"/>
    <Polyline :options="BluePath14" @click="road"/>
    <Polyline :options="BluePath15" @click="road"/>
    <Polyline :options="BluePath16" @click="road"/>
    <Polyline :options="BluePath17" @click="road"/>
    <Polyline :options="BluePath18" @click="road"/>
    <Polyline :options="BluePath19" @click="road"/>
    <Polyline :options="BluePath20" @click="road"/>
    <Polyline :options="BluePath21" @click="road"/>
    <Polyline :options="BluePath22" @click="road"/>
    <Polyline :options="BluePath23" @click="road"/>
    <Polyline :options="BluePath24" @click="road"/>
    <Polyline :options="BluePath25" @click="road"/>
    <Polyline :options="BluePath26" @click="road"/>
  </GoogleMap>
</template>


<style>
.googleMap {
  width: 100%;
  height: 100vh;

}
</style>
