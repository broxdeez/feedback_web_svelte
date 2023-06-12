<script>
	import FeedbackList from './components/FeedbackList.svelte';
	import FeedbackStats from './components/FeedbackStats.svelte';
	import FeedbackForm from './components/FeedbackForm.svelte';

	let feedback = [
		{
			id: 1,
			rating: 10,
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.'
		},
		{
			id: 2,
			rating: 9,
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.'
		},
		{
			id: 3,
			rating: 8,
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.'
		}
	];

	$: count = feedback.length
	$: average = feedback.reduce((total, next)=> total + next.rating, 0) / count

	const addFeedback = (e) => {
		const newFeedback = e.detail;
		feedback = [newFeedback, ...feedback]
	}

    const deleteFeedback = (e) => {
        const itemId = e.detail
        feedback = feedback.filter((item) => item.id != itemId)
    }
</script>


    
<main class='container max-w-3xl mx-auto px-15 py-20'>
	<FeedbackForm on:add-feedback={addFeedback} />
	
	<FeedbackStats {count} {average} />
	<FeedbackList {feedback} on:delete-feedback={deleteFeedback} />
</main>


<style>
</style>
