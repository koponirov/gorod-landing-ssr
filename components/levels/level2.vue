<template lang="pug">
  .level
    img.level-image(src='../../../src/assets/img/gorod-levels/gorod-2-level.png' alt="gorod-level-2")
    .view-details2
    .line2
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
@mixin line($value,$top,$left,$width) {
  position: absolute;
  border-bottom: 2px solid #FFFFFF;
  transform: rotate($value);
  top: $top;
  left: $left;
  width: $width;
}

.view-details2 {
  position: absolute;
  top: 53px;
  left: -146px;
  width: 200px;
  height: 200px;
  background-image: url("../../../src/assets/img/gorod-levels/gorod-2-level-detailed.png");
}
.line2 {
  @include line(-169.5deg,227px,41px,360px)
}


</style>