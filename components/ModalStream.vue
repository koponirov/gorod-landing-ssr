<template>
  <transition name="modal-stream">
    <div class="modal-mask" @touchmove.self="$emit('close')" @click.self="$emit('close')">

        <div class="modal-container" :style="st" :class="sz">
            <div class="header">
                <span v-if="!$slots['header']"></span>
                <slot name="header"></slot>
            </div>

            <div class="body">
                <slot>
                default body
                </slot>
            </div>

            <slot name="footer">
            </slot>
        </div>

    </div>
  </transition>
</template>

<script>

export default {
  name: 'ModalStream',
  props: {
      st: {
         default() {return {}}
      },
      h: {
          default: 0
      },
      sz: {
          default: ''
      }
  },
  data() {
    return {
      showModal: false
    }
  }
}
</script>

<style lang="scss" scoped>
.modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .5);
    display: flex;
    transition: opacity .3s ease;
}

.modal-container {
    position: relative;
    margin: auto;
    transition: all .3s ease;
    background: #29283A;
    padding: 0 5px;
    border-radius: 2px;
    width: 476px;
    height: 100%;
    &.wide {
        width: 890px;
        height: 700px;
    }
    max-height: 788px;
    @media screen and (orientation: portrait) {
        width: 80%;
        height: unset;
        max-height: 100vh;
        &.wide {
            width: 75%;
            height: unset;
            max-height: 100vh;
        }
    }
    overflow: auto;
}

.header {
    position: relative;
    min-height: 56px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 5px;
}

.close {
    width: 15px;
    height: 15px;
}
.body {
  width: 100%;
}

.footer {
    position: relative;
}

.modal-enter {
    opacity: 0;

}

.modal-leave-active {
    opacity: 0;
}

.modal-enter .modal-container {
    transform: scale(.5);
}
.modal-leave-active .modal-container{
    transform: scale(1.25);
}
</style>
