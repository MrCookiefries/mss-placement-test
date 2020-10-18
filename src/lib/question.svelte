<script lang="ts">
import { createEventDispatcher } from "svelte";

    export let question;
    
    function shuffle(arr) {
        let newArr = [];
        let num;
        while (arr.length) {
            num = Math.floor(Math.random() * arr.length);
            newArr.push(arr.splice(num, 1));
        }
        return newArr;
    }

    $: answers = shuffle([question.correct, question.option1, question.option2, question.option3]);
    let selection;
    $: disabled = !selection;
    const dispatch = createEventDispatcher();

    function makeSelection(choice) {
        if (choice === selection) {
            selection = "";
        } else {
            selection = choice;
        }
    }

    function next() {
        dispatch("continue", selection);
        selection = "";
    }
</script>

<style lang="less">
    @colors: {
        main: hsla(175, 100%, 72%, 1);
        accent: hsla(130, 100%, 72%, 1);
        light: hsla(0, 0%, 100%, 1);
        dark: hsla(0, 0%, 22%, 1);
    }

    .round(@input) {
        border-radius: @input;
    }

    h2 {
        font-size: 2em;
        color: @colors[main];
        text-align: center;
        margin-bottom: 1em;
    }

    div.answers {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        grid-gap: 1em;
        margin-bottom: 1em;

        p {
            border: 2px solid @colors[light];
            color: @colors[accent];
            padding: 0.5em;
            text-align: center;
            font-size: 1.25em;
            font-weight: 500;
            .round(1em);
            transition: transform ease-in-out 400ms;

            &:hover {
                cursor: pointer;
                transform: scale(0.9);
            }
        }

        p.selected {
            color: @colors[light];
            border-color: @colors[accent]
        }

        p.idk {
            grid-column: span 2
        }
    }

    div.btn {
        display: grid;
        justify-content: right;

        button {
        padding: 0.5em;
        font-size: 1.5em;
        color: @colors[main];
        border: 2px solid @colors[light];
        text-align: center;
        background-color: @colors[dark];
        .round(1em);
        transition: transform ease-in-out 400ms;

            &:disabled {
                display: none;
            }

            &:hover {
                color: @colors[light];
                border-color: @colors[main];
                cursor: pointer;
                transform: scale(0.9);
            }
        }
    }

    @media screen and (max-width: 600px) {
        h2 {
            font-size: 1.25em;
        }

        div.answers p {
            font-size: 1em;
            padding: 0.25em;
        }

        div.btn {
            button {
                font-size: 1.25em;
                padding: 0.25em;
            }
        }
    }
</style>

<h2>
    {question.question}
</h2>
<div class="answers">
    {#each answers as answer}
        <p class:selected={selection === answer} on:click="{() => makeSelection(answer)}">
            {answer}
        </p>
    {/each}
    <p class:selected={selection === question.idk} class="idk" on:click="{() => makeSelection(question.idk)}">
        {question.idk}
    </p>
</div>
<div class="btn">
    <button on:click="{() => next()}" type="button" {disabled}>
        Continue
    </button>
</div>
