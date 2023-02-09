<script>
export let items;
export let title;

</script>

<h1 class="m-2.5 p-2.5 text-xl">{title}</h1>
<ul class="m-2.5 p-1.5">
  {#each items as item}
  <li>
    <input type="checkbox" bind:checked={item.isDone} class="checkbox checkbox-accent">
    {item.name}    
</li>
  {/each}
</ul>