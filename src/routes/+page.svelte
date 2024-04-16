<script>
     import '../style.css';
     let tadpol = '';
     let foamnest = [];
     $: isDone = foamnest.filter(item => item.done);

     function addToArray() {
          if (tadpol == '') {
               return;
          }
          foamnest = [...foamnest, {
               value: tadpol,
               done: false
          }];
          console.log(foamnest);
          tadpol = ''
     }
     function removeThis(index) {
          foamnest.splice(index, 1);
          foamnest = foamnest;
     }
     function clearDone(){
          foamnest = foamnest.filter(item => !item.done)

     }
</script>

<h1>Hop To It!</h1>

<form on:submit|preventDefault={addToArray}>
     <input type="text" bind:value={tadpol}>
     <button type="submit">&#43;</button>
</form>

<ul>
     {#each foamnest as item, index}
          <li>
               <input type="checkbox" bind:checked={item.done}>
               <span class:done={item.done}>{item.value}</span>
               <span on:click={() => removeThis(index)} class="remove" tabindex="0">&#45</span>
          </li>
     {/each}
</ul>
{#if isDone.length > 0}
<button on:click={clearDone}>Remove Done</button>
{/if}
<style>
     body {
          color: #bcdbc1;
     }
     ul {
          list-style: none;
     }
     li {
          font-size: 1.3rem;
     }
     .done {
          color: rgb(165, 165, 165);
          text-decoration: line-through;
     }
     .remove {
          color: red;
     }
</style>