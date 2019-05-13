<template>
  <div class="test">
    <van-notice-bar
  text="欢迎大家来到这个梦幻般的网址！在这里会体验到其他地方体验不到的危险。"
  left-icon="volume-o"/>
   <button @click="addProducts">添加商品</button>
     <button @click="addTypes">添加类型</button>
     <button @click="addMenu"> 添加菜单</button>
     
   <van-button class='btn' type="danger" @click="showImagePreview(3)">危险按钮</van-button>
  </div>
 
</template>

<script>
	import { NoticeBar } from 'vant';
	
	import { ImagePreview } from 'vant';
	import products from '../data/data.js'
	import types from '../data/types.js'
	import menu from '../data/data2.js'
	const images = [
'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1554908765019&di=8cba8c02476fd3efe7772d79f9505130&imgtype=0&src=http%3A%2F%2Fpic112.nipic.com%2Ffile%2F20161021%2F20180988_102939240000_2.jpg',
  'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1554908765012&di=648143b18a33f98c6dcc3977a4bbb2be&imgtype=0&src=http%3A%2F%2Fwww.deyu.ln.cn%2Fimages%2Fo5qw46tbn4zc4yrqfz2xayljpf2w4ltdn5wq%2Fsystem%2Fpictures%2F27365415%2Foriginal%2F1439369364_640x371.jpg',
  'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1554908916791&di=ff62f9d6864c00b715758f1ed38658e6&imgtype=0&src=http%3A%2F%2Fpic.58pic.com%2F58pic%2F12%2F57%2F86%2F75Q58PICMhI.jpg',
  'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1554908916791&di=d0e0317b3d136f56df175be525ecddfe&imgtype=0&src=http%3A%2F%2Fwww.ps-xxw.cn%2Fuploadfile%2F201506%2F16%2F35133814625.jpg'
];

		
export default {
  name: 'Test',
  
  components: {
			[NoticeBar.name]: NoticeBar,
			[ImagePreview.name]: ImagePreview
		},
		
	methods: {
    showImagePreview(position, timer) {
      const instance = ImagePreview({
        images,
        asyncClose: !!timer,
        startPosition: typeof position === 'number' ? position : 0
      });
      if (timer) {
        setTimeout(() => {
          instance.close();
        }, timer);
      }
    },
    addProducts(){
    	localStorage.setItem('products',JSON.stringify(products));
    },
    addTypes(){
    	localStorage.setItem("types",JSON.stringify(types));
    },
     addMenu(){
    	localStorage.setItem("menu",JSON.stringify(menu));
    },
  }
		
}



</script>


<style   scoped>
		.btn{
			position: fixed;
			bottom: 0;
			left: 0;
		}
</style>
