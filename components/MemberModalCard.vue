<template lang="pug">
  modal.member-modal-overlay(v-if="idx>=0" @close="idx=-1" :st="{width:'537px', background: '#2e303f', height: 'fit-content', borderRadius: '5px', overflow: 'hidden'}")
    div.member-modal-inner
      img.member-modal-preview-img(:src="items[idx].avatar" alt="")

      h3.member-modal-title {{ items[idx].name }}
      p.member-modal-position {{ items[idx].position }}
      p.member-modal-desc(v-html="items[idx].description" v-if="items[idx].description")

      div.member-portfolio-container(v-if="items[idx].portfolio.images.length > 0" )
        img.member-portfolio-img(:src="image" alt="portfolio-img" :key = "image" v-for="image in items[idx].portfolio.images" )

      p.member-portfolio-text(v-if="items[idx].portfolio && items[idx].portfolio.text" v-html="items[idx].portfolio.text" )

      div.contacts-container
        a(href="items[idx].contacts.tel" v-if="items[idx].contacts.tel") {{ items[idx].contacts.tel }}
        div.contact-icons-group
          a(:href="items[idx].contacts.fb" target="_blank" v-if="items[idx].contacts.fb")
            svg-icon(name='fb' class="contact-social-icon")
          a(:href="items[idx].contacts.tw" target="_blank" v-if="items[idx].contacts.tw")
            svg-icon(name='tw' class="contact-social-icon")
          a(:href="items[idx].contacts.te" target="_blank" v-if="items[idx].contacts.te")
            svg-icon(name='te' class="contact-social-icon")
          a(:href="items[idx].contacts.inst" target="_blank" v-if="items[idx].contacts.inst")
            svg-icon(name='inst' class="contact-social-icon")
          a(:href="items[idx].contacts.vk" target="_blank" v-if="items[idx].contacts.vk")
            svg-icon(name='vk' class="contact-social-icon")
</template>

<script>
import Modal from "@/components/Modal";
import SvgIcon from './SvgIcon';

export default {
  name: "MemberModalCard",
  components: {
    Modal,
    SvgIcon,
  },
  props: ['items','idx'],
  methods: {
    closeModal() {
      this.$emit('close-modal',  -1);
    }
  },
}
</script>

<style lang="scss" scoped>

</style>
