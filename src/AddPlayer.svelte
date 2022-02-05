<script lang="ts">
   import { createEventDispatcher } from 'svelte'
   import { initialPlayer } from './initializer'

   const dispatch = createEventDispatcher()

   let player = initialPlayer

   const onSubmit = (e: SubmitEvent) => {
      e.preventDefault()
      dispatch('add-player', player)
      player = initialPlayer
   }
</script>

<form on:submit={onSubmit} class="grid-3">
   <input type="text" placeholder="Player Name" bind:value={player.name} />
   <input
      type="number"
      placeholder="Player Points"
      bind:value={player.points}
   />
   <input type="submit" class="btn btn-primary" value="Add Player" />
</form>