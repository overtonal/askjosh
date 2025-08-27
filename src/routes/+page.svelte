<script>
	import { goto } from '$app/navigation';
	function goToChat() {
		goto('/chat');
	}
</script>

<main class="home-container">
	<h1 class="site-title">AskJosh Chatbot</h1>
	<img src="/osh.png" alt="OSH Logo" class="osh-image" />
	<button class="chat-btn" on:click={goToChat}>Go to Chat</button>
</main>

<style>
	.home-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		min-height: 80vh;
		padding: 2rem;
	}
	.site-title {
		font-size: 3rem;
		margin-bottom: 2rem;
		font-weight: 700;
		letter-spacing: 0.05em;
	}
	.osh-image {
		width: 320px;
		height: 320px;
		object-fit: contain;
		margin-bottom: 2.5rem;
		border-radius: 2rem;
		box-shadow: 0 4px 32px rgba(0,0,0,0.10);
		background: #fff;
	}
	.chat-btn {
		font-size: 1.5rem;
		padding: 1rem 2.5rem;
		border: none;
		border-radius: 1.5rem;
		background: #2d72d9;
		color: #fff;
		cursor: pointer;
		transition: background 0.2s;
		box-shadow: 0 2px 12px rgba(45,114,217,0.10);
	}
	.chat-btn:hover {
		background: #1a4e96;
	}
</style>
