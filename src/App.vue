<template>
    <div class="app-container">
        <Header :title="title">
            <div class="header-container">{{ title }}</div>
        </Header>
        <Goods v-for="goods in list" :key="goods.id" :goods="goods" @change_checked="change_checked">
            <!-- 默认槽的使用! -->
            <Counter :goods="goods" @num_change="num_change(goods, $event)"></Counter>
        </Goods>
        <Footer :list="list" @all_checked="all_checked"></Footer>
    </div>
</template>

<script>
import axios from 'axios'

import Header from '@/components/header/Header.vue'
import Goods from '@/components/goods/Goods.vue'
import Footer from '@/components/footer/Footer.vue'
import Counter from '@/components/counter/Counter.vue'

export default {
    data() {
        return {
            title: '购物车案例',
            list: []
        }
    },

    created() {
        this.initGoods();
    },

    methods: {
        async initGoods() {
            var result = await axios.get("http://localhost:8888/initGoods")
            /** 页面需要渲染的东西, 理论上都应该在 data 中定义! */
            // console.log(result);
            if (result.status === 200) {
                this.list = result.data;
            }
        },

        change_checked: function (obj) {
            // console.log(obj);
            var id = obj.goods_id;
            var goods_state = obj.goods_state;
            this.list.some((item, index) => {
                if (id === item.id) {
                    this.list[index].goods_state = goods_state;
                    return true;
                }
            })
        },

        all_checked: function (checked) {
            this.list.forEach((item, index) => {
                this.list[index].goods_state = checked;
            });
        },

        num_change: function(goods, val) {
            goods.goods_count = val;
        }
    },

    mounted() {
    },

    // 注册组件
    components: {
        Header,
        Goods,
        Footer,
        Counter
    },

}
</script>

<style lang="less" scoped>
.app-container {
    padding-top: 45px;
    padding-bottom: 50px;
}
</style>
