
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
    });
  const handelClickSubMenu = (e)=>{
    // e.children[0].classList.toggle('');
  }
</script>
<div class="sider-bar">
  <div class="menu">
    {#each itemesMenu as item}
      <div class="item">
        {#if item.submenu === undefined}
          <a href="#"><i class="{item.icon}"></i>{item.modulo}</a>
        {:else}
          <a href="#" class="sub-btn"><i class="{item.icon}"></i>{item.modulo}<i class="fas fa-angle-right dropdown"></i></a>
          <div class="sub-menu">
            {#each item.submenu as submenu}
              <a href="#" class="sub-item">{submenu.submodulo}</a>
            {/each}
          </div>
        {/if}
      </div>
    {/each}
  </div>
</div>