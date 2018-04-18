<template>
	<div id="login">
		<h2>登录</h2>
		<label for='userAccount'>用户名</label>
		<input type="text" id="userAccount" name="userAccount" required v-model="userAccount">
		<label for="userPassword">密码</label>
		<input type="password" id="userPassword" name="userPassword" required v-model="userPassword">
		<button type="submit" @click="loginQuest">登录</button>
		<router-link to="/register">
			<button type="button">注册</button>
		</router-link>
	</div>
</template>
<script>
	import axios from 'axios';

	export default {
		name: 'login',
		data(){
			return {
				userAccount:'',
				userPassword:''
			}
		},
		methods:{
			loginQuest(){
				let that = this;
				if(this.userPassword.length===0||this.userAccount.length===0){
					return false;
				}
				axios.post('/login',{
					'data': JSON.stringify({
						userAccount: that.userAccount,
						userPassword:that.userPassword
					})})
					.then(function(res){
						/*if(res.status===200){*/
							that.$router.push('/orderindex');
						/*}*/
					})
					.catch(function(res){
						alert("登录失败！")
					})
				
			}
		},
		created:function(){
			document.getElementsByTagName('body')[0].className = '';
		}

	}
</script>
<style scoped src="../assets/css/login_register.css"></style>