<template lang="pug">
section.future
  scroll-view.sw(tag="div", :offset="0")
    template(slot-scope="futurevisibility")
      .container
        h2.title(v-html="$t('futureTitle')")

        .parts
          .part
            .dot
            .line
            p(v-html="$t('you')")

          .part
            lazy-image(:to="require('../assets/img/future/future-we.png')", :visible="futurevisibility.we" key="we")
            .line
            p(v-html="$t('we')")

          .part
            lazy-image.building(:to="require('../assets/img/future/future-building.png')", :visible="futurevisibility.building" key="building")
            .line
            p(v-html="$t('future')")

        div.world
          lazy-image.future-world(:to="require('../assets/img/future/future-world.png')", :visible="futurevisibility.vw" key="vw")
          h2.title(ref="investors", v-html="investors + ' ' + $t('peopleMultiple')")
          p.subtitle(v-html="$t('alreadyBecome')")
          a.btn-blue.btn-grd(:href="ref", v-html="$t('btnBeFuture')")
</template>

<script>
import LazyImage from './LazyImage'

export default {
  components: {
    LazyImage
  },
  data() {
    return {
      login: '',
      investors: '917',
      showInvestors: false,
      loadedInvestors: false,
      ref: 'https://cabinet.les.denistiaglin.com/auth'
    }
  },
  methods: {
    getInvestors() {
      fetch(window.origin + '/meta')
        .then(res => res.json())
        .then(res => {
          console.log(res)
          this.investors = res.user
          localStorage.setItem("investors", res.user)
        }).catch(e => {
          this.investors = localStorage.getItem("investors") || 917
        })
    }
  },
  mounted() {
    this.login = this.$cookies.get('weter_ref')
    if (this.login) this.ref += `?u=${this.login}`
    const evl = window.addEventListener('scroll', _ => {
        const top = this.$refs.investors.getBoundingClientRect().top;
        this.showInvestors = top - 500 < window.innerHeight;
        if (this.showInvestors && !this.loadedInvestors) {
          this.getInvestors()
          this.loadedInvestors = true
        }
    })
  }
}
</script>

<style lang="scss" scoped>
.sw {
  width: 100%;
}
</style>
