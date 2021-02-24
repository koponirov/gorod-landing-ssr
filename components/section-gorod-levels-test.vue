<template lang="pug">
section.section-top
  .container
    .gorod-wrapper
      .about
        h1(v-html="$t('gorodTitle')")
        p(v-html="$t('gorodDescription')")
        .btns-block-wrapper
          form.btns-block
            label.btn.btn-level-1(
              @mouseenter="changeLevel('level1')",
              @mouseleave="setDefault"
            )
              input#level1.img.img-level-1(
                type="checkbox",
                name="level",
                data-value="level1",
                @click="handleRadioClick",
                ref="level1"
              )
              .level-text(v-html="$t('level1')")
            label.btn.btn-level-2(
              @mouseenter="changeLevel('level2')",
              @mouseleave="setDefault"
            )
              input#level2.img.img-level-2(
                type="checkbox",
                name="level",
                data-value="level2",
                @click="handleRadioClick",
                ref="level2"
              )
              .level-text(v-html="$t('level2')")
            label.btn.btn-level-3(
              @mouseenter="changeLevel('level3')",
              @mouseleave="setDefault"
            )
              input#level3.img.img-level-3(
                type="checkbox",
                name="level",
                data-value="level3",
                @click="handleRadioClick",
                ref="level3"
              )
              .level-text(v-html="$t('level3')")
            label.btn.btn-level-4(
              @mouseover="changeLevel('level4')",
              @mouseleave="setDefault"
            )
              input#level4.img.img-level-4(
                type="checkbox",
                name="level",
                data-value="level4",
                @click="handleRadioClick",
                ref="level4"
              )
              .level-text(v-html="$t('level4')")

      .levels
        transition(name="fade", mode="out-in")
          component(:is="component")
    .container
      .download-wrapper
        p.download-text(v-html="$t('invention')")
        .download-button
          a.download(href="./files/submission.jpg", download)
            .icon
              .icon-dw

            .dw-btn-text-wrapper
              .dw-btn-text1 45 Mb
              .dw-btn-text2(v-html="$t('download')")
</template>

<script>
import Level0 from "./levels/level0";
import Level1 from "./levels/level1";
import Level2 from "./levels/level2";
import Level3 from "./levels/level3";
import Level4 from "./levels/level4";

export default {
  components: {
    Level0,
    Level1,
    Level2,
    Level3,
    Level4,
  },
  data: function () {
    return {
      component: "Level0",
      defaultLevel: "level0",
      levelImg1: "",
    };
  },
  methods: {
    changeLevel: function (level) {
      this.component = level;
    },

    handleRadioClick: function (event) {
      const currentValue = event.target.checked;
      const name = event.target.dataset.value;

      if (!currentValue) {
        this.resetAllRadio();
        this.changeDefaultLevel("level0");
        // Focus state seems like clicked, so we have to drop focus
        this.$refs[name].blur();
        return;
      } 

      if(currentValue){
        this.resetAllRadio();
        this.$refs[name].checked = true;
        this.changeDefaultLevel(name);
        return
      }
    },

    resetAllRadio: function () {
      this.$refs.level1.checked = false;
      this.$refs.level2.checked = false;
      this.$refs.level3.checked = false;
      this.$refs.level4.checked = false;
    },

    setDefault: function (event) {
      this.component = this.defaultLevel;
    },

    changeDefaultLevel: function (level) {
      this.defaultLevel = level;
    },
  },
  computed: {
    imageSource: function () {
      return require("@/assets/icons/download.svg");
    },
  },
};
</script>

<style lang="scss" scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 150ms;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.section-top {
  position: relative;
  max-width: 100%;
  margin: 0;
}
.gorod-container {
  margin-top: 100px;
  width: 100%;
  height: 800px;
}
.gorod-wrapper {
  display: flex;
  height: 574px;
  margin-top: 100px;
}
.about {
  display: flex;
  flex-direction: column;

  h1 {
    margin-top: 127px;
  }
  p {
    margin-top: 93px;
    font-style: normal;
    font-weight: 500;
    font-size: 15px;
    line-height: 18px;
  }
}
.btns-block-wrapper {
  position: relative;
  margin-top: 35px;
}
.btns-block {
  display: flex;
  flex-direction: column;
  position: relative;

  .btn {
    display: flex;
    align-items: center;
    position: absolute;

    input[type="checkbox"] {
      position: absolute;
      z-index: -1;
      opacity: 0;
      vertical-align: top;
      width: 400px;

      & + .level-text {
        cursor: pointer;
        padding-left: 120px;
        transition: all 0.2s;
        font-weight: normal;
        //text-decoration: underline;
      }

      @mixin hexagon-before($url) {
        content: "";
        position: absolute;
        top: -10px;
        left: 0;
        width: 100px;
        height: 40px;
        background: url($url) no-repeat;
        filter: drop-shadow(0.35rem 0.35rem 0.4rem rgba(0, 0, 0, 0.5));
        transition: 0.2s;
        cursor: pointer;
      }

      &#level1 + .level-text:before {
        @include hexagon-before("../assets/img/gorod-levels/btn-level-1.svg");
      }

      &#level2 + .level-text:before {
        @include hexagon-before("../assets/img/gorod-levels/btn-level-2.svg");
      }

      &#level3 + .level-text:before {
        @include hexagon-before("../assets/img/gorod-levels/btn-level-3.svg");
      }

      &#level4 + .level-text:before {
        @include hexagon-before("../assets/img/gorod-levels/btn-level-4.svg");
      }

      // Styles for image with hexagon while input is active
      &:focus + .level-text:before,
      &:hover + .level-text:before,
      &:checked + .level-text:before {
        transform: scale(1.2);
      }

      // Styles for tooltip while input is active
      &:focus + .level-text,
      &:hover + .level-text,
      &:checked + .level-text {
        margin-left: 20px;
        transition: all 0.2s;
      }
    }

    // Animation to attract the user's attention (now doesnt work)
    $animation-time: 0.8s;
    $delay-gap: 0.2s;
    $animation-count: 1;
    .animation-1 {
      animation: jump $animation-time $animation-count;
    }
    .animation-2 {
      animation: jump $animation-time $delay-gap $animation-count;
    }
    .animation-3 {
      animation: jump $animation-time $delay-gap * 2 $animation-count;
    }
    .animation-4 {
      animation: jump $animation-time $delay-gap * 3 $animation-count;
    }
  }

  .btn-level-1 {
    top: 0;
    z-index: 5;
  }
  .btn-level-2 {
    top: 30px;
    z-index: 4;
  }
  .btn-level-3 {
    top: 60px;
    z-index: 3;
  }
  .btn-level-4 {
    top: 90px;
    z-index: 2;
  }
}

.levels {
  min-width: 705px;
  transition: all 0.3s;
  .level-main {
    height: 100%;
    position: relative;
    img {
      position: absolute;
      left: 0;
      bottom: -47px;
    }
  }
}

.download-wrapper {
  margin-top: 135px;
  display: flex;
  justify-content: space-between;

  .download-button {
    display: flex;
    background-color: #253866;
    border-radius: 5px;
    width: 231.88px;
    height: 68.2px;
  }

  .download {
    display: flex;
    align-items: center;
  }

  .download-text {
    //margin-left: 50px;
    max-width: 610px;
    font-style: normal;
    font-weight: 500;
    font-size: 15px;
    line-height: 18px;
  }

  .icon {
    display: flex;
    align-items: center;
    margin: 0 10px;
  }
  .icon-dw {
    width: 40px;
    height: 32px;
    background: url("../assets/img/gorod-levels/download.svg") no-repeat center;
  }
  .dw-btn-text-wrapper {
    display: flex;
    flex-direction: column;
    align-items: flex-start;

    .dw-btn-text1 {
      font-style: normal;
      font-weight: normal;
      font-size: 15px;
      line-height: 18px;
    }

    .dw-btn-text2 {
      text-decoration: underline;
      font-style: normal;
      font-weight: normal;
      font-size: 15px;
      line-height: 18px;
    }
  }

  @keyframes jump {
    0% {
      transform: translateX(0);
    }
    50% {
      transform: scale(1.2);
    }
    100% {
      transform: translateX(0);
    }
  }
}
</style>