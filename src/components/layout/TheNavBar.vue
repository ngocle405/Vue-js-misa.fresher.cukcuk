<template>
   <div class="m-navbar">
        <div class="m-logo-site">
            <div class="m-icon-toggle"></div>
            <div class="m-cukcuk-logo"></div>
        </div>
        <div class="m-navbar-content">
            <div class="m-navbar-item">
                <div class="m-icon-dashboard"></div>
                <div class="m-nav-item-text">Tổng quan</div>
            </div>
            <div class="m-navbar-item">
                <div class="m-icon-report"></div>
                <div class="m-nav-item-text">Báo cáo</div>
            </div>
            <div class="m-navbar-item">
                <div class="m-icon-dashboard"></div>
                <div class="m-nav-item-text">Mua hàng</div>
            </div>
            <router-link to="/customer" style="text-decoration: none;color: black;" class="m-navbar-item">
                <div class="m-icon-dicEmployee"></div>
                <div class="m-nav-item-text">Danh mục khách hàng</div>
            </router-link>
            <router-link to="/employee" style="text-decoration: none;color: black" class="m-navbar-item">
                <div class="m-icon-dicEmployee"></div>
                <div class="m-nav-item-text">Danh mục nhân viên</div>
            </router-link>
            <div class="m-navbar-item">
                <div class="m-icon-setting"></div>
                <div class="m-nav-item-text">Thiết lập hệ thống</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>

@import url('../../style/common/navbar.css');
</style>
