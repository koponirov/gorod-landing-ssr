<template lang="pug">
    .StreamInParent(ref="stream")


      iframe( :src="streamSrc" :style="streamStyle" scrolling="no" allowfullscreen="true" allow="autoplay" webkitallowfullscreen="true" mozallowfullscreen="true" id="stream")


</template>

<script>
import SvgIcon from "./SvgIcon";
import ModalStream from "./ModalStream";

export default {

  data() {

    return {


    };
  },
  props: ['streamSrc', 'width', 'height'],
  components: {
    SvgIcon,
    ModalStream,
  },

  computed: {

    streamStyle: function () {
      return `width: ${this.width}px; height: ${this.height + (this.seeAlsoCameraIDList && this.seeAlsoCameraIDList.length ? 200 : 0)}px; border: 0px;`
    }
  },
  mounted() {
    // console.log(this.$refs.stream.frames)
    // const stream = document.getElementById('stream')
    // const streamDoc= stream.contentWindow.document
    // console.log(streamDoc)
    // streamDoc.


  },


};
</script>

<style lang="scss">

    .StreamInParent {
        // display: flex;
        position: relative;
        width: 1140px;
        // min-height: 400px;
        // align-content: center;
        // justify-content: center;
        z-index: 500;
      .stream-unavalible {
        background-color: #1b1b29;
      }
    }
</style>
