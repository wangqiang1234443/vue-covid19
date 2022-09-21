<template>
    <div>
        <p class="title"><i></i>疫情地图</p>
        <Tabs :currentIndex="currentIndex" @onIndex="getIndex">
            <Tab index="1" label="国内疫情">
                <div id="chinaMap"></div>
            </Tab>
            <Tab index="2" label="国外疫情">
                <div id="worldMap"></div>
            </Tab>
        </Tabs>
    </div>
</template>

<script>
import api from "../api";
import axios from "axios";

export default {
    data() {
        return {
            currentIndex: "1",
        };
    },
    mounted() {
        function nocvCity() {
            return axios.get(
                "http://api.tianapi.com/txapi/ncovcity/index?key=62e34ad34025d5d5127135efa58d4ca8"
            );
        }

        function nocvaBroad() {
            return axios.get(
                "http://api.tianapi.com/txapi/ncovabroad/index?key=62e34ad34025d5d5127135efa58d4ca8"
            );
        }
        // 合并网络请求
        axios.all([nocvCity(), nocvaBroad()]).then(
            axios.spread((nocvCity, nocvaBroad) => {
                // 两个请求现在都执行完成
                let allCitys = [];
                for (let i = 0; i < nocvCity.data.newslist.length; i++) {
                    let temp = {
                        name: nocvCity.data.newslist[i].provinceShortName,
                        value: nocvCity.data.newslist[i].currentConfirmedCount,
                    };
                    allCitys.push(temp);
                }
                //  { name: '俄罗斯', value: 28397.812 },
                let worlds = [];
                for(let j = 0;j<nocvaBroad.data.newslist.length;j++){
                    let temp = {
                        name:nocvaBroad.data.newslist[j].provinceName,
                        value:nocvaBroad.data.newslist[j].currentConfirmedCount
                    }
                    worlds.push(temp)
                }
                this.$charts.chinaMap("chinaMap", allCitys);
                this.$charts.worldMap("worldMap",worlds);
            })
        );
    },
    methods: {
        getIndex(index) {
            this.currentIndex = index;
        },
    },
};
</script>

<style scoped>
#chinaMap {
    width: 375px;
    height: 400px;
}
#worldMap {
    width: 375px;
    height: 400px;
}
.title {
    border-top: 0.005rem solid #ebebeb;
    border-bottom: 0;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    -webkit-box-pack: start;
    -ms-flex-pack: start;
    justify-content: flex-start;
    height: 0.44rem;
    padding: 0 0.16rem;
    font-weight: 500;
    font-size: 0.17rem;
    line-height: 0.44rem;
    background: #fff;
}
.title::before {
    content: "";
    width: 5px;
    height: 20px;
    background: #4169e2;
    margin-right: 10px;
}
</style>