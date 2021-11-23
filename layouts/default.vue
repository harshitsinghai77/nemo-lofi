<template>
    <Nuxt />
</template>

<script>
import { events } from "@/plugins/bus";
export default {
    mounted() {
        this.initKeyUpListener();
    },
    methods: {
        initKeyUpListener() {
            document.addEventListener("keydown", (e) => {
                const { key, code } = e;
                if (key === "f") {
                    this.toggleFullscreen();
                } else if (key === "ArrowUp" || key === "ArrowDown") {
                    this.handlePlayerVolume(key);
                } else if (key === "ArrowLeft" || key === "ArrowRight") {
                    this.handleActiveMusic(key);
                } else if (code === "Space") {
                    events.$emit("toggle-player");
                } else if ((key === "T" || key === "t") && e.altKey) {
                    events.$emit("show-playlist");
                } else if ((key === "M" || key === "m") && e.altKey) {
                    events.$emit("show-moods");
                } 
            });
        },
        toggleFullscreen() {
            const element = document.body;

            const isFullscreen = document.webkitIsFullScreen || document.mozFullScreen || false;

            element.requestFullScreen =
                element.requestFullScreen ||
                element.webkitRequestFullScreen ||
                element.mozRequestFullScreen ||
                function () {
                    return false;
                };
            document.cancelFullScreen =
                document.cancelFullScreen ||
                document.webkitCancelFullScreen ||
                document.mozCancelFullScreen ||
                function () {
                    return false;
                };

            isFullscreen ? document.cancelFullScreen() : element.requestFullScreen();
        },
        handlePlayerVolume(key) {
            if (key === "ArrowUp") {
                events.$emit("volume-up");
            } else {
                events.$emit("volume-down");
            }
        },
        handleActiveMusic(key) {
            if (key === "ArrowLeft") {
                events.$emit("seek-backward");
            } else {
                events.$emit("seek-forward");
            }
        },
    },
};
</script>
