<template>
    <el-container>
        <el-aside>
            <el-menu>
                <el-menu-item>
                    <template><i class="el-icon-menu"></i>Tổng quan</template>
                </el-menu-item>
                <el-menu-item class="productControl">
                    <template ><i class="el-icon-s-shop"></i>Quản lý sản phẩm</template>
                </el-menu-item>
                <el-menu-item>
                    <template><i class="el-icon-document"></i>Quản lý hóa đơn</template>
                </el-menu-item>
                <el-menu-item>
                    <template><i class="el-icon-s-data"></i>Báo cáo thống kê</template>
                </el-menu-item>
                <el-submenu index="1">
                    <template slot="title"><i class="el-icon-location"></i><span style="color: #fff">Quản lý chi nhánh</span></template>
                    <el-menu-item-group title="Hoạt động">
                        <el-menu-item index="1-1">Sản phẩm</el-menu-item>
                        <el-menu-item index="1-2">Đơn hàng</el-menu-item>
                        <el-menu-item index="1-3">Khách hàng</el-menu-item>
                    </el-menu-item-group>
                    <el-menu-item-group title="Báo cáo">
                        <el-menu-item index="1-4">Doanh thu</el-menu-item>
                        <el-menu-item index="1-5">Tồn kho</el-menu-item>
                    </el-menu-item-group>
                </el-submenu>
                <el-menu-item>
                    <template><i class="el-icon-setting"></i>Cài đặt hệ thống</template>
                </el-menu-item>
            </el-menu>
        </el-aside>

        <el-container>
            <el-header>
                <el-row>
                    <el-col :span="14" class="title">
                        <slot name="title"></slot>
                    </el-col>
                    <el-col :span="10" class="avatar">
                        <i class="el-icon-bell"
                            style="margin-right: 20px; font-size: 18px; margin-bottom: 20px">
                        </i>
                        <el-dropdown>
                            <el-avatar :size="40" :src="circleUrl"></el-avatar>
                            <el-dropdown-menu slot="dropdown">
                                <el-dropdown-item>Thông tin tài khoản</el-dropdown-item>
                                <el-dropdown-item>Đổi mật khẩu</el-dropdown-item>
                                <el-dropdown-item>Cấu hình</el-dropdown-item>
                                <el-dropdown-item>Đăng xuất</el-dropdown-item>
                            </el-dropdown-menu>
                        </el-dropdown>
                    </el-col>
                </el-row>
                
            </el-header>

            <slot name="table"></slot>
        </el-container>
    </el-container>
</template>

<script>
export default {
    name: 'BaseLayout',
    data() {
        return {
            circleUrl: "https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png",
        }
    },
    methods: {
        handleSizeChange(val) {
            console.log(`${val} items per page`);
        },
        handleCurrentChange(val) {
            console.log(`current page: ${val}`);
        }
    },
}
</script>
<style lang="scss" scoped>
    .el-container {
        height: 700px;
        .el-header {
            background-color: #dae6f6;
            line-height: 60px;

            .el-row {
                .title {
                    text-align: left;
                    font-weight: bold;
                }
                .avatar {
                    text-align: right;

                    .el-dropdown {
                        margin-top: 10px;
                    }
                }
            }

        }
        
        .el-aside {
            width: 200px;
            background-color: #001529;
            text-align: left;

            .el-menu-item {
                background-color: #001529;
                color: #fff;
            }
            .productControl {
                color: #FFD04B !important;
                i {
                    color: #FFD04B !important;
                }
            }

            .el-submenu {
                color: #fff;
                background-color: #001529;
                
                .titleSubmenu {
                    color: #fff;
                }

                .el-menu-item-group {
                    background-color: #001529;
                }
            .el-menu-item:hover {
                background-color: #001529 !important;
            }

            .el-submenu:hover {
                background-color: #001529 !important;
            }
        }
    }
}

</style>