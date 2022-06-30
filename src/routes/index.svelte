<main class="main_container">
	<div class="equalize_size">
		<h1>Learn to code by watching others</h1>
		<p>See how experienced developers solve problems in real-time. Watching scripted tutorials is great, but understanding how developers this is invaluable.</p>
	</div>
	<div class="equalize_size">
		<div class="try_it_free"><b>Try it free 7 days</b> then $20/mo. thereafter</div>
		<div class="form_container">
			<form action="javascript: void(0)" class="sign_up_form" novalidate on:submit={send_form}>
				{#each form_inputs as input}
					<input type={input.type} placeholder={input.name} bind:this={input.element} on:input={() => input.valid = true} class:invalid_input={!input.valid} />
					{#if !input.valid}
						<i>{input.error_message}</i>
					{/if}
				{/each}
				<input type="submit" value="CLAIM YOUR FREE TRIAL" class="claim_button" />
			</form>
			<div class="terms_and_services_text">By clicking the button you are agreeing to our <b class="red_text">Terms and Services</b></div>
		</div>
	</div>
</main>

<script>
let form_inputs = [ // Defines what inputs should be on the form
	{
		name: "First Name",
		type: "text",
		element: null,
		valid: true,
		error_message: "First Name cannot be empty"
	},
	{
		name: "Last Name",
		type: "text",
		element: null,
		valid: true,
		error_message: "Last Name cannot be empty"
	},
	{
		name: "Email Address",
		type: "email",
		element: null,
		valid: true,
		error_message: "Looks like this is not an email"
	},
	{
		name: "Password",
		type: "password",
		element: null,
		valid: true,
		error_message: "Password cannot be empty"
	},
];

// Sends the form's data to the Developyn Contact Form API if the data is valid
const send_form = () => {
	let valid_form = true;
	for (let index = 0; index < form_inputs.length; index++) {
		const input = form_inputs[index];
		const value = input.element.value;
		if (value === "") {
			valid_form = false;
			input.valid = false;
			input.error_message = input.name + " cannot be empty";
		} else if ((input.type === "email") && !/^\w+@\w+.\w+$/.test(value)) {
			valid_form = false;
			input.valid = false;
			input.error_message = "Looks like this is not an email";
		} else input.valid = true;
	}
	form_inputs = form_inputs;
	if (valid_form) {
		const fetch_body = {
			id: "2BBBaXk9nlWATEaowPVP7gJdJGv"
		};
		form_inputs.forEach(input => fetch_body[input.name] = input.element.value);
		fetch("https://api.developyn.com/public/contact-service/send", {
			method: "POST",
			headers: {
				"x-api-key": "e6ccfc1f584a7341fdf5dd46ab9db95cf309bd78f9fcd93f1f9a73b9fa3fb007"
			},
			body: JSON.stringify(fetch_body)
		});
	}
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap");

* {
	font-family: Poppins, sans-serif;
}

b {
	font-weight: 600;
}

h1 {
	color: white;
	font-size: 3rem;
	font-weight: 700;
	line-height: 1;
	margin-bottom: 2rem;
}

input {
	border-color: rgba(0, 0, 0, 0.25);
	border-radius: 0.25rem;
	border-style: solid;
	border-width: 0.1rem;
	color: hsl(249, 10%, 26%);
	font-weight: 600;
	margin: 0.5rem;
	padding: 1rem 2.5rem;
}

p {
	color: white;
	font-weight: 400;
}

.claim_button {
	background-color: hsl(154, 59%, 51%);
	border-radius: 0.5rem;
	box-shadow: inset 0 -0.25rem rgba(0, 0, 0, 0.1);
	color: white;
	letter-spacing: 0.05rem;
	white-space: normal;
}

.form_container {
	background-color: white;
	border-radius: 0.5rem;
	box-shadow: 0 0.5rem rgba(0, 0, 0, 0.1);
	color: hsl(0, 100%, 74%);
	font-size: 0.75rem;
	font-weight: 500;
	padding: 2rem;
	text-align: right;
}

.invalid_input {
  background-image: url("icon-error.svg");
  background-position: 97.5%;
  background-repeat: no-repeat;
  background-size: 1.5rem;
  border-color: hsl(0, 100%, 74%);
  border-width: 0.2rem;
  color: hsl(0, 100%, 74%);
}

.main_container {
	align-content: center;
	align-items: center;
	background-color: hsl(0, 100%, 74%);
	background-image: url("bg-intro-desktop.png");
	display: flex;
	flex-wrap: wrap;
	flex-direction: row;
	height: 100vh;
	justify-content: center;
	padding: 0 10%;
}

.red_text {
	color: hsl(0, 100%, 74%);
}

.sign_up_form {
	display: flex;
	flex-direction: column;
}

.terms_and_services_text {
	color: hsl(246, 25%, 77%);
	text-align: center;
}

.try_it_free {
	background-color: hsl(248, 32%, 49%);
	border-radius: 0.5rem;
	box-shadow: 0 0.5rem rgba(0, 0, 0, 0.1);
	color: white;
	font-weight: 500;
	margin: 2rem 0;
	padding: 1rem 0;
	text-align: center;
}

.equalize_size {
	flex: 1 1 0;
	margin: 0 2rem;
	max-width: 100%;
}
</style>