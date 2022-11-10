<template>
	<div class="lightMode">
		<h1>Encrypt</h1>
		<div class="inputField">
			<v-text-field filled color="black" v-model="text"></v-text-field>
		</div>
		<div class="icon">
			<v-icon color="black" size="45">mdi-lock</v-icon>
		</div>
		<div class="encryptedMessage">
			{{ encrypted }}
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				text: "",
	      encrypted: ""
	     };
		},

		watch: {
			text(){
				
				this.encrypted = "";
				for(let i =0; i< this.text.length; i++){
				
					let ascii = this.text.charCodeAt(i);
					let result = ((ascii - 1) * 16) + 2001 + "";
					let numbers = [];
					
					numbers.push(parseInt(result[0] + result[1]))
					numbers.push(parseInt(result[2]))
					numbers.push(parseInt(result[3]))

					numbers[0] += 65;
					numbers[1] += 48;
					numbers[2] += 33

					this.encrypted += String.fromCharCode(numbers[0], numbers[1], numbers[2])
				}


			}
		}
	};
</script>

<style scoped>
	.lightMode {
		margin: 80px auto;
		text-align: center;
	}
	h1 {
		font-size: 50px;
		margin: 20px 0px;
	}

	.inputField {
		margin: auto;
		width: 400px;
	}

	.encryptedMessage {
		padding: 40px;
		font-weight: 500;
	}
</style>
