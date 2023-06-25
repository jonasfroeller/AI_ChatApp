<script lang="ts">
	import { useChat } from 'ai/svelte';

	const { messages, handleSubmit, input } = useChat({
		api: '/chat'
	});
</script>

<main class="p-8">
	<article class="prose mb-4">
		<h1><a href="/">AI Chat App</a></h1>
	</article>

	<section class="mx-auto w-[48rem] max-w-full">
		<div class="indicator w-full p-4 my-4 rounded-lg bg-neutral-focus border border-tertiary-focus">
			<span class="indicator-item indicator-start badge badge-primary">Chat GPT</span>

			<div class="overflow-auto min-h-16 w-full max-h-96">
				{#each $messages as message}
					<div class="chat {message.role == 'user' ? 'chat-end' : 'chat-start'}">
						<div class="chat-bubble">{message.content}</div>
					</div>
				{/each}
			</div>
		</div>

		<form
			class="md:container md:mx-auto flex justify-center items-start gap-2 px-4"
			on:submit={handleSubmit}
		>
			<textarea
				bind:value={$input}
				class="textarea textarea-primary w-full"
				placeholder="question..."
			/>
			<button class="btn btn-primary">Send</button>
		</form>
	</section>
</main>
