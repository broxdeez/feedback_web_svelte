<script>
    import {v4 as uuidv4} from 'uuid'
    import { createEventDispatcher } from 'svelte';
	import Card from './Card.svelte';
	import RatingSelect from './RatingSelect.svelte';

    const dispatch = createEventDispatcher()

	let rating = 10;
	let text = '';
	let disabled = true;
	let message;

	const handleSelect = (e) => (rating = e.detail);

	const handleInput = () => {
		if (text.trim().length <= 10) {
			message = `Text must be at least 10 characters`;
			disabled = true;
		} else {
			message = null;
			disabled = false;
		}
	};

    const handleSubmit = () => {
        if(text.trim().length > 10){
            const newFeedback = {
                id: uuidv4(),
                text,
                rating: +rating
            }
            dispatch('add-feedback', newFeedback)

            text = ''
        }
    }
</script>

<Card>
	<header class="font-extrabold text-2xl text-center px-32">
		How would you rate your service with us?
	</header>
	<form on:submit|preventDefault={handleSubmit}>
		<RatingSelect on:rating-select={handleSelect} />

		<div class="relative flex flex-grow items-center border-2 rounded-2xl p-4 mt-9">
			<input
				on:input={handleInput}
				bind:value={text}
				class="border-none w-3/4 block focus:outline-none"
				type="text"
				name=""
				id=""
				placeholder="Tell us something that keeps you coming back"
			/>
			<button
				type="submit"
				class={disabled
					? 'absolute right-4 pr-2 bg-gray-200 text-white w-32 h-10 rounded-xl'
					: 'absolute right-4 pr-2 bg-violet-600 text-white w-32 h-10 rounded-xl'}>Send</button
			>
		</div>

		{#if message}
			<div class="text-center mt-2 text-violet-600 font-semibold">
				{message}
			</div>
		{/if}
	</form>
</Card>
