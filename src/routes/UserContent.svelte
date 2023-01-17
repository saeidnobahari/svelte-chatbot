<script>
  import messageSender from '$lib/images/avatar.png';
  export let prompt = '';
</script>

<div class="chat-content-wrapper">
  <img src={messageSender} width="40" height="40" alt="message_sender" />
  <div class="message_content_wrapper">
    <p>{prompt}</p>
  </div>
</div>

<style>
  .chat-content-wrapper {
    max-width: 70% !important;
    display: flex;
    flex-direction: row-reverse;
    margin-bottom: 1rem;
  }
  .message_content_wrapper {
    background-color: rgba(47, 131, 228, 1);
    border-radius: 5px;
    margin-left: 0.75rem;
    padding: 10px;
    color: white;
  }
  img {
    border-radius: 50%;
    margin-left: 8px;
  }
  p {
    color: white;
    font-size: 14px;
    margin: 0;
    padding: 0;
    word-wrap: break-word;
    line-break: anywhere;
    /* line-break: auto; */
  }
</style>