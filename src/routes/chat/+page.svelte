<h1 class="title">Ask Josh!</h1>
<script>
  import { onMount } from "svelte";
  import { base } from '$app/paths';

  /** @type {{ sender: "user" | "bot", text: string }[]} */
  let messages = [];
  let input = "";
  let isTyping = false;

  // simple preset responses
  function getBotResponse(message) {
    return "idk lol, anyway I have to go and play badminton";
  }

  async function sendMessage() {
    if (input.trim() === "") return;

    // add user message
    messages = [...messages, { sender: "user", text: input }];
    const userInput = input;
    input = "";

    // show typing animation
    isTyping = true;
    await new Promise((resolve) => setTimeout(resolve, 1200));
    isTyping = false;

    // bot response
    const response = getBotResponse(userInput);
    messages = [...messages, { sender: "bot", text: response }];
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
    {#if isTyping}
      <div class="message bot typing">
        <strong>Bot:</strong> <span class="typing-dots"><span>.</span><span>.</span><span>.</span></span>
      </div>
    {/if}

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
  :global(body) {
    background: #f4f6fb;
    font-family: 'Segoe UI', 'Roboto', Arial, sans-serif;
    margin: 0;
    color: #222;
  }
  .main-layout {
    display: flex;
    align-items: flex-start;
    gap: 2.5rem;
    max-width: 800px;
    margin: 2.5rem auto;
    background: #fff;
    border-radius: 18px;
    box-shadow: 0 4px 32px 0 rgba(60,72,88,0.10);
    padding: 2.5rem 2rem;
  }
  .oshie {
    object-fit: cover;
    margin-top: 1.5rem;
    width: 120px;
    height: 120px;
    border-radius: 16px;
    box-shadow: 0 2px 12px 0 rgba(60,72,88,0.10);
    background: #f9fafb;
  }
  .chat-section {
    flex: 1;
    display: flex;
    flex-direction: column;
    min-width: 320px;
  }
  .chat-container {
    border: 1.5px solid #e3e7ef;
    border-radius: 12px;
    padding: 1.2rem 1rem;
    height: 320px;
    overflow-y: auto;
    margin-bottom: 1.2rem;
    background: #f8fafc;
    box-shadow: 0 1px 4px 0 rgba(60,72,88,0.04);
    font-size: 1.05rem;
  }
  .message {
    margin: 0.6rem 0;
    padding: 0.7rem 1rem;
    border-radius: 8px;
    transition: background 0.2s;
    word-break: break-word;
    box-shadow: 0 1px 2px 0 rgba(60,72,88,0.03);
  }
  .message.user {
    background: linear-gradient(90deg, #e3f0ff 0%, #eaf6ff 100%);
    text-align: right;
    align-self: flex-end;
    border-bottom-right-radius: 2px;
    border-top-right-radius: 12px;
    border-top-left-radius: 12px;
    border-bottom-left-radius: 12px;
  }
  .message.bot {
    background: linear-gradient(90deg, #f3f6e7 0%, #f8fbe9 100%);
    text-align: left;
    align-self: flex-start;
    border-bottom-left-radius: 2px;
    border-top-right-radius: 12px;
    border-top-left-radius: 12px;
    border-bottom-right-radius: 12px;
  }
  .message.typing {
    font-style: italic;
    color: #888;
    background: #f5f5f5;
    box-shadow: none;
  }
  .typing-dots span {
    animation: blink 1.2s infinite both;
    font-size: 1.2em;
    opacity: 0.5;
    margin-right: 2px;
  }
  .typing-dots span:nth-child(2) {
    animation-delay: 0.2s;
  }
  .typing-dots span:nth-child(3) {
    animation-delay: 0.4s;
  }
  @keyframes blink {
    0%, 80%, 100% { opacity: 0.2; }
    40% { opacity: 1; }
  }
  .input-container {
    display: flex;
    gap: 0.7rem;
    align-items: center;
  }
  input {
    flex: 1;
    padding: 0.7rem 1rem;
    border-radius: 8px;
    border: 1.5px solid #d1d9e6;
    font-size: 1.05rem;
    background: #f9fafb;
    transition: border 0.2s;
  }
  input:focus {
    outline: none;
    border-color: #1976d2;
    background: #fff;
  }
  button {
    padding: 0.7rem 1.3rem;
    border: none;
    border-radius: 8px;
    background: linear-gradient(90deg, #1976d2 0%, #2196f3 100%);
    color: white;
    font-weight: 600;
    font-size: 1.05rem;
    cursor: pointer;
    box-shadow: 0 1px 4px 0 rgba(60,72,88,0.08);
    transition: background 0.2s, box-shadow 0.2s;
  }
  button:hover {
    background: linear-gradient(90deg, #1565c0 0%, #1976d2 100%);
    box-shadow: 0 2px 8px 0 rgba(60,72,88,0.12);
  }
  .title {
    text-align: center;
    font-size: 2.2rem;
    font-weight: 700;
    margin-bottom: 2.2rem;
    color: #1976d2;
    letter-spacing: 1px;
    text-shadow: 0 2px 8px rgba(60,72,88,0.08);
  }
</style>
