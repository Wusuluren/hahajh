<template>
  <!-- 右侧边栏 -->
  <div class="col-sm-3 hidden-xs main-right">
    <div class="publish" @click.prevent="check_user_state">
      <a href="">
        <span class="glyphicon glyphicon-edit"></span>
        <span style="position: relative;bottom: 3px">发帖</span>
      </a>
    </div>
    <div class="hxjx" v-if="note_haha_list.length === 4">
      <div class="hxjx-title">欢笑精选</div>
        <div>
          <div style="float: left; width: 50%; padding: 0 5px">
            <a :href="note_haha_list[0].detail_url" data-toggle="tooltip" :title="note_haha_list[0].text"><img :src="note_haha_list[0].image_crop?note_haha_list[0].image_crop:note_haha_list[0].image" class="img-responsive">{{ note_haha_list[0].text }}</a>
          </div>
          <div style="float: right; width: 50%; padding: 0 5px">
            <a :href="note_haha_list[1].detail_url" data-toggle="tooltip" :title="note_haha_list[1].text"><img :src="note_haha_list[1].image_crop?note_haha_list[1].image_crop:note_haha_list[1].image" class="img-responsive">{{ note_haha_list[1].text }}</a>
          </div>
        </div>
        <div>
          <div style="float: left; width: 50%; padding: 0 5px">
            <a :href="note_haha_list[2].detail_url" data-toggle="tooltip" :title="note_haha_list[2].text"><img :src="note_haha_list[2].image_crop?note_haha_list[2].image_crop:note_haha_list[2].image" class="img-responsive">{{ note_haha_list[2].text }}</a>
          </div>
          <div style="float: right; width: 50%; padding: 0 5px">
            <a :href="note_haha_list[3].detail_url" data-toggle="tooltip" :title="note_haha_list[3].text"><img :src="note_haha_list[3].image_crop?note_haha_list[3].image_crop:note_haha_list[3].image" class="img-responsive">{{ note_haha_list[3].text }}</a>
          </div>
        </div>
    </div>
  </div>
</template>
<style scoped="scoped">
  .hxjx {
    margin: 10px 0;
  }

  .hxjx div {
    line-height: 35px;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }

  .hxjx-title {
    background-color: #d43f3a;
    padding: 2px 5px;
    font-size: 15px;
    letter-spacing: 1px;
    color: white;
    margin-bottom: 10px;
  }
</style>
<script>
    export default {
      name: 'SideBar',
      data: function () {
        return {
          is_login: false,
          note_haha_list: [{detail_url: ''}, {detail_url: ''}, {detail_url: ''}, {detail_url: ''}]
        }
      },
      methods: {
        check_user_state: function () {
          let url = `${this.GLOBAL.api}/manager/user-state/`
          let this_ = this
          this_.$axios.get(url).then(
            function (response) {
              if (response.data.hasOwnProperty('is_login')) {
                this_.is_login = response.data.is_login
              }
              if (this_.is_login === true) {
                window.location.href = '/publish'  // 刷新标题栏
              } else {
                sessionStorage.setItem('last_herf', '/publish')
                window.location.href = '/login'
              }
            }
          )
        },
        get_note_haha_list: function () {
          let url = `${this.GLOBAL.api}/api/note-jx/`
          let this_ = this
          this_.$axios.get(url).then(
            function (response) {
              if (response.data.hasOwnProperty('note_haha_list')) {
                this_.note_haha_list = response.data.note_haha_list
              }
            }
          )
        }
      },
      created: function () {
        this.GLOBAL.debug('sidebar created')
        this.get_note_haha_list()
//        let this_ = this
//        this.Bus.$on('loginEvent', (isLogin, user) => {
//          this_.is_login = isLogin
//          this_.user = user
//          this_.GLOBAL.debug('login event')
//        })
      }
    }
</script>
