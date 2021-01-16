<template>
    <div class="productForm">
        <h3>Sản phẩm</h3>
        <p>Tên sản phẩm <span>(*)</span></p>
        <input type="text"
            placeholder="Nhập tên sản phảm"
            v-model="productName"
            @input="changeProductName"
        >
        <div class="error">
            <p class="textError" v-show="nameError">Tên sản phẩm không được để trống</p>
        </div>
        <p>Đơn giá <span>(*)</span></p>
        <input type="text"
            placeholder="Nhập đơn giá sản phảm"
            v-model="productPrice"
            @input="changeProductPrice"
        >
        <div class="error">
            <p class="textError" v-show="priceError">Giá sản phẩm không được để trống</p>
        </div>
        <p>Số lượng <span>(*)</span></p>
        <input type="text"
            placeholder="Nhập số lượng sản phảm"
            v-model="productQty"
            @input="changeProductQty"
        >
        <div class="error">
            <p class="textError" v-show="qtyError">Số lượng sản phẩm không được để trống</p>
        </div>
        <div class="btn">
            <button class="btnCreate" @click="submit">Tạo mới</button>
            <button class="btnCancel" @click="cancel">Hủy</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProductForm",

    data () {
        return {
            productName: '',
            productPrice: '',
            productQty: '',
            nameError: '',
            priceError: '',
            qtyError: '',
            products: [],
        }
    },

    methods: {
        submit: function () {
            if(!this.productName.length > 0) {
                this.nameError = true;
            }
            if(!this.productPrice.length > 0) {
                this.priceError = true;
            }
            if(!this.productQty.length > 0) {
                this.qtyError = true;
            }

            if(this.productName.length > 0 && this.productPrice.length > 0 && this.productQty.length > 0) {
                if(this.productQty > 0){
                    let product = {
                        id: 'SP' + Math.floor(100000 + Math.random() * 900000),
                        name: this.productName,
                        price: this.productPrice,
                        qty: this.productQty,
                        status: true
                    }
                    this.products.push(product);

                }else {
                    let product = {
                        id: 'SP' + Math.floor(100000 + Math.random() * 900000),
                        name: this.productName,
                        price: this.productPrice,
                        qty: this.productQty,
                        status: false,
                        
                    }
                    this.products.push(product);
                }

                console.log(this.products);
                this.productName  = '';
                this.productPrice = '';
                this.productQty   = '';
                this.$emit('data', this.products);
            }
        },

        cancel: function () {
            this.productName  = '';
            this.productPrice = '';
            this.productQty   = '';
        },

        changeProductName: function () {
            return this.nameError = false;
        },

        changeProductPrice: function () {
            return this.priceError = false;
        },

        changeProductQty: function () {
            return this.qtyError = false;
        }
    },
}
</script>

<style lang="scss" scoped>
    .productForm {
        width: 90%;
        margin: 10px auto;
        h3 {
            color: #67BBF6;
            text-align: left;
        }
        p {
            text-align: left;
            font-size: 14px;
            font-weight: bold;
            margin-bottom: 0px;
            margin-top: 10px;

            span {
                color: #F66296;
            }
        }

        input {
            width: 100%;
            padding: 10px 0;
            border: 1px solid #EFF2F6;
            border-radius: 5px;
            text-indent: 10px;

        }
        .error {
            width: 100%;
            height: 14px;

            p {
                width: 100%;
                text-align: left;
                font-size: 12px;
                color: #dc3545;
                margin: 0;
                font-weight: normal;
            }
        }

        .btn {
            text-align: right;
            .btnCreate {
                background-color: #0080DD;
                color: #fff;
                font-weight: bold;
                padding: 10px;
                border-radius: 5px;
                border: 2px solid #000;
                outline: none;
                cursor: pointer;
                margin-right: 5px;
            }
            .btnCancel {
                font-weight: bold;
                padding: 10px 20px;
                border-radius: 5px;
                outline: none;
                cursor: pointer;
            }
        }
    }
</style>
