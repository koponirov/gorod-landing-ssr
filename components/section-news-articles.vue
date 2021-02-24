<template lang="pug">
.news-articles(ref="a")
  carousel(
    name="articles"
    :items-to-show="4"
    :initial-slide="0"
    :infinite-scroll="true"
    :loaded="loaded"
    :wheel-control="false"
    h="420px"
    :items="items"
  )
    template(slot-scope="{item , index}")
      card(:item="item" :index="index" :idx="idx" @change-idx="changeIdxParent" )


  modal.news-modal-overlay(
    v-if="idx >= 0",
    @close="idx = -1",
    :st="{ width: '800px', background: '#2e303f' }"
  )
    .news-modal-inner
      .news-main-banner

        picture
          source(:srcset="items[idx].img + '.webp'" type="image/webp" media="(min-width: 1280px)")
          source(:srcset="items[idx].img + '.jpg'" media="(min-width: 1280px)")
          source(:srcset="items[idx].img + '_992.webp'" type="image/webp" media="(min-width: 992px)")
          source(:srcset="items[idx].img + '_992.jpg'" media="(min-width: 992px)")
          source(:srcset="items[idx].img + '_766.webp'" type="image/webp" media="(min-width: 766px)")
          source(:srcset="items[idx].img + '_766.jpg'" media="(min-width: 766px)")
          source(:srcset="items[idx].img + '_576.webp'" type="image/webp" media="(min-width: 576px)")
          source(:srcset="items[idx].img + '_576.jpg'" media="(min-width: 576px)")
          img.orig(:src="items[idx].img + '.jpg'" alt="news-main-img")

        picture
          source(:srcset="items[idx].img + '.webp'" type="image/webp" media="(min-width: 1280px)")
          source(:srcset="items[idx].img + '.jpg'" media="(min-width: 1280px)")
          source(:srcset="items[idx].img + '_992.webp'" type="image/webp" media="(min-width: 992px)")
          source(:srcset="items[idx].img + '_992.jpg'" media="(min-width: 992px)")
          source(:srcset="items[idx].img + '_766.webp'" type="image/webp" media="(min-width: 766px)")
          source(:srcset="items[idx].img + '_766.jpg'" media="(min-width: 766px)")
          source(:srcset="items[idx].img + '_576.webp'" type="image/webp" media="(min-width: 576px)")
          source(:srcset="items[idx].img + '_576.jpg'" media="(min-width: 576px)")
          img.fake(:src="items[idx].img + '.jpg'" alt="news-main-img" )


      h3.news-modal-title {{ items[idx].title }}
      p.news-modal-date {{ items[idx].date }}
      p.news-modal-desc(v-html="items[idx].description")

      .news-main-banner(v-if="items[idx].img_collection")

        picture
          source(:srcset="items[idx].img_collection[imgCollectionIndex] + '.webp'" type="image/webp" media="(min-width: 1280px)")
          source(:srcset="items[idx].img_collection[imgCollectionIndex] + '.jpg'" media="(min-width: 1280px)")
          source(:srcset="items[idx].img_collection[imgCollectionIndex] + '_992.webp'" type="image/webp" media="(min-width: 992px)")
          source(:srcset="items[idx].img_collection[imgCollectionIndex] + '_992.jpg'" media="(min-width: 992px)")
          source(:srcset="items[idx].img_collection[imgCollectionIndex] + '_766.webp'" type="image/webp" media="(min-width: 766px)")
          source(:srcset="items[idx].img_collection[imgCollectionIndex] + '_766.jpg'" media="(min-width: 766px)")
          source(:srcset="items[idx].img_collection[imgCollectionIndex] + '_576.webp'" type="image/webp" media="(min-width: 576px)")
          source(:srcset="items[idx].img_collection[imgCollectionIndex] + '_576.jpg'" media="(min-width: 576px)")
          img.orig(:src="items[idx].img_collection[imgCollectionIndex] + '.jpg'" )

      div.img-container(
        v-if="items[idx].img_collection && items[idx].img_collection_preview"
      )
        div.img-item(
          v-for="(image, i) in items[idx].img_collection_preview",
          @click="setCollectionIndex(i)"
        )

          picture
            source(:srcset="image + '.webp'" type="image/webp" media="(min-width: 1280px)")
            source(:srcset="image + '.jpg'" media="(min-width: 1280px)")
            source(:srcset="image + '_992.webp'" type="image/webp" media="(min-width: 992px)")
            source(:srcset="image + '_992.jpg'" media="(min-width: 992px)")
            source(:srcset="image + '_766.webp'" type="image/webp" media="(min-width: 766px)")
            source(:srcset="image + '_766.jpg'" media="(min-width: 766px)")
            source(:srcset="image + '_576.webp'" type="image/webp" media="(min-width: 576px)")
            source(:srcset="image + '_576.jpg'" media="(min-width: 576px)")
            img( v-if="image", :src="image + '.jpg'", alt="news post image" )

</template>

<script>

import Modal from "./Modal";
import Carousel from "./Carousel"
import Card from "./NewsCard"
export default {
  components: {
    Carousel,
    Modal,
    Card
  },
  data() {
    return {
      items: [],
      count: 0,
      loaded: false,
      show: false,
      idx: -1,
      locale: this.$i18n.locale,
      rshow: true,
      lshow: true,
      imgCollectionIndex: 0,
    };
  },
  watch: {
    idx: function (newIdx, oldIdx) {
      debugger;
      if (newIdx < 0) {
        this.imgCollectionIndex = 0;
      }
    },
  },

  methods: {
    getArticles() {
      fetch(`/files/articles/${this.$i18n.locale}.json`)
        .then((res) => res.text())
        .then((res) => {
          debugger
          this.items = JSON.parse(res.replace(/\n/g, "")).items;
          this.count = Math.round(this.$refs.a.clientWidth / 284);
        });
    },

    setCollectionIndex(i) {
      this.imgCollectionIndex = i;
    },
    changeIdxParent(idx) {
      this.idx = idx
    }
  },

  mounted() {
    const top = this.$refs.a.getBoundingClientRect().top;
    this.show = top < window.innerHeight;
    const evl = window.addEventListener("scroll", (_) => {
      const top = this.$refs.a.getBoundingClientRect().top;
      this.show = top < window.innerHeight;
      if (this.show && (!this.loaded || this.locale !== this.$i18n.locale)) {
        this.getArticles();
        this.loaded = true;
        this.locale = this.$i18n.locale;
      }
    });
    //
    // const app = document.getElementById("app");
    //
    // this.$refs.a.addEventListener("touchstart", (event) => {
    //
    //   document.body.style.overflow = "hidden";
    // });
    // this.$refs.a.addEventListener("touchend", (event) => {
    //
    //   document.body.style.overflow = "auto";
    // });
  },
};
</script>
