<template>
  <transition name="modalTransit">
    <div class="modal" v-show="modalContSet">
      <div class="modal__bg" @click="emitModal()"></div>
      <div class="modal__content">
        <div v-html="modalContSet"></div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'Modal',
  props: ['modal-contents', 'modal-switch'],
  computed: {
    modalContSet () {
      return this.modalContents
    },
    modalSwitcher () {
      return this.modalSwitch
    }
  },
  methods: {
    emitModal: function () {
      this.$emit('modal-switch', false)
    }
  }
}
</script>

<style lang="scss" scoped>
*{
  box-sizing: border-box;
}
.modal{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  z-index:100;
  padding:3rem 5rem;
  word-break: break-all;

  &__bg{
    position: fixed;
    top: 0;
    left: 0;
    color: #000;
    background: rgba(255,255,255,0.9);
    width: 100%;
    height: 100%;
    z-index: -1;
  }
}

.modalTransit-enter-active, .modalTransit-leave-active {
  transition: opacity .5s
}
.modalTransit-enter, .modalTransit-leave-to{
  opacity: 0
}
</style>
