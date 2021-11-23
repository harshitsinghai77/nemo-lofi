<template>
    <div class="main_layout">
        <player-title />
        <player />
        <slider />
        <noise />
        <navbar />
    </div>
</template>

<script>
import title from "@/components/title.vue";
import player from "@/components/player/player.vue";
import slider from "@/components/slider.vue";
import noise from "@/components/noise.vue";
import navbar from "@/components/sidemenu.vue";
export default {
    components: {
        playerTitle: title,
        player,
        slider,
        noise,
        navbar
    },

    created() {
        import("@/data/streams.json").then((module) => {
            this.$store.commit("player/SET_PAYLIST", module.default);
        });
    },
};
</script>

<style lang="scss" scoped>
.main_layout {
    text-align: center;
    @include query_IPad() {
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
}
</style>
