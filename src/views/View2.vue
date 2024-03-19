<template>
    <div>
        <div id="container"></div>
        <button @click="addLayer">加载图层</button>
        <button @click="addTraffic">创建实时交通路况图层</button>
        <button @click="showTraffic">显示路况图层</button>
        <button @click="hideTraffic">隐藏路况图层</button>
    </div>
</template>

<script>
import {initAMap, destroy} from '../utils/amapUtils'

export default {
    name: "View2",
    data()
    {
        return {
            map: null,
            traffic: null,
        }
    },
    methods: {
        addLayer()
        {
            const layer = new AMap.createDefaultLayer({
                zooms: [3, 20], //可见级别
                visible: true, //是否可见
                opacity: 1, //透明度
                zIndex: 0, //叠加层级
            });
            this.map.setLayers(layer);
        },
        addTraffic()
        {
            if (this.traffic)
            {
                return;
            }
            const traffic = new AMap.TileLayer.Traffic({
                autoRefresh: true, //是否自动刷新，默认为false
                interval: 60, //刷新间隔，默认180s
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
