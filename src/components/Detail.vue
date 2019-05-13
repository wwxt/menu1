<template>
	<div class="detail">
	<van-nav-bar class="nav-text" title="菜谱详情" left-text="返回" left-arrow
@click-left="onClickLeft" @click-right="onClickRight">
<van-icon ref="color" class="color" name="like" color="#DFC64B" slot="right" />
	</van-nav-bar>
	<van-row class="nav" >
		<van-col span='12' >
			<img  class= "auto-img" :src='detailProduct.images.small '/>
		</van-col>
		<van-col span='12'>
			<div class=name><p>{{detailProduct.name}}</p></div>
			<div class="sp">
				<van-rate v-model="detailProduct.value" icon="like"void-icon="like-o" @change="onRate" :readonly="isHow"/>
				<span class="sb">{{detailProduct.value}}分</span>
			</div>
		</van-col>
	</van-row>
	<van-row class="content">
		<van-col span="4">
			<div class="cai"><p>材料</p></div>
		</van-col>
		<van-col span="20" class="con">
			<div><p>{{detailProduct.materials}}</p></div>
		</van-col>
		<van-col span="4">
			<div class="cai"><p>做法</p></div>
		</van-col>
			<van-col span="20" >
			<div><p ref="practice" class="practice">{{detailProduct.desc}}</p></div>	
			</van-col>
	</van-row>
	<van-button type="danger" @click.native="onCollects">
		<div class="collect" >
			<van-icon name='like-o' class="colle"></van-icon>&nbsp;&nbsp;<span>点击收藏</span>
		</div>
	</van-button>
	</div>
</template>

<script>
	import { NavBar, Toast ,Rate,Icon,Button} from 'vant';
	
	import tool from '../lib/tool.js'
	export default{
		name:'Detail',
		components:{
			[NavBar.name]:NavBar,
			[Toast.name]:Toast,
			[Rate.name]:Rate,
			[Icon.name]:Icon,
			[Button.name]:Button,
		},
		data(){
			return{
				value:4,
				coll:0,
				isHow:false,
				detailProduct:null,
				collects:null,
				historys:[],
				userLoginStatus:null,
			}
		},
		methods: {
			onRate(){
			this.isHow=true;
			Toast.success('评分成功！');
		
			},
		onClickLeft() {
		this.$router.go(-1);
		},
		onClickRight() {
			var color =this.$refs.color;
			color.style.color="red";
				Toast('点赞+1');
				this.coll++;
				if (this.coll>=2) {
					Toast('不能重复点赞！除非您是会员。');
				}
	},
		onCollects(){
			let userLogin = localStorage.getItem('userLogin');

//				console.log(span1[0].style.backgroundColor)
				this.userLoginStatus = userLogin == undefined ? null : JSON.parse(userLogin);
				if (!this.userLoginStatus) {
    			//如果未登录, 提示用户登录
//  			this.$toast('您尚未登录');
					alert("先去登錄吧！")
    			} else if (this.userLoginStatus.loginStatus) {
						for (var i=0;i<this.collects.length;i++) {
							if (this.collects[i].id == this.detailProduct.id) {
								Toast("此菜谱加入收藏，请收藏其他")
								return
							}	
					}
					var collect={
						imgs:this.detailProduct.images.small,
						 name:this.detailProduct.name,
						 id:this.detailProduct.id,
						 router:"Detail"
					}
					this.collects.push(collect)
					var collectData=JSON.stringify(this.collects);
					localStorage.setItem("collects",collectData);
							
	
	    		}

		
		}
	},
mounted(){
var practice =this.$refs.practice;

	var text= practice.innerHTML;
practice.innerHTML=text.replace(/。/g,"。<br>")
for(var i=0;i<this.historys.length;i++){
		if (this.detailProduct.id == this.historys[i].id ) {
			console.log("已加入历史记录")
		return;
	}
}
var histroya={
			imgs:this.detailProduct.images.small,
		name:this.detailProduct.name,
		id:this.detailProduct.id,
	time:tool.format(new Date(), 'yyyy-MM-dd hh:mm:ss'),
			router:"Detail"
		};
			this.historys.push(histroya)
			localStorage.setItem("history",JSON.stringify(this.historys));
},
	created(){
			var products=JSON.parse(localStorage.getItem('products'));
			for (var i = 0; i<products.products.length;i++) {
				if (this.$route.params.pid == products.products[i].id) {
					this.detailProduct = products.products[i]
					break;
				}
			}
			
			var collectData =localStorage.getItem("collects");
		this.collects= collectData ==undefined ? [] : JSON.parse(collectData);
		var historysData=localStorage.getItem("history");
		this.historys= historysData == undefined ? [] : JSON.parse(historysData);
	}

	}
</script>

<style scoped="scoped">
	.van-nav-bar__title{
		color: #F9CC9D;
	}
	.color{
		font-size: 20px;
	}
	.name{
		text-align: center;
		font-size: 19px;
	}
	.sp{
		
		color: #FA7E3E;
		padding-left: 1.781rem;
	
	}
	.sb{
		display: inline-block;
		padding-top: 0.312rem;
		padding-left: 2.081rem;
	}
	.nav{
		padding: 0.468rem;
		margin-bottom: 0.39rem;
	}
	.content{
		margin-left: 0.625rem;
	}
	.cai{
		color: #A69F96;
	}
	.con{
		color: #FA7E3E;
	}
	.practice{
		color: #424242;
	}
	.collect{
		vertical-align: middle;
		font-size: 16px;
	}
	.van-button--normal{
		margin-left: 8.343rem;
	}
	.colle{
		font-size: 20px;
	}
	.van-nav-bar {
    height: 2.22667rem;
    line-height: 2.22667rem;
}
</style>