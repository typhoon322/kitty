<template>
	<div class="container">
		<div class="header" >
			<div class="logo"></div>
			<div class="nav">
					<div class="nav_wrapper"><p class="nav_item">摄影</p></div>
					<div class="nav_wrapper"><p class="nav_item">设计</p></div>
					<div class="nav_wrapper"><p class="nav_item">视频</p></div>
					<div class="nav_wrapper"><p class="nav_item">日志</p></div>
					<div class="nav_wrapper"><p class="nav_item">关于</p></div>
			</div>
			<div class="menu_icon"></div>
		</div>
		<div class="content">
			<div class="avatar"></div>
			<div class="text_wrapper">
				<p>无论你怎么拉都看不到眼睛的</p>
				<p>随便拉 无所谓啦</p>
				<p>就酱啦</p>
        <p>{{index.greeting}}</p>
        <div v-for="image in index.images" :key="image._id">
          <img class="pics"  :src="`${image.url}?imageView2/0/w/1280/h/1280/q/94
`"/>
          <p>{{image.title}}</p>
        </div>
			</div>
		</div>
		<div class="end">00<br><br><br>你真无聊</div>
	</div>
</template>
<script>
import Vue from 'vue';
import VueResource from 'vue-resource';
Vue.use(VueResource);

const timeoutErr = {
  code: 1,
  msg: '请求超时',
};
const catchErr = {
  code: 1,
  msg: '网络异常',
};
const timeOut = 15;
const requestHeaders = {
  'Accept': 'application/json',
  'Content-Type': 'application/json',
};

export default {
  data() {
    return {
      index : {
        images: [],
      },
    };
  },
  created() {
    console.log('created');
    this.fetch();
  },
  methods: {
    fetch() {
      // const baseUrl = '192.168.1.3:3333';
      // const path = '/index';
      // const requestUrl = `${baseUrl}${path}`;
      // this.doGet(requestUrl).then(res => {
      //   console.log(res);
      //   if (res) {
      //     this.index = res;
      //   }
      // });
      return Vue.http.get('http://111.230.249.146:3077/index')
      .then((data) => {
        console.log(data);
        if (data.status === 200) {
          this.index =  data.body.data;
        }
      });
    },

    timerPromisefy(delay) {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(timeoutErr);
        }, delay * 1000);
      });
    },
    doGet(path) {
      console.log('path: '+path);
      return Promise.race([
        this.timerPromisefy(timeOut),
        new Promise((resolve, reject) => {
          fetch(path, {
            method: 'GET',
          }).then(response => response.json(),
          ).then((json) => {
            resolve(json);
          }).catch((err) => {
            reject(catchErr);
          });
        }),
      ]).then(value => value).catch(err => err);
    },
  },

}
</script>
<style lang="less">
body {
  height: 100%;
  background-color: #fff;//#002325 //#000f10
  max-width: 640px;
  min-width: 320px;
  margin: 0 auto;
}
.container{
	margin: 0;
	padding: 0;
	background-color: #000f10;
	.header {
		background-color: #002325;
		.nav {
			display: flex ;
			width: 70%;
			height: 50px;
			position: relative;
			margin-left: 50px;
			margin-right: 50px;
			.nav_wrapper{
				position: relative;
				width: 20%;
				text-align: center;
				.nav_item{
					padding: 12px 0;
					font-size: 12px;
					color: #fff;
				}
			}
		}
		.logo {
			position: absolute;
		  height: 50px;
		  width: 50px;
		  background-image: url('../assets/images/logo.jpeg');
		  background-size: 100%;
		  background-repeat: no-repeat;
		}
		.menu_icon {
			position: absolute;
			right: 0;
			top: 0;
		  height: 50px;
		  width: 50px;
		  background-image: url('../assets/images/icon_menu.png');
		  background-size: 100%;
		  background-repeat: no-repeat;
		}
	}
	.content {
		width: 100%;
		height: 70000px;
		color: #fff;
		text-align: center;
		.avatar {
		  margin: 0 auto;
		  height: 200px;
		  width: 200px;
		  background-image: url('../assets/images/avatar.jpg');
		  background-size: 100%;
		  background-repeat: no-repeat;
    }
    .pics {
      width: 100%;

    }
	}
	.end {
		color: #fff;
		text-align: center;
		font-size:40px;
	}

}
</style>
