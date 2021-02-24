<template lang="pug">
  div.members(ref="a" id="members"  )
    carousel(
      name="team"
      :items-to-show="4"
      :initial-slide="0"
      :infinite-scroll="true"
      :loaded="loaded"
      :wheel-control="false"
      h="515px"
      W="1140px"
      :items="items"
    )
      template(v-slot="{item , index}")
        card(:item="item" :index="index" :idx="idx" @change-idx="changeIdxParent" )


    // Модальное окно
    modal-card(:items="items" :idx="idx" @close-modal="closeModal")

    //modal.member-modal-overlay(v-if="idx>=0" @close="idx=-1" :st="{width:'537px', background: '#2e303f', height: 'fit-content', borderRadius: '5px', overflow: 'hidden'}")
    //  div.member-modal-inner
    //    img.member-modal-preview-img(:src="items[idx].avatar" alt="")
    //
    //    h3.member-modal-title {{ items[idx].name }}
    //    p.member-modal-position {{ items[idx].position }}
    //    p.member-modal-desc(v-html="items[idx].description" v-if="items[idx].description")
    //
    //    div.member-portfolio-container(v-if="items[idx].portfolio.images.length > 0" )
    //      img.member-portfolio-img(:src="image" alt="portfolio-img" :key = "image" v-for="image in items[idx].portfolio.images" )
    //
    //    p.member-portfolio-text(v-if="items[idx].portfolio && items[idx].portfolio.text" v-html="items[idx].portfolio.text" )
    //
    //    div.contacts-container
    //      a(href="items[idx].contacts.tel" v-if="items[idx].contacts.tel") {{ items[idx].contacts.tel }}
    //      div.contact-icons-group
    //        a(:href="items[idx].contacts.fb" target="_blank" v-if="items[idx].contacts.fb")
    //          svg-icon(name='fb' class="contact-social-icon")
    //        a(:href="items[idx].contacts.tw" target="_blank" v-if="items[idx].contacts.tw")
    //          svg-icon(name='tw' class="contact-social-icon")
    //        a(:href="items[idx].contacts.te" target="_blank" v-if="items[idx].contacts.te")
    //          svg-icon(name='te' class="contact-social-icon")
    //        a(:href="items[idx].contacts.inst" target="_blank" v-if="items[idx].contacts.inst")
    //          svg-icon(name='inst' class="contact-social-icon")
    //        a(:href="items[idx].contacts.vk" target="_blank" v-if="items[idx].contacts.vk")
    //          svg-icon(name='vk' class="contact-social-icon")


</template>

<script>
import SvgIcon from './SvgIcon'
import Carousel from './Carousel'
import Card from './MemberCard'
import ModalCard from './MemberModalCard'

export default {
  components: {
    ModalCard,
    SvgIcon,
    Carousel,
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
    }
  },

  methods: {
    getTeam() {
      fetch(`/files/team/${this.$i18n.locale}.json`)
          .then(res => res.text())
          .then(res => {
            this.items = JSON.parse(res.replace(/\n/g, '')).items
            this.count = Math.round(this.$refs.a.clientWidth / 284);
          })
    },

    changeIdxParent(idx) {
      this.idx = idx
    },
    closeModal( idx ) {
      this.idx = idx
    },
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

  }
}
</script>
