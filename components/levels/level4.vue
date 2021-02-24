<template lang="pug">
  .level
    img.level-image(src="../../../src/assets/img/gorod-levels/gorod-4-level.png" alt="gorod-level-4")
    .view-details4_top
    .view-details4_left
    .view-details4_right
    .line4
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

.view-details4_top {
  position: absolute;
  top: 0;
  left: -74px;
  width: 120px;
  height: 120px;
  background-image: url("../../../src/assets/img/gorod-levels/gorod-4-level-detailed-top.png");
}
.view-details4_left {
  position: absolute;
  top: 123px;
  left: -143px;
  width: 120px;
  height: 120px;
  background-image: url("../../../src/assets/img/gorod-levels/gorod-4-level-detailed-left.png");
}
.view-details4_right {
  position: absolute;
  top: 123px;
  left: 0;
  width: 120px;
  height: 120px;
  background-image: url("../../assets/img/gorod-levels/gorod-4-level-detailed-right.png");
}
.line4 {
  @include line(-159.5deg,240px,110px,270px)
}

</style>