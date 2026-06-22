<script lang="ts">
  import '../app.css';
  import { onMount } from 'svelte';
  import { useRegisterSW } from 'virtual:pwa-register/svelte';

  const { needRefresh, updateServiceWorker } = useRegisterSW({
    onRegistered(r: ServiceWorkerRegistration | undefined) {
      console.log('SW Registered:', r);
    },
    onRegisterError(error: Error) {
      console.error('SW registration error', error);
    }
  });

  function close() {
    needRefresh.set(false);
  }
</script>

<slot />

{#if $needRefresh}
  <div class="pwa-toast" role="alert">
    <div class="message">
      <span>New content available, click on reload button to update.</span>
    </div>
    <button on:click={() => updateServiceWorker(true)}>Reload</button>
    <button on:click={close}>Close</button>
  </div>
{/if}

<style>
  .pwa-toast {
    position: fixed;
    right: 0;
    bottom: 0;
    margin: 16px;
    padding: 12px;
    border: 1px solid #8096b7;
    border-radius: 4px;
    z-index: 1000;
    text-align: left;
    box-shadow: 3px 4px 5px 0 #8096b7;
    background-color: white;
  }
  .pwa-toast .message {
    margin-bottom: 8px;
  }
  .pwa-toast button {
    border: 1px solid #8096b7;
    outline: none;
    margin-right: 5px;
    border-radius: 2px;
    padding: 3px 10px;
    cursor: pointer;
  }
</style>
