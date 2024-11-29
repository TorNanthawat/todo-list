<script>
	import '../styles/global.css';
</script>

<head>
	<title>Todo List App</title>
</head>

<div class="layout">
	<header>
		<h1>Todo List Application</h1>
	</header>

	<main>
		<slot />
	</main>

	<footer>
		<p>© 2024 SvelteKit Todo List App by TorDev</p>
	</footer>
</div>

<style>
	.layout {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	header {
		background: linear-gradient(350deg, #09d1fc, #0077ff, #09d1fc, #0077ff);
		background-size: 400% 400%;
		animation: gradient 10s ease infinite;
		color: #fff;
		text-align: center;
	}

	h1 {
		font-weight: 500;
		cursor: default;
	}

	main {
		display: flex;
		flex-grow: 1;
		padding: 30px;
		background: #2d3242;
		color: #fff;
	}

	footer {
		background: linear-gradient(350deg, #09d1fc, #0077ff, #09d1fc, #0077ff);
		background-size: 400% 400%;
		animation: gradient 10s ease infinite;
		color: white;
		text-align: center;
	}

	@keyframes gradient {
		0% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0% 50%;
		}
	}
</style>
