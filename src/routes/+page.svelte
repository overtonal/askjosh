<h1 class="title">Ask Josh!</h1>
<script>
  import { onMount } from "svelte";
  import { base } from '$app/paths';

  let messages = [];
  let input = "";

  // simple preset responses
  function getBotResponse(message) {
    return "idk lol, anyway I have to go and play badminton";
  }

  function sendMessage() {
    if (input.trim() === "") return;

    // add user message
    messages = [...messages, { sender: "user", text: input }];

    // bot response
    const response = getBotResponse(input);
    messages = [...messages, { sender: "bot", text: response }];

    // clear input
    input = "";
  }
</script>

<!-- Main Layout with Image and Chat -->
<div class="main-layout">
  <!-- Placeholder Image -->
  <img src="{base}/osh.png" alt="Oshie Bear" class="oshie" />

  <!-- Chat Section -->
  <div class="chat-section">
    <!-- Chat Window -->
    <div class="chat-container">
      {#each messages as message}
        <div class="message {message.sender}">
          <strong>{message.sender === "user" ? "You" : "Bot"}:</strong> {message.text}
        </div>
      {/each}
    </div>

    <!-- Input Area -->
    <div class="input-container">
      <input
        type="text"
        bind:value={input}
        placeholder="Type a message..."
        on:keydown={(e) => e.key === "Enter" && sendMessage()}
      />
      <button on:click={sendMessage}>Send</button>
    </div>
  </div>
</div>

<style>
    .main-layout {
    display: flex;
    align-items: flex-start;
    gap: 2rem;
  }
  .oshie {
    object-fit: cover;
    margin-top: 1.5rem;
  }
  .chat-section {
    flex: 1;
    display: flex;
    flex-direction: column;
  }
  .chat-container {
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 1rem;
    height: 300px;
    overflow-y: auto;
    margin-bottom: 1rem;
    background: #fafafa;
  }
  .message {
    margin: 0.5rem 0;
    padding: 0.5rem;
    border-radius: 6px;
  }
  .message.user {
    background: #e0f7fa;
    text-align: right;
  }
  .message.bot {
    background: #f1f8e9;
    text-align: left;
  }
  .input-container {
    display: flex;
    gap: 0.5rem;
  }
  input {
    flex: 1;
    padding: 0.5rem;
    border-radius: 6px;
    border: 1px solid #ccc;
  }
  button {
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 6px;
    background: #1976d2;
    color: white;
    cursor: pointer;
  }
  button:hover {
    background: #1565c0;
  }
</style>
