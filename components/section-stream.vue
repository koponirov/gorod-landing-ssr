<template lang="pug">
section.stream(ref="a")
    .container
        h2.title.title(v-html="$t('streamTitle')")
        //h3(v-html="$t('techwork')" style="textAlign: center")
        StreamGroup
</template>

<script>
import StreamGroup from './StreamGroup1'

export default {
    data(){
        return{
            //play:false,
        }
    },

    components:{
        StreamGroup,
    }
}
</script>
<style scoped>
.stream {
  margin-bottom: 50px;
}
</style>
