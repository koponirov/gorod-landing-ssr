<template lang="pug">
section.section-news
  div.container
    h2.title(v-html="$t('newsTitle')")

    div.articles
      h3(v-html="$t('newsArticles')")
      section-news-articles

    //div.videos
    //    h3(v-html="$t('newsVideos')")
    //    section-news-videos

    //div.skolkovo
    //  section-news-skolkovo

</template>

<script>
//import SectionNewsArticles from './16-section-news-articles'
import SectionNewsArticles from './16-section-news-articles'
//import SectionNewsVideos from './16-section-news-videos'
import SectionNewsSkolkovo from './16-section-news-skolkovo'

export default {
    components: {
        SectionNewsArticles, //: () => import(/* webpackChunkName: "sec-16-news-articles" */ './16-section-news-articles'),
        //SectionNewsVideos,//: () => import(/* webpackChunkName: "sec-16-news-videos" */'./16-section-news-videos')
        SectionNewsSkolkovo//: () => import(/* webpackChunkName: "sec-16-news-videos" */'./16-section-news-videos')
    }
}
</script>
