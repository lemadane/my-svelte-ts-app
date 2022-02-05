<script lang="ts">
   import { createEventDispatcher } from 'svelte'
   import { initialPlayer } from './initializer'
   import type { PlayerType } from './types'

   const dispatch = createEventDispatcher()

   export let player: PlayerType = initialPlayer

   let isControlShown = false

   const toggleControls = () => (isControlShown = !isControlShown)

   const onDelete = () => dispatch('remove-player', player.name)

   const addPoint = () => (player.points += 1)

   const removePoint = () => (player.points -= 1)
</script>

<div class="card">
   <h1>{player.name}</h1>
   <button class="btn btn-sm" on:click={toggleControls}>
      {#if isControlShown}
         -
      {:else}
         +
      {/if}
   </button>
   <button class="btn btn-sm btn-danger" on:click={onDelete}>x</button>
   <h3>Points: {player.points}</h3>
   {#if isControlShown}
      <button class="btn" on:click={addPoint}>+1</button>
      <button class="btn btn-dark" on:click={removePoint}>-1</button>
      <input type="number" bind:value={player.points} />
   {/if}
</div>

<style>
   /* Cards */
   .card {
      padding: 1rem;
      border: #ccc 1px dotted;
      margin: 0.7rem 0;
   }
   h1 {
      color: #204f6e;
   }
   h3 {
      margin-bottom: 10px;
   }
</style>
