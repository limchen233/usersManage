<template>
  <div class="add container">
    <Alert v-if="alert" v-bind:message="alert"></Alert>
   <h2 class="page-header">添加用户</h2>
   <form @submit="addCustomer">
     <div class="well">
       <h4>用户信息</h4>
       <div class="form-group">
         <label>姓名</label>
         <input type="text" class="form-control" placeholder="name（必填）" v-model="customer.name">
       </div>
       <div class="form-group">
         <label>年龄</label>
         <input type="text" class="form-control" placeholder="age" v-model="customer.age">
       </div>
       <div class="form-group">
         <label>电话</label>
         <input type="text" class="form-control" placeholder="phone（必填）" v-model="customer.phone">
       </div>
       <div class="form-group">
         <label>邮箱</label>
         <input type="text" class="form-control" placeholder="email（必填）" v-model="customer.email">
       </div>
       <div class="form-group">
         <label>学历</label>
         <input type="text" class="form-control" placeholder="education" v-model="customer.education">
       </div>
       <div class="form-group">
         <label>毕业院校</label>
         <input type="text" class="form-control" placeholder="graduation" v-model="customer.graduation">
       </div>
       <div class="form-group">
         <label>职业</label>
         <input type="text" class="form-control" placeholder="profession" v-model="customer.profession">
       </div>
       <div class="form-group">
         <label>个人简介</label>
         <!-- <input type="text" class="form-control" placeholder="introduction" v-model="customer.introduction"> -->
         <textarea class="form-control" rows="10" v-model="customer.introduction"></textarea>
       </div>
       <button type="submit" class="btn btn-primary">添加</button>
     </div>
   </form>
  </div>
</template>

<script>
// 引入组件
import Alert from './Alert';

export default {
  name: 'add',
  data () {
    return {
      customer: {},
      alert: ''
    }
  },
  methods: {
    addCustomer(e) {
      // console.log(123);
      if(!this.customer.name || !this.customer.phone || !this.customer.email){
        // console.log("请添加对应的信息");
        this.alert = "请添加对应的信息";
      }else{
        let newCustmer = {
          name: this.customer.name,
          age: this.customer.age,
          phone: this.customer.phone,
          email: this.customer.email,
          education: this.customer.education,
          graduation: this.customer.graduation,
          profession: this.customer.profession,
          introduction: this.customer.introduction
        }
        this.$axios.post("http://localhost:3000/users",newCustmer)
          .then((response) => {
            // console.log(response);
            
            // 成功后跳转到根目录
            this.$router.push({path:"/",query:{alert:"用户信息添加成功！"}});
          })
      }
      e.preventDefault();
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
