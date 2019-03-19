<template>
    <div class="customers container">
      <!-- v-if用于 当alert为空时不显示弹窗-->
      <Alert v-if="alert" :message="alert"></Alert>
      <h1 class="page-header">用户管理系统</h1>
      <input type="text" class="form-control" placeholder="搜索" v-model="filterInput">
      <table class="table table-striped">
        <thead>
          <tr>
            <th>姓名</th>
            <th>电话</th>
            <th>邮箱</th>
          </tr>
        </thead>
        <tbody>
        <tr v-for="customer in filterBy(customers,filterInput)">
          <td>{{customer.name}}</td>
          <td>{{customer.phone}}</td>
          <td>{{customer.email}}</td>
          <td><router-link class="btn btn-default" :to="'/customer/' + customer.id">详情</router-link></td>
        </tr>
        </tbody>
      </table>
    </div>
</template>

<script>
  import Alert from "./Alert"
  import axios from "axios"
    export default {
        name: 'customers',
        data() {
            return {
              customers:[],
              alert:"",
              filterInput:""
            }
        },
      components:{
        Alert,
      },
      methods:{
          fetchCustomers(){
            axios.get("http://localhost:3000/users")
              .then(response => {
                this.customers = response.data;
              })
          },
        filterBy(customers,value){
            return customers.filter(customer => {
              // 任何字符串与空字符串匹配都将返回一个true
              return customer.name.match(value)
            })
        }
      },
      created(){
          //当页面从Add.vue跳转过来时，URL会携带query:{alert:"xxx"},可以通过this.$route获取即可
          if (this.$route.query.alert) {
            this.alert = this.$route.query.alert;
          }
          this.fetchCustomers();
      },
      updated(){
          //this.fetchCustomers();
      }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
