<template>
	<div class="collect">
	<van-nav-bar title="收藏菜谱"/>
	<van-row v-show="istrue">
		<van-col class="nav-img" span="11" v-for="(item,index) in collects" 
@touchstart.native="gotouchstart" @touchmove.native="gotouchmove" @click.native="goIndex({name: collects[index].router,params:{pid:collects[index].id}})" :key="index">
			<div class="colse-box " >
				<img class="auto-img" :src="collects[index].imgs"/>
			</div>
			
			<span>{{collects[index].name}}</span>
			<div class="mistake" v-show="isOpen" @click.stop='del(index)' ><van-icon name="close" /></div>
		</van-col>
	</van-row>
	<div class="text" v-show="isfalse">清先登陸</div>
		<div class="text" @click="goIndex({name:'Index'})"><span >去收藏更多</span></div>	
		

	</div>
</template>

<script>
	import { NavBar,Icon, Toast} from 'vant';
	export default{
		name:"Collect",
		data(){
			return{
				collects:null,
				isOpen:false,
				timeOutEvent:0,
				userLoginStatus:null,
				istrue:false,
				isfalse:false,
			}
		},
		components:{
			[NavBar.name]:NavBar,
			[Icon.name]:Icon,
			[Toast.name]:Toast,
		},
		methods:{
			goIndex(path){
				this.$router.push(path)
//				console.log("aaaa")
			},
			gotouchstart(){
					
					
//				clearTimeout(timeOutEvent);//清除定时器
					
				this.timeOutEvent = setTimeout(()=>{
//执行长按要执行的内容，
			this.timeOutEvent = 0;

			this.isOpen=true

			},500);//这里设置定时
				},
//手释放，如果在500毫秒内就释放，则取消长按事件，此时可以执行onclick应该执行的事件
				gotouchend(){
					clearTimeout(this.timeOutEvent);
						if(this.timeOutEvent!=0){
							for(var i=0;i<this.collects.length;i++){
						this.$router.push({name:this.collects[i].router, 					params:{pid:this.collects[i].id}})
				}
		
	
		//这里写要执行的内容（尤如onclick事件）
		}
			},
//如果手指有移动，则取消所有事件，此时说明用户只是要移动而不是长按 
				gotouchmove(){
				clearTimeout(this.timeOutEvent);//清除定时器
				this.timeOutEvent = 0;
			},
			del(index){
				var product = index == undefined ? this.collects.splice(0) : this.collects.splice(index, 1);

				var collect=JSON.parse(localStorage.getItem("collects"));
				
				for (var i=0;i<collect.length;i++) {
					if (product.id == collect[i].id) {
						collect.splice(i,1)	
						break;
					}
				}

				localStorage.setItem("collects",JSON.stringify(this.collects));
			}

		},
		created(){
			
											
//				獲取登陸信息,如果登陸過,就可以進入,如果沒有就提示先登陸在選擇查看我的
				let userLogin = localStorage.getItem('userLogin');

//				console.log(span1[0].style.backgroundColor)
				this.userLoginStatus = userLogin == undefined ? null : JSON.parse(userLogin);
				if (!this.userLoginStatus) {
				//如果未登录, 提示用户登录
//				this.$toast('您尚未登录');
					this.isfalse=true;
					this.istrue=false;
					alert("先去登錄吧！")
				} else if(this.userLoginStatus.loginStatus) {
					var collect=JSON.parse(localStorage.getItem("collects"));
					this.collects=collect
					this.istrue=true;
					this.isfalse=false;
				}


			
		}
	}
</script>

<style scoped="scoped">
	.nav-img{
		margin-right: 0.656rem;
		margin-bottom:1.656rem;
		text-align: center;
	}
	.text{
		text-align: center;
		margin-top: 1.781rem;
	}
	.colse-box{
		/*position: relative;*/
		/*right: -71px;
		top: -130px;*/
	}
	.mistake{
		position: relative;
		right: -72px;
		top: -152px;
		font-size: 1.812rem;
		/*height: 1.812rem;*/
		color: #C92407;
	}
	.van-nav-bar {
    height: 2.22667rem;
    line-height: 2.22667rem;
}
</style>