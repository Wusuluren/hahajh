<template xmlns:v-bind="http://www.w3.org/1999/xhtml">
  <div class="section">
    <div class="container">
      <div class="row">
        <!-- 小屏兼容 -->
        <div class="hidden-sm hidden-md hidden-lg main-left-s" style="text-align: center">
          <table border="0" style="margin: 0 auto">
            <tr>
              <td align="left" style="width: 80px ">
                <div class="person-info">
                  <span>
                      <a href="/manager/setting">
                          <img src="" alt="头像无法显示" class="info-avatar">
                      </a>
                  </span>
                </div>
              </td>
              <td align="left" style="width: 160px;padding-top: 8px">
                <div class="info-name-s" data-toggle="tooltip" :title="user.username">user.username</div>
                <div class="info-score-s">积分：0</div>
                <div class="info-signature-s" data-toggle="tooltip" :title="user.profile">user.profile</div>
              </td>
              <td align="left" style="width: 40px">
                <div class="publish-s">
                  <a href="/user/publish/pic" style="color: #FFFFFF">
                    <span class="glyphicon glyphicon-edit" style="top:2px;"></span>
                    <span>发帖</span>
                  </a>
                </div>
              </td>
              <td></td>
            </tr>
          </table>
        </div>
        <!-- 分页内容 -->
        <div class="col-sm-offset-1 col-sm-7 main-left">
          <!-- 排序标签 -->
          <div>
            <ul class="nav nav-justified hidden-xs">
              <li :class="{active:(tab_current==0)}" @click.prevent="tab_sw(0)" style="border-bottom: 1px solid #eee;border-right: 1px solid #eee;">
                <a href="" v-bind:style="{'color':(tab_current==0)?'#ac483d':'', 'background-color': 'white'}">发表</a>
              </li>
              <li :class="{active:(tab_current==1)}" @click.prevent="tab_sw(1)" style="border-bottom: 1px solid #eee;border-right: 1px solid #eee;">
                <a href="" v-bind:style="{'color':(tab_current==1)?'#ac483d':'', 'background-color': 'white'}">分享</a>
              </li>
              <li :class="{active:(tab_current==2)}" @click.prevent="tab_sw(2)" style="border-bottom: 1px solid #eee">
                <a href="" v-bind:style="{'color':(tab_current==2)?'#ac483d':'', 'background-color': 'white'}">评论</a>
              </li>
            </ul>
            <ul class="nav nav-tabs hidden-sm hidden-md hidden-lg">
              <li :class="{active:(tab_current==0)}" @click.prevent="tab_sw(0)" style="border-bottom: 1px solid #eee">
                <a href="" v-bind:style="{'color':(tab_current==0)?'#ac483d':'', 'background-color': 'white'}">发表</a>
              </li>
              <li :class="{active:(tab_current==1)}" @click.prevent="tab_sw(1)" style="border-bottom: 1px solid #eee">
                <a href="" v-bind:style="{'color':(tab_current==1)?'#ac483d':'', 'background-color': 'white'}">分享</a>
              </li>
              <li :class="{active:(tab_current==2)}" @click.prevent="tab_sw(2)" style="border-bottom: 1px solid #eee">
                <a href="" v-bind:style="{'color':(tab_current==2)?'#ac483d':'', 'background-color': 'white'}">评论</a>
              </li>
            </ul>
          </div>
          <div>
            <ul class="list-unstyled">
              <div v-if="note_list.length === 0" class="no-content-tips">
                <div v-if="tab_current === 0">你还没有发表任何内容</div>
                <div v-else-if="tab_current === 1">你还没有分享任何内容</div>
                <div v-else-if="tab_current === 2">你还没有评论任何内容</div>
              </div>
              <div v-for="note in note_list">
                <li class="nav" style="border-bottom: 1px solid #d5d5d5;">
                  <!-- 基本信息 -->
                  <div class="u-bar" data-id="note.id">
                    <a href="" @click.prevent="del_note(note.id)">
                      <span class="pull-left note-info glyphicon glyphicon-remove"></span>
                    </a>
                    <span class="pull-left pub-time"> {{ note.pub_date }} </span>
                    <div class="pull-right">
                      <div class="total-bar">
                        <div class="praise-1">
                        <span class="praise-2">
                          <img :src="note.Praised?'/static/focus/images/yizan.png':'/static/focus/images/zan.png'" class="praise-img" @click.prevent="praise_tread_share(note, 'praise')">
                        </span>
                        </div>
                        <span class="praise-txt"> {{ note.praise_str }} </span>
                        <span class="add-num-praise">
                          <em>+1</em>
                        </span>
                        <div class="tread-1">
                          <span class="tread-2">
                              <img :src="note.Treaded ? '/static/focus/images/yicai.png':'/static/focus/images/cai.png'" class="tread-img" @click.prevent="praise_tread_share(note, 'tread')">
                          </span>
                        </div>
                        <span class="tread-txt"> {{ note.tread_str }} </span>
                        <span class="add-num-tread">
                          <em>+1</em>
                        </span>
                      </div>
                      <span style="float: right">
                        <div v-if="is_login">
                          <a href="/detail_note.id"></a>
                        </div>
                        <div v-else="">
                          <a href="/manager/login?url=/detail_note.id"></a>
                        </div>
                        <span class="glyphicon glyphicon-comment comment-img"></span>
                        <span class="comment-txt"> {{ note.comment_str }} </span>
                      </span>
                    </div>
                  </div>
                  <!-- 发布内容 -->
                  <div class="cont" style="display: block">
                    <router-link :to="'/detail/' + note.id">
                      <div class="c-text" v-if="note.text">
                        {{ note.text }}
                      </div>
                      <div class="content-img" v-if="note.image">
                        <img :src="note.image" alt="图片无法显示"
                             class="img-responsive center-block" width="100%">
                      </div>
                    </router-link>
                  </div>
                </li>
              </div>
            </ul>
          </div>
          <Pagination v-if="note_list.length > 0" :total="total" :display="display" :currentPage="current" @pagechange="page_change"></Pagination>
        </div>
        <!-- 右侧边栏 -->
        <div class="col-sm-3 hidden-xs main-right">
          <div style="text-align: left">
            <span style="">
                <router-link to="/setting">
                    <img :src="user.avatar" alt="头像无法显示" class="info-avatar" data-toggle="tooltip" title="修改个人信息">
                </router-link>
            </span>
            <span class="info-name" data-toggle="tooltip" :title="user.username">{{ user.username }} </span>
            <span class="info-score">积分：0</span>
            <span class="info-signature" data-toggle="tooltip" :title="user.profile">{{ user.profile }}</span>
          </div>
          <div class="publish">
            <router-link to="/publish">
              <span class="glyphicon glyphicon-edit"></span>
              <span style="position: relative;bottom: 3px">发帖</span>
            </router-link>
          </div>
          <img src="/static/focus/images/test_img1.png" alt="图片无法显示" class="img-thumbnail">
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped="scoped">
  .no-content-tips {
    padding: 50px;
  }
  .total-bar {
    float:left;
    width: auto;
  }
  .info-avatar {
    width: 80px;
    height: 80px;
    border-radius: 40px;
    margin: 10px;
  }
  .info-name {
    word-break: break-all;
    overflow: hidden;
    white-space: pre-wrap;
    word-wrap: break-word;
    width: auto;
    height: 20px;
    font-size: 15px;
    position: absolute;
    top: 10px;
    margin-right: 10px;
  }
  .info-name-s {
    word-break: break-all;
    overflow: hidden;
    white-space: pre-wrap;
    word-wrap: break-word;
    width: auto;
    height: 20px;
    font-size: 15px;
    /*position: absolute;*/
    /*top: 120px;*/
    margin-right: 10px;
  }
  .info-score {
    color: #888;
    position: absolute;
    top: 40px;
  }
  .info-score-s {
    color: #888;
    font-size: 12px;
    /*position: absolute;*/
    /*top: 150px;*/
  }
  .info-signature {
    color: #888;
    word-break: break-all;
    width: auto;
    height: 43px;
    white-space: pre-wrap;
    word-wrap: break-word;
    overflow: hidden;
    position: absolute;
    margin-right: 10px;
    top: 60px;
  }
  .info-signature-s {
    color: #888;
    font-size: 12px;
    word-break: break-all;
    width: auto;
    height: 43px;
    white-space: pre-wrap;
    word-wrap: break-word;
    overflow: hidden;
    /*position: absolute;*/
    margin-right: 10px;
    /*top: 170px;*/
  }
</style>
<script>
//  import Bus from '@/components/bus.js'
  import Pagination from '@/components/Pagination'

  export default {
    name: 'User',
    components: {Pagination},
    data: function () {
      return {
        is_login: false,
        user: {},
        tab_current: 0,
        note_list: [],
        total: 1,
        current: 1,
        display: 5
      }
    },
    methods: {
      /*  换页钩子函数  */
      page_change: function (cur) {
        this.current = cur
        this.update_data()
      },
      update_data: function () {
        this.GLOBAL.debug('user created')
        let url = `${this.GLOBAL.api}/api/ucenter/`
        let this_ = this
        let params = JSON.stringify({
          'type': this.tab_current,
          'current': this.current,
          'display': this.display
        })
        this.$axios.post(url, params).then(
          response => {
            this_.user = response.data.user
            this_.is_login = response.data.is_login
            this_.note_list = response.data.note_list
            this_.total = response.data.total
            this_.current = response.data.current
            this_.GLOBAL.debug(response)
          }
        ).catch(
          response => {
          }
        )
      },
      /*  导航栏切换  */
      tab_sw: function (index) {
        this.tab_current = index
        this.update_data()
      },
      praise_tread_share: function (note, action) {
        this.GLOBAL.praise_tread_share(this, note, action)
      },
      /*  删帖  */
      del_note: function (id) {
        let url = `${this.GLOBAL.api}/api/del-n-c/`
        let this_ = this
        let params = JSON.stringify({
          'note_id': id
        })
        this.$axios.post(url, params).then(
          response => {
            this_.GLOBAL.debug(response)
            if (response.data.is_success) {
              this_.$router.go(0)
            }
          }
        )
      }
    },
    created: function () {
      this.update_data()
    },
    destroyed: function () {
    }
  }
</script>
