<script>
    import Test from "./lib/test.svelte";
</script>

<style global lang="less">
    .round(input) {
        border-radius: input;
    }

    @fonts: {
        title: 'Carter One', cursive;
        subtitle: 'Piazzolla', serif;
        text: 'Roboto Mono', monospace;
    }

    @colors: {
        main: hsla(175, 100%, 72%, 1);
        accent: hsla(130, 100%, 72%, 1);
        light: hsla(0, 0%, 100%, 1);
        dark: hsla(0, 0%, 22%, 1);
    }

    body {
        box-sizing: border-box;
        font-family: @fonts[text];
        min-height: 100vh;
        color: @colors[light];
        background-color: @colors[light];
    }

    *, *::before, *::after {
        margin: 0;
        padding: 0;
        box-sizing: inherit;
    }

    a {
        text-decoration: none;
        color: initial;
    }

    li {
        list-style: none;
    }

    h1, button {
        font-family: @fonts[title];
    }

    h2 {
        font-family: @fonts[subtitle];
    }

    main.top {
        background-color: @colors[dark];
        padding: 0.5em;
        min-height: 100vh;
        max-width: 800px;
        margin: 0 auto;

        div {
            margin-bottom: 2em;

            h1, h2 {
                text-align: center;
            }

            h1 {
                color: @colors[main];
                font-size: 3em;
            }

            h2 {
                color: @colors[accent];
                font-size: 2em;
            }
        }
    }

    @media screen and (max-width: 600px) {
        main.top {
            div {
                h1 {
                    font-size: 2.5em;
                }

                h2 {
                    font-size: 1.5em;
                }
            }
        }
    }
</style>

<main class="top">
    <div>
        <h1>Mexican Spanish School</h1>
        <h2>Placement Test</h2>
    </div>
    <section>
        <Test/>
    </section>
</main>
