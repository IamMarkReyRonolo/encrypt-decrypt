<template>
	<div class="darkMode">
		<h1>Decrypt</h1>
		<div class="inputField">
			<v-text-field filled color="white" dark v-model="text"></v-text-field>
		</div>
		<div class="icon">
			<v-icon color="white" size="45">mdi-key-outline</v-icon>
		</div>
		<div class="decryptedMessage">
      {{decrypted}}
    </div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				text: "",
        decrypted: ""
      };
		},
		
		watch: {
			text(){
				
				this.decrypted = "";
				for(let i =0; i< this.text.length; i+=3){
					let numbers = [];
					
					numbers.push(this.text.charCodeAt(i) - 65)
					numbers.push(this.text.charCodeAt(i + 1) - 48)
					numbers.push(this.text.charCodeAt(i + 2) - 33)

					let result = numbers[0].toString() + numbers[1].toString() + numbers[2].toString()
					let ascii = ((parseInt(result) - 2001 )/ 16 ) + 1
					this.decrypted += String.fromCharCode(ascii)
				}


			}
		}
	};
</script>

<style scoped>
	.darkMode {
		margin: 80px auto;
		text-align: center;
    color: white;
	}
	h1 {
		font-size: 50px;
		margin: 20px 0px;
	}

	.inputField {
		margin: auto;
		width: 400px;
	}

  .decryptedMessage{
    padding:40px;
    font-weight: 500;
  }
</style>
