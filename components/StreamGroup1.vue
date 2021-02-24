<template lang="pug">
  div.group-container

    div.stream-wrapper(v-if="showStream")

      Stream(:streamSrc="streamPath" :width="width" :height="height")
      h4(v-html="$t(`${streamTitle}`)")
      p(v-html="$t(`${streamAddress}`)")

    div.stream-wrapper(v-else)
      div.fake-stream
      h4(v-html="$t(`${streamTitle}`)")
      p(v-html="$t(`${streamAddress}`)")

    carousel(
      v-if="items&&items.length > 0"
      name="stream"
      :items-to-show="2.65"
      :infinite-scroll="true"
      :initialSlide="initialSlide"
      :wheel-control="false"
      h="300px"
      w="1140px"
      :items="items"
    )
      template(slot-scope=" {item , index}")
        card(:item="item" :index="index" :id="id" @change-stream-id="changeId" )

</template>

<script>
import Stream from './Stream'
import SvgIcon from './SvgIcon';
import Carousel from './Carousel'
import Card from './StreamCard'

export default {

  components: {
    Carousel,
    Stream,
    SvgIcon,
    Card
  },
  data() {

    return {
      items: [],
      id: 3945,
      initialSlide: 1,
      width: 1140,
      height: 641,
      html5: true,
      logo: "",
      seeAlsoCameraIDList: [],
      streamTitle: 'streamTitle2',
      streamAddress: 'streamAddress2'
    }
  },
  computed: {
    streamPath: function () {

      //добавить вконце строки src для автовоспроизведения
      //&autostart=true

      return `https://cam.mega-com.ru/site/embed.html?id=${this.id}&html5=${this.html5}&logo=${this.logo}'&w=${this.width}&h=${this.height}&ids=${this.seeAlsoCameraIDList && this.seeAlsoCameraIDList.length ? JSON.stringify(this.seeAlsoCameraIDList) : ''}&autostart=true  `
    },
    showStream: function () {
      return Number(this.id) !== 0;
    }
  },
  methods: {
    getStreams() {
      fetch(`/files/streams/streams.json`)
          .then(res => res.text())
          .then(res => {
            this.items = JSON.parse(res.replace(/\n/g, '')).items
          })
    },
    changeId(data) {
      this.id = data.id
      this.initialSlide = data.index
    }
  },

  mounted() {
    //this.getStreams()
  }

}
</script>
<style scoped lang="scss">

.is-current {
  display: none;
}

.hooper {
  width: 1140px;
  min-width: 1140px;
  height: 800px;
  position: relative;
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

.stream-collection {
  height: 350px;

  .stream-item {
    cursor: pointer;
  }
}

</style>
