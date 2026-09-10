<script lang="ts">
	let password = '';
	let length = 10;
	let includeUppercase = true;
	let includeLowercase = true;
	let includeNumbers = true;
	let includeSpecialChars = true;

	const generatePassword = () => {
		const uppercaseChars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
		const lowercaseChars = 'abcdefghijklmnopqrstuvwxyz';
		const numberChars = '0123456789';
		const specialChars = '!@#$%^&*()-_+=~';

		let chars = '';
		if (includeUppercase) chars += uppercaseChars;
		if (includeLowercase) chars += lowercaseChars;
		if (includeNumbers) chars += numberChars;
		if (includeSpecialChars) chars += specialChars;

		let generatedPassword = '';
		for (let i = 0; i < length; i++) {
			generatedPassword += chars.charAt(Math.floor(Math.random() * chars.length));
		}
		password = generatedPassword;
	};

	const savePasswordToFile = () => {
		const fileContent = `Generated Password: ${password}`;
		const blob = new Blob([fileContent], { type: 'text/plain' });
		const url = window.URL.createObjectURL(blob);
		const a = document.createElement('a');
		a.href = url;
		a.download = 'generated_password.txt';
		document.body.appendChild(a);
		a.click();
		window.URL.revokeObjectURL(url);
		document.body.removeChild(a);
	};
</script>

<div class="wrapper">
	<img src="/logos/passcraft-serif.svg" alt="" />

	<p class="center">The easiest password generator you'll find!</p>

	<hr />

	<label class="number">
		<h3>Password Length</h3>
		:
		<input type="number" bind:value={length} min="4" max="32" />
	</label>

	<label>
		<input type="checkbox" bind:checked={includeUppercase} />
		<em>Uppercase Letters</em>
	</label>

	<label>
		<input type="checkbox" bind:checked={includeLowercase} />
		<em>Lowercase Letters</em>
	</label>

	<label>
		<input type="checkbox" bind:checked={includeNumbers} />
		<em>Numbers</em>
	</label>

	<label>
		<input type="checkbox" bind:checked={includeSpecialChars} />
		<em>Special Characters</em>
	</label>

	<button class="gen" onclick={generatePassword}>Generate Password</button>

	<button class="save" onclick={savePasswordToFile}>Save Password to File</button>

	<div class="generated">
		<h4>Your password is:</h4>
		<p class="center"><b>{password}</b></p>
	</div>
</div>

<style>
	.wrapper {
		background-color: #ffffff95;
		border-radius: 10px;
		padding: 1rem;
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
		width: 100%;
		max-width: 500px;
		box-sizing: border-box;

		& hr {
			border: none;
			border-top: 2px solid #4e4e4e;
			margin-inline: auto;
			width: 100%;
		}

		& .number {
			display: flex;
			align-items: center;
			justify-content: space-evenly;
		}

		& .center {
			text-align: center;
			color: #242424;
		}
		& label {
			display: flex;
			align-items: center;
			gap: 0.5rem;
			margin-left: 1.1rem;
			margin-bottom: 0.5rem;
			letter-spacing: 2px;
			font-family: Verdana, Geneva, Tahoma, sans-serif;
			font-size: 1rem;

			& em {
				color: #333333;
				font-weight: 500;
			}

			& h3 {
				color: #242424;
			}

			&:first-child {
				margin-bottom: -0.25rem;
				margin-left: 0;

				& input {
					border-radius: 10px;
				}
			}

			&:nth-child(5) {
				margin-bottom: 1rem;
			}
		}

		& b {
			font-size: clamp(1rem, 1.2vw, 1.3rem);
			font-weight: bold;
			word-break: break-all;
			overflow-wrap: anywhere;
			line-height: 1.4;
			padding: 0.5rem;
			display: block;
		}

		& button {
			display: block;
			color: rgb(231, 231, 231);
			border: none;
			border-radius: 5px;
			padding: 10px 24px;
			font-size: clamp(1rem, 1.25vw, 1.15rem);
			font-weight: 800;
			letter-spacing: 1px;
			cursor: pointer;
			text-align: center;
			margin-bottom: 0.5rem;

			&.gen {
				margin-top: 1.75rem;
				background-color: hsl(90, 98%, 23%);
				margin-inline: auto;

				&:hover {
					background: rgb(231, 231, 231);
					color: hsl(90, 98%, 25%);
					border: 1px solid hsl(90, 98%, 25%);
				}
			}
		}

		& .save {
			font-size: clamp(1rem, 1.25vw, 1.15rem);
			margin-inline: auto;
			background-color: hsl(231, 95%, 29%);

			&:hover {
				background: rgb(231, 231, 231);
				color: hsl(231, 95%, 34%);
				border: 1px solid hsl(231, 95%, 34%);
			}
		}

		& input[type='number'] {
			width: fit-content;
			padding: 5px;
			font-size: clamp(1rem, 1vw, 1.3rem);
			font-weight: 600;
			letter-spacing: 2px;
			text-align: center;
		}
		& input[type='checkbox'] {
			margin-right: 0.5rem;
			width: clamp(1rem, 1vw, 1.5rem);
			height: clamp(1rem, 1vw, 1.5rem);
			cursor: pointer;
			border-radius: 5px;
		}

		& .generated {
			border: 2px solid #242424;
			border-radius: 10px;

			& h4 {
				color: #7c7b7b;
				letter-spacing: 3px;
				font-family: Verdana, Geneva, Tahoma, sans-serif;

				font-size: clamp(0.9rem, 1vw, 1.1rem);
				font-weight: 200;
				text-align: center;
				margin-bottom: -1rem;
			}

			& p {
				font-family: Verdana, Geneva, Tahoma, sans-serif;
				font-size: clamp(1rem, 1.2vw, 1.3rem);
				color: #111;
			}
		}

		& img {
			width: 100%;
			max-width: 300px;
			height: auto;
			display: block;
			margin: 0 auto 1rem auto;
		}
	}

	/* Mobile responsive styles */
	@media (width <= 768px) {
		.wrapper {
			margin: 0 0.5rem;
			padding: 0.75rem;
			max-width: calc(100vw - 1rem);

			& img {
				max-width: 250px;
			}

			& b {
				font-size: clamp(0.9rem, 4vw, 1.1rem);
				line-height: 1.5;
				padding: 0.75rem 0.5rem;
				background-color: rgba(255, 255, 255, 0.8);
				border-radius: 8px;
				/* border: 1px solid #ddd; */
				margin: 0.5rem 0;
				min-height: 2.5rem;
				display: flex;
				align-items: center;
				justify-content: center;
				text-align: center;
			}

			& .center {
				margin: 0.5rem 0;
				padding: 0 0.25rem;
			}
		}
	}
</style>
