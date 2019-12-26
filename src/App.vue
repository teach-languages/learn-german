<template>
    <div id="app">
        <router-view class="router"/>
        <SideMenu />
    </div>
</template>

<script>
    import SideMenu from '@/components/SideMenu.vue';

    export default {
        components: { SideMenu }
    };
</script>

<style lang="scss">
    html, body, #app {
        width: 100%;
        height: 100%;
        overflow: hidden;
    }

    #app {
        display: flex;
        flex-direction: row;

        .router {
            width: 100%;
            height: 100%;
            overflow: hidden;
        }
    }

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: $font-base;
        transition: 100ms;
        -webkit-tap-highlight-color: transparent;
    }
</style>
