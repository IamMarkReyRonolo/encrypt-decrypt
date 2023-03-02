<template>
	<div class="lightMode">
		<h1>Shift-Cypher Encrypt</h1>
		<div class="inputField">
			<v-textarea
				filled
				color="black"
				v-model="text"
				placeholder="Message"
			></v-textarea>

			<v-text-field
				filled
				color="black"
				placeholder="Key"
				type="number"
				v-model="shiftKey"
			></v-text-field>
		</div>
		<div class="icon">
			<v-btn color="black" dark x-large @click="encrypt">Encrypt</v-btn>
		</div>
		<div class="encryptedMessage" v-if="showEncrypted">
			<p>
				{{ encrypted }}
			</p>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				text: "",
				encrypted: "",
				showEncrypted: false,
				shiftKey: 0,
				alphabet: "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ",
			};
		},
		methods: {
			encrypt() {
				this.encrypted = "";
				for (let i = 0; i < this.text.length; i++) {
					let character = this.text.charAt(i);
					if (character == " ") {
						this.encrypted += " ";
					} else {
						let index =
							(this.alphabet.indexOf(character) + +this.shiftKey) % 52;

						this.encrypted += this.alphabet.charAt(index);
					}
				}
				this.showEncrypted = true;
			},
		},

		watch: {
			text() {
				this.showEncrypted = false;
			},
			shiftKey() {
				this.showEncrypted = false;
			},
		},

		// watch: {
		// 	text() {
		// 		this.encrypted = "";
		// 		for (let i = 0; i < this.text.length; i++) {
		// 			let ascii = this.text.charCodeAt(i);
		// 			let result = (ascii - 1) * 16 + 2001 + "";
		// 			let numbers = [];

		// 			numbers.push(parseInt(result[0] + result[1]));
		// 			numbers.push(parseInt(result[2]));
		// 			numbers.push(parseInt(result[3]));

		// 			numbers[0] += 65;
		// 			numbers[1] += 48;
		// 			numbers[2] += 33;

		// 			this.encrypted += String.fromCharCode(
		// 				numbers[0],
		// 				numbers[1],
		// 				numbers[2]
		// 			);
		// 		}
		// 	},
		// },
	};
</script>

<style scoped>
	.lightMode {
		margin: 40px auto;
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
		width: 500px;
		max-width: 500px;
		word-wrap: break-word;
		margin: 20px auto;
		padding: 40px;
		font-weight: 500;
	}
</style>
