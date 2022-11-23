<template>
    <div class="number-container d-flex justify-content-center align-items-center">
        <!-- 减 1 的按钮 -->
        <button @click="sub" type="button" class="btn btn-light btn-sm">-</button>
        <!-- 购买的数量 -->
        <span class="number-box">{{ goods.goods_count }}</span>
        <!-- 加 1 的按钮 -->
        <button @click="add" type="button" class="btn btn-light btn-sm">+</button>
    </div>
</template>
  
<script>

export default {

    props: {
        goods: {
            default: {},
            type: Object
        }
    },

    data() {
        return {

        };
    },

    mounted() {

    },

    methods: {
        sub() {
            // console.log('counter.vue sub');
            if (this.goods.goods_count <= 1) {
                return;
            } else {
                this.$emit('num_change', this.goods.goods_count - 1);
            }
        },

        add() {
            // console.log('counter.vue add');
            this.$emit('num_change', this.goods.goods_count + 1);
        }
    },
};
</script>


<style lang="less" scoped>
.number-box {
    min-width: 30px;
    text-align: center;
    margin: 0 5px;
    font-size: 12px;
}

.btn-sm {
    width: 30px;
}
</style>


