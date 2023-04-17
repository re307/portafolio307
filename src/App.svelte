
<script>
// @ts-nocheck
  import { onMount } from 'svelte';
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
    <div class="item"><a href="#"><i class="fas fa-desktop"></i>Dasboard</a></div>
    <div class="item">
      <a href="#" class="sub-btn"><i class="fas fa-table"></i>Tabla<i class="fas fa-angle-right dropdown"></i></a>
      <div class="sub-menu">
        <a href="#" class="sub-item">Submenu1</a>
        <a href="#" class="sub-item">Submenu2</a>
        <a href="#" class="sub-item">Submenu3</a>
      </div>
    </div>
    <div class="item"><a href="#"><i class="fas fa-th"></i>Dasboard</a></div>
    <div class="item">
      <a href="#" class="sub-btn"><i class="fas fa-cogs"></i>Settings<i class="fas fa-angle-right dropdown"></i></a>
      <div class="sub-menu">
        <a href="#" class="sub-item">Submenu1</a>
        <a href="#" class="sub-item">Submenu2</a>
      </div>
    </div>
    <div class="item"><a href="#"><i class="fas fa-info-circle"></i>About</a></div>
  </div>
</div>