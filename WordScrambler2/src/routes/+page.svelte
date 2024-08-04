<script lang="ts">
    let word = "guess";
    let wordArray = word.split('');
    let scrambled = [];
    let answerLength: string[] = [];

    for(let i = 0; i < word.length; i++) {
        let next = Math.floor(Math.random() * wordArray.length);
        scrambled.push(wordArray[next]);
        wordArray.splice(next, 1);
    }
    let solve = scrambled.join('');

    answerLength.length = scrambled.length;
</script>

<section>
    <div>
        <h1>Word Scrambler 2.0</h1>
        <p>Directions: Descramble the word.</p>
    </div>
    <div>
        <h1>{solve}</h1>
    </div>
    <div>
        {#each answerLength as item}
            <input bind:value={item} />
        {/each}
    </div>
</section>