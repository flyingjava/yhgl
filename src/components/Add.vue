<template>
<div class="add container">
    <h1 class="page-header">添加用户</h1>
    <Alert v-if='alert' :message='alert'></Alert>
    <form v-on:submit='addCustomer'>
        <div class='well'>
            <h4>用户信息</h4>
            <div class='form-group'>
                <label>姓名</label>
                <input type='text' class='form-control' placeholder='name' v-model='customer.name'>
            </div>
            <div class='form-group'>
                <label>电话</label>
                <input type='text' class='form-control' placeholder='phone' v-model='customer.phone'>
            </div>
            <div class='form-group'>
                <label>邮箱</label>
                <input type='text' class='form-control' placeholder='email' v-model='customer.email'>
            </div>
            <div class='form-group'>
                <label>年龄</label>
                <input type='text' class='form-control' placeholder='age' v-model='customer.age'>
            </div>
            <button type='submit' class='btn btn-primary'>添加</button>
        </div>
    </form>
 </div>
</template>

<script>
import Alert from './Alert'
export default {
    name:'add',
    data(){
        return {
            customer:{},
            alert:''
        }
    },
    methods:{
        addCustomer(e){
            if(!this.customer.name||!this.customer.phone||!this.customer.email){
                this.alert='请添加对应信息'
            }else{
                let newCustomer = {
                    name:this.customer.name,
                    phone:this.customer.phone,
                    email:this.customer.email,
                    age:this.customer.age
                }
                this.$http.post('http://localhost:3000/users',newCustomer)
                .then((response)=>{
                    this.$router.push({path:'/',query:{alert:'用户信息添加成功！'}})
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
