<template>
    <div>
        <div id="container"></div>
        <button @click="add">添加像素点</button>
    </div>
</template>

<script>
import {initAMap, destroy} from '../utils/amapUtils'

export default {
    name: "View8",
    data()
    {
        return {
            map: null,
        }
    },
    methods: {
        add()
        {
            const offset = new AMap.Pixel(-16, -30);
            const marker = new AMap.Marker({
                position: [113, 23],
                offset: offset,
            });
            this.map.add(marker);
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
