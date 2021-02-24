<template lang="pug">
footer.footer
  .container
    .phone
      a(href="tel:79069091091") +7 906 909-10-91
      p(v-html="$t('weAnswerByPhone')")

    .mail
      a(href="mailto:GOROD@denistiaglin.com")  GOROD@denistiaglin.com
      p(v-html="$t('footerAddress')")

    .social

        div(@click="showLinks($event)" class="social-icon" id="telegram" v-click-outside="hide" role="menu")
            svg-icon.telegram-icon(name="telegram" :class="{ active: links === 'telegram' }")
            div.social-links(v-if="links === 'telegram'")
                a.social-link(:href="telegram.group" target="_blank")
                    img(src='../../src/assets/img/social/groups.svg')
                    span Official group
                a.social-link(:href="telegram.support" target="_blank")
                    img(src='../../src/assets/img/social/support.svg')
                    span Support

        div(@click="showLinks($event)" class="social-icon" id="whatsapp" v-click-outside="hide" role="menu" )
            svg-icon.whatsapp-icon(name="whatsapp" :class="{ active: links === 'whatsapp' }")
            div.social-links(v-if="links ==='whatsapp'")
                a.social-link(href="https://chat.whatsapp.com/Ih3TajqGVlHL1bXc39regd" target="_blank")
                    img(src='../../src/assets/img/social/groups.svg')
                    span Official group
                a.social-link(href="https://wa.me/79069091091" target="_blank")
                    img(src='../../src/assets/img/social/support.svg')
                    span Support

        div(class="social-icon")

</template>

<script>
    import SvgIcon from './SvgIcon'
    import ClickOutside from 'vue-click-outside'


    export default {
        components: {
            SvgIcon
        },
        data: function () {
            return {
                links: '',
                telegram: {
                    group: '',
                    support: 'https://t.me/ENERGY2020_SUPPORT'
                }
            }
        },
        methods: {
            setTelegramLink: function () {
                if (this.$i18n.locale === 'ru') {
                    return this.telegram.group = "https://t.me/joinchat/J_qsohtY5RZaZM06M5d1-Q"
                } else {
                    return this.telegram.group = "https://t.me/joinchat/DRUw9Rqr-aauwEjqwwTSGg"
                }
            },

            showLinks: function (event) {

                this.setTelegramLink()

                switch (event.currentTarget.id) {
                    case 'telegram':
                        this.links = this.links === 'telegram' ? this.component = '' : this.component = 'telegram'
                        break
                    case 'whatsapp':
                        this.links = this.links === 'whatsapp' ? this.component = '' : this.component = 'whatsapp'
                        break
                }
            },
            hide () {
                this.links = ''
            },
            localeTelegramLink: function () {
                // `this` указывает на экземпляр vm
                if (this.$i18n.locale === 'ru') {
                    return this.telegram.ru
                } else {
                    return this.telegram.en
                }
            }

        },
        mounted () {
            // prevent click outside event with popupItem.
            this.popupItem = this.$el
        },

        // do not forget this section
        directives: {
            ClickOutside
        }
    }
</script>



<style lang="scss" scoped>
    .active {
        filter: drop-shadow(2px 5px 4px rgba(52, 125, 254, 1));
    }

    .social-icon {
        position: relative;
        margin-right: 30px;
        cursor: pointer;

        svg:hover,svg:focus {
            filter: drop-shadow(2px 5px 4px rgba(52, 125, 254, 1));
        }
    }


    .social-links {
        display: flex;
        flex-direction: column;
        background-color: #2e355e;
        width: max-content;
        position: absolute;
        bottom: 100px;
        right: -58px;
        border-radius: 5px;
        padding: 10px;

        .social-link {
            display: flex;
            align-items: center;
            font-size: 18px;
            font-weight: normal;
            img {
                height: 38px;
                width: 38px;
                margin-right: 10px;
            }
        }

        .social-link:hover {
            text-decoration: underline;
            cursor: pointer;
        }

    }
    .social-links::after {
        content: ' ';
        position: absolute;
        width: 0;
        height: 0;
        border-left: 10px solid transparent;
        border-right: 10px solid transparent;
        border-top: 20px solid #2e355e;
        top: 110px;
        right: 65px;
    }


    .whatsapp-icon {
        width: 35px;
        height: 35px;
    }
    .telegram-icon {
        width: 38px;
        height: 35px;
    }
</style>