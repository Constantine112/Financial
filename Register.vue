<template>
	<div id="register">
		<h2>注册</h2>
		<label>店主名字</label>
		<input type="text" name="userName" id="userName" required v-model="userName">
		<label>账户</label>
		<input type="text" name="userAccount" id="userAccount" required v-model="userAccount">
		<label>密码</label>
		<input type="password" name="userPassword" id="userPassword" required v-model="userPassword">
		<label>商店名</label>
		<input type="text" name="userStore" id="userStore" required v-model="userStore">
		<label>商家地址</label>
		<input type="text" name="userAddress" id="userAddress" required v-model="userAddress">
		<label>商家电话</label>
		<input type="text" name="userPhone" id="userPhone" required v-model="userPhone">
		<div id="printer">
			<label>打印机编号</label>
			<input type="text" name="id" id="id" required v-model="id">
		</div>
		<router-link to="login">
					<button type="button">登录</button>
				</router-link>
		<button type="submit" @click="registerQuest">注册</button>
	</div>
</template>
<script>
	import axios from 'axios';

	export default {
		name: 'register',
		data(){
			return {
				userName: '',
				userAccount:'',
				userPassword: '',
				userStore: '',
				userAddress: '',
				userPhone: '',
				id: ''
			}
		},
		methods:{
			registerQuest(){
				let that = this;
				axios.post('/register',{
					'data': JSON.stringify({
						userName:that.userName,
						userAccount: that.userAccount,
						userPassword:that.userPassword,
						userPhone:that.userPhone,
						userStore:that.userStore,
						id:that.id,
						userAddress:that.userAddress
					})})
					.then(function(res){
						if(res.status===200){
							that.$router.push('/login');
						}
					})
					.catch(function(res){
						console.log(res);
						alert("注册失败!");
					})
			}
		},
		created:function(){
			document.getElementsByTagName('body')[0].className = '';
		}
	}
</script>
<style scoped src="../assets/css/login_register.css"></style>