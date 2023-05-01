<script>
	import Card from "./Card.svelte";
	import Modal from "./Modal.svelte";
	import Bookmark from "./Bookmark.svelte";

  	let optionData = { pwLength: 0, pwUpperCase: false, pwLowerCase: false, pwSymbol: false, pwNumber: false }

	const upperCase = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
	const lowerCase = "abcdefghijklmnopqrstuvwxyz";
	const symbols = "!@#$%^&*()_+=-[]{}/?.,<>;:p`~";
	const numbers = "1234567890";
	let userPassword = "";
	let showModal = false;

	const optionsCheck = () => {
		let initialPw = "";

		if (optionData.pwUpperCase) {initialPw += upperCase};
		if (optionData.pwLowerCase) {initialPw += lowerCase};
		if (optionData.pwSymbol) {initialPw += symbols};
		if (optionData.pwNumber) {initialPw += numbers};

		userPassword = generatePassword(optionData.pwLength, initialPw);
	}

	const generatePassword = (l, initialPw) => {
		let pwGenerated = ""
		for (let i = 0; i < l; i++) {
			pwGenerated += initialPw.charAt(
				Math.floor(
					Math.random() * initialPw.length
				)
			)
		}
		return pwGenerated;
	}

	const copyPassword = () => {
		let copyText = document.getElementById("pw");
		copyText.select();
		navigator.clipboard.writeText(copyText.value);
		toggleModal();
	}

	const toggleModal = () => {
		showModal = !showModal;
	}

</script>

<Modal {showModal} on:click = {toggleModal}>Text copied!</Modal>
<main>
	<Bookmark />
	<Card>
		<img src="./img/title.svg" alt="Password Generator Title">
		<div class="card-header">
			<input type="text" id = "pw" bind:value={userPassword}> <!-- pw means password -->
			<button class="copy-pw" on:click={copyPassword}>Copy</button>
		</div>
		<div class="card-body">
			<div class="form-option">
				<label for="pw-length">Password Length</label>
				<input type="number" bind:value={optionData.pwLength} min="5" max="30">
				<span class="checkmark"></span>
			</div>
			<div class="form-option">
				<label for="pw-uppercase">Uppercase Inclusion</label>
				<input type="checkbox" bind:checked={optionData.pwUpperCase}>
				<span class="checkmark"></span>
			</div>
			<div class="form-option">
				<label for="pw-lowercase">Lowercase Inclusion</label>
				<input type="checkbox" bind:checked={optionData.pwLowerCase}>
				<span class="checkmark"></span>
			</div>
			<div class="form-option">
				<label for="pw-symbol">Symbol Inclusion</label>
				<input type="checkbox" bind:checked={optionData.pwSymbol}>
				<span class="checkmark"></span>
			</div>
			<div class="form-option">
				<label for="pw-number">Number Inclusion</label>
				<input type="checkbox" bind:checked={optionData.pwNumber}>
				<span class="checkmark"></span>
			</div>
		
			<button class = "gen-btn" on:click = {optionsCheck} id="generate">Generate Password</button>
		</div>
	</Card>
</main>

<style>
	img {
		width: 250px;
		margin: -20px 0px;
	}

	.form-option {
		display: grid;
		grid-template-columns: 200px 50px;
		align-items: center;
		padding: 10px 0;
		border-bottom: 2px solid #0066b2;
	}

	.card-body input {
		padding: 3px 5px;
	}

	.copy-pw {
        border: 0;
        border-radius: 6px;
        cursor: pointer;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.15);
        padding: 7px 20px;
		margin: 10px 0;
		background-image: linear-gradient(120deg, #0066b2, #0276c4);
        color: #fff;
    }

	.gen-btn {
		margin-top: 20px;
	}

	button {
        border: 0;
        border-radius: 6px;
        cursor: pointer;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.15);
        padding: 10px 20px;
		margin: 10px 0;
		background-image: linear-gradient(120deg, #0066b2, #0276c4);
        color: #fff;
    }

	button:hover {
        box-shadow: none; 
    }

	button:focus {
		outline: max(2px, 0.15em) solid #108ff0;
  		outline-offset: max(2px, 0.15em);
	}

    button:active {
        box-shadow: none; 
		background-image: none;
        background-color: #fff;
        color: #0066b2;
    }
</style>