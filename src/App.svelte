<script>

	let strength = 0;
	let validations = []

	function validatePassword(e) {
		const password = e.target.value;

		validations = [
			(password.length > 5),
			(password.search(/[A-Z]/) > -1),
			(password.search(/[0-9]/) > -1),
			(password.search(/[$&+,:;=?@#]/) > -1)
		]

		strength = validations.reduce((acc, cur) => acc + cur)
	}

</script>

<style>

	form{
		--text-color: #afafaf;
		max-width: 500px;
	}

	.field {
		width: 100%;
		position: relative;
		border-bottom: 2px solid var(--text-color);
		margin: 4rem auto 1rem;
	}

	.label {
		color: var(--text-color);
		font-size: 1.2rem;
		font-weight: bold;
	}

	.input{
		outline: none;
		border: none;
		overflow: hidden;
		margin: 0;
		width: 100%;
		padding: 0.25rem 0;
		background: none;
		color: white;
		font-size: 1.2rem;
	}

	.input:invalid{
		color: tomato;
	}

	.input:valid{
		color: yellowgreen;
	}

	.field::after {
		content: "";
		position: relative;
		display: block;
		height: 4px;
		width: 100%;
		background-color: #d16dff;
		transform: scaleX(0);
		transform-origin: 0%;
		transition: transform 500ms ease;
		top: 2px;
	}

	.field:focus-within {
		border-color: transparent;
	}

	.field:focus-within::after{
		transform: scaleX(1);
	}

	.label {
		z-index: -1;
		position: absolute;
		transform: translateY(-2rem);
		transform-origin: 0%;
		transition: transform 400ms;
	}

	.field:focus-within .label,
	.input:not(:placeholder-shown) + .label{
		transform: scale(0.8) translateY(-5rem);
	}

	.strength{
		display: flex;
		height: 20px;
		width: 100%;
	}

	.bar {
		margin-right: 5px;
		height: 100%;
		width: 25%;
		transition: box-shadow 500ms;
		box-shadow: inset 0px 20px #1f1f1f;
	}

	.bar-show {
		box-shadow: none;
	}

	.bar-1{
		background: linear-gradient(to right, red, orangered);
	}

	.bar-2{
		background: linear-gradient(to right, orangered, yellow);
	}

	.bar-3{
		background: linear-gradient(to right, yellow, yellowgreen);
	}

	.bar-4{
		background: linear-gradient(to right, yellowgreen, green);
	}

	ul{
		list-style-type: none;
	}

	.content{
		display: flex;
		justify-content: center;
	}

</style>

<main class="content">
	<form>
		<div class="field">
			<input type="email" name="email" class="input" placeholder="" />
			<label for="email" class="label">Email</label>
		</div>

		<div class="field">
			<input type="password" name="password" class="input" placeholder="" on:input={validatePassword} />
			<label for="password" class="label">Password</label>
		</div>

		<div class="strength">
			<span class="bar bar-1" class:bar-show={strength > 0}></span>
			<span class="bar bar-2" class:bar-show={strength > 1}></span>
			<span class="bar bar-3" class:bar-show={strength > 2}></span>
			<span class="bar bar-4" class:bar-show={strength > 3}></span>
		</div>

		<ul>
			<li> {validations[0] ? '✅': '❌' } Must be atleast 5 characters</li>
			<li> {validations[1] ? '✅': '❌' } Must contain capital letters</li>
			<li> {validations[2] ? '✅': '❌' } Must contain a number</li>
			<li> {validations[3] ? '✅': '❌' } Must contain one of $@+,:;=?@#</li>
		</ul>
	</form>
</main>

