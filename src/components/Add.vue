<template>
    <div class="add container">
      <Alert v-if="alert" v-bind:message="alert"></Alert>
      <h1 class="page-header">添加用户</h1>
      <form v-on:submit="addCustomer">
        <div class="well">
          <h4>用户信息</h4>
          <div class="form-group">
            <label>姓名</label>
            <input type="text" class="form-control" placeholder="name" v-model="customer.name">
          </div>
          <div class="form-group">
            <label>电话</label>
            <input type="text" class="form-control" placeholder="phone" v-model="customer.phone">
          </div>
          <div class="form-group">
            <label>邮箱</label>
            <input type="text" class="form-control" placeholder="email" v-model="customer.email">
          </div>
          <div class="form-group">
            <label>学历</label>
            <input type="text" class="form-control" placeholder="education" v-model="customer.education">
          </div>
          <div class="form-group">
            <label>学校</label>
            <input type="text" class="form-control" placeholder="school" v-model="customer.school">
          </div>
          <div class="form-group">
            <label>职业</label>
            <input type="text" class="form-control" placeholder="job" v-model="customer.job">
          </div>
          <div class="form-group">
            <label>个人简介</label>
            <textarea class="form-control" rows="10" v-model="customer.profile"></textarea>
          </div>
          <button type="submit" class="btn btn-primary">添加</button>
        </div>
      </form>
    </div>
</template>

<script>
  import Alert from "./Alert"
    export default {
        name: 'add',
        data() {
            return {
              customer:{},
              alert:"",
            }
        },
      methods:{
        addCustomer(event) {
          //console.log(123);
          if (!this.customer.name || !this.customer.phone || !this.customer.email){
            this.alert = "请添加必要信息";
          }else {
            let newCustomer = {
              name:this.customer.name,
              phone:this.customer.phone,
              email:this.customer.email,
              education:this.customer.education,
              school:this.customer.school,
              job:this.customer.job,
              profile:this.customer.profile
            };
            this.$http.post("http://localhost:3000/users",newCustomer)
              .then(response => {
                console.log(response);
                // 通过URL获取到query的值为"用户信息添加成功"
                this.$router.push({path:'/',query:{alert:"用户信息添加成功"}});
              });
            event.preventDefault();
          }
          event.preventDefault();
        }
      },
      components:{
          Alert
      }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
