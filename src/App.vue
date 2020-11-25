<template>
	<div>
		<img alt="Vue logo" src="./assets/logo.png" />
		<h2>欢迎光临</h2>
		<div>选择一位美女为你服务</div>
		<div>
			<button
				v-for="(item, index) in girls"
				v-bind:key="index"
				@click="selectGirlFun(index)"
			>
				{{ index }} :{{ item }}
			</button>
		</div>

		<div>你选择了{{ selectGirl }}为你服务</div>
		<button @click="overAction()">点餐完毕</button>
		<div>{{ overText }}</div>
	</div>
</template>

<script lang="ts">
import {
	onBeforeMount,
	onBeforeUpdate,
	onMounted,
	onRenderTracked,
	onRenderTriggered,
	onUpdated,
	reactive,
	ref,
	toRefs,
	watch,
} from "vue";
interface PropsI {
	girls: string[];
	selectGirl: string;
	selectGirlFun: (index: number) => void;
}
export default {
	name: "App",
	setup() {
		console.log("开始创建组件 ----setup");
		const data: PropsI = reactive({
			girls: ["大脚", "李颖", "小红"],
			selectGirl: "",
			selectGirlFun: (index: number) => {
				console.log("123");
				data.selectGirl = data.girls[index];
			},
		});
		/**
		 * 组件挂载之前执行
		 */
		onBeforeMount(() => {
			console.log("2. 组件挂载之前");
		});

		/**
		 * 组件挂载之后执行
		 */
		onMounted(() => {
			console.log("3. 组件挂载之后执行");
		});

		onBeforeUpdate(() => {
			console.log("4,在组件更新之前");
		});

		onUpdated(() => {
			console.log("5. 组件更新之后");
		});

		onRenderTracked((e1) => {
			// console.log(e1);
		});
		onRenderTriggered((e1) => {
			console.log(e1);
		});

		const refData = toRefs(data);
		const overText = ref("红浪漫");
		const overAction = () => {
			overText.value = "点餐完成|" + overText.value;
		};
		watch(overText, (newValue, oldValue) => {
			console.log(`new---->${newValue}`);
			console.log(`old---->${oldValue}`);
			document.title = newValue;
		});

		return {
			...refData,
			overText,
			overAction,
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
