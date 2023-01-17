<script>
  import messageSender from '$lib/images/useravatar.png';
  export let prompt = '';
  console.log("message props", prompt)
</script>

<div class="chat-content-wrapper">
  <img src={messageSender} width="40" height="40" alt="message_sender" />
  <div class="message_content_wrapper">
    <p>{prompt}</p>
  </div>
</div>

<style>
  .chat-content-wrapper {
    width: 70%;
    display: flex;
    flex-direction: row;
    margin-bottom: 1rem;
  }
  .message_content_wrapper {
    background-color: rgba(0, 19, 41, 1);
    border: 1px solid rgba(47, 131, 228, 1);
    border-radius: 5px;
    margin-left: 0.75rem;
    padding: 10px;
    color: white;
  }
  img {
    border-radius: 50%;
  }
  p {
    color: white;
    font-size: 14px;
    margin: 0;
    padding: 0;
    width: 100%;
    max-width: 300px;
  }
</style>