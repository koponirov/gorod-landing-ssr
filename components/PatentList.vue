<template lang="pug">

div.wrapper
  div(:key='i', v-for='i in _list', class='group')

    h2(v-html="$t('patentApplications')")
    div.items
      div(v-for='item in list[i].items', :key='item.code', @click="()=>{country=item.code; modalShow=true}", class="item")


        svg-icon(f, :name="`${item.code}`", class="flag")
        span.name {{ $t(item.code) }}

    h2(v-html="$t('obtainedPatents')")
    div.items
      div(v-for='item in list[i].items_accepted', :key='item.code', @click="()=>{country=item.code; modalShow=true}", class="item")


        svg-icon(f, :name="`${item.code}`", class="flag")
        span.name {{ $t(item.code) }}


    modal(v-if="modalShow", @close="modalShow=false")

      template(v-if="country", v-slot:header)
        div.modal-header
          svg-icon(f, :name="`${country}`", class="flag-modal")
          span {{ $t(country) }}


      div.slider-link
        a(:href="`/files/patents/${banners[country].mp || country}.pdf`", download) Download document of patent for current country


      div.modal-img

        img(:src="`/files/patents/${banners[country].mp || country}-1.jpg`" v-if="banners[country].mp !== 'waiting'")
        div.modal-text(v-else)
          p(v-html="$t('waiting')")


      template(v-slot:footer)
        a(v-if="banners[country].link", target="_blank", class="slider-link", :href="banners[country].link") Link to review the progress of the National Phase
</template>


<script>
import Modal from './Modal'
import SvgIcon from './SvgIcon'

export default {
    components: {
        Modal,
        SvgIcon,
    },
    props: {
        cnt: {
            type: Number,
            default: 4
        },
        
    },
  data() {
    return {
      country: undefined,
      pageCount: 0,
      currentPage: 0,
      banners: {
        'ae': {count: 1, mp: 'waiting'},
        'al': {count: 1, mp: 'epo'},
        'am': {count: 1, mp: 'eapo'},
        'at': {count: 2, mp: 'epo'},
        'au': {count: 3},
        'az': {count: 1, mp: 'eapo'},
        'ba': {count: 2, mp: 'epo'},
        'be': {count: 2, mp: 'epo'},
        'bg': {count: 2, mp: 'epo'},
        'br': {count: 35},
        'by': {count: 1, mp: 'eapo'},
        'ca': {count: 1},
        'ch': {count: 2, mp: 'epo'},
        'cn': {count: 3},
        'cy': {count: 2, mp: 'epo'},
        'cz': {count: 2, mp: 'epo'},
        'de': {count: 2, mp: 'epo'},
        'dk': {count: 2, mp: 'epo'},
        'ee': {count: 2, mp: 'epo'},
        'eg': {count: 1},
        'es': {count: 2, mp: 'epo'},
        'gb': {count: 2, mp: 'epo'},
        'ge': {count: 1, mp: 'eapo'},
        'gr': {count: 2, mp: 'epo'},
        'hr': {count: 2, mp: 'epo'},
        'hu': {count: 2, mp: 'epo'},
        'id': {count: 3},
        'ie': {count: 2, mp: 'epo'},
        //'il': {count: 2},
        'in': {count: 1},
        'is': {count: 2, mp: 'epo'},
        'it': {count: 2, mp: 'epo'},
        'fi': {count: 2, mp: 'epo'},
        'fr': {count: 2, mp: 'epo'},
        'jp': {count: 2},
        'kg': {count: 1, mp: 'eapo'},
        'kh': {count: 2, mp: 'epo'},
        'kr': {count: 3},
        'kz': {count: 1, mp: 'eapo'},
        'li': {count: 2, mp: 'epo'},
        'lt': {count: 2, mp: 'epo'},
        'lu': {count: 2, mp: 'epo'},
        'lv': {count: 2, mp: 'epo'},
        'ma': {count: 2, mp: 'epo'},
        'mc': {count: 2, mp: 'epo'},
        'md': {count: 2, mp: 'epo'},
        'me': {count: 2, mp: 'epo'},
        'mk': {count: 2, mp: 'epo'},
        'mt': {count: 2, mp: 'epo'},
        'mx': {count: 6},
        'my': {count: 1},
        'nl': {count: 2, mp: 'epo'},
        'no': {count: 2, mp: 'epo'},
        'nz': {count: 2},
        //'om': {count: 3},
        'ph': {count: 3},
        'pl': {count: 2, mp: 'epo'},
        'pt': {count: 2, mp: 'epo'},
        'ro': {count: 2, mp: 'epo'},
        'rs': {count: 2, mp: 'epo'},
        'ru': {count: 1},
        'sa': {count: 2, mp: 'waiting'},
        'se': {count: 2, mp: 'epo'},
        //'sg': {count: 14},
        'si': {count: 2, mp: 'epo'},
        'sk': {count: 2, mp: 'epo'},
        'sm': {count: 2, mp: 'epo'},
        'sn': {count: 2, mp: 'epo'},
        'th': {count: 4},
        'tj': {count: 1, mp: 'eapo'},
        'tm': {count: 1, mp: 'eapo'},
        'tn': {count: 1, mp: 'epo'},
        //'tr': {count: 2},
        'us': {count: 5},
        //'vn': {count: 9},
        'za': {count: 1}
      },
      modalShow: false,
      list: [
        {
          id: 2,
          title: 'podacha',
          items_accepted: [
            { code: 'ru' },
          ],
          items: [
            { code: 'us' },
            { code: 'jp' },
            { code: 'ae' },
            { code: 'al' },
            { code: 'am' },
            { code: 'at' },
            { code: 'az' },
            { code: 'au' },
            { code: 'ba' },
            { code: 'be' },
            { code: 'bg' },
            { code: 'br' },
            { code: 'by' },
            { code: 'ca' },
            { code: 'ch' },
            { code: 'cn' },
            { code: 'cy' },
            { code: 'cz' },
            { code: 'de' },
            { code: 'dk' },
            { code: 'ee' },
            { code: 'eg' },
            { code: 'es' },
            { code: 'gb' },
            { code: 'ge' },
            { code: 'gr' },
            { code: 'hu' },
            { code: 'id' },
            { code: 'ie' },
            //{ code: 'il' },
            { code: 'in' },
            { code: 'is' },
            { code: 'it' },
            { code: 'fi' },
            { code: 'fr' },

            { code: 'hr' },
            { code: 'kg' },
            { code: 'kh' },
            { code: 'kr' },
            { code: 'kz' },
            { code: 'li' },
            { code: 'lv' },
            { code: 'lt' },
            { code: 'lu' },
            { code: 'ma' },
            { code: 'mc' },
            { code: 'me' },
            { code: 'md' },
            { code: 'mk' },
            { code: 'mt' },
            { code: 'mx' },
            { code: 'my' },
            { code: 'nl' },
            { code: 'no' },
            { code: 'nz' },
            //{ code: 'om' },
            { code: 'ph' },
            { code: 'pl' },
            { code: 'pt' },
            { code: 'rs' },

            { code: 'ro' },
            { code: 'sa' },
            { code: 'se' },
            //{ code: 'sg' },
            { code: 'si' },
            { code: 'sk' },
            { code: 'sm' },
            { code: 'th' },
            { code: 'tj' },
            { code: 'tm' },
            { code: 'tn' },
            //{ code: 'tr' },

            //{ code: 'vn' },
            { code: 'za' },
          ]
        }
      ]
    }
  },
    computed: {
        _list() {
            return [0]
        }
    }
}
</script>

<style lang="scss" scoped>
.modal-img {
    width: 100%;
    height: 100%;
}
.wrapper {
    //padding: 0 10px;
}

.group {
    position: relative;
    width: 95%;
}

.title {
    font-size: 14px;
    font-weight: 600;
    margin-bottom: 26px;
}

.items {
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
    //@media screen and (orientation: portrait) {
    //    justify-content: center;
    //}
    align-content: center;
    padding-bottom: 26px;
}
.item {
    width: 66px;
    height: 82px;
    //@media screen and (orientation: portrait) {
    //    width: 100px;
    //    height: 124px;
    //}
    margin: 10px 10px 10px 0;
    background: #2e355e;
    text-align: center;
    border-radius: 4px;
    cursor: pointer;
    overflow: hidden;

}
.flag {
   margin: 1px;
   width: 98%;
   height: 60%;
}
.name {
    font-size: 9px;
    margin-top: 3px;
    line-height: 10px;
    @media screen and (orientation: portrait) {
        font-size: 14px;
        margin-top: 6px;
    }
}
.pages {
    margin-left: 20px;
}
.modal-header {
    display: flex;
    align-items: center;
    .flag-modal {
        width: 40px;
        height: 30px;
        margin-right: 40px;
    }
}

.slider-link {
    margin-bottom: 10px;
    margin-top: 10px;
    text-decoration: underline;
    color: #347dfe;
    display: block;
    font-style: italic;
    text-align: center;
}

.modal-text {
  display: flex;
  justify-content: center;
  align-items: center;
  p {
    margin: 150px 15px;
    font-style: normal;
    font-weight: 500;
    font-size: 15px;
    line-height: 18px;
    text-align: center;
  }
}
</style>
