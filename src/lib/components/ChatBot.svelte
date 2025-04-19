<script lang="ts">
  import { onMount } from 'svelte';
  
  let showChatBubble = true;
  let showChatDialog = false;
  let userMessage = '';
  
  function closeChatBubble() {
    showChatBubble = false;
  }
  
  function toggleChatDialog() {
    showChatDialog = !showChatDialog;
    showChatBubble = false;
  }
  
  function closeChatDialog() {
    showChatDialog = false;
  }
  
  function sendMessage() {
    if (userMessage.trim() !== '') {
      // Here you would normally process the message and get a response
      userMessage = '';
    }
  }
  
  function getCurrentDate() {
    const now = new Date();
    const months = [
      'января', 'февраля', 'марта', 'апреля', 'мая', 'июня', 
      'июля', 'августа', 'сентября', 'октября', 'ноября', 'декабря'
    ];
    return `${now.getDate()} ${months[now.getMonth()]}`;
  }
  
  onMount(() => {
    // Any initialization code can go here
  });
</script>

<div class="chat-bot">
  {#if showChatBubble}
    <div class="chat-bubble">
      <span class="close-bubble" on:click={closeChatBubble}>&times;</span>
      Привет! Я - физик,<br>твой виртуальный помощник
    </div>
  {/if}
  <div class="bot-icon" on:click={toggleChatDialog}>
    <img src="/chatbot head.svg" alt="Чат-бот" />
  </div>
</div>

{#if showChatDialog}
  <div class="chat-dialog-overlay">
    <div class="chat-dialog">
      <div class="chat-header">
        <div class="chat-header-left">
          <img src="/chatbot head.svg" alt="Физик" class="chat-avatar" />
          <h3>Физик чат-бот</h3>
        </div>
        <div class="chat-header-right">
          <button class="settings-button">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="3"></circle>
              <path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"></path>
            </svg>
          </button>
          <button class="close-dialog" on:click={closeChatDialog}>&times;</button>
        </div>
      </div>
      
      <div class="chat-divider"></div>
      
      <div class="chat-date">
        {getCurrentDate()}
      </div>
      
      <div class="chat-messages">
        <div class="message bot">
          <div class="message-sender">Физик</div>
          <div class="message-content">
            Привет! Я - физик,<br>
            твой виртуальный помощник<br>
            С чем тебе помочь сегодня?<br>
            Навигация по сайту или<br>
            пересказ лекции?
          </div>
        </div>
        <!-- More messages would be added here -->
      </div>
      
      <div class="chat-input">
        <button class="voice-button">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"></path>
            <path d="M19 10v2a7 7 0 0 1-14 0v-2"></path>
            <line x1="12" y1="19" x2="12" y2="23"></line>
            <line x1="8" y1="23" x2="16" y2="23"></line>
          </svg>
        </button>
        <input 
          type="text" 
          placeholder="Ваше сообщение" 
          bind:value={userMessage}
          on:keydown={(e) => e.key === 'Enter' && sendMessage()}
        />
        <button class="send-button" on:click={sendMessage}>
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="22" y1="2" x2="11" y2="13"></line>
            <polygon points="22 2 15 22 11 13 2 9 22 2"></polygon>
          </svg>
        </button>
      </div>
    </div>
  </div>
{/if}

<style>
  /* Chat Bot */
  .chat-bot {
    position: fixed;
    bottom: 0;
    right: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    padding: 15px;
  }

  .chat-bot img {
    width: 65px;
    height: 65px;
    cursor: pointer;
  }

  .chat-bubble {
    position: absolute;
    bottom: 70px;
    right: 20px;
    background-color: #fff;
    padding: 10px 20px;
    border-radius: 18px;
    width: 320px;
    max-width: 90vw;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    font-size: 14px;
    line-height: 1.4;
    z-index: 10;
    border: 1px solid #e0e0e0;
    text-align: left;
  }

  .close-bubble {
    position: absolute;
    top: 5px;
    right: 12px;
    font-size: 20px;
    font-weight: bold;
    cursor: pointer;
    color: #aaa;
    line-height: 1;
  }

  .close-bubble:hover {
    color: #555;
  }

  .chat-bubble:after {
    content: '';
    position: absolute;
    bottom: -10px;
    right: 20px;
    width: 0;
    height: 0;
    border-left: 10px solid transparent;
    border-right: 10px solid transparent;
    border-top: 10px solid #fff;
  }
  
  /* Chat Dialog */
  .chat-dialog-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 3000;
    display: flex;
    justify-content: flex-end;
    align-items: flex-end;
  }
  
  .chat-dialog {
    width: 90%;
    max-width: 450px;
    height: 80vh;
    background-color: #f5f5f5;
    border-radius: 20px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
    margin-right: 10px;
    margin-bottom: 10px;
  }
  
  .chat-header {
    padding: 15px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #ffffff;
  }
  
  .chat-header-left {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .chat-header-left h3 {
    margin: 0;
    font-size: 18px;
    font-weight: 600;
  }
  
  .chat-avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }
  
  .chat-header-right {
    display: flex;
    align-items: center;
    gap: 15px;
  }
  
  .settings-button, .close-dialog {
    background: none;
    border: none;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #555;
  }
  
  .close-dialog {
    font-size: 24px;
    font-weight: bold;
    color: #999;
  }
  
  .chat-divider {
    height: 1px;
    background-color: #e0e0e0;
    width: 100%;
  }
  
  .chat-date {
    text-align: center;
    padding: 15px 0;
    color: #999;
    font-size: 16px;
  }
  
  .chat-messages {
    flex: 1;
    padding: 0 20px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 15px;
  }
  
  .message {
    max-width: 70%;
    border-radius: 18px;
    padding: 12px 15px;
    position: relative;
  }
  
  .message.bot {
    align-self: flex-start;
    background-color: #fff;
    border-top-left-radius: 0;
  }
  
  .message.user {
    align-self: flex-end;
    background-color: #e3f2fd;
    border-top-right-radius: 0;
  }
  
  .message-sender {
    font-weight: 600;
    margin-bottom: 5px;
    font-size: 14px;
  }
  
  .message-content {
    line-height: 1.4;
  }
  
  .chat-input {
    padding: 15px;
    display: flex;
    align-items: center;
    gap: 10px;
    background-color: #fff;
    border-top: 1px solid #e0e0e0;
  }
  
  .chat-input input {
    flex: 1;
    padding: 10px 15px;
    border: none;
    border-radius: 30px;
    background-color: #f0f0f0;
    font-size: 16px;
    outline: none;
  }
  
  .voice-button, .send-button {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: none;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    background: none;
    color: #999;
  }
  
  .send-button {
    color: #666;
  }

  @media (max-width: 768px) {
    .chat-dialog {
      width: 100%;
      height: 100%;
      max-width: 100%;
      border-radius: 0;
      margin-right: 0;
    }
  }

  .bot-icon {
    position: fixed;
    bottom: 20px;
    right: 20px;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background-color: transparent;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    z-index: 1000;
    box-shadow: none;
  }
  
  .bot-icon img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
</style> 