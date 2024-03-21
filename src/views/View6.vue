<template>
    <div>
        <div id="container"></div>
        <button @click="addPoint1">添加点1</button>
        <button @click="addPoint2">添加点2</button>
    </div>
</template>

<script>
import {initAMap, destroy} from '../utils/amapUtils'

export default {
    name: "View6",
    data()
    {
        return {
            map: null,
        }
    },
    methods: {
        addPoint1()
        {
            const marker = new AMap.Marker({
                title: '标记点1',
                position: new AMap.LngLat(113.34, 23.6532),
            })
            this.map.add(marker)
        },
        addPoint2()
        {
            const marker = new AMap.Marker({
                title: '标记点1',
                position: [114.45, 23.765]
            })
            this.map.add(marker)
        },

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
