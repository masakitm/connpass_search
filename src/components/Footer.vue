<template>
  <footer>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
    <div class="footer">
      <div class="copyright">
        @2017 Masaki Tomotsuka
      </div>
      <div class="sns">
        <a :href="github" target="_blank"><i class="fa-github"></i></a>
        <a :href="facebook" target="_blank"><i class="fa-facebook-official"></i></a>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  data: function () {
    return {
      github: 'https://github.com/masakitm/',
      facebook: 'https://www.facebook.com/pnk.mnmt'
    }
  }
}
</script>

<style lang="scss" scoped>
$black: #000000;
$navy: #4267b2;

a{
  text-decoration: none;
}

.footer{
  padding: 6rem 0;
}

.copyright{
  margin: 0 0 2rem 0;
}

i[class^="fa"] {
  font-style:normal;
  font-family: fontawesome;
  font-size: 2.5rem;
  margin:0 0.25rem;

  &.fa-github{
    color: $black;
  }

  &.fa-facebook-official{
    color: $navy;
  }
}

</style>
