<template>
    <div class="home">
        <div class="main-title">
            Learn German
        </div>
        <div class="footer">
            Made with ❤️ by Nathan Seymour
        </div>
    </div>
</template>

<script>
    export default {
        name: 'home',
        components: {
        }
    }
</script>

<style lang="scss" scoped>
    .home {
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;;

        .main-title {
            font-size: $fsz-main-title;
        }

        .footer {
            margin-top: 1em;
        }
    }
</style>