<template>
  <div class="customers container">
    <!-- 如果alert有内容就弹出来，否则就不显示 -->
    <Alert v-if="alert" v-bind:message="alert"></Alert>
   <h2 class="page-header">用户管理系统
     <!-- <input type="text" class="form pull-right" placeholder="搜索" v-model="filterInput"> -->
   </h2>

   <input type="text" class="form pull-right" placeholder="搜索" v-model="filterInput">
   <br />

   <table class="table table-striped">
     <thead>
       <tr>
         <th>姓名</th>
         <th>电话</th>
         <th>邮箱</th>
         <th></th>
       </tr>
     </thead>

     <tbody>
       <tr v-for="customer in filterBy(customers,filterInput)" :key="customer.id">
         <td class="td">{{customer.name}}</td>
         <td class="td">{{customer.phone}}</td>
         <td class="td">{{customer.email}}</td>
         <!-- to需要绑定，因为后面是个表达式，如果是字符串就不用绑定 -->
         <td><router-link class="btn btn-primary" v-bind:to="'/customer/'+customer.id">详情</router-link>
         </td>
         
       </tr>
     </tbody>
   </table>
  </div>
</template>

<script>
import Alert from './Alert.vue';
import { log } from 'util';

export default {
  name: 'customers',
  data () {
    return {
      customers:[],
      alert:'',
      filterInput:''
    }
  },
  methods: {
    fetchCustomers(){
      // 发送请求
      this.$axios.get('http://localhost:3000/users')
        .then((response) => {
          // console.log(response);
          this.customers = response.data;
        })
    },
    filterBy(customers,value){
      return customers.filter(function(customer){
      return customer.name.match(value);
      })
    }
  },
  // 初始化完成就显示用户信息
  created() {
    if(this.$route.query.alert) {
      this.alert = this.$route.query.alert;
    }
    this.fetchCustomers();
  },

  // 更新完成获取用户信息
  updated() {
    this.fetchCustomers();
  },
  components:{
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .td{
    vertical-align: middle;
  }

  .pull-right {
    margin-right:45px;
  }
</style>
