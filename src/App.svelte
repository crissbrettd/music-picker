<script>

    let currentSelectedSong = ''

    async function loadSongList() {
        let response = await fetch("song-list.json")
        let songs = await response.json();
        return songs;
    }
    const promise = loadSongList()

</script>

<main>
    <h1>Tree of Life Worship Music Aid</h1>
    <div id="mainDiv">
        <div id="songInfoDiv">
            {#if currentSelectedSong != ''}
                <p>Name: {currentSelectedSong.name}</p>
                <p>Author: {currentSelectedSong.name}</p>
                <p>Tags: {currentSelectedSong.tags}</p>
            {:else}
                <p>Name:</p>
                <p>Author:</p>
                <p>Tags:</p>
            {/if}
        </div>
        <div id="songListDiv">
            {#await promise}

            <p>loading song list...</p>
                
            {:then song}
                {#each song.list as song}
                    <div 
                        class="songListItemDiv"
                        on:click={() => currentSelectedSong = song} >
                        {song.name}
                    </div>
                {/each}
            {:catch error}
                <p style="color: red">{error.message}</p>
            {/await}
        </div>
    </div>

</main>


<style>
	main {
        color: lightgrey;
		text-align: center;
		padding: 1em;
		max-width: 500px;
		margin: 0 auto;
	}

	h1 {
		color: darkgreen;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

    #songInfoDiv {
        border-color: lightgrey;
        border-style: solid;
        border-width: 1px;
        height: 25%;
        position: absolute;
        right: 0;
        text-align: left;
        width: 25%;
    }

    #songListDiv {
        align-self: center;
    }

    .songListItemDiv {
        border-color: darkgreen;
        background-color: lightgrey;
        border-radius: 1em;
        border-style: solid;
        border-width: 1px;
        color: darkgreen;
        margin-bottom: 2%;
        padding: 1%;
        text-align: left;
        user-select: none;
        width: 25%;
    }

    .songListItemDiv:hover {
        background-color: darkgrey;
        cursor: pointer;
    }

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>