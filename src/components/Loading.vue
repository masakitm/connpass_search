<template>
  <transition name="loader">
    <div class="loading" v-show="isLoading">
      <div class="spinner">
        <div class="rect1"></div>
        <div class="rect2"></div>
        <div class="rect3"></div>
        <div class="rect4"></div>
        <div class="rect5"></div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'Loading',
  props: {
    loading: Boolean
  },
  computed: {
    isLoading: function () {
      return this.loading
    }
  }
}
</script>

<style lang="scss" scoped>
.loader-enter-active {
  animation: loader-in .5s;
}
.loader-leave-active {
  animation: loader-in.5s reverse;
}
@keyframes loader-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}

/* css loading */
.loading{
	background: rgba(255,255,255,0.9);
	position: fixed;
	top: 0;
	left: 0;
	width: 100vw;
	height: 100vh;
	z-index:101;
}
.spinner {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%,-50%);
  width: 50px;
  height: 40px;
  text-align: center;
  font-size: 10px;

  > div{
    background-color: #333;
    height: 100%;
    width: 6px;
    display: inline-block;
    -webkit-animation: sk-stretchdelay 1.2s infinite ease-in-out;
    animation: sk-stretchdelay 1.2s infinite ease-in-out;
  }

  .rect2 {
    -webkit-animation-delay: -1.1s;
    animation-delay: -1.1s;
  }

  .rect3 {
    -webkit-animation-delay: -1.0s;
    animation-delay: -1.0s;
  }

  .rect4 {
    -webkit-animation-delay: -0.9s;
    animation-delay: -0.9s;
  }

  .rect5 {
    -webkit-animation-delay: -0.8s;
    animation-delay: -0.8s;
  }
}

@-webkit-keyframes sk-stretchdelay {
  0%, 40%, 100% { -webkit-transform: scaleY(0.4) }
  20% { -webkit-transform: scaleY(1.0) }
}

@keyframes sk-stretchdelay {
  0%, 40%, 100% {
    transform: scaleY(0.4);
    -webkit-transform: scaleY(0.4);
  }  20% {
    transform: scaleY(1.0);
    -webkit-transform: scaleY(1.0);
  }
}
/* /css loading */

</style>
