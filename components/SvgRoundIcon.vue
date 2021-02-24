<template>
  <svg  :width="width" :height="height">
    <defs>
      <clipPath :id="id">
        <circle :cx="width/2" :cy="height/2" :r="width/2.777" fill="#FFFFFF"></circle>
      </clipPath>
    </defs>
    <circle :cx="width/2" :cy="height/2" :r="width/2" :fill="`#${circleColor}`"></circle>
    <image :xlink:href="iconPath" width="100%" height="100%" :clip-path="`url(#${id})`"></image>
  </svg>
</template>

<script>
export default {
  name: 'svg-icon',

  props: {
    name: {
      type: String,
      required: true
    },

    width: {
      type: String,
    },
    height: {
      type: String,
    },
    id: {
      type: String,
    },
    circleColor: {
      type: String,
    }


  },

  computed: {
    iconPath() {
      let icon
      icon = require(`@/assets/icons/flags/${this.name}.svg`);

      if (Object.prototype.hasOwnProperty.call(icon, 'default')) {
        icon = icon.default;
      }
      return icon.url;
    },

    className() {
      return 'svg-icon svg-icon--' + this.name;
    }
  }
};
</script>

<style>
  .svg-icon {
    /* fill: currentColor; */
    height: 24px;
    width: 24px;
  }
</style>
