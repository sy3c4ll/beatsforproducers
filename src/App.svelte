<script lang="ts">
  // --- MOCK DATA ---
  // In a real app, this would come from your Rust backend
  const songs = [
    { 
      id: 1, 
      rank: 1, 
      title: "Neon Nights", 
      artist: "The Synthetics", 
      album: "City Lights",
      color: "bg-indigo-500" 
    },
    { 
      id: 2, 
      rank: 2, 
      title: "Coffee Shop Jazz", 
      artist: "Luna & The Cats", 
      album: "Morning Brew",
      color: "bg-amber-500" 
    },
    { 
      id: 3, 
      rank: 3, 
      title: "Electric Dreams", 
      artist: "Voltage", 
      album: "High Voltage",
      color: "bg-rose-500" 
    },
    { 
      id: 4, 
      rank: 4, 
      title: "Midnight Rain", 
      artist: "Echoes", 
      album: "Silence",
      color: "bg-emerald-500" 
    },
    { 
      id: 5, 
      rank: 5, 
      title: "Lost in the City", 
      artist: "Unknown", 
      album: "Urban Drift",
      color: "bg-cyan-500" 
    },
  ];

  const navItems = ["Hottest Today", "Discover New", "Post Your Own", "My Purchases"];

  // --- STATE ---
  let currentTrack = $state<string | null>(null);
  let isPlaying = $state(false);

  // --- ACTIONS ---
  function togglePlay(songTitle: string) {
    if (currentTrack === songTitle && isPlaying) {
      isPlaying = false;
      currentTrack = null;
    } else {
      currentTrack = songTitle;
      isPlaying = true;
    }
    alert(`(TODO) Now playing: ${songTitle}`);
  }

  function handleNavClick(label: string) {
    alert(`(TODO) Navigating to: ${label}`);
    // In a real app, you might use a router here
  }
</script>

<div class="min-h-screen bg-gray-50 text-gray-900 font-sans flex flex-col">
  
  <!-- TOP NAVBAR -->
  <header class="sticky top-0 z-10 bg-white/90 backdrop-blur-md border-b border-gray-200 px-6 py-4 flex justify-between items-center shadow-sm">
    <div class="flex items-center gap-2">
      <div class="w-8 h-8 bg-gradient-to-tr from-indigo-600 to-purple-600 rounded-lg flex items-center justify-center text-white font-bold text-lg">
        I
      </div>
      <span class="font-bold text-xl tracking-tight text-gray-800">beatsforproducers.com</span>
    </div>
    
    <button title="My Profile" onclick={() => handleNavClick("My Profile")} class="w-10 h-10 rounded-full bg-gray-100 hover:bg-gray-200 transition flex items-center justify-center text-gray-600">
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
    </button>
  </header>

  <!-- MAIN CONTENT (Scrollable) -->
  <main class="flex-1 max-w-3xl mx-auto w-full p-6 pb-32">
    <h2 class="text-3xl font-bold mb-8 text-gray-900">Hottest Today</h2>

    <div class="space-y-3">
      {#each songs as song}
        <div class="group flex items-center gap-4 p-3 rounded-xl hover:bg-white hover:shadow-md transition-all duration-200 border border-transparent hover:border-gray-100">
          
          <!-- Rank -->
          <span class="w-6 text-center font-bold text-gray-400 text-lg group-hover:text-indigo-600 transition-colors">
            {song.rank}
          </span>

          <!-- Play Button -->
          <button 
            onclick={() => togglePlay(song.title)}
            class="w-10 h-10 flex-shrink-0 flex items-center justify-center rounded-full bg-gray-100 text-gray-600 group-hover:bg-indigo-600 group-hover:text-white transition-all duration-200 shadow-sm hover:shadow-md"
          >
            {#if currentTrack === song.title && isPlaying}
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><rect x="6" y="4" width="4" height="16"/><rect x="14" y="4" width="4" height="16"/></svg>
            {:else}
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><polygon points="5 3 19 12 5 21 5 3"/></svg>
            {/if}
          </button>

          <!-- Album Art (Placeholder) -->
          <div class={`w-14 h-14 rounded-lg shadow-sm flex-shrink-0 ${song.color} flex items-center justify-center text-white font-bold text-xs opacity-90`}>
            {song.album.substring(0, 2).toUpperCase()}
          </div>

          <!-- Info -->
          <div class="flex-1 min-w-0">
            <div class="font-semibold text-gray-900 truncate text-base">
              {song.title}
              {#if currentTrack === song.title && isPlaying}
                <span class="ml-2 inline-block w-2 h-2 bg-green-500 rounded-full animate-pulse"></span>
              {/if}
            </div>
            <div class="text-sm text-gray-500 truncate">{song.artist} • {song.album}</div>
          </div>
        </div>
      {/each}
    </div>
  </main>

  <!-- BOTTOM NAVBAR -->
  <nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200 shadow-[0_-4px_6px_-1px_rgba(0,0,0,0.05)] z-20">
    <div class="max-w-3xl mx-auto grid grid-cols-4 gap-1 p-2">
      {#each navItems as item}
        <button 
          onclick={() => handleNavClick(item)}
          class="flex flex-col items-center justify-center py-2 px-1 rounded-lg hover:bg-gray-50 active:bg-gray-100 transition-colors group"
        >
          <span class="text-xs font-medium text-gray-600 group-hover:text-indigo-600 transition-colors">
            {item}
          </span>
        </button>
      {/each}
    </div>
  </nav>

</div>
