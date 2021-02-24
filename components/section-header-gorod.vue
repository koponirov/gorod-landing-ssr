<template lang="pug">
    header.section-header
        .container
            .logo-wrapper
                a(href='https://denistiaglin.com/')
                    svg-icon.back(name='back')
                .logo-gorod
                    img(src='~assets/img/header/gorod-logo.png' alt="logo-gorod")

                .text
                  span.logo-title GOROD
                  span.logo-subtitle Logistic Eco System

            .header-nav
                //lang-switcher
                nav.nav
                    a.link(href='https://denistiaglin.com/') {{ $t('main') }}
                    a.btn-blue(href="https://cabinet.les.denistiaglin.com/sign-in") {{ $t('login') }}
                    a.btn-blue(:href="ref") {{ $t('reg') }}
</template>

<script>
import LangSwitcher from './LangSwitcher'
import SvgIcon from './SvgIcon'

export default {
    components: {
        SvgIcon,
        LangSwitcher
    },
    props: [
        'redirect'
    ],
    // data() {
    //     return {
    //         v: false,
    //         login: '',
    //         ref: 'https://cabinet.les.denistiaglin.com/auth?redirect=signup'
    //     }
    // },
    methods: {
        // markerVisible(name) {
        //     this.v=true
        // },
        // markerNotVisible(name) {
        //     this.v=false
        // }
    },
    mounted() {
      //   this.login = this.$cookies.get('weter_ref')
      //   if (this.login) this.ref += `&u=${this.login}`
      // console.log(this.$cookies.get('gorod_ref'))
    }
}
</script>

<style lang="scss" scoped>

.text {
  margin-left: 20px;
  .logo-title {
    font-size: 36px;
    letter-spacing: 2px;
    line-height: 1.2;
  }
  .logo-subtitle {
    display: block;
    font-size: 12px;
    text-align: center;
  }
}



.sw {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
}
</style>
