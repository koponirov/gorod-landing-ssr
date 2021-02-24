<template lang="pug">
    section.section-patents
        .container
            canvas(id="canvas" width="1200" height="1600")
            .patent-container

                .patent-item(@click="()=>{ this.name='diplom'; this.modalShow=true}")
                    img(src="../../src/assets/img/patents/diplom.jpg" alt="gorod-diplom" class="preview")
                .patent-item(@click="()=>{ this.name='patent-new'; this.modalShow=true}")
                    img(src="../../src/assets/img/patents/patent-new.jpg" alt="gorod-patent" class="preview")
                .video-block
                    .video-container
                        .video-play-button(@click="playVideo1")
                            .play-video-btn
                                svg-icon(name="play")
                        .video-label
                            .icon
                                img(src="../../src/assets/img/patents/rospatent_logo.png" alt="logo-rospatent")
                            .video-title
                                span(v-html="$t('video-label1')")
                    .video-container
                        .video-play-button(@click="playVideo2" )
                            .play-video-btn
                                svg-icon(name="play")
                        .video-label
                            .icon
                                img(src="../../src/assets/img/patents/raasn-logo.jpg" alt="logo-raasn")
                            .video-title
                                span(v-html="$t('video-label2')")
                    .video-container
                        .video-play-button(@click="playVideo3")
                            .play-video-btn
                                svg-icon(name="play")
                        .video-label
                            .icon
                                img(src="../../src/assets/img/patents/rospatent_logo.jpg" alt="logo-rospatent")
                            .video-title
                                span(v-html="$t('video-label3')")


            .wipo-container
                .patent-text
                    img.wipo-logo(src="../../src/assets/img/patents/wipo-logo.83fe6abe.png" alt="logo-wipo")
                    p(v-html="$t('applicationForAnInvention')")
                .patent-item1(@click="()=>{this.name = 'sert'; this.modalShow=true}")
                    img(src="../../src/assets/img/patents/sert.jpg" alt="gorod-sertificate" class="preview")
                    span РСТ
                .patent-text

            .patent-countries
                patent-list
            modal(v-if="modalShow", :name="name" @close="modalShow=false")
            youtube-player(v-if="play" :videoId="videoId" @close="play=false")


</template>

<script>
    import SvgIcon from './SvgIcon'
    import YoutubePlayer from "@/components/YoutubePlayer";
    import Modal from './Modal1'
    import PatentList from './PatentList'

    export default {
        components: {
            Modal,
            PatentList,
            SvgIcon,
            YoutubePlayer
        },
        data: function () {
            return {
                modalShow: false,
                play: false,
                name: null,
                videoId: null
            }
        },
        methods: {
            playVideo1: function () {
                debugger
                this.videoId = (this.$i18n.locale === 'ru') ? 'UxaB0xzgIw8' : "Upo-UU0P9E0";
                this.play = true
            },
            playVideo2: function () {
                this.videoId = (this.$i18n.locale === 'ru') ? 'TXTnwgxYVZU' : "9wnvtjeOWIM";
                this.play = true
            },
            playVideo3: function () {
                this.videoId = (this.$i18n.locale === 'ru') ? 'v9SWoHCu1Dc' : "-1BtpW2T6-Q";
                this.play = true
            }
        },
        mounted() {
            var canvas = document.getElementById('canvas');
            var ctx = canvas.getContext('2d');


            function electronX(start_pos_x, start_pos_y, end_pos_x, end_pos_y, width, height) {

                let startPointX = start_pos_x;
                let endPointX = end_pos_x;

                return function () {

                    ctx.fillStyle = "#4c4b6a"
                    ctx.fillRect(startPointX, start_pos_y, width, height)

                    if (startPointX >= endPointX - width) {
                        startPointX = start_pos_x

                    }

                    startPointX += 3;
                }
            }

            function electronX_reverse(start_pos_x, start_pos_y, end_pos_x, end_pos_y, width, height, shift) {

                let startPointX = (start_pos_x - width - shift);
                let endPointX = end_pos_x;


                return function () {

                    ctx.fillStyle = "#4c4b6a"
                    ctx.fillRect(startPointX, start_pos_y, width, height)

                    if (startPointX <= endPointX) {
                        startPointX = start_pos_x - width

                    }

                    startPointX -= 3;
                }
            }

            function electronY(start_pos_x, start_pos_y, end_pos_x, end_pos_y, width, height, increment, shift = 0) {

                let startPointY = (start_pos_y + height + shift);
                let endPointY = end_pos_y;

                return function () {

                    ctx.fillStyle = "#4c4b6a"
                    ctx.fillRect(start_pos_x, startPointY, width, height)

                    if (startPointY >= endPointY - height) {
                        startPointY = start_pos_y
                    }

                    startPointY += increment;
                }
            }

            function electronXY(start_pos_x, start_pos_y, end_pos_x, end_pos_y, width = 2, height = 2, shift = 0) {

                let startPointX = (start_pos_x - shift);
                let startPointY = (start_pos_y + shift);

                let endPointX = end_pos_x;
                let endPointY = end_pos_y;

                return function () {

                    ctx.fillStyle = "#4c4b6a"
                    ctx.fillRect(startPointX, startPointY, 2, 2)

                    if (startPointY >= endPointY - 3) {

                        startPointX = start_pos_x
                        startPointY = start_pos_y

                    }

                    startPointX -= 3;
                    startPointY += 3;
                }
            }

            //top line
            //horizontal
            let drawElectronX1 = electronX(413, 44, 1120, 44, 18, 2)
            let drawElectronX1_1 = electronX(385, 44, 1120, 44, 35, 2)
            let drawElectronX1_2 = electronX(250, 44, 1120, 44, 12, 2)
            let drawElectronX1_3 = electronX(240, 44, 1120, 44, 15, 2)
            let drawElectronX1_4 = electronX(235, 44, 1120, 44, 22, 2)
            let drawElectronX1_5 = electronX(350, 44, 1120, 44, 27, 2)
            let drawElectronX1_6 = electronX(375, 44, 1120, 44, 19, 2)
            let drawElectronX1_7 = electronX(1000, 44, 1120, 44, 18, 2)
            let drawElectronX1_8 = electronX(890, 44, 1120, 44, 35, 2)
            let drawElectronX1_9 = electronX(950, 44, 1120, 44, 12, 2)
            //vertical
            let drawElectronY1 = electronY(1119, 44, 1119, 270, 2, 21, 3)
            let drawElectronY1_1 = electronY(1119, 44, 1119, 270, 2, 14, 3)
            let drawElectronY1_2 = electronY(1119, 44, 1119, 270, 2, 17, 3)
            let drawElectronY1_3 = electronY(1119, 44, 1119, 270, 2, 25, 3)
            //angle 1
            let drawElectronXY1_1 = electronXY(1120, 270, 1035, 360, 2, 12)
            let drawElectronXY1_2 = electronXY(1120, 270, 1035, 360, 2, 12)
            let drawElectronXY1_3 = electronXY(1120, 270, 1035, 360, 2, 12)
            //horizontal 2
            let drawElectronX_top_reverse_1 = electronX_reverse(1035, 359, 439, 359, 12, 2, 15)
            let drawElectronX_top_reverse_2 = electronX_reverse(1035, 359, 440, 359, 25, 2, 45)
            let drawElectronX_top_reverse_3 = electronX_reverse(1035, 359, 438, 359, 17, 2, 85)
            let drawElectronX_top_reverse_4 = electronX_reverse(1035, 359, 440, 359, 22, 2, 146)
            let drawElectronX_top_reverse_5 = electronX_reverse(1035, 359, 440, 359, 15, 2, 187)
            let drawElectronX_top_reverse_6 = electronX_reverse(1035, 359, 440, 359, 19, 2, 199)
            let drawElectronX_top_reverse_7 = electronX_reverse(1035, 359, 440, 359, 13, 2, 250)
            let drawElectronX_top_reverse_8 = electronX_reverse(1035, 359, 440, 359, 8, 2, 340)
            let drawElectronX_top_reverse_9 = electronX_reverse(1035, 359, 440, 359, 8, 2, 450)
            let drawElectronX_top_reverse_10 = electronX_reverse(1035, 359, 440, 359, 8, 2, 490)
            let drawElectronX_top_reverse_11 = electronX_reverse(1035, 359, 440, 359, 8, 2, 535)
            //angle 2
            let drawElectronXY2_top_1 = electronXY(439, 360, 359, 440, 1, 1)
            let drawElectronXY2_top_2 = electronXY(437, 362, 359, 440, 1, 1)
            //vertical 2
            let drawElectronY1_4 = electronY(359, 440, 359, 460, 2, 3, 1)
            //horizontal 3
            let drawElectronX1_10 = electronX(360, 459, 480, 459, 12, 2)
            let drawElectronX1_11 = electronX(360, 459, 480, 459, 15, 2)
            let drawElectronX1_12 = electronX(360, 459, 480, 459, 22, 2)
            //horizontal 4
            let drawElectronX1_13 = electronX(560, 599, 1120, 599, 12, 2)
            let drawElectronX1_14 = electronX(580, 599, 1120, 599, 15, 2)
            let drawElectronX1_15 = electronX(590, 599, 1120, 599, 22, 2)
            let drawElectronX1_16 = electronX(610, 599, 1120, 599, 25, 2)
            let drawElectronX1_17 = electronX(630, 599, 1120, 599, 18, 2)
            let drawElectronX1_18 = electronX(660, 599, 1120, 599, 11, 2)
            //vertical 3
            let drawElectronY1_5 = electronY(1119, 600, 1119, 720, 2, 3, 2)
            let drawElectronY1_6 = electronY(1119, 600, 1119, 720, 2, 6, 2)
            let drawElectronY1_7 = electronY(1119, 600, 1119, 720, 2, 13, 2)
            //angle 3
            let drawElectronXY2_top_3 = electronXY(1119, 719, 1039, 819, 1, 1)
            let drawElectronXY2_top_4 = electronXY(1119, 719, 1039, 819, 1, 1)
            //horizontal 5
            let drawElectronX_top_reverse_12 = electronX_reverse(1039, 799, 215, 799, 12, 2, 15)
            let drawElectronX_top_reverse_13 = electronX_reverse(1039, 799, 215, 799, 25, 2, 45)
            let drawElectronX_top_reverse_14 = electronX_reverse(1039, 799, 215, 799, 17, 2, 85)
            let drawElectronX_top_reverse_15 = electronX_reverse(1039, 799, 215, 799, 22, 2, 146)
            let drawElectronX_top_reverse_16 = electronX_reverse(1039, 799, 215, 799, 15, 2, 187)
            let drawElectronX_top_reverse_17 = electronX_reverse(1039, 799, 215, 799, 19, 2, 199)
            let drawElectronX_top_reverse_18 = electronX_reverse(1039, 799, 215, 799, 13, 2, 250)
            let drawElectronX_top_reverse_19 = electronX_reverse(1039, 799, 215, 799, 8, 2, 340)
            let drawElectronX_top_reverse_20 = electronX_reverse(1039, 799, 215, 799, 8, 2, 450)
            let drawElectronX_top_reverse_21 = electronX_reverse(1039, 799, 215, 799, 8, 2, 490)
            let drawElectronX_top_reverse_22 = electronX_reverse(1039, 799, 215, 799, 8, 2, 535)
            //angle 4
            let drawElectronXY2_top_5 = electronXY(214, 799, 184, 829, 1, 1)
            //vertical 4
            let drawElectronY1_8 = electronY(184, 830, 184, 1150, 2, 6, 2)
            let drawElectronY1_9 = electronY(184, 830, 184, 1140, 2, 3, 2)
            let drawElectronY1_10 = electronY(184, 830, 184, 1130, 2, 9, 2)
            let drawElectronY1_11 = electronY(184, 1150, 184, 1350, 2, 6, 2)
            let drawElectronY1_12 = electronY(184, 1140, 184, 1350, 2, 9, 2)
            let drawElectronY1_13 = electronY(184, 1130, 184, 1350, 2, 2, 2)
            // //2vertical
            // ctx.moveTo(185, 830)
            // ctx.lineTo(185, 1200)


            //middle line
            //horizontal
            let drawElectronX2 = electronX(413, 129, 1100, 129, 18, 2)
            let drawElectronX2_1 = electronX(385, 129, 1100, 129, 35, 2)
            let drawElectronX2_2 = electronX(250, 129, 1100, 129, 12, 2)
            let drawElectronX2_3 = electronX(240, 129, 1100, 129, 15, 2)
            let drawElectronX2_4 = electronX(235, 129, 1100, 129, 22, 2)
            let drawElectronX2_5 = electronX(350, 129, 1100, 129, 27, 2)
            let drawElectronX2_6 = electronX(375, 129, 1100, 129, 19, 2)
            let drawElectronX2_7 = electronX(1000, 129, 1100, 129, 18, 2)
            let drawElectronX2_8 = electronX(890, 129, 1100, 129, 35, 2)
            let drawElectronX2_9 = electronX(950, 129, 1100, 129, 12, 2)
            //vertical
            let drawElectronY2 = electronY(1099, 129, 1159, 260, 2, 18, 3)
            let drawElectronY2_1 = electronY(1099, 129, 1159, 260, 2, 25, 3)
            let drawElectronY2_2 = electronY(1099, 129, 1159, 260, 2, 18, 2)
            let drawElectronY2_3 = electronY(1099, 129, 1159, 260, 2, 15, 3)
            //angle
            let drawElectronXY2_1 = electronXY(1099, 260, 1025, 340, 2, 12)
            let drawElectronXY2_2 = electronXY(1099, 260, 1025, 340, 2, 12)
            let drawElectronXY2_3 = electronXY(1099, 260, 1025, 340, 2, 12)
            //horizontal
            let drawElectronX_middle_reverse_1 = electronX_reverse(1025, 339, 430, 339, 13, 2, 16)
            let drawElectronX_middle_reverse_2 = electronX_reverse(1025, 339, 430, 339, 24, 2, 47)
            let drawElectronX_middle_reverse_3 = electronX_reverse(1025, 339, 430, 339, 18, 2, 83)
            let drawElectronX_middle_reverse_4 = electronX_reverse(1025, 339, 430, 339, 21, 2, 156)
            let drawElectronX_middle_reverse_5 = electronX_reverse(1025, 339, 430, 339, 15, 2, 197)
            let drawElectronX_middle_reverse_6 = electronX_reverse(1025, 339, 430, 339, 19, 2, 209)
            let drawElectronX_middle_reverse_7 = electronX_reverse(1025, 339, 430, 339, 13, 2, 256)
            let drawElectronX_middle_reverse_8 = electronX_reverse(1025, 339, 430, 339, 5, 2, 345)
            let drawElectronX_middle_reverse_9 = electronX_reverse(1025, 339, 430, 339, 11, 2, 451)
            let drawElectronX_middle_reverse_10 = electronX_reverse(1025, 339, 430, 339, 9, 2, 492)
            let drawElectronX_middle_reverse_11 = electronX_reverse(1025, 339, 430, 339, 8, 2, 536)
            //2angle
            let drawElectronXY2_4 = electronXY(430, 339, 340, 429)
            //vertical 2
            let drawElectronY2_4 = electronY(339, 430, 339, 480, 2, 3, 1)
            let drawElectronY2_5 = electronY(339, 430, 339, 480, 2, 6, 1)
            //horizontal 3
            let drawElectronX2_10 = electronX(340, 479, 480, 479, 12, 2)
            let drawElectronX2_11 = electronX(340, 479, 480, 479, 15, 2)
            let drawElectronX2_12 = electronX(340, 479, 480, 479, 22, 2)
            //horizontal 4 after sertificate
            let drawElectronX2_13 = electronX(660, 619, 1100, 619, 12, 2)
            let drawElectronX2_14 = electronX(630, 619, 1100, 619, 15, 2)
            let drawElectronX2_15 = electronX(645, 619, 1100, 619, 22, 2)
            let drawElectronX2_16 = electronX(625, 619, 1100, 619, 8, 2)
            let drawElectronX2_17 = electronX(600, 619, 1100, 619, 10, 2)
            let drawElectronX2_18 = electronX(590, 619, 1100, 619, 9, 2)
            //vertical 3
            let drawElectronY2_6 = electronY(1099, 620, 1099, 710, 2, 6, 2)
            let drawElectronY2_7 = electronY(1099, 620, 1099, 710, 2, 3, 2)
            let drawElectronY2_8 = electronY(1099, 620, 1099, 710, 2, 2, 2)
            //2angle
            let drawElectronXY2_5 = electronXY(1099, 709, 1029, 779)
            //horizontal 5
            let drawElectronX_middle_reverse_12 = electronX_reverse(1030, 779, 160, 779, 18, 2, 83)
            let drawElectronX_middle_reverse_13 = electronX_reverse(1030, 779, 160, 779, 21, 2, 156)
            let drawElectronX_middle_reverse_14 = electronX_reverse(1030, 779, 160, 779, 15, 2, 197)
            let drawElectronX_middle_reverse_15 = electronX_reverse(1030, 779, 160, 779, 19, 2, 209)
            let drawElectronX_middle_reverse_16 = electronX_reverse(1030, 779, 160, 779, 13, 2, 256)
            let drawElectronX_middle_reverse_17 = electronX_reverse(1030, 779, 160, 779, 5, 2, 345)
            let drawElectronX_middle_reverse_18 = electronX_reverse(1030, 779, 160, 779, 11, 2, 451)
            let drawElectronX_middle_reverse_19 = electronX_reverse(1030, 779, 160, 779, 9, 2, 492)
            let drawElectronX_middle_reverse_20 = electronX_reverse(1030, 779, 160, 779, 8, 2, 536)
            let drawElectronX_middle_reverse_21 = electronX_reverse(1030, 779, 160, 779, 8, 2, 570)
            let drawElectronX_middle_reverse_22 = electronX_reverse(1030, 779, 160, 779, 8, 2, 595)
            let drawElectronX_middle_reverse_23 = electronX_reverse(1030, 779, 160, 779, 8, 2, 615)
            //angle 3
            let drawElectronXY2_6 = electronXY(159, 779, 109, 859)
            //vertical 4
            let drawElectronY2_9 = electronY(109, 830, 109, 1150, 2, 6, 2)
            let drawElectronY2_10 = electronY(109, 830, 109, 1140, 2, 3, 2)
            let drawElectronY2_11 = electronY(109, 830, 109, 1130, 2, 9, 2)
            let drawElectronY2_12 = electronY(109, 1150, 109, 1350, 2, 6, 2)
            let drawElectronY2_13 = electronY(109, 1140, 109, 1350, 2, 9, 2)
            let drawElectronY2_14 = electronY(109, 1130, 109, 1350, 2, 2, 2)


            //bottom line
            //horizontal
            let drawElectronX3_01 = electronX(50, 179, 335, 179, 18, 2)
            let drawElectronX3_02 = electronX(40, 194, 350, 194, 17, 2)
            let drawElectronX3_03 = electronX(35, 209, 320, 209, 16, 2)
            let drawElectronX3 = electronX(413, 224, 1080, 224, 18, 2)
            let drawElectronX3_1 = electronX(385, 224, 1080, 224, 35, 2)
            let drawElectronX3_2 = electronX(250, 224, 1080, 224, 12, 2)
            let drawElectronX3_3 = electronX(240, 224, 1080, 224, 15, 2)
            let drawElectronX3_4 = electronX(235, 224, 1080, 224, 22, 2)
            let drawElectronX3_5 = electronX(350, 224, 1080, 224, 27, 2)
            let drawElectronX3_6 = electronX(375, 224, 1080, 224, 19, 2)
            let drawElectronX3_7 = electronX(1000, 224, 1080, 224, 18, 2)
            let drawElectronX3_8 = electronX(890, 224, 1080, 224, 35, 2)
            let drawElectronX3_9 = electronX(950, 224, 1080, 224, 12, 2)
            let drawElectronX3_10 = electronX(50, 224, 413, 224, 12, 2)
            let drawElectronX3_11 = electronX(40, 224, 385, 224, 12, 2)
            //vertical
            let drawElectronY3 = electronY(1079, 224, 1079, 250, 2, 3, 1)
            //angle
            let drawElectronXY3_1 = electronXY(1079, 249, 1017, 320, 2, 2)
            let drawElectronXY3_2 = electronXY(1079, 249, 1017, 320, 2, 1)
            let drawElectronXY3_3 = electronXY(1079, 249, 1017, 320, 2, 2)
            //horizontal 2
            let drawElectronX_bottom_reverse_1 = electronX_reverse(1017, 319, 420, 319, 13, 2, 16)
            let drawElectronX_bottom_reverse_2 = electronX_reverse(1017, 319, 420, 319, 24, 2, 47)
            let drawElectronX_bottom_reverse_3 = electronX_reverse(1017, 319, 420, 319, 18, 2, 83)
            let drawElectronX_bottom_reverse_4 = electronX_reverse(1017, 319, 420, 319, 21, 2, 156)
            let drawElectronX_bottom_reverse_5 = electronX_reverse(1017, 319, 420, 319, 15, 2, 197)
            let drawElectronX_bottom_reverse_6 = electronX_reverse(1017, 319, 420, 319, 19, 2, 209)
            let drawElectronX_bottom_reverse_7 = electronX_reverse(1017, 319, 420, 319, 13, 2, 256)
            let drawElectronX_bottom_reverse_8 = electronX_reverse(1017, 319, 420, 319, 5, 2, 345)
            let drawElectronX_bottom_reverse_9 = electronX_reverse(1017, 319, 420, 319, 11, 2, 451)
            let drawElectronX_bottom_reverse_10 = electronX_reverse(1017, 319, 420, 319, 9, 2, 492)
            let drawElectronX_bottom_reverse_11 = electronX_reverse(1017, 319, 420, 319, 8, 2, 536)
            //2angle
            let drawElectronXY3_4 = electronXY(420, 319, 320, 419)
            //vertical 2
            let drawElectronY3_1 = electronY(319, 420, 319, 499, 2, 3, 2)
            let drawElectronY3_2 = electronY(319, 420, 319, 499, 2, 6, 2)
            let drawElectronY3_3 = electronY(319, 420, 319, 499, 2, 8, 2)
            //horizontal 3
            let drawElectronX3_12 = electronX(320, 499, 480, 499, 27, 2)
            let drawElectronX3_13 = electronX(320, 499, 480, 499, 19, 2)
            let drawElectronX3_14 = electronX(320, 499, 480, 499, 18, 2)
            //horizontal 4 after sertificate
            let drawElectronX3_15 = electronX(660, 639, 1080, 639, 22, 2)
            let drawElectronX3_16 = electronX(640, 639, 1080, 639, 27, 2)
            let drawElectronX3_17 = electronX(620, 639, 1080, 639, 19, 2)
            let drawElectronX3_18 = electronX(600, 639, 1080, 639, 18, 2)
            let drawElectronX3_19 = electronX(550, 639, 1080, 639, 35, 2)
            let drawElectronX3_20 = electronX(570, 639, 1080, 639, 12, 2)
            //vertical 3
            let drawElectronY3_4 = electronY(1079, 640, 1079, 700, 2, 3, 2)
            let drawElectronY3_5 = electronY(1079, 640, 1079, 700, 2, 6, 2)
            let drawElectronY3_6 = electronY(1079, 640, 1079, 700, 2, 8, 2)
            //angle 3
            let drawElectronXY3_5 = electronXY(1079, 700, 1019, 760)
            //horizontal 5
            let drawElectronX_bottom_reverse_12 = electronX_reverse(1020, 759, 105, 759, 13, 2, 16)
            let drawElectronX_bottom_reverse_13 = electronX_reverse(1020, 759, 105, 759, 24, 2, 47)
            let drawElectronX_bottom_reverse_14 = electronX_reverse(1020, 759, 105, 759, 18, 2, 83)
            let drawElectronX_bottom_reverse_15 = electronX_reverse(1020, 759, 105, 759, 21, 2, 156)
            let drawElectronX_bottom_reverse_16 = electronX_reverse(1020, 759, 105, 759, 15, 2, 197)
            let drawElectronX_bottom_reverse_17 = electronX_reverse(1020, 759, 105, 759, 19, 2, 209)
            let drawElectronX_bottom_reverse_18 = electronX_reverse(1020, 759, 105, 759, 13, 2, 256)
            let drawElectronX_bottom_reverse_19 = electronX_reverse(1020, 759, 105, 759, 5, 2, 345)
            let drawElectronX_bottom_reverse_20 = electronX_reverse(1020, 759, 105, 759, 11, 2, 451)
            let drawElectronX_bottom_reverse_21 = electronX_reverse(1020, 759, 105, 759, 9, 2, 492)
            let drawElectronX_bottom_reverse_22 = electronX_reverse(1020, 759, 105, 759, 10, 2, 536)
            let drawElectronX_bottom_reverse_23 = electronX_reverse(1020, 759, 105, 759, 12, 2, 566)
            let drawElectronX_bottom_reverse_24 = electronX_reverse(1020, 759, 105, 759, 7, 2, 586)
            let drawElectronX_bottom_reverse_25 = electronX_reverse(1020, 759, 105, 759, 20, 2, 626)
            //angle 4
            let drawElectronXY3_6 = electronXY(104, 759, 34, 829)
            //vertical 4
            let drawElectronY3_7 = electronY(34, 830, 34, 1146, 2, 12, 2, 15)
            let drawElectronY3_8 = electronY(34, 832, 34, 1148, 2, 15, 2, 45)
            let drawElectronY3_9 = electronY(34, 833, 34, 1150, 2, 8, 2, 85)
            let drawElectronY3_10 = electronY(34, 1146, 34, 1546, 2, 12, 2, 148)
            let drawElectronY3_11 = electronY(34, 1148, 34, 1548, 2, 15, 2, 247)
            let drawElectronY3_12 = electronY(34, 1150, 34, 1550, 2, 8, 2, 368)

            //4 vertical line
            //4angle
            // ctx.moveTo(291, 800)
            // ctx.lineTo(261, 830)
            let drawElectronXY3_7 = electronXY(290, 799, 260, 829, 2, 2, 3)
            // //4vert
            // ctx.moveTo(261, 830)
            // ctx.lineTo(261, 1350)
            let drawElectronY3_13 = electronY(260, 830, 260, 1350, 2, 5, 2, 10)
            let drawElectronY3_14 = electronY(260, 830, 260, 1350, 2, 15, 2, 158)
            let drawElectronY3_15 = electronY(260, 830, 260, 1350, 2, 8, 2, 279)
            let drawElectronY3_16 = electronY(260, 830, 260, 1350, 2, 12, 2, 333)
            let drawElectronY3_17 = electronY(260, 830, 260, 1350, 2, 15, 2, 379)
            let drawElectronY3_18 = electronY(260, 830, 260, 1350, 2, 18, 2, 417)

            //
            // //5 vertical line
            // //5angle
            // ctx.moveTo(367, 800)
            // ctx.lineTo(337, 830)
            let drawElectronXY3_8 = electronXY(366, 799, 336, 829, 2, 2, 5)
            // //5vert
            // ctx.moveTo(337, 830)
            // ctx.lineTo(337, 1350)
            let drawElectronY3_19 = electronY(336, 830, 336, 1350, 2, 12, 2, 8)
            let drawElectronY3_20 = electronY(336, 830, 336, 1350, 2, 15, 2, 127)
            let drawElectronY3_21 = electronY(336, 830, 336, 1350, 2, 8, 2, 157)
            let drawElectronY3_22 = electronY(336, 830, 336, 1350, 2, 12, 2, 289)
            let drawElectronY3_23 = electronY(336, 830, 336, 1350, 2, 15, 2, 344)
            let drawElectronY3_24 = electronY(336, 830, 336, 1350, 2, 8, 2, 415)
            //
            // //6 vertical line
            // //6angle
            // ctx.moveTo(4430 88290// ctx.lineTo(413, 830)
            let drawElectronXY3_9 = electronXY(442, 799, 412, 829, 2, 2, 7)
            // //6vert
            // ctx.moveTo(413, 830)
            // ctx.lineTo(413, 1350)
            let drawElectronY3_25 = electronY(412, 830, 412, 1350, 2, 12, 2, 18)
            let drawElectronY3_26 = electronY(412, 830, 412, 1350, 2, 15, 2, 147)
            let drawElectronY3_27 = electronY(412, 830, 412, 1350, 2, 8, 2, 187)
            let drawElectronY3_28 = electronY(412, 830, 412, 1350, 2, 12, 2, 269)
            let drawElectronY3_29 = electronY(412, 830, 412, 1350, 2, 15, 2, 374)
            let drawElectronY3_30 = electronY(412, 830, 412, 1350, 2, 8, 2, 515)
            //
            // //7 vertical line
            // //7angle
            // ctx.moveTo(519, 800)
            // ctx.lineTo(489, 830)
            let drawElectronXY3_10 = electronXY(519, 799, 489, 829, 2, 2, 9)
            // //7vert
            // ctx.moveTo(489, 830)
            // ctx.lineTo(489, 1350)
            let drawElectronY3_31 = electronY(488, 830, 488, 1350, 2, 12, 2, 13)
            let drawElectronY3_32 = electronY(488, 830, 488, 1350, 2, 15, 2, 138)
            let drawElectronY3_33 = electronY(488, 830, 488, 1350, 2, 8, 2, 169)
            let drawElectronY3_34 = electronY(488, 830, 488, 1350, 2, 12, 2, 249)
            let drawElectronY3_35 = electronY(488, 830, 488, 1350, 2, 15, 2, 364)
            let drawElectronY3_36 = electronY(488, 830, 488, 1350, 2, 8, 2, 495)

            //
            // //8 vertical line
            // //8angle
            // ctx.moveTo(595, 800)
            // ctx.lineTo(565, 830)
            let drawElectronXY3_11 = electronXY(594, 799, 564, 829, 2, 2, 17)

            // //8vert
            // ctx.moveTo(565, 830)
            // ctx.lineTo(565, 1350)
            let drawElectronY3_37 = electronY(564, 830, 564, 1350, 2, 10, 2, 23)
            let drawElectronY3_38 = electronY(564, 830, 564, 1350, 2, 15, 2, 168)
            let drawElectronY3_39 = electronY(564, 830, 564, 1350, 2, 8, 2, 199)
            let drawElectronY3_40 = electronY(564, 830, 564, 1350, 2, 12, 2, 229)
            let drawElectronY3_41 = electronY(564, 830, 564, 1350, 2, 15, 2, 354)
            let drawElectronY3_42 = electronY(564, 830, 564, 1350, 2, 18, 2, 485)

            //
            // //9 vertical line
            // //9angle
            // ctx.moveTo(671, 800)
            // ctx.lineTo(641, 830)
            let drawElectronXY3_12 = electronXY(671, 799, 641, 829, 2, 2, 11)
            // //9vert
            // ctx.moveTo(641, 830)
            // ctx.lineTo(641, 1350)
            let drawElectronY3_43 = electronY(640, 830, 640, 1350, 2, 10, 2, 23)
            let drawElectronY3_44 = electronY(640, 830, 640, 1350, 2, 15, 2, 168)
            let drawElectronY3_45 = electronY(640, 830, 640, 1350, 2, 8, 2, 299)
            let drawElectronY3_46 = electronY(640, 830, 640, 1350, 2, 12, 2, 329)
            let drawElectronY3_47 = electronY(640, 830, 640, 1350, 2, 15, 2, 454)
            let drawElectronY3_48 = electronY(640, 830, 640, 1350, 2, 18, 2, 555)
            //
            // //10 vertical line
            // //10angle
            // ctx.moveTo(747, 800)
            // ctx.lineTo(717, 830)
            let drawElectronXY3_13 = electronXY(746, 799, 716, 829)
            // //10vert
            // ctx.moveTo(717, 830)
            // ctx.lineTo(717, 1350)
            let drawElectronY3_49 = electronY(716, 830, 716, 1350, 2, 10, 2, 3)
            let drawElectronY3_50 = electronY(716, 830, 716, 1350, 2, 15, 2, 178)
            let drawElectronY3_51 = electronY(716, 830, 716, 1350, 2, 8, 2, 289)
            let drawElectronY3_52 = electronY(716, 830, 716, 1350, 2, 12, 2, 359)
            let drawElectronY3_53 = electronY(716, 830, 716, 1350, 2, 15, 2, 464)
            let drawElectronY3_54 = electronY(716, 830, 716, 1350, 2, 18, 2, 565)
            //
            // //11 vertical line
            // //11angle
            // ctx.moveTo(823, 800)
            // ctx.lineTo(793, 830)
            let drawElectronXY3_14 = electronXY(822, 799, 792, 829)
            // //11vert
            // ctx.moveTo(793, 830)
            // ctx.lineTo(793, 1350)
            let drawElectronY3_55 = electronY(792, 830, 792, 1350, 2, 10, 2, 5)
            let drawElectronY3_56 = electronY(792, 830, 792, 1350, 2, 15, 2, 158)
            let drawElectronY3_57 = electronY(792, 830, 792, 1350, 2, 8, 2, 299)
            let drawElectronY3_58 = electronY(792, 830, 792, 1350, 2, 12, 2, 399)
            let drawElectronY3_59 = electronY(792, 830, 792, 1350, 2, 15, 2, 474)
            let drawElectronY3_60 = electronY(792, 830, 792, 1350, 2, 18, 2, 575)
            //
            // //12 vertical line
            // //12angl9
            // ctx.moveTo(899, 800)
            // ctx.lineTo(869, 830)
            let drawElectronXY3_15 = electronXY(822, 799, 792, 829)
            // //12vert
            // ctx.moveTo(869, 830)
            // ctx.lineTo(869, 1350)
            let drawElectronY3_61 = electronY(868, 830, 868, 1350, 2, 10, 2, 7)
            let drawElectronY3_62 = electronY(868, 830, 868, 1350, 2, 15, 2, 138)
            let drawElectronY3_63 = electronY(868, 830, 868, 1350, 2, 8, 2, 309)
            let drawElectronY3_64 = electronY(868, 830, 868, 1350, 2, 12, 2, 399)
            let drawElectronY3_65 = electronY(868, 830, 868, 1350, 2, 15, 2, 487)
            let drawElectronY3_66 = electronY(868, 830, 868, 1350, 2, 18, 2, 564)
            //
            // //13 vertical line
            // //13angle
            // ctx.moveTo(975, 800)
            // ctx.lineTo(945, 830)
            let drawElectronXY3_16 = electronXY(974, 799, 944, 829)
            // //13vert
            // ctx.moveTo(945, 830)
            // ctx.lineTo(945, 1350)
            let drawElectronY3_67 = electronY(944, 830, 944, 1350, 2, 10, 2, 7)
            let drawElectronY3_68 = electronY(944, 830, 944, 1350, 2, 15, 2, 178)
            let drawElectronY3_69 = electronY(944, 830, 944, 1350, 2, 8, 2, 379)
            let drawElectronY3_70 = electronY(944, 830, 944, 1350, 2, 12, 2, 499)
            let drawElectronY3_71 = electronY(944, 830, 944, 1350, 2, 15, 2, 517)
            let drawElectronY3_72 = electronY(944, 830, 944, 1350, 2, 18, 2, 569)
            //
            // //14 vertical line
            // //14angle
            // ctx.moveTo(1050, 790)
            // ctx.lineTo(1021, 820)

            // //14vert
            // ctx.moveTo(1021, 820)
            // ctx.lineTo(1021, 1250)
            let drawElectronY3_73 = electronY(1020, 830, 1020, 1250, 2, 10, 2, 5)
            let drawElectronY3_74 = electronY(1020, 830, 1020, 1250, 2, 15, 2, 188)
            let drawElectronY3_75 = electronY(1020, 830, 1020, 1250, 2, 8, 2, 389)
            let drawElectronY3_76 = electronY(1020, 830, 1020, 1250, 2, 12, 2, 489)
            let drawElectronY3_77 = electronY(1020, 830, 1020, 1250, 2, 15, 2, 527)
            let drawElectronY3_78 = electronY(1020, 830, 1020, 1250, 2, 18, 2, 549)


            function drawSchema() {

                ctx.beginPath();

                ctx.lineWidth = 3;

                ctx.strokeStyle = '#292939';
                for (var i = 1; i <= 4; i++) {
                    ctx.moveTo(180, (165 + (i * 15)));
                    ctx.lineTo(240, (165 + (i * 15)));
                }


                //lines between sertificate and video


                //lines after video

                //top line
                //horizontal 1
                const topLine_h1_x_start = 415
                const topLine_h1_x_end = 1120
                const topLine_h1_y_start = 45
                const topLine_h1_y_end = 45

                ctx.moveTo(topLine_h1_x_start, topLine_h1_y_start)
                ctx.lineTo(topLine_h1_x_end, topLine_h1_y_start)


                //vertical1
                const topLine_v1_x_start = 1120
                const topLine_v1_x_end = 1160
                const topLine_v1_y_start = 45
                const topLine_v1_y_end = 270

                ctx.moveTo(topLine_v1_x_start, topLine_v1_y_start)
                ctx.lineTo(topLine_v1_x_start, topLine_v1_y_end)
                //angle
                ctx.moveTo(1120, 270)
                ctx.lineTo(1035, 360)
                //horizontal
                ctx.moveTo(1035, 360)
                ctx.lineTo(440, 360)
                //2angle
                ctx.moveTo(440, 360)
                ctx.lineTo(360, 440)
                //vertical
                ctx.moveTo(360, 440)
                ctx.lineTo(360, 460)
                //2horizontal
                ctx.moveTo(360, 460)
                ctx.lineTo(480, 460)


                //middle line
                ctx.moveTo(415, 130)
                ctx.lineTo(1100, 130)
                ctx.moveTo(1100, 130)
                ctx.lineTo(1100, 260)
                //angle
                ctx.moveTo(1100, 260)
                ctx.lineTo(1025, 340)
                //horizontal
                ctx.moveTo(1025, 340)
                ctx.lineTo(430, 340)
                //2angle
                ctx.moveTo(430, 340)
                ctx.lineTo(340, 430)
                //vertical
                ctx.moveTo(340, 430)
                ctx.lineTo(340, 480)
                //2horizontal
                ctx.moveTo(340, 480)
                ctx.lineTo(480, 480)


                //bottom line
                ctx.moveTo(415, 225)
                ctx.lineTo(1080, 225)
                ctx.moveTo(1080, 225)
                ctx.lineTo(1080, 250)
                //angle
                ctx.moveTo(1080, 250)
                ctx.lineTo(1010, 320)
                //horizontal
                ctx.moveTo(1010, 320)
                ctx.lineTo(420, 320)
                //2angle
                ctx.moveTo(420, 320)
                ctx.lineTo(320, 420)
                //vertical
                ctx.moveTo(320, 420)
                ctx.lineTo(320, 500)
                //2horizontal
                ctx.moveTo(320, 500)
                ctx.lineTo(480, 500)


                //after sertificat lines
                //top
                ctx.moveTo(660, 600)
                ctx.lineTo(1120, 600)
                //vertical
                ctx.moveTo(1120, 600)
                ctx.lineTo(1120, 720)
                //angle
                ctx.moveTo(1120, 720)
                ctx.lineTo(1040, 800)
                //horizontal
                ctx.moveTo(1040, 800)
                ctx.lineTo(215, 800)
                //2angle
                ctx.moveTo(215, 800)
                ctx.lineTo(185, 830)
                //2vertical
                ctx.moveTo(185, 830)
                ctx.lineTo(185, 1350)


                //middle
                ctx.moveTo(660, 620)
                ctx.lineTo(1100, 620)
                //vertical
                ctx.moveTo(1100, 620)
                ctx.lineTo(1100, 710)
                //angle
                ctx.moveTo(1100, 710)
                ctx.lineTo(1030, 780)
                //horizontal
                ctx.moveTo(1030, 780)
                ctx.lineTo(160, 780)
                //2angle
                ctx.moveTo(160, 780)
                ctx.lineTo(110, 830)
                //2vertical
                ctx.moveTo(110, 830)
                ctx.lineTo(110, 1350)


                //bottom
                ctx.moveTo(660, 640)
                ctx.lineTo(1080, 640)
                //vertical
                ctx.moveTo(1080, 640)
                ctx.lineTo(1080, 700)
                //angle
                ctx.moveTo(1080, 700)
                ctx.lineTo(1020, 760)
                //horizontal
                ctx.moveTo(1020, 760)
                ctx.lineTo(105, 760)
                //2angle
                ctx.moveTo(105, 760)
                ctx.lineTo(35, 830)
                //2vertical
                ctx.moveTo(35, 830)
                ctx.lineTo(35, 1550)

                //4 vertical line
                //4angle
                ctx.moveTo(291, 800)
                ctx.lineTo(261, 830)
                //4vert
                ctx.moveTo(261, 830)
                ctx.lineTo(261, 1350)

                //5 vertical line
                //5angle
                ctx.moveTo(367, 800)
                ctx.lineTo(337, 830)
                //5vert
                ctx.moveTo(337, 830)
                ctx.lineTo(337, 1350)

                //6 vertical line
                //6angle
                ctx.moveTo(443, 800)
                ctx.lineTo(413, 830)
                //6vert
                ctx.moveTo(413, 830)
                ctx.lineTo(413, 1350)

                //7 vertical line
                //7angle
                ctx.moveTo(519, 800)
                ctx.lineTo(489, 830)
                //7vert
                ctx.moveTo(489, 830)
                ctx.lineTo(489, 1350)

                //8 vertical line
                //8angle
                ctx.moveTo(595, 800)
                ctx.lineTo(565, 830)
                //8vert
                ctx.moveTo(565, 830)
                ctx.lineTo(565, 1350)

                //9 vertical line
                //9angle
                ctx.moveTo(671, 800)
                ctx.lineTo(641, 830)
                //9vert
                ctx.moveTo(641, 830)
                ctx.lineTo(641, 1350)

                //10 vertical line
                //10angle
                ctx.moveTo(747, 800)
                ctx.lineTo(717, 830)
                //10vert
                ctx.moveTo(717, 830)
                ctx.lineTo(717, 1350)

                //11 vertical line
                //11angle
                ctx.moveTo(823, 800)
                ctx.lineTo(793, 830)
                //11vert
                ctx.moveTo(793, 830)
                ctx.lineTo(793, 1350)

                //12 vertical line
                //12angl9
                ctx.moveTo(899, 800)
                ctx.lineTo(869, 830)
                //12vert
                ctx.moveTo(869, 830)
                ctx.lineTo(869, 1350)

                //13 vertical line
                //13angle
                ctx.moveTo(975, 800)
                ctx.lineTo(945, 830)
                //13vert
                ctx.moveTo(945, 830)
                ctx.lineTo(945, 1350)

                //14 vertical line
                //14angle
                ctx.moveTo(1050, 790)
                ctx.lineTo(1021, 820)
                //14vert
                ctx.moveTo(1021, 820)
                ctx.lineTo(1021, 1250)


                ctx.stroke();

            }


            function drawFrame() {

                // Очистить холст
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                drawSchema();
                ctx.beginPath();
                //top line
                drawElectronX1()
                drawElectronX1_1()
                drawElectronX1_2()
                drawElectronX1_3()
                drawElectronX1_4()
                drawElectronX1_5()
                drawElectronX1_6()
                drawElectronX1_7()
                drawElectronX1_8()
                drawElectronX1_9()
                drawElectronY1()
                drawElectronY1_1()
                drawElectronY1_2()
                drawElectronY1_3()
                drawElectronXY1_1()
                drawElectronXY1_2()
                drawElectronXY1_3()
                drawElectronX_top_reverse_1()
                drawElectronX_top_reverse_2()
                drawElectronX_top_reverse_3()
                drawElectronX_top_reverse_4()
                drawElectronX_top_reverse_5()
                drawElectronX_top_reverse_6()
                drawElectronX_top_reverse_7()
                drawElectronX_top_reverse_8()
                drawElectronX_top_reverse_9()
                drawElectronX_top_reverse_10()
                drawElectronX_top_reverse_11()
                drawElectronXY2_top_1()
                drawElectronXY2_top_2()
                drawElectronY1_4()
                drawElectronX1_10()
                drawElectronX1_11()
                drawElectronX1_12()
                drawElectronX1_13()
                drawElectronX1_14()
                drawElectronX1_15()
                drawElectronX1_16()
                drawElectronX1_17()
                drawElectronX1_18()
                drawElectronY1_5()
                drawElectronY1_6()
                drawElectronY1_7()
                drawElectronXY2_top_3()
                drawElectronXY2_top_4()
                drawElectronX_top_reverse_12()
                drawElectronX_top_reverse_13()
                drawElectronX_top_reverse_14()
                drawElectronX_top_reverse_15()
                drawElectronX_top_reverse_16()
                drawElectronX_top_reverse_17()
                drawElectronX_top_reverse_18()
                drawElectronX_top_reverse_19()
                drawElectronX_top_reverse_20()
                drawElectronX_top_reverse_21()
                drawElectronX_top_reverse_22()
                drawElectronXY2_top_5()
                drawElectronY1_8()
                drawElectronY1_9()
                drawElectronY1_10()
                drawElectronY1_11()
                drawElectronY1_12()
                drawElectronY1_13()


                //middle line
                drawElectronX2()
                drawElectronX2_1()
                drawElectronX2_2()
                drawElectronX2_3()
                drawElectronX2_4()
                drawElectronX2_5()
                drawElectronX2_6()
                drawElectronX2_7()
                drawElectronX2_8()
                drawElectronX2_9()
                drawElectronY2()
                drawElectronY2_1()
                drawElectronY2_2()
                drawElectronY2_3()
                drawElectronXY2_1()
                drawElectronXY2_2()
                drawElectronXY2_3()
                drawElectronX_middle_reverse_1()
                drawElectronX_middle_reverse_2()
                drawElectronX_middle_reverse_3()
                drawElectronX_middle_reverse_4()
                drawElectronX_middle_reverse_5()
                drawElectronX_middle_reverse_6()
                drawElectronX_middle_reverse_7()
                drawElectronX_middle_reverse_8()
                drawElectronX_middle_reverse_9()
                drawElectronX_middle_reverse_10()
                drawElectronX_middle_reverse_11()
                drawElectronXY2_4()
                drawElectronY2_4()
                drawElectronY2_5()
                drawElectronX2_10()
                drawElectronX2_11()
                drawElectronX2_12()
                drawElectronX2_13()
                drawElectronX2_14()
                drawElectronX2_15()
                drawElectronX2_16()
                drawElectronX2_17()
                drawElectronX2_18()
                drawElectronY2_6()
                drawElectronY2_7()
                drawElectronY2_8()
                drawElectronXY2_5()
                drawElectronX_middle_reverse_12()
                drawElectronX_middle_reverse_13()
                drawElectronX_middle_reverse_14()
                drawElectronX_middle_reverse_15()
                drawElectronX_middle_reverse_16()
                drawElectronX_middle_reverse_17()
                drawElectronX_middle_reverse_18()
                drawElectronX_middle_reverse_19()
                drawElectronX_middle_reverse_20()
                drawElectronX_middle_reverse_21()
                drawElectronX_middle_reverse_22()
                drawElectronX_middle_reverse_23()
                drawElectronXY2_6()
                drawElectronY2_9()
                drawElectronY2_10()
                drawElectronY2_11()
                drawElectronY2_12()
                drawElectronY2_13()
                drawElectronY2_14()


                //bottom line
                drawElectronX3_01()
                drawElectronX3_02()
                drawElectronX3_03()
                drawElectronX3()
                drawElectronX3_1()
                drawElectronX3_2()
                drawElectronX3_3()
                drawElectronX3_4()
                drawElectronX3_5()
                drawElectronX3_6()
                drawElectronX3_7()
                drawElectronX3_8()
                drawElectronX3_9()
                drawElectronX3_10()
                drawElectronX3_11()
                drawElectronY3()
                drawElectronXY3_1()
                drawElectronXY3_2()
                drawElectronXY3_3()
                drawElectronX_bottom_reverse_1()
                drawElectronX_bottom_reverse_2()
                drawElectronX_bottom_reverse_3()
                drawElectronX_bottom_reverse_4()
                drawElectronX_bottom_reverse_5()
                drawElectronX_bottom_reverse_6()
                drawElectronX_bottom_reverse_7()
                drawElectronX_bottom_reverse_8()
                drawElectronX_bottom_reverse_9()
                drawElectronX_bottom_reverse_10()
                drawElectronX_bottom_reverse_11()
                drawElectronXY3_4()
                drawElectronY3_1()
                drawElectronY3_2()
                drawElectronY3_3()
                drawElectronX3_12()
                drawElectronX3_13()
                drawElectronX3_14()
                drawElectronX3_15()
                drawElectronX3_16()
                drawElectronX3_17()
                drawElectronX3_18()
                drawElectronX3_19()
                drawElectronX3_20()
                drawElectronY3_4()
                drawElectronY3_5()
                drawElectronY3_6()
                drawElectronXY3_5()
                drawElectronX_bottom_reverse_12()
                drawElectronX_bottom_reverse_13()
                drawElectronX_bottom_reverse_14()
                drawElectronX_bottom_reverse_15()
                drawElectronX_bottom_reverse_16()
                drawElectronX_bottom_reverse_17()
                drawElectronX_bottom_reverse_18()
                drawElectronX_bottom_reverse_19()
                drawElectronX_bottom_reverse_20()
                drawElectronX_bottom_reverse_21()
                drawElectronX_bottom_reverse_22()
                drawElectronX_bottom_reverse_23()
                drawElectronX_bottom_reverse_24()
                drawElectronX_bottom_reverse_25()
                drawElectronXY3_6()
                drawElectronY3_7()
                drawElectronY3_8()
                drawElectronY3_9()
                drawElectronY3_10()
                drawElectronY3_11()
                drawElectronY3_12()

                //angles to flaggs
                //4
                drawElectronXY3_7()
                //5
                drawElectronXY3_8()
                //6
                drawElectronXY3_9()
                //7
                drawElectronXY3_10()
                //8
                drawElectronXY3_11()
                //9
                drawElectronXY3_12()
                //10
                drawElectronXY3_13()
                //11
                drawElectronXY3_14()
                //12
                drawElectronXY3_15()
                //13
                drawElectronXY3_16()


                //vert throught flags
                //4
                drawElectronY3_13()
                drawElectronY3_14()
                drawElectronY3_15()
                drawElectronY3_16()
                drawElectronY3_17()
                drawElectronY3_18()
                //5
                drawElectronY3_19()
                drawElectronY3_20()
                drawElectronY3_21()
                drawElectronY3_22()
                drawElectronY3_23()
                drawElectronY3_24()
                //6
                drawElectronY3_25()
                drawElectronY3_26()
                drawElectronY3_27()
                drawElectronY3_28()
                drawElectronY3_29()
                drawElectronY3_30()
                //7
                drawElectronY3_31()
                drawElectronY3_32()
                drawElectronY3_33()
                drawElectronY3_34()
                drawElectronY3_35()
                drawElectronY3_36()

                //8
                drawElectronY3_37()
                drawElectronY3_38()
                drawElectronY3_39()
                drawElectronY3_40()
                drawElectronY3_41()
                drawElectronY3_42()

                //9
                drawElectronY3_43()
                drawElectronY3_44()
                drawElectronY3_45()
                drawElectronY3_46()
                drawElectronY3_47()
                drawElectronY3_48()
                //10
                drawElectronY3_49()
                drawElectronY3_50()
                drawElectronY3_51()
                drawElectronY3_52()
                drawElectronY3_53()
                drawElectronY3_54()
                //11
                drawElectronY3_55()
                drawElectronY3_56()
                drawElectronY3_57()
                drawElectronY3_58()
                drawElectronY3_59()
                drawElectronY3_60()
                //12
                drawElectronY3_61()
                drawElectronY3_62()
                drawElectronY3_63()
                drawElectronY3_64()
                drawElectronY3_65()
                drawElectronY3_66()
                //13
                drawElectronY3_67()
                drawElectronY3_68()
                drawElectronY3_69()
                drawElectronY3_70()
                drawElectronY3_71()
                drawElectronY3_72()
                //14
                drawElectronY3_73()
                drawElectronY3_74()
                drawElectronY3_75()
                drawElectronY3_76()
                drawElectronY3_77()
                drawElectronY3_78()


                ctx.stroke();

            }


            // Рисуем следующий кадр через 20 миллисекунд
            let refresh = setInterval(drawFrame, 20);

        }
    }


</script>

<style scoped lang="scss">

    #canvas {
        position: absolute;
        z-index: -1;
    }

    .play-video-btn {
        display: block;
        padding: 0;
        background: #25417c;
        border: 1px solid #347dfe;
        border-radius: 50%;
        cursor: pointer;
        position: relative;

        z-index: 10;
        width: 46px;
        height: 46px;
        outline: 0;
        opacity: 0.9;
        color: #fff;

        &:before {
            content: "";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            display: none;
            width: calc(100% - 10px);
            height: calc(100% - 10px);
            background: #347dfe;
            border-radius: 50%;
            z-index: -1;
        }

        &:hover:before {
            display: block;
        }

        svg {
            position: absolute;
            top: 50%;
            left: 47%;
            transform: translate(-50%, -50%);

        }
    }

    .section-patents {
        margin-top: 100px;
        margin-bottom: 0;
    }

    .patent-container {
        height: 300px;
        display: flex;
        margin-top: 16px;
    }

    .wipo-container {
        display: flex;
        margin-top: 120px;
    }

    .patent-countries {
        margin-top: 100px;
    }

    .patent-text {
        width: 420px;

        p {
            margin-top: 24px;
            font-style: normal;
            font-weight: 500;
            font-size: 15px;
            line-height: 18px;
        }
    }

    .wipo-logo {
        height: 130px;
    }

    .preview {
        display: block;
        //width: 100%;
        max-width: 186px;
        cursor: pointer;

        animation-name: pulse;
        animation-duration: 1s;
        animation-timing-function: ease-out;
        animation-delay: 0s;
        animation-direction: alternate;
        animation-iteration-count: infinite;
        animation-fill-mode: none;
        animation-play-state: running;
    }

    @keyframes pulse {
        0% {
            box-shadow: 0px 0px 15px 4px rgba(86, 92, 135, 0);
        }
        100% {
            box-shadow: 0px 0px 15px 4px rgba(86, 92, 135, 1);
        }
    }

    .patent-item {
        margin-right: 50px;
        min-width: 186px;
    }

    .video-block {
        display: flex;
        flex-direction: column;

        .video-container {
            margin-bottom: 10px;
            display: flex;
        }

        .video-play-button {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 82px;
            width: 82px;
            background-color: #253866;
            border-radius: 5px;
            margin-right: 5px;
        }

        .video-label {
            display: flex;
            align-items: center;
            background-color: #FFFFFF;
            border-radius: 5px;
            width: 455px;
            height: 82px;

            .icon {
                width: 90px;
                display: flex;
                justify-content: center;
                align-items: center;
                margin-right: 30px;

                img {
                    height: 60px;
                }
            }

            .video-title {
                max-width: 275px;
                display: block;
                color: #0f1222;
                font-weight: 600;

            }
        }

    }

    .patent-item1 {
        margin: auto;
        display: flex;
        flex-direction: column;

        span {
            text-align: center;
        }

        img {
            height: 270px;
            margin-bottom: 15px;
        }
    }

    .proposals-container {
        margin-top: 100px;
    }

    .flags-container {
        display: flex;
        flex-wrap: wrap;
        padding-bottom: 26px;

        .flag-item {
            width: 66px;
            height: 82px;
            background: #29283a;
            text-align: center;
            border-radius: 4px;
            cursor: pointer;
            margin-bottom: 10px;
            margin-right: 10px;

            .flag {
                padding: 1px;
                width: calc(100% - 2px);
                height: 60%;
            }

            .name {
                font-size: 9px;
                margin-top: 3px;
            }
        }
    }
</style>