<template>
  <div class="section">
    <div class="container">
      <div class="row">
        <!-- 小屏兼容 -->
        <div class="hidden-sm hidden-md hidden-lg main-left-s" style="text-align: center">
          <table border="0" style="margin:0 auto">
            <tr>
              <td align="left" style="width: 80px ">
                <div class="person-info">
                  <span>
                      <a href="/manager/setting">
                          <img :src="user.avatar" alt="头像无法显示" class="info-avatar">
                      </a>
                  </span>
                </div>
              </td>
              <td align="left" style="width: 160px;padding-top: 8px">
                <div class="info-name-s" data-toggle="tooltip" :title="user.username">{{ user.username }}</div>
                <div class="info-score-s">积分：0</div>
                <div class="info-signature-s" data-toggle="tooltip" :title="user.profile">{{ user.profile }}</div>
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
        <!-- 主要内容 -->
        <div class="col-sm-offset-1 col-sm-7 main-left">
          <div class="edit">
            <div class="pic">
              <div>预览</div>
              <div class="img">
                <img :src="picture" @click="setPic">
                <span>选择</span>
              </div>
              <input type="file" name="pic" accept="image/gif,image/jpeg,image/jpg,image/png" style="display:none" @change="changeImage($event)" ref="picInput">
            </div>
            <table border="0" class="table" style="font-size: 15px">
              <tr>
                <td align="right" style="color:#888;width:200px"><label>用户名</label></td>
                <td style="width: 10px"></td>
                <td align="left" style="width: 200px">
                  <input type="text" v-model="user.username" style="width: 135px"/>
                </td>
              </tr>
              <tr>
                <td align="right" style="color:#888;width:200px"><label>性别</label></td>
                <td style="width: 10px"></td>
                <td align="left" style="width: 200px">
                  <input type="radio" value="m" :checked="{checked:user.sex==='m'}" v-model="user.sex" style="border: none"/> 男
                  <input type="radio" value="f" :checked="{checked:user.sex==='f'}" v-model="user.sex" style="border: none"/> 女
                </td>
              </tr>
              <tr>
                <td align="right" style="color:#888;width:200px;padding: 0"><label>个性签名</label></td>
                <td style="width: 10px"></td>
                <td align="left" style="width: 200px;padding: 0">
                  <textarea v-model="user.profile" style="width: 135px;height: 100px;padding: 4px; resize: none; cursor: text"></textarea>
                </td>
              </tr>
            </table>
            <button type="button" @click="edit">确认修改</button>
          </div>
        </div>
        <!-- 右侧边栏 -->
        <div class="col-sm-3 hidden-xs main-right">
          <div style="text-align: left">
            <span style="">
                <router-link to="/setting">
                    <img :src="user.avatar" alt="头像无法显示" class="info-avatar">
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
  .edit {
    text-align: center;
    padding-top: 0;
  }
  .edit .table {
    width: 60%;
    margin: 30px auto
  }
  .edit .pic {
    padding: 30px 30px 0 30px;
    cursor: pointer;
  }
  .edit .pic div{
    margin: 5px 0;
  }
  .edit .pic .img {
    width: 100px;
    height: 100px;
    position: relative;
    margin: 0 auto;
    overflow: hidden;
    border-radius: 50%;
  }
  .edit .pic .img img {
    width: 100px;
    height: 100px;
    display: block;
  }
  .edit .pic .img span {
    width: 100px;
    background-color: rgba(0, 0, 0, .3);
    display: block;
    position: absolute;
    bottom: 0;
    font-size: 12px;
    color: #FFF;
    padding: 8px 0;
    pointer-events: none;
  }
  .edit .my-input {

    padding-top: 30px;
    padding-bottom: 30px;
  }
  .edit .my-input textarea {
    width: 400px;
    height: 200px;
  }
  .edit button[type="button"] {
    display: block;
    width: 200px;
    height: 40px;
    margin: 20px auto 10px;
    color: #FFFFFF;
    border: none;
    font-size: 14px;
    cursor: pointer;
    box-shadow: 0 0 0 1000px #EB4F38 inset;
  }
  .myalign1 {
    padding:0 10px 0 0;
  }
  .myalign2 {
    padding:0 0 0 10px;
  }
</style>
<script>
//  import Bus from '@/components/bus.js'

  export default {
    name: 'Notice',
    data: function () {
      return {
        user: {
          username: '',
          sex: 'm',
          profile: ''
        },
        picture: '/static/focus/images/test_img1.png',
//        text_area: 'tttt',
        is_login: false,
        form: {},
        message: ''
      }
    },
    methods: {
      update_user_state: function () {
        let url = `${this.GLOBAL.api}/manager/user-state/`
        let this_ = this
        this_.$axios.get(url).then(
          function (response) {
            if (response.data.hasOwnProperty('is_login')) {
              this_.is_login = response.data.is_login
            }
            if (response.data.hasOwnProperty('user')) {
              this_.user = response.data.user
            }
            this_.GLOBAL.debug(response)
          }
        )
      },
      edit () {
        let formData = new FormData()
        let url = `${this.GLOBAL.api}/manager/setting/`
        let this_ = this
        formData.append('pic_file', this.$refs.picInput.files[0])
        formData.append('username', this.user.username)
        formData.append('sex', this.user.sex)
        formData.append('profile', this.user.profile)
        this.$axios.post(url, formData, {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        }).then(
          function (response) {
            this_.GLOBAL.debug(response)
            if (response.data.hasOwnProperty('is_success') && response.data.is_success === true) {
              this_.$router.go(0)
            }
          })
      },
      // 模拟触发click事件
      setPic () {
        this.$refs.picInput.click()
      },
      // 选择新的头像后，可以预览
      changeImage (e) {
        let file = e.target.files[0]
        let reader = new FileReader()
        let this_ = this
        reader.readAsDataURL(file)
        reader.onload = function (e) {
          console.log(e)
          this_.picture = e.target.result
        }
      }
    },
    created: function () {
      this.update_user_state()
      this.GLOBAL.debug('setting created')
    },
    destroyed: function () {
    }
  }
</script>
