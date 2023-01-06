{#if toggle == 'true'}
<button class:active="{active}" on:click="{() => active = !active}">{text}</button>
{:else}
<button on:click="{() => active = !active}">{text}</button>
{/if}


<script>
    let active = false;
    export let text = '';
    export const click = '';
    export let toggle = 'true';
  </script>

  <style>

    button{
        background-image: url('src/images/tool-svgrepo-com.png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        margin-left: 5em;
        font-size: 2rem;
        background-size: 25.5px 26.17px;
        border-radius: 100px;
        border: #3D6889;
        margin-right: 56.4px;
        background-color:#83B0D1;
    }

    

    .active {background-color: #F4D19B; color: #83B0D1;}
    button:hover {background-color: #F4D19B; color: #83B0D1;}

</style>