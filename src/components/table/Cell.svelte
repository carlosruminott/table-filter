<script>
    export let cellType = 'td'
    export let text = ''
</script>

{#if cellType === 'td'}
    <td class={text}>{text}</td>
{:else}
    <th class={text}>{text}</th>
{/if}