<template lang="pug">
    modal(v-if="show" @close="show=false; $emit('close')", :st="{width:'100%', height:'750px', maxHeight: 'unset', background:'unset'}")
      youtube(:video-id="videoId" ref="youtube", :player-vars="playerVars" width="100%" height="650px")
</template>

<script>
import Modal from './Modal'

export default {
    props: [
        'videoId'
    ],
    components: {
        Modal
    },
    data() {
        return {
            playerVars: {
                autoplay: 1
            },
            show: true
        }
    },
    mounted() {
        this.$refs.youtube.player.playVideo()
    }
}
</script>>