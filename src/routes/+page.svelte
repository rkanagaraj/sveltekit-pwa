<script lang="ts">
  import { browser } from '$app/environment';

  let deferredPrompt: BeforeInstallPromptEvent | null = null;
  let showInstallBanner = false;

  interface BeforeInstallPromptEvent extends Event {
    prompt(): Promise<void>;
    userChoice: Promise<{ outcome: 'accepted' | 'dismissed' }>;
  }

  if (browser) {
    window.addEventListener('beforeinstallprompt', (e: Event) => {
      e.preventDefault();
      deferredPrompt = e as BeforeInstallPromptEvent;
      showInstallBanner = true;
    });
  }

  async function installApp() {
    if (!deferredPrompt) return;
    await deferredPrompt.prompt();
    const { outcome } = await deferredPrompt.userChoice;
    console.log(`User ${outcome} the install prompt`);
    deferredPrompt = null;
    showInstallBanner = false;
  }
</script>

<svelte:head>
  <title>SvelteKit PWA</title>
  <meta name="description" content="A SvelteKit Progressive Web App" />
</svelte:head>

<main>
  <section class="hero">
    <div class="logo">
      <img src="/icons/icon-192x192.png" alt="App Icon" width="96" height="96" />
    </div>
    <h1>SvelteKit <span class="highlight">PWA</span></h1>
    <p class="subtitle">A Progressive Web App built with SvelteKit &amp; Vite PWA</p>

    {#if showInstallBanner}
      <button class="install-btn" on:click={installApp}>
        📲 Install App
      </button>
    {/if}
  </section>

  <section class="features">
    <div class="card">
      <span class="icon">⚡</span>
      <h2>Lightning Fast</h2>
      <p>Powered by Vite for blazing-fast development and optimized production builds.</p>
    </div>
    <div class="card">
      <span class="icon">📦</span>
      <h2>Offline Ready</h2>
      <p>Service worker caches assets so the app works even without a network connection.</p>
    </div>
    <div class="card">
      <span class="icon">📲</span>
      <h2>Installable</h2>
      <p>Add to your home screen on mobile or desktop for a native app-like experience.</p>
    </div>
    <div class="card">
      <span class="icon">🔄</span>
      <h2>Auto Update</h2>
      <p>Service worker automatically updates in the background and prompts for reload.</p>
    </div>
  </section>
</main>

<style>
  main {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
    max-width: 900px;
    margin: 0 auto;
    padding: 2rem 1rem;
    color: #333;
  }

  .hero {
    text-align: center;
    padding: 3rem 1rem;
  }

  .logo img {
    border-radius: 20px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
  }

  h1 {
    font-size: 3rem;
    margin: 1rem 0 0.5rem;
  }

  .highlight {
    color: #ff3e00;
  }

  .subtitle {
    font-size: 1.2rem;
    color: #666;
    margin-bottom: 2rem;
  }

  .install-btn {
    background: #ff3e00;
    color: white;
    border: none;
    padding: 0.8rem 2rem;
    font-size: 1rem;
    border-radius: 8px;
    cursor: pointer;
    transition: background 0.2s;
  }

  .install-btn:hover {
    background: #cc3200;
  }

  .features {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
    margin-top: 3rem;
  }

  .card {
    background: #f9f9f9;
    border: 1px solid #eee;
    border-radius: 12px;
    padding: 1.5rem;
    text-align: center;
    transition: box-shadow 0.2s;
  }

  .card:hover {
    box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
  }

  .icon {
    font-size: 2rem;
  }

  .card h2 {
    font-size: 1.1rem;
    margin: 0.5rem 0;
    color: #ff3e00;
  }

  .card p {
    font-size: 0.9rem;
    color: #555;
    line-height: 1.5;
  }
</style>
