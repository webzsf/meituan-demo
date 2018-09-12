<!-- 模板 -->
<template>
<div class="app-home">
	<ul class="icons">
		<!-- vue cli中，v-for指令一定要设置key属性 -->
		<router-link v-for="(item, index) in icons" :key="index" :to="'/list/type/' + item.id" tag="li">
			<img :src="'img/icon/' + item.img" alt="">
			<p>{{item.text}}</p>
		</router-link>
	</ul>
	<!-- 广告模块 -->
	<ul class="ad">
		<router-link v-for="(item, index) in ad" tag="li" :to="'/detail/' + item.id" :key="index">
			<h3 :class="'color-' + index">{{item.title}}</h3>
			<p>{{item.description}}</p>
			<img :src="'img/ad/' + item.url" alt="">
		</router-link>
	</ul>
	<div class="like">
		<h2 class="title">猜你喜欢</h2>
		<ul class="items">
			<router-link v-for="(item, index) in list" :key="index" :to="'/detail/' + item.id" tag="li">
				<img :src="'img/list/' + item.img" alt="">
				<div class="content">
					<h3>{{item.title}}</h3>
					<p>
						<span class="price">{{item.price}}元</span>
						<span class="origin">门市价:{{item.originPrice}}元</span>
						<span class="sales">销量{{item.sales}}</span>
					</p>
				</div>
			</router-link>
		</ul>
	</div>
</div>
</template>
<!-- 样式 -->
<style type="text/css" lang="scss">
@import '../base.scss';
.app-home {
	.icons {
		@include clearfix;
		background: #fff;
		margin-bottom: 10px;
		padding: 10px 0;
		li {
			float: left;
			width: (100% / 5);
			text-align: center;
			img {
				width: 60%;
			}
			p {
				font-size: 12px;
				margin: 5px 0 10px;
			}
		}
	}
	.ad {
		display: flex;
		background: #fff;
		margin-bottom: 10px;
		li {
			flex: 1;
			border-right: 1px solid #ccc;
			text-align: center;
			padding: 15px 0;
			&:last-child {
				border-right: none;
			}
			img {
				width: 60%;
			}
			h3 {
				font-size: 14px;
			}
			p {
				font-size: 12px;
				margin: 5px 0 8px;
			}
			.color-0 {
				color: red;
			}
			.color-1 {
				color: green;
			}
			.color-2 {
				color: purple;
			}
		}
	}
	.like {
		background: #fff;
		.title {
			padding-top: 5px;
			line-height: 35px;
			height: 35px;
			margin: 0 10px;
			border-bottom: 1px solid #ccc;
		}
		.items {
			@extend %items;
		}
	}
}
</style>
<!-- 脚本 -->
<script type="text/javascript">
export default {
	// 绑定数据
	data() {
		return {
			icons: [
				{ img: '01.png', text: '美食', id: 1 },
				{ img: '02.png', text: '电影', id: 2 },
				{ img: '03.png', text: '酒店', id: 3 },
				{ img: '04.png', text: '休闲', id: 4 },
				{ img: '05.png', text: '外卖', id: 5 },
				{ img: '06.png', text: 'KTV', id: 6 },
				{ img: '07.png', text: '周边游', id: 7 },
				{ img: '08.png', text: '丽人', id: 8 },
				{ img: '09.png', text: '小吃', id: 9 },
				{ img: '10.png', text: '火车票', id: 10 }
			],
			// 广告数据
			ad: [],
			// 商品数据
			list: []
		}
	},
	// 发送请求
	created() {
		// get请求
		this.$http.get('/data/home.json')
			// 监听返回
			.then(({ data }) => {
				// this就是组件实例化对象
				this.ad = data.ad;
				this.list = data.list;
			})
	}
}
</script>