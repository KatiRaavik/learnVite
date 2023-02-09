<script>
    import { each, text } from "svelte/internal";

  let message = 'Tere!';
  let items = [
    {name: 'Piim', isDone: false}, 
    {name: 'sai', isDone: false}, 
    {name: 'leib', isDone: false},
  ];

  $: doneItems = items.filter((item)=>item.isDone);

  $: notDoneItems = items.filter(item => !item.isDone)

  function add(){
    if (message.trim() !== ''){
      items = [
        ...items,
        {name: message, isDone: false},
      ];
    }
    message = '';
  }

  function keyDown(evt){
    if(evt.key === 'Enter'){
      add();
    }
  }
</script>

<input type="text" bind:value={message} on:keydown={keyDown}/>
<button on:click={()=>add()}>Add</button>

<h1>All items</h1>
<ul>
  {#each items as item}
  <li>
    {item.name}
    <input type="checkbox" bind:checked={item.isDone}>
    </li>
  {/each}
</ul>

<h1>Done items</h1>
<ul>
  {#each doneItems as item}
  <li>
    {item.name}
    <input type="checkbox" bind:checked={item.isDone}>
    </li>
  {/each}
</ul>

<h1>Not done items</h1>
<ul>
  {#each notDoneItems as item}
  <li>
    {item.name}
    <input type="checkbox" bind:checked={item.isDone}>
    </li>
  {/each}
</ul>