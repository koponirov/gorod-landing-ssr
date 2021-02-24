<template lang="pug">
  .level
    img.level-image(src='../../../src/assets/img/gorod-levels/gorod-1-level (1).png' alt="gorod-level-1")
    .view-details1
    .line1
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


.view-details1 {
  position: absolute;
  top: 53px;
  left: -146px;
  width: 200px;
  height: 200px;
  transition-delay: 5s;
  background-image: url("../../../src/assets/img/gorod-levels/gorod-1-level-detailed.png");
}
.line1 {
  @include line(-168.69deg,227px,42px,400px)
}


</style>