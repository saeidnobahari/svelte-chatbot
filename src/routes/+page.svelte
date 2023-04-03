<script>
	import avatar from '$lib/images/avatar.png';
	import MessageContent from './MessageContent.svelte';
	import UserContent from './UserContent.svelte';
	let prompt = '';
	/**
	 * @type {any[]}
	 */
	let messages = [{ prompt: '' }];
	let answers = [{ answer: '' }];

	const DEFAULT_PARAMS = {
		model: 'text-davinci-003',
		temperature: 0,
		max_tokens: 3000,
		top_p: 1,
		frequency_penalty: 0,
		presence_penalty: 0
	};
	const openai_api_key = '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';

	const sendMessage = async () => {
		if (prompt !== '') {
			messages = [...messages, { prompt }];
			let value = prompt;
			prompt = '';
			let answer = await generateAnswer(value);
			console.log("answer", answer)
			answers = [...answers, { answer: answer }];
		}
	};

	const pressEnter = (e) => {
		if (e.key == 'Enter') {
			sendMessage();
		}
	};
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<div class="chatting-wrapper">
		<div class="chat-channel-wrapper">
			<div class="contract-wrapper chat-bg-color" />
			<div class="adss-wrapper chat-bg-color" />
		</div>
		<div class="chat-page-wrapper">
			<div class="chat-header chat-bg-color">
				<div class="avatar-wrapper">
					<img src={avatar} width="78" height="78" alt="avatar" />
					<div class="profile-info-wrapper">
						<h2>Elon Musk</h2>
						<p>Created by @unely</p>
					</div>
				</div>
				<div class="action-button-wrapper">
					<svg
						width="24"
						height="24"
						viewBox="0 0 24 24"
						fill="none"
						xmlns="http://www.w3.org/2000/svg"
					>
						<path
							d="M18 8C19.6569 8 21 6.65685 21 5C21 3.34315 19.6569 2 18 2C16.3431 2 15 3.34315 15 5C15 6.65685 16.3431 8 18 8Z"
							stroke="white"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						/>
						<path
							d="M6 15C7.65685 15 9 13.6569 9 12C9 10.3431 7.65685 9 6 9C4.34315 9 3 10.3431 3 12C3 13.6569 4.34315 15 6 15Z"
							stroke="white"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						/>
						<path
							d="M18 22C19.6569 22 21 20.6569 21 19C21 17.3431 19.6569 16 18 16C16.3431 16 15 17.3431 15 19C15 20.6569 16.3431 22 18 22Z"
							stroke="white"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						/>
						<path
							d="M8.58997 13.51L15.42 17.49"
							stroke="white"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						/>
						<path
							d="M15.41 6.51001L8.58997 10.49"
							stroke="white"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						/>
					</svg>
					<svg
						width="24"
						height="24"
						viewBox="0 0 24 24"
						fill="none"
						xmlns="http://www.w3.org/2000/svg"
					>
						<path
							d="M12 13C12.5523 13 13 12.5523 13 12C13 11.4477 12.5523 11 12 11C11.4477 11 11 11.4477 11 12C11 12.5523 11.4477 13 12 13Z"
							stroke="white"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						/>
						<path
							d="M12 6C12.5523 6 13 5.55228 13 5C13 4.44772 12.5523 4 12 4C11.4477 4 11 4.44772 11 5C11 5.55228 11.4477 6 12 6Z"
							stroke="white"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						/>
						<path
							d="M12 20C12.5523 20 13 19.5523 13 19C13 18.4477 12.5523 18 12 18C11.4477 18 11 18.4477 11 19C11 19.5523 11.4477 20 12 20Z"
							stroke="white"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						/>
					</svg>
				</div>
			</div>
			<div class="chat-room chat-bg-color">
				<div class="chat-history-wrapper">
					{#each messages as message, i}
						{#if message.prompt !== ''}
							<div class="user-content-wrapper">
								<MessageContent prompt={message.prompt} />
							</div>
							{#if answers[i]}
								<div class="bot-content-wrapper">
									<UserContent prompt={answers[i].answer} />
								</div>
							{/if}
						{/if}
					{/each}
				</div>
				<div class="text-input-wrapper">
					<div class="text-input">
						<svg
							width="22"
							height="22"
							viewBox="0 0 22 22"
							fill="none"
							xmlns="http://www.w3.org/2000/svg"
						>
							<circle cx="11" cy="11" r="10.5" stroke="#2F83E4" />
							<path
								fill-rule="evenodd"
								clip-rule="evenodd"
								d="M11 6.1875C11.116 6.1875 11.2273 6.23359 11.3094 6.31564C11.3914 6.39769 11.4375 6.50897 11.4375 6.625V10.5625H15.375C15.491 10.5625 15.6023 10.6086 15.6844 10.6906C15.7664 10.7727 15.8125 10.884 15.8125 11C15.8125 11.116 15.7664 11.2273 15.6844 11.3094C15.6023 11.3914 15.491 11.4375 15.375 11.4375H11.4375V15.375C11.4375 15.491 11.3914 15.6023 11.3094 15.6844C11.2273 15.7664 11.116 15.8125 11 15.8125C10.884 15.8125 10.7727 15.7664 10.6906 15.6844C10.6086 15.6023 10.5625 15.491 10.5625 15.375V11.4375H6.625C6.50897 11.4375 6.39769 11.3914 6.31564 11.3094C6.23359 11.2273 6.1875 11.116 6.1875 11C6.1875 10.884 6.23359 10.7727 6.31564 10.6906C6.39769 10.6086 6.50897 10.5625 6.625 10.5625H10.5625V6.625C10.5625 6.50897 10.6086 6.39769 10.6906 6.31564C10.7727 6.23359 10.884 6.1875 11 6.1875Z"
								fill="white"
							/>
						</svg>
						<input
							type="text"
							bind:value={prompt}
							class="prompt-content"
							on:keypress={pressEnter}
							placeholder="Write the message..."
						/>
						<button type="button" class="send-button" on:click={sendMessage}>
							<svg
								width="16"
								height="16"
								viewBox="0 0 16 16"
								fill="none"
								xmlns="http://www.w3.org/2000/svg"
							>
								<g clip-path="url(#clip0_45_181)">
									<path
										d="M14.6667 1.33337L7.33337 8.66671"
										stroke="white"
										stroke-linecap="round"
										stroke-linejoin="round"
									/>
									<path
										d="M14.6667 1.33337L10 14.6667L7.33337 8.66671L1.33337 6.00004L14.6667 1.33337Z"
										stroke="white"
										stroke-linecap="round"
										stroke-linejoin="round"
									/>
								</g>
								<defs>
									<clipPath id="clip0_45_181">
										<rect width="16" height="16" fill="white" />
									</clipPath>
								</defs>
							</svg>
						</button>
					</div>
				</div>
			</div>
		</div>
		<div class="bot-profile-wrapper chat-bg-color" />
	</div>
</section>

<style>
	.chatting-wrapper {
		width: 100%;
		display: flex;
		flex-direction: row;
	}
	.chat-channel-wrapper {
		width: 26%;
		display: flex;
		flex-direction: column;
		margin-right: 0.75rem;
	}
	.contract-wrapper {
		width: 100%;
		height: 550px;
		border-radius: 10px;
		margin-bottom: 0.75rem;
	}
	.adss-wrapper {
		width: 100%;
		height: 240px;
		border-radius: 10px;
	}

	.chat-page-wrapper {
		width: 48%;
		display: flex;
		flex-direction: column;
	}
	.chat-header {
		position: relative;
		width: 100%;
		height: 120px;
		display: flex;
		align-items: center;
		border-radius: 10px;
		margin: 0 0 0.75rem 0;
	}
	.action-button-wrapper {
		position: absolute;
		right: 2rem;
	}
	.avatar-wrapper {
		display: flex;
		flex-direction: row;
		color: white;
		margin-left: 1.5rem;
	}
	.chat-history-wrapper {
		height: 560px;
		padding: 1rem 0.75rem;
		display: flex;
		flex-direction: column;
		overflow-y: auto;
		overflow-x: hidden;
	}
	.user-content-wrapper {
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: end;
		margin-right: 52px;
	}
	.bot-content-wrapper {
		width: 100%;
		display: flex;
		flex-direction: column-reverse;
		justify-content: flex-start;
		align-items: end;
	}
	.profile-info-wrapper {
		display: flex;
		flex-direction: column;
		justify-content: center;
		margin-left: 0.75rem;
	}
	img {
		border-radius: 50%;
	}
	h2 {
		font-size: 1.5rem;
		font-weight: bold;
		margin: 0;
	}
	p {
		line-height: 1;
		margin-bottom: 0;
	}
	/* .none-message-wrapper {
		display: flex;
		justify-content: center;
	}
	.none-message-wrapper > p {
		font-size: 18px;
		color: white;
	} */
	.chat-room {
		display: flex;
		flex-direction: column;
		width: 100%;
		height: 670px;
		position: relative;
		border-radius: 10px;
	}
	.text-input-wrapper {
		width: 100%;
		position: absolute;
		bottom: 12px;
		display: flex;
		justify-content: center;
	}
	.text-input {
		padding: 0.75rem;
		width: 90%;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: rgba(0, 19, 41, 1);
	}
	.text-input > button {
		width: 25px;
		height: 25px;
		background-color: rgba(47, 131, 228, 1);
		color: white;
	}
	input {
		all: unset;
	}
	.prompt-content {
		border: none;
		width: 90%;
		margin-left: 0.75rem;
		background-color: rgba(0, 19, 41, 1);
		color: white;
		font-size: 20px;
		border-radius: 3px;
	}
	.send-button {
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 2px;
		border: none;
		margin-left: 0.5rem;
	}
	.prompt-content:active {
		border: none;
		border-color: rgba(0, 19, 41, 1);
	}

	.bot-profile-wrapper {
		flex: 1;
		height: 802px;
		border-radius: 10px;
		margin-left: 0.75rem;
	}

	.chat-bg-color {
		background-color: rgba(47, 131, 228, 0.1);
	}

	.chat-history-wrapper::-webkit-scrollbar {
		background-color: rgba(2, 27, 59, 1);
	}
	.chat-history-wrapper::-webkit-scrollbar-thumb {
		background-color: rgba(47, 131, 228, 1);
	}
</style>
