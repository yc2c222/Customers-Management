<template>
    <div class="customerdetails container">
      <router-link to="/" class="btn btn-default">返回</router-link>
      <h1 class="page-header">
        {{customer.name}}
        <span class="pull-right">
          <router-link v-bind:to="'/edit/'+customer.id" class="btn btn-primary">
            编辑
          </router-link>
          <button class="btn btn-danger" @click="deleteCustomer(customer.id)">删除</button>
        </span>
      </h1>
      <ul class="list-group">
        <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.phone}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.email}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.education}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.school}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.job}}</span></li>
        <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.profile}}</span></li>
      </ul>
    </div>
</template>

<script>
    export default {
        name: 'customerdetails',
        data() {
            return {
              customer:{}
            }
        },
      methods:{
        fetchCustomers(id){
          this.$http.get("http://localhost:3000/users/" + id)
            .then(response => {
              this.customer = response.body;
              console.log(this.customer)
            })
        },
        deleteCustomer(id){
          this.$http.delete("http://localhost:3000/users/"+id)
            .then(response => {
              this.$router.push({path:'/',query:{alert:"用户删除成功"}});
            })
        }
      },
      created() {
          this.fetchCustomers(this.$route.params.id)
      }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
