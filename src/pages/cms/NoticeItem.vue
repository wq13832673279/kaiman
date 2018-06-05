<template>
    <div class="notice">
      <img src="../../assets/images/call.png">
      <div class="content-wrap">
        <div class="header">
          <h2>{{title}}</h2>
          <span>{{time}}</span>
        </div>
        <div class="content">
          <span v-html="content"></span>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
      data() {
        return {
          title:"",
          time:"",
          content:""
        }
      },
      created: function() {
        this.initialize();
      },
      methods: {
        initialize() {
          this.loadNoticeInfo();
        },
        loadNoticeInfo() {
          let id = this.$route.query.id;
          if (id == null || id == "") {
            this.$router.push("/notice");
            return;
          }
          this.$http.get(this.host + '/uc/announcement/'+id).then(response => {
            var result = response.body;
            if (result.code == 0) {
              this.title = result.data.title;
              this.time = result.data.createTime;
              this.content = result.data.content;
            }
          });
        },
      }
    }
</script>

<style scoped>
  .notice {
    background: #fff;
    padding-bottom: 20px;
    overflow-x: hidden;
  }
  .content-wrap {
    width: 1200px;
    margin: 0 auto;
    background: #fff;
  }
  .header {
    text-align: center;
    margin-bottom: 10px;
    padding: 10px 0;
    border-bottom: 1px dashed #ccc;
  }
  .header h2 {
    display: inline;
  }
  .header span {
    padding: 0 10px;
  }
</style>
