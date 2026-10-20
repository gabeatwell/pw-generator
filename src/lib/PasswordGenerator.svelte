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
	<img src="/logos/passcraft-serif.svg" alt="passcraft logo" />

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
		background-color: #e0e0e0;
		border-radius: 10px;
		padding: 1rem;
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
		width: 100%;
		max-width: 500px;
		box-sizing: border-box;

		@media (width <= 768px) {
			margin: 0 0.5rem;
			padding: 0.75rem;
			max-width: calc(100vw - 1rem);
		}

		& hr {
			border: none;
			border-top: 2px solid #b1afaf;
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
			color: var(--fg);
		}

		& label {
			display: flex;
			align-items: center;
			gap: 0.5rem;
			margin-left: 1.1rem;
			margin-bottom: 0.5rem;
			letter-spacing: 1px;
			font-family: Verdana, Geneva, Tahoma, sans-serif;
			font-size: 1rem;

			& em {
				color: var(--fg);
				font-weight: 500;
			}

			& h3 {
				color: var(--fg);
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

			@media (width <= 768px) {
				font-size: clamp(0.9rem, 4vw, 1.1rem);
				line-height: 1.5;
				padding: 0.75rem 0.5rem;
				border-radius: 8px;
				margin: 0.5rem 0;
				min-height: 2.5rem;
				display: flex;
				align-items: center;
				justify-content: center;
				text-align: center;
			}
		}
	}

	button {
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
			background-color: hsl(90, 98%, 22%);
			margin-inline: auto;

			&:hover {
				background: rgb(231, 231, 231);
				color: hsl(90, 98%, 25%);
			}
		}
	}

	.save {
		font-size: clamp(1rem, 1.25vw, 1.15rem);
		margin-inline: auto;
		background-color: hsl(231, 95%, 29%);

		&:hover {
			background: rgb(231, 231, 231);
			color: hsl(231, 95%, 34%);
		}
	}

	input {
		&[type='number'] {
			width: fit-content;
			padding: 5px;
			font-size: clamp(1rem, 1vw, 1.3rem);
			font-weight: 600;
			letter-spacing: 1px;
			text-align: center;
		}

		&[type='checkbox'] {
			accent-color: hsl(90, 98%, 22%);
			margin-right: 0.5rem;
			width: clamp(1rem, 1vw, 1.5rem);
			height: clamp(1rem, 1vw, 1.5rem);
			cursor: pointer;
			border-radius: 5px;
		}
	}

	.generated {
		border: 2px solid var(--fg);
		border-radius: 10px;

		& h4 {
			color: #3a3939;
			letter-spacing: 3px;
			font-family: Verdana, Geneva, Tahoma, sans-serif;
			font-size: clamp(0.9rem, 1vw, 1.1rem);
			font-weight: 600;

			text-align: center;
			margin-bottom: -1rem;
		}

		& p {
			font-family: Verdana, Geneva, Tahoma, sans-serif;
			font-size: clamp(1rem, 1.2vw, 1.3rem);
			color: #eee;
		}
	}

	img {
		width: 100%;
		max-width: 300px;
		height: auto;
		display: block;
		margin: 0 auto 1rem auto;

		@media (width <= 768px) {
			max-width: 250px;
		}
	}
</style>
