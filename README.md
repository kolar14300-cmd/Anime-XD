# Anime-XD
```react
import React, { useState, useEffect, useRef } from 'react';

// Mock Anime Data with Fallback Cover SVGs / Placeholders
const ANIME_DATA = [
  {
    id: 1,
    title: "Demon Slayer: Kimetsu no Yaiba",
    rating: "4.9",
    episodes: "26 + Movies",
    studio: "ufotable",
    year: "2019 - Present",
    genres: ["Action", "Fantasy", "Historical"],
    synopsis: "In Taisho-era Japan, kindhearted Tanjiro Kamado finds his family slaughtered by a demon. To make matters worse, his younger sister Nezuko has been turned into a demon herself. Though consumed by rage and grief, Tanjiro decides to become a demon slayer to find a cure for his sister and avenge his family.",
    bannerColor: "from-red-600 via-orange-500 to-amber-900",
    glowColor: "shadow-red-500/50",
    tagline: "Unsheathe your blade and slay the demons of the night.",
    characters: [
      { name: "Tanjiro Kamado", role: "Protagonist", power: "Water & Sun Breathing" },
      { name: "Nezuko Kamado", role: "Demon Companion", power: "Blood Demon Art" },
      { name: "Zenitsu Agatsuma", role: "Slayer", power: "Thunder Breathing" }
    ],
    episodesList: [
      { num: 1, title: "Cruelty", duration: "23m" },
      { num: 2, title: "Trainer Sakonji Urokodaki", duration: "24m" },
      { num: 3, title: "Sabito and Makomo", duration: "24m" },
      { num: 4, title: "Final Selection", duration: "23m" }
    ],
    bgPattern: "https://images.unsplash.com/photo-1578632767115-351597cf2477?w=1200&auto=format&fit=crop&q=80"
  },
  {
    id: 2,
    title: "Jujutsu Kaisen",
    rating: "4.8",
    episodes: "47",
    studio: "MAPPA",
    year: "2020 - Present",
    genres: ["Action", "Supernatural", "School"],
    synopsis: "Yuji Itadori, a high school student with exceptional physical strength, swallows a cursed finger to save his friends. He becomes the host of Ryomen Sukuna, the legendary King of Curses. Guided by the strongest sorcerer, Satoru Gojo, Yuji enters the Jujutsu High School to battle terrifying curses.",
    bannerColor: "from-blue-600 via-purple-700 to-indigo-950",
    glowColor: "shadow-blue-500/50",
    tagline: "In a world of curses, only curses can save you.",
    characters: [
      { name: "Yuji Itadori", role: "Vessel of Sukuna", power: "Divergent Fist" },
      { name: "Satoru Gojo", role: "Special Grade Sorcerer", power: "Limitless & Six Eyes" },
      { name: "Megumi Fushiguro", role: "Shadow User", power: "Ten Shadows Technique" }
    ],
    episodesList: [
      { num: 1, title: "Ryomen Sukuna", duration: "24m" },
      { num: 2, title: "For Myself", duration: "23m" },
      { num: 3, title: "Girl of Steel", duration: "24m" }
    ],
    bgPattern: "https://images.unsplash.com/photo-1607604276583-eef5d076aa5f?w=1200&auto=format&fit=crop&q=80"
  },
  {
    id: 3,
    title: "Solo Leveling",
    rating: "4.9",
    episodes: "12",
    studio: "A-1 Pictures",
    year: "2024",
    genres: ["Action", "Adventure", "Fantasy"],
    synopsis: "In a world where hunters must battle deadly monsters to protect mankind, Sung Jinwoo, notoriously known as the weakest hunter of all mankind, finds himself in an absolute struggle for survival within a double dungeon. Miraculously surviving, he receives a mysterious UI system that allows him to level up endlessly.",
    bannerColor: "from-cyan-600 via-blue-500 to-slate-950",
    glowColor: "shadow-cyan-500/50",
    tagline: "The weakest hunter becomes the ultimate shadow sovereign.",
    characters: [
      { name: "Sung Jinwoo", role: "Shadow Monarch", power: "Shadow Extraction & Stealth" },
      { name: "Cha Hae-In", role: "S-Rank Hunter", power: "Sword Dance" },
      { name: "Igris", role: "Shadow Commander", power: "Unmatched Swordsmanship" }
    ],
    episodesList: [
      { num: 1, title: "I'm Used to It", duration: "24m" },
      { num: 2, title: "If I Had One More Chance", duration: "24m" },
      { num: 3, title: "It's Like a Game", duration: "23m" }
    ],
    bgPattern: "https://images.unsplash.com/photo-1534447677768-be436bb09401?w=1200&auto=format&fit=crop&q=80"
  },
  {
    id: 4,
    title: "Chainsaw Man",
    rating: "4.7",
    episodes: "12",
    studio: "MAPPA",
    year: "2022",
    genres: ["Gore", "Comedy", "Dark Fantasy"],
    synopsis: "Denji is a teenage boy living with a Chainsaw Devil named Pochita. Due to the debt his father left behind, he has been living a rock-bottom life while repaying his debt by harvesting devil corpses with Pochita. One day, Denji is betrayed and killed. As his consciousness fades, he makes a contract with Pochita.",
    bannerColor: "from-orange-600 via-red-700 to-stone-900",
    glowColor: "shadow-orange-500/50",
    tagline: "A dream of a normal life, bought with blood and steel.",
    characters: [
      { name: "Denji", role: "Chainsaw Man", power: "Chainsaw Transformation" },
      { name: "Makima", role: "Control Devil", power: "Absolute Domination" },
      { name: "Power", role: "Blood Fiend", power: "Blood Manipulation" }
    ],
    episodesList: [
      { num: 1, title: "Dog & Chainsaw", duration: "25m" },
      { num: 2, title: "Arrival in Tokyo", duration: "24m" },
      { num: 3, title: "Meowy's Rescue", duration: "24m" }
    ],
    bgPattern: "https://images.unsplash.com/photo-1563089145-599997674d42?w=1200&auto=format&fit=crop&q=80"
  },
  {
    id: 5,
    title: "One Piece",
    rating: "4.9",
    episodes: "1100+",
    studio: "Toei Animation",
    year: "1999 - Present",
    genres: ["Adventure", "Fantasy", "Comedy"],
    synopsis: "Monkey D. Luffy refuses to let anyone or anything stand in the way of his quest to become the King of all Pirates. With a course charted for the treacherous waters of the Grand Line and beyond, this is one captain who'll never give up until he's claimed the greatest treasure on Earth: the Legendary One Piece!",
    bannerColor: "from-yellow-600 via-sky-500 to-blue-900",
    glowColor: "shadow-yellow-500/50",
    tagline: "Inherited Will, the Destiny of Age, and Human Dreams.",
    characters: [
      { name: "Monkey D. Luffy", role: "Captain", power: "Gear 5 & Gum-Gum Fruit" },
      { name: "Roronoa Zoro", role: "Swordsman", power: "Three-Sword Style" },
      { name: "Nami", role: "Navigator", power: "Clima-Tact Manipulation" }
    ],
    episodesList: [
      { num: 1, title: "I'm Luffy! The Man Who'll Become the Pirate King!", duration: "25m" },
      { num: 1015, title: "Straw Hat Luffy - The King of Pirates!", duration: "24m" },
      { num: 1071, title: "Luffy's Peak - Attained! Gear 5", duration: "26m" }
    ],
    bgPattern: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?w=1200&auto=format&fit=crop&q=80"
  },
  {
    id: 6,
    title: "Attack on Titan",
    rating: "4.9",
    episodes: "88",
    studio: "WIT & MAPPA",
    year: "2013 - 2023",
    genres: ["Action", "Drama", "Mystery"],
    synopsis: "After his hometown is destroyed and his mother is killed, young Eren Jaeger vows to cleanse the earth of the giant humanoid Titans that have brought humanity to the brink of extinction. However, as the mystery of the Titans unravels, the boundaries between friend and foe become tragically blurred.",
    bannerColor: "from-amber-800 via-orange-950 to-neutral-950",
    glowColor: "shadow-amber-700/50",
    tagline: "If we win, we live. If we lose, we die. If we don't fight, we can't win!",
    characters: [
      { name: "Eren Yeager", role: "Attack Titan", power: "Founding Titan Power" },
      { name: "Mikasa Ackerman", role: "Elite Scout", power: "Unmatched Ackerman Reflexes" },
      { name: "Levi Ackerman", role: "Captain", power: "Humanity's Strongest Soldier" }
    ],
    episodesList: [
      { num: 1, title: "To You, 2000 Years in the Future", duration: "24m" },
      { num: 2, title: "That Day", duration: "23m" },
      { num: 3, title: "A Dim Light Amid Despair", duration: "24m" }
    ],
    bgPattern: "https://images.unsplash.com/photo-1518709268805-4e9042af9f23?w=1200&auto=format&fit=crop&q=80"
  }
];

export default function App() {
  const [activeTab, setActiveTab] = useState('home'); // 'home', 'ai-lab', 'watchlist', 'community'
  const [searchQuery, setSearchQuery] = useState('');
  const [selectedGenre, setSelectedGenre] = useState('All');
  const [watchlist, setWatchlist] = useState([]);
  const [selectedAnime, setSelectedAnime] = useState(null);
  
  // Custom Toast Message System
  const [toastMessage, setToastMessage] = useState(null);
  
  // AI Wallpaper Generator States
  const [aiPrompt, setAiPrompt] = useState('glowing eyes neon samurai anime character, sharp illustration, highly detailed, vivid cyber colors, 4k');
  const [generatedImage, setGeneratedImage] = useState(null);
  const [isGenerating, setIsGenerating] = useState(false);
  const [aiError, setAiError] = useState(null);

  // Live Community Chat States
  const [chatUser, setChatUser] = useState('');
  const [chatInput, setChatInput] = useState('');
  const [messages, setMessages] = useState([
    { id: 1, user: "ZoroFan99", text: "Luffy's Gear 5 was absolute cinema! 🔥", time: "2 mins ago" },
    { id: 2, user: "Mikasa_Ack", text: "Solo Leveling Episode 12 left me speechless...", time: "1 min ago" },
    { id: 3, user: "GojoSatoru", text: "Don't worry, I am the strongest. 😉", time: "Just now" }
  ]);

  // Set randomized active header on start
  const [heroAnime, setHeroAnime] = useState(ANIME_DATA[0]);

  useEffect(() => {
    // Select random hero anime on load
    const randIndex = Math.floor(Math.random() * ANIME_DATA.length);
    setHeroAnime(ANIME_DATA[randIndex]);
  }, []);

  const showToast = (msg) => {
    setToastMessage(msg);
    setTimeout(() => {
      setToastMessage(null);
    }, 3000);
  };

  const toggleWatchlist = (anime) => {
    if (watchlist.some(item => item.id === anime.id)) {
      setWatchlist(watchlist.filter(item => item.id !== anime.id));
      showToast(`${anime.title} removed from Watchlist! 💔`);
    } else {
      setWatchlist([...watchlist, anime]);
      showToast(`${anime.title} added to Watchlist! 💖`);
    }
  };

  // AI Generation using imagen-4.0-generate-001 with robust exponential backoff
  const generateAIWallpaper = async () => {
    if (!aiPrompt.trim()) return;
    setIsGenerating(true);
    setAiError(null);
    setGeneratedImage(null);

    const apiKey = ""; // Environment key handled at runtime
    const url = `https://generativelanguage.googleapis.com/v1beta/models/imagen-4.0-generate-001:predict?key=${apiKey}`;
    const payload = {
      instances: [{ prompt: aiPrompt }],
      parameters: { sampleCount: 1 }
    };

    let delay = 1000;
    for (let attempt = 1; attempt <= 5; attempt++) {
      try {
        const response = await fetch(url, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        });

        if (!response.ok) {
          throw new Error(`API Status Code: ${response.status}`);
        }

        const data = await response.json();
        if (data?.predictions?.[0]?.bytesBase64Encoded) {
          const base64Url = `data:image/png;base64,${data.predictions[0].bytesBase64Encoded}`;
          setGeneratedImage(base64Url);
          setIsGenerating(false);
          showToast("Anime Wallpaper generated successfully! ✨🎨");
          return;
        } else {
          throw new Error("No image data found in response.");
        }
      } catch (err) {
        if (attempt === 5) {
          setAiError("Sorry, we couldn't generate the wallpaper. Please try again later.");
          setIsGenerating(false);
          showToast("Failed to generate AI Wallpaper. ❌");
        } else {
          await new Promise(resolve => setTimeout(resolve, delay));
          delay *= 2; // Exponential backoff
        }
      }
    }
  };

  const handleSendMessage = (e) => {
    e.preventDefault();
    if (!chatInput.trim()) return;
    const userNickname = chatUser.trim() || "Anonymous Otaku";
    const newMsg = {
      id: Date.now(),
      user: userNickname,
      text: chatInput,
      time: "Just now"
    };
    setMessages([...messages, newMsg]);
    setChatInput('');
    showToast("Comment posted! 💬");
  };

  // Extract all unique genres
  const allGenres = ['All', ...new Set(ANIME_DATA.flatMap(item => item.genres))];

  // Filtering Logic
  const filteredAnimeList = ANIME_DATA.filter(anime => {
    const matchesSearch = anime.title.toLowerCase().includes(searchQuery.toLowerCase()) || 
                          anime.genres.some(g => g.toLowerCase().includes(searchQuery.toLowerCase()));
    const matchesGenre = selectedGenre === 'All' || anime.genres.includes(selectedGenre);
    return matchesSearch && matchesGenre;
  });

  return (
    <div className="min-h-screen bg-[#0a0715] text-gray-100 font-sans selection:bg-purple-600 selection:text-white">
      
      {/* Toast Notification */}
      {toastMessage && (
        <div className="fixed top-5 right-5 z-50 bg-gradient-to-r from-purple-600 to-indigo-600 text-white px-5 py-3 rounded-xl shadow-2xl flex items-center gap-3 border border-purple-400 animate-bounce duration-300">
          <svg className="w-6 h-6 animate-pulse" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
          </svg>
          <span className="font-semibold text-sm">{toastMessage}</span>
        </div>
      )}

      {/* HEADER NAVBAR */}
      <header className="sticky top-0 z-40 backdrop-blur-md bg-[#0a0715]/80 border-b border-purple-900/40 px-4 py-3 md:px-10">
        <div className="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
          
          {/* Logo & Slogan */}
          <div className="flex items-center gap-3 cursor-pointer" onClick={() => setActiveTab('home')}>
            <div className="relative flex items-center justify-center w-12 h-12 bg-gradient-to-tr from-purple-600 via-pink-600 to-blue-500 rounded-2xl shadow-[0_0_20px_rgba(168,85,247,0.4)] hover:scale-105 transition-transform">
              <span className="text-2xl font-black tracking-tighter text-white">X</span>
              <div className="absolute -inset-0.5 bg-gradient-to-tr from-purple-500 to-pink-500 rounded-2xl blur opacity-30 group-hover:opacity-100 transition duration-1000"></div>
            </div>
            <div>
              <h1 className="text-2xl font-black bg-gradient-to-r from-purple-400 via-pink-500 to-white bg-clip-text text-transparent tracking-widest">
                ANIME <span className="text-white">X</span>
              </h1>
              <p className="text-[10px] text-purple-400 font-semibold tracking-wider uppercase">Your Ultimate Anime Hub</p>
            </div>
          </div>

          {/* Navigation Links */}
          <nav className="flex items-center gap-1 bg-purple-950/25 p-1 rounded-xl border border-purple-900/30">
            <button 
              onClick={() => setActiveTab('home')}
              className={`px-4 py-2 rounded-lg text-sm font-semibold transition-all duration-300 ${activeTab === 'home' ? 'bg-gradient-to-r from-purple-600 to-pink-600 text-white shadow-lg' : 'text-gray-400 hover:text-white'}`}>
              🔮 Discover
            </button>
            <button 
              onClick={() => setActiveTab('ai-lab')}
              className={`px-4 py-2 rounded-lg text-sm font-semibold transition-all duration-300 ${activeTab === 'ai-lab' ? 'bg-gradient-to-r from-purple-600 to-pink-600 text-white shadow-lg animate-pulse' : 'text-gray-400 hover:text-white'}`}>
              🎨 AI Creator
            </button>
            <button 
              onClick={() => setActiveTab('watchlist')}
              className={`px-4 py-2 rounded-lg text-sm font-semibold transition-all duration-300 ${activeTab === 'watchlist' ? 'bg-gradient-to-r from-purple-600 to-pink-600 text-white shadow-lg' : 'text-gray-400 hover:text-white'}`}>
              💖 My List ({watchlist.length})
            </button>
            <button 
              onClick={() => setActiveTab('community')}
              className={`px-4 py-2 rounded-lg text-sm font-semibold transition-all duration-300 ${activeTab === 'community' ? 'bg-gradient-to-r from-purple-600 to-pink-600 text-white shadow-lg' : 'text-gray-400 hover:text-white'}`}>
              💬 Fans Club
            </button>
          </nav>

          {/* Social Profiles / Streaming Indicator */}
          <div className="hidden lg:flex items-center gap-4">
            <div className="flex items-center gap-2 px-3 py-1.5 rounded-full bg-green-500/10 border border-green-500/30 text-green-400 text-xs font-bold animate-pulse">
              <span className="w-2 h-2 rounded-full bg-green-400"></span>
              9,842 Otakus Active
            </div>
          </div>
        </div>
      </header>

      {/* MAIN VIEWPORT */}
      <main className="max-w-7xl mx-auto px-4 py-6 md:px-10 pb-24">

        {/* ==================== TAB: HOME ==================== */}
        {activeTab === 'home' && (
          <div>
            
            {/* HERO DYNAMIC BANNER */}
            {heroAnime && (
              <div className="relative rounded-3xl overflow-hidden mb-12 shadow-[0_15px_50px_rgba(0,0,0,0.8)] border border-purple-500/20">
                {/* Visual Backdrop Overlay */}
                <div className="absolute inset-0 z-0 bg-cover bg-center opacity-45 transform scale-105 transition-transform duration-1000" style={{ backgroundImage: `url(${heroAnime.bgPattern})` }}></div>
                <div className={`absolute inset-0 z-10 bg-gradient-to-r ${heroAnime.bannerColor} mix-blend-multiply opacity-80`}></div>
                <div className="absolute inset-0 z-10 bg-gradient-to-t from-[#0a0715] via-transparent to-[#0a0715]/40"></div>

                <div className="relative z-20 px-6 py-12 md:p-16 flex flex-col justify-end min-h-[400px] md:min-h-[500px]">
                  <div className="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-black/40 backdrop-blur-md border border-white/20 text-xs text-yellow-400 font-bold mb-4 w-fit">
                    ⭐ TOP SELECTION
                  </div>
                  
                  <h1 className="text-4xl md:text-6xl font-black tracking-tight text-white mb-2 max-w-3xl drop-shadow-lg">
                    {heroAnime.title}
                  </h1>
                  <p className="text-purple-200 text-lg md:text-xl font-medium max-w-2xl mb-4 italic drop-shadow-md">
                    "{heroAnime.tagline}"
                  </p>
                  
                  <div className="flex flex-wrap items-center gap-3 text-xs md:text-sm text-gray-300 font-semibold mb-6">
                    <span className="bg-black/40 px-3 py-1.5 rounded-md border border-purple-500/30 text-purple-300">{heroAnime.year}</span>
                    <span className="bg-black/40 px-3 py-1.5 rounded-md border border-purple-500/30 text-purple-300">{heroAnime.studio}</span>
                    <span className="bg-yellow-400 text-black px-3 py-1.5 rounded-md font-bold">★ {heroAnime.rating}</span>
                    <span className="bg-purple-600 text-white px-3 py-1.5 rounded-md">{heroAnime.episodes} Episodes</span>
                  </div>

                  <p className="text-gray-300 text-sm md:text-base max-w-2xl line-clamp-3 mb-8">
                    {heroAnime.synopsis}
                  </p>

                  <div className="flex flex-wrap gap-4">
                    <button 
                      onClick={() => setSelectedAnime(heroAnime)}
                      className="bg-white hover:bg-purple-200 text-black font-extrabold px-8 py-3.5 rounded-xl flex items-center gap-2 transform active:scale-95 transition-all shadow-xl">
                      <svg className="w-5 h-5 fill-current" viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg>
                      Watch Episode 1
                    </button>
                    <button 
                      onClick={() => toggleWatchlist(heroAnime)}
                      className="bg-purple-950/50 hover:bg-purple-900/60 text-white font-extrabold px-6 py-3.5 rounded-xl flex items-center gap-2 border border-purple-500/30 backdrop-blur-sm transition-all">
                      {watchlist.some(i => i.id === heroAnime.id) ? '❤️ Bookmarked' : '🤍 Add to List'}
                    </button>
                  </div>
                </div>
              </div>
            )}

            {/* SECTIONS & FILTERS */}
            <div className="flex flex-col md:flex-row items-start md:items-center justify-between gap-6 mb-8 border-b border-purple-950/50 pb-6">
              
              {/* Genre Pills */}
              <div className="flex flex-wrap gap-2">
                {allGenres.map((genre) => (
                  <button
                    key={genre}
                    onClick={() => setSelectedGenre(genre)}
                    className={`px-4 py-2 rounded-full text-xs md:text-sm font-bold transition-all duration-300 ${
                      selectedGenre === genre 
                        ? 'bg-gradient-to-r from-purple-600 to-pink-600 text-white shadow-md scale-105' 
                        : 'bg-purple-950/30 text-gray-400 hover:text-white border border-purple-900/20'
                    }`}>
                    {genre}
                  </button>
                ))}
              </div>

              {/* Dynamic Search Bar */}
              <div className="relative w-full md:w-80">
                <input
                  type="text"
                  placeholder="Search characters, title, genres..."
                  value={searchQuery}
                  onChange={(e) => setSearchQuery(e.target.value)}
                  className="w-full bg-purple-950/20 text-white placeholder-gray-500 px-4 py-2.5 pl-10 rounded-xl border border-purple-900/40 focus:outline-none focus:border-purple-500 focus:ring-1 focus:ring-purple-500 transition-all text-sm"
                />
                <svg className="w-4 h-4 absolute left-3 top-3.5 text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                </svg>
                {searchQuery && (
                  <button onClick={() => setSearchQuery('')} className="absolute right-3 top-3.5 text-gray-500 hover:text-white text-xs">
                    Clear
                  </button>
                )}
              </div>

            </div>

            {/* ANIME CARDS GRID */}
            <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-8">
              {filteredAnimeList.length > 0 ? (
                filteredAnimeList.map((anime) => (
                  <div 
                    key={anime.id} 
                    className="group relative bg-[#120b24] rounded-2xl overflow-hidden border border-purple-950 hover:border-purple-500/50 transition-all duration-500 hover:-translate-y-2 hover:shadow-[0_10px_30px_rgba(168,85,247,0.15)] flex flex-col justify-between">
                    
                    {/* Beautiful SVG Art Thumbnail (Custom fallback rendering if img error) */}
                    <div className="relative h-64 overflow-hidden">
                      <div className="absolute inset-0 bg-gradient-to-t from-black/80 via-black/10 to-transparent z-10"></div>
                      
                      {/* Dynamic Background Colored Blocks for high visual aesthetic */}
                      <div className={`absolute inset-0 bg-gradient-to-br ${anime.bannerColor} opacity-20 group-hover:scale-110 transition-transform duration-700`}></div>
                      
                      <img 
                        src={anime.bgPattern} 
                        alt={anime.title} 
                        className="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700 opacity-80"
                        onError={(e) => {
                          e.target.style.display = 'none'; // hide broken images, dynamic CSS takes place
                        }}
                      />

                      {/* Overlays / Badges */}
                      <div className="absolute top-3 left-3 z-20 flex gap-1.5">
                        <span className="bg-black/60 backdrop-blur-md text-[11px] font-bold text-yellow-400 px-2.5 py-1 rounded-md border border-yellow-500/30">
                          ★ {anime.rating}
                        </span>
                        <span className="bg-purple-600 text-white text-[11px] font-bold px-2.5 py-1 rounded-md shadow-md">
                          {anime.episodes} EP
                        </span>
                      </div>

                      <button 
                        onClick={(e) => { e.stopPropagation(); toggleWatchlist(anime); }}
                        className="absolute top-3 right-3 z-20 bg-black/50 backdrop-blur-md p-2 rounded-full hover:bg-pink-600 transition-colors text-white border border-white/10">
                        {watchlist.some(i => i.id === anime.id) ? '💖' : '🤍'}
                      </button>

                      {/* Quick Genre Tags */}
                      <div className="absolute bottom-3 left-3 z-20 flex flex-wrap gap-1">
                        {anime.genres.map(g => (
                          <span key={g} className="bg-black/60 backdrop-blur-md text-[10px] text-gray-300 px-2 py-0.5 rounded-md font-medium border border-purple-500/10">
                            {g}
                          </span>
                        ))}
                      </div>
                    </div>

                    {/* Anime Content Block */}
                    <div className="p-5 flex-1 flex flex-col justify-between">
                      <div>
                        <h2 className="text-xl font-extrabold text-white group-hover:text-purple-400 transition-colors mb-2 line-clamp-1">
                          {anime.title}
                        </h2>
                        <p className="text-gray-400 text-xs mb-4 line-clamp-2 leading-relaxed">
                          {anime.synopsis}
                        </p>
                      </div>

                      {/* Bottom action elements */}
                      <div className="flex items-center justify-between pt-4 border-t border-purple-950/60 mt-auto">
                        <span className="text-[11px] text-purple-400 font-semibold tracking-wider uppercase">
                          {anime.studio}
                        </span>
                        <button 
                          onClick={() => setSelectedAnime(anime)}
                          className="text-xs font-bold text-white bg-gradient-to-r from-purple-700 to-pink-600 hover:from-purple-600 hover:to-pink-500 px-4 py-2 rounded-lg transition-all shadow-md transform active:scale-95">
                          View Details ➔
                        </button>
                      </div>
                    </div>

                  </div>
                ))
              ) : (
                <div className="col-span-full py-16 text-center">
                  <div className="w-16 h-16 bg-purple-950/30 rounded-full flex items-center justify-center mx-auto mb-4 border border-purple-900/30">
                    🔍
                  </div>
                  <h3 className="text-xl font-bold text-white mb-1">No Anime Found</h3>
                  <p className="text-gray-400 text-sm">We couldn't find anything matching your search criteria. Try another keyword!</p>
                </div>
              )}
            </div>

          </div>
        )}

        {/* ==================== TAB: AI CREATOR ==================== */}
        {activeTab === 'ai-lab' && (
          <div className="max-w-4xl mx-auto bg-[#120b24] p-6 md:p-10 rounded-3xl border border-purple-900/50 shadow-2xl relative overflow-hidden">
            
            {/* Grid background effect */}
            <div className="absolute inset-0 bg-[linear-gradient(to_right,#1f1338_1px,transparent_1px),linear-gradient(to_bottom,#1f1338_1px,transparent_1px)] bg-[size:4rem_4rem] [mask-image:radial-gradient(ellipse_60%_50%_at_50%_0%,#000_70%,transparent_100%)] opacity-30 pointer-events-none"></div>

            <div className="relative z-10 text-center max-w-2xl mx-auto mb-10">
              <span className="px-3 py-1 bg-purple-500/10 border border-purple-500/30 text-purple-300 text-xs font-bold rounded-full uppercase tracking-widest">
                AI LAB CO-CREATOR
              </span>
              <h1 className="text-3xl md:text-5xl font-black mt-3 text-white">
                Generate Custom Anime Art
              </h1>
              <p className="text-gray-400 text-sm md:text-base mt-2">
                Type your wildest anime thoughts, character descriptions, or dynamic fighting poses. Powered by <span className="text-purple-400 font-bold">Imagen 4.0</span>.
              </p>
            </div>

            <div className="relative z-10 grid grid-cols-1 md:grid-cols-12 gap-8 items-center">
              
              {/* Input Control Console */}
              <div className="md:col-span-6 flex flex-col gap-5">
                <div>
                  <label className="block text-xs font-bold text-purple-300 tracking-wider uppercase mb-2">Prompt Input Console</label>
                  <textarea
                    rows="4"
                    value={aiPrompt}
                    onChange={(e) => setAiPrompt(e.target.value)}
                    placeholder="Describe your customized anime character. Eg: Cyberpunk female anime protagonist with purple neon hair, digital weapon..."
                    className="w-full bg-purple-950/20 text-white placeholder-gray-500 p-4 rounded-2xl border border-purple-900/50 focus:outline-none focus:border-purple-500 transition-all text-sm leading-relaxed"
                  />
                </div>

                {/* Quick Prompts Helper */}
                <div>
                  <span className="block text-xs font-bold text-purple-300 uppercase tracking-widest mb-2">Try these tags:</span>
                  <div className="flex flex-wrap gap-1.5">
                    {[
                      'cyberpunk', 'retro anime 90s', 'mystical spirit foxes', 
                      'mecha battle robot', 'cherry blossoms falling', 'futuristic Tokyo neon'
                    ].map((tag) => (
                      <button
                        key={tag}
                        onClick={() => setAiPrompt(tag + " anime style, highly detailed, vibrant aesthetics, 8k")}
                        className="text-xs bg-purple-950/40 hover:bg-purple-900/60 text-purple-300 px-2.5 py-1.5 rounded-lg border border-purple-900/40 transition-all">
                        + {tag}
                      </button>
                    ))}
                  </div>
                </div>

                <button
                  onClick={generateAIWallpaper}
                  disabled={isGenerating}
                  className="w-full bg-gradient-to-r from-purple-600 via-pink-600 to-blue-500 hover:opacity-90 text-white font-extrabold py-4 rounded-xl shadow-lg transition-all transform active:scale-[0.98] disabled:opacity-50 disabled:scale-100 flex items-center justify-center gap-2">
                  {isGenerating ? (
                    <>
                      <div className="animate-spin rounded-full h-5 w-5 border-t-2 border-b-2 border-white"></div>
                      Channelling Spiritual Power... (Attempting API)
                    </>
                  ) : (
                    <>
                      🎨 Generate Wallpaper
                    </>
                  )}
                </button>

                {aiError && (
                  <div className="bg-red-500/10 border border-red-500/30 text-red-400 p-4 rounded-xl text-xs">
                    ⚠️ {aiError}
                  </div>
                )}
              </div>

              {/* Generated Image Output Screen */}
              <div className="md:col-span-6 flex flex-col items-center justify-center">
                <div className="relative w-full aspect-square bg-[#0c071a] rounded-2xl overflow-hidden border border-purple-900/30 flex flex-col items-center justify-center shadow-inner group">
                  {generatedImage ? (
                    <>
                      <img 
                        src={generatedImage} 
                        alt="AI generated Anime Wallpaper" 
                        className="w-full h-full object-cover animate-fade-in"
                      />
                      {/* Download Overlay Actions */}
                      <div className="absolute inset-0 bg-black/50 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center gap-4 z-10">
                        <a 
                          href={generatedImage} 
                          download="AnimeX-Wallpaper.png"
                          className="bg-white text-black px-4 py-2 rounded-lg text-xs font-bold hover:scale-105 transition-transform flex items-center gap-1">
                          📥 Download Art
                        </a>
                      </div>
                    </>
                  ) : isGenerating ? (
                    <div className="text-center p-6">
                      <div className="relative w-20 h-20 mx-auto mb-4">
                        <div className="absolute inset-0 rounded-full border-t-4 border-b-4 border-purple-500 animate-spin"></div>
                        <div className="absolute inset-2 rounded-full border-r-4 border-l-4 border-pink-500 animate-spin-reverse"></div>
                      </div>
                      <p className="text-purple-300 font-bold text-sm animate-pulse">Engaging Neural Networks...</p>
                      <p className="text-gray-500 text-xs mt-1">Transforming text elements to beautiful anime canvas</p>
                    </div>
                  ) : (
                    <div className="text-center p-6">
                      <div className="text-5xl mb-3 filter grayscale opacity-40">🌠</div>
                      <h4 className="text-white font-bold text-sm mb-1">Canvas screen is empty</h4>
                      <p className="text-gray-500 text-xs max-w-xs mx-auto">Your masterpiece will be rendered here. Write a prompt on the left console and hit Generate.</p>
                    </div>
                  )}
                </div>
              </div>

            </div>
          </div>
        )}

        {/* ==================== TAB: WATCHLIST ==================== */}
        {activeTab === 'watchlist' && (
          <div>
            <div className="text-center max-w-lg mx-auto mb-10">
              <span className="text-3xl">💖</span>
              <h1 className="text-3xl font-black mt-2 text-white">Your Saved Favorites</h1>
              <p className="text-gray-400 text-sm mt-1">Keep track of all the anime you intend to watch or love the most.</p>
            </div>

            {watchlist.length > 0 ? (
              <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-8">
                {watchlist.map((anime) => (
                  <div key={anime.id} className="bg-[#120b24] rounded-2xl overflow-hidden border border-purple-950 flex flex-col justify-between">
                    <div className="relative h-48 overflow-hidden">
                      <img src={anime.bgPattern} alt={anime.title} className="w-full h-full object-cover" />
                      <div className="absolute inset-0 bg-gradient-to-t from-[#120b24] via-transparent to-transparent"></div>
                      <button 
                        onClick={() => toggleWatchlist(anime)}
                        className="absolute top-3 right-3 bg-red-600/80 p-2 rounded-full text-white text-xs hover:bg-red-700 transition-all">
                        Remove
                      </button>
                    </div>
                    <div className="p-5 flex-1 flex flex-col justify-between">
                      <div>
                        <h3 className="text-lg font-extrabold text-white mb-2">{anime.title}</h3>
                        <div className="flex gap-2 mb-3">
                          <span className="bg-purple-950/80 text-[10px] px-2 py-0.5 rounded text-purple-400 font-bold">★ {anime.rating}</span>
                          <span className="bg-purple-950/80 text-[10px] px-2 py-0.5 rounded text-purple-400 font-bold">{anime.episodes} EP</span>
                        </div>
                      </div>
                      <button 
                        onClick={() => setSelectedAnime(anime)}
                        className="w-full bg-purple-950 hover:bg-purple-900 text-white font-bold py-2 rounded-xl text-xs border border-purple-500/20 transition-all">
                        Open Streaming Player
                      </button>
                    </div>
                  </div>
                ))}
              </div>
            ) : (
              <div className="text-center py-20 bg-purple-950/10 rounded-3xl border border-purple-950/40">
                <span className="text-5xl mb-4 block">🎬</span>
                <h3 className="text-xl font-bold text-white mb-1">Your Watchlist is empty</h3>
                <p className="text-gray-500 text-sm mb-6">Browse the Discover page and tap the heart icon on any anime.</p>
                <button onClick={() => setActiveTab('home')} className="bg-purple-600 hover:bg-purple-500 text-white font-bold px-6 py-2.5 rounded-xl text-sm transition-all shadow-md">
                  Browse Shows Now
                </button>
              </div>
            )}
          </div>
        )}

        {/* ==================== TAB: COMMUNITY ==================== */}
        {activeTab === 'community' && (
          <div className="max-w-4xl mx-auto grid grid-cols-1 md:grid-cols-12 gap-8">
            
            {/* Left Info Column */}
            <div className="md:col-span-4 flex flex-col gap-6">
              <div className="bg-[#120b24] p-5 rounded-2xl border border-purple-950">
                <h3 className="text-lg font-bold text-purple-300 mb-2">📢 Anime X Fans Club</h3>
                <p className="text-gray-400 text-xs leading-relaxed">
                  Discuss your favorite characters, fight strategies, ongoing plotlines, and share custom images generated in the AI Lab!
                </p>
              </div>
              <div className="bg-gradient-to-tr from-purple-900/30 to-pink-900/30 p-5 rounded-2xl border border-purple-500/10">
                <h4 className="text-sm font-bold text-white mb-2">Club Guidelines:</h4>
                <ul className="text-xs text-gray-400 space-y-2 list-disc pl-4">
                  <li>No spoilers without warnings.</li>
                  <li>Respect every fan's waifu/husbando choices.</li>
                  <li>Have fun & build anime friendship!</li>
                </ul>
              </div>
            </div>

            {/* Right Chat Box Column */}
            <div className="md:col-span-8 bg-[#120b24] rounded-3xl border border-purple-950 overflow-hidden flex flex-col justify-between shadow-2xl h-[500px]">
              {/* Chat Header */}
              <div className="bg-purple-950/40 px-6 py-4 border-b border-purple-900/40 flex items-center justify-between">
                <div>
                  <h3 className="text-sm font-bold text-white">#general-otaku-talk</h3>
                  <p className="text-[10px] text-green-400 font-semibold animate-pulse">🟢 Active Room • 12,304 Online</p>
                </div>
                <button 
                  onClick={() => setMessages([])}
                  className="text-[10px] text-purple-400 hover:text-white transition-all uppercase font-bold tracking-wider">
                  Clear Chat
                </button>
              </div>

              {/* Chat Stream */}
              <div className="flex-1 p-6 overflow-y-auto space-y-4 scrollbar-thin scrollbar-thumb-purple-900">
                {messages.map((msg) => (
                  <div key={msg.id} className="flex flex-col gap-1 items-start bg-purple-950/15 p-3 rounded-xl border border-purple-900/10 max-w-[85%]">
                    <div className="flex items-center gap-2">
                      <span className="text-xs font-black text-pink-400">{msg.user}</span>
                      <span className="text-[9px] text-gray-500">{msg.time}</span>
                    </div>
                    <p className="text-xs md:text-sm text-gray-200 leading-relaxed">{msg.text}</p>
                  </div>
                ))}
              </div>

              {/* Chat Input Console */}
              <form onSubmit={handleSendMessage} className="p-4 bg-purple-950/25 border-t border-purple-900/40 flex flex-col gap-3">
                <div className="flex gap-2">
                  <input
                    type="text"
                    placeholder="Otaku Nickname (optional)..."
                    value={chatUser}
                    onChange={(e) => setChatUser(e.target.value)}
                    className="w-1/3 bg-[#0a0715] text-white placeholder-gray-600 px-3 py-2 rounded-xl border border-purple-900/50 focus:outline-none focus:border-purple-500 text-xs"
                  />
                  <input
                    type="text"
                    placeholder="Add your message to the discussion..."
                    value={chatInput}
                    onChange={(e) => setChatInput(e.target.value)}
                    className="flex-1 bg-[#0a0715] text-white placeholder-gray-600 px-4 py-2 rounded-xl border border-purple-900/50 focus:outline-none focus:border-purple-500 text-xs"
                  />
                  <button 
                    type="submit"
                    className="bg-purple-600 hover:bg-purple-500 text-white px-5 py-2 rounded-xl text-xs font-bold transition-all transform active:scale-95">
                    Send ⚡
                  </button>
                </div>
              </form>
            </div>

          </div>
        )}

      </main>

      {/* ==================== ANIME DETAIL MODAL ==================== */}
      {selectedAnime && (
        <div className="fixed inset-0 z-50 bg-black/90 flex items-center justify-center p-4 backdrop-blur-md animate-fade-in">
          <div className="bg-[#0f0c1b] rounded-3xl overflow-hidden w-full max-w-4xl border border-purple-500/30 max-h-[90vh] overflow-y-auto shadow-[0_0_50px_rgba(168,85,247,0.3)]">
            
            {/* Modal Hero Header Banner */}
            <div className="relative h-60 md:h-80 bg-cover bg-center" style={{ backgroundImage: `url(${selectedAnime.bgPattern})` }}>
              <div className="absolute inset-0 bg-gradient-to-t from-[#0f0c1b] via-black/40 to-transparent"></div>
              <button 
                onClick={() => setSelectedAnime(null)}
                className="absolute top-4 right-4 bg-black/60 hover:bg-red-600 text-white p-2.5 rounded-full border border-white/15 transition-all text-sm font-bold leading-none">
                ✕
              </button>
              <div className="absolute bottom-4 left-6 right-6">
                <span className="bg-purple-600 text-white text-[10px] font-bold px-2.5 py-1 rounded-md uppercase mb-2 inline-block">
                  {selectedAnime.studio}
                </span>
                <h2 className="text-2xl md:text-4xl font-black text-white drop-shadow-md">
                  {selectedAnime.title}
                </h2>
              </div>
            </div>

            {/* Modal Tabs Content details */}
            <div className="p-6 md:p-8 grid grid-cols-1 md:grid-cols-12 gap-8">
              
              {/* Left detail grid info */}
              <div className="md:col-span-8 flex flex-col gap-6">
                <div>
                  <h3 className="text-xs font-bold text-purple-300 tracking-widest uppercase mb-2">STORY SUMMARY</h3>
                  <p className="text-gray-300 text-sm md:text-base leading-relaxed">
                    {selectedAnime.synopsis}
                  </p>
                </div>

                {/* Character Profiles */}
                <div>
                  <h3 className="text-xs font-bold text-purple-300 tracking-widest uppercase mb-3">KEY CHARACTERS</h3>
                  <div className="grid grid-cols-1 sm:grid-cols-3 gap-3">
                    {selectedAnime.characters.map((char, index) => (
                      <div key={index} className="bg-purple-950/20 p-3 rounded-xl border border-purple-900/30">
                        <h4 className="text-xs font-bold text-white mb-0.5">{char.name}</h4>
                        <p className="text-[10px] text-pink-400 font-semibold mb-1">{char.role}</p>
                        <p className="text-[10px] text-gray-400 italic">Power: {char.power}</p>
                      </div>
                    ))}
                  </div>
                </div>

                {/* Episodes Stream list */}
                <div>
                  <div className="flex items-center justify-between mb-3 border-b border-purple-950 pb-2">
                    <h3 className="text-xs font-bold text-purple-300 tracking-widest uppercase">EPISODES GUIDE</h3>
                    <span className="text-xs text-purple-400 font-bold">Watch Season 1</span>
                  </div>
                  <div className="space-y-2 max-h-48 overflow-y-auto pr-2">
                    {selectedAnime.episodesList.map((ep, idx) => (
                      <div 
                        key={idx} 
                        onClick={() => showToast(`Streaming Episode ${ep.num} of ${selectedAnime.title}... 🎥`)}
                        className="bg-[#120b24] hover:bg-purple-950/40 p-3 rounded-xl border border-purple-900/20 flex items-center justify-between cursor-pointer group transition-all">
                        <div className="flex items-center gap-3">
                          <span className="w-8 h-8 rounded-lg bg-purple-900/50 flex items-center justify-center text-xs text-purple-300 group-hover:bg-purple-600 group-hover:text-white font-bold transition-all">
                            {ep.num}
                          </span>
                          <span className="text-xs font-semibold text-gray-300 group-hover:text-white transition-colors">{ep.title}</span>
                        </div>
                        <span className="text-[11px] text-gray-500">{ep.duration}</span>
                      </div>
                    ))}
                  </div>
                </div>
              </div>

              {/* Right Sidebar specs */}
              <div className="md:col-span-4 flex flex-col gap-6">
                
                {/* Score Stats Card */}
                <div className="bg-gradient-to-br from-[#120b24] to-[#251545] p-5 rounded-2xl border border-purple-900/40 text-center">
                  <span className="text-[10px] font-bold text-purple-400 tracking-widest uppercase block mb-1">AUDIENCE SCORE</span>
                  <div className="text-4xl font-black text-yellow-400 mb-1">
                    ★ {selectedAnime.rating}
                  </div>
                  <p className="text-xs text-gray-400">based on 18,342 fan ratings</p>
                </div>

                {/* Specifications Checklist */}
                <div className="bg-purple-950/10 p-5 rounded-2xl border border-purple-950 space-y-3.5">
                  <div className="flex justify-between text-xs">
                    <span className="text-gray-400">Release Year:</span>
                    <span className="text-white font-bold">{selectedAnime.year}</span>
                  </div>
                  <div className="flex justify-between text-xs">
                    <span className="text-gray-400">Creative Studio:</span>
                    <span className="text-white font-bold">{selectedAnime.studio}</span>
                  </div>
                  <div className="flex justify-between text-xs">
                    <span className="text-gray-400">Format:</span>
                    <span className="text-white font-bold">TV Animation Series</span>
                  </div>
                  <div className="flex justify-between text-xs">
                    <span className="text-gray-400">Status:</span>
                    <span className="text-green-400 font-bold">Currently Streaming</span>
                  </div>
                </div>

                <div className="flex flex-col gap-2">
                  <button 
                    onClick={() => { toggleWatchlist(selectedAnime); }}
                    className="w-full bg-purple-600 hover:bg-purple-500 text-white font-bold py-3.5 rounded-xl text-sm transition-all shadow-md">
                    {watchlist.some(i => i.id === selectedAnime.id) ? '💔 Remove watchlist' : '💖 Keep in Watchlist'}
                  </button>
                  <button 
                    onClick={() => {
                      setSelectedAnime(null);
                      setActiveTab('community');
                    }}
                    className="w-full bg-purple-950 hover:bg-purple-900 text-purple-300 font-bold py-3.5 rounded-xl text-sm border border-purple-900/30 transition-all">
                    Discuss on Fans Club
                  </button>
                </div>

              </div>

            </div>

          </div>
        </div>
      )}

      {/* FOOTER BAR */}
      <footer className="bg-purple-950/20 border-t border-purple-950 py-10 mt-20">
        <div className="max-w-7xl mx-auto px-6 text-center space-y-4">
          <h2 className="text-xl font-black bg-gradient-to-r from-purple-400 to-pink-500 bg-clip-text text-transparent tracking-widest uppercase">
            ANIME X
          </h2>
          <p className="text-xs text-gray-500 max-w-md mx-auto leading-relaxed">
            All anime imagery, thumbnails, and descriptions are dynamically customized mockup instances. Custom art generator utilizes the Gemini API endpoint.
          </p>
          <div className="flex justify-center gap-6 text-xs text-purple-400 font-semibold pt-2">
            <a href="#" onClick={(e) => {e.preventDefault(); setActiveTab('home');}} className="hover:text-white transition-all">Discover Portal</a>
            <span>•</span>
            <a href="#" onClick={(e) => {e.preventDefault(); setActiveTab('ai-lab');}} className="hover:text-white transition-all">AI Wallpaper Studio</a>
            <span>•</span>
            <a href="#" onClick={(e) => {e.preventDefault(); setActiveTab('community');}} className="hover:text-white transition-all">Fans Room</a>
          </div>
          <p className="text-[10px] text-gray-600 pt-4">© 2026 Anime X Entertainment. Built with Passion for Otakus.</p>
        </div>
      </footer>

    </div>
  );
}

```
