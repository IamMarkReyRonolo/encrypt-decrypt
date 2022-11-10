<template>
	<div class="mainWrapper" :class="toggle_exclusive == 0 ? 'lightMode' : 'darkMode'">
		<div class="creatorDiv" @click="goToLink">
			<v-icon :color="toggle_exclusive == 0 ? 'black' : 'white'" size="40">mdi-github</v-icon>
			<h2>IamMarkReyRonolo</h2>
		</div>
    <br>
    <br>
		<div class="nav">
			<v-btn-toggle v-model="toggle_exclusive" mandatory>
				<v-btn> encrypt </v-btn>

				<v-btn> decrypt </v-btn>
			</v-btn-toggle>
		</div>
		<LightMode v-if="toggle_exclusive == 0"/>
    <DarkMode v-if="toggle_exclusive == 1"/>
	</div>
</template>

<script>
	import LightMode from "../components/LightMode.vue";
  import DarkMode from "../components/DarkMode.vue";
	export default {
		components: { LightMode, DarkMode },
		data() {
			return { toggle_exclusive: 0 };
		},

		methods: {
			goToLink() {
				window.open("https://github.com/IamMarkReyRonolo/encrypt-decrypt");
			},
		},
	};
</script>

<style scoped>
	.mainWrapper {
		height: 100vh;
		padding: 20px 40px;
	}

  .lightMode{
    background-color: #ffffff;
    color: black;
  }

  .darkMode{
    background-color: #2e2e2e;
    color: white;
  }

	.creatorDiv {
		display: flex;
		justify-content: flex-start;
		align-items: center;
	}
	.creatorDiv h2 {
		font-size: 20px;
		font-weight: 500;
		cursor: pointer;
		padding: 0px 5px;
	}

	.nav {
		width: 400px;
		margin: auto;
    text-align: center;
	}
</style>
