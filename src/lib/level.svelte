<script lang="ts">
    export let level;
    let levelName;
    switch (level) {
        case 1: levelName = "Cheeto Puff"; break;
        case 2: levelName = "Cheeto"; break;
        case 3: levelName = "Hot Cheeto"; break;
        case 4: levelName = "Flaming Hot Cheeto"; break;
        case 5: levelName = "Taki"; break;
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
        Congrats you're a
        <span id="class">
            {levelName}!
        </span>
    </h2>
</div>
