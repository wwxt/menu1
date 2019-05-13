<template>
	<div class="search">
		<form>
	<van-search ref="search" class="search" placeholder="输入商品名称关键字" show-action  v-model="count"  >
		<div slot="action" @click="search"><van-icon name="search" size="20px"  /></div>
	</van-search>
		</form>
		<div class="table" v-show="isHow" >
			<van-row>
				<van-col span="11" offset="1" v-for="(item,index) in serchData" :key="index" @click.native="goDaint({name:'Detail',params:{pid:item.id}})">
					<div><img class= " auto-img" :src="item.images.small"/></div>
					<div>{{item.name}}</div>
				</van-col>
			</van-row>
		</div>
		<!--<van-button plain hairline type="danger" class="btn" @click="goIndex"  >退出搜索</van-button>
		<van-button plain hairline type="danger" class="btn1" @click="goDaint({name:'Index'})">返回主页</van-button>
		<van-button plain hairline type="danger" class="btn2" @click="goDaint({name:'Collect'})">返回收藏</van-button>-->
	</div>
</template>

<script>
	import {Search,Icon,Toast,Button} from 'vant'
	export default {
		name:"Search",
		components:{
			[Search.name]:Search,
			[Icon.name]:Icon,
			[Toast.name]:Toast,
			[Button.name]:Button,
		},
		data(){
			return{
				isHow:false,
				count:"",
				serchData:[],
			}
		},
		methods:{
			search(){
				this.isHow=false;
				if (this.count=='' || this.count==undefined) {
					this.$toast("搜索不能为空")
					return;
				}
				this.serchData=[];
				var match = new RegExp('(' + this.count + ')', 'img');
			var productDats=JSON.parse(localStorage.getItem("products")).products;
			
			productDats.forEach(v=>{
				if(match.test(v.name)){
					this.serchData.push(v);
					this.isHow=true;
				}
				if (!match.test(v.name)) {
					this.$toast("未能搜索到相关信息！")
					this.count='';
				}
				
			})
		},
			goDaint(path){
				this.$router.push(path)
			},
//			goIndex(){
//				this.$router.go(-1)
//			},
		}
	}
</script>

<style scoped="scoped">
	.search{
		position: sticky;
		top: 0;
		z-index: 100;
	}
	.van-search__content{
		border-radius: 18px;
	}
	.table{
		margin-top: 0.781rem;
	}
	.btn{
		position: fixed;
		bottom: 0;
		right: 0;
	}
	.btn1{
		position: fixed;
		bottom: 0;
		left: 7.812rem;
	}
	.btn2{
		position: fixed;
		bottom: 0;
		left: 0;
	}
</style>