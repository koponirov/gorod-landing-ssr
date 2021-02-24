<template lang="pug">
  div.watchers(ref="a")
    carousel(
      name="watchers"
      :items-to-show="8"
      :initial-slide="0"
      :infinite-scroll="false"
      :loaded="loaded"
      :wheel-control="false"
      h="720px"
      w="1140px"
      :items="items"
    )
      template(v-slot:watchers="{item , index}")
        card(v-for="(watcher, n) in item" :item="watcher" :index="index" :number="n" :key="n+'w'"  @change-idx="changeIdxParent")

    // Модальное окно
    modal-card(:items="items" :idx="idx" :number="number" @close-modal="closeModal")

</template>

<script>
import ModalCard from "./WatcherModalCard";
import Carousel from './Carousel';
import Card from './WhatcherCard'
import { Hooper, Slide } from "hooper";
import "hooper/dist/hooper.css";


export default {
  components: {
    ModalCard,
    Carousel,
    Card,
    Hooper,
    Slide
  },
  data() {
    return {
      items: [],
      loaded: false,
      show: false,
      idx: -1,
      number: null,
      locale: this.$i18n.locale,
      rshow: true,
      lshow: true,
      slideChanged: false
    }
  },
  methods: {
    getTeam() {
      fetch(`/files/committee/${this.$i18n.locale}.json`)
          .then(res => res.text())
          .then(res => {
            let items = JSON.parse(res.replace(/\n/g, '')).items
            let size = 5; //размер подмассива
            let slicedItems = []; //массив в который будет выведен результат.
            for (let i = 0; i < Math.ceil(items.length / size); i++) {
              slicedItems[i] = items.slice((i * size), (i * size) + size);
            }
            this.items = slicedItems
          })
    },
    changeIdxParent( data ) {
      this.idx = data.index
      this.number = data.number
    },
    closeModal( idx ) {
      this.idx = idx
    },
    slide() {
      this.slideChanged = true
      setTimeout(() => {
        this.slideChanged = false
      }, 0)
    }
  },

  mounted() {
    const top = this.$refs.a.getBoundingClientRect().top;
    this.show = top < window.innerHeight;
    const evl = window.addEventListener('scroll', _ => {
      const top = this.$refs.a.getBoundingClientRect().top;
      this.show = top < window.innerHeight;
      if (this.show && (!this.loaded || this.locale !== this.$i18n.locale)) {
        this.getTeam()
        this.loaded = true
        this.locale = this.$i18n.locale
      }
    })
  },
}
</script>
<style lang="scss" scoped>
.watchers {
  position: relative;

  .slider-controls {
    position: absolute;
    margin-top: -385px;
    width: 100%;
    pointer-events: none;

    button {
      pointer-events: auto;
    }
  }
}

.right {
  &::after {
    content: '';
    right: 0;
    background: linear-gradient(to left, #1B1A28, #1B1A28 13px, rgba(27, 26, 40, 0));
    position: absolute;
    width: 35px;
    height: 720px;
    top: 50%;
    z-index: 1;
    transform: translateY(-50%);
  }
}

.left {

  &::before {
    content: '';
    left: 0;
    background: linear-gradient(to right, #1B1A28, #1B1A28 13px, rgba(27, 26, 40, 0));
    position: absolute;
    width: 35px;
    height: 720px;
    top: 50%;
    z-index: 1;
    transform: translateY(-50%);
  }
}

</style>
