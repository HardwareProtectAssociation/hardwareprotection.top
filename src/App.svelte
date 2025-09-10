<script>
  import { onMount } from 'svelte'
  import { fade } from 'svelte/transition'

  let showIntro = true

  let testimonials = [
    {
      name: 'Alice',
      role: 'Engineer',
      text: 'HPA ensures our hardware deployments remain secure and reliable.',
    },
    {
      name: 'Bob',
      role: 'Researcher',
      text: 'The association provides excellent resources for hardware protection.',
    },
    {
      name: 'Chen',
      role: 'Developer',
      text: 'Joining HPA improved our compliance and safety protocols.',
    },
    {
      name: 'Dana',
      role: 'Security Analyst',
      text: 'HPA keeps us connected with the latest in hardware protection.',
    },
  ]

  let offset = 0
  let interval
  let paused = false

  onMount(() => {
    setTimeout(() => (showIntro = false), 2500)
    interval = setInterval(() => {
      if (!paused) {
        offset = (offset + 1) % testimonials.length
      }
    }, 3000)
    return () => clearInterval(interval)
  })
</script>

<!-- Fullscreen intro animation -->
{#if showIntro}
  <div
    class="fixed inset-0 bg-gradient-to-b from-slate-900 to-black flex items-center justify-center z-50"
    transition:fade
  >
    <img
      src="/logo.png"
      alt="HPA Logo"
      class="w-32 h-32 md:w-40 md:h-40 animate-pulse"
    />
    <h1
      class="text-4xl md:text-6xl font-extrabold text-emerald-400 animate-pulse"
    >
      Hardware Protection Association
    </h1>
  </div>
{/if}

<div
  class="min-h-screen bg-gradient-to-b from-slate-900 via-slate-800 to-black text-slate-100 antialiased"
>
  <!-- Nav -->
  <nav class="w-full px-6 py-6 flex items-center justify-between">
    <img
      src="/logo.png"
      alt="HPA Logo"
      class="w-10 h-10 shadow-lg flex items-center justify-center font-bold"
    />
    <div class="font-semibold tracking-wide">HPA</div>
    <div class="flex items-center gap-3">
      <button class="btn btn-sm">Docs</button>
    </div>
  </nav>

  <!-- Hero -->
  <header class="w-full px-6 py-12 text-center">
    <h1 class="text-4xl md:text-5xl font-extrabold leading-tight">
      Protecting the Future of Hardware
    </h1>
    <p class="text-slate-300 mt-4 max-w-2xl mx-auto">
      Hardware Protection Association (HPA) promotes best practices,
      research, and collaboration in securing hardware systems
      worldwide.
    </p>
    <div class="mt-6 flex flex-col sm:flex-row gap-3 justify-center">
      <a
        href="https://discord.gg/9qjEPEGfwz"
        target="_blank"
        class="btn btn-success">Join Us</a
      >
      <a href="#features" class="btn btn-outline">Learn More</a>
    </div>
  </header>

  <!-- Features -->
  <section id="features" class="w-full px-6 py-12 text-center">
    <h2 class="text-3xl font-bold mb-6">Our Mission</h2>
    <div class="space-y-6 max-w-2xl mx-auto">
      <div class="card bg-base-200 p-6">
        <h3 class="font-semibold">Advocacy</h3>
        <p class="text-slate-400 text-sm mt-2">
          Representing the community in standards and policy
          discussions.
        </p>
      </div>
      <div class="card bg-base-200 p-6">
        <h3 class="font-semibold">Research</h3>
        <p class="text-slate-400 text-sm mt-2">
          Encouraging academic and industrial collaboration on
          protection technologies.
        </p>
      </div>
      <div class="card bg-base-200 p-6">
        <h3 class="font-semibold">Education</h3>
        <p class="text-slate-400 text-sm mt-2">
          Providing training and resources for engineers, developers,
          and organizations.
        </p>
      </div>
    </div>
  </section>

  <!-- Testimonials -->
  <section id="testimonials" class="w-full px-6 py-12 text-center">
    <h2 class="text-3xl font-bold mb-6">What Our Members Say</h2>
    <div class="relative overflow-hidden">
      <!-- 滚动容器 -->
      <div
        class="flex gap-6 animate-scroll hover:[animation-play-state:paused]"
      >
        {#each [...testimonials, ...testimonials] as t, i}
          <div class="card bg-base-200 p-6 w-72 flex-shrink-0">
            <div class="flex items-center gap-3 mb-3">
              {#if t.avatar}
                <img
                  src={t.avatar}
                  alt={t.name}
                  class="w-10 h-10 rounded-full"
                />
              {/if}
              <div class="text-left">
                <div class="font-semibold">{t.name}</div>
                {#if t.role}
                  <div class="text-xs text-slate-400">{t.role}</div>
                {/if}
              </div>
            </div>
            <p class="text-sm text-slate-300">“{t.text}”</p>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- Download CTA -->
  <section id="download" class="w-full px-6 py-12 text-center">
    <div class="card bg-base-200 p-8 max-w-2xl mx-auto">
      <h3 class="text-2xl font-bold">
        Join the Hardware Protection Movement
      </h3>
      <p class="text-slate-400 mt-2">
        Become a member and access exclusive resources, events, and
        community support.
      </p>
      <div
        class="mt-6 flex flex-col sm:flex-row gap-3 justify-center"
      >
        <a
          href="https://github.com/HardwareProtectAssociation"
          class="btn btn-outline">View on GitHub</a
        >
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer class="w-full px-6 py-8 text-center text-slate-400">
    <div>
      © {new Date().getFullYear()} Hardware Protection Association — Built
      with ❤️
    </div>
  </footer>
</div>

<style>
  @keyframes scroll {
    0% {
      transform: translateX(0%);
    }
    100% {
      transform: translateX(-50%);
    }
  }
  .animate-scroll {
    animation: scroll 30s linear infinite;
    width: max-content; /* 保证可以无缝拼接 */
  }
</style>
