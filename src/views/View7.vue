<template>
    <div>
        <div id="container"></div>
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
            marker1: null,
            marker2: null,
        }
    },
    watch:
        {
            map(map)
            {
                if (map)
                {
                    this.map.on('click', (e) =>
                    {
                        console.log(e.lnglat)
                        if (this.marker1 == null)
                        {
                            console.log("1")
                            this.marker1 = new AMap.Marker({
                                position: e.lnglat
                            })
                            this.map.add(this.marker1)
                            return;
                        }
                        if (this.marker1 != null)
                        {
                            this.marker2 = new AMap.Marker({
                                position: e.lnglat
                            })
                            this.map.add(this.marker2)
                            console.log(this.marker1.getPosition())
                            const position = this.marker1.getPosition()
                            const distance = position.distance(e.lnglat);
                            window.alert("距离：" + distance + "米");
                            //lnglat1向东1000m，向北500m的位置的经纬度
                            const lnglat3 = e.lnglat.offset(1000, 500)
                            const marker3 = new AMap.Marker({
                                position: lnglat3
                            })
                            this.map.add(marker3);
                            this.map.remove(this.marker1)
                            this.map.remove(this.marker2)
                            this.marker1 = null;
                            this.marker2 = null;
                        }
                    })
                }
            }
        },
    methods: {},
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
