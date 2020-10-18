<script lang="ts">
import Question from "./question.svelte";
import Level from "./level.svelte";

    let promiseError = false;
    let isTesting = true;
    const reader = require("g-sheets-api");
    const readerOptions = {
        sheetId: "1l4YvHqJresTVNRittIt8n__wq0Fw_gbQGl2dgeT_Qkk",
        returnAllResults: false
    };
    let index: number;
    let question;
    let quiz;
    let level = 1;

    let promise = reader(readerOptions, test => {
        test.forEach(e => {
            e.status = "unanswered";
        });
        quiz = test;
        nextQuestion();

    }, error => {
        promiseError = true;
    });

    function nextQuestion() {
        let unansweredQuestions = [];
        getLevelQuestions(level, quiz).forEach(question => {
            question.status === "unanswered" ? unansweredQuestions.push(question): "";
        })
        index = getNum(unansweredQuestions.length);
        question = unansweredQuestions[index];
    }

    function getNum(range) {
        return Math.floor(Math.random() * range);
    }

    function getLevelQuestions(num: number, test) {
        let questions = [];
        test.forEach(e => {
            if (e.level == num) {
                questions.push(e);
            }
        });
        return questions;
    }

    function continueTest(e) {
        if (e.detail[0] === question.correct) {
            question.status = "correct";
        } else {
            question.status = "incorrect";
        }
        navigation();
    }

    function checkLevel(num: number) {
        let stats = {
            right: 0,
            wrong: 0,
            unanswered: 0
        };
        getLevelQuestions(num, quiz).forEach(question => {
            switch(question.status) {
                case "correct": stats.right++; break;
                case "incorrect": stats.wrong++; break;
                default: stats.unanswered++; break;
            }
        })
        return stats;
    }

    function navigation() {
        let levelStats = checkLevel(level);
        if (levelStats.unanswered <= getLevelQuestions(level, quiz).length / 2) {
            if (levelStats.right > levelStats.wrong) {
                if (level === 4) {
                    level++;
                    isTesting = false;
                } else {
                    level++;
                    nextQuestion();
                }
            } else {
                isTesting = false;
            }
        } else {
            nextQuestion();
        }
    }
</script>

<style lang="less">
    @colors: {
        main: hsla(175, 100%, 72%, 1);
        accent: hsla(130, 100%, 72%, 1);
        light: hsla(0, 0%, 100%, 1);
        dark: hsla(0, 0%, 22%, 1);
    }

    h2 {
        text-align: center;

        &.error {
            color: @colors[main];
            font-weight: 800;
        }
    }

    section {
        margin: 1em;
    }
</style>

{#await promise}
    <h2 class="loading">Loading your test...</h2>
{:then pop}
    {#if promiseError}
        <h2 class="error">Error loading test!</h2>
    {:else}
        {#if isTesting}
            <section>
                <Question question={question} on:continue="{continueTest}"/>
            </section>
        {:else}
            <section>
                <Level {level}/>
            </section>
        {/if}
    {/if}
{/await}

