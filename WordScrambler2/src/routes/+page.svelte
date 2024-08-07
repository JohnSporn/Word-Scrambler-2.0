<script lang="ts">
	import { onMount } from "svelte";
    import "../app.css";

    let fileContent: string[] = [];
    let scrambled = [];
    let answerLength: string[] = [];
    let solve = '';

    onMount(async () => {
        try {
            const response = await fetch('src/data/words.json');
            if(!response.ok) {
                throw new Error(`Response status: ${response.status}`);
            }
            fileContent = await response.json();  
        }
        catch (error: any) {
            console.error(error.message);
        }
        let random = Math.floor(Math.random() * fileContent.length);
        let word = fileContent[random];
        let wordArray = word.split('');

        for(let i = 0; i < word.length; i++) {
            let next = Math.floor(Math.random() * wordArray.length);
            scrambled.push(wordArray[next]);
            wordArray.splice(next, 1);
        }
        solve = scrambled.join('');

        answerLength.length = scrambled.length;
    });
</script>

<section class="container mx-auto text-center">
    <div class="py-3">
        <h1 class="text-7xl font-bold">Word Scrambler 2.0</h1>
        <p class="text-3xl">Directions: Descramble the word.</p>
    </div>
    <div class="py-3">
        <h1 class="text-5xl">{solve}</h1>
    </div>
    <div class="flex flex-row flex-wrap justify-center gap-3">
        {#each answerLength as item}
            <input class="border-2 outline outline-1 w-14 h-20 shadow-lg" bind:value={item} maxlength="1" />
        {/each}
    </div>
</section>