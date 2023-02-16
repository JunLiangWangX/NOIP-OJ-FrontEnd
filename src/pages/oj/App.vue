<!--
 * @Description: 
 * @Author: JunLiangWang
 * @Date: 2023-02-11 10:35:53
 * @LastEditors: JunLiangWang
 * @LastEditTime: 2023-02-16 15:04:47
-->
<template>
  <div>
    <NavBar :oprity="oprity"></NavBar>
    <div class="content-app" ref="content" @scroll="scrollDs">
      <transition name="fadeInUp" mode="out-in">
        <router-view></router-view>
      </transition>
      <div class="footer">
        <p v-html="website.website_footer"></p>
        <p>Powered by 源码风暴
          <span v-if="version">&nbsp; Version: {{ version }}</span>
        </p>
      </div>
    </div>
    <BackTop></BackTop>
  </div>
</template>

<script>
import { mapActions, mapState } from 'vuex'
import NavBar from '@oj/components/NavBar.vue'

export default {
  name: 'app',
  components: {
    NavBar
  },
  data() {
    return {
      version: process.env.VERSION,
      oprity: 0
    }
  },
  created() {
    try {
      document.body.removeChild(document.getElementById('app-loader'))
    } catch (e) {
    }
  },
  mounted() {
    this.getWebsiteConfig()
  },
  methods: {
    ...mapActions(['getWebsiteConfig', 'changeDomTitle']),
    scrollDs() {
      let scrollTop = this.$refs['content'].scrollTop
      if (scrollTop < 100) {
        this.oprity = scrollTop / 100.0
      }
      else {
        this.oprity = 1
      }
    }
  },
  computed: {
    ...mapState(['website'])
  },
  watch: {
    'website'() {
      this.changeDomTitle()
    },
    '$route'() {
      this.changeDomTitle()
      this.$refs['content'].scrollTo({ top: 0, behavior: 'auto' });
    }
  }
}
</script>

<style lang="less">
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

a {
  text-decoration: none;
  background-color: transparent;

  &:active,
  &:hover {
    outline-width: 0;
  }
}

.content-app {
  overflow: auto;
  position: absolute;
  right: 0;
  left: 0;
  bottom: 0;
  top: 0;
}


@media screen and (max-width: 1200px) {
  .content-app {}
}

@media screen and (min-width: 1200px) {
  .content-app {}
}

.footer {
  margin-top: 20px;
  margin-bottom: 10px;
  text-align: center;
  font-size: small;
}

.fadeInUp-enter-active {
  animation: fadeInUp .8s;
}
</style>
