<template lang="pug">
  .article-block(@click="changeIdx")
    .img-wrapper

      picture
        source(:srcset="item.img_prev + '.webp'" type="image/webp" media="(min-width: 1280px)")
        source(:srcset="item.img_prev + '.jpg'" media="(min-width: 1280px)")
        source(:srcset="item.img_prev + '_992.webp'" type="image/webp" media="(min-width: 992px)")
        source(:srcset="item.img_prev + '_992.jpg'" media="(min-width: 992px)")
        source(:srcset="item.img_prev+ '_766.webp'" type="image/webp" media="(min-width: 766px)")
        source(:srcset="item.img_prev+ '_766.jpg'" media="(min-width: 766px)")
        source(:srcset="item.img_prev + '_576.webp'" type="image/webp" media="(min-width: 576px)")
        source(:srcset="item.img_prev + '_576.jpg'" media="(min-width: 576px)")
        img.news-preview-img(:src="item.img_prev + '.jpg'" alt="news-main-img")

      picture
        source(:srcset="item.img_prev + '.webp'" type="image/webp" media="(min-width: 1280px)")
        source(:srcset="item.img_prev + '.jpg'" media="(min-width: 1280px)")
        source(:srcset="item.img_prev + '_992.webp'" type="image/webp" media="(min-width: 992px)")
        source(:srcset="item.img_prev + '_992.jpg'" media="(min-width: 992px)")
        source(:srcset="item.img_prev + '_766.webp'" type="image/webp" media="(min-width: 766px)")
        source(:srcset="item.img_prev + '_766.jpg'" media="(min-width: 766px)")
        source(:srcset="item.img_prev + '_576.webp'" type="image/webp" media="(min-width: 576px)")
        source(:srcset="item.img_prev + '_576.jpg'" media="(min-width: 576px)")
        img.news-fake-preview-img(:src="item.img_prev + '.jpg'" alt="news-main-img" )

    .news-info
      h3.news-title(v-html="item.title")
      p.news-date {{ item.date }}
      p.news-crop-desc(v-html="item.crop_description")
      .news-full-desc(v-html="item.description")
</template>

<script>
export default {
  name: "NewsCard",
  props: ["item", "index"],
  methods: {
    changeIdx() {
      this.$emit('change-idx', this.index);
    }
  }
}
</script>

<style scoped lang="scss">
.article-block {
  width: 260px;
  height: 415px;
  margin: 0 15px 0 10px;
  background-color: #2f303f;
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;

  &:hover {
    background-color: #343540;
  }

  + .article-block {
    margin-left: 30px;
  }

  .img-wrapper {
    overflow: hidden;
    position: relative;
    width: 100%;
    height: 150px;

    .news-preview-img {
      height: 150px;
      position: absolute;
      z-index: 10;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    .news-fake-preview-img {
      position: absolute;
      width: 100%;
      filter: blur(10px);
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 5;
    }
  }

  .news-info {
    padding: 15px;

    .news-title {
      font-size: 15px;
      font-weight: 500;
      line-height: 22px;
      margin: 0;
    }

    .news-date {
      color: #8c8f9e;
      font-size: 13px;
      margin: 5px 0;
    }

    .news-crop-desc {
      color: #cbcfe2;
      font-size: 13px;
      margin: 5px 0;
    }

    .news-full-desc {
      display: none;
    }
  }
}
</style>
