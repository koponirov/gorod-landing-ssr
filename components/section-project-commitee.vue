<template lang="pug">
section.section-committee
  div.container
    h2.title(v-html="$t('committeeTitle')")
    p.subtitle(v-html="$t('committeeAbout')")

    div.articles
      project-committee

</template>

<script>
import ProjectCommittee from "@/components/ProjectCommitteeLarge";

export default {
    components: {
      ProjectCommittee,
    }
}
</script>

<style lang="scss" scoped>

.section-committee {

  > .container {
    > .title {
      margin-bottom: 33px;
    }
    > .subtitle {
      margin-bottom: 69px;
    }

  }
}

</style>
