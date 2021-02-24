<template lang="pug">

    .watcher-block(@click="changeIdx" :key="index+'cw'" )
      //фэйковые наблюдатели
      .watcher-img-wrapper(v-if="item.default")
        img.watcher-preview-img(:src="`/files/committee-img/${item.img}.svg`" alt="item.img")
      //настоящие наблюдателм
      .watcher-img-wrapper(v-else)
        img.watcher-preview-img(:src="`/files/committee-img/${item.img}.jpg`" alt="item.img")
        svg-round-icon.flag(v-if="item.country" :name='item.country' :id="index+'cw'" width="25" height="25" circle-color="21202F")

      .watcher-info
        p.watcher-title(v-html="item.name")

</template>

<script>
import SvgRoundIcon from './SvgRoundIcon';

export default {
  name: "WhatcherCard",
  components: {
    SvgRoundIcon
  },
  props: ["item", "index", "number"],
  methods: {
    changeIdx() {
      this.$emit('change-idx', {index: this.index, number: this.number});
    }
  },
}
</script>

<style scoped lang="scss">
.watcher-block {
  margin-bottom: 8px;
  width: 135px;
  height: 135px;
  border-radius: 5px;
  background: rgba(46, 48, 63, 0.3);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  transition: background-color 50ms ease-in-out;
  cursor: pointer;

  .watcher-img-wrapper {
    width: 79px;
    height: 79px;
    margin: 5px auto;
    position: relative;

    .watcher-preview-img {
      border-radius: 50%;
      display: block;
      margin: 0 auto;
      height: 100%;
      width: 100%;
      z-index: 10;
      object-fit: cover;
    }

    .flag {
      position: absolute;
      right: -10px;
      bottom: 0;
    }
  }

  .watcher-info {
    display: flex;
    flex-direction: column;
    align-items: center;

    p {
      max-width: 80%;
    }

    .watcher-title {
      font-weight: bold;
      font-size: 15px;
      line-height: 18px;
      letter-spacing: -0.05em;
      margin-bottom: 10px;
      text-align: center;
    }

    .watcher-crop-desc {
      text-align: center;
      font-weight: 300;
      font-size: 13px;
      line-height: 16px;
      letter-spacing: -0.05em;
      color: #C7CBDE;
      margin: 5px 0 27px 0;
    }

    .watcher-link {
      font-weight: 300;
      font-size: 15px;
      line-height: 18px;
      letter-spacing: -0.05em;
      color: #347DFE;
    }

    .news-full-desc {
      display: none;
    }
  }
}

.watcher-block:hover {
  background-color: #2f303f;
}

</style>
