<template>
  <div class="zhuye">
      <div class="customres container">
      <Alert v-if='alert' :message='alert'></Alert>
  <h1 calss='page-header'>用户管理系统</h1>
  <input type='text' class='form-control' placeholder='搜索' v-model='filterInput'>
  <br>
  <table width="90%" id="mytab"   class="t1">
    <thead>
      <tr>
        <th>姓名</th>
        <th>电话</th>
        <th>邮箱</th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for='(customer,index) in filterBy(customers,filterInput)' :key='index'>
        <td>{{customer.name}}</td>
        <td>{{customer.phone}}</td>
        <td>{{customer.email}}</td>
        <td><router-link class='btn btn-default' :to="'/customer/'+customer.id">详情</router-link></td>
      </tr>
    </tbody>
  </table>
  </div>
  </div>
</template>

<script>
import Alert from './Alert'
export default {
    name:'zhuye',
    data(){
      return {
        customers:[],
        filterInput:'',
        alert:''
      }
    },
    methods:{
      fetchCustomers(){
        this.$http.get('http://localhost:3000/users')
        .then((response)=>{
          this.customers = response.data
        })
      },
      filterBy(customers,value){
        return customers.filter(function(customer){
          return customer.name.match(value)
        })
      }
    },
    created(){
      if(this.$route.query.alert){
        this.alert = this.$route.query.alert
      }
      this.fetchCustomers()
    },
    components:{
      Alert
    },
    updated(){
      this.fetchCustomers()
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table{  
    table-layout:fixed;  
    empty-cells:show;   
    border-collapse: collapse;  
    margin:0 auto;
    margin-left:0; 
    text-align:center; 
    border:1px solid #ccc;
}  
tr{  
    height:30px;  
    border:1px solid #ccc;
}  
th{
  text-align:center;
  border:1px solid #ccc;
}
td{
  border:1px solid #ccc;
}
</style>
