<script lang="ts">
    import Tile from "./Tile.svelte";
    let player : string = "X";
    let plrFailed : boolean = false;

    function handleClick(event) {
        let elm : HTMLDivElement;
        elm = event.target;
        if(elm.classList[0] == "Tile") {
            if (!(elm.classList[elm.classList.length - 1] == "clicked")) {

                elm.innerText = player;
                if (player == "X") player = "O";
                else player = "X";

                elm.className += " clicked";
                plrFailed = false;
            }
            else {
                if (!(plrFailed)) {
                    alert(`Player: "${player}", you may not select a box already selected by the other player!`); 
                    plrFailed = true;
                }
            }
        }
    }
</script>
<div class="flex justify-center items center">
    <div on:click={handleClick} class="flex items center justify-center">
        {#each [1, 2, 3] as _}
            <div>
                {#each [1, 2, 3] as _}
                    <Tile/>
                    {#if !(_ == 3)}
                        <div class="w-full h-[25px] bg-black"></div>
                    {/if}
                {/each}
            </div>
            {#if !(_ == 3)}
                <div class="w-[25px] bg-black"></div>
            {/if}
        {/each}
    </div>
</div>
<div class="w-screen flex items-center justify-center">
    <div class="border-black border-solid rounded-md border-2 w-[25%] text-center text-lg font-bold">
        It is player: {player}'s turn
    </div>
</div>