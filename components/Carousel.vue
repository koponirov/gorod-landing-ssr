<template lang="pug">
  div(:ref="`${name}-wrapper`" class="streams")

    Hooper(
      :ref="name"
      :itemsToShow="itemsToShow"
      :infiniteScroll="infiniteScroll"
      :initialSlide="initialSlide"
      :wheelControl="wheelControl"
      :trimWhiteSpace="true"
      :style="`height: ${h}; min-width: ${w};`"
      :class="{ right: rshow, left: lshow }"
      @slide="slide"
    )
      Slide(v-for="(item, index) in items", :key="index", :index="index")

        slot(:item="item"  :index="index")
        slot(name="watchers" :item="item"  :index="index")

    .slider-controls(v-if="items && items.length > 0")
      button.slick-prev(@click.prevent="slidePrev" :style="{opacity: lshow ? 1:0}")
      button.slick-next(@click.prevent="slideNext" :style="{opacity: rshow ? 1:0}")

</template>

<script>
import { Hooper, Slide } from "hooper";
import "hooper/dist/hooper.css";

export default {
  name: 'carousel',
  components: {
    Hooper,
    Slide,
  },
  data() {
      return {
        slideChanged: false,
        rshow: true,
        lshow: true,
      }
  },
  props: {
    name: String,
    items: Array,
    itemsToShow: Number,
    infiniteScroll: Boolean,
    initialSlide: Number,
    wheelControl: Boolean,
    h: String,
    w: String,
    loaded: Boolean
  },
  watch: {
    initialSlide() {
      this.$refs[this.name].slideTo(this.initialSlide);
    },
    slideChanged() {
      this.showArrows()
    }
  },

  methods: {
    slidePrev() {
      this.$refs[this.name].slidePrev();
    },
    slideNext() {
      this.$refs[this.name].slideNext();
    },
    showArrows() {
      const hooper = this.$refs[this.name].$el

      this.rshow = hooper.getElementsByClassName('is-next').length > 0;
      this.lshow = hooper.getElementsByClassName('is-prev').length > 0;
    },
    slide() {
      this.slideChanged = true
      setTimeout(() => {
        this.slideChanged = false
      }, 0)
    }
  },

  mounted() {

    this.$refs[`${this.name}-wrapper`].addEventListener("touchstart", (event) => {
      document.body.style.overflow = "hidden";
    });
    this.$refs[`${this.name}-wrapper`].addEventListener("touchend", (event) => {
      document.body.style.overflow = "auto";
    });
    this.showArrows()
  },
  updated() {
    this.showArrows()
  }
};
</script>
<style lang="scss" scoped>

.streams {
  position: relative;

}
.hooper {
  min-width: 1140px;
}

.slider-controls {
  position: absolute;
  width: 100%;
  pointer-events: none;

  button {
    pointer-events: auto;
  }
}

.right {
  &::after {
    content: '';
    right: 0;
    background: linear-gradient(to left, #1B1A28, #1B1A28 13px, rgba(27, 26, 40, 0));
    position: absolute;
    width: 35px;
    height: 100%;
    top: 50%;
    z-index: 0;
    transform: translateY(-50%);
    //display: contents;
  }
}

.left {

  &::before {
    content: '';
    left: 0;
    background: linear-gradient(to right, #1B1A28, #1B1A28 13px, rgba(27, 26, 40, 0));
    position: absolute;
    width: 22px;
    height: 100%;
    top: 50%;
    z-index: 0;
    transform: translateY(-50%);
    //display: contents;
  }
}
</style>
