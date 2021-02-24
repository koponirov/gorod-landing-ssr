<template lang="pug">
  .level
    img.level-image(src="../../../src/assets/img/gorod-levels/gorod-3-level.png" alt="gorod-level-3")
    .view-details3_top
    .view-details3_left
    .view-details3_right
    .line3
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

.view-details3_top {
  position: absolute;
  top: 0;
  left: -74px;
  width: 120px;
  height: 120px;
  background-image: url("../../../src/assets/img/gorod-levels/gorod-3-level-detailed-top.png");
}
.view-details3_left {
  position: absolute;
  top: 123px;
  left: -143px;
  width: 120px;
  height: 120px;
  background-image: url("../../../src/assets/img/gorod-levels/gorod-3-level-detailed-left.png");
}
.view-details3_right {
  position: absolute;
  top: 123px;
  left: 0;
  width: 120px;
  height: 120px;
  background-image: url("../../assets/img/gorod-levels/gorod-3-level-detailed-right.png");
}
.line3 {
  @include line(-169.5deg,227px,112px,260px)
}

</style>