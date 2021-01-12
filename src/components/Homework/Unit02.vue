<template>
    <div class="container">
        <div class="leftWarp">
            <div class="formSearch">
                <img src="https://cdn2.iconfinder.com/data/icons/ios-7-icons/50/search-512.png" 
                    class="searchIcon"
                >
                <input 
                    type="text" 
                    id="inputSearch"
                    :style="{ border: color }"
                    v-model="keyword" 
                    @focus="changeColor()"
                    @blur="removeColor()"
                    @keydown.enter="search"
                    placeholder="Tìm kiếm theo tên sản phẩm"
                >
                <img 
                    src="https://cdn.iconscout.com/icon/premium/png-512-thumb/clear-16-216586.png" 
                    class="clearIcon" 
                    v-show="inputSearchChange" 
                    @click="clearSearch()"
                >
            </div>
            <table class="table">
                <thead>
                    <tr>
                        <th>STT</th>
                        <th>Sản phẩm</th>
                        <th>Giá</th>
                        <th>Số lượng</th>
                        <th>Trạng thái</th>
                        <th>Hành động</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(product, index) in list" :key='index'>
                        <td>{{ index + 1}}</td>
                        <td class="productName" v-if="product.image == ''">
                            <img src="https://cdn4.iconfinder.com/data/icons/ionicons/512/icon-image-512.png" 
                                class="productImage"
                            >
                            {{ product.name }}
                        </td>
                        <td v-else class="productName">
                            <img :src="product.image" class="productImage">
                            {{ product.name }}
                        </td>
                        <td>{{ formatMoney(product.price) }}</td>
                        <td>{{ product.quantity }}</td>
                        <td v-if="product.isAvailable"><span class="available">Còn hàng</span></td>
                        <td v-else><span class="notAvailable">Hết hàng</span></td>
                        <td><button class="addToCart" @click="addToCart(product)">Thêm vào giỏ</button></td>
                    </tr>
                </tbody>
                
                <tbody v-show="this.value.length > 0 && this.resultSearch.length == 0">
                    <tr>
                        <td colspan="5">Không có sản phẩm</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <div class="rightWarp">
            <p class="title">Giỏ hàng</p>
            <table>
                <tr v-for="product in carts" :key="product">
                    <td class="productName" v-if="product.image == ''">
                        <img src="https://cdn4.iconfinder.com/data/icons/ionicons/512/icon-image-512.png" 
                            class="productImage"
                        >
                        <p class="name">{{ product.name }}</p>
                        <p class="price">{{ formatMoney(product.price) }} đ</p>
                        
                    </td>
                    <td v-else class="productName">
                        <img :src="product.image" class="productImage">
                        <p class="name">{{ product.name }}</p>
                        <p class="price">{{ formatMoney(product.price) }} đ</p>
                    </td>
                    <td>
                        <input type="number" class="quantity" :value="product.quantity">
                    </td>
                    <td>
                        <button class="btnRemove" @click="removeToCart(product)">Remove</button>
                    </td>
                    
                </tr>
            </table>
            <div v-if="this.carts.length == 0" class="cart">
                <span class="cartText">Không có sản phẩm nào được thêm vào giỏ</span>
            </div>
            <div class="cart">
                <div class="cartProduct">
                    
                </div>
            </div>
            <div class="cartTotal">
                <span>Tổng tiền: {{ formatMoney(total) }} đ</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'HomeworkUnit02',
    data() {
        return {
            resultSearch: [],
            keyword: "",
            value: "",
            carts: [],
            color: "",
            products: [
                {
                    name: 'iPhone 12 Pro Max Chính Hãng',
                    image: 'https://cdn.cellphones.com.vn/media/catalog/product/cache/1/image/9df78eab33525d08d6e5fb8d27136e95/p/h/photo_2020-10-13_22-12-24.jpg_1_2.png',
                    price: 32990000,
                    quantity: 566,
                    isAvailable: true
                },
                {
                    name: 'iPhone 12 Chính Hãng (VN/A)',
                    image: '',
                    price: 21790000,
                    quantity: 123,
                    isAvailable: true
                },
                {
                    name: 'iPhone 11 Chính hãng',
                    image: 'https://cdn.cellphones.com.vn/media/catalog/product/cache/1/image/9df78eab33525d08d6e5fb8d27136e95/_/0/_0004_layer_5.jpg',
                    price: 16690000,
                    quantity: 0,
                    isAvailable: false
                },
                {
                    name: 'Apple iPhone XR 64GB Chính hãng(VN/A)',
                    image: 'https://cdn.cellphones.com.vn/media/catalog/product/cache/1/image/9df78eab33525d08d6e5fb8d27136e95/i/p/iphone-xr_5_.jpg',
                    price: 12190000,
                    quantity: 1023,
                    isAvailable: true
                },
                {
                    name: 'iPhone 11 Pro Max Chính hãng(VN/A)',
                    image: '',
                    price: 26500000,
                    quantity: 45,
                    isAvailable: true
                }
            ]
        }
    },
    methods: {
        changeColor: function () {
            this.color = "2px solid #4e99e4";
        },

        removeColor: function () {
            this.color = "";
        },
        
        search: function () {
            this.value = this.keyword;
            this.resultSearch = [];
            this.products.forEach(product => {
                if(product.name.toLowerCase().includes(this.keyword.toLowerCase())){
                    this.resultSearch.push(product);
                }
            });
        },

        clearSearch: function () {
            this.keyword = "";
            this.value = this.keyword;
        },

        addToCart: function (product) {
            let isInCart = false;
            if (product.isAvailable) {
                this.carts.forEach((item) => {
                    if(product.name == item.name){
                        item.quantity += 1;
                        isInCart = true;
                    }
                });
                if(!isInCart) {
                    product.quantity = 1;
                    this.carts.push(product);
                    console.log(this.carts.quantity)
                }
            }else {
                alert("Sản phẩm hết hàng");
            }
            
        },

        formatMoney: function (money) {
            return Intl.NumberFormat().format(money);
        },

         removeToCart: function (product) {
             console.log(product);
         }
    },

    computed: {
        inputSearchChange: function () {
            if (this.keyword != '') {
                return true;
            }else {
                return false;
            }
        },

        list: function () {
            if (this.resultSearch.length >= 0 && this.value.length > 0) {
                return this.resultSearch; 
            } else {
                return this.products;
            }
        },

        total: function () {
            let total = 0;  
            this.carts.forEach((item) => {
                total = total + +item.quantity * item.price;
            });
            return total;
        },
        
        formatString (string) {
             if(string.length > 25) {
                return string.substr(0, 24) + '...';
             } else {
                return string;
             }
        },
    },
}
</script>

<style lang="scss" scoped>
    .container {
        .leftWarp {
            margin-right: 0;
            float: left;
            width: 64%;
            .formSearch {
                margin-bottom: 20px;
                height: 30px;
                width: 100%;
                input {
                    border: 1px solid #b4bfbb;
                    position: absolute;
                    padding: 10px 10px;
                    padding-left: 40px;
                    border-radius: 5px;
                    text-align: left;
                    font-size: 16px;
                    outline: none;
                    width: 20%;
                    left: 7px;
                }
                .searchIcon {
                    position: absolute;
                    z-index: 999;
                    width: 20px;
                    left: 15px;
                    top: 70px;
                }
                .clearIcon {
                    position: absolute;
                    z-index: 999;
                    width: 20px;
                    left: 335px;
                    top: 70px;
                }
            }
            table {
                border: 1px solid #b4bfbb;
                text-align: center;
                margin-top: 40px;
                clear: both;
                width: 100%;
                tr {
                    width: 100%;
                }
                p {
                    text-align: center;
                    width: 100%;
                }
                
                th{
                    background: #f2f6fe;
                    padding: 10px 19px;
                } 

                td {
                    padding: 20px 20px;
                    .available {
                        color:#2ecc71;
                    }
                    .notAvailable {
                        color: red;
                    }
                    .addToCart {
                        background: #0080dd;
                        border-radius: 5px;
                        font-weight: bold;
                        padding: 5px 10px;
                        font-size: 14px;
                        color: white;
                        line-height: 2;
                        border: 0px;
                    }
                }
                .productName {
                    text-align: left;
                    color: #3737df;
                    .productImage {
                        position: relative;
                        width: 30px;
                        top: 8px;
                    }
                }
            }
        }

        .rightWarp {
            border: 1px solid #b4bfbb;
            margin-top: 70px;
            height: 500px;
            float: right;
            width: 35%;
            .title {
                text-indent: 20px;
                font-weight: bold;
                text-align: left;
            }
            .cart {
                position: relative;
                .cartText {
                    position: absolute;
                    text-align: center;
                    top: 80px;
                    left: 25%;
                }
            }
            .cartTotal {
                position: absolute;
                font-weight: bold;
                color: #dc3545;
                right: 20px;
                bottom: 100px;
            }
            table {
                width: 100%;
                tr {
                    margin-bottom: 10px;
                    border-bottom: 1px solid ;
                    .productName {
                        margin-left: 5px;
                        text-align: left;
                        color: #3737df;
                        line-height: 2;
                        .productImage {
                            position: relative;
                            width: 30px;
                            top: 8px;
                        }
                    }

                    td {
                        .btnRemove {
                            background: #dc3545;
                            border-radius: 5px;
                            font-weight: bold;
                            padding: 5px 10px;
                            color: #ffff;
                            line-height: 2;
                            border: 0;
                        }
                        .quantity {
                            width: 30%;
                        }
                        .price {
                            font-size: 14px;
                            color: #9e949d;
                            margin: 0;
                        }
                        .name {
                            color: black;
                            font-weight: bold;
                            margin-bottom: 0;
                        }
                    }
                    
                }
            }
        }
    }
</style>
