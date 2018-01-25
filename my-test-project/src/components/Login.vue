<template>
	<el-row>
		<el-col :span="24">
			<div class="loginBox">
				<el-form :model="userInfo" status-icon :rules="rules" ref="userInfo" label-width="0px" class="demo-ruleForm">
					<el-form-item prop="username">
						<el-input type="text" v-model="userInfo.username" auto-complete="off" placeholder="请输入用户名"></el-input>
					</el-form-item>
					<el-form-item prop="pass">
						<el-input type="password" v-model="userInfo.pass" auto-complete="off" placeholder="请输入密码"></el-input>
					</el-form-item>
					<el-form-item>
						<div class="operator">
							<el-button type="primary" @click="Login('userInfo')">登录</el-button>
							<el-button @click="resetForm('userInfo')">重置</el-button>
						</div>
					</el-form-item>
				</el-form>
			</div>
		</el-col>
	</el-row>
</template>

<script>
	export default {
		data() {
			var checkName = (rule, value, callback) => {
				let that = this;
				if(value === '') {
					return callback(new Error('用户名不能为空'));
				}else{
					callback();
				}
			};
			var validatePass = (rule, value, callback) => {
				if(value === '') {
					callback(new Error('请输入密码'));
				}else{
					callback();
				}
			};
			return {
				userInfo: {
					username: '',
					pass: ''
				},
				rules: {
					username: [{
						validator: checkName,
						trigger: 'blur'
					}],
					pass: [{
						validator: validatePass,
						trigger: 'blur'
					}]
				}
			};
		},
		methods: {
			Login(formName) {
				this.$refs[formName].validate((valid) => {
					if(valid) {
						alert('submit!');
					} else {
						console.log('error submit!!');
						return false;
					}
				});
			},
			resetForm(formName) {
				this.$refs[formName].resetFields();
			}
		}
	}
</script>

<style lang="less" scoped>
	.loginBox {
		width: 20%;
		height: 240px;
		border: 1px solid #ccc;
		margin: 9% auto 0px auto;
		border-radius: 4px;
		padding: 30px 40px 0px 40px;
		box-shadow: 0 0 25px #cac6c6;
		.operator {
			margin-top: 20px;
		}
	}
</style>