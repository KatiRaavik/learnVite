<script>
    import { each, text } from "svelte/internal";
    import ItemList from "./lib/itemList.svelte";

  let message = '';
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
<div class="container mx-auto mt-3 p-10 items-center">

  <div class="form-control">
    <div class="input-group">
      <input type="text" bind:value={message} on:keydown={keyDown} class="bg-yellow-100 rounded-md p-2.5"/>
      <button on:click={()=>add()} class="bg-teal-400 items-center justify-center rounded-md p-2.5 text-gray-900">Add</button>
    </div>
  </div>

  <ItemList title='All items' bind:items={items}/>
  <ItemList title='Done items' bind:items={doneItems}/>
  <ItemList title='Undone items' bind:items={notDoneItems}/>
</div>
