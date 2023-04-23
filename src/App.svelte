
<script>
// @ts-nocheck
  import { onMount } from 'svelte';
  import itemesMenu from './assets/menuConfig.json';
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
  const handelClickSubMenu = (e)=>{
    // e.children[0].classList.toggle('');
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
          <div class="a-item"><i class="{item.icon}"></i>{item.modulo}</div>
        {:else}
          <div class="sub-btn a-item"><i class="{item.icon}"></i>{item.modulo}<i class="fas fa-angle-right dropdown"></i></div>
          <div class="sub-menu">
            {#each item.submenu as submenu}
              <div class="a-item sub-menu-item">{submenu.submodulo}</div>
            {/each}
          </div>
        {/if}
      </div>
    {/each}
  </div>
</div>
<section class="main">
  <h1>Hola mundo</h1>
</section>