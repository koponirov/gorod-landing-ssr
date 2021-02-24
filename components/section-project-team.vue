<template lang="pug">
section.section-team(id="section-team")
  div.container
    h2.title(v-html="$t('teamTitle')")
    div.members-container
      project-team

</template>

<script>
import ProjectTeam from './ProjectTeam'

export default {
    components: {
      ProjectTeam,
    }
}
</script>

<style lang="scss" scoped>

.section-team {
    margin-bottom: 50px;

  > .container {
    > .title {
      margin-bottom: 28px;
    }
  }
}

</style>
