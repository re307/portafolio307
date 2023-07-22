
<script>
// @ts-nocheck
  import { onMount } from 'svelte';
  import itemesMenu from './assets/menuConfig.json';
  import Inicio from './lib/Inicio.svelte'
  import Buscaminas from './lib/Buscaminas/Buscaminas.svelte'
  import CodeVisual from './lib/Componentes/CodeVisual/CodeVisual.svelte'
  import Calendario from './lib/Componentes/Calendario/Calendario.svelte'
  import LineaTiempo from './lib/Componentes/LineaTiempo/LineaTiempo.svelte'
  export let modulo = "";
  const j = window.$;
  onMount(()=>{
    j('.sub-btn').click((e)=>{
      j(e.target).next('.sub-menu').slideToggle();
      j(e.target).find('.dropdown').toggleClass('rotate');
    });
    j('.menu-btn').click(()=>{
      j('.sider-bar').addClass('active');
      j('.menu-btn').css('visibility','hidden');
    });
    j('.close-btn').click(()=>{
      j('.sider-bar').removeClass('active');
      j('.menu-btn').css('visibility','visible');
    });
  });
  const clickMenu = (item)=>{
    console.log(item);
    if (item.modulo !== undefined) {
      modulo = item.modulo
    }else{
      modulo = item.submodulo
    }
  }
</script>
<div class="menu-btn">
  <i class="fas fa-bars"></i>
</div>
<div class="sider-bar">
  <div class="close-btn">
    <i class="fas fa-times"></i>
  </div>
  <div class="menu">
    {#each itemesMenu as item}
      <div class="item">
        {#if item.submenu === undefined}
          <div class="a-item" on:click={()=>{clickMenu(item)}}><i class="{item.icon}" ></i>{item.titulo}</div>
        {:else}
          <div class="sub-btn a-item"><i class="{item.icon}"></i>{item.titulo}<i class="fas fa-angle-right dropdown"></i></div>
          <div class="sub-menu">
            {#each item.submenu as submenu}
              <div class="a-item sub-menu-item" on:click={()=>{clickMenu(submenu)}}>{submenu.titulo}</div>
            {/each}
          </div>
        {/if}
      </div>
    {/each}
  </div>
</div>
<div class="main" id="main">
  {#if modulo === 'Inicio'||modulo === ''}
    <Inicio desde={modulo}></Inicio>
  {/if}
  {#if modulo === 'Buscaminas'}
    <Buscaminas recarga={true}></Buscaminas>
  {/if}
  {#if modulo === "Calendario"}
    <Calendario></Calendario>
  {/if}
  {#if modulo === "VizualizarCode"}
    <CodeVisual></CodeVisual>
  {/if}
</div>