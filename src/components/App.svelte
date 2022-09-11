<script>
import Cell from "./table/Cell.svelte";

let value = ''
//let response = []

//const handleInput = (event) => value.target.value


let response = fetch(`https://rickandmortyapi.com/api/character/`)
    .then(res => res.json())
    .then(apiResponse =>  apiResponse.results || [])

// const rowProps = {
//   action: '',
//   file: '',
//   idprodmkt: '',
//   sede: '',
//   source: '',
//   medium: '',
//   campaign: '',
// }

</script>

<main>
  <h1>Table filter</h1>
  
  <!-- <input type="text" placeholder="Search" value={value} on:input={handleInput}> -->

  {#await response}
    <p>Loading...</p>
  {:then response} 
    <table>
      <tbody>
        {#each response as {id,name,status,gender} }
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
