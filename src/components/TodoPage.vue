<template>
	<div>
		<h1 > {{ time }}</h1>
		<input type="text" id="inputItem" />
	</div>
</template>
<script >
	var nIntervId ;
	function counting(){
		nIntervId = setInterval(showTime,1000);
	}

	function showTime(){

	}
	export default{
		name: 'TodoPage',

		data(){
			return {
				time: new Date().toLocaleTimeString(),
				inputItem: '122'
			}
		}
	}
</script>