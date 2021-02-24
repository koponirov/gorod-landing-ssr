<template lang="pug">

  div.member-block(@click="changeIdx" )

    div.img-wrapper
      img.member-preview-img(:src="item.avatar" alt="team member avatar")

    div.member-info
      div
        h3.member-title {{item.name}}
        p.member-position {{item.position}}
        p.member-crop-desc(v-if="item.crop_description") {{item.crop_description }}
      a.member-link {{ $t('about') }}

</template>

<script>


export default {

  name: "MemberCard",
  props: ["item", "index"],
  methods: {
    changeIdx() {
      this.$emit('change-idx', this.index);
    }
  }
}
</script>

<style scoped lang="scss">

.member-block {
  width: 260px;
  border-radius: 5px;
  //background-color: #1b1a28;
  background: rgba(46, 48, 63, 0.3);
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: background-color 50ms ease-in-out;
  margin: 5px 15px 5px 10px;
  padding: 5px;
  cursor: pointer;

  .img-wrapper {
    overflow: hidden;
    position: relative;
    width: 100%;
    height: 330px;
    border-radius: 5px;

    .member-preview-img {
      height: 100%;
      width: 100%;
      object-fit: cover;
    }
  }

  .member-info {
    margin-bottom: 25px;
    margin-left: 5px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    width: 100%;

    > div {
      overflow: hidden;
      position: relative;

      .member-title {
        font-weight: bold;
        font-size: 20px;
        line-height: 24px;
        letter-spacing: -0.05em;
        margin-bottom: 10px;
      }

      .member-position {
        color: #8B8E9D;
        font-weight: 300;
        font-size: 18px;
        line-height: 22px;
        letter-spacing: -0.05em;
        margin-bottom: 28px;
      }

      .member-crop-desc {
        font-weight: 300;
        font-size: 15px;
        line-height: 18px;
        letter-spacing: -0.05em;
        height: 126px;
        color: #C7CBDE;
        margin: 5px 0 27px 0;
        overflow: hidden;
        position: relative;
      }

      .member-crop-desc:after {
        content: "";
        position: absolute;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 40px;
        background: linear-gradient(180deg, transparent, #1b1a28 50%);
      }
    }

    .member-link {
      font-weight: 300;
      font-size: 15px;
      line-height: 18px;
      letter-spacing: -0.05em;
      color: #347DFE;
    }
  }
}

.member-block:hover {
  background-color: #2f303f;

  > div {
    .member-crop-desc:after {
      background: linear-gradient(180deg, transparent, #2f303f 50%);
    }
  }
}

</style>
