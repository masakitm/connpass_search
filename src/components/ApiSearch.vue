<template>
  <div>
    <Loading :loading="this.loading"></Loading>

    <h1>{{ msg }}</h1>

    <div>
      <div>
        <input type="text" @keyup.enter="getPosts(conpassApiUrl)" v-model="keyword">
        <select class="" name="" v-model="selectState" @change="getPosts(conpassApiUrl)">
          <option v-for="state in stateData" val="state.label">
            {{ state.label }}
          </option>
        </select>
      </div>

      <p>
        <button @click="getPosts(conpassApiUrl)">Search!</button>
      </p>

      <div class="resultInfo" v-show="available">
        検索結果  全 {{ available }} 件　
        {{ nowPage }} / {{ pageCount }}ページ
      </div>

      <div class="pagination">
        <a href="#" v-if="postStart > 0" @click.stop.prevent="paging('prev')">PREV</a>
        <a href="#" v-if="available - postStart > postCount" @click.stop.prevent="paging('next')">NEXT</a>
      </div>

      <div class="resultsWrap">
          <div class="resultsWrap__single" v-for="(item, index) in jsonData" @click.self="">

            <div class="date">
              {{ item.started_at }}.
            </div>

            <div class="title">
              <a :href="item.event_url" target="_blank">
                {{ item.title }}
              </a>
            </div>

            <div class="address">
              {{ item.address }}
            </div>

            <div class="">
              <a :href="item.gmapLink" target="_blank">
                <img class="mapImg" :src="item.gmapSrc" alt="">
              </a>
            </div>
          </div>
      </div>

      <div class="pagination">
        <a href="#" v-if="postStart > 0" @click.stop.prevent="paging('prev')">PREV</a>
        <a href="#" v-if="available - postStart > postCount" @click.stop.prevent="paging('next')">NEXT</a>
      </div>

    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import VueJsonp from 'vue-jsonp'
import Loading from './Loading'
const state = require('../state.json')
Vue.use(VueJsonp)

export default {
  name: 'ApiSearch',
  data () {
    return {
      asdf: true,
      msg: 'Connpass API検索',
      conpassApiUrl: 'https://connpass.com/api/v1/event/',
      keyword: 'vue',
      googleApiUrl: 'https://maps.googleapis.com/maps/api/staticmap',
      googleApiKey: 'AIzaSyBvMTD_s_4107jBVh-ouuaTs0FE1IlDxVU',
      jsonData: '',
      available: '',
      postStart: 0,
      postCount: 12,
      nowPage: 0 + 1,
      stateData: state,
      selectState: '東京都',
      loading: true
    }
  },
  mounted: function () {
    this.getPosts(this.conpassApiUrl)
  },
  computed: {
    pageCount: function () {
      return Math.ceil(this.available / this.postCount)
    }
  },
  methods: {
    getPosts (url, postStart) {
      const _this = this
      this.loading = true
      if (!postStart) {
        postStart = 0
      }

      // url sample https://connpass.com/api/v1/event/?order=2&start=0&keyword=vue.js
      this.$jsonp(url, { order: 2, start: postStart, keyword: this.keyword + ',' + this.selectState, count: this.postCount }).then(json => {
        // Success.
        this.loading = false
        this.available = json.results_available
        this.jsonData = json.events
        this.jsonData.map(function (value) {
          let gmapPlace
          if (value['lat'] && value['lon']) {
            gmapPlace = value['lat'] + ',' + value['lon']
          } else {
            gmapPlace = value['address']
          }
          value['started_at'] = value['started_at'].substring(0, value['started_at'].indexOf('T'))
          value['gmapSrc'] = _this.googleApiUrl + '?key=' + _this.googleApiKey + '&size=480x320&maptype=roadmap' + '&markers=color:red%7C' + gmapPlace
          value['gmapLink'] = 'https://www.google.co.jp/maps/place/' + value['address']
          return value
        })
      }).catch(err => {
        // Failed.
        console.log(err)
      })
    },
    paging (pushed, event) {
      if (pushed === 'prev') {
        this.nowPage--
        this.postStart = this.postStart - this.postCount
        this.getPosts(this.conpassApiUrl, this.postStart)
      } else if (pushed === 'next') {
        this.nowPage++
        this.postStart = this.postStart + this.postCount
        this.getPosts(this.conpassApiUrl, this.postStart)
      }
    }
  },
  components: {
    Loading
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
html,body{
  font-size:12px;
}

*{
  box-sizing: border-box;
}

h1, h2 {
  font-weight: normal;
}

h1{
  margin-bottom: 3rem;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
  font-weight:bold;
}


button{
  background: #42b983;
  border: none;
  color: #fff;
  font-size:1.5rem;
  padding: 0.5rem 2rem;
  cursor:pointer;
  border:1px solid  #42b983;
  transition: 0.2s;

  &:hover{
    color: #42b983;
    background: #fff;

  }
}


input{
  width: 35vw;
  display: inline-block;
  font-size: 1.2rem;
  border: 1px solid #ddd;
  padding: 10px 10px;
}

select{
  width: 35vw;
  font-size: 1rem;
  padding: 10px 10px;
  border-radius: 0;
  border: 1px solid #ddd;
  background: #fff;
  text-align: center;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  vertical-align: top;
  cursor:pointer;
}

p.subtit{
  margin: 1rem auto 0.5rem;
}

.resultInfo{
  margin: 2rem auto;
}

.resultsWrap{
  width:90vw;
  margin:0 auto;
  display:flex;
  flex-wrap:wrap;
  justify-content: space-around;

  &__single{
    position:relative;
    width:32%;
    max-width:480px;
    padding:2rem 1.5rem;
    border:1px solid #ddd;
    margin:1rem auto;

    .mapImg{
      width: 100%;
      height: auto;
    }

    .title{
      margin-bottom: 1rem;
    }

    .date{
      margin-bottom:1rem;
    }

    .address{
      font-size: 0.85rem;
      margin-bottom: 1rem;
    }
  }
}

.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active for below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}

.pagination{
  padding: 1rem 0;

  a{
    display: inline-block;
    margin: 0 0.5rem;
  }
}

</style>
