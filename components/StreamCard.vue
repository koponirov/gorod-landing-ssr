<template lang="pug">
  div.stream-item-content
    div.preview-item(@click="changeStreamId")

      img.preview-item(v-if="item.img" :src="itemImage" )

      button.play-video-btn
        svg-icon(name="play")
    h4(v-html="$t(`${ item.name }`)")
    p(v-html="$t(`${ item.address }`)")
</template>

<script>
import SvgIcon from "@/components/SvgIcon";
export default {
  name: "StreamCard",
  components: {
    SvgIcon
  },
  props: ["item", "index"],
  methods: {
    changeStreamId() {
      this.$emit('change-stream-id',
          {
            id: this.item.id,
            index: this.index
          });
    },
  },
  computed: {
    itemImage() {
      if (!this.item) {
        return
      }
      const fileName = this.item.img;
      return require(`../assets/img/stream-group/${fileName}.jpg`);
    }
  },

}
</script>

<style scoped lang="scss">

.is-current {
  display: none;
}
.stream-item-content {
  cursor: pointer;
}

.play-video-btn {
  display: block;
  padding: 0;
  background: #25417c;
  border: 1px solid #347dfe;
  border-radius: 50%;
  cursor: pointer;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 10;
  width: 46px;
  height: 46px;
  outline: 0;
  opacity: 0.9;
  color: #fff;
  &:before {
    content: "";
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: none;
    width: calc(100% - 10px);
    height: calc(100% - 10px);
    background: #347dfe;
    border-radius: 50%;
    z-index: -1;
  }
  &:hover:before {
    display: block;
  }
  .svg-icon {
    position: absolute;
    top: 25%;
    left: 18%;
  }
}

.stream-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 1140px;
  margin-bottom: 30px;
  .fake-stream {
    background-color: #000;
    width: 1140px;
    height: 641px;
    margin-bottom: 5px;
  }
}
h4 {
  font-weight: bold;
  font-size: 20px;
  line-height: 24px;
  letter-spacing: -0.05em;
  align-self: flex-start;
}
p {
  font-size: 15px;
  line-height: 18px;
  letter-spacing: -0.05em;
  color: #9E9BAD;
  align-self: flex-start;
}
.stream-item {
  cursor: pointer;
}

    .stream-item-content {
      width: 385px;
      .preview-item {
        width: 93%;
        height: 170px;
        background-color: #000000;
        border: 1px solid #2e355e;
        position: relative;
        img {
          object-fit: cover;
          width: 100%;
          height: 100%;
        }
      }
      p {
        width: 65%;
      }
    }

</style>
