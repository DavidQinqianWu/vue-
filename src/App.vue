<template>
	<div></div>
</template>

<script lang="ts">
import { ref } from "vue";

export default {
	setup() {
		const nowTime = ref("00:00:00");
		const getNowTime = () => {
			const now = new Date();
			const hour = 0;
			const min = 0;
			const second = 0;
			nowTime.value = hour + ":" + min + ":" + second;
			setTimeout(getNowTime, 1000);
		};
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
