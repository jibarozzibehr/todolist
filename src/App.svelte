<script>
  import { slide } from "svelte/transition";
  import { elasticInOut } from "svelte/easing";
  import Clock from "./Clock.svelte";
  import Switch from "./Switch.svelte";

  let todos = [];
  let input = "";

  function addTodo() {
    if (input)
      todos = [
        ...todos,
        {
          text: input,
          id: Math.random()
            .toString(36)
            .substr(2, 9)
        }
      ];
    input = "";
  }

  function removeTodo(id) {
    const index = todos.findIndex(todo => todo.id === id);
    todos.splice(index, 1);
    todos = todos;
  }

  let darkMode = false;

  if (darkMode == true) {
    alert('Modo oscuro activado.');
  }
</script>

<svelte:head>
  <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/npm/bulma@0.8.0/css/bulma.min.css"/>
  <script src="https://use.fontawesome.com/releases/v5.3.1/js/all.js"></script>
</svelte:head>

<main class="container is-fluid color-fondo">
  

  <div class="columns is-centered is-vcentered is-mobile">
    <div class="column is-narrow" style="width: 70%">
      
      <!--<div>
        <div class='reloj'>
          <h1>Hola</h1>
        </div>
      </div>-->
      <div class='info'>
        <p class="infoText">i<span class="infoTextSpan">Cosas para hacer<br><p class="description">Lista de cosas para hacer siguiendo la tendencia de diseño neomorfista.</p></span></p>
      </div>

      <Clock />
      <div class="darkModeWrapper">
        <div class="darkMode">
          <div class="darkModeText"><p class="darkModeText">Modo oscuro</p></div>
          <div class="darkModeSwitch"><Switch bind:checked={darkMode}></Switch></div>
        </div>
      </div>
      

      <h1 class="has-text-centered title" style="margin-top: 10px;">Cosas para hacer</h1>
      <form class="field has-addons" style="justify-content: center" on:submit|preventDefault={addTodo}>
        <div class="control">
          <input bind:value={input} class="input" type="text" placeholder="Tarea">
        </div>
        <div class="control">
          <button class="button is-primary">
            <span class="icon is-small">
              <i class="fas fa-plus"></i>
            </span>
          </button>
        </div>
      </form>
      <ul class:list={todos.length > 0} style="max-width: 500px; margin: 0 auto;">
        {#each todos as todo (todo.id)}
          <li class="list-item" transition:slide="{{duration: 300, easing: elasticInOut}}">
            <div class="is-flex" style="align-items: center;">
              <span class="is-pulled-left">{todo.text}</span>
              <div style="flex: 1"></div>
              <button class="button is-text is-pulled-right is-small" on:click={()=> removeTodo(todo.id)}>
                <span class="icon">
                  <i class="fas fa-check"></i>
                </span>
              </button>
            </div>
          </li>
        {:else}
          <li class="has-text-centered" transition:slide="{{delay: 600, duration: 300, easing: elasticInOut}}">¡No tenés nada para hacer!</li>
        {/each}
      </ul>
    </div>
  </div>
</main>

<style>
  .darkModeWrapper {
    margin: 0 auto;
  }

  .darkMode {
    margin-top: 10px;
    text-align: center;
  }

  .darkModeText {
    display: inline-block;
    vertical-align: middle;
  }

  :global(body.dark-mode) .darkModeText {
    color: white;
  }

  .darkModeSwitch {
    display: inline-block;
    vertical-align: middle;
  }

  .info {
    position: fixed;
    top: 2%;
    right: 2%;
    width: 50px;
    height: 50px;

    text-align: center;
    vertical-align: middle; 
    line-height: 50px;

    border-radius: 50px;
    background: #dde9f7;
    box-shadow: 6px 6px 12px #bcc6d2, 
                -6px -6px 12px #feffff;

    transition: background 0.3s, box-shadow 0.3s;
  }

  .info:hover {
    background: linear-gradient(145deg, #c7d2de, #ecf9ff);
  }

  :global(body.dark-mode) .info {
    background: #1A1A1A;
    box-shadow: 6px 6px 12px #121212, 
                -6px -6px 12px #2A2A2A;
  }

  :global(body.dark-mode) .info:hover {
    background: linear-gradient(145deg, #111111, #1c1c1c);
  }

  .infoText {
    font-weight: 700;
    font-size: 30px;
    font-family: Georgia, 'Times New Roman', Times, serif
  }

  .infoText:hover span{
    display:block;
}

  .infoTextSpan {
    border-radius: 30px;
    background: #dde9f7;
    box-shadow:  6px 6px 12px #bcc6d2, 
                -6px -6px 12px #feffff;
    position: fixed;
    top: 10%;
    right: 2%;
    width: 500px;
    height: 100px;
    display: none;
    font-family: sans-serif;

    /*background:#F8F8F8;*/
    /*border: 5px solid #DFDFDF;*/
    /*color: #717171;*/
    /*font-size: 13px;*/
    /*height: 30px;*/
    /*letter-spacing: 1px;*/
    /*line-height: 30px;*/
    /*position: relative;*/
    /*text-align: center;*/
    /*text-transform: uppercase;
    top: -80px;
    left:-30px;
    display:none;
    padding:0 20px;*/
  }

  :global(body.dark-mode) .infoTextSpan {
    background: #1A1A1A;
    box-shadow: 6px 6px 12px #121212, 
                -6px -6px 12px #2A2A2A;
  }

  .description {
    font-size: 15px;
    line-height: 15px;
    text-align: left;
    padding: 0px 30px 10px 30px;
  }


	/*.reloj {
    width: 200px;
    height: 80px;
    margin: 0 auto;
    margin-top: 20px;
    background: linear-gradient(130deg, rgba(125,140,115,1) 0%, rgba(88,98,82,1) 100%);
    color:rgb(53, 53, 53);
    border-radius: 5px;
    text-align: center;
    vertical-align: middle;*/
    /*line-height: 70px;*/ /*div height - border size*/
    /*font-weight: 900;
    font-size: 30px;
    border: 10px;
    border-style: solid;*/
    /*border-color: #EFEEEE;*/

    /*-webkit-box-shadow: 6px 6px 16px 0px rgba(209,205,199,0.5);
    -moz-box-shadow: 6px 6px 16px 0px rgba(209,205,199,0.5);*/
    /*border-color: #dde9f7;
    box-shadow: 6px 6px 11px #bcc6d2, 
                -6px -6px 11px #feffff;
  }*/

  .color-fondo {
    background-color: #dde9f7;
    transition: background-color 0.3s
  }

  :global(body.dark-mode) .color-fondo {
    background-color: #1A1A1A;
  }

  main {
    height: 100%;
  }
</style>