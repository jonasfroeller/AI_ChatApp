<script lang="ts">
	import toast, { Toaster } from 'svelte-french-toast';
	import { useChat } from 'ai/svelte';

	const { messages, handleSubmit, input } = useChat({
		api: '/chat'
	});
</script>

<Toaster />

<main class="p-8">
	<article class="mb-4 prose">
		<h1><a href="/">AI Chat App</a></h1>
	</article>

	<section class="mx-auto w-[48rem] max-w-full">
		<div class="w-full p-4 my-4 border rounded-lg indicator bg-neutral-focus border-tertiary-focus">
			<span class="indicator-item indicator-start badge badge-primary">Chat GPT</span>

			<div class="w-full overflow-auto min-h-16 max-h-96">
				{#each $messages as message}
					<div class="chat {message.role == 'user' ? 'chat-end' : 'chat-start'}">
						<div class="chat-bubble">{message.content}</div>
					</div>
				{:else}
					<div class="chat chat-start">
						<div class="chat-bubble" data-error={toast.error('something went wrong...')}>
							the chat is empty...
						</div>
					</div>
				{/each}
			</div>
		</div>

		<form
			class="flex items-start justify-center gap-2 px-4 md:container md:mx-auto"
			on:submit={handleSubmit}
		>
			<textarea
				bind:value={$input}
				class="w-full textarea textarea-primary"
				placeholder="question..."
			/>
			<button class="btn btn-primary">Send</button>
		</form>
	</section>
</main>
