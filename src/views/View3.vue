<template>
    <div>
        <div id="container"></div>
        <button @click="addTraffic">创建卫星与路网图层</button>
        <button @click="showTraffic">显示图层</button>
        <button @click="hideTraffic">隐藏图层</button>
    </div>
</template>

<script>
import {initAMap, destroy} from '../utils/amapUtils'

export default {
    name: "View3",
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
            const traffic = new AMap.TileLayer.Satellite();
            //创建路网图层
            var roadNet = new AMap.TileLayer.RoadNet();
            this.traffic = traffic;
            this.map.setLayers([traffic, roadNet]);
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
        initAMap(this);
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
    height: 90vh;
}
</style>
