<template>
      <div class="sidebar" :style="{ width: sidebarWidth }">
        <h1>
          <span v-if="collapsed" class="init">
            <div>a</div>
            <div>b</div>
          </span>
          <span v-else>
            <img src="../../../public/img/logo.png"  id="logo">
          </span>
        </h1>
    
        <SidebarLink to="/" icon="fas fa-home">Home</SidebarLink>
        <SidebarLink to="/cadastros" icon="fas fa-columns">Cadastros</SidebarLink>
    
        <span
          class="collapse-icon"
          :class="{ 'rotate-180': collapsed }"
          @click="toggleSidebar"
        >
          <i class="fas fa-angle-double-left" />
        </span>
      </div>
</template>
<script>
    import SidebarLink from './SidebarLink'
    import { collapsed, toggleSidebar, sidebarWidth } from './state'
    export default {
      props: {},
      components: { SidebarLink },
      setup() {
        return { collapsed, toggleSidebar, sidebarWidth }
      }
    }
</script>
    
<style>
    :root {
      --sidebar-bg-color: #222;
      --sidebar-item-hover: #D9AF3D;
      --sidebar-item-active: #FCBA03;
    }
</style>
    
<style scoped>
    .sidebar {
      background-color: var(--sidebar-bg-color);
      float: left;
      position: fixed;
      z-index: 1;
      top: 0;
      left: 0;
      bottom: 0;
      padding: 0.5em;
      transition: 0.3s ease;
      display: flex;
      flex-direction: column;
    }
    .sidebar :hover{
        color: white;
    }
    .sidebar h1 {
      height: 2.5em;
    }
    .collapse-icon {
      position: absolute;
      bottom: 0;
      padding: 0.75em;
      color: #FCBA03;
      transition: 0.2s linear;
    }
    .rotate-180 {
      transform: rotate(180deg);
      transition: 0.2s linear;
    }
    .init {
        color: #FFF;
    }
    
    #logo {
        width: 80px;
        height: 80px;
    }
    
</style>