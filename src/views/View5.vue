<template>
    <div>
        <div id="container"></div>
        <button @click="addItem1">添加工具条</button>
        <button @click="showItem(0)">显示工具条</button>
        <button @click="hideItem(0)">隐藏工具条</button>
        <button @click="addItem2">添加比例尺</button>
        <button @click="showItem(1)">显示比例尺</button>
        <button @click="hideItem(1)">隐藏比例尺</button>
        <button @click="addItem3">添加鹰眼</button>
        <button @click="showItem(2)">显示鹰眼</button>
        <button @click="hideItem(2)">隐藏鹰眼</button>
        <button @click="addItem4">添加控制控件</button>
        <button @click="showItem(3)">显示控制控件</button>
        <button @click="hideItem(3)">隐藏控制控件</button>

    </div>
</template>

<script>
import {initAMap, destroy} from '../utils/amapUtils'

export default {
    name: "View1",
    data()
    {
        return {
            map: null,
            itemList: {
                item1: null,
                item2: null,
                item3: null,
                item4: null,
            }
        }
    },
    methods: {
        addItem1()
        {
            if (this.itemList.item1)
            {
                return;
            }
            AMap.plugin('AMap.ToolBar', () =>
            {
                this.itemList.item1 = new AMap.ToolBar();
                this.map.addControl(this.itemList.item1);
            });
        },
        addItem2()
        {
            if (this.itemList.item2)
            {
                return;
            }
            AMap.plugin('AMap.Scale', () =>
            {
                this.itemList.item2 = new AMap.Scale();
                this.map.addControl(this.itemList.item2);
            });
        },
        addItem3()
        {
            if (this.itemList.item3)
            {
                return;
            }
            AMap.plugin('AMap.HawkEye', () =>
            {
                this.itemList.item3 = new AMap.HawkEye();
                this.map.addControl(this.itemList.item3);
            });
        },
        addItem4()
        {
            if (this.itemList.item4)
            {
                return;
            }
            AMap.plugin('AMap.ControlBar', () =>
            {
                this.itemList.item4 = new AMap.ControlBar();
                this.map.addControl(this.itemList.item4);
            });
        },

        showItem(index)
        {
            const key = Object.keys(this.itemList)[index];
            this.itemList[key].show();
        },
        hideItem(index)
        {
            const key = Object.keys(this.itemList)[index];
            this.itemList[key].hide();
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
    height: 88vh;
}
</style>
