<template>
	<div class="my">
		<van-nav-bar title="我的"/>
		<van-row>
			<van-col offset="5" span="15">
				<div class="bj" style='background-image: url("https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1555666072658&di=58bbb9e2f034e9cad3023413efa4e8d9&imgtype=0&src=http%3A%2F%2Fwww.logo8.cn%2Fupimg%2F2014%2Ftu30upzyiu1.jpg");'>

				</div>
				<div class="login">
					<span @click="goHistory({name:'Denglu'})">登录</span> &nbsp;/&nbsp;&nbsp;<span @click="goHistory({name:'Zhuche'})">注册</span>
				</div>
			</van-col>
			<!--<van-collapse v-model="activeNames">
				<van-collapse-item name="1">
				<div slot="title">有赞微商城<van-icon name="question-o" /></div>
	 				
				 </van-collapse-item>
			</van-collapse>-->
			<van-col offset="2" span="22" class="btn" @click.native="goHistory({name:'History'})">
				<van-button type="default"><van-icon name="clock-o" /> &nbsp;历史记录</van-button>
			</van-col>
			<van-col offset="2" span="22" class="btn"@click.native="onDood">
				<van-button type="default"><van-icon name="thumb-circle-o" /> &nbsp;用着不错，赏个好评去</van-button>
			</van-col>
		</van-row>
	</div>
</template>

<script>
	import { NavBar, Collapse, CollapseItem,Icon,Button,Toast } from 'vant';
	export default{
		name:"My",
		components:{
			[NavBar.name]:NavBar,
			[Collapse.name]:Collapse,
			[CollapseItem.name]:CollapseItem,
			[Icon.name]:Icon,
			[Button.name]:Button,
			[Toast.name]:Toast,
		},
		data(){
			return {
				activeNames:'1',
			}
		},
		methods:{
			onDood(){
				Toast('请加作者vx，给他好评！');
			},
			goHistory(path){
				this.$router.push(path);
			}
		}
	}
</script>

<style scoped>
	.bj{
    height: 20.73333rem;

	background-repeat: no-repeat;
	background-position-x: -77px;
	}
	.login{
		padding-left: 3.125rem;
	}
	.btn{
		margin-top:2.562rem ;
	
	}
	.van-button--default{
		background: #DAE2EA;
	}

	.van-button--normal{
		padding-right: 6.562rem;
		font-size: 14px;
		border-radius: 2.156rem;
	}
	
.van-button {
    height: 2.17333rem;
}
.van-nav-bar {
    position: relative;
    -webkit-user-select: none;
    user-select: none;
    text-align: center;
    height: 2.22667rem;
    line-height: 2.22667rem;
    background-color: #fff;
}

</style>