<script lang="ts">
    let segments = Array(20).fill(0);
    let percentage = 0;
    let grabbing = "grab";

    export let left = 100;
	export let top = 100;
	
	let moving = false;
	
	function onMouseDown() {
		moving = true;
        grabbing = "grabbing";
	}
	
	function onMouseMove(e: MouseEvent) {
		if (moving) {
			left += e.movementX;
			top += e.movementY;
		}
	}
	
	function onMouseUp() {
		moving = false;
        grabbing = "grab";
	}
    function onKeyDown(e: KeyboardEvent) {
        // console.log(e.code);
        switch (e.code) {
            case "ArrowLeft":
                left -= 10;
                break;
            case "ArrowRight":
                left += 10;
                break;
            case "ArrowUp":
                top -= 10;
                break;
            case "ArrowDown":
                top += 10;
                break;
        }
    }
</script>

<svelte:window on:keydown|preventDefault={onKeyDown} on:mouseup={onMouseUp} on:mousemove={onMouseMove} />

<button class="draggable" draggable="true" tabindex="0" aria-grabbed="true" aria-dropeffect="move" on:mousedown={onMouseDown}>
    <div class="outer-box acrylic" style="top: {top}px; left: {left}px; cursor: -webkit-{grabbing}; cursor: {grabbing}; transition: 0.05s">
        <div class="inner-box acrylic">
            {#each segments as segment, i}
                <div class="segment segment-{i+1}"></div>
            {/each}
            <span class="percentage">{percentage}%</span>
        </div>
    </div>
</button>

<style lang="scss">
    .outer-box {
        position: absolute;
        $box-border: 2px solid lightgray;
        padding: 1em;
        border: $box-border;
        width: 20em;
        border-radius: .25em;
        .inner-box {
            border: $box-border;
            position: relative;
            display: flex;
            box-shadow: none; // override acrylic styles
            background-color: #bdcee6bb;
            color: white;
            .percentage {
                position: absolute;
                margin-left: auto;
                margin-right: auto;
                left: 0;
                right: 0;
                text-align: center;
            }
            .segment {
                height: 1.5em;
                flex-basis: 100%;
            }
        }
    }
    .acrylic {
        border-width: thin;
        border-style: solid;
        border-color: #e5e5e5;
        -webkit-backdrop-filter: blur(40px);
        backdrop-filter: blur(40px);
        background-color: #ffffffbb;
        overflow-y: auto;
        // background-image: url('noise.png');
        background-repeat: repeat;
        box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
    }
    button.draggable {
        border: 0;
        background: transparent;
        width: 0;
        height: 0;
        font-family: var(--fds-font-family-text);
        outline: 0;
    }
</style>