<template>
	<div class="index">
		<!--<!--頭部信息-->
		<!--<div id="header">
			<ul>
				<li>
					<a href="">美食之家</a>
				</li>
			</ul>
		</div>-->
		<van-search ref="search" class="search" @focus="goDatail({name: 'Search'})" placeholder="输入商品名称关键字" />
		<van-swipe :autoplay="3000" indicator-color="white">
			<van-swipe-item class="box-img" v-for="(item,index) in images" :key="index">
				<img class="auto-img" :src="item.url" />
			</van-swipe-item>
		</van-swipe>
		<van-notice-bar text="本网站是免费开放的，欢迎各位美食大佬在这相互交流。共同进步，把中华5000千年的美食文化传承下去！！" left-icon="volume-o" />
		<van-row class="recommend" @click.native="goDatail({name:'Recommend',params:{pid:meun.id}})">
			<p class="nve-p">每次推荐</p>
			<van-col span="24">
				<div class="icon" :style="{backgroundImage: 'url(' + meun.albums + ')', backgroundRepeat:'no-repeat',backgroundSize:'100% 100%'}">
				</div>

				<div class="recommend-p">
					<p class="p-title">{{meun.title}}</p><span> <van-icon name="fire" color="#FE3026" class="fire"></van-icon></span></div>
				<div class="abstract">{{meun.intro}}</div>
			</van-col>
		</van-row>
		<van-tabs v-model="active" :swipeable="true" ref="vtabs">
			<van-tab title="主菜">
				<van-row>
					<van-col span='12' v-for="(item,index) in products['jirou']" class="box-col" @click.native="goDatail({name:'Detail',params:{pid:item.id}})">
						<div class="box-big">
							<div><img class="auto-img" :src="item.images.small" /></div>
							<div class="index-name">
								<p>{{item.name}}</p>
							</div>
						</div>

						<div class="rate">
							<van-rate v-model='item.value' icon="like" void-icon="like-o " color="#f44" :readonly='true' />
						</div>
					</van-col>
				</van-row>
			</van-tab>
			<van-tab title="鱼肉">
				<van-row>
					<van-col span='12' v-for="(item,index) in products['yurou']" class="box-col" @click.native="goDatail({name:'Detail',params:{pid:item.id}})" :key="index">
						<div><img class="auto-img" :src="item.images.small" /></div>
						<div class="index-name">
							<p>{{item.name}}</p>
						</div>
						<div class="rate">
							<van-rate v-model='item.value' icon="like" void-icon="like-o " color="#f44" :readonly='true' />
						</div>
					</van-col>
				</van-row>
			</van-tab>
			<van-tab title="汤水">
				<van-row>
					<van-col span='12' v-for="(item,index) in products['tangshui']" class="box-col" @click.native="goDatail({name:'Detail',params:{pid:item.id}})" :key="index">
						<div><img class="auto-img" :src="item.images.small" /></div>
						<div class="index-name">
							<p>{{item.name}}</p>
						</div>
						<div class="rate">
							<van-rate v-model='item.value' icon="like" void-icon="like-o " color="#f44" :readonly='true' />
						</div>
					</van-col>
				</van-row>
			</van-tab>

		</van-tabs>
	</div>
</template>

<script>
	
	
	import { Search, Swipe, SwipeItem, NoticeBar, Tab, Tabs, Rate, Icon, Loading } from 'vant';

	export default {
		name: "Index",

		components: {
			[Search.name]: Search,
			[Swipe.name]: Swipe,
			[SwipeItem.name]: SwipeItem,
			[NoticeBar.name]: NoticeBar,
			[Tab.name]: Tab,
			[Tabs.name]: Tabs,
			[Rate.name]: Rate,
			[Icon.name]: Icon,
			[Loading.name]: Loading,
		},
		data() {
			return {
				active: 0,
				products: {

				},
				meun: null,
				imgs: null,
				images: [{
						url: 'http://s8.sinaimg.cn/middle/4ac0a7ccg7767b9393877&690'
					},
					{
						url: 'http://www.ddmeishi.com/uploads/allimg/171103/2-1G103112047.jpg'
					},
					{
						url: 'http://n1.itc.cn/img8/wb/recom/2016/05/01/146211394530257944.jpeg'
					},
				],

			}
		},
		created() {

			var types = JSON.parse(localStorage.getItem("types"));

			var products = JSON.parse(localStorage.getItem("products"));
			var menu = JSON.parse(localStorage.getItem("menu"))

			var j = parseInt(Math.random() * (9 - 0 + 1)) + 0;
			this.meun = menu.result[j]
			types.types.forEach(v1 => {
				this.products[v1.type] = [];
				products.products.forEach(v2 => {
					if(v1.type == v2.type) {
						this.products[v1.type].push(v2);
					}
				})
			})
//			console.log(this.products)
		},
		mounted() {

			var search = this.$refs.search;
			var searchHeight = getComputedStyle(search).height;

			this.offsetTop = parseFloat(searchHeight)
			var vtabs = this.$refs.vtabs.$el.firstChild;
			vtabs.style.position = 'sticky';
			vtabs.style.top = searchHeight;
		},
		methods: {
			goDatail(path) {
				this.$router.push(path)
			},

			gode() {
//				console.log("ssss")
			}
		}
	}
</script>

<style scoped="scoped">
	/*=========*/
	.index{
		padding: 0 0.78rem;
	}
	.search {
		position: sticky;
		top: 0;
		z-index: 100;
	}
	
	.van-search__content {
		border-radius: 18px;
	}
	
	.vtabs {
		padding-top: 0;
	}
	
	.van-swipe {
		height: 9.375rem
	}
	
	.box-col {
		padding: 0.156rem;
	}
	
	.index-name {
		text-align: center;
		color: #5A6E86;
		font-size: .8rem;
	}
	
	.van-tabs--line {
		padding-bottom: 0.687rem;
		padding-top: 0;
	}
	
	.box-col[data-v-82b7485c] {
		padding-bottom: 2.5rem;
	}
	
	.rate {
		text-align: center;
	}
	
	.van-col--24 {
		height: 18.687rem;
	}
	
	.recommend {
		margin-bottom: 8.781rem;
	}
	
	.recommend-p {
		text-align: center;
		font-size: 18px;
		color: #2E2D2D;
	}
	
	.nve-p {
		text-align: center;
		color: #FA894F;
		font-size: 18px;
	}
	
	.fire {
		padding-left: 1.156rem;
	}
	
	.p-title {
		display: inline-block;
	}
	
	.abstract {
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 3;
		-webkit-box-orient: vertical;
		padding-left: 15px;
		text-indent: 2em;
		color: #7D7D7D;
	}
.abstract[data-v-82b7485c] {
    font-size: 0.837333rem;
    color: #000000;
    overflow: scroll;
    line-height: 1.269333rem;
    position: relative;
}
.abstract:after {
  content: '...';
  text-align: right;
  position: absolute;
  bottom: 0;
  right: 0;
  width: 10%;
  height: 1.8em;
  background: linear-gradient(to right, rgba(255, 255, 255, 0), rgba(255, 255, 255, 1) 50%);
}
	
	.icon {
		height: 18.812rem;
	}

</style>