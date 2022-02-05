<script lang="ts">
   import type { PlayerType } from './types'
   import Player from './Player.svelte'
   import AddPlayer from './AddPlayer.svelte'
   import Navbar from './Navbar.svelte'

   let players: PlayerType[] = [
      {
         name: 'John Doe',
         points: 53,
      },
      {
         name: 'Sam Smith',
         points: 45,
      },
      {
         name: 'Sara Wilson',
         points: 34,
      },
   ]
   const addPlayer = (e: CustomEvent<any>) => {
      const newPlayer = e.detail as PlayerType
      players = [...players, newPlayer]
   }

   const removePlayer = (e: CustomEvent<any>) => {
      const playerTobeDeleted = e.detail
      players = players.filter((player) => player.name !== playerTobeDeleted)
   }
</script>

<Navbar />
<div class="container">
   <AddPlayer on:add-player={addPlayer} />
   {#if players.length === 0}
      <p>No Players</p>
   {:else}
      {#each players as player}
         <Player {player} on:remove-player={removePlayer} />
      {/each}
   {/if}
</div>
