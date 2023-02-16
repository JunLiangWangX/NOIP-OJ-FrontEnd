<template>
  <div id="header" :style="'background: rgb(255, 255, 255,'+oprity+ ');box-shadow: 0px 2px 2px 0px rgb(232 229 229 / '+oprity+ ');'" >
    <Menu theme="light" mode="horizontal" @on-select="handleRoute" :active-name="activeMenu" class="oj-menu">
      <div class="logo">
        <img src="@/assets/logo.svg" />
        <p>{{ website.website_name }}</p>
      </div>
      <div class="center-container">
        <Menu-item name="/">
          <Icon type="home"></Icon>
          {{ $t('m.Home') }}
        </Menu-item>
        <Menu-item name="/problem">
          <Icon type="ios-keypad"></Icon>
          {{ $t('m.NavProblems') }}
        </Menu-item>
        <Menu-item name="/contest">
          <Icon type="trophy"></Icon>
          {{ $t('m.Contests') }}
        </Menu-item>
        <Menu-item name="/status">
          <Icon type="ios-pulse-strong"></Icon>
          {{ $t('m.NavStatus') }}
        </Menu-item>
        <Submenu name="rank">
          <template slot="title">
            <Icon type="podium"></Icon>
            {{ $t('m.Rank') }}
          </template>
          <Menu-item name="/acm-rank">
            {{ $t('m.ACM_Rank') }}
          </Menu-item>
          <Menu-item name="/oi-rank">
            {{ $t('m.OI_Rank') }}
          </Menu-item>
        </Submenu>
        <Submenu name="about">
          <template slot="title">
            <Icon type="information-circled"></Icon>
            {{ $t('m.About') }}
          </template>
          <Menu-item name="/about">
            {{ $t('m.Judger') }}
          </Menu-item>
          <Menu-item name="/FAQ">
            {{ $t('m.FAQ') }}
          </Menu-item>
        </Submenu>
      </div>
      <template v-if="!isAuthenticated">
        <div class="btn-menu">
          <Button type="ghost" class="main"  ref="loginBtn" shape="circle" @click="handleBtnClick('login')">{{ $t('m.Login') }}
          </Button>
          <Button  v-if="website.allow_register" type="ghost" shape="circle" @click="handleBtnClick('register')"
            style="margin-left: 5px;">{{ $t('m.Register') }}
          </Button>
        </div>
      </template>
      <template v-else>
        <Dropdown class="drop-menu" @on-click="handleRoute" placement="bottom" trigger="click">
          <Button type="text" class="drop-menu-title">{{ user.username }}
            <Icon type="arrow-down-b"></Icon>
          </Button>
          <Dropdown-menu slot="list">
            <Dropdown-item name="/user-home">{{ $t('m.MyHome') }}</Dropdown-item>
            <Dropdown-item name="/status?myself=1">{{ $t('m.MySubmissions') }}</Dropdown-item>
            <Dropdown-item name="/setting/profile">{{ $t('m.Settings') }}</Dropdown-item>
            <Dropdown-item v-if="isAdminRole" name="/admin">{{ $t('m.Management') }}</Dropdown-item>
            <Dropdown-item divided name="/logout">{{ $t('m.Logout') }}</Dropdown-item>
          </Dropdown-menu>
        </Dropdown>
      </template>
    </Menu>
    <Modal v-model="modalVisible" :width="400">
      <div slot="header" class="modal-title">{{ $t('m.Welcome_to') }} {{ website.website_name_shortcut }}</div>
      <component :is="modalStatus.mode" v-if="modalVisible"></component>
      <div slot="footer" style="display: none"></div>
    </Modal>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import login from '@oj/views/user/Login'
import register from '@oj/views/user/Register'

export default {
  components: {
    login,
    register
  },
  props:{
    oprity:{
      type:Number,
      default:0
    }
  },
  mounted() {
    this.getProfile()
  },
  methods: {
    ...mapActions(['getProfile', 'changeModalStatus']),
    handleRoute(route) {
      if (route && route.indexOf('admin') < 0) {
        this.$router.push(route)
      } else {
        window.open('/admin/')
      }
    },
    handleBtnClick(mode) {
      this.changeModalStatus({
        visible: true,
        mode: mode
      })
    }
  },
  computed: {
    ...mapGetters(['website', 'modalStatus', 'user', 'isAuthenticated', 'isAdminRole']),
    // 跟随路由变化
    activeMenu() {
      return '/' + this.$route.path.split('/')[1]
    },
    modalVisible: {
      get() {
        return this.modalStatus.visible
      },
      set(value) {
        this.changeModalStatus({ visible: value })
      }
    }
  }
}
</script>
<style lang="less">
#header .ivu-menu-item,
#header .ivu-menu-submenu {
  border: none !important;
}

#header .ivu-menu-horizontal.ivu-menu-light:after {
  content: '';
  display: block;
  width: 100%;
  height: 1px;
  background: transparent;
  position: absolute;
  bottom: 0;
  left: 0;
}
#header .ivu-menu-horizontal {
    height: 80px;
    line-height: 80px;
}
#header .ivu-menu-light.ivu-menu-horizontal .ivu-menu-item-active, .ivu-menu-light.ivu-menu-horizontal .ivu-menu-item:hover, .ivu-menu-light.ivu-menu-horizontal .ivu-menu-submenu-active, .ivu-menu-light.ivu-menu-horizontal .ivu-menu-submenu:hover {
    color: @primary-text-color;
    border-bottom: @primary-text-color;
}

#header .ivu-menu-item ,#header .ivu-menu-submenu-title{
    font-size: 17px;
    font-weight: 500;
}

#header .ivu-btn{
    width: 90px;
    font-size: 14px;
    background: white;
}
#header .drop-menu .ivu-btn{
    background: transparent;
}

#header .main{
  background: @primary-color;
  border-color: @primary-color;
  color: white;
}
</style>
<style lang="less" scoped>
#header {
  min-width: 300px;
  position: fixed;
  top: 0;
  left: 0;
  height: auto;
  width: 100%;
  z-index: 1000;
  padding: 0 4%;

  .oj-menu {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-between;
    border: none;
    background: #00000000;
  }

  .logo {
    margin-right: 2%;
    font-size: 20px;
    float: left;
    line-height: 60px;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    align-items: center;

    img {
      height: 60%;
      margin-right: 10px;
    }
  }

  .drop-menu {
    float: right;
    margin-right: 30px;
    right: 10px;

    &-title {
      font-size: 18px;
    }
  }

  .btn-menu {
    font-size: 16px;
    float: right;
    margin-left: 2%;
  }
}

.modal {
  &-title {
    font-size: 18px;
    font-weight: 600;
  }
}
</style>
