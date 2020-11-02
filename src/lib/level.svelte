<script lang="ts">
    export let level;
    let levelName;
    switch (level) {
        case 1: levelName = "(1) One"; break;
        case 2: levelName = "(2) Two"; break;
        case 3: levelName = "(3) Three"; break;
        case 4: levelName = "(4) Four"; break;
        case 5: levelName = "(5) Five"; break;
        default: levelName = "Undetermined"; break;
    }
</script>

<style lang="less">
     @colors: {
        main: hsla(175, 100%, 72%, 1);
        accent: hsla(130, 100%, 72%, 1);
        light: hsla(0, 0%, 100%, 1);
        dark: hsla(0, 0%, 22%, 1);
    }

    @keyframes color-change {
        50% {
            color: @colors[accent];
        }
    }

    div {
        h2 {
            text-align: center;
            color: @colors[light];

            span {
                font-size: 2em;
                color: @colors[main];
                display: block;
                transform: scale(1);
                animation: color-change infinite ease-in-out 3s;
                transition: transform ease-in-out 600ms;

                &:hover {
                    transform: scale(0.75);
                }
            }
        }
    }
</style>

<div>
    <h2>
        Congrats you're in level
        <span id="class">
            {levelName}!
        </span>
    </h2>
</div>
