<script>
    import { createEventDispatcher } from "svelte";
    import Card from "./Card.svelte";
    export let item;

    const dispatch = createEventDispatcher()

    const handleDelete = (itemId) => {
        dispatch('delete-feedback',itemId)
    }
</script>

<Card>
    <div class='absolute w-10 h-10 rounded-full -top-3 -left-3 border-1 text-center bg-pink-600 text-white flex items-center justify-center'>
        {item.rating}
    </div>
    <button class='absolute top-2 right-2 cursor-pointer' on:click={()=> handleDelete(item.id)}>
        X
    </button>
    <p class='font-medium'>
        {item.text}
    </p>
</Card>