<template>
    <div class="productList">
        <table>
            <thead>
                <tr>
                    <th>Mã sản phẩm</th>
                    <th>Tên sản phẩm</th>
                    <th>Giá</th>
                    <th>Số lượng</th>
                    <th>Trạng thái</th>
                    <th>Hành động</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(product, index) in data" :key="index">
                    <td>{{ product.id }}</td>
                    <td class="productName">{{ product.name }}</td>
                    <td>{{ formatMoney(product.price) }} đ</td>
                    <td>{{ product.qty }}</td>
                    <td v-if="product.status" class="notEmpty">Còn hàng</td>
                    <td v-else class="isEmpty">Hết hàng</td>
                    <td>
                        <button class="btnEdit">Sửa</button>
                        <button class="btnDelete" @click="deleteProduct">Xóa</button>
                    </td>
                </tr>
                <tr>
                    <td>SP987457487584</td>
                    <td class="productName">Bánh kem</td>
                    <td>50.000 đ</td>
                    <td>0</td>
                    <td>Hết hàng</td>
                    <td>
                        <button class="btnEdit">Sửa</button>
                        <button class="btnDelete">Xóa</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: "ProductList",
    props: ['data'],
    methods: {
        formatMoney: function (money) {
            return Intl.NumberFormat().format(money);
        },

        deleteProduct: function () {
            console.log(this.id);
        }
    }
}
</script>

<style lang="scss" scoped>
    .productList {
        width: 95%;
        margin: 0 auto;

        table {
            width: 100%;
            background-color: #EFF2F6;
            border: 2px solid #EFF2F6;

            thead {
                background-color: #F2F6FE;
                line-height: 200%;
            }

            tbody {
                background-color: #ffff;
                text-align: left;
                text-indent: 10px;
                line-height: 2;
                font-size: 14px;

                tr {

                    .productName {
                        color: #67BBF6;
                    }

                    .btnEdit {
                        background-color: #F2994A;
                        color: #ffff;
                        font-weight: bold;
                        border-radius: 5px;
                        border: none;
                        cursor: pointer;
                        outline: none;
                        padding: 7px 12px;
                        margin-right: 5px;
                        margin-top: 5px;
                        margin-bottom: 5px;
                    }

                    .btnDelete {
                        color: #ffff;
                        background-color: #F54B5E;
                        font-weight: bold;
                        border-radius: 5px;
                        border: none;
                        cursor: pointer;
                        outline: none;
                        padding: 7px 12px;
                        margin-bottom: 5px;
                        margin-top: 5px;
                    }

                    .isEmpty {
                        color: #dc3545;
                    }

                    .notEmpty {
                        color: #2ecc71;
                    }
                }
            }
        }
        
    }
</style>
