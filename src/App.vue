<template>
<div id="app">
	<div class="app-header">
		<div class="goback">
			<span class="arrow">
				<span class="arrow green"></span>
			</span>
		</div>
		<h1>美团网</h1>
		<div class="login">登录</div>
	</div>
	<!-- 如果是详情页，不能显示 -->
	<div class="app-search" v-show="$route.path.indexOf('/detail/') !== 0">
		<input type="text" placeholder="请输入搜索关键字" v-model="msg" @keyup.enter="gotoSearch">
	</div>
	<!-- 路由渲染位置 -->
	<router-view></router-view>
</div>
</template>

<script>
export default {
	// 绑定的数据
	data() {
		return {
			msg: ''
		}
	},
	// 方法
	methods: {
		// 开始搜索
		gotoSearch() {
			// 将数据提交给store
			this.$store.commit('updateWord', this.msg);
			// 清空msg
			this.msg = '';
		}
	}
}
</script>

<style lang="scss">
@import './base.scss';
* {
	margin: 0;
	padding: 0;
	list-style: none;
}
body, html {
	background: #efefef;
}
.app-header {
	background: $navColor;
	height: 60px;
	line-height: 60px;
	display: flex;
	text-align: center;
	color: #fff;
	.goback {
		width: 50px;
		position: relative;
		.arrow {
			@include arrow(10px, #fff, right);
			position: absolute;
			top: 22px;
			left: 2px;
			.green {
				border-right-color: $navColor;
				top: -10px;
				left: -7px;
			}
		}
	}
	h1 {
		flex: 1;
		font-size: 24px;
		text-indent: -0.5em;
	}
	.login {
		width: 50px;
	}
}
.app-search {
	display: flex;
	padding: 10px 20px;
	background: #fff;
	input {
		display: block;
		flex: 1;
		padding: 10px 20px;
		border: none;
		font-size: 14px;
		border-radius: 18px;
		background: #efefef;
		outline: none;
	}
}
</style>
