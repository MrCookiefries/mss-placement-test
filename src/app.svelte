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

    span#class {
        font-family: @fonts[title];
    }

    @keyframes dots {
        0%, 100% {
            border-bottom: 0.5em dotted @colors[light];
        }
        25%, 75% {
            border-bottom: 0.5em dotted @colors[accent];
        }
        50% {
            border-bottom: 0.5em dotted @colors[main];
        }
    }

    @keyframes text-breathe {
        50% {
            font-variation-settings: 'wght' 700;
            letter-spacing: 0.25em;
        }
    }

    @keyframes title-expand {
        0%, 100% {
            text-shadow: 2px 2px lighten(@colors[dark], 10%),
                4px 4px lighten(@colors[dark], 20%),
                6px 6px lighten(@colors[dark], 30%),
                8px 8px lighten(@colors[dark], 40%);
        }
        75% {
            text-shadow: 2px -2px lighten(@colors[dark], 10%),
                4px -4px lighten(@colors[dark], 20%),
                6px -6px lighten(@colors[dark], 30%),
                8px -8px lighten(@colors[dark], 40%);
        }
        50% {
            text-shadow: -2px -2px lighten(@colors[dark], 10%),
                -4px -4px lighten(@colors[dark], 20%),
                -6px -6px lighten(@colors[dark], 30%),
                -8px -8px lighten(@colors[dark], 40%);
        }
        25% {
            text-shadow: -2px 2px lighten(@colors[dark], 10%),
                -4px 4px lighten(@colors[dark], 20%),
                -6px 6px lighten(@colors[dark], 30%),
                -8px 8px lighten(@colors[dark], 40%);
        }
    }

    main.top {
        background-image: linear-gradient(180deg, fade(darken(@colors[dark], 10%), 50%), fade(lighten(@colors[dark], 10%), 50%)),
            linear-gradient(-90deg, fade(darken(@colors[dark], 10%), 50%), fade(lighten(@colors[dark], 10%), 50%));
        padding: 0.5em;
        min-height: 100vh;
        max-width: 800px;
        margin: 0 auto;

        div.header {
            padding-bottom: 2em;
            border-bottom: 0.5em dotted @colors[light];
            animation: dots infinite forwards linear 12s;

            h1, h2 {
                text-align: center;
            }

            h1 {
                color: @colors[main];
                font-size: 3em;
                animation: title-expand infinite ease-in-out 5s;
            }

            h2 {
                color: @colors[accent];
                font-size: 2em;
                font-variation-settings: 'wght' 200;
                animation: text-breathe infinite linear 3s;
                letter-spacing: 0.1em;
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
    <div class="header">
        <h1>Mexican Spanish School</h1>
        <h2>Placement Test</h2>
    </div>
    <section>
        <Test/>
    </section>
</main>
