<template>
    <div>
        <div id="city"></div>
    </div>
</template>

<script>
import api from "../api";
export default {
    props: {
        city: {
            type: String,
            default: "",
        },
    },
    mounted() {
        var citys = [];
        api.getNocvCity({
            key: "62e34ad34025d5d5127135efa58d4ca8",
        }).then((res) => {
            if (res.status === 200) {
                for (var i = 0; i < res.data.newslist.length; i++) {
                    if (res.data.newslist[i].provinceShortName === this.city) {
                        for (
                            var j = 0;
                            j < res.data.newslist[i].cities.length;
                            j++
                        ) {
                            var temp = {
                                name: res.data.newslist[i].cities[j].cityName+"市",
                                value:
                                    res.data.newslist[i].cities[j].currentConfirmedCount,
                            };
                            citys.push(temp);
                        }
                    }
                }
            }
            this.$charts.provinceMap("city", this.city, citys);
        });
    },
};
</script>

<style scoped>
#city {
    width: 375px;
    height: 500px;
}
</style>