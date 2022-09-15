<script>
import { onMount } from 'svelte'
import Cell from "./table/Cell.svelte"

const items = [
  'ID',
  'Name',
  'Status',
  'Gender'
]

let filterType = 'name'
let search = undefined
let users = []

$: visibleUsers = search ? 
  users.filter(user => user[filterType].toLowerCase().includes(search.toLowerCase()))
  : users

onMount(async () => {
  const resp = await fetch('https://rickandmortyapi.com/api/character/')
  const data = await resp.json()
  users = data.results
});

</script>

<main>
  <h1>Table filter</h1>
  
  <input type="search" bind:value={search} class="ms-auto w-auto" placeholder={`Filter by ${filterType}`}>
  <select name="filterType" id="filterType" bind:value={filterType}>
    {#each items as item}
      <option value={item.toLocaleLowerCase()}>{item}</option>
    {/each}
  </select>

  {#await visibleUsers}
    <p>Loading...</p>
  {:then visibleUsers} 
    <table>
      <thead>
        <tr>
          {#each items as item}
            <Cell cellType="th" text={item} />
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each visibleUsers as {id,name,status,gender} }
          <tr>
            <Cell cellType="td" text={id} />
            <Cell cellType="td" text={name} />
            <Cell cellType="td" text={status} />
            <Cell cellType="td" text={gender} />
          </tr>
        {/each}
      </tbody>
    </table>
  {/await}

</main>

<style>
</style>
