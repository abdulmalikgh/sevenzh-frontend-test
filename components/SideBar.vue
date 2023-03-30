
<template>
  <div
    class="side-bar"
  >
  <div>
  <b-nav vertical>
    <b-nav-item class="side-bar-active px-4 py-2">
        <div class="d-flex">
            <img src="../static/icons/Group 1432.svg" alt="">
            <span class="side-bar-nav-text pl-4">Dashboard</span>
        </div>
    </b-nav-item>
    <b-nav-item class="px-4 py-2">
        <div class="d-flex">
            <img src="../static/icons/Vector (7).svg" alt="">
            <span class="side-bar-nav-text pl-4">Profile</span>
        </div>
    </b-nav-item>
    <b-nav-item class="px-4 py-2">
        <div class="d-flex justify-content-between">
            <div class="d-flex align-item-center">
                <img src="../static/icons/Vector 7.svg" alt="">
                <span class="side-bar-nav-text pl-4">Services</span>
            </div>
            <img style="float: right;" src="../static/icons/arrow down.svg" alt="">
        </div>
    </b-nav-item>
    <b-nav-item class="px-4 py-2">
        <div class="d-flex">
            <img src="../static/icons/Vector (6).svg" alt="">
            <span class="side-bar-nav-text pl-4">Medical Records</span>
        </div>
    </b-nav-item>
    <b-nav-item class="px-4 py-2">
        <div class="d-flex">
            <img src="../static/icons/Vector (5).svg" alt="">
            <span class="side-bar-nav-text pl-4">Care Wallet</span>
        </div>
    </b-nav-item>
    <b-nav-item class="px-4 py-2">
        <div class="d-flex">
            <img src="../static/icons/Vector (4).svg" alt="">
            <span class="side-bar-nav-text pl-4">Messages</span>
        </div>
    </b-nav-item>
    <b-nav-item class="px-4 py-2">
        <div class="d-flex">
            <img src="../static/icons/Vector (3).svg" alt="">
            <span class="side-bar-nav-text pl-4">Resources</span>
        </div>
    </b-nav-item>
    <b-dropdown-divider></b-dropdown-divider>
    <b-nav-item class="px-4 py-2">
        <div class="d-flex">
            <img src="../static/icons/Vector (2).svg" alt="">
            <span class="side-bar-nav-text pl-4">Account Settings</span>
        </div>
    </b-nav-item>
    <b-nav-item class="px-4 py-2">
        <div class="d-flex">
            <img src="../static/icons/Vector (1).svg" alt="">
            <span class="side-bar-nav-text pl-4">Contact Support</span>
        </div>
    </b-nav-item>
    <b-nav-item class="px-4 py-2">
        <div class="d-flex">
            <img src="../static/icons/Vector.svg" alt="">
            <span class="side-bar-nav-text pl-4">Logout</span>
        </div>
    </b-nav-item>
  </b-nav>
</div>
  </div>
</template>

<script>
export default {
  name: 'SideBar',
}
</script>