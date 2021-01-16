<template>
    <div class="container">
        <div class="leftWarp">
            <ProductForm @data="handleData" />
        </div>
        <div class="rightWarp">
            <ProductList :data="data" />
        </div>
    </div>
</template>

<script>
import ProductForm from "./ProductForm.vue";
import ProductList from "./ProductList.vue";
export default {
    name: "Exercise",
    components: {
        ProductForm,
        ProductList
    },

    data () {
        return {
            data: [],
        }
    },

    methods: {
        handleData: function (data) {
            this.data = data;
            console.log(this.data);
        }
    }
}
</script>

<style lang="scss" scoped>
    .container {
        width: 100%;
        display: flex;

        .leftWarp {
            width: 30%;
            border: 2px solid #EFF2F6;
            margin: 0;
        }

        .rightWarp {
            width: 70%;
        }
    }
</style>
