<!DOCTYPE html>
<html>
<head>
	<title>User Form</title>
	<style>
		label {
			display: block;
			margin-bottom: 5px;
		}
		input {
			display: block;
			margin-bottom: 10px;
			padding: 5px;
			border: 1px solid #ccc;
			border-radius: 3px;
			width: 250px;
			box-sizing: border-box;
		}
		button {
			padding: 10px 15px;
			background-color: #007bff;
			color: #fff;
			border: none;
			border-radius: 3px;
			cursor: pointer;
		}
	</style>
</head>
<body>
	<h1>User Form</h1>
	<form id="user-form">
		<label for="name">Name:</label>
		<input type="text" id="name" name="name" required>

		<label for="email">Email:</label>
		<input type="email" id="email" name="email" required>

		<label for="phone">Phone:</label>
		<input type="tel" id="phone" name="phone" required>

		<button type="submit">Submit</button>
	</form>

	<script>
		const form = document.querySelector('#user-form');

		form.addEventListener('submit', async (event) => {
			event.preventDefault();

			const name = document.querySelector('#name').value;
			const email = document.querySelector('#email').value;
			const phone = document.querySelector('#phone').value;

			try {
				// Check if user exists
				const user = await fetch(`https://example.com/api/getUser?email=${email}`);
				if (user.status === 200) {
					alert('User found');
				} else {
					// Create new user
					const response = await fetch('https://example.com/api/createUser', {
						method: 'POST',
						headers: {
							'Content-Type': 'application/json'
						},
						body: JSON.stringify({
							name,
							email,
							phone
						})
					});

					if (response.status === 201) {
						alert('User created successfully');
					} else {
						throw new Error('Failed to create user');
					}
				}
			} catch (error) {
				console.error(error);
				alert('An error occurred');
			}
		});
	</script>
</body>
</html>
