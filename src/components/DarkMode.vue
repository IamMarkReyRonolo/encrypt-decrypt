<template>
	<div class="darkMode">
		<h1>Shift-Cypher Decrypt</h1>
		<div class="inputField">
			<v-textarea
				filled
				color="white"
				v-model="text"
				class="white"
				hide-details=""
				placeholder="Message"
			></v-textarea>
			<br />
			<v-text-field
				filled
				color="white"
				placeholder="Key"
				type="number"
				class="white"
				hide-details=""
				v-model="shiftKey"
			></v-text-field>
		</div>
		<br />
		<div class="icon">
			<v-btn color="white" x-large @click="decrypt">Decrypt</v-btn>
		</div>
		<div class="decryptedMessage" v-if="showDecrypted">
			{{ decrypted }}
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				text: "",
				decrypted: "",
				showDecrypted: false,
				shiftKey: 0,
				alphabet: "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ",
			};
		},

		methods: {
			decrypt() {
				this.decrypted = "";
				let key = +this.shiftKey;
				for (let i = 0; i < this.text.length; i++) {
					let character = this.text.charAt(i);
					if (character == " ") {
						this.decrypted += " ";
					} else {
						if (this.alphabet.indexOf(character) < key) {
							let index = (this.alphabet.indexOf(character) + 52 - key) % 52;
							this.decrypted += this.alphabet.charAt(index);
						} else {
							let index = (this.alphabet.indexOf(character) - key) % 52;
							this.decrypted += this.alphabet.charAt(index);
						}
					}
				}
				this.showDecrypted = true;
			},
		},

		watch: {
			text() {
				this.showDecrypted = false;
			},
			shiftKey() {
				this.showDecrypted = false;
			},
		},

		// watch: {
		// 	text() {
		// 		this.decrypted = "";
		// 		for (let i = 0; i < this.text.length; i += 3) {
		// 			let numbers = [];

		// 			numbers.push(this.text.charCodeAt(i) - 65);
		// 			numbers.push(this.text.charCodeAt(i + 1) - 48);
		// 			numbers.push(this.text.charCodeAt(i + 2) - 33);

		// 			let result =
		// 				numbers[0].toString() +
		// 				numbers[1].toString() +
		// 				numbers[2].toString();
		// 			let ascii = (parseInt(result) - 2001) / 16 + 1;
		// 			this.decrypted += String.fromCharCode(ascii);
		// 		}
		// 	},
		// },
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

	.decryptedMessage {
		padding: 40px;
		font-weight: 500;
	}
</style>
