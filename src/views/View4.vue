<template>
    <div>
        <div id="container"></div>
        <button @click="addTraffic">创建楼块图层</button>
        <button @click="showTraffic">显示楼块图层</button>
        <button @click="hideTraffic">隐藏楼块图层</button>
    </div>
</template>

<script>
import {initAMap, destroy} from '../utils/amapUtils'

export default {
    name: "View4",
    data()
    {
        return {
            map: null,
            traffic: null,
        }
    },
    methods: {
        addTraffic()
        {
            if (this.traffic)
            {
                return;
            }
            const traffic =  new AMap.Buildings({
                zooms: [17, 20],
                zIndex: 10,
                heightFactor: 2, //2倍于默认高度（3D 视图下生效）
            });
            this.traffic = traffic;
            this.map.add(traffic);
        },
        showTraffic()
        {
            if (this.traffic)
            {
                this.traffic.show();
            }
        },
        hideTraffic()
        {
            if (this.traffic)
            {
                this.traffic.hide();
            }
        }
    },
    created()
    {
        console.log("初始化")
        initAMap(this,undefined,{
            center: [116.397428, 39.90923], //地图中心点
            viewMode: "3D", //地图模式
            pitch: 60, //俯仰角度
            rotation: -35, //地图顺时针旋转角度
            zoom: 17, //地图级别
            showBuildingBlock: false,
        });
    },
    beforeDestroy()
    {
        console.log("销毁")
        destroy(this.map)
    },
}
</script>

<style scoped>
#container {
    padding: 0px;
    margin: 0px;
    width: 100%;
    height: 88vh;
}
</style>
