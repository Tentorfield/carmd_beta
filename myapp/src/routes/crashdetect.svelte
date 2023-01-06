{#if toggle == 'true'}
<button class:active="{active}" on:click="{() => active = !active}">{text}</button>
{:else}
<button on:click="{() => active = !active}">{text}</button>
{/if}


<script>
  let active = false;
  export let text = '';
  export let toggle = 'true';
</script>


<style>

  button{
      position: relative;
      background-image: url('src/images/car-crash-svgrepo-com (1).png');
      background-repeat: no-repeat;
      background-position: center;
      width: 67px;
      height: 68px;
      font-size: 2rem;
      margin-left: -3em;
      background-size: 22.56px 37.6px;
      border-radius: 100px;
      border: #3D6889;
      margin-right: 56.4px;
      background-color:#83B0D1;
  }
    .active {background-color: #F4D19B; color: #83B0D1;}
    button:hover {background-color: #F4D19B; color: #83B0D1;}

</style>