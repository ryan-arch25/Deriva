import { useState } from "react";

// ─── BRAND COLORS ─────────────────────────────────────────────────────────────
const c = {
  cream: "#F5F0E8",
  parchment: "#EDE6D8",
  sand: "#D8CCBA",
  tan: "#C8B89A",
  gold: "#9E8660",
  mid: "#7A6E62",
  charcoal: "#3A3630",
  ink: "#1E1C18",
  bark: "#2A2520",
  white: "#FDFAF5",
};

// ─── QUIZ DATA ─────────────────────────────────────────────────────────────────
const questions = [
  { q: "What's pulling you toward a trip right now?", sub: "Select all that apply", label: "Mode", prompt: "Anything more specific pulling you?",
    opts: [{ val: "escape", text: "I need to fully disconnect" }, { val: "culture", text: "I want to learn something real" }, { val: "food", text: "I'm chasing food and wine" }, { val: "adventure", text: "I want to feel genuinely alive" }, { val: "beauty", text: "I want to be somewhere that stops me cold" }] },
  { q: "Who's making this trip with you?", sub: "Select all that apply", label: "Party", prompt: "Any context on the group dynamic?",
    opts: [{ val: "solo", text: "Just me" }, { val: "partner", text: "My partner" }, { val: "friends", text: "A group of friends" }, { val: "family", text: "Family" }, { val: "mixed", text: "A mix — it's complicated" }] },
  { q: "How long are you actually going for?", sub: "Select all that apply", label: "Duration", prompt: "Any flexibility or constraints?",
    opts: [{ val: "short", text: "Long weekend (3–4 days)" }, { val: "week", text: "One week" }, { val: "twoweeks", text: "Two weeks" }, { val: "longer", text: "Three weeks or more" }, { val: "open", text: "Flexible — I'll stay as long as it's good" }] },
  { q: "What's your honest travel vibe?", sub: "Select all that apply", label: "Style", prompt: "How do you actually travel?",
    opts: [{ val: "luxury", text: "I want to be completely taken care of" }, { val: "local", text: "I want to live like a local" }, { val: "explorer", text: "I want to go entirely off-script" }, { val: "balanced", text: "Mix of everything" }, { val: "spontaneous", text: "I figure it out when I get there" }] },
  { q: "How far outside your comfort zone do you want to go?", sub: "Select all that apply", label: "Range", prompt: "Where's your edge?",
    opts: [{ val: "safe", text: "Familiar but elevated — I know what I like" }, { val: "stretch", text: "Push me a little" }, { val: "bold", text: "Make me the first one there" }, { val: "wild", text: "I have no limits, surprise me" }, { val: "depends", text: "Depends — bold on some things, not others" }] },
  { q: "What kind of scenery feeds you?", sub: "Select all that apply", label: "Scenery", prompt: "What does your ideal backdrop look like?",
    opts: [{ val: "coast", text: "Coast and water" }, { val: "mountains", text: "Mountains and dramatic landscapes" }, { val: "cities", text: "Dense cities with layers of history" }, { val: "countryside", text: "Countryside, villages, slow pace" }, { val: "desert", text: "Desert, volcanoes, extreme landscapes" }] },
  { q: "What does a perfect travel day look like?", sub: "Select all that apply", label: "Day", prompt: "Describe your ideal day if you want",
    opts: [{ val: "wander", text: "No plan, just wander and see what happens" }, { val: "eat", text: "Market in the morning, long lunch, repeat" }, { val: "explore", text: "Hire a car, drive into the unknown" }, { val: "absorb", text: "One museum, one neighborhood, absorb it all" }, { val: "nothing", text: "A great view, a great book, nowhere to be" }, { val: "physical", text: "Something physical — a long hike, a swim, movement" }, { val: "fullday", text: "Up early, out late — full immersion from sunrise" }, { val: "spontaneous", text: "Something spontaneous I couldn't have planned" }] },
  { q: "What's your actual budget?", sub: "Select all that apply", label: "Budget", prompt: "Any specifics on how you spend?",
    opts: [{ val: "budget", text: "Keeping it lean — experiences over comfort" }, { val: "midrange", text: "Mid-range, splurge when it's worth it" }, { val: "flexible", text: "I spend on what matters, save on what doesn't" }, { val: "open", text: "Money isn't the question" }] },
  { q: "How do you actually research trips?", sub: "Select all that apply", label: "Research", prompt: "How do you find places?",
    opts: [{ val: "none", text: "I don't — I just go and figure it out" }, { val: "article", text: "One good article or recommendation and I'm sold" }, { val: "deep", text: "I research obsessively before committing" }, { val: "people", text: "I ask someone who's actually been" }, { val: "feel", text: "I look at photos and go with what feels right" }] },
  { q: "What do you never want to do again on a trip?", sub: "Select all that apply — and write your own", label: "Never Again", prompt: "What's your hard no?",
    opts: [{ val: "crowds", text: "Fight through crowded tourist sites" }, { val: "rushed", text: "Pack too much into too little time" }, { val: "generic", text: "Stay somewhere that could be anywhere" }, { val: "badsleep", text: "Compromise on where I sleep" }, { val: "tourist", text: "Feel like a tourist the whole time" }] },
  { q: "What's a trip you almost took but didn't?", sub: "Free text — this one matters", label: "Almost", prompt: "Tell us — destination, what stopped you, what you were imagining",
    opts: [] },
];

// ─── DESTINATION MATCHING ──────────────────────────────────────────────────────
const destinations = {
  portugal: {
    name: "Portugal", region: "Southern Europe", tag: "Wine · Coast · Culture",
    hook: "Everyone flies over it on the way somewhere else. That's your advantage.",
    why: "Portugal right now is that rare moment — world-class food, wine, and hospitality before prices fully catch up to the reputation. The people who went five years ago still can't stop talking about it. Go before the next wave figures it out.",
    img: "https://images.unsplash.com/photo-1555881400-74d7acaacd8b?w=1200&q=80",
    match: (a) => { let s = 0; if (a[0]?.includes("food")||a[0]?.includes("escape")) s+=3; if (a[0]?.includes("culture")) s+=2; if (a[3]?.includes("local")||a[3]?.includes("balanced")) s+=2; if (a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if (a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=2; if (a[6]?.includes("eat")||a[6]?.includes("wander")) s+=2; return s; },
  },
  italy: {
    name: "Italy", region: "Southern Europe", tag: "Food · History · Landscape",
    hook: "Skip Rome. The Italy worth finding is still waiting to be found.",
    why: "Italy is one of those places where everybody thinks they've done it — they did Rome and Florence in a week and checked the box. The real Italy, the one that changes you, is Puglia at harvest time, a borrowed Fiat on a Sicilian cliff road, the Dolomites at dawn. That Italy is completely open.",
    img: "https://images.unsplash.com/photo-1516483638261-f4dbaf036963?w=1200&q=80",
    match: (a) => { let s = 0; if (a[0]?.includes("food")||a[0]?.includes("culture")) s+=3; if (a[3]?.includes("local")||a[3]?.includes("explorer")) s+=2; if (a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if (a[5]?.includes("mountains")||a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=2; if (a[6]?.includes("eat")||a[6]?.includes("explore")) s+=2; if (a[2]?.includes("twoweeks")||a[2]?.includes("week")) s+=1; return s; },
  },
  iceland: {
    name: "Iceland", region: "North Atlantic", tag: "Landscape · Raw · Adventure",
    hook: "It looks fake. It isn't.",
    why: "Iceland is one of the few places left where the landscape genuinely stops you cold. Waterfalls you can walk behind, black sand beaches that look like another planet, hot springs in the middle of nowhere. It has no equivalent.",
    img: "https://images.unsplash.com/photo-1531366936337-7c912a4589a7?w=1200&q=80",
    match: (a) => { let s = 0; if (a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=3; if (a[3]?.includes("explorer")) s+=3; if (a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if (a[5]?.includes("mountains")||a[5]?.includes("desert")) s+=3; if (a[6]?.includes("explore")) s+=2; return s; },
  },
  chile: {
    name: "Chile", region: "South America", tag: "Desert · Patagonia · Fjords",
    hook: "From the driest desert on earth to the end of the world. One country, impossible variety.",
    why: "Chile is 4,300km long and averages 177km wide — the most geographically extreme country on earth. The Atacama in the north gets no rain. Patagonia in the south gets everything. Between them: wine valleys, lakes, volcanoes, fjords, and an island with its own mythology. Nobody has done all of it.",
    img: "https://images.unsplash.com/photo-1501854140801-50d01698950b?w=1200&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=2; if(a[6]?.includes("explore")) s+=2; return s; },
  },
  spain: {
    name: "Spain", region: "Southern Europe", tag: "Food · Energy · Coast",
    hook: "San Sebastián has more Michelin stars per capita than anywhere on earth. You probably haven't been.",
    why: "Spain gets unfairly flattened into Barcelona and Madrid. The real draw is the regional diversity — Basque Country, Andalusia, the Canary Islands, the coast between Valencia and Alicante. Each one a completely different country inside a country.",
    img: "https://images.unsplash.com/photo-1543783207-ec64e4d95325?w=1200&q=80",
    match: (a) => { let s = 0; if (a[0]?.includes("food")||a[0]?.includes("culture")) s+=3; if (a[1]?.includes("friends")||a[1]?.includes("partner")) s+=1; if (a[3]?.includes("local")||a[3]?.includes("balanced")) s+=2; if (a[5]?.includes("coast")||a[5]?.includes("cities")) s+=2; if (a[6]?.includes("eat")||a[6]?.includes("wander")) s+=2; return s; },
  },
  japan: {
    name: "Japan", region: "East Asia", tag: "Culture · Food · Precision",
    hook: "Nowhere on earth is this considered normal. That is the point.",
    why: "Japan operates on a completely different frequency. The precision, the food culture, the way beauty shows up in completely unexpected places — a bowl of ramen, a train departure, a temple garden. It recalibrates how you see everything else.",
    img: "https://images.unsplash.com/photo-1493976040374-85c8e12f0c0e?w=1200&q=80",
    match: (a) => { let s = 0; if (a[0]?.includes("culture")||a[0]?.includes("food")) s+=3; if (a[3]?.includes("explorer")||a[3]?.includes("local")) s+=2; if (a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=2; if (a[5]?.includes("cities")||a[5]?.includes("mountains")) s+=2; if (a[6]?.includes("absorb")||a[6]?.includes("eat")) s+=2; return s; },
  },
  oman: {
    name: "Oman", region: "Middle East", tag: "Desert · Fjords · Frankincense",
    hook: "The most hospitable country in the Middle East. The Gulf capital that chose not to become Dubai. The desert camps that have been here for 3,000 years.",
    why: "Oman is what the Gulf used to be before the money arrived — traditional, genuine, and extraordinarily beautiful. The Wahiba Sands, the fjords of the Musandam, the mountain plateau of Jebel Akhdar, and the ancient souqs of Muscat are all completely different and all completely extraordinary.",
    img: "https://images.unsplash.com/photo-1578895101408-1a36b834405b?w=1200&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("desert")||a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; return s; },
  },
  australia: {
    name: "Australia", region: "South Pacific", tag: "Wilderness · Reef · Red Centre",
    hook: "Most people see the cities. The country is somewhere else entirely.",
    why: "Australia is so large and so varied that most visitors see almost none of it. The Red Centre, the Kimberley, Tasmania, and Kangaroo Island are completely different countries inside one country. The reef is real, the rock is real, and the wilderness is the most remote and extraordinary on earth.",
    img: "https://images.unsplash.com/photo-1529108190281-9a4f620bc2d8?w=1200&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=3; if(a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=3; if(a[5]?.includes("desert")||a[5]?.includes("coast")||a[5]?.includes("mountains")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=2; return s; },
  },
  georgia: {
    name: "Georgia", region: "Caucasus", tag: "Wine · Towers · Mountains",
    hook: "The country that invented wine 8,000 years ago. The medieval towers of Svaneti. A capital city that is one of the great undiscovered food destinations in the world.",
    why: "Georgia is the most surprising country in the world right now — a place where the food and wine culture is extraordinary, the landscapes are extreme, and almost nobody you know has been. The Caucasus mountains, the ancient wine region of Kakheti, and the towers of Svaneti are all completely different and all completely worth going for.",
    img: "https://images.unsplash.com/photo-1565008576549-57569a49371d?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")||a[0]?.includes("adventure")) s+=3; if(a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=4; if(a[5]?.includes("mountains")||a[5]?.includes("cities")||a[5]?.includes("countryside")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; return s; },
  },
  colombia: {
    name: "Colombia", region: "South America", tag: "Caribbean · Coffee · Transformation",
    hook: "Cartagena's walls have been standing since 1586. Medellin was the murder capital of the world in 1991 and is now a city that urban planners fly in to study. The coffee is from here.",
    why: "Colombia is the most complex country in South America — the Caribbean coast, the Andean cities, the coffee region, and the Amazon are all completely different countries inside one border. The transformation story of Medellin alone is worth the flight.",
    img: "https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")||a[0]?.includes("adventure")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("cities")||a[5]?.includes("mountains")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=3; return s; },
  },
  vietnam: {
    name: "Vietnam", region: "Southeast Asia", tag: "Pho · Karsts · Ancient Towns",
    hook: "The most beautiful 50 cents you will ever spend is a glass of bia hoi on a plastic stool in Hanoi. The rest is extraordinary too.",
    why: "Vietnam is 1,650km of coastline, mountain rice terraces in the north, ancient trading ports in the center, and a Mekong Delta in the south that feeds half of Southeast Asia. The food culture is one of the great undiscovered ones in the world. The history is everywhere and treated with honesty.",
    img: "https://images.unsplash.com/photo-1509030450996-dd1a26dda07a?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")||a[0]?.includes("adventure")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("mountains")||a[5]?.includes("cities")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=2; return s; },
  },
  newzealand: {
    name: "New Zealand", region: "South Pacific", tag: "Fiords · Adventure · Landscape",
    hook: "The landscape here is so extreme it was used to represent another world. It is not another world. It is just New Zealand.",
    why: "New Zealand is two islands of completely different character — the South Island is raw wilderness, the North Island is subtropical, Maori culture, and the most underrated capital city in the Southern Hemisphere. The Fiordland national park alone covers more land than some countries. Almost no one has seen all of it.",
    img: "https://images.unsplash.com/photo-1507699622108-4be3abd695ad?w=1200&q=80",
    match: (a) => { let s = 0; if (a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=3; if (a[3]?.includes("explorer")) s+=3; if (a[4]?.includes("wild")||a[4]?.includes("bold")) s+=3; if (a[5]?.includes("mountains")||a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=3; if (a[6]?.includes("physical")||a[6]?.includes("explore")||a[6]?.includes("nothing")) s+=2; return s; },
  },
};

function getMatch(answers) {
  const allRegions = [
    ...portugalRegions.map(r => ({ ...r, country: "portugal" })),
    ...italyRegions.map(r => ({ ...r, country: "italy" })),
    ...spainRegions.map(r => ({ ...r, country: "spain" })),
    ...chileRegions.map(r => ({ ...r, country: "chile" })),
    ...icelandRegions.map(r => ({ ...r, country: "iceland" })),
    ...japanRegions.map(r => ({ ...r, country: "japan" })),
    ...newZealandRegions.map(r => ({ ...r, country: "newzealand" })),
    ...omanRegions.map(r => ({ ...r, country: "oman" })),
    ...georgiaRegions.map(r => ({ ...r, country: "georgia" })),
    ...colombiaRegions.map(r => ({ ...r, country: "colombia" })),
    ...vietnamRegions.map(r => ({ ...r, country: "vietnam" })),
    ...australiaRegions.map(r => ({ ...r, country: "australia" })),
  ];
  const scored = allRegions.map(r => ({ ...r, score: r.match(answers) }));
  scored.sort((a, b) => b.score - a.score);
  return scored[0];
}

// ─── PORTUGAL REGIONS (each carries its own eat + stay data) ──────────────────
const portugalRegions = [
  {
    name: "Lisbon", country: "portugal", tag: "City · Neighborhoods · Nightlife",
    hook: "Everyone thinks they know Lisbon after two days. They don't.",
    img: "https://images.unsplash.com/photo-1555881400-74d7acaacd8b?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("culture")) s+=3; if(a[3]?.includes("local")||a[3]?.includes("balanced")) s+=2; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("cities")) s+=3; if(a[6]?.includes("eat")||a[6]?.includes("wander")) s+=2; if(a[1]?.includes("solo")||a[1]?.includes("partner")) s+=1; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("surprise")||a[8]?.includes("connection")) s+=2; if(a[9]?.includes("sit")||a[9]?.includes("eat")) s+=2; if(a[8]?.includes("article")||a[8]?.includes("people")) s+=2; if(a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=1; if(a[6]?.includes("fullday")||a[6]?.includes("spontaneous")) s+=1; return s; },
    intro: "Everyone lands in Lisbon and thinks they know it after two days. They don't. Lisbon rewards the people who stay long enough to get past the Alfama viewpoints. It's actually a collection of very different neighborhoods — each with its own personality, its own food scene, its own crowd.",
    highlights: [
      { label: "Mouraria", text: "The oldest neighborhood. Fado spills from open windows, streets narrow enough to touch both walls, restaurants with no menus and no English — just whatever was good at the market that morning." },
      { label: "LX Factory", text: "Repurposed textile factory in Alcântara with some of the best independent restaurants and bars in the city. Go on Sunday when the market runs." },
      { label: "Príncipe Real", text: "The neighborhood locals actually live in when they can afford to. Antique shops, wine bars, a Saturday market that's better than any tourist market you've been to." },
      { label: "Sintra (30 min by train)", text: "Fairy-tale palaces on forested hills above the Atlantic. Pena Palace is the famous one — get there before 9am or it's wall-to-wall crowds. The walk down through the forest to Cabo da Roca, the westernmost point of Europe, is the real reason to come." },
      { label: "Cascais (40 min by train)", text: "The coastal town at the end of the Lisbon Riviera. Better beaches than anything near the city, a good fish market, and the kind of easy afternoon that turns into dinner and a late train back. Locals come here to decompress." },
    ],
    eat: [
      { name: "Belcanto", desc: "José Avillez's flagship — two Michelin stars, modern Portuguese, the tasting menu is one of the best meals you'll have in Europe. Book two months out." },
      { name: "Solar dos Presuntos", desc: "Old-school tasca doing northern Portuguese cuisine properly. The presunto and the açorda are definitive. Book ahead." },
      { name: "Cantinho do Avillez", desc: "The casual sibling of Belcanto. Great for lunch, no reservation needed if you go at noon." },
      { name: "A Cevicheria", desc: "The best ceviche in the city from a chef who did serious restaurant time. Lunch only — get there early." },
      { name: "Pastéis de Belém", desc: "The original pastel de nata. The queue moves fast. Get four." },
      { name: "Mercado da Ribeira", desc: "Time Out Market — yes, touristy, but the food stalls are legitimately good and the beer selection is serious." },
    ],
    stay: [
      { name: "Bairro Alto Hotel", tier: "High end", desc: "The best hotel in the city center. Rooftop bar, beautiful rooms, staff that actually knows Lisbon." },
      { name: "1908 Lisboa Hotel", tier: "Mid range", desc: "Converted pharmacy in Intendente neighborhood. Beautifully designed, genuinely good location for exploring on foot." },
      { name: "Alfama District Apartments", tier: "Good value", desc: "Old tilework, rooftop access, walk to everything. Best neighborhood to stay in Lisbon. Book direct on Airbnb." },,
      { name: "Bairro Alto Hotel", tier: "High end", desc: "The most design-forward hotel in Lisbon — a 18th-century palace on the edge of the Bairro Alto, with a rooftop terrace looking over the city to the Tagus. The bar at dusk is the best in Lisbon." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October are the sweet spots. The light is extraordinary and the city hasn't hit peak-summer saturation. July–August is busy and hot (30–35°C). March–April is underrated — quieter, cheaper, and the pastéis de nata taste the same." },
      { q: "Getting there", a: "Humberto Delgado Airport (LIS) is well connected from the US and all of Europe. The metro red line runs directly from the airport to the city center in 20 minutes for €1.65. Skip the taxi queue." },
      { q: "Getting around", a: "Lisbon is walkable but hilly — the trams are iconic but slow. Metro is fast and cheap (€1.65 flat). Uber works well and is inexpensive. For Sintra and Cascais, the suburban train (Comboios de Portugal) runs directly from Cais do Sodré and Rossio stations." },
      { q: "How long", a: "Four nights minimum to get past the surface. Two days of Lisbon proper, one day for Sintra, one day for Cascais or Setúbal. If you leave after two days, you've only seen the postcard version." },
      { q: "Money", a: "€3–4 for espresso and pastel de nata, €15–25 for a solid tasca lunch with wine, €40–70 at a serious dinner. Tipping is not expected but 5–10% is appreciated. Cards work everywhere. Multibanco ATMs don't charge foreign fees." },
      { q: "Neighborhoods", a: "Stay in Alfama, Mouraria, or Príncipe Real — not near the waterfront tourist strip. Bairro Alto is great for nightlife but loud at 3am. For families or a quieter stay, Belém is beautiful and underrated." },
    ],
  },
  {
    name: "Porto", country: "portugal", tag: "Wine · River · Grit",
    hook: "Porto is what Lisbon was ten years ago. Go now.",
    img: "https://images.unsplash.com/photo-1564564321837-a57b7070ac4f?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("culture")) s+=2; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("cities")||a[5]?.includes("countryside")) s+=2; if(a[6]?.includes("eat")||a[6]?.includes("wander")) s+=2; if(a[2]?.includes("short")||a[2]?.includes("week")) s+=1; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("connection")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("eat")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("article")) s+=2; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")) s+=1; if(a[6]?.includes("fullday")||a[6]?.includes("spontaneous")) s+=1; return s; },
    intro: "Porto is what Lisbon was ten years ago — slightly rougher, significantly cheaper, and completely magnetic. Built on hills above the Douro River, it's a city that makes no effort to be pretty and ends up being one of the most beautiful places in Europe.",
    highlights: [
      { label: "The wine caves", text: "Vila Nova de Gaia sits across the river and holds virtually every major Port wine house. Most offer tastings. Graham's has the best terrace view in the city." },
      { label: "Mercado do Bolhão", text: "Renovated but still legitimate. Go early, have a coffee at the counter, buy cheese, eat a francesinha somewhere nearby." },
      { label: "Matosinhos", text: "The coastal neighborhood that locals go to for the best grilled fish in Portugal. Fifteen minutes from central Porto and almost nobody goes." },
    ],
    eat: [
      { name: "The Yeatman Restaurant", desc: "The wine hotel's restaurant. Views over the Douro, serious wine list, tasting menu built around Portuguese producers. Worth every euro." },
      { name: "DOP", desc: "Rui Paula's restaurant in a converted palace. Elevated regional food without the Michelin price tag." },
      { name: "Restaurante O Paparico", desc: "Local institution. The kitchen closes when the food runs out. Go early or call ahead." },
      { name: "Café Santiago", desc: "Order the francesinha — Porto's signature sandwich in a meat-and-cheese sauce — with a cold Super Bock. This is the one." },
      { name: "Taberna dos Mercadores", desc: "Small wine bar near the cathedral. Excellent petiscos and the kind of local wine list you won't find online." },
    ],
    stay: [
      { name: "The Yeatman", tier: "High end", desc: "Wine hotel in Gaia with the best views in the city. Every room has a wine minibar stocked with serious bottles." },
      { name: "Torel Avantgarde", tier: "Mid range", desc: "Hilltop boutique hotel with a pool, terraced gardens, reasonable prices for what you get." },
      { name: "Ribeira Area Apartments", tier: "Good value", desc: "The historic riverside neighborhood. A bit loud at night, completely worth it. Great base for exploring on foot." },,
      { name: "Flores Village Hotel", tier: "Good value", desc: "Boutique hotel in a row of converted townhouses in the Flores street district. Individually designed rooms, warm service, walking distance to the Ribeira. The best mid-range discovery in Porto." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October. Porto's Atlantic weather means it can rain any month — pack a layer. July–August is peak season and the city genuinely fills up. December is underrated: quieter, cheaper, and the Christmas markets in Aliados are excellent." },
      { q: "Getting there", a: "Francisco Sá Carneiro Airport (OPO) is 20 minutes from the city center by Metro line E (violet). €2.25 to the center. Direct flights from the US are limited — most connect through Lisbon or London. Flying into Lisbon and taking the train to Porto (3 hours, €25–35) is often the smarter move." },
      { q: "Getting around", a: "Porto is a walking city, but the hills are serious. Tram line 22 is useful and historic. Uber works well. For Matosinhos (the seafood neighborhood), it's a 15-minute Uber or Metro line A. For the Douro Valley wine country, you need a car — rent from the airport." },
      { q: "How long", a: "Three nights is ideal. Two full days for the city — Ribeira, the wine caves in Gaia, Matosinhos for dinner — plus a day trip up the Douro by train or car. Porto pairs naturally with the Douro Valley: add two nights in Pinhão and you have the best five-day trip in northern Portugal." },
      { q: "Money", a: "Porto is cheaper than Lisbon. €2.50 for a coffee and pastel de nata at a counter, €12–20 for lunch at a tasca. The Yeatman's tasting menu is worth the splurge (€120+). Port wine tastings at the caves in Gaia run €15–30 and are almost always worth it." },
      { q: "The vibe", a: "Porto is grittier and more local than Lisbon. Less tourist infrastructure, more genuine neighborhood life. The people are direct and warm. Don't mistake the rougher edges for unwelcome — Porto is one of the most hospitable cities in Europe." },
    ],
  },
  {
    name: "Douro Valley", country: "portugal", tag: "Wine · Landscape · Quiet",
    hook: "One of the great wine regions of the world. Almost nobody goes.",
    img: "https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("luxury")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("eat")||a[6]?.includes("explore")) s+=2; if(a[1]?.includes("partner")) s+=2; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=2; if(a[8]?.includes("quiet")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("sit")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("people")) s+=2; if(a[9]?.includes("crowds")||a[9]?.includes("rushed")) s+=2; return s; },
    intro: "Terraced vineyards dropping into a river valley, quintas producing wine they've made the same way for centuries, and almost no one from outside Portugal. The Douro is one of the great undiscovered wine regions of the world — mostly because getting there requires effort.",
    highlights: [
      { label: "The train from Porto", text: "The Douro line from Porto to Pinhão is genuinely one of the best train journeys in Europe. Three hours of river views, no tour bus involved." },
      { label: "Quinta do Crasto", text: "One of the best estates in the valley. Call ahead, book a tasting, stay if you can. The table wine is better than most €40 bottles you've had elsewhere." },
      { label: "Pinhão village", text: "The hub of the valley. Tiny, beautiful tiled train station, one good restaurant, best base for exploring further east." },
    ],
    eat: [
      { name: "Quinta do Vallado Restaurant", desc: "Estate dining on a working winery. The meal is whatever was made that day with whatever was harvested that season. Book ahead." },
      { name: "DOC Restaurant (Folgosa)", desc: "Rui Paula's Douro outpost. Glass cube suspended over the river, lamb slow-cooked in the valley clay, serious wine list." },
      { name: "Tasquinha da Tia Bia (Pinhão)", desc: "The local lunch spot in Pinhão village. No menu. Whatever the owner made. One of the best meals in Portugal." },
    ],
    stay: [
      { name: "Six Senses Douro Valley", tier: "High end", desc: "The benchmark luxury estate in the valley. Converted 19th-century manor, vineyard views from every room, wine spa." },
      { name: "Quinta do Crasto", tier: "Mid range", desc: "Stay on the estate itself. Simple rooms, extraordinary location, tasting included. Book months ahead." },
      { name: "Casa da Calcada (Amarante)", tier: "Mid range", desc: "Baroque manor house just outside the valley. Better value than the valley quintas and just as beautiful." },,
      { name: "Casa de Canilhas (Sabrosa)", tier: "Good value", desc: "A 19th-century manor house in the hills above the Douro run by the family that built it. Five rooms, breakfasts using their own farm produce, wine from the estate. The most authentic stay in the valley." },
    ],
    logistics: [
      { q: "When to go", a: "September–October is the window — harvest season, warm days, cool nights, and the valley smells of fermenting grapes. May–June is beautiful and green. July–August is hot (35–40°C) but the river keeps things tolerable." },
      { q: "Getting there", a: "The train from Porto (Douro line) to Pinhão takes 2.5 hours and is one of the great train journeys in Europe — river views the entire way, €15–20 each way. Or rent a car and drive the N222 along the south bank of the Douro, one of the best driving roads in the world." },
      { q: "Getting around", a: "You need a car to explore properly. The valley roads are narrow and winding — take your time. The N222 along the river is the main artery. Pinhão village is the hub and walkable once you arrive." },
      { q: "How long", a: "Two nights at a quinta is the right amount. Day one: arrive, winery visit and tasting. Day two: drive further east into the upper Douro. Day three: slow morning, train back to Porto. The valley pairs perfectly with Porto as a 4–5 day northern Portugal trip." },
      { q: "Money", a: "Luxury quintas run €400–800 a night. Mid-range quinta stays €150–250. Wine tastings at estates €15–50. Local restaurants in Pinhão are genuinely affordable — €20–35 for a serious meal with wine." },
      { q: "What to buy", a: "Wine, bought directly from the quintas — you'll pay less than at home and can taste before committing. Quinta do Crasto, Quinta do Vale Meão, and Ramos Pinto are all worth visiting. Most estates ship internationally." },
    ],
  },
  {
    name: "Alentejo", country: "portugal", tag: "Slow · Wine · Countryside",
    hook: "The antidote to everywhere else. It will slow you down on purpose.",
    img: "https://images.unsplash.com/photo-1591113580684-e4c3f8d6c8c6?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("food")) s+=3; if(a[3]?.includes("luxury")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("safe")) s+=2; if(a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("eat")||a[6]?.includes("wander")) s+=3; if(a[1]?.includes("partner")||a[1]?.includes("solo")) s+=1; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=1; if(a[8]?.includes("quiet")||a[8]?.includes("freedom")) s+=3; if(a[9]?.includes("sit")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("none")||a[8]?.includes("feel")) s+=2; if(a[9]?.includes("crowds")||a[9]?.includes("rushed")) s+=3; return s; },
    intro: "The vast cork oak plains of southern Portugal. Alentejo moves at a different pace entirely — long lunches, afternoon silence, wine drunk under shade in someone's courtyard. It's the antidote to everywhere else.",
    highlights: [
      { label: "Évora", text: "A UNESCO World Heritage walled city that most people skip entirely. Roman temple in the center, bone chapel in a church, restaurants where lunch takes three hours by design." },
      { label: "Monsaraz", text: "A medieval hilltop village so well preserved it barely seems real. Almost no one lives there year-round. Spectacular at sunset." },
      { label: "The wine", text: "Alentejo produces some of Portugal's most serious red wines. Herdade do Esporão is the benchmark estate — they do excellent winery visits." },
    ],
    eat: [
      { name: "Restaurante Fialho (Évora)", desc: "The institution. Three generations, same recipes, same room. The migas (bread-based side), pork with clams, and Alentejo wine. Book ahead." },
      { name: "Herdade do Esporão Restaurant", desc: "Winery restaurant on the estate. The food is as serious as the wine. Go for the tasting menu at lunch on a day visit." },
      { name: "Taberna Típica Quarta-Feira (Évora)", desc: "Tiny, no reservations, shows up on no lists. The bacalhau (salt cod) is the best version of Portugal's national dish you'll find." },
    ],
    stay: [
      { name: "Sublime Comporta", tier: "High end", desc: "Rice fields, cork oaks, a pool that seems to disappear into the landscape. The most beautiful hotel in Portugal." },
      { name: "Herdade da Malhadinha Nova", tier: "High end", desc: "Working winery estate with rooms. Horses, dogs, a pool, and bottles of their wine waiting when you arrive." },
      { name: "Casa de Terena", tier: "Mid range", desc: "18th-century manor house converted to a small inn. Stone floors, wood beams, the owner cooks breakfast. Book direct." },,
      { name: "Monte da Ravasqueira (Arraiolos)", tier: "High end", desc: "A working wine and olive estate converted into a luxury guest house — private pool, farm dinners, horseback rides through the cork forest. The full Alentejo experience in one property." },
    ],
    logistics: [
      { q: "When to go", a: "April–May and September–October. The plains bloom in spring and the heat is manageable. July–August is brutal — 38–42°C in the interior — but if you're at a pool on an estate it's actually wonderful. The silence in winter is extraordinary if you don't mind everything being closed." },
      { q: "Getting there", a: "Évora is 1.5 hours from Lisbon by car on the A6. There's also a train from Lisbon's Oriente station (€12–18, about 1.5 hours). For the rural Alentejo — Monsaraz, Herdade do Esporão, the estates — you need a car. Rent in Lisbon before leaving." },
      { q: "Getting around", a: "Car is essential. The Alentejo is vast and flat, the distances between towns are long, and there's almost no public transport connecting the villages. Roads are excellent and traffic is minimal. Drive with the windows down." },
      { q: "How long", a: "Two to three nights. Évora deserves a full day. Monsaraz at sunset is an afternoon. A winery visit at Esporão or Malhadinha takes a morning. Combine with Comporta to the west for a complete southern Portugal week." },
      { q: "Money", a: "The most affordable region in mainland Portugal. A three-course lunch with Alentejo wine at a proper restaurant in Évora: €20–30 per person. The luxury estates (Sublime Comporta, Malhadinha) run €200–500 but deliver extraordinary value for what they are." },
      { q: "The pace", a: "Alentejo runs on its own clock. Lunch starts at 1:30pm and goes until 4pm. Shops close in the afternoon. Nobody is rushing. If you arrive with a tight itinerary and an urgency to tick boxes, the Alentejo will quietly resist you. Let it." },
    ],
  },
  {
    name: "Algarve", country: "portugal", tag: "Coast · Cliffs · Sea",
    hook: "Go to the western end. The development stops and the cliffs take over.",
    img: "https://images.unsplash.com/photo-1548782996-7e0b8e735441?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("adventure")) s+=2; if(a[3]?.includes("balanced")||a[3]?.includes("explorer")) s+=2; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("coast")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("explore")) s+=2; if(a[1]?.includes("friends")||a[1]?.includes("family")) s+=2; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=1; if(a[8]?.includes("freedom")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("deep")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=1; return s; },
    intro: "Yes, the Algarve is touristy. It's also genuinely one of the most dramatic coastlines in Europe. The trick is going to the western end — the Alentejo coast and the area around Sagres, where the development stops and the cliffs take over.",
    highlights: [
      { label: "Sagres and the Southwest tip", text: "The furthest southwest point of continental Europe. The wind is constant, the cliffs are vertical, the light is extraordinary. Feels like the edge of the world." },
      { label: "Tavira in the east", text: "The most underrated town on the coast. Old, beautiful, authentic, and a completely different experience from the resort strip further west." },
    ],
    eat: [
      { name: "Casa Velha (Sagres)", desc: "Small, right in Sagres town, the freshest fish you've ever eaten because it came off a boat two hours ago. No reservations, arrive at noon." },
      { name: "Quatro Aguas (Tavira)", desc: "On the waterfront in Tavira, traditional Algarvian seafood. The cataplana (seafood stew cooked in a copper pot) is what you order." },
      { name: "Mar à Vista (Lagos)", desc: "Grilled fish, view of the sea, no frills. The kind of lunch that takes three hours and feels like the point of the whole trip." },
    ],
    stay: [
      { name: "Boca do Rio Estate", tier: "High end", desc: "Isolated clifftop property between Sagres and Lagos. Private beach access, no neighbors, extraordinary sunsets." },
      { name: "Hotel Memmo Baleeira (Sagres)", tier: "Mid range", desc: "Design hotel at the edge of Sagres. Modern, well-priced, right next to the best surf beach." },
      { name: "Tavira Old Town Apartments", tier: "Good value", desc: "Stay inside the walled old city. Walk to the market, the river, the best restaurants. Much better than any resort hotel." },,
      { name: "Casa Modesta (Olhão)", tier: "Good value", desc: "A converted farmhouse in the Ria Formosa marshes near Olhão. Kayaks, bicycles, a salt water pool, and a kitchen stocked from the local market. The alternative to the Algarve resort strip." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October for the coast. July–August is peak season — beaches are crowded, prices spike 30–40%, and Albufeira and the central Algarve become a different country. For surf (Sagres, Arrifana, Aljezur), October through March is when the Atlantic swells run and the crowds disappear entirely." },
      { q: "Getting there", a: "Faro Airport (FAO) has direct flights from most European cities and is expanding US connections. From Lisbon, it's a 3-hour drive on the A2 or a 3-hour train (€25–35). Rent a car at Faro Airport — the Algarve without a car means you're stuck in one resort town." },
      { q: "Getting around", a: "Car is essential for the western Algarve (Sagres, Lagos, the coastal cliff walks). The east (Tavira, Cacela Velha) is accessible by train from Faro. The main EN125 road runs the length of the coast but is slow in summer — use the A22 toll road if you're covering distance." },
      { q: "Where to base yourself", a: "Sagres for surf and dramatic cliffs. Tavira for the most authentic and beautiful town on the coast. Lagos for a good base with nightlife and beach access. Avoid the strip between Albufeira and Portimão unless package holidays are your thing." },
      { q: "How long", a: "Four to five days. The western coast (Sagres to Lagos) is a full two days. Tavira and the eastern Algarve are another two days. If you're combining with Alentejo or Lisbon, three focused days in the Algarve is enough." },
      { q: "Money", a: "More expensive than inland Portugal but still reasonable by European standards. Fish lunch with wine at a local restaurant: €20–30. Resorts and cliff-edge hotels: €200–500 in peak season, significantly less in shoulder season. Book accommodations 3–6 months out for July–August." },
    ],
  },
  {
    name: "Aveiro", country: "portugal", tag: "Canals · Tiles · Seafood",
    hook: "Portugal's Venice apology — and better than that description in every way.",
    img: "https://images.unsplash.com/photo-1528360983277-13d401cdc186?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=2; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=2; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=3; if(a[5]?.includes("cities")||a[5]?.includes("coast")) s+=2; if(a[6]?.includes("wander")||a[6]?.includes("eat")) s+=2; if(a[2]?.includes("short")) s+=2; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("sit")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("people")) s+=2; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")) s+=2; return s; },
    intro: "People call it the Venice of Portugal and then immediately apologize for the comparison — because Aveiro is better than that description. It's a small city built on a lagoon, with striped wooden boats (moliceiros) that were originally used to harvest seaweed now used to take tourists through painted canal streets. The real draw is the Art Nouveau architecture, the ovos moles (egg yolk sweets), and a food scene built around the Ria de Aveiro seafood that most visitors to Portugal never find.",
    highlights: [
      { label: "The moliceiro boats", text: "The painted wooden boats on the central canal. Take a 45-minute tour in the morning before the crowds. Each boat has its own hand-painted panels — the imagery is often surprisingly irreverent." },
      { label: "Costa Nova", text: "The striped wooden houses of Costa Nova are one of the most photographed streets in Portugal. Fifteen minutes from Aveiro by bus. The beach in front is one of the best on the Atlantic coast." },
      { label: "The fish market", text: "Mercado do Peixe opens at 7am. The seafood that goes through here — eels from the lagoon, razor clams, barnacles — is extraordinary and almost entirely consumed locally." },
      { label: "Art Nouveau architecture", text: "Aveiro has more Art Nouveau buildings per square meter than almost anywhere in Portugal. The train station's azulejo tile panels are among the best in the country." },
    ],
    eat: [
      { name: "Salpoente", desc: "The serious restaurant in Aveiro. A converted salt warehouse on the canal, tasting menu built around Ria seafood. One of the most interesting meals in central Portugal." },
      { name: "O Bairro", desc: "Wine bar and small plates in the old town. The best selection of natural Portuguese wine in Aveiro and staff who actually know what they're talking about." },
      { name: "Confeitaria Peixinho", desc: "The ovos moles come from here. The egg-yolk pastries are shaped like shells and fish and taste like nothing else. Buy a box and eat them on the canal." },
      { name: "Maré Alta", desc: "Fish restaurant right on the lagoon in São Jacinto, across the water from Aveiro. Accessible only by ferry. The caldeirada (fisherman's stew) is the one." },
    ],
    stay: [
      { name: "Aveiro Palace Hotel", tier: "Mid range", desc: "Central, well-run, good breakfast, canal views from the upper floors. The most reliable mid-range option in the city." },
      { name: "Moliceiro Hotel", tier: "Mid range", desc: "Boutique hotel right on the main canal. Small rooms, but the location and the breakfast terrace justify it completely." },
      { name: "Costa Nova Beach Houses", tier: "Good value", desc: "Rent one of the famous striped houses on Costa Nova for a night or two. A completely different experience than staying in the city. Book through local rental agencies." },,
      { name: "Moliceiro Boats (self-catering)", tier: "Good value", desc: "Several converted moliceiro boats moored on the canal system offer overnight accommodation. Sleeping on a traditional canal boat in Aveiro's waterways is unlike anything else in Portugal." },
    ],
    logistics: [
      { q: "When to go", a: "May–October. Aveiro is a year-round city but summer brings the best weather for Costa Nova beach. July–August is busy but nowhere near as crowded as Lisbon or the Algarve — the Portuguese come here on weekends but it doesn't feel overrun. Spring is excellent for the canals and markets." },
      { q: "Getting there", a: "Aveiro is on the main Lisbon–Porto rail line — 1 hour from Porto (€10–15), 2.5 hours from Lisbon (€20–30). Trains are frequent and reliable. If you're driving, it's just off the A1 motorway. There's no airport; fly into Porto or Lisbon." },
      { q: "Getting around", a: "Aveiro's center is compact and very walkable. The canal tours run from the main canal all day. For Costa Nova (15 min), take the local bus or an Uber. For the lagoon villages and São Jacinto, you need a car or boat. Cycling is excellent — the city has good bike lanes along the canal." },
      { q: "How long", a: "Two nights is ideal. One day for the city: canal tour, fish market, Art Nouveau architecture, ovos moles. Second day: Costa Nova beach in the morning, lagoon villages in the afternoon. Aveiro fits naturally into a Porto–Aveiro–Coimbra–Lisbon route along the coast." },
      { q: "Money", a: "One of the most affordable cities in Portugal. Lunch at a canal-side restaurant: €15–20. The Salpoente tasting menu (the serious restaurant) runs €80–100 per person and is worth every cent. Moliceiro boat tour: €15. Buy ovos moles to take home — €8–12 for a box." },
      { q: "Local tip", a: "Aveiro has a significant student population from the University of Aveiro, which keeps the restaurant and bar scene lively and affordable year-round. The area around the university is worth exploring for coffee shops and wine bars that aren't in any guidebook." },
    ],
  },
  {
    name: "Comporta", country: "portugal", tag: "Barefoot · Rice Fields · Atlantic",
    hook: "The Hamptons comparison is wrong. Comporta is better and you haven't heard of it yet.",
    img: "https://images.unsplash.com/photo-1566438480900-0609be27a4be?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")) s+=4; if(a[3]?.includes("luxury")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("wander")) s+=3; if(a[1]?.includes("partner")||a[1]?.includes("solo")) s+=2; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("sit")) s+=2; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=2; if(a[8]?.includes("quiet")||a[8]?.includes("freedom")) s+=3; if(a[9]?.includes("sit")||a[9]?.includes("walk")) s+=3; if(a[8]?.includes("people")||a[8]?.includes("article")) s+=2; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=3; return s; },
    intro: "Comporta is what happens when a stretch of Atlantic coastline stays undeveloped because it sits inside a protected natural reserve for long enough that it becomes the most desirable place in Portugal. Rice paddies, cork oaks, flamingos wading in the lagoon, and one of the most beautiful beaches in Europe — backed by nothing but pine trees. It's been called 'the Hamptons of Lisbon' by the people who ruined the Hamptons, but ignore that: Comporta is still genuinely extraordinary.",
    highlights: [
      { label: "Comporta beach", text: "Eighteen kilometers of completely undeveloped Atlantic beach. No beach bars, no parasols for rent, no development of any kind behind the dunes. Bring everything you need and stay all day." },
      { label: "The rice fields", text: "The flat landscape of flooded rice paddies between the beach and the village is unlike anywhere else in Portugal. Drive or cycle through at sunset when the light turns everything gold." },
      { label: "Carvalhal and Brejos da Carregueira", text: "The two villages that make up the Comporta area. Small, whitewashed, quiet. The kind of places that have one restaurant and one café and that's enough." },
      { label: "Flamingos", text: "The Sado Estuary, which borders Comporta, hosts one of the largest flamingo colonies in Europe. They're often visible from the road. Nobody mentions this and everyone is surprised by it." },
    ],
    eat: [
      { name: "Comporta Café", desc: "The gathering point of the village. Lunch under the trees, simple fish dishes, excellent wine list. The kind of table where nobody checks the time." },
      { name: "Casa da Cultura — O Galito", desc: "The local seafood restaurant that has been here longer than the designers and architects who now summer in Comporta. The best ameijoas (clams) in the region." },
      { name: "Sublime Comporta Restaurant", desc: "The hotel's restaurant is worth going even if you're not staying. The tasting menu changes with what came in that day. The terrace at sunset is extraordinary." },
      { name: "Cavalariça", desc: "Inside the Sublime hotel complex but more casual — wood-fired dishes, natural wine, the kind of dinner that goes until midnight without trying." },
    ],
    stay: [
      { name: "Sublime Comporta", tier: "High end", desc: "The benchmark hotel. Scattered villas through the cork oak forest, a pool that looks like it's part of the landscape, and a genuine commitment to doing nothing quickly. The most beautiful hotel in Portugal." },
      { name: "Ecork Hotel (Évora, nearby)", tier: "Mid range", desc: "Cork-clad eco-hotel in the Alentejo countryside near Évora, 45 minutes from Comporta. Good base for combining both areas." },
      { name: "Private Villa Rental", tier: "Good value", desc: "Renting a private house in Carvalhal or Comporta village is the way to actually live here for a week. Search through local agencies like Comporta Real Estate or Casa da Comporta." },,
      { name: "Sublime Comporta", tier: "High end", desc: "Forty cottages scattered through the pine forest, each with a private pool and terrace. The most serious hotel in Comporta — a spa, a beach club, two restaurants. The one that set the tone for the destination." },
    ],
    logistics: [
      { q: "When to go", a: "May–October. Comporta is best in the shoulder months — June and September are ideal. July–August the Lisbon crowd arrives in force and the vibe shifts. The flamingos in the estuary are present year-round but most visible in winter and early spring when the rice fields flood." },
      { q: "Getting there", a: "Comporta is 1.5 hours from Lisbon by car via the A2 and the Setúbal peninsula. There's no train and no easy public transport — you need a car. The drive itself is beautiful once you cross the Sado estuary ferry at Setúbal or go via the long route through Alcácer do Sal. Many Lisbon visitors drive down for a long weekend." },
      { q: "Getting around", a: "Comporta is tiny — the village, the beach, and the rice fields are all within cycling distance. Rent a bike at the village or from your accommodation. A car is useful for exploring further up the coast toward Carvalhal or across to Grandola and the Alentejo." },
      { q: "How long", a: "Two to three nights. One day: arrive, walk to the beach, eat at Comporta Café. Day two: cycling through the rice fields, sunset at the lagoon, dinner at Sublime. Day three: morning on the beach, slow departure. Comporta is deliberately unhurried — you'll feel it within a few hours." },
      { q: "Money", a: "Comporta is not cheap. The Sublime Comporta runs €400–900 a night. Private villa rentals are €250–600. Even the casual restaurants have caught up with the reputation. Budget €50–80 per person for dinner. That said, the beach is free, the flamingos are free, and the sunset over the rice fields costs nothing." },
      { q: "Who goes", a: "Comporta has become a destination for Lisbon's creative class, architects, and designers — along with European visitors looking for a quieter alternative to Ibiza or Mykonos. It's not exclusive, but it is intentional. People come to slow down. The vibe rewards that approach." },
    ],
  },
  {
    name: "Nazaré", country: "portugal", tag: "Waves · Cliffs · Fishing Village",
    hook: "A traditional fishing village that also hosts the biggest waves on earth. Both things are real.",
    img: "https://images.unsplash.com/photo-1580654843061-8c90a9e2b3a5?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("culture")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("coast")) s+=2; if(a[6]?.includes("wander")||a[6]?.includes("explore")) s+=2; if(a[2]?.includes("short")) s+=2; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=2; if(a[8]?.includes("quiet")||a[8]?.includes("freedom")) s+=3; if(a[9]?.includes("sit")||a[9]?.includes("walk")) s+=3; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("explore")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("none")) s+=2; if(a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=2; return s; },
    intro: "Nazaré has two identities that somehow coexist. It's a traditional Portuguese fishing village where the women still wear seven petticoats (one for each day of the week, supposedly) and dried fish hang outside every door — and it's also home to the biggest surfable waves on earth, which break at Praia do Norte every winter and have made it the place where world records are set. Both things are equally true and equally worth seeing.",
    highlights: [
      { label: "Praia do Norte and the big waves", text: "Between October and March, when the Atlantic swells run, the underwater canyon that amplifies Nazaré's waves produces 60-80 foot faces. You watch from the cliff. It's incomprehensible in person." },
      { label: "The Sítio", text: "The clifftop neighborhood above the beach, connected by a funicular. The viewpoint looks straight down onto the beach and town below. Better than any postcard view in Portugal." },
      { label: "The fishing beach", text: "The main beach at Nazaré is where the traditional fishing boats still come in. Go early morning and watch the catch being sorted and sold right there on the sand." },
      { label: "The dried fish", text: "Polvo seco (dried octopus) and various other dried fish hang on wooden racks outside houses throughout the old town. It's genuinely atmospheric and the octopus, when you eat it later, is extraordinary." },
    ],
    eat: [
      { name: "A Tasca da Lexi", desc: "The best seafood restaurant in Nazaré, run by a family who has fished these waters for generations. The grilled fish is whatever came in that morning. No menu in English, no apologies." },
      { name: "Restaurante Mar Bravo", desc: "On the clifftop in Sítio, looking out over the Atlantic. The caldeirada (fish stew) is the house specialty and worth the trip from Lisbon alone." },
      { name: "O Casalinho", desc: "Tiny, no reservations, closes when it runs out of food. The bacalhau à Brás (salt cod with eggs and potato) here is among the best versions in Portugal." },
      { name: "Nortada Bar", desc: "The surf bar near Praia do Norte. Open October through March during the big wave season. The clientele is international surfers and the people who come to watch them. Cold beer and good views." },
    ],
    stay: [
      { name: "Hotel Miramar Sul", tier: "Mid range", desc: "On the clifftop in Sítio with views over the main beach. Well-run, honest prices, good breakfast with local pastries." },
      { name: "Magic Nazaré Hostel", tier: "Good value", desc: "The gathering point for the international surf community during big wave season. Clean, social, incredibly well-located near Praia do Norte." },
      { name: "Nazaré Old Town Apartments", tier: "Good value", desc: "Stay in the old fishing neighborhood above the beach. Walk to the viewpoint, the fish market, everything. Look for apartments in the Pederneira area." },,
      { name: "Villa Nazaré", tier: "Good value", desc: "A family-run guesthouse in the upper town (Sítio) with a terrace looking directly down the cliff to the beach and the Atlantic. Breakfast included, parking, the best view in Nazaré for the price." },
    ],
    logistics: [
      { q: "When to go", a: "Two completely different seasons. For the big waves: October through March, when the Atlantic swells activate the underwater canyon and Praia do Norte produces 60–80 foot faces. For beach and village life: May through September, when the fishing community is active, the beach is swimmable, and the dried fish racks are full. Both are worth it for entirely different reasons." },
      { q: "Getting there", a: "Nazaré is 1.5 hours from Lisbon by car (A8 motorway, then N242). There's also a bus from Lisbon's Sete Rios terminal (2 hours, €12). No train. The closest train station is in Valado dos Frades, 6km away — take a taxi from there. Most people drive." },
      { q: "Getting around", a: "Nazaré is small enough to walk entirely. The funicular (ascensor) connects the beach neighborhood (Praia) to the clifftop neighborhood (Sítio) — €1.20 each way and worth the experience. For Praia do Norte and the big wave viewpoint, it's a 20-minute walk from the main beach or a short Uber." },
      { q: "How long", a: "Two nights is perfect. Day one: arrive via the cliff road, walk the fishing beach, take the funicular up to Sítio for sunset. Day two: early morning at Praia do Norte (waves permitting), dried fish market, lunch at a tasca. Nazaré pairs naturally with Óbidos (30 minutes south) and Alcobaça (15 minutes inland, one of Portugal's great Gothic monasteries)." },
      { q: "Big wave season tips", a: "Swell forecasts for Nazaré are tracked on Surfline and MagicSeaweed. The best viewpoint for big wave days is the Fort of São Miguel Arcanjo at the end of the cliff above Praia do Norte — arrive early, the crowd grows fast. The waves are not swimmable; you watch from above." },
      { q: "Money", a: "Nazaré is one of the most affordable coastal towns in Portugal. A fish lunch at a local tasca: €15–20. Even the clifftop hotels with views are reasonably priced (€80–150 in peak season). The dried octopus and fish make excellent gifts — buy from the racks in the old town, not the tourist shops." },
    ],
  },
];

// ─── ITALY REGIONS (each carries its own eat + stay data) ─────────────────────
const italyRegions = [
  {
    name: "Puglia", country: "italy", tag: "Coast · Trulli · Olive Groves",
    hook: "The Instagram images undersell it. That's not something you can usually say.",
    img: "https://images.unsplash.com/photo-1633321088355-2f9e8c517be4?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("eat")||a[6]?.includes("explore")) s+=2; if(a[2]?.includes("week")||a[2]?.includes("twoweeks")) s+=1; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("explore")) s+=2; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("connection")) s+=2; if(a[9]?.includes("eat")||a[9]?.includes("explore")) s+=2; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=2; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")) s+=2; return s; },
    intro: "The heel of Italy's boot is one of the great undiscovered corners of Europe — and the Instagram images you've been saving actually undersell it. Whitewashed hilltop towns, trulli (those conical stone houses that look like they were built by Hobbits), olive trees that are 2,000 years old, and an Adriatic coastline that makes the Amalfi Coast look crowded.",
    highlights: [
      { label: "Alberobello", text: "Yes, it's the trulli town everyone photographs. Go early morning before the tour buses. The Valle d'Itria around it — Locorotondo, Cisternino, Martina Franca — is where you actually want to stay." },
      { label: "Ostuni", text: "The white city. Perched on a hill, all whitewashed walls and steep staircases. Genuinely beautiful at night when the crowds thin out." },
      { label: "Lecce", text: "Called the 'Florence of the South.' Baroque architecture so ornate it looks like it was carved from butter. Better food than Florence. A quarter the tourists." },
      { label: "Polignano a Mare", text: "The town built on cliff edges over the sea. You've seen the photos. It's better in person. Stay at one of the cave hotels." },
    ],
    eat: [
      { name: "Casa Bruta (Polignano a Mare)", desc: "Cave restaurant built into the cliff. The raw seafood is extraordinary — ricci di mare (sea urchin) straight from the Adriatic. Book well in advance." },
      { name: "Il Frantoio (Fasano)", desc: "Dinner on a working olive farm. One long table, one menu, whatever was made that day. One of the great meal experiences in Italy." },
      { name: "Già Sotto l'Arco (Carovigno)", desc: "The most serious restaurant in Puglia. Teresa Buongiorno's cooking is the best argument for why this region matters. Book months out." },
      { name: "Pescaria (Polignano)", desc: "Fish street food. The raw seafood sandwich on a brioche bun is what everyone photographs on Instagram. Eat it standing up at the counter." },
      { name: "Osteria del Tempo Perso (Ostuni)", desc: "Stone vaulted ceilings, local wine, orecchiette with whatever ragù they made that morning. Exactly what Puglia should taste like." },
    ],
    stay: [
      { name: "Borgo Egnazia", tier: "High end", desc: "Masseria resort built like a medieval village near Fasano. Enormous pool, incredible food, genuinely beautiful. Where international celebrities go." },
      { name: "Masseria Torre Coccaro", tier: "Mid range", desc: "Converted farmhouse near Fasano with an underground spa carved from the rock. The most characterful mid-range option in the south." },
      { name: "Trullo Rental (Valle d'Itria)", tier: "Good value", desc: "Sleeping in a 400-year-old conical stone house with a private pool for €100 a night. Book through Airbnb. Non-negotiable." },,
      { name: "Masseria Torre Coccaro (Fasano)", tier: "High end", desc: "A 16th-century watchtower converted into a luxury masseria. The olive grove is 2,000 years old. Private beach, spa in the original caves, cooking classes in the farmhouse kitchen." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October are ideal — warm enough for the coast, not brutally hot. July–August the heat in inland Puglia hits 38–42°C. September is the best month: olive harvest begins, the sea is still warm, crowds thin significantly after August 15th (Ferragosto)." },
      { q: "Getting there", a: "Fly into Bari (BRI) or Brindisi (BDS) — both have good European connections. Bari is better for Polignano, Alberobello, and the Valle d'Itria. Brindisi is better for Lecce and the Salento. Rent a car at the airport — Puglia without a car is a frustrating experience." },
      { q: "Getting around", a: "Car is essential. The distances between Puglia's highlights aren't large but they're all spread across a wide flat landscape. The Valle d'Itria (Alberobello, Locorotondo, Cisternino) is a 30-minute loop. Lecce to Polignano is 1.5 hours. Fasano and the masseria belt is central to everything." },
      { q: "How long", a: "Five to seven days to do it properly. Base yourself in the Valle d'Itria for the trulli experience, Ostuni for coast access, or Lecce for the city. A week gives you: Alberobello and the valley, Polignano a Mare, Ostuni, Lecce and the Salento coast, and at least one long masseria lunch." },
      { q: "Money", a: "Puglia is one of the best value regions in Italy. A serious lunch with wine at a masseria: €25–40. Trullo rental with pool: €100–200 a night. The luxury masserias (Borgo Egnazia) run €500–900 but are genuinely extraordinary. Street food in Polignano (the arancini, the raw seafood sandwich) is €5–10." },
      { q: "Food notes", a: "Orecchiette (ear-shaped pasta) with cime di rapa (turnip tops) or ragù is the regional dish — you'll eat it everywhere and it should never get old. Burrata was invented here. The olive oil is some of the best in the world. Ask for local wine (Primitivo, Negroamaro) rather than anything from a list." },
    ],
  },
  {
    name: "Sicily", country: "italy", tag: "History · Food · Coastline",
    hook: "Every civilization that ever mattered colonized this island. All of them left something.",
    img: "https://images.unsplash.com/photo-1523906834658-6e24ef2386f9?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("coast")||a[5]?.includes("cities")) s+=2; if(a[6]?.includes("wander")||a[6]?.includes("eat")) s+=2; if(a[2]?.includes("week")||a[2]?.includes("twoweeks")) s+=2; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("eat")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("none")||a[8]?.includes("feel")) s+=2; if(a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=1; return s; },
    intro: "Sicily is its own country inside Italy. It's been colonized by almost every great civilization that ever existed — Greeks, Arabs, Normans, Spanish — and all of them left something behind. The food alone is worth the trip: arancini, pasta alla Norma, cannoli eaten in the town where they were invented, granita for breakfast because this is Sicily and that's what you do.",
    highlights: [
      { label: "Palermo", text: "Chaotic, beautiful, and completely alive. The street food markets — Ballarò, Vucciria — are the best in Italy. Go with no plan and follow the noise." },
      { label: "Valley of the Temples (Agrigento)", text: "Greek temples in better condition than anything in Greece, standing in a field of almond trees. One of the great ancient sites in the world." },
      { label: "Taormina", text: "The postcard town with Etna in the background. The Greek theater with that view is genuinely unforgettable. Stay outside town to avoid peak-season prices." },
      { label: "Ragusa Ibla", text: "A Baroque hillside city in the south of the island. Almost nobody goes. Quiet streets, serious restaurants, the kind of place you tell everyone about when you get home." },
    ],
    eat: [
      { name: "Osteria dei Vespri (Palermo)", desc: "Inside a historic palazzo in Piazza Croce dei Vespri. The best tasting menu in Palermo. Sophisticated, local, serious wine list." },
      { name: "Trattoria Ai Cascinari (Palermo)", desc: "Where Palermitans eat when they want to eat well. No tourists, no English menu, no apologies. The pasta con le sarde is the reason you came." },
      { name: "Ballarò Market (Palermo)", desc: "Not a restaurant — the oldest street market in the city. Arancini, panelle, sfincione (Sicilian pizza). Breakfast and lunch, standing up, every day." },
      { name: "Ristorante La Pergola (Taormina)", desc: "Family-run terrace restaurant in Taormina with the best arancini and pasta alla Norma you'll find. No Michelin star, better than restaurants that have them." },
      { name: "Pasticceria Cappello (Palermo)", desc: "The cannoli are made fresh every hour. The granita is the best in the city. Go at 8am and call it breakfast." },
    ],
    stay: [
      { name: "Rocco Forte Verdura Resort", tier: "High end", desc: "Clifftop resort on the south coast between Agrigento and Palermo. Three pools, a spa, golf, and the best seafood restaurant on the island." },
      { name: "Hotel Gutkowski (Syracuse)", tier: "Mid range", desc: "Small design hotel on the waterfront in Ortigia, the ancient island center of Syracuse. Blue and white, beautiful, excellent breakfast." },
      { name: "B&Bs in Palermo's Kalsa", tier: "Good value", desc: "The historic Arab-Norman neighborhood. Cheap, atmospheric, walking distance to everything. Search Booking.com for the word 'palazzo' and filter by Old Town." },,
      { name: "Zash Country Boutique Hotel (Riposto)", tier: "Mid range", desc: "A citrus farmhouse on the slopes of Etna converted into a design hotel. Lava stone walls, an infinity pool with sea views, a Michelin-starred restaurant using the farm's produce." },
    ],
    logistics: [
      { q: "When to go", a: "March–May and September–November. The island is spectacular in spring when the almond trees bloom and the landscape is green. Summer (July–August) is brutally hot at 38–42°C inland but the coast is magnificent and the sea is perfect. Avoid major sites like the Valley of the Temples in July midday — go at 7am." },
      { q: "Getting there", a: "Fly into Palermo (PMO) for the west and interior, or Catania (CTA) for the east (Etna, Taormina, Syracuse). Both have good European connections. The ferry from Naples or Reggio Calabria is a great option if you're doing a southern Italy road trip — it's overnight and you wake up in Sicily." },
      { q: "Getting around", a: "Rent a car — Sicily is large and the highlights are spread across the island. The autostrada system is good between major cities. The coastal roads (especially the SS115 along the south coast) are slow but extraordinary. Palermo has decent local transport, but everywhere else requires wheels. Park outside historic centers and walk in." },
      { q: "How long", a: "One week minimum to scratch the surface. Week one: Palermo (2 nights) → Agrigento and the Valley of the Temples → Ragusa Ibla (2 nights) → Syracuse and Ortigia (2 nights). Two weeks adds Taormina, Etna, and the Aeolian Islands by ferry. Sicily resists being rushed." },
      { q: "Money", a: "One of the best value destinations in Italy. Street food in Palermo (arancini, panelle, cannoli) costs €2–5. A serious sit-down dinner with wine: €30–50 per person. Luxury resorts (Verdura) run €400–800. B&Bs and small hotels in Palermo and Syracuse: €80–150. The Aeolian Islands cost significantly more in summer." },
      { q: "Food rules", a: "Granita for breakfast is not optional — it's the local breakfast. Order it with a brioche and eat it at the bar standing up like everyone else. Arancini should be eaten immediately, hot. Cannoli should be filled to order; pre-filled ones are for tourists. The street markets in Palermo (Ballarò, Vucciria) are where you eat lunch." },
    ],
  },
  {
    name: "The Dolomites", country: "italy", tag: "Mountains · Hiking · Altitude",
    hook: "They look like they were designed by someone who had never seen mountains. They weren't.",
    img: "https://images.unsplash.com/photo-1551632811-561732d1e306?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("luxury")) s+=2; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("mountains")) s+=5; if(a[5]?.includes("coast")) s-=1; if(a[6]?.includes("explore")) s+=3; if(a[1]?.includes("partner")||a[1]?.includes("friends")) s+=1; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("beauty")||a[8]?.includes("freedom")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("walk")) s+=3; if(a[8]?.includes("deep")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("crowds")||a[9]?.includes("rushed")) s+=2; if(a[6]?.includes("physical")||a[6]?.includes("fullday")) s+=2; return s; },
    intro: "The Dolomites look like they were designed by someone who had never seen mountains and was working purely from imagination. Vertical pale rock faces, meadows that are genuinely green, mountain huts (rifugi) serving wine and pasta at 2,500 meters. It's the most dramatic landscape in Europe that isn't being talked about enough.",
    highlights: [
      { label: "Cortina d'Ampezzo", text: "The base camp for serious Dolomite exploration. Also happens to be Italy's most glamorous ski resort — the combination of proper wilderness and good restaurants is unusual." },
      { label: "Alta Via 1", text: "The classic Dolomite long-distance hiking route. Two weeks end-to-end, or pick a three-day section. Hut-to-hut with beds and meals included." },
      { label: "Tre Cime di Lavaredo", text: "Three vertical towers of rock that have been painted, photographed, and climbed for a century. The easy circular hike takes three hours. Go at sunrise." },
      { label: "Val Gardena", text: "A valley with a distinct culture — technically Italy but the locals speak Ladin, a Latin dialect surviving since Roman times. Beautiful without being overrun." },
    ],
    eat: [
      { name: "St. Hubertus (San Cassiano)", desc: "Three Michelin stars inside a mountain hotel. Norbert Niederkofler's cooking is built entirely around the alpine landscape — no imported ingredients, everything from the valley or above it. One of the great restaurants in Italy." },
      { name: "Rifugio Scotoni (Alta Badia)", desc: "Mountain hut at 1,985 meters. Order the canederli (bread dumplings in broth) and a glass of local wine and eat on the terrace looking at the Dolomites. This is why you came." },
      { name: "La Perla Restaurant (Corvara)", desc: "The restaurant inside La Perla hotel. South Tyrolean cuisine at its most refined — venison, speck, polenta, local cheese. The wine cellar has 60,000 bottles." },
      { name: "Rifugio Auronzo (Tre Cime)", desc: "The hut at the top of the road to Tre Cime. Arrive at 6am, eat breakfast with your back to the valley and the three peaks in front of you. Worth every euro of the €30 cable car." },
    ],
    stay: [
      { name: "Rosa Alpina (San Cassiano)", tier: "High end", desc: "The benchmark Dolomite hotel. Family-run, three Michelin stars in the restaurant, ski-in ski-out in winter, hiking from the door in summer." },
      { name: "La Perla (Corvara)", tier: "High end", desc: "Another great family hotel, slightly less famous than Rosa Alpina, slightly better value. The pool is extraordinary." },
      { name: "Hotel Garnì Venezia (Corvara)", tier: "Mid range", desc: "Small family-run hotel in Alta Badia. Proper mountain breakfast, ski-in/out in winter, hiking from the door in summer. Half the price of the luxury options." },,
      { name: "Rifugio huts (hiking season)", tier: "Good value", desc: "The mountain hut network across the Dolomites — simple dormitory rooms, hot meals, extraordinary locations on ridges and at high passes. The Via Ferrata experience requires staying in rifugi. Book through the SAT or CAI websites." },
    ],
    logistics: [
      { q: "When to go", a: "Two distinct seasons. Summer (late June–September): wildflower meadows, clear skies, hiking from hut to hut, rifugi open and serving food. Winter (December–March): world-class skiing on the Sella Ronda circuit, the most beautiful ski landscape in Europe. Avoid October–November and April–May when many rifugi and hotels close between seasons." },
      { q: "Getting there", a: "Fly into Venice (VCE) or Innsbruck (INN) and rent a car — there's no good way to get here without one. Venice to Cortina is 2.5 hours. Innsbruck to Alta Badia is 1.5 hours. The drive up into the mountains is part of the experience. Book rental cars well in advance in peak season." },
      { q: "Getting around", a: "Car for getting between valleys and villages. Gondolas and lifts for getting up the mountains (summer hiking passes available, ~€30/day). In winter, ski in/out at the luxury hotels and use the ski bus between resorts. The Sella Ronda ski circuit connects four valleys by lift — you can ski the whole circuit in a day." },
      { q: "How long", a: "Four to five days for hiking, three to four days for skiing. The Dolomites reward slow exploration — one valley per day, one rifugio lunch per day. Alta Badia, Cortina, and Val Gardena are the three main bases. Combining two in one trip gives you a complete picture." },
      { q: "Money", a: "The Dolomites are not cheap. Luxury hotels (Rosa Alpina, La Perla) run €400–900 per night. Mid-range family hotels: €150–300. Rifugio lunch (pasta, wine, view): €25–40. Lift passes in winter: €60–70 per day. Summer hiking passes: €25–35. The food and wine at St. Hubertus (three Michelin stars) runs €200–250 for the tasting menu." },
      { q: "Cultural note", a: "The Dolomites are in South Tyrol — technically Italy but historically Austrian. Many locals speak German as a first language and Ladin as a second. Italian is the third language. The food reflects this: speck, canederli, strudel, and venison alongside Italian pasta. Menus are often in all three languages." },
    ],
  },
  {
    name: "Lake Como & the Lakes", country: "italy", tag: "Water · Villas · Elegance",
    hook: "European aristocracy has been coming here for three centuries. The light still hasn't changed.",
    img: "https://images.unsplash.com/photo-1518548419970-58e3b4079ab2?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("culture")) s+=2; if(a[3]?.includes("luxury")||a[3]?.includes("balanced")) s+=3; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("coast")||a[5]?.includes("mountains")) s+=2; if(a[6]?.includes("wander")||a[6]?.includes("absorb")) s+=2; if(a[1]?.includes("partner")) s+=3; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=2; if(a[8]?.includes("beauty")||a[8]?.includes("quiet")) s+=2; if(a[9]?.includes("sit")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("crowds")||a[9]?.includes("badsleep")) s+=1; return s; },
    intro: "Lake Como has been the summer escape of European aristocracy for three centuries. The villas are still there, the light on the water hasn't changed, and if you base yourself in one of the smaller towns instead of Como or Bellagio, it's still surprisingly manageable. Lake Maggiore to the west is more Italian, less photographed, and worth combining.",
    highlights: [
      { label: "Varenna", text: "The best town on the lake. Ferry access only to most of it, cobblestone paths, a small harbor, two excellent restaurants. Book a room with a lake view and don't leave for two days." },
      { label: "Villa del Balbianello", text: "The most famous villa on the lake — Star Wars and Casino Royale were filmed here. Book the garden tour and take the ferry from Lenno." },
      { label: "Bellagio", text: "Yes, it's busy. But the old town above the waterfront, early morning, is genuinely special. Worth an afternoon." },
      { label: "Isole Borromee (Lake Maggiore)", text: "Three private islands in the middle of Lake Maggiore, each with baroque palaces and extravagant gardens. Take the ferry from Stresa." },
    ],
    eat: [
      { name: "Ristorante Il Cavatappi (Varenna)", desc: "The best restaurant in Varenna on a terrace above the lake. The risotto with lake perch is the dish. Book ahead — it's small and everyone knows about it." },
      { name: "Trattoria Baita Belvedere (Griante)", desc: "Above Cadenabbia, off every list, local clientele only. The pasta is made that morning, the wine is from the hillside behind the building." },
      { name: "Locanda dell'Isola Comacina (Isola Comacina)", desc: "On a tiny island in the lake only accessible by boat. The menu hasn't changed since 1947 — one fixed meal for everyone. Book well in advance, the whole experience is the point." },
      { name: "Barchetta (Bellagio)", desc: "On the waterfront in Bellagio, tables outside, lake trout and local wines. Go for lunch when the day trippers haven't yet arrived." },
    ],
    stay: [
      { name: "Grand Hotel Tremezzo", tier: "High end", desc: "Belle Époque palace on the lake with a floating pool in the water. The most beautiful hotel on Lake Como and one of the most beautiful in Europe." },
      { name: "Hotel du Lac (Varenna)", tier: "Mid range", desc: "Small hotel right on the water in Varenna. Simple rooms, spectacular views, excellent breakfast. The best value on the lake." },
      { name: "Villa rental in Lenno or Tremezzo", tier: "Good value", desc: "Rent a villa on the lake for a week and cook with ingredients from the local market. An entirely different experience than any hotel. Search Airbnb filtered by 'lake view'." },,
      { name: "Villa Cipressi (Varenna)", tier: "Mid range", desc: "A 15th-century villa with terraced gardens dropping to the lake in the quieter village of Varenna. The alternative to the Bellagio crowds — same views, significantly more peace, better value." },
    ],
    logistics: [
      { q: "When to go", a: "April–June and September–October. The lake is beautiful year-round, but spring brings camellias and azaleas blooming across the villa gardens. July–August is peak season — Bellagio is wall-to-wall tourists and boat traffic is constant. November–March is quiet and atmospheric but many restaurants and smaller hotels close." },
      { q: "Getting there", a: "Milan Malpensa (MXP) is the closest major airport — 1.5 hours to the lake by car or bus. Milan Centrale train station connects to Como and Varenna. For Varenna specifically, take the train from Milan Centrale to Varenna-Esino (1.5 hours, €10) — it runs along the east shore of the lake and the journey is beautiful." },
      { q: "Getting around", a: "The ferry system on Lake Como is excellent and connects all the main towns. Buy a day pass (€15–20) and hop between Varenna, Bellagio, Tremezzo, and Menaggio. For the western shore and Villa Balbianello, take the boat from Lenno. Renting a car is useful for exploring the valleys behind the lake but not necessary for the lake itself." },
      { q: "How long", a: "Three to four nights. Base yourself in Varenna (quieter, more authentic) rather than Bellagio or Como itself. Day one: arrive and settle. Day two: Villa del Balbianello and the western shore by ferry. Day three: Monte Crocione hike above the lake (views are extraordinary). Day four: slow morning, departure." },
      { q: "Money", a: "Lake Como is not cheap. The Grand Hotel Tremezzo runs €500–1,200. Mid-range lakefront hotels: €200–400. Dinner with lake view: €50–80 per person. The ferry day pass (€15–20) is the best value on the lake. Driving on the lake road (SS340) is free but narrow — allow twice as long as Google Maps suggests." },
      { q: "Varenna vs. Bellagio", a: "Bellagio is the famous one — more restaurants, more ferries, more everything. Varenna is smaller, quieter, and significantly more beautiful for staying overnight. The views from Varenna looking across to the mountains are the defining image of Lake Como. Take the ferry to Bellagio for an afternoon and come back to Varenna to sleep." },
    ],
  },
  {
    name: "Tuscany — Off the Trail", country: "italy", tag: "Wine · Countryside · Medieval Towns",
    hook: "Everyone does the Chianti road. The Tuscany worth finding is in the corners.",
    img: "https://images.unsplash.com/photo-1534281939400-b00bdb5b3218?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("culture")) s+=2; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("eat")||a[6]?.includes("explore")) s+=2; if(a[2]?.includes("week")||a[2]?.includes("twoweeks")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=2; if(a[8]?.includes("quiet")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("eat")) s+=2; if(a[8]?.includes("deep")||a[8]?.includes("people")) s+=1; if(a[9]?.includes("rushed")||a[9]?.includes("generic")) s+=2; return s; },
    intro: "Everybody does the Chianti road between Florence and Siena. The Tuscany worth finding is in the corners — the Maremma coast where there are almost no tourists, the Val d'Orcia which looks exactly like a Renaissance painting, the wine towns of Montalcino and Montepulciano which are far better than the Chianti strip and see a fraction of the traffic.",
    highlights: [
      { label: "Val d'Orcia", text: "UNESCO-listed landscape of rolling hills, cypress tree lines, and medieval towers. Pienza is the perfect town — built by a pope in the 15th century as the ideal Renaissance city. The pecorino cheese is the best in Italy." },
      { label: "Montalcino", text: "Home of Brunello di Montalcino — one of Italy's greatest wines. The town is a small fortress on a hill with some of the best enotecas in the country. Go in November during harvest." },
      { label: "The Maremma coast", text: "Southern Tuscany's coast is almost entirely undeveloped. Argentario, Talamone, Capalbio — all beautiful, all accessible by car, almost none of it in any guidebook." },
      { label: "San Gimignano at dawn", text: "Famous for its medieval towers and extremely crowded. Arrive before 8am or stay overnight and you'll have the streets to yourself." },
    ],
    eat: [
      { name: "Osteria del Cinghiale Bianco (Florence)", desc: "Old stone walls, paper tablecloths, wild boar pappardelle that's been on the menu for decades because it's perfect. The version of Florence that still exists if you know where to find it." },
      { name: "La Buca delle Fate (Colle di Val d'Elsa)", desc: "Off every tourist list, twenty minutes from Siena. Local farmers eat here. The bistecca is Chianina beef from a farm you can see from the window." },
      { name: "Enoteca La Torre (Montalcino)", desc: "Wine bar in the fortress. Brunello by the glass, local charcuterie, view over the valley. The right way to spend an afternoon in Montalcino." },
      { name: "Trattoria Latte di Luna (Pienza)", desc: "The spot in Pienza. Handmade pasta, local Cinta Senese pork, Pienza pecorino on everything. The terrace looks out over the Val d'Orcia." },
      { name: "Il Tufo Allegro (Pitigliano)", desc: "In one of Tuscany's most dramatic hidden towns — a city built entirely on a tufa rock outcrop. The Jewish-Tuscan menu is one of a kind." },
    ],
    stay: [
      { name: "Castiglion del Bosco", tier: "High end", desc: "A 5,000-acre private estate in Montalcino with its own Brunello wine label. Villas, a golf course, cooking classes, and Brunello in the minibar." },
      { name: "Adler Thermae (Bagno Vignoni)", tier: "High end", desc: "Thermal spa hotel in one of the most beautiful villages in Val d'Orcia. Natural thermal pools, complete silence, extraordinary landscape." },
      { name: "Agriturismo in Val d'Orcia", tier: "Good value", desc: "Farm stays with home-cooked dinner included. Arrive at 7pm, sit outside with wine, eat whatever was made that day. Search TripAdvisor for 'agriturismo Val d\'Orcia'." },,
      { name: "Podere Il Casale (Pienza)", tier: "Good value", desc: "An organic farm near Pienza that makes its own cheese, salami, and wine and rents four stone farmhouses. The weekly communal dinner around a long table with other guests is the point." },
    ],
    logistics: [
      { q: "When to go", a: "April–May and September–October. Spring brings poppies in the Val d'Orcia and the countryside is at its most photogenic. Harvest (September–October) fills the wine towns with activity and the olive groves come alive in November. July–August is extremely hot and the Chianti road becomes a traffic jam of wine tourists." },
      { q: "Getting there", a: "Florence (FLR or the main train hub) is the gateway for northern Tuscany. Rome (FCO) is the gateway for the south — the Val d'Orcia is 2 hours from Rome by car. You need a car for all of rural Tuscany. Rent in Florence or Rome before heading into the countryside. The train gets you to Siena and Grosseto but nowhere useful after that." },
      { q: "Getting around", a: "Car is essential. The SR2 from Siena to Montalcino and the SP146 across the Val d'Orcia are among the most beautiful drives in Italy. ZTL (restricted traffic) zones apply in historic town centers — park at the marked lots outside the walls and walk in. GPS is unreliable on some back roads; download offline maps." },
      { q: "How long", a: "Four to five days for a proper Tuscan countryside trip. Base yourself in Montalcino for the south (Val d'Orcia, Pienza, Bagno Vignoni) or near Pienza for a more central position. A week allows you to add the Maremma coast and Pitigliano in the far south — one of the most underrated corners of Italy." },
      { q: "Money", a: "A range. The luxury estates (Castiglion del Bosco, Adler Thermae) run €400–900. Agriturismi with dinner included: €100–200. A Brunello di Montalcino at the winery: €25–60 per bottle — a fraction of what you'd pay at home. Lunch at a Val d'Orcia trattoria: €25–40 with local wine." },
      { q: "Wine notes", a: "Brunello di Montalcino is the prestige wine — complex, age-worthy, expensive. The Rosso di Montalcino is the same grape, younger, and half the price — drink it with lunch. Vino Nobile di Montepulciano is excellent and undervalued. Ask any restaurant for their house wine (vino della casa) first — in Tuscany it's often remarkable." },
    ],
  },
  {
    name: "Rome", country: "italy", tag: "Gateway · Ancient · Neighborhoods",
    hook: "Most people do Rome wrong. Budget two days and go beyond the Colosseum.",
    img: "https://images.unsplash.com/photo-1552832230-c0197dd311b5?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=3; if(a[3]?.includes("balanced")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("safe")) s+=2; if(a[5]?.includes("cities")) s+=3; if(a[6]?.includes("absorb")||a[6]?.includes("wander")) s+=2; if(a[2]?.includes("short")||a[2]?.includes("week")) s+=1; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=1; if(a[9]?.includes("walk")||a[9]?.includes("plan")) s+=2; if(a[8]?.includes("deep")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("tourist")) s-=1; return s; },
    intro: "Rome is where most people fly into Italy and where most people stay too long doing the wrong things. The Colosseum and Vatican are real and worth seeing — but the Rome that changes you is in the neighborhoods: Trastevere at midnight, a wine bar in Pigneto, a Sunday morning market in Porta Portese, an aperitivo in the Campo de' Fiori before the tourists take over. Budget two days before you go south or north. You'll want three.",
    highlights: [
      { label: "Trastevere", text: "The neighborhood that looks like a movie set but isn't. Cobblestones, ivy-covered walls, restaurants without signs. Go after 9pm when the day-trippers leave and it becomes Roman again." },
      { label: "Pigneto and Ostiense", text: "The neighborhoods Rome doesn't include in the brochure. Street art, natural wine bars, the kind of restaurants that are genuinely good because they haven't been reviewed yet. Twenty minutes by tram from the center." },
      { label: "The Pantheon at 7am", text: "Free, open, and almost empty if you arrive right when the doors open. Stand in the center, look up at the oculus. This is what staying in Rome instead of rushing through it earns you." },
      { label: "Borghese Gallery", text: "Bernini's sculptures are in here. Book well in advance — timed entry, two hours maximum, and you will not want to leave. One of the great art experiences in the world." },
    ],
    eat: [
      { name: "Roscioli", desc: "Deli, restaurant, and wine bar in one building near Campo de' Fiori. The carbonara is what people fly to Rome for. Book weeks ahead or arrive at noon and wait." },
      { name: "Osteria dell'Angelo", desc: "Roman neighborhood restaurant in Prati, near the Vatican. Cucina romana at its most honest — cacio e pepe, coda alla vaccinara (oxtail), artichokes. Cash only, no tourists, book by phone." },
      { name: "Supplì Roma", desc: "The best suppli (fried rice balls) in Rome. Two locations, long queue, eat them standing on the street while they're still hot. This is breakfast." },
      { name: "Il Sorpasso", desc: "Aperitivo bar in Prati that's been doing it right before aperitivo bars were everywhere. Great natural wine list, excellent cicchetti, the right place to start a Roman evening." },
      { name: "Fatamorgana", desc: "The best gelato in Rome — all unusual flavors (gorgonzola and walnut, basil and walnuts, rose and cardamom). Multiple locations. Mandatory." },
    ],
    stay: [
      { name: "Hotel de Russie", tier: "High end", desc: "The classic Rome stay for people who know Rome. Garden terrace, beautiful rooms, right between the Spanish Steps and the Tiber. Worth every euro if budget allows." },
      { name: "G-Rough", tier: "Mid range", desc: "Design hotel in a palazzo near the Pantheon. Antiques mixed with modern art, genuinely interesting interiors, small but the location is unbeatable." },
      { name: "Trastevere Apartments", tier: "Good value", desc: "Staying in Trastevere in an apartment is the Rome experience. Walk to everything, have a coffee at the same bar every morning, do the neighborhood market on Sunday. Airbnb the word 'Trastevere'." },,
      { name: "Palazzo Manfredi", tier: "High end", desc: "Six rooms above the Colosseum — the only hotel in Rome with a direct view of the arena from the rooftop terrace. Breakfast with the gladiators' amphitheatre below. Extraordinary and expensive." },,
      { name: "Fortyseven Hotel", tier: "Mid range", desc: "A boutique hotel on Via Petroselli overlooking the Circus Maximus and the Aventine Hill. Rooftop terrace with one of the best views in Rome — the ancient chariot track below, the Palatine Hill beyond. Quieter than the centro storico hotels and significantly more character." },
    ],
    logistics: [
      { q: "When to go", a: "April–May and October–November. Spring in Rome is extraordinary — warm, manageable crowds, the city at its most beautiful light. July–August is brutally hot (35–40°C) and the tourist density at the Colosseum and Vatican becomes genuinely oppressive. October is the local's favorite month — still warm, the crowds are gone, the light turns gold." },
      { q: "Getting there", a: "Rome Fiumicino (FCO) is the main international hub with direct US connections on most major carriers. The Leonardo Express train runs from FCO to Roma Termini in 32 minutes (€14). Avoid the expensive private taxis from the airport — the train is faster." },
      { q: "Getting around", a: "Rome is best explored on foot. The historic center is compact and walkable. Metro lines A and B cover the main tourist areas. Trams connect Trastevere to the center and east neighborhoods. Uber works well and is often faster than a taxi. Never drive in Rome's historic center — ZTL restrictions and impossible parking will ruin your day." },
      { q: "How long", a: "Three nights minimum. Day one: Colosseum, Roman Forum, Palatine Hill (book ahead). Day two: Vatican Museums and Sistine Chapel (book weeks ahead), Trastevere at night. Day three: Pantheon at 7am, Borghese Gallery (book ahead), aperitivo in Pigneto. If you're using Rome as a gateway to southern Italy, two nights is workable but you'll feel the rush." },
      { q: "Booking ahead", a: "Roscioli (the carbonara restaurant): book 3–4 weeks ahead. Borghese Gallery: book 2–3 weeks ahead, timed entry only. Vatican Museums: book 1–2 months ahead for July–August. Colosseum: book online same week. If you arrive without reservations at peak season, plan to eat standing up or at less famous restaurants — which are often better anyway." },
      { q: "Money", a: "Rome is mid-range by European capital standards. Espresso at the bar: €1.50. Suppli (fried rice ball) at Supplì Roma: €2.50. A serious trattoria dinner: €35–60 per person. Gelato at Fatamorgana: €3–5. Hotel de Russie runs €500–900. Mid-range hotels near the center: €150–300. Trastevere apartments: €100–200 per night." },
    ],
  },
  {
    name: "Florence", country: "italy", tag: "Renaissance · Food · Craft",
    hook: "The museums are overwhelming. The Oltrarno neighborhood is why you stay.",
    img: "https://images.unsplash.com/photo-1543429776-2782fc8e1acd?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")) s+=4; if(a[0]?.includes("food")) s+=2; if(a[3]?.includes("balanced")||a[3]?.includes("luxury")) s+=2; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("cities")||a[5]?.includes("countryside")) s+=2; if(a[6]?.includes("absorb")||a[6]?.includes("eat")) s+=3; if(a[1]?.includes("partner")||a[1]?.includes("solo")) s+=1; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("beauty")||a[8]?.includes("surprise")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("sit")) s+=2; if(a[8]?.includes("deep")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")) s-=1; return s; },
    intro: "Florence is one of those cities where the museums are so overwhelming that people forget it's actually a living place. The Uffizi and David are real and should not be missed — but the Florence worth staying for is the Oltrarno neighborhood across the river, the Mercato Centrale at 8am, the bistecca Fiorentina at a table with no tablecloth, the Chianti in a carafe that cost €6 and was better than most €40 bottles. Give it three days. The second day is always better than the first.",
    highlights: [
      { label: "Oltrarno", text: "The neighborhood across the Ponte Vecchio. Artisan workshops, aperitivo bars, restaurants that have been there for forty years. The real Florence lives here." },
      { label: "Uffizi — book ahead", text: "The greatest collection of Renaissance painting in the world. Book online two weeks in advance, arrive at your time slot, and give yourself three hours minimum. The Botticellis alone justify the trip." },
      { label: "Mercato Centrale", text: "The covered market near San Lorenzo. Go early morning for fresh produce, cheese, and the truffle merchants. The upstairs food hall is great for lunch — arrive before noon." },
      { label: "San Miniato al Monte at sunset", text: "The Romanesque church on the hill above the Piazzale Michelangelo. Almost no one walks up here. The view over Florence at sunset, with no one around, is one of the best things in Italy." },
    ],
    eat: [
      { name: "Osteria del Cinghiale Bianco", desc: "Old stone walls, paper tablecloths, wild boar pappardelle that's been on the menu for decades because it's perfect. The version of Florence that still exists if you know where to find it." },
      { name: "Trattoria Mario", desc: "Long communal tables, no reservations, cash only, open for lunch only Monday through Saturday. The ribollita (Tuscan bread soup) and bistecca are why locals have been eating here since 1953." },
      { name: "Il Latini", desc: "The famous loud Florentine trattoria. Long tables, shared plates, wine in carafes, strangers becoming friends. Touristy? Yes. Still worth it? Also yes." },
      { name: "Buca Mario", desc: "The oldest restaurant in Florence, opened in 1886. The menu is Florentine classics — lampredotto (tripe sandwich), pappardelle with wild boar, bistecca. Order the bistecca for two." },
      { name: "Gelateria dei Neri", desc: "Oltrarno neighborhood gelato. The ricotta and fig, the dark chocolate with orange peel. Go twice." },
    ],
    stay: [
      { name: "Portrait Firenze", tier: "High end", desc: "Salvatore Ferragamo's boutique hotel on the Lungarno. Suites only, river views, rooftop terrace. Small, private, exceptional service." },
      { name: "Hotel Davanzati", tier: "Mid range", desc: "Family-run hotel in the center, right near the Piazza della Repubblica. Honest prices, genuinely helpful staff, good breakfast. They'll book everything for you if you ask." },
      { name: "Oltrarno Apartments", tier: "Good value", desc: "Renting in Oltrarno puts you in the neighborhood Florentines actually live in. Search for apartments in San Frediano or Santo Spirito specifically." },,
      { name: "AdAstra (Oltrarno)", tier: "Mid range", desc: "A small guesthouse in a Renaissance palazzo on the south side of the Arno. Five rooms, beautiful original frescoes, the Oltrarno neighbourhood right outside the door. The un-touristy Florence base." },
    ],
    logistics: [
      { q: "When to go", a: "April–May and September–October. Florence in June–August is extremely crowded and hot (35°C+). The Uffizi queue in July is a full day without advance booking. Spring is exceptional — the city is manageable and the light is perfect. November is underrated: crowds disappear, prices drop, and the city returns to the Florentines." },
      { q: "Getting there", a: "Florence Santa Maria Novella station is on the main high-speed rail line — 1.5 hours from Rome (€25–50), 2 hours from Milan (€30–60). The train is almost always better than flying. Florence Peretola Airport (FLR) has some European connections but is small. Most people fly into Rome or Milan and take the train." },
      { q: "Getting around", a: "Florence's historic center is almost entirely walkable — the Uffizi, Duomo, Ponte Vecchio, and Oltrarno are all within 20 minutes of each other on foot. Buses run efficiently for anything further out. Avoid renting a car in Florence — the historic center is ZTL-restricted, parking is impossible, and you don't need it." },
      { q: "Booking ahead", a: "Uffizi: book at least 2 weeks in advance online, arrive at your timed slot. Accademia (Michelangelo's David): same — book ahead. Osteria del Cinghiale Bianco: 1–2 weeks in advance. Trattoria Mario is first-come, first-served — arrive at 11:45am when they open for lunch. The Borghese Gallery in Rome is not in Florence, but the Bargello museum here is equally extraordinary and rarely queued." },
      { q: "How long", a: "Three nights minimum, four is better. Day one: Uffizi (half day), Oltrarno evening. Day two: Accademia, Mercato Centrale, San Miniato at sunset. Day three: day trip to Fiesole or Chianti wine country by car. Day four: slow morning in Oltrarno, departure. Florence rewards taking your time — the second day is always better than the first." },
      { q: "Money", a: "Florence is more expensive than southern Italy but reasonable by northern European standards. Espresso at the bar: €1.50. Bistecca Fiorentina for two at a serious trattoria: €60–80. Uffizi entry: €20. Portrait Firenze runs €600–1,200. Hotel Davanzati: €150–250. Oltrarno apartments: €120–200 per night." },
    ],
  },
  {
    name: "Milan", country: "italy", tag: "Design · Fashion · Gateway",
    hook: "Most people fly through Milan on the way somewhere else. That's a mistake.",
    img: "https://images.unsplash.com/photo-1513581166391-887a96ddeafd?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=2; if(a[3]?.includes("luxury")||a[3]?.includes("balanced")) s+=3; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("cities")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("absorb")) s+=2; if(a[1]?.includes("partner")||a[1]?.includes("friends")) s+=1; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("connection")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("plan")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("tourist")) s+=1; return s; },
    intro: "Milan is the city most people fly into and leave immediately for somewhere more 'Italian.' That's a mistake, but also exactly the mistake that keeps Milan good. It's a serious, working city — the design capital of the world, the fashion capital of Europe, home to one of the great paintings ever made (The Last Supper), and a food scene that has quietly become one of the best in Italy. Two days minimum. You'll be surprised.",
    highlights: [
      { label: "The Last Supper — book months ahead", text: "Leonardo da Vinci's mural in the refectory of Santa Maria delle Grazie. Fifteen-minute timed entry slots, 25 people at a time. Books out six months in advance. Do it before anything else or you will miss it." },
      { label: "Navigli canals", text: "Milan's canal district. Aperitivo bars line the water, the scene goes from 6pm to midnight, the prices are lower than the city center. The best place to eat and drink in Milan." },
      { label: "Brera neighborhood", text: "The art district. Gallery, design studios, the best antique market in Milan on the third Saturday of every month, restaurants that don't need a reservation because the tourists haven't found them yet." },
      { label: "Galleria Vittorio Emanuele II", text: "The 19th-century shopping arcade is one of the most beautiful buildings in Italy. Go for the architecture, not the shops. The Camparino bar inside has been serving aperitivo since 1915." },
    ],
    eat: [
      { name: "Trattoria del Nuovo Macello", desc: "The real Milan. Offal dishes, braised meats, risotto alla Milanese (with saffron, bone marrow, and an intensity that will recalibrate what you think risotto is). No tourists, book ahead." },
      { name: "Luini", desc: "Panzerotti — deep-fried half-moon pastries filled with tomato and mozzarella — from a tiny shop near the Duomo that has been there since 1888. Queue starts at 11am. Worth it." },
      { name: "Il Salumaio di Montenapoleone", desc: "Deli and restaurant in a courtyard off Via Montenapoleone. The best charcuterie and cheese lunch in Milan, surrounded by fashion buyers on their lunch break." },
      { name: "Ratanà", desc: "Milan's most respected modern Milanese restaurant. Cassoeula (pork and cabbage stew), cotoletta Milanese, ossobuco — all done properly with great wine." },
    ],
    stay: [
      { name: "Armani Hotel Milano", tier: "High end", desc: "Giorgio Armani designed every detail himself. On Via Manzoni, the most elegant street in Milan. For people who understand that Milan is a fashion city and want a hotel that agrees." },
      { name: "Nhow Milano", tier: "Mid range", desc: "Design hotel in the Tortona district — Milan's design quarter, near the Navigli. One of the best mid-range options in the city for people interested in design." },
      { name: "Navigli District Apartments", tier: "Good value", desc: "Staying in the Navigli area means aperitivo is your doorstep and the Porta Genova market is your Saturday morning. Best neighborhood to base yourself in Milan." },,
      { name: "Maison Borella (Navigli)", tier: "Mid range", desc: "A Belle Époque canal house on the Naviglio Grande. The most characterful hotel in Milan — antique furniture, canal views, the aperitivo strip outside the door." },
    ],
    logistics: [
      { q: "When to go", a: "April–June and September–November. Milan is a working city and operates year-round, but spring and autumn are when the fashion and design weeks bring the city alive. July–August is quieter (Milanese leave for the lakes and coast), which is actually pleasant — less traffic, easier reservations. December is excellent for the Christmas markets around the Duomo." },
      { q: "Getting there", a: "Milan Malpensa (MXP) is the main international airport — good US connections and the widest European choice. The Malpensa Express train to Milano Centrale takes 52 minutes (€13). Milan Linate (LIN) is closer to the city (25 minutes by bus) and handles European routes. The city is also a major rail hub — trains to Turin, Venice, Florence, and Rome leave from Centrale constantly." },
      { q: "Getting around", a: "Milan's Metro (4 lines) is efficient and covers all the main neighborhoods. The tram network is excellent and faster than it looks on the map. Uber works well. Walking is the best option in the Navigli, Brera, and Tortona districts. A car is unnecessary and parking is expensive — avoid it entirely." },
      { q: "How long", a: "Two to three nights. Day one: The Last Supper (pre-booked), Brera neighborhood, Navigli aperitivo. Day two: Duomo, Galleria Vittorio Emanuele, lunch at Il Salumaio, afternoon at the Pinacoteca di Brera (underrated art museum, rarely crowded). Day three: Tortona design district or a day trip to Lake Como (1 hour by train to Varenna)." },
      { q: "Aperitivo culture", a: "Milan invented the aperitivo hour and does it better than anywhere else in Italy. From 6–9pm, most bars offer free food with every drink — a selection that ranges from olives and chips to full buffet spreads. The Navigli is the best neighborhood for it. Order a Campari (invented in Milan in 1860), an Aperol spritz, or a local vermouth. Budget €8–12 per drink." },
      { q: "Money", a: "Milan is the most expensive city in Italy. Espresso at the bar: €1.50–2. Panzerotti at Luini: €3. Lunch at Il Salumaio: €30–50. Dinner at Ratanà: €50–80. Armani Hotel runs €500–1,000. Nhow Milano: €180–300. The Navigli neighborhood is significantly cheaper than the fashion district for restaurants and bars." },
    ],
  },
  {
    name: "Capri", country: "italy", tag: "Island · Sea · Glamour",
    hook: "Stay overnight. The island becomes completely different when the ferries leave.",
    img: "https://images.unsplash.com/photo-1555990793-da11153b2473?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("food")) s+=2; if(a[3]?.includes("luxury")||a[3]?.includes("balanced")) s+=3; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("coast")) s+=4; if(a[6]?.includes("wander")||a[6]?.includes("eat")) s+=2; if(a[1]?.includes("partner")) s+=3; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=2; if(a[8]?.includes("beauty")||a[8]?.includes("quiet")) s+=2; if(a[9]?.includes("sit")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")) s-=1; return s; },
    intro: "Capri has been the most glamorous island in the Mediterranean for over a century — Roman emperors, Jackie Kennedy, Brigitte Bardot, the whole lineage. It's also genuinely, irreducibly beautiful: white villages on vertical cliffs, water so clear it looks digital, a Blue Grotto that earns every superlative ever applied to it. The trick is staying overnight when the day-trippers leave and the island becomes itself again. One night changes everything.",
    highlights: [
      { label: "The Blue Grotto", text: "A sea cave lit by an underwater opening that turns the water an impossible electric blue. Go in the morning when the light is right and the queue is manageable. The boats that take you in are absurdly small." },
      { label: "Anacapri and Monte Solaro", text: "Take the chairlift from Anacapri to the top of Monte Solaro. The view from the summit — Vesuvius, the Amalfi Coast, the Bay of Naples — is one of the great views in Italy." },
      { label: "Via Krupp and the Faraglioni", text: "The zigzag cliff path from the Gardens of Augustus down to the Marina Piccola. The view of the Faraglioni rock formations from here is the defining image of Capri." },
      { label: "Stay overnight", text: "The last hydrofoil back to Naples leaves at 7pm. Everyone is on it. The people who stay for dinner and take a room have a completely different island." },
    ],
    eat: [
      { name: "Lo Smeraldo", desc: "On the Marina Grande waterfront, directly opposite the hydrofoil dock. The seafood pasta is why you arrived. Eat here on arrival before going up to Capri town." },
      { name: "Da Paolino", desc: "Tables set under a lemon grove, lit at night, lemon-based everything — pasta al limone, lemon granite, limoncello made from the trees above your head. One of the most atmospheric restaurants in Italy." },
      { name: "Il Riccio", desc: "Michelin-starred seafood restaurant hanging over the water in Anacapri. The sea urchin pasta is the reason this restaurant exists. Lunch only, reserve well in advance." },
      { name: "Bar Tiberio (Piazzetta)", desc: "The café on Capri's famous Piazzetta. Overpriced and worth every cent for the 45 minutes of theater that is the Piazzetta at aperitivo hour. Order a Campari spritz and watch." },
    ],
    stay: [
      { name: "Grand Hotel Quisisana", tier: "High end", desc: "The classic Capri hotel. In the center of Capri town, pool, gardens, impeccable service. Where every famous person who has ever been to Capri has stayed at least once." },
      { name: "Hotel La Tosca", tier: "Mid range", desc: "Small, quiet, family-run, with a garden and terraces looking over the sea. The best value on the island — not cheap, but genuinely good for Capri. Book months ahead." },
      { name: "Villa rental in Anacapri", tier: "Good value", desc: "Anacapri is quieter and cheaper than Capri town. Renting a private villa here for three nights with a terrace and a lemon tree is the right way to do the island." },,
      { name: "Hotel La Minerva", tier: "Mid range", desc: "A family-run hotel in Capri town with a terrace garden and views over the rooftops to the sea. The honest alternative to the grand hotels — personal service, genuine character, a fraction of the price." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October. July–August the island is at maximum capacity — the hydrofoils are packed, Capri town is wall-to-wall, and the Piazzetta becomes a performance rather than a place. June and September are close to the same beauty with half the crowd. The Blue Grotto closes when seas are rough (October–April); plan accordingly." },
      { q: "Getting there", a: "Hydrofoil or ferry from Naples (Molo Beverello) — 40–50 minutes by hydrofoil (€20–25), 80 minutes by ferry (€15). Also ferries from Sorrento (25 minutes, €15) and Positano in summer. Naples is a 45-minute train from Rome. The last hydrofoil back to Naples is around 7pm — missing it means staying overnight, which you should plan to do anyway." },
      { q: "Getting around", a: "No private cars are allowed on Capri without a permit. From Marina Grande (where you dock), take the funicular up to Capri town (€2) or a taxi. For Anacapri, take the local bus from Capri town (€2). The island is small enough to walk between most points — Via Krupp and the path to Monte Solaro are best done on foot. Scooter rental is available and excellent." },
      { q: "Stay overnight", a: "This is the single most important piece of Capri advice. The last ferry leaves at 7pm and every day-tripper is on it. The people who stay for dinner, watch the sunset from the Gardens of Augustus, and have Capri town to themselves after 8pm have a completely different experience. One night is transformative. Book hotels months in advance for peak season." },
      { q: "Money", a: "Capri is expensive by Italian standards. A Campari spritz at the Piazzetta: €15–20. Dinner at Da Paolino (the lemon grove restaurant): €60–100 per person. Grand Hotel Quisisana runs €400–900. Hotel La Tosca (the best value): €180–350. The Blue Grotto boat tour: €15 plus €14 entry. Budget significantly more than anywhere else on this site." },
      { q: "Day trip vs. overnight", a: "A day trip from Naples or Sorrento covers the main sights — Blue Grotto, Anacapri, the Piazzetta. An overnight stay gives you the island after the ferries leave, dinner under a lemon grove, sunrise from the Gardens of Augustus, and the Piazzetta at breakfast when it belongs to the locals. The difference is not incremental — it's a completely different place." },
    ],
  },
  {
    name: "Sardinia", country: "italy", tag: "Sea · Wild Interior · Nuraghe",
    hook: "The water will make you check if your camera is broken. It isn't.",
    img: "https://images.unsplash.com/photo-1594222082006-5c6adb8d4bbc?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("coast")) s+=3; if(a[6]?.includes("explore")||a[6]?.includes("wander")) s+=2; if(a[2]?.includes("week")||a[2]?.includes("twoweeks")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("freedom")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("walk")) s+=3; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=2; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")) s+=2; if(a[6]?.includes("physical")||a[6]?.includes("spontaneous")) s+=1; return s; },
    intro: "Sardinia has the most extraordinary water in the Mediterranean — the kind of blue-green that makes people check whether their camera is broken. But the island is much more than its coast: a wild, mountainous interior that has barely changed in centuries, a cuisine completely unlike mainland Italy, and the nuraghe — thousands of ancient stone towers built by a Bronze Age civilization that left behind almost no written record. Sardinia rewards people who rent a car and get lost.",
    highlights: [
      { label: "Costa Smeralda", text: "The Emerald Coast in the northeast — the most famous and expensive stretch of coastline on the island. The water is worth the hype. Stay in the villages behind the coast (Arzachena, Cannigione) rather than Porto Cervo itself." },
      { label: "The Nuraghe", text: "Over 7,000 ancient stone towers scattered across the island, built by the Nuragic civilization between 1800 and 700 BC. The Nuraghe Su Nuraxi near Barumini is UNESCO-listed and the most impressive. Seeing them in the middle of nowhere, with no explanation and no other tourists, is better." },
      { label: "Orgosolo", text: "A mountain village in the Barbagia region whose walls are covered in murals — political, cultural, historical. It looks like nothing else in Italy. Get there by driving through the Gennargentu mountains." },
      { label: "The southwest — Sulcis-Iglesiente", text: "The least visited corner of the island. Ancient mining towns, Phoenician ruins, cliffs over a sea that looks prehistoric. Almost no tourists, extraordinary landscape." },
    ],
    eat: [
      { name: "Su Gologone Restaurant (Oliena)", desc: "In the mountains of the Barbagia region, this is where you eat porceddu — whole suckling pig roasted over myrtle wood. One of the fundamental Sardinian experiences. Book ahead." },
      { name: "Dal Corsaro (Cagliari)", desc: "The best restaurant in the capital. Sardinian classics executed with real precision — bottarga (cured fish roe shaved over pasta), malloreddus (Sardinian gnocchi), seadas (cheese pastry with honey). Two Michelin stars." },
      { name: "La Stella Marina di Montecristo (Alghero)", desc: "Alghero's seafood restaurant institution. The lobster — aragosta — prepared alla catalana (cold with tomatoes and onions) is the local specialty. Order the whole one." },
      { name: "Trattoria Lilicu (Cagliari)", desc: "The honest version of Cagliari eating. Fregola (Sardinian couscous) with clams, pane carasau (the paper-thin flatbread) with everything, local Vermentino wine. Locals only, book ahead." },
    ],
    stay: [
      { name: "Hotel Cala di Volpe", tier: "High end", desc: "The iconic Costa Smeralda hotel designed to look like a Sardinian fishing village. Lagoon-style pool that extends to the sea. The benchmark luxury experience on the island." },
      { name: "Su Gologone Hotel (Oliena)", tier: "Mid range", desc: "The mountain hotel attached to the famous restaurant. An extraordinary place — art everywhere, a pool carved from stone, the silence of the Barbagia. Nowhere like it in Italy." },
      { name: "Agriturismo in the interior", tier: "Good value", desc: "Farm stays in the Barbagia or Ogliastra regions. Dinner is included (usually porceddu or lamb), the pace is prehistoric, and the landscape is completely untouched. Search Agriturismi.it filtered by Sardinia." },,
      { name: "Agriturismo Su Carduleu (Abbasanta)", tier: "Good value", desc: "A sheep farm in the Sardinian interior serving dinner at one long table — porceddu, culurgiones, homemade wine. Rooms are simple, the food is the reason people go. The most honest Sardinian experience." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October. July–August the Costa Smeralda becomes the most expensive and crowded coastline in the Mediterranean — Sardinians and wealthy Europeans fill every hotel. June is warm, the sea is swimmable, and the island feels like yours. September is the sweet spot: peak warmth, fading crowds. The interior (Barbagia, Gennargentu) is good year-round — the festivals happen in winter." },
      { q: "Getting there", a: "Fly into Cagliari (CAG) for the south and interior, or Olbia (OLB) for the Costa Smeralda and north. Both have European connections and summer US charter flights. Alghero (AHO) in the northwest is the gateway for that coast. Ferries from Civitavecchia (near Rome), Genoa, and Livorno take 8–12 hours — beautiful overnight crossing if you have a car to bring." },
      { q: "Getting around", a: "Car is essential for anything beyond the main cities. The SS125 running down the east coast is one of the great coastal drives in Italy. The mountain roads through the Barbagia are slower but extraordinary. Rent a car at the airport and keep it for the whole trip. In Cagliari and Alghero, the centers are walkable. The Costa Smeralda has a shuttle system in summer but a car makes everything possible." },
      { q: "How long", a: "One week minimum to see more than one part of the island. Days 1–3: Costa Smeralda and the northeast (Baia Sardinia, Santa Teresa, the Maddalena islands). Days 4–5: drive south through the interior via Orgosolo and the Barbagia, lunch at Su Gologone. Days 6–7: Cagliari and the southern coast. Two weeks allows the full circuit including the west coast (Alghero, Bosa) and the Sulcis mining region." },
      { q: "Money", a: "Sardinia has a wide range. Costa Smeralda in July–August is among the most expensive destinations in Europe — Hotel Cala di Volpe runs €800–2,000, beach clubs charge €50 for a sun lounger. The interior is dramatically cheaper — agriturismi with dinner: €80–150, local restaurants: €20–35. Cagliari is excellent value. Going in June or September cuts Costa Smeralda prices by 30–50%." },
      { q: "Food notes", a: "Sardinian cuisine is completely distinct from mainland Italy. Porceddu (whole suckling pig roasted over myrtle wood) is the signature dish. Bottarga (cured grey mullet roe grated over pasta) is extraordinary and unique. Pane carasau (paper-thin flatbread) is on every table. The local white wine is Vermentino — light, mineral, perfect with seafood. Cannonau (Grenache) is the red — one of the oldest wine varieties in the world." },
    ],
  },
  {
    name: "Amalfi Coast", country: "italy", tag: "Cliffs · Sea · The Wrong Way to Do It",
    hook: "Everyone does Positano. Go to Ravello and Cetara instead. Same coast, different planet.",
    img: "https://images.unsplash.com/photo-1533587851505-d119e13fa0d7?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("beauty")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("luxury")||a[3]?.includes("explorer")) s+=2; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("coast")) s+=4; if(a[6]?.includes("wander")||a[6]?.includes("eat")) s+=2; if(a[1]?.includes("partner")) s+=3; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=2; if(a[8]?.includes("beauty")||a[8]?.includes("quiet")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("sit")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")) s-=2; return s; },
    intro: "The Amalfi Coast is 50km of cliffs dropping into the Tyrrhenian Sea, vertical villages painted in terracotta and ochre, and a road — the SS163 — that is one of the great drives in Europe. It is also one of the most visited places in Italy, which means Positano in July is a traffic jam of Instagram photographers. The solution is simple: go to Ravello instead of Positano, go to Cetara instead of Amalfi town, and go in May or October instead of August. The same coast. Completely different experience.",
    highlights: [
      { label: "Ravello", text: "The village on the clifftop above the coast, 365 meters above sea level, accessible by a steep road from Amalfi town. Wagner composed here. The Villa Rufolo garden, with its terrace hanging over the sea, is one of the most beautiful places in Italy. Almost no day-trippers make it up. Spend the night." },
      { label: "Cetara", text: "The fishing village the tour buses skip. No designer boutiques, no famous hotels — just a working harbor, an anchovy processing cooperative, and the best seafood restaurant on the coast (Acquapazza). The colatura di alici (anchovy extract, aged in oak barrels) produced here is one of the great condiments of Italy." },
      { label: "The Path of the Gods (Sentiero degli Dei)", text: "The hiking trail from Agerola to Nocelle that follows the clifftops 600 meters above the sea. Four to five hours, the most dramatic coastal views in southern Italy. Take the bus up to Agerola, walk to Nocelle, then take the steps down to Positano for a late lunch and a boat back." },
      { label: "Praiano at dawn", text: "The village between Positano and Amalfi that nobody chooses as a base, which means it has almost no tourist infrastructure — and very few tourists. Wake up early, walk to the San Gennaro church terrace, and watch the sun come up over the coast before the first ferry arrives." },
    ],
    eat: [
      { name: "Acquapazza (Cetara)", desc: "The only restaurant you need on the Amalfi Coast. Gennaro Marciante's cooking is built entirely around what came off the boats that morning. The spaghetti con colatura (pasta with anchovy extract), the fresh-caught alici (anchovies) in every form. Book ahead — it's small." },
      { name: "Ristorante Rossellinis (Ravello)", desc: "The Palazzo Avino hotel restaurant with a terrace hanging over the sea at 365 meters. The Michelin-starred menu uses local Campanian ingredients — buffalo mozzarella, local lemons, Amalfi citrus. The view from the table is the main dish." },
      { name: "Il Pirata (Praiano)", desc: "The most atmospheric restaurant on the coast — in a sea cave accessible by a private boat from the harbor. Grilled fish, fresh pasta, the sound of the sea. Lunch only. Book through the restaurant." },
      { name: "Da Gemma (Amalfi)", desc: "Open since 1872, run by the same family. The sfusato amalfitano lemon — enormous, sweet, almost no pith — appears in everything: the limoncello, the pasta, the desserts. Eat the scialatielli ai frutti di mare (fresh pasta with shellfish) and order a carafe of the house white." },
      { name: "Nonna Rosa (Vico Equense)", desc: "One of the great small restaurants in Campania, just north of the coast. Peppe Guida's cooking celebrates the overlooked ingredients of the region — chestnuts, local beans, the simplest pasta. One Michelin star, deserves three." },
    ],
    stay: [
      { name: "Palazzo Avino (Ravello)", tier: "High end", desc: "A 12th-century villa on the clifftop in Ravello. The best hotel on the Amalfi Coast — a pool hanging over the sea, extraordinary restaurant, the correct choice if budget allows." },
      { name: "Hotel Villa Cimbrone (Ravello)", tier: "High end", desc: "A Gothic villa with the most dramatic garden terrace in southern Italy — the Belvedere of Infinity, a balustrade of classical busts overlooking the sea 300 meters below. Virginia Woolf and Greta Garbo stayed here." },
      { name: "Hotel il Convento (Praiano)", tier: "Mid range", desc: "A converted 16th-century convent in Praiano with a pool and sea views. The best mid-range option on the coast — away from the Positano crowds, genuinely peaceful, walking distance to good restaurants." },,
      { name: "Agriturismo La Ginestra (Vico Equense)", tier: "Good value", desc: "A farm on the hillside above the coast between Sorrento and Positano. Simple rooms, extraordinary views, and a kitchen using only farm produce. The antidote to the Amalfi Coast price spiral." },
    ],
    logistics: [
      { q: "When to go", a: "May and October. June is still manageable. July–August the SS163 becomes a car park and Positano fills to the point of unpleasantness. October is the best month: the sea is still warm (24°C), the crowds are gone, the light is extraordinary, and the lemon groves are fragrant. May has the wildflowers and the Path of the Gods at its best." },
      { q: "Getting there", a: "Fly into Naples (NAP) — well connected from major European hubs and with some US connections. From Naples, take the Circumvesuviana train to Sorrento (1 hour) then the SITA bus along the coast (1.5 hours to Amalfi) or ferry in season. Alternatively, rent a car in Naples and drive — the SS163 is spectacular but slow (40km takes 90 minutes in summer). Parking is almost impossible in the villages — use the paid lots at the village entrances." },
      { q: "Getting around", a: "The SITA bus runs the length of the coast and is the most practical option — €2.50 per journey, runs every 30 minutes in season. The ferry system connects the main villages in summer (April–October) — faster and more beautiful than the road. For Ravello and inland villages, you need a car or taxi. The roads are narrow enough that local taxis know shortcuts that save significant time." },
      { q: "How long", a: "Four nights minimum. Night one: base in Ravello — walk the gardens, eat at Rossellinis. Day two: drive or bus to Cetara for lunch at Acquapazza, explore Amalfi town. Day three: Path of the Gods hike, end in Positano for a boat back. Day four: Praiano at dawn, ferry to Capri for the day. The coast pairs naturally with Naples (extraordinary food city, 1 hour) and Pompei (45 minutes from Sorrento)." },
      { q: "The Positano question", a: "Go to Positano for one afternoon — take the ferry in, walk the village, have a limoncello on a terrace, take the ferry out. Don't stay there: the accommodation is 40% more expensive than anywhere else on the coast, the traffic is brutal, and the village is so vertical that everything requires climbing steps. The experience is beautiful. The overnight is unnecessary." },
      { q: "Money", a: "The Amalfi Coast is expensive — one of the pricier destinations in Italy. Palazzo Avino: €500–1,200. Hotel il Convento (Praiano): €150–280. A seafood lunch at Acquapazza: €50–70 per person. The SITA bus: €2.50. The ferry from Amalfi to Positano: €8. A limoncello on a Positano terrace: €12. Budget €200–300 per person per day for a mid-range Amalfi experience." },
    ],
  },
  {
    name: "Matera", country: "italy", tag: "Cave City · UNESCO · Ancient",
    hook: "People have lived continuously in these caves for 9,000 years. It was a national disgrace. Then it became a European Capital of Culture.",
    img: "https://images.unsplash.com/photo-1569338081481-6c8be10842c5?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=3; if(a[5]?.includes("cities")||a[5]?.includes("countryside")) s+=2; if(a[6]?.includes("absorb")||a[6]?.includes("wander")) s+=3; if(a[7]?.includes("midrange")||a[7]?.includes("budget")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=4; if(a[9]?.includes("walk")||a[9]?.includes("sit")) s+=3; if(a[8]?.includes("people")||a[8]?.includes("article")) s+=2; if(a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=3; if(a[6]?.includes("fullday")||a[6]?.includes("absorb")) s+=1; return s; },
    intro: "Matera is one of the oldest continuously inhabited cities on earth — the sassi (stone cave dwellings carved into a ravine) have been occupied for at least 9,000 years, possibly longer. In the 1950s the Italian government declared the sassi a national disgrace and forcibly relocated 15,000 people to new housing on the plateau above. Fifty years later the sassi were declared a UNESCO World Heritage Site and the same caves became boutique hotels. Matera was European Capital of Culture in 2019. The city is disorienting, beautiful, and completely unlike anything else in Italy or anywhere else.",
    highlights: [
      { label: "The Sassi Barisano and Caveoso", text: "The two cave districts on either side of the ravine. Walk through them at night when most visitors have left — the labyrinth of carved stone streets, the cave churches, the gorge below lit by a thousand small lights. The view from the opposite ridge across the ravine is the one on every photograph. The reality is better." },
      { label: "The rupestrian churches", text: "Cave churches carved into the rock and painted with Byzantine frescoes between the 8th and 13th centuries. Santa Maria de Idris, Santa Lucia alle Malve, the Madonna delle Virtù — each one a different light, a different set of frescoes, a different depth in the rock. The Cripta del Peccato Originale outside town has the most extraordinary frescoes in the region." },
      { label: "The ravine (Gravina)", text: "The deep gorge that the ancient city was built around — and that the city looks directly into. Walk down into it in the morning before it's warm, cross the bottom, and look back up at the sassi rising 200 meters above you. The ancient cave dwellings on the opposite cliff face are even older than the inhabited sassi." },
      { label: "Piazza Vittorio Veneto at dusk", text: "The main square of the new town on the plateau above the sassi. At dusk, the Materans come out — the passeggiata, the aperitivo, the evening ritual. The view from the square's edge down into the illuminated sassi as the sky goes dark is the moment the city reveals why it became a Capital of Culture." },
    ],
    eat: [
      { name: "Ristorante Vitantonio Lombardo", desc: "The best restaurant in Matera — one Michelin star, in a 13th-century cave palazzo. The menu is built entirely on Basilicata's forgotten ingredients: crusco peppers, Senise chili, local lamb, ancient grain pasta. Book well ahead." },
      { name: "Osteria Il Casale", desc: "The most honest local restaurant in Matera. Handmade orecchiette, slow-braised lamb, the local caciocavallo cheese, good Aglianico wine. Full of Materans at lunch. Exactly what it should be." },
      { name: "Baccanti", desc: "Natural wine bar and restaurant in the sassi. The wine list is focused on southern Italian producers — Basilicata, Campania, Calabria — and the small plates are made to match them. Good for dinner after a long day of walking." },
      { name: "Pasticceria Sassidea", desc: "The best pastry shop in Matera. The calzoncelli (fried pastries filled with fig jam and chocolate), the pasticciotto, the local almond sweets. Go at 8am when everything is fresh. Go again at 5pm." },
    ],
    stay: [
      { name: "Sextantio Le Grotte della Civita", tier: "High end", desc: "Eighteen cave rooms carved into the rock of the Caveoso, restored with minimalist precision — bare rock walls, handmade linens, candlelight. The most extraordinary hotel in Italy and one of the most extraordinary in the world. Breakfast delivered to your cave." },
      { name: "Palazzo Viceconte", tier: "Mid range", desc: "A 19th-century palazzo on the edge of the sassi with views across the ravine. Beautiful rooms, excellent breakfast, the most characterful mid-range option in the city." },
      { name: "Cave apartment rental", tier: "Good value", desc: "Rent a restored cave apartment in the Sassi Barisano for a week. Many have been converted into self-catering rentals — stone walls, domed ceilings, sleeping in a space that has been inhabited for millennia. Search Airbnb filtered by 'Matera sassi'." },,
      { name: "Locanda di San Martino", tier: "Mid range", desc: "A cave hotel in the Sassi Barisano with a rooftop terrace and a swimming pool carved into the rock. More affordable than Sextantio with the same cave experience. Book the cave room not the standard room." },
    ],
    logistics: [
      { q: "When to go", a: "April–June and September–October. Matera sits inland in Basilicata and gets very hot in July–August (38–42°C) — the stone city absorbs heat and holds it. Spring and autumn are perfect: 20–28°C, the light is extraordinary, and the tourist numbers are manageable. The city is equally beautiful in winter — cold, often foggy, almost empty." },
      { q: "Getting there", a: "The nearest airports are Bari (BRI, 65km, 1 hour) and Naples (NAP, 230km, 2.5 hours). From Bari, take the FAL train to Matera (1.5 hours) or rent a car. Matera is awkward to reach by public transport from most of Italy — a car is the most practical option for combining it with Puglia, Calabria, or the Amalfi Coast." },
      { q: "Getting around", a: "Matera is entirely walkable — the sassi are pedestrianized and the city is compact. The ravine requires some climbing — wear comfortable shoes and be prepared for uneven stone surfaces. The new town (Piano) above the sassi is 10 minutes on foot from the sassi entrance. There's no public transport within the sassi. The Cripta del Peccato Originale (15km outside town) requires a car or taxi." },
      { q: "How long", a: "Two nights minimum, three is better. Day one: arrive afternoon, walk the Sassi Barisano at dusk, dinner in the sassi. Day two: early morning walk into the ravine, rupestrian churches in the morning, Piazza Vittorio Veneto in the evening. Day three: day trip to the Cripta del Peccato Originale, slow departure. Matera pairs naturally with Puglia (1.5 hours) and Calabria (2 hours) for a southern Italian road trip." },
      { q: "The cave hotel experience", a: "Sextantio Le Grotte della Civita is expensive (€250–500 per night) but genuinely unlike any other hotel experience in the world. Sleeping in a cave that has been inhabited since the Paleolithic, in a room with no right angles, with candles as the only light, is disorienting in the best possible way. If you're going to Matera, stay in a cave." },
      { q: "Money", a: "Matera is excellent value by Italian standards. Sextantio: €250–500. Palazzo Viceconte: €100–180. Cave apartment: €80–150. Dinner at Vitantonio Lombardo: €80–120 per person. An osteria lunch: €20–35. A glass of Aglianico in a wine bar: €5–8. The sassi themselves are free to walk — the church entry fees are €3–8 each." },
    ],
  },
  {
    name: "Calabria", country: "italy", tag: "Overlooked · Nduja · Wild Coast",
    hook: "The toe of Italy's boot. The most overlooked region in Western Europe. The food alone is worth the trip.",
    img: "https://images.unsplash.com/photo-1612528443702-f6741f70a049?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=4; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=4; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("eat")) s+=3; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=3; if(a[8]?.includes("surprise")||a[8]?.includes("connection")) s+=4; if(a[9]?.includes("walk")||a[9]?.includes("eat")) s+=2; if(a[8]?.includes("none")||a[8]?.includes("people")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; if(a[6]?.includes("spontaneous")||a[6]?.includes("physical")) s+=2; return s; },
    intro: "Calabria is the toe of Italy's boot — the southernmost region of the peninsula, separated from Sicily by the Strait of Messina, and the most overlooked region in Western Europe. It produces the nduja (spreadable spiced salami) that every London restaurant now claims to use authentically. It has two extraordinary coastlines: the Tyrrhenian to the west, turquoise and dramatic; the Ionian to the east, flat, sandy, and backed by ancient Greek ruins. The Aspromonte mountains in the interior are genuinely wild. Almost nobody from outside Italy goes. The people who do go come back changed.",
    highlights: [
      { label: "Tropea", text: "The medieval town on a rock above the Tyrrhenian Sea — the most photographed place in Calabria and the one exception to the region's obscurity. The sea here is genuinely Caribbean in color. The red onion grown on the slopes below the town is world-famous in Italy and almost unknown outside it. Go in June or September — August is the one Italian month where even Calabria fills up." },
      { label: "The Ionian coast and Magna Graecia", text: "The eastern coast was colonized by ancient Greeks who called it Magna Graecia — Greater Greece. Locri, Caulonia, and Sybaris all have significant archaeological sites. The Riace Bronzes (two extraordinary 5th-century BC Greek bronze statues found by a diver in 1972) are in the Museo Nazionale di Reggio Calabria — the best ancient Greek sculptures in Italy." },
      { label: "The Aspromonte", text: "The mountain massif at the toe of the boot — 1,955 meters at its highest, with forests, gorges, and small villages that time forgot. The Polsi sanctuary in the gorge is one of the most atmospheric religious sites in southern Italy. Drive the Aspromonte roads and stop in villages where the bar has been open since 1952 and hasn't changed." },
      { label: "Scilla", text: "The fishing village on the Strait of Messina with Sicily visible across the water. The old fishermen's quarter (Chianalea) built directly on the rocks — houses with boats moored at their front doors. Swordfish is caught here in the traditional way using long-boat fishing that hasn't changed in centuries. The most beautiful village in Calabria." },
    ],
    eat: [
      { name: "Nduja at source (Spilinga)", desc: "Spilinga is the town that invented nduja — the spreadable, fiery salami made from pork and Calabrian chili. Buy it directly from producers in the town market: La Rupa or Alimentari Bartolotta. Nothing sold anywhere outside Calabria tastes like this." },
      { name: "Ristorante Vecchia Tropea", desc: "The best restaurant in Tropea. The cipolla rossa (red onion) appears in everything — stuffed, caramelized, in the local pasta. The swordfish from the Strait is the other constant. Terrace looking over the sea." },
      { name: "Il Bergamotto (Reggio Calabria)", desc: "Calabria produces 95% of the world's bergamot — the citrus that flavors Earl Grey tea. This restaurant uses it in everything: bergamot pasta, bergamot granita, bergamot liqueur. Extraordinary." },
      { name: "Ristorante Scilla (Scilla)", desc: "Pesce spada (swordfish) caught by the lampara boats in the Strait and served on a terrace looking directly at Sicily. Grilled with local herbs, in pasta with bottarga, as carpaccio. The freshest fish you will eat in Italy." },
      { name: "Da Salvatore (Brancaleone)", desc: "A family restaurant in a small Ionian coast village that has been serving the same menu since 1961. Pasta with nduja, grilled local fish, Cirò wine. The owner's grandmother still makes the pasta. Cash only, no menu in English." },
    ],
    stay: [
      { name: "Capo Spartivento Lighthouse", tier: "High end", desc: "A converted lighthouse at the southernmost point of the Italian peninsula. Eight rooms, extraordinary isolation, surrounded by the sea on three sides. One of the most unusual hotel experiences in Italy." },
      { name: "Residenza il Barone (Tropea)", tier: "Mid range", desc: "Boutique hotel in a 17th-century palazzo in Tropea's historic center. Rooftop terrace with views over the sea, walking distance to the beach, the best mid-range option in the town." },
      { name: "Agriturismo rental (Aspromonte)", tier: "Good value", desc: "Rent a traditional Calabrian farmhouse in the mountains above the coast. Pigs, olive trees, nduja being made in the barn. Look through Agriturismo.it filtered by Calabria — prices are extraordinarily low by Italian standards." },,
      { name: "Palazzo del Corso (Tropea)", tier: "Mid range", desc: "A 17th-century noble palazzo in the historic centre of Tropea, converted to a boutique hotel. Rooftop terrace with the best view of the sea-cliff and the beach below. Walking distance to everything." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October. July–August Calabria gets extremely hot (38–42°C on the coasts) and Tropea becomes the one crowded place. The Ionian coast fills with Italian tourists in August — everyone else's August avoidance strategy means Calabria gets their overflow. June is the sweet spot: hot enough for the sea, empty enough to have the beaches to yourself." },
      { q: "Getting there", a: "Fly into Lamezia Terme (SUF) — the main regional airport with connections to Rome, Milan, and some European cities. Alternatively, fly into Reggio Calabria (REG) or Catanzaro Lamezia. From Naples, the high-speed train to Reggio Calabria takes 3.5 hours. Car is essential once you're there — Calabria has almost no useful public transport outside the main towns." },
      { q: "Getting around", a: "Rent a car at Lamezia airport and drive. The SS18 along the Tyrrhenian coast is beautiful and slow. The Aspromonte roads require confidence on mountain passes. The Ionian coast is flat and easy. Most of the best places (Scilla, Tropea, Aspromonte villages, Ionian archaeological sites) are impossible to reach on public transport. Fill up on petrol when you see a station — they're less frequent than you'd expect." },
      { q: "How long", a: "One week minimum to cover the two coasts and the interior properly. Days 1–2: Tyrrhenian coast — Tropea, Scilla. Day 3: Aspromonte drive, mountain villages. Day 4: Reggio Calabria (Riace Bronzes, strait views). Days 5–6: Ionian coast — Greek ruins, Cirò wine country, fishing villages. Day 7: slow departure. Calabria connects naturally with Sicily (ferry from Villa San Giovanni) and Matera (2 hours north)." },
      { q: "The attitude adjustment", a: "Calabria is southern Italy at its most southern — time moves differently, restaurants open when they open, service operates on its own clock. Embrace it. The people are extraordinarily hospitable to anyone who makes the effort to be there. Speak any Italian at all and the response is disproportionate warmth. Go without an itinerary and it will fill itself." },
      { q: "Money", a: "Calabria is the best value region in Italy by a significant margin. An agriturismo with dinner: €60–100. A good restaurant meal: €20–35 per person. Cirò wine at a local enoteca: €4–8 a glass. Capo Spartivento Lighthouse: €300–500. Residenza il Barone (Tropea): €80–150. Nduja direct from Spilinga: €8–15 a jar that would cost €30 in London. Go before anyone else figures this out." },
    ],
  },
];

// ─── LOGISTICS DATA ────────────────────────────────────────────────────────────
const portugalLogistics = [
  { q: "When to go", a: "May–June and September–October are the windows. Warm enough to swim, cool enough to walk all day. July–August the entire country fills with tourists and the heat in Alentejo and Algarve becomes serious (35–40°C). March–April is underrated — 20–25% cheaper, noticeably quieter, and the light on the Atlantic coast is extraordinary. For surf (Nazaré, Sagres), October through March is peak season." },
  { q: "Flying in", a: "Lisbon's Humberto Delgado Airport (LIS) is the main hub — well connected from the US (TAP, United, Delta direct from NYC, Boston, Newark) and throughout Europe. Porto's Francisco Sá Carneiro Airport (OPO) is worth considering if you're spending most of your time in the north. Both airports have direct metro connections to the city centers. Skip the expensive airport taxis — the metro is 20 minutes and €1.65." },
  { q: "Getting around", a: "Trains (CP — comboio.pt) connect Lisbon, Porto, Coimbra, and the Algarve reliably and cheaply. Lisbon to Porto is €25–35 and takes 3 hours. For the Douro Valley, Alentejo, Nazaré, Comporta, or anywhere rural, rent a car — Budget and Europcar are cheapest booked in advance. Driving is easy: highways are well-maintained, tolls are manageable (get a Via Verde transponder from the rental company). In Lisbon, use the metro (€1.65 flat) or walk — Ubers are cheap but traffic is brutal." },
  { q: "How long", a: "One week: Lisbon (4 nights) + either Porto (2 nights) or Alentejo (2 nights). Two weeks: Lisbon, Porto, Douro Valley, and Algarve without rushing. For Comporta or Nazaré, add 2 nights to either itinerary. A note: Lisbon rewards staying longer than you think. Four nights is the minimum to get past the surface." },
  { q: "Money", a: "Portugal is still genuinely good value. Expect €3–4 for a coffee and pastel de nata, €15–25 for a solid lunch with wine at a tasca, €40–60 at a good mid-range restaurant. Tipping: leave 5–10% at restaurants if the service was good — it's not expected but it's appreciated. Credit cards are widely accepted everywhere. ATMs (Multibanco) are everywhere and don't charge fees for most international cards." },
  { q: "Language", a: "Portuguese is not Spanish and the Portuguese are quietly proud of that. English is widely spoken in Lisbon, Porto, and anywhere with tourists. Outside the cities — Alentejo, Douro Valley, smaller Algarve towns — a few words go a long way: obrigado/obrigada (thank you, m/f), por favor (please), faz favor (excuse me / waiter), um café por favor (an espresso please). Google Translate works well offline for menus." },
  { q: "SIM card", a: "Buy a NOS or Vodafone prepaid SIM at the airport arrivals hall — €15 gets you 10GB of data that works everywhere in Portugal including the Algarve and islands. An EU SIM from home also works with no roaming charges if you have one." },
  { q: "The vibe", a: "Portuguese hospitality is quiet and genuine — nobody is performing for tourists. Restaurants don't rush you. Bars close when the last person leaves. People are genuinely helpful when you ask for directions. It's one of the least anxious countries in Europe to travel in, which is part of why people keep coming back." },
];

const italyLogistics = [
  { q: "When to go", a: "April–May and September–October are the sweet spots nationally. For the Dolomites: July–August for hiking, December–March for skiing. Sicily: March through November — summer is brutally hot (38–42°C) but the coast is magnificent and the sea is perfect. Puglia in September during olive harvest is the right call. Avoid Rome and Florence in July–August if you can — the crowds are genuinely miserable." },
  { q: "Flying in", a: "Rome Fiumicino (FCO) and Milan Malpensa (MXP) are the two main international hubs. FCO has direct US connections on most major carriers. For Southern Italy (Puglia, Sicily), fly into Bari (BRI), Brindisi (BDS), or Catania (CTA) — often cheaper and saves you 4+ hours of driving. For Sardinia, fly into Cagliari (CAG) or Olbia (OLB). For the Dolomites, fly into Venice (VCE) or Innsbruck (INN) and rent a car." },
  { q: "Getting around", a: "Trenitalia and Italo high-speed trains connect Rome, Florence, Milan, Naples, and Bologna fast and cheaply — book on trenitalia.com or italotreno.it at least 2 weeks out for best prices. For Sicily, Puglia, Tuscany, Sardinia, the Dolomites, and anywhere off the train lines: rent a car. The drives are often the experience (SS163 along the Amalfi, SP17 through the Dolomites). Download the Waze app — Italian roads require it. ZTL zones (restricted traffic areas in historic centers) will fine you if you drive into them with a rental car. Ask your hotel where to park." },
  { q: "How long", a: "Italy is too big to rush. One week: pick one region and go deep (all of Sicily, or Rome + Puglia, or Florence + Tuscany countryside). Two weeks: one major city as hub plus two distinct regions. If you try to do Rome, Florence, Puglia, and Sicily in ten days you will see everything and feel nothing. The slow version always wins." },
  { q: "The food rules", a: "Espresso standing at the bar costs less than at a table — always order at the bar if you can. Cappuccino is strictly a morning drink; after noon, order a caffè (espresso). The coperto (€1–3 bread/cover charge) is legal and normal — not a scam. Tipping is not expected but rounding up or leaving €2–5 is appreciated at a good restaurant. If the menu has pictures, leave. If it's written on a chalkboard, stay." },
  { q: "Money", a: "More expensive than Portugal but delivers value. A serious trattoria meal with wine: €35–60 per person. Mid-range hotels in major cities: €150–250. The south (Puglia, Sicily, Calabria) and islands are 20–30% cheaper than the north. Cash is still important — many smaller restaurants and agriturismi are cash only. Carry €50–100 in cash at all times." },
  { q: "Language", a: "Buongiorno (good morning until noon, then buonasera), grazie (thank you), per favore (please), un tavolo per due (a table for two), il conto per favore (the bill please) — that's most of what you need. Italian people respond very warmly to any attempt at the language. Outside of tourist cities, English is limited. Google Translate's camera function on menus is excellent and will save you from ordering things you didn't intend to." },
  { q: "SIM card", a: "Buy a TIM or WindTre prepaid SIM at any airport or tabaccheria (tobacco shop). €15–20 gets you 30–50GB valid for 30 days. Works throughout Italy including islands and mountains. An EU SIM from home works with no roaming charges if you have one." },
];

// ─── SPAIN REGIONS ────────────────────────────────────────────────────────────
const spainRegions = [
  {
    name: "San Sebastián", country: "spain", tag: "Food · Pintxos · Basque Country",
    hook: "More Michelin stars per capita than anywhere on earth. You probably haven't been.",
    img: "https://images.unsplash.com/photo-1558642452-9d2a7deb7f62?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")) s+=5; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("coast")||a[5]?.includes("cities")) s+=2; if(a[6]?.includes("eat")) s+=4; if(a[1]?.includes("partner")||a[1]?.includes("friends")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("eat")||a[9]?.includes("walk")) s+=3; if(a[8]?.includes("people")||a[8]?.includes("article")) s+=2; if(a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=2; if(a[6]?.includes("fullday")||a[6]?.includes("spontaneous")) s+=2; return s; },
    intro: "San Sebastián has more Michelin stars per capita than any city on earth except Kyoto. That fact alone should settle the argument about where to go in Spain. But it's not just the restaurants — it's the pintxos bars in the Parte Vieja where lunch costs €3 a bite and is better than most tasting menus, the bay that looks like it was designed for postcards, the surf beach at the edge of the old city. San Sebastián is the most complete food city in Europe.",
    highlights: [
      { label: "The Parte Vieja", text: "The old town. Every street is lined with pintxos bars — small plates displayed on the bar, eat standing up, pay at the end. Bar Nestor's tomato salad and tortilla are legendary. Bar Txepetxa does anchovies twenty ways. Go at 1pm and 8pm when the bars refresh." },
      { label: "La Concha beach", text: "The perfect urban beach — a crescent bay right next to the old town. Swim in the morning before the crowds, walk the promenade, eat pintxos. The combination of serious food city and beautiful beach is extremely rare." },
      { label: "Arzak and the three-stars", text: "Arzak has held three Michelin stars since 1989. Juan Mari and Elena Arzak are legends. Book six months ahead. Mugaritz, Akelarre, and Martín Berasategui are the other three-star options — all within driving distance." },
      { label: "Txakoli wine", text: "The local slightly sparkling white wine, poured from height to aerate it. Crisp, low-alcohol, goes with everything. Order a glass at every pintxos bar. Buy bottles to take home — it travels well and costs €8 locally." },
    ],
    eat: [
      { name: "Bar Nestor", desc: "The most famous bar in San Sebastián for one reason: the tortilla. Made twice a day, sells out in minutes. Arrive at 12:45pm or 7:45pm and join the queue. The tomato salad is equally serious." },
      { name: "Bar Txepetxa", desc: "Anchovy specialists in the Parte Vieja. Every pintxo involves anchovies in some form — with truffle, with sea urchin, with peppers. The best anchovies you've ever eaten. €2–3 each." },
      { name: "Arzak", desc: "Three Michelin stars, family-run since 1897. Elena Arzak is one of the best chefs in the world. The tasting menu is €250+ but represents genuine gastronomic history. Book six months ahead." },
      { name: "La Cuchara de San Telmo", desc: "The best pintxos bar in the city for hot pintxos — dishes cooked to order rather than displayed on the bar. The foie with apple, the slow-cooked veal cheek. Small, always crowded, worth the wait." },
      { name: "Borda Berri", desc: "Tiny bar, extraordinary pintxos. The risotto de idiazabal (smoked Basque cheese) and the braised pig cheek are the ones. Get there early, the best stuff goes fast." },
    ],
    stay: [
      { name: "Hotel Maria Cristina", tier: "High end", desc: "The grand belle époque hotel on the river. Where the film festival crowd stays. Beautiful rooms, excellent breakfast, five-minute walk to the Parte Vieja." },
      { name: "Zenit San Sebastián", tier: "Mid range", desc: "Clean, well-run, good location near the beach. No frills but everything works. The best honest mid-range option in the city." },
      { name: "Parte Vieja Apartments", tier: "Good value", desc: "Staying in the old town means pintxos bars are your kitchen. Search Airbnb for 'Parte Vieja' — apartments in the old streets above the bars are the right call." },,
      { name: "Pensión Edorta (Old Town)", tier: "Good value", desc: "A small guesthouse in the Parte Vieja — simple rooms, excellent location, walking distance to every pintxos bar in the old town. The classic San Sebastián base for people who are there to eat, not to be seen at a hotel." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October. The Basque Country is green year-round because it rains — that's why the landscape is so beautiful. July–August is peak season and the city fills but never feels as overrun as Barcelona. The San Sebastián Film Festival in late September is worth planning around." },
      { q: "Getting there", a: "San Sebastián Airport (EAS) has limited connections — fly into Bilbao (BIO, 1 hour by bus) or Biarritz (BIQ, 30 minutes, France) for the best options. From Madrid it's a 5-hour drive or 5.5-hour train. From Barcelona it's 6 hours by train. The Bilbao bus (PESA) runs every hour and costs €17." },
      { q: "Getting around", a: "The city is completely walkable. The Parte Vieja, La Concha beach, the Gros neighborhood, and the market are all within 20 minutes on foot. For the three-star restaurants (Arzak, Mugaritz, Akelarre), take a taxi — they're in the hills outside the center." },
      { q: "How long", a: "Three nights minimum. Anything less and you won't get through the pintxos bars properly. Day one: Parte Vieja circuit at lunch and dinner. Day two: La Concha morning swim, Mercado de la Bretxa, Michelin dinner. Day three: day trip to Biarritz (30 min) or the Rioja Alavesa wine country (1 hour). Four nights if you're serious about the food." },
      { q: "Pintxos rules", a: "Go at peak hours — 1–3pm for lunch, 8–10pm for dinner. The best bars refresh their pintxos at these times. Grab a plate, point at what you want, eat standing up, tell the bartender what you had at the end. A full pintxos lunch with txakoli: €15–25. Don't sit down unless you're at a restaurant — standing at the bar is the experience." },
      { q: "Money", a: "San Sebastián is mid-range to expensive by Spanish standards. Pintxos: €2–4 each. Txakoli by the glass: €3–4. A serious dinner at a non-Michelin restaurant: €50–80. The three-star tasting menus run €200–300. Hotel Maria Cristina: €300–600. Mid-range hotels: €120–200. The pintxos culture means you can eat extraordinarily well for €30 a day if you do it right." },
    ],
  },
  {
    name: "Barcelona", country: "spain", tag: "Architecture · Food · Energy",
    hook: "Everyone knows Barcelona. Almost nobody finds the city underneath the tourism layer.",
    img: "https://images.unsplash.com/photo-1539037116277-4db20889f2d4?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=2; if(a[3]?.includes("balanced")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("cities")||a[5]?.includes("coast")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("absorb")) s+=2; if(a[1]?.includes("friends")||a[1]?.includes("partner")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=1; if(a[9]?.includes("walk")||a[9]?.includes("plan")) s+=2; if(a[8]?.includes("deep")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")) s-=1; return s; },
    intro: "Barcelona is one of the great cities of the world and everyone knows it, which is the problem. The key is going beyond the Gaudí circuit and the Ramblas and finding the city that actually exists underneath the tourism layer: the Eixample neighborhood's modernista buildings, the Boqueria at 7am before the tour groups, the Barceloneta fishermen's quarter at lunch, the craft cocktail bars of the Raval. Barcelona rewards people who look slightly sideways.",
    highlights: [
      { label: "Sagrada Família — book ahead", text: "Gaudí's unfinished basilica is genuinely one of the most extraordinary buildings ever conceived. Book tickets online well in advance and add the tower access. Go early morning when the light comes through the stained glass on the eastern facade. It's impossible to be unimpressed." },
      { label: "El Born and Sant Pere", text: "The neighborhoods the locals actually use. Medieval streets, some of the best restaurants and bars in the city, the Palau de la Música (book a concert), the Basílica de Santa Maria del Mar which is more beautiful than the cathedral. Base yourself here." },
      { label: "Mercat de Santa Caterina", text: "The local alternative to the Boqueria — same extraordinary produce, no tourists, no overpriced smoothies. The mosaic tiled roof is extraordinary. Go for breakfast and lunch ingredients." },
      { label: "Montjuïc at sunset", text: "The hill above the city. Take the cable car up, walk through the gardens, watch the sun go down over the port. The view of the city from the Castell de Montjuïc is the one that goes in your memory." },
    ],
    eat: [
      { name: "Bar del Pla", desc: "The best casual restaurant in El Born. Catalan classics — croquetes, escalivada, cod with honey — done properly. Always busy, worth the wait. Go for lunch." },
      { name: "Bodega Sepúlveda", desc: "Old-school Catalan wine bar in the Eixample. Natural wines, excellent cheese and charcuterie, the kind of place that has been here forever and will be here forever. Lunch only." },
      { name: "Tickets", desc: "Albert Adrià's tapas bar — the most fun restaurant in the city. Playful, creative, genuinely exciting food. Book weeks ahead online or line up at opening for walk-in spots." },
      { name: "Cervecería Catalana", desc: "The perfect neighborhood bar on Carrer Mallorca. Patatas bravas, croquetes, the best pan con tomate in the city. Queue starts at 1pm — arrive early or go at 8pm." },
      { name: "La Cova Fumada", desc: "The original bombas (meat and potato croquettes) were invented here in 1945. Cash only, no menu in English, opens at 9am for breakfast, closes when it sells out. Barceloneta neighborhood." },
    ],
    stay: [
      { name: "Hotel Arts Barcelona", tier: "High end", desc: "Frank Gehry's fish sculpture outside, Ritz-Carlton inside. On the Barceloneta beachfront. The most glamorous hotel in the city." },
      { name: "Hotel Praktik Rambla", tier: "Mid range", desc: "Modernista building on the Rambla de Catalunya (the good Rambla). Well-designed rooms, good location for the Eixample and El Born. Excellent value for Barcelona." },
      { name: "El Born Apartments", tier: "Good value", desc: "Staying in El Born puts you in the best neighborhood. Medieval streets, great restaurants, walking distance to everything. Search Airbnb filtered by El Born or Sant Pere." },,
      { name: "Hotel Neri (Gothic Quarter)", tier: "Mid range", desc: "A medieval palace in the Gothic Quarter converted into a boutique hotel. Stone walls, rooftop terrace, the sound of the old city outside the window. The alternative to the Eixample design hotels." },
    ],
    logistics: [
      { q: "When to go", a: "April–May and September–October. June is excellent. July–August the city is at maximum capacity — the beaches are crowded, the tourist infrastructure strains, and prices peak. The weather is good almost year-round; January–February is quiet, cheap, and pleasant." },
      { q: "Getting there", a: "Barcelona El Prat (BCN) is well connected from the US and all of Europe. The Aerobus runs to Plaça Catalunya in 35 minutes (€6.75). The train (Rodalies R2 Nord) is slower but cheaper (€5). From Madrid, the AVE high-speed train takes 2.5 hours (€30–80 booked ahead) — significantly better than flying." },
      { q: "Getting around", a: "Metro is excellent and covers everything (T-Casual 10-trip card: €12.15). Walking is the best option in the Gothic Quarter, El Born, and Barceloneta. Taxi and Uber work well for Montjuïc and the hills. Avoid renting a car in the city — parking is impossible and unnecessary." },
      { q: "How long", a: "Four nights minimum. Day one: Sagrada Família, Eixample exploration. Day two: El Born, Mercat de Santa Caterina, Barceloneta lunch. Day three: Montjuïc, Poble Sec, Tickets dinner. Day four: Gràcia neighborhood, Park Güell, slow departure. Barcelona is inexhaustible — a week goes quickly." },
      { q: "Money", a: "Barcelona is the most expensive city in Spain. Café amb llet at a neighborhood bar: €1.80. Lunch menu del día (3 courses with wine): €12–15. Dinner at a serious restaurant: €50–80 per person. Hotel Arts: €400–900. Mid-range hotels: €150–250. Tourist trap warning: any restaurant directly on Las Ramblas is overpriced — walk one block in either direction." },
      { q: "Neighborhoods", a: "Stay in El Born, Eixample, or Gràcia — not the Gothic Quarter (overrun) or Barceloneta (noisy). El Born has the best restaurant density. Eixample has the best architecture walking. Gràcia has the most local feel. All are connected by metro in under 15 minutes." },
    ],
  },
  {
    name: "Madrid", country: "spain", tag: "Art · Nightlife · Food Markets",
    hook: "Madrid runs 3 hours later than the rest of Europe. Adjust your clock or miss everything.",
    img: "https://images.unsplash.com/photo-1558370781-d6196591e1f3?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=3; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=2; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("cities")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("absorb")) s+=2; if(a[1]?.includes("friends")||a[1]?.includes("solo")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("connection")||a[8]?.includes("surprise")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("sit")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("none")) s+=1; if(a[9]?.includes("tourist")) s+=1; return s; },
    intro: "Madrid doesn't try to seduce you the way Barcelona does. It's a serious, proud, slightly difficult city that reveals itself slowly — and once it does, it tends to become the Spanish city people prefer. The Prado alone is worth the trip. But the real Madrid is the Mercado de San Miguel at midnight, the rooftop bars of the Malasaña neighborhood, the jamón ibérico at a century-old taberna, the verbenas (street festivals) that turn entire neighborhoods into outdoor parties. Madrid runs at a different clock than everywhere else in Europe.",
    highlights: [
      { label: "The Prado", text: "One of the great art museums of the world. Velázquez, Goya, El Greco, Bosch — the collection is staggering. Go when it opens at 10am, allow three hours minimum. The Goya black paintings in the basement are the most haunting rooms in any museum in Europe." },
      { label: "Malasaña and Chueca", text: "The neighborhoods that make Madrid interesting. Malasaña is 1980s-revival bars, record shops, vermouth at noon. Chueca is the design and food destination — better restaurants per block than anywhere else in Madrid." },
      { label: "Mercado de San Miguel", text: "The glass and iron market near the Plaza Mayor. Open until midnight, all tapas and wine. The jamón ibérico de bellota (acorn-fed Iberian ham) counter is the main event. Go late when the after-dinner crowd arrives." },
      { label: "El Rastro Sunday market", text: "The largest flea market in Europe, every Sunday in La Latina. Antiques, vintage clothes, junk, and some genuinely good finds. The vermouth bars around it open at 11am. Start here and spend Sunday morning in La Latina." },
    ],
    eat: [
      { name: "Sobrino de Botín", desc: "The oldest restaurant in the world, according to the Guinness Book. Opened in 1725. The cochinillo asado (roast suckling pig) and cordero asado (roast lamb) are cooked in the original 18th-century wood-fired oven. Book ahead. Tourist? Yes. Worth it? Absolutely." },
      { name: "Casa Lucio", desc: "La Latina institution. The huevos rotos (fried eggs broken over jamón and potatoes) are Madrid's defining dish. The King of Spain eats here. Book ahead — it's been full for 40 years." },
      { name: "Mercado de Vallehermoso", desc: "The locals' alternative to San Miguel. Excellent produce stalls, good tapas bars, a fraction of the tourist density. Chamberí neighborhood, worth the extra 10-minute walk." },
      { name: "DiverXO", desc: "David Muñoz's three-Michelin-star restaurant — the most avant-garde and exciting in Spain. Rock music, theatrical plating, genuinely boundary-pushing food. Book months ahead. One of the great restaurant experiences in Europe." },
      { name: "Bar Cock", desc: "Madrid's oldest cocktail bar, open since 1921. The bartenders have worked there for decades. No cocktail list — tell them what you like and they make something. The Dry Martini is the benchmark." },
    ],
    stay: [
      { name: "Hotel Urso", tier: "High end", desc: "Boutique hotel in a 19th-century palace in the Alonso Martínez neighborhood. One of the most beautiful hotels in Spain — vaulted ceilings, original stonework, excellent restaurant." },
      { name: "Hotel Praktik Metropol", tier: "Mid range", desc: "Right on Gran Vía, Art Deco building. Well-run, good rooms, rooftop terrace with views of the city. The best mid-range option for the central neighborhoods." },
      { name: "Malasaña Apartments", tier: "Good value", desc: "Staying in Malasaña puts you in the best neighborhood for nightlife and the local bar scene. Search Airbnb filtered by Malasaña — large apartments with terraces are good value." },,
      { name: "Posada del León de Oro (La Latina)", tier: "Good value", desc: "A converted 19th-century posada in the La Latina neighbourhood. Seventeen rooms, original stone and brick, the Sunday El Rastro market right outside. Madrid's most characterful mid-range option." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October. Madrid summers are brutal — 38–42°C in July–August and the city empties as Madrileños leave for the coast. The spring and autumn are perfect: warm, culturally alive, manageable crowds. December is excellent for the Christmas markets around the Plaza Mayor." },
      { q: "Getting there", a: "Madrid Barajas (MAD) is one of Europe's major hubs with extensive US connections. Metro line 8 runs from the airport to Sol and Nuevos Ministerios in 13–25 minutes (€5 with supplement). From Barcelona, the AVE high-speed train (2.5 hours, €30–80 booked ahead) is almost always better than flying." },
      { q: "Getting around", a: "The Metro is excellent and covers the entire city (10-trip card: €12.20). The city center is walkable between the Prado, Retiro park, Sol, and La Latina. Taxis are cheap by European standards. Night buses (búhos) run all night when the Metro closes at 1:30am — important because Madrid doesn't sleep until 4am." },
      { q: "How long", a: "Three nights minimum, four is better. Day one: Prado (half day), La Latina tapas circuit. Day two: Malasaña and Chueca exploring, Mercado de San Miguel at night. Day three: Retiro park, Reina Sofía (Guernica is here), rooftop bar at sunset. Day four: El Rastro Sunday market, slow departure. Madrid rewards unhurried exploration." },
      { q: "The Madrid clock", a: "Madrid runs 2–3 hours later than the rest of Europe. Lunch starts at 2:30pm and goes until 4:30pm. Dinner doesn't start until 9:30–10pm. Nightlife doesn't begin until midnight. If you arrive and eat dinner at 7:30pm, you'll be eating alone in an empty restaurant. Adjust your schedule or you'll miss everything." },
      { q: "Money", a: "Madrid is good value by European capital standards. Coffee at a neighborhood bar: €1.50. Menu del día (3-course lunch with wine): €12–18. Tapas dinner with wine: €30–50 per person. DiverXO tasting menu: €250+. Hotel Urso: €250–450. Mid-range hotels: €120–200. Malasaña apartments: €100–180 per night." },
    ],
  },
  {
    name: "Andalusia", country: "spain", tag: "Flamenco · Alhambra · White Villages",
    hook: "The Alhambra at dawn is one of the most beautiful things you will ever see.",
    img: "https://images.unsplash.com/photo-1538928027697-21c088e4e987?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("cities")||a[5]?.includes("countryside")) s+=2; if(a[6]?.includes("wander")||a[6]?.includes("absorb")) s+=2; if(a[2]?.includes("week")||a[2]?.includes("twoweeks")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("budget")) s+=1; if(a[8]?.includes("beauty")||a[8]?.includes("surprise")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("people")) s+=2; if(a[9]?.includes("rushed")||a[9]?.includes("generic")) s+=2; return s; },
    intro: "Andalusia is the Spain of imagination — flamenco, sherry, the Alhambra palace, white villages on hilltops, orange trees in church courtyards. It's also genuinely extraordinary in ways that photographs can't prepare you for. The Alhambra at dawn is one of the most beautiful things you will ever see. The tapas culture in Granada (free with every drink) is unlike anywhere else in Spain. The Jerez sherry bodegas produce wines that changed the world and remain almost unknown. Rent a car and drive through the pueblos blancos. You'll understand why people never leave.",
    highlights: [
      { label: "The Alhambra (Granada)", text: "Book as far in advance as possible — tickets sell out weeks ahead. The Nasrid Palaces are the reason: rooms of carved stucco, geometric tile work, water channels that run through the floors. The Generalife gardens above are extraordinary. Go for the first morning entry slot at 8:30am." },
      { label: "Seville's Barrio Santa Cruz", text: "The old Jewish quarter. Orange-tree-lined streets, hidden courtyards, the best tapas bars in the city. The Real Alcázar (book ahead) is a Moorish palace still used by the Spanish royal family. More beautiful than its own photographs." },
      { label: "The pueblos blancos", text: "The white villages of the Cádiz and Málaga hinterland — Ronda, Grazalema, Zahara de la Sierra, Vejer de la Frontera. Drive the route between them over two days. Each village looks like the last one except completely different. The mountain road between Ronda and Grazalema is extraordinary." },
      { label: "Jerez de la Frontera", text: "The sherry capital. González Byass, Lustau, and Tío Pepe do cellar tours and tastings. The fino and manzanilla sherries are some of the most complex wines in the world and cost almost nothing locally. The flamenco tradition here (Jerez style) is different from Seville — rougher, more intense." },
    ],
    eat: [
      { name: "El Churrasco (Córdoba)", desc: "The benchmark Córdoban restaurant. Rabo de toro (oxtail stew), salmorejo (cold tomato soup), flamenquín (fried pork roll). The wine cellar in the old city wall is extraordinary." },
      { name: "Bar Las Teresas (Seville)", desc: "The most atmospheric tapas bar in the Barrio Santa Cruz. Jamón hanging from the ceiling, sherry by the glass, gambas al ajillo (garlic prawns). Standing room only." },
      { name: "Tragabuches (Ronda)", desc: "Modern Andalusian cuisine in a beautiful town. Dani García trained here. The rabo de toro and the gazpacho de cerezas (cherry gazpacho) are the dishes." },
      { name: "La Yedra (Vejer de la Frontera)", desc: "Rooftop terrace restaurant in the most beautiful village in Andalusia. Atún rojo (bluefin tuna from Barbate) is the local specialty. The view from the terrace is extraordinary." },
      { name: "González Byass (Jerez)", desc: "Not a restaurant but unmissable — the Tío Pepe bodega tour ends with a serious tasting of fino, amontillado, and oloroso sherries. Book ahead. The 19th-century cathedral-scale cellars are stunning." },
    ],
    stay: [
      { name: "Parador de Granada", tier: "High end", desc: "Inside the Alhambra complex itself — a converted 15th-century convent. The only hotel where you can walk to the Nasrid Palaces at night after all the day visitors leave. Book six months ahead." },
      { name: "Hotel Casa 1800 (Seville)", tier: "Mid range", desc: "Boutique hotel in the Barrio Santa Cruz in a 19th-century palace. Rooftop terrace with views over the city, excellent breakfast, walking distance to everything." },
      { name: "Cortijo Rental (Pueblos Blancos)", tier: "Good value", desc: "Rent a traditional whitewashed farmhouse in the hills between Ronda and Grazalema. A week in a cortijo with a pool and a view of the mountains is the Andalusia experience." },,
      { name: "Hacienda de San Rafael (Las Cabezas)", tier: "High end", desc: "A working olive farm between Seville and Jerez converted into a ten-room country house. Horseback rides through the olive grove, a pool in the orchard, dinners of Andalusian ingredients. The definitive rural Andalusia stay." },
    ],
    logistics: [
      { q: "When to go", a: "March–May and September–November. Spring brings the azahar (orange blossom) scent across Seville and the landscape is green. April is Semana Santa (Holy Week) — extraordinary processions but accommodation books out a year ahead. July–August in Seville and Córdoba is 42–45°C and genuinely hostile. The coast (Cádiz, Tarifa) stays cooler with Atlantic winds." },
      { q: "Getting there", a: "Fly into Seville (SVQ) or Málaga (AGP) for the best access. Málaga is the largest airport with the most connections. High-speed AVE trains connect Madrid to Seville (2.5 hours) and Málaga (2.5 hours) — often the best option from Madrid. Granada airport is small but has some connections; otherwise train or bus from Málaga (1.5 hours)." },
      { q: "Getting around", a: "Car is essential for the pueblos blancos and the Cádiz coast. Seville, Granada, and Córdoba are all walkable once you're there. The train connects the major cities efficiently. For a complete Andalusia trip: fly into Málaga, pick up a car, drive the pueblos blancos circuit, end in Seville or Granada. Return flight from either." },
      { q: "How long", a: "One week minimum for the highlights. Days 1–2: Granada and the Alhambra. Day 3: drive to Ronda and the pueblos blancos. Days 4–5: Seville (Real Alcázar, Santa Cruz tapas circuit, flamenco show). Day 6: Jerez bodega tour and sherry tasting. Day 7: Cádiz coastal drive, departure. Two weeks allows Córdoba (the Mezquita is extraordinary) and the full coast." },
      { q: "The Alhambra", a: "Book Alhambra tickets at alhambra-tickets.es as soon as your dates are confirmed — they routinely sell out 3–4 weeks ahead in peak season. The Nasrid Palaces slot is the critical one (timed entry). The ticket also includes the Alcazaba fortress and Generalife gardens which don't require a time slot. If you miss the advance booking, try the official website at 8am two days before your visit when any returned tickets go back on sale." },
      { q: "Money", a: "Andalusia is among the best value regions in Spain. Tapas in Granada are still largely free with drinks — a custom that has almost disappeared elsewhere. A full tapas dinner with wine: €20–35 per person. The Parador de Granada runs €250–500 but includes the extraordinary location. Mid-range hotels in Seville: €100–200. Cortijo rentals: €150–350 per night." },
    ],
  },
  {
    name: "Valencia", country: "spain", tag: "Paella · Design · Underrated",
    hook: "Valencia invented paella and has been unfairly overlooked by everyone since.",
    img: "https://images.unsplash.com/photo-1583422409516-2895a77efced?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("culture")) s+=3; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=3; if(a[5]?.includes("cities")||a[5]?.includes("coast")) s+=2; if(a[6]?.includes("eat")||a[6]?.includes("wander")) s+=2; if(a[2]?.includes("short")||a[2]?.includes("week")) s+=2; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("connection")) s+=2; if(a[9]?.includes("eat")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=2; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")) s+=2; return s; },
    intro: "Valencia invented paella and has been unfairly overshadowed by Barcelona and Madrid ever since. It's Spain's third-largest city, genuinely beautiful, with a historic center that rivals any in the country, a converted riverbed (the Turia gardens) that is the longest urban park in Europe, and the most extraordinary contemporary architecture complex in Spain — the City of Arts and Sciences. The food is outstanding, the beaches are 20 minutes from the center, and it costs significantly less than either of the cities that overshadow it.",
    highlights: [
      { label: "Real paella", text: "Paella Valenciana is rice with chicken, rabbit, and green beans — not seafood. That's a different dish. Eat the real thing at a restaurant in the Albufera lagoon south of the city, where the rice is grown. La Pepica on the beach has been making it since 1898." },
      { label: "La Lonja de la Seda", text: "The 15th-century silk exchange — a UNESCO World Heritage masterpiece of Gothic civil architecture. One of the most beautiful buildings in Spain and almost always empty. The twisted stone columns in the main hall are extraordinary." },
      { label: "City of Arts and Sciences", text: "Santiago Calatrava's futuristic complex at the eastern end of the Turia gardens. The Hemisfèric, Museo de las Ciencias, and L'Oceanogràfic (Europe's largest aquarium) are the main buildings. Best seen at night when the light reflects in the lagoon pools." },
      { label: "Mercado Central", text: "The largest fresh produce market in Europe, under a spectacular Art Nouveau dome. Open Monday–Saturday mornings. Buy ingredients, eat at the stalls, watch the city feed itself. Arrive at 9am before it fills." },
    ],
    eat: [
      { name: "La Pepica", desc: "Valencian institution on the Malvarrosa beach since 1898. Hemingway ate here. The paella Valenciana is the definitive version — rice, chicken, rabbit, green beans, cooked over a wood fire. Lunch only, book ahead." },
      { name: "Riff", desc: "The most serious restaurant in Valencia. Bernd Knöller's creative Valencian cuisine with one Michelin star. The tasting menu changes with what's seasonal from the local market. Book ahead." },
      { name: "Bar Pilar", desc: "The best clóchinas (local mussels, smaller and sweeter than Atlantic mussels) and tigres (mussels in spiced sauce) in Valencia. Order a horchata (tiger nut milk) alongside. Standing only, always busy." },
      { name: "Bodega Casa Montaña", desc: "150-year-old wine bar in the Cabanyal neighborhood near the beach. Old wooden barrels, remarkable wine list of old Spanish bottles, exceptional charcuterie and tinned fish. One of the great bar experiences in Spain." },
      { name: "Mercado Central stalls", desc: "The market stalls inside serve breakfast and lunch. The jamón stalls, the olive bar, the fresh horchata at the horchata stalls near the entrance. Eat here at 10am for the best market breakfast in Spain." },
    ],
    stay: [
      { name: "The Westin Valencia", tier: "High end", desc: "Belle époque palace in the city center. Rooftop pool with views of the old city, excellent restaurant, walking distance to the cathedral and Mercado Central." },
      { name: "Hotel Casual Valencia del Cine", tier: "Mid range", desc: "Boutique hotel in the historic center, cinema-themed design, good rooms and great location. The best value mid-range option in the city center." },
      { name: "El Cabanyal Apartments", tier: "Good value", desc: "The historic fishermen's neighborhood near the beach, recently revitalized. Staying here puts you close to the Malvarrosa beach and the best wine bars. Search Airbnb filtered by Cabanyal." },,
      { name: "Casa Dona Urraca (El Carmen)", tier: "Good value", desc: "A restored medieval house in the El Carmen district — the oldest neighbourhood in Valencia. Exposed stone walls, a rooftop terrace, five rooms. Walking distance to the Central Market and the best horchata in the city." },
    ],
    logistics: [
      { q: "When to go", a: "March–June and September–November. Valencia is warm year-round — even January rarely drops below 12°C. The one time to absolutely be here is March 15–19 for Las Fallas — the most spectacular street festival in Europe: giant papier-mâché sculptures throughout the city, fireworks at 2pm daily, the whole city on fire on the final night. Book accommodation a year ahead for Fallas." },
      { q: "Getting there", a: "Valencia Airport (VLC) has good European connections and some US charters in summer. From Madrid, the AVE high-speed train takes 1.5 hours (€15–40 booked ahead) — much better than flying. From Barcelona, the train takes 3.5 hours. The airport is 20 minutes from the city center by metro (line 3 or 5, €4.90)." },
      { q: "Getting around", a: "Valencia is a cycling city — flat, with excellent bike lanes throughout. Valenbisi (the public bike share) costs €2/week for unlimited 30-minute rides. Metro and tram cover everything else. Walking is fine for the historic center. The beach (Malvarrosa) is a 20-minute tram ride from the center." },
      { q: "How long", a: "Three nights is perfect. Day one: Mercado Central, La Lonja, El Carmen neighborhood. Day two: City of Arts and Sciences, Turia gardens walk, Cabanyal and beach. Day three: Albufera lagoon (30 minutes south), real paella lunch, departure. Valencia also makes an excellent base for day trips to the Costa Blanca (Alicante, Altea, Dénia)." },
      { q: "Money", a: "Valencia is significantly cheaper than Madrid and Barcelona. Coffee: €1.30. Menu del día: €12–15. Paella lunch at La Pepica: €25–35 per person. Dinner at Riff: €80–100. Westin Valencia: €180–350. Mid-range hotels: €80–150. The best value major city in Spain." },
      { q: "Horchata", a: "Horchata de chufa (tiger nut milk) is Valencia's other great contribution to the world alongside paella. It's a cold, slightly sweet, milky drink made from tiger nuts grown in the Huerta Valenciana. The correct way to drink it: with fartons (elongated soft pastries for dipping). Horchatería Santa Catalina in the old town has been making it since 1836." },
    ],
  },
  {
    name: "Mallorca", country: "spain", tag: "Coast · Tramuntana · Hidden Coves",
    hook: "Rent a car and go northwest. Most tourists never discover it exists.",
    img: "https://images.unsplash.com/photo-1570077188670-e3a8d69ac5ff?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("adventure")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("luxury")) s+=2; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("coast")) s+=3; if(a[5]?.includes("mountains")) s+=1; if(a[6]?.includes("explore")||a[6]?.includes("wander")) s+=3; if(a[1]?.includes("partner")||a[1]?.includes("friends")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("freedom")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("sit")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("generic")||a[9]?.includes("badsleep")) s+=1; return s; },
    intro: "Mallorca's reputation as a package holiday destination is both earned and completely misleading. The north and west of the island — the Serra de Tramuntana mountain range, the cove-dotted northwest coast, the medieval hilltop villages of the interior — is one of the most beautiful landscapes in the Mediterranean and sees a fraction of the tourists who fly in for the south coast resorts. The trick is renting a car and going the other way from the airport.",
    highlights: [
      { label: "Serra de Tramuntana", text: "The UNESCO-listed mountain range running along the northwest coast. Drive the MA-10 from Andratx to Pollença — one of the great coastal mountain drives in Europe. Villages like Valldemossa, Deià, and Sóller are built into the cliffs above the sea." },
      { label: "Deià", text: "The hilltop village where Robert Graves lived and wrote. Artists and writers have been coming here for a century. The rocky cove (Cala Deià) below the village is one of the most beautiful swimming spots in the Mediterranean." },
      { label: "Cap de Formentor", text: "The northern tip of the island — a narrow peninsula of cliff roads and pine forests above the sea. The lighthouse at the end looks out over water that goes all the way to France. Drive at sunrise or sunset." },
      { label: "Palma old city", text: "The capital is genuinely beautiful. The Gothic cathedral (La Seu) looming over the sea, the Arab baths, the Mercat de l'Olivar, the cocktail bars of the Santa Catalina neighborhood. Most tourists miss the city entirely and go straight to the resorts." },
    ],
    eat: [
      { name: "Ca Na Toneta (Caimari)", desc: "The most celebrated restaurant in Mallorca — two sisters cooking traditional Mallorcan food from their family's farm. In a village in the Tramuntana hills. Book months ahead. One of the great rural restaurant experiences in Spain." },
      { name: "Simply Fosh (Palma)", desc: "Marc Fosh's one-Michelin-star restaurant in a beautiful 16th-century convent. Modern Mediterranean cooking at its most refined. The lunch menu is exceptional value." },
      { name: "Sa Llotja (Palma)", desc: "Fish and rice restaurant in Palma's Santa Catalina market neighborhood. The arròs brut (Mallorcan 'dirty rice' with meat and vegetables) is the dish." },
      { name: "El Barrigón de Xesc (Fornalutx)", desc: "Village restaurant in one of the most beautiful villages in the Tramuntana. Traditional mallorquín cooking — tumbet (vegetable ratatouille), roast lamb, excellent local wines. Book ahead." },
      { name: "Mercat de l'Olivar (Palma)", desc: "Palma's covered market — the fish and produce halls are extraordinary. The tapas bars inside open at 8am. Go for the sobrasada (soft spiced sausage), the ensaïmada pastry, and the local Mallorcan wines." },
    ],
    stay: [
      { name: "Belmond La Residencia (Deià)", tier: "High end", desc: "The benchmark luxury hotel in Mallorca. In Deià on the clifftop above the sea, two pools, excellent restaurant, the most beautiful hotel setting on the island." },
      { name: "Ca'n Reus (Fornalutx)", tier: "Mid range", desc: "Small converted manor house in the Tramuntana village of Fornalutx. Stone floors, mountain views, excellent breakfast. The best mid-range option in the mountains." },
      { name: "Finca rental (Interior Mallorca)", tier: "Good value", desc: "Rent a traditional stone farmhouse with a pool in the interior for a week. Significantly cheaper than the coast and more beautiful. Search through Mallorcan Farmhouses or Airbnb filtered by Tramuntana." },,
      { name: "Son Brull Hotel (Pollença)", tier: "High end", desc: "A converted 18th-century Jesuit monastery in the Serra de Tramuntana. Olive trees, a natural pool fed by spring water, one of the best restaurants on the island. The serious Mallorca alternative to the beach hotels." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October. July–August the south coast resorts are at maximum capacity and the roads to the popular coves are gridlocked. The Tramuntana and the northwest coast are manageable year-round — even winter is mild (15–18°C) and the mountain villages are at their most peaceful October–April." },
      { q: "Getting there", a: "Palma de Mallorca Airport (PMI) is one of the busiest in Europe in summer — excellent connections from most European cities. Direct US flights are limited; connect through Madrid or Barcelona. From Barcelona the ferry takes 7–8 hours (overnight option available — worth it for the experience). Domestic flights from Madrid take 45 minutes." },
      { q: "Getting around", a: "Car is essential for anything beyond Palma. Rent at the airport and head northwest immediately — the MA-10 along the Serra de Tramuntana is the road you came for. The south coast resorts are accessible but not the point. Palma itself is walkable. In summer, some cove roads have access restrictions — check ahead and consider the 30-minute walk in from the restricted zone." },
      { q: "How long", a: "Five to seven days. Days 1–2: Palma (cathedral, Mercat de l'Olivar, Santa Catalina). Day 3: Drive the MA-10, Valldemossa and Deià. Days 4–5: Base in Deià or Sóller, explore the northwest coves. Day 6: Cap de Formentor and Pollença. Day 7: slow return to Palma." },
      { q: "The two Mallorcas", a: "The south and east coasts are resort Spain — busy, English-friendly, good for beaches and nightlife. The northwest (Tramuntana, Deià, Sóller, Fornalutx) is completely different — one of the most beautiful landscapes in Europe, excellent food, genuinely authentic villages. Most people who fly in never discover the northwest exists. Go northwest." },
      { q: "Money", a: "Mallorca ranges enormously. South coast resorts are affordable (package deals, all-inclusive). The northwest is moderate to expensive. Belmond La Residencia runs €500–1,200. Mid-range mountain hotels: €150–300. Finca rentals in the interior: €200–500 per night for a whole property. Dinner at Ca Na Toneta: €80–100 per person. Palma tapas: €30–50 per person." },
    ],
  },
  {
    name: "Galicia", country: "spain", tag: "Seafood · Pilgrimage · Green Coast",
    hook: "The Spain nobody expects. Green hills, the best shellfish in Europe, and a thousand-year pilgrimage route.",
    img: "https://images.unsplash.com/photo-1596394516093-501ba68a0ba6?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=3; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=2; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("explore")) s+=2; if(a[2]?.includes("week")||a[2]?.includes("twoweeks")) s+=2; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("connection")) s+=2; if(a[9]?.includes("walk")||a[9]?.includes("eat")) s+=2; if(a[8]?.includes("none")||a[8]?.includes("people")) s+=2; if(a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=3; if(a[6]?.includes("spontaneous")||a[6]?.includes("physical")) s+=2; return s; },
    intro: "Galicia is the Spain nobody expects. Green hills that look like Ireland, a coastline of drowned river valleys (rías) that produce the best shellfish in Europe, a culture closer to Celtic Portugal than to Andalusia, and Santiago de Compostela — the endpoint of the Camino de Santiago pilgrimage that has been drawing walkers from across Europe for a thousand years. Galicia gets a fraction of Spain's international visitors and rewards the ones who find it disproportionately.",
    highlights: [
      { label: "Santiago de Compostela", text: "The endpoint of the Camino. The cathedral is one of the great Romanesque buildings in Europe. The Praza do Obradoiro in front of it, when a pilgrim arrives after weeks of walking, is one of the most emotionally charged public spaces in the world. You don't have to walk the Camino to feel it." },
      { label: "The Rías Baixas coast", text: "The drowned valleys of the southwest Galician coast. Cambados is the center of Albariño wine country. The seafood — percebes (barnacles), nécoras (velvet crabs), vieiras (scallops) — comes straight from the rías. Eat at a marisquería on the waterfront." },
      { label: "A Coruña", text: "The city of glass — the famous glazed gallery balconies (galerías) that face the Atlantic reflect the sky in extraordinary ways. The Torre de Hércules is the oldest working lighthouse in the world, built by the Romans. The seafront tapas scene is excellent." },
      { label: "Cabo Fisterra", text: "The 'end of the world' — the westernmost point of Spain and traditionally the final destination of the Camino. The lighthouse at the tip, with nothing but ocean to America, is one of the great edge-of-the-world experiences in Europe." },
    ],
    eat: [
      { name: "A Tafona (Santiago)", desc: "The best restaurant in Santiago de Compostela. Lucía Freitas's cooking is rooted in Galician produce — the pulpo á feira (octopus with paprika), the cocido gallego (slow-cooked meat stew), the filloas (Galician crepes). Book ahead." },
      { name: "Marisquería Rías de Galicia (Cambados)", desc: "Waterfront seafood restaurant in the heart of Albariño country. The percebes (barnacles), the nécoras, the vieiras are all straight from the ría. Order Albariño wine and let the kitchen decide what's best." },
      { name: "O Dezaseis (Santiago)", desc: "The best pintxos and tapas bar near the cathedral. Small, always full, excellent local wines. The empanada gallega (stuffed pastry) here is definitive." },
      { name: "Casa Solla (Pontevedra)", desc: "Pepe Solla's one-Michelin-star restaurant south of Santiago. Modern Galician cooking at its most precise — extraordinary seafood tasting menu. Book ahead." },
      { name: "Pulpeira de Melide (Melide)", desc: "The best pulpo á feira (boiled octopus with paprika and olive oil) in Galicia, in the small town of Melide on the Camino. Pilgrims have been stopping here for decades. Order the octopus with a Ribeiro wine and bread." },
    ],
    stay: [
      { name: "Parador de Santiago (Hostal dos Reis Católicos)", tier: "High end", desc: "The most extraordinary hotel in Spain — a 15th-century royal hospital on the Praza do Obradoiro, directly facing the cathedral. Now a state-run parador. Staying here and watching pilgrims arrive from your window is an experience with no equivalent." },
      { name: "Hotel Costa Vella (Santiago)", tier: "Mid range", desc: "Small garden hotel in the old city, stone walls, excellent breakfast with local products. The most characterful mid-range option in Santiago." },
      { name: "Casa Rural rental (Rías Baixas)", tier: "Good value", desc: "Rent a traditional stone Galician house (pazo) in the Rías Baixas wine country for a week. Vineyards outside, shellfish at the market, Albariño at the bodega. Search through RuraliaTurismo." },,
      { name: "Parador de Santiago (Hostal dos Reis Católicos)", tier: "High end", desc: "A 15th-century royal hospital directly facing the cathedral — the most extraordinary hotel in Spain. Watching pilgrims complete the Camino from your window while eating breakfast is an experience with no equivalent." },
    ],
    logistics: [
      { q: "When to go", a: "May–September for the best weather. Galicia is the rainiest region in Spain — that's why it's green and why the seafood is extraordinary. June and September are the sweet spots. The Feast of Santiago (July 25th) fills Santiago de Compostela with pilgrims and the cathedral puts on an extraordinary display — book accommodation a year ahead. Winter in Galicia is atmospheric and very affordable." },
      { q: "Getting there", a: "Santiago de Compostela Airport (SCQ) has good European connections and some international routes. A Coruña (LCG) and Vigo (VGO) are the other regional airports. From Madrid, the high-speed train (AVE) to A Coruña takes 2.5 hours and is excellent. The train to Santiago from Madrid is 3.5 hours." },
      { q: "Getting around", a: "Car is essential for the Rías Baixas, the coast, and Cabo Fisterra. Santiago de Compostela itself is walkable — the old city is compact and pedestrianized. For the Camino, the last 100km from Sarria to Santiago qualifies for the Compostela certificate and is walkable in 5 days." },
      { q: "How long", a: "Four to five days. Day one: Santiago de Compostela — cathedral, Praza do Obradoiro, old city. Day two: drive to the Rías Baixas (Cambados, O Grove for seafood). Day three: A Coruña and Torre de Hércules. Day four: Cabo Fisterra drive. Day five: Pontevedra old city, slow departure. Galicia also pairs naturally with northern Portugal — Porto is 1.5 hours south of Vigo." },
      { q: "The Camino", a: "Walking the full Camino Francés from St-Jean-Pied-de-Port takes 33 days. The last 100km (from Sarria) takes 5 days and earns the official Compostela certificate. The Portuguese Way from Porto to Santiago takes 12 days. Spring (April–June) and autumn (September–October) are the best times to walk — summer is extremely crowded and hot." },
      { q: "Money", a: "Galicia is excellent value. Seafood that would cost €80 in any other European capital costs €25–35 here. Albariño wine at a bodega: €8–15 a bottle. Pulpo á feira at a pulpería: €12–15 a ración. Parador de Santiago: €200–400. Mid-range hotels: €80–150. Casa rural rentals: €100–200 per night." },
    ],
  },
  {
    name: "Canary Islands", country: "spain", tag: "Volcanic · Year-Round · Wild",
    hook: "Off the coast of Morocco, year-round warmth, and nothing like mainland Spain.",
    img: "https://images.unsplash.com/photo-1510312305653-8ed496efae75?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=3; if(a[5]?.includes("coast")) s+=3; if(a[5]?.includes("mountains")) s+=1; if(a[6]?.includes("explore")||a[6]?.includes("wander")) s+=3; if(a[2]?.includes("week")||a[2]?.includes("twoweeks")) s+=1; if(a[7]?.includes("midrange")||a[7]?.includes("budget")) s+=1; if(a[8]?.includes("freedom")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("none")) s+=1; if(a[9]?.includes("rushed")||a[9]?.includes("crowds")) s+=1; return s; },
    intro: "The Canary Islands sit off the coast of Morocco and have nothing in common with mainland Spain beyond the language. Each island has a completely different character: Lanzarote is volcanic moonscape and César Manrique architecture; La Palma is the greenest and most vertical island in the Atlantic; Fuerteventura has the best beaches in Europe outside of the tropics; Tenerife has both the highest peak in Spain and a significant whale and dolphin population offshore. All of them have year-round warmth and almost no tourists in the right sense of the word.",
    highlights: [
      { label: "Timanfaya (Lanzarote)", text: "The volcanic national park covers a third of the island. Lava fields from eruptions that lasted six years (1730–1736), still thermally active — staff cook chicken using the geothermal heat at the park restaurant. Walking the Ruta de los Volcanes is one of the great hiking experiences in Europe." },
      { label: "César Manrique's work", text: "The Lanzarote-born artist designed most of the island's major buildings and tourist sites to blend into the volcanic landscape. The Jameos del Agua (a concert hall inside a lava tube cave), the Mirador del Río, the Fundación César Manrique. All extraordinary." },
      { label: "El Teide (Tenerife)", text: "The highest peak in Spain at 3,715m. The cable car gets you to 3,500m. The landscape around the summit is genuinely Martian — red and orange volcanic rock, nothing alive. Book the summit permit weeks ahead." },
      { label: "La Palma's stargazing", text: "La Palma has some of the darkest skies in Europe — the Roque de los Muchachos observatory sits at 2,400m above the clouds. The Starlight certification makes it one of the best stargazing destinations on earth. On a clear night from the caldera rim you can see the Milky Way without any optical aid." },
    ],
    eat: [
      { name: "El Diablo (Lanzarote)", desc: "The geothermal restaurant in Timanfaya. Chicken and meat cooked over volcanic heat from a grill positioned directly above a geothermal vent. Theatrical, delicious, and utterly unique." },
      { name: "La Tegala (Lanzarote)", desc: "The best restaurant on the island. Modern Canarian cuisine in a beautiful space designed in Manrique's tradition. The mojo negro (black pepper sauce) and the local goat cheese are the regional specialties done right." },
      { name: "El Cine (Tenerife)", desc: "In the village of Los Gigantes, looking out over the enormous sea cliffs. Fresh fish from the Atlantic, Canarian potatoes with mojo, local Tacoronte-Acentejo wine. The sunset from the terrace is extraordinary." },
      { name: "Casa Marcos (La Palma)", desc: "The best traditional Palmero restaurant. Potaje de berros (watercress stew), puchero canario (Canarian stew), the local queso de cabra. In Los Llanos de Aridane, the main town in the west." },
      { name: "Mercado Municipal (Las Palmas, Gran Canaria)", desc: "The covered market in the Vegueta neighborhood. Local tropical fruits, Canarian cheeses, mojo verde and mojo rojo by the jar. The tapas bars inside open at 10am." },
    ],
    stay: [
      { name: "Finca de Arrieta (Lanzarote)", tier: "High end", desc: "Beautiful converted finca north of Arrieta. Pools, volcanic gardens, extraordinary quiet. The most characterful luxury stay on the island." },
      { name: "Hotel San Roque (Garachico, Tenerife)", tier: "Mid range", desc: "16th-century colonial mansion in the most beautiful town in Tenerife. Pool in the courtyard, excellent restaurant, walking distance to the natural rock pools." },
      { name: "Rural house rental (La Palma)", tier: "Good value", desc: "The most rewarding way to experience La Palma — rent a traditional stone house in the Aridane Valley or the Cumbre Vieja highlands for a week. Search through CasasRuralesCanarias." },,
      { name: "Finca Malvasia (Lanzarote)", tier: "Good value", desc: "A traditional Lanzarotean farmhouse with whitewashed walls and green shutters, converted into a guesthouse with a courtyard pool. Near the wine region. The real Lanzarote, not the resort strip." },
    ],
    logistics: [
      { q: "When to go", a: "Any time of year — the Canaries are Europe's year-round destination. Average temperatures are 20–28°C every month. December–February is peak season for northern Europeans escaping winter. Spring and autumn are quieter and pleasant. Summer is warm but Lanzarote and Fuerteventura get hot (35°C+) due to Saharan wind — the western islands (La Palma, La Gomera, El Hierro) stay cooler year-round." },
      { q: "Getting there", a: "Each major island has its own airport. Lanzarote (ACE), Gran Canaria (LPA), Tenerife South (TFS), and Fuerteventura (FUE) have the most international connections. Inter-island ferries and flights connect the archipelago — Naviera Armas and Fred Olsen run the ferry routes. A multi-island trip by ferry is one of the great Atlantic travel experiences." },
      { q: "Getting around", a: "Car rental is essential on all the main islands — the landscapes are the point and you need wheels to reach them. Lanzarote is small enough to drive completely in a day. Tenerife is larger and more varied — the north (Anaga peninsula, Garachico) and south (Los Gigantes, Teide) require two separate bases. La Palma is compact and the mountain roads are extraordinary." },
      { q: "Which island", a: "Lanzarote for architecture, volcanic landscape, and César Manrique. Fuerteventura for the best beaches and wind sports. Tenerife for variety — Teide, whales, historic towns, and the Anaga rainforest. La Palma for hiking, stargazing, and complete authenticity. Gran Canaria for the dunes at Maspalomas and the old city of Las Palmas. La Gomera and El Hierro for the most remote and wild experiences." },
      { q: "How long", a: "One island: four to five days is enough to see most of it properly. Multi-island: seven to ten days with inter-island ferries. The typical mistake is staying too long on one island when the variety across the archipelago is the real draw." },
      { q: "Money", a: "The Canaries are Spain but operate under a special tax regime — VAT is 7% instead of 21%, which makes everything noticeably cheaper. Petrol is significantly cheaper than mainland Spain. A serious fish dinner: €25–40. Hotel San Roque (Garachico): €130–200. Rural house rentals on La Palma: €80–150. Lanzarote luxury fincas: €200–400." },
    ],
  },
  {
    name: "Costa Brava", country: "spain", tag: "Coves · Dalí · Hidden Fishing Villages",
    hook: "Your friend who lived in Spain for three years told you about it. Everyone else is still in Barcelona.",
    img: "https://images.unsplash.com/photo-1534508254575-d4ea4c4d4b40?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=3; if(a[5]?.includes("coast")) s+=5; if(a[6]?.includes("wander")||a[6]?.includes("explore")) s+=3; if(a[1]?.includes("partner")||a[1]?.includes("friends")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("surprise")||a[8]?.includes("beauty")) s+=3; if(a[9]?.includes("walk")||a[9]?.includes("explore")) s+=2; if(a[8]?.includes("people")||a[8]?.includes("article")) s+=2; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=3; if(a[6]?.includes("spontaneous")||a[6]?.includes("physical")) s+=2; return s; },
    intro: "The Costa Brava runs for 200km along the Catalan coast north of Barcelona to the French border — a coastline of limestone coves, medieval fishing villages, and Cap de Creus, the easternmost point of the Iberian peninsula where the Pyrenees meet the sea. Calella de Palafrugell and Cadaqués are the names that separate people who actually know this coast from people who've only been to Barcelona. Salvador Dalí was born here, lived here, and is buried here. The coast that shaped him is still largely intact.",
    highlights: [
      { label: "Calella de Palafrugell", text: "The Costa Brava in its purest form. A small whitewashed fishing village with a curved harbor, three small beaches separated by rock outcrops, and a handful of restaurants where the catch comes off the boat in the morning and onto your plate at lunch. The habaneras (traditional sailor songs) festival in July is extraordinary. Walk the coastal path to Llafranc for the best views on the coast." },
      { label: "Cadaqués", text: "The most beautiful village in Spain, according to most people who've been. At the end of a winding mountain road that kept it isolated until the 1960s — Dalí lived in the next cove at Port Lligat his entire adult life and the town still has his energy. White houses, a blue bay, one road in and out. Go in June or September — July–August it's discovered but still worth it." },
      { label: "Cap de Creus", text: "The rocky headland at the northeastern tip of Spain where the Pyrenees drop into the Mediterranean. Dalí called it the most surrealist landscape on earth and it's hard to argue with him — the wind-carved limestone formations, the violent Tramontane wind, the light on the water. The Cap de Creus Natural Park is one of the best hiking areas in Catalonia." },
      { label: "Begur and the hidden coves", text: "The medieval hilltop town of Begur has the best position on the coast — sitting above four coves that are some of the most beautiful in the Mediterranean: Aiguafreda, Sa Tuna, Aiguablava, and Fornells. Each is 10–15 minutes down a footpath, each completely different. Begur itself has good restaurants and a castle ruin with 360-degree views." },
      { label: "The coastal path (GR-92)", text: "The long-distance coastal path connects all the villages and coves from Blanes to the French border. Walk sections of it rather than driving — the views from the path between Calella and Llafranc, or around Cap de Creus, are the best way to see the coast. A full day on the path between Begur's coves is the defining Costa Brava experience." },
    ],
    eat: [
      { name: "La Gamba (Roses)", desc: "The landmark seafood restaurant of the Costa Brava. Roses is the fishing capital of the north — the catch here is extraordinary. Gambas de Roses (the local prawns, considered the best in Spain) are the only thing you need to order. Simply grilled, nothing else." },
      { name: "Restaurant Pa i Raïm (Palafrugell)", desc: "The best restaurant in the Baix Empordà. Catalan seafood cooking at its most honest — suquet de peix (fish stew), rossejat de fideus (toasted noodles with lobster), local wine. In a farmhouse 10 minutes from Calella. Book ahead." },
      { name: "Es Balconet (Cadaqués)", desc: "The terrace restaurant with the best view in Cadaqués — looking directly over the bay. Grilled fish from the local boats, Catalan dishes, good house wine. Go for lunch when the light on the water is extraordinary." },
      { name: "El Bulli (closed, but the story matters)", desc: "Ferran Adrià's restaurant sat in a cove near Roses and ran for 30 years as the most influential restaurant in the world. It's now a foundation. The Cala Montjoi where it sat is still there — accessible by boat from Roses. Go for the pilgrimage." },
      { name: "Bar Calella (Calella de Palafrugell)", desc: "The bar on the harbor front that has been serving the village since the 1950s. Cold beer, fried anchovies, the sound of the sea. Order whatever they made that morning, sit at the table closest to the water, go nowhere." },
    ],
    stay: [
      { name: "Hotel Sa Riera (Begur)", tier: "High end", desc: "Boutique hotel in a restored manor house above the coves of Begur. Pool, beautiful gardens, walking distance to the coastal path. The best hotel on the Costa Brava." },
      { name: "Hotel Llane Petit (Cadaqués)", tier: "Mid range", desc: "Small hotel directly on the beach in Cadaqués, family-run since 1965. Simple rooms, extraordinary location, the sea outside every window. Book a year ahead for July–August." },
      { name: "Casa Rural (Palafrugell hinterland)", tier: "Good value", desc: "Rent a traditional Catalan farmhouse (masia) in the hills behind Calella for a week. Olive trees, a pool, 15 minutes to the coast. Search through Rusticae or Airbnb filtered by Palafrugell." },,
      { name: "El Far Hotel (Llafranc)", tier: "Mid range", desc: "A converted lighthouse keeper's house on the headland above Llafranc, with a terrace looking down the coast toward Calella. One of the most dramatic hotel locations on the Costa Brava." },,
      { name: "Hotel Garbi (Calella de Palafrugell)", tier: "Mid range", desc: "A well-run hotel directly in Calella de Palafrugell — simple, clean, and in the right place. Steps from the harbour beach, walking distance to the coastal path to Llafranc. The straightforward choice for families and couples who want to be in the village without paying boutique prices. Note: this is Calella de Palafrugell on the Costa Brava — not the larger Calella town further south on the Maresme coast." },
    ],
    logistics: [
      { q: "When to go", a: "May–June and September–October. July–August the coast is beautiful but discovered — Cadaqués in particular fills with Barcelona weekenders and prices spike. June is the sweet spot: warm enough to swim, empty enough to walk into a restaurant without a reservation. The habaneras festival in Calella is late July and worth the crowds. October is extraordinary — warm sea, empty coves, the light turns golden." },
      { q: "Getting there", a: "Barcelona is the gateway — fly into El Prat (BCN). From Barcelona, the Costa Brava requires a car: rent at the airport and drive 1.5–2 hours north on the AP-7 motorway. There's no direct train to the coast villages. SARFA buses connect Girona with the main towns (Palafrugell, Begur, Roses) but frequency is limited. Rent a car — it's the only way to reach the coves." },
      { q: "Getting around", a: "Car is essential for moving between sections of the coast. Within each village, walk — Cadaqués, Calella, and Begur are all compact and parking is difficult in summer. The coastal path (GR-92) connects many villages on foot. In summer, boat taxis run between coves along the central Costa Brava — the best way to reach the more hidden beaches without walking." },
      { q: "Cadaqués specifically", a: "The road to Cadaqués is a 20km mountain pass with hairpin bends — narrow, spectacular, and slow. In July–August a traffic management system limits access: check ahead for current restrictions. The village has almost no parking — arrive early, park at the entrance, and walk in. The isolation that the road provides is exactly what has kept Cadaqués as it is. Respect it." },
      { q: "How long", a: "Five to six nights to do the full coast properly. Days 1–2: Calella de Palafrugell base — coastal path to Llafranc, Begur coves. Days 3–4: drive north to Cadaqués, stay two nights, walk Cap de Creus. Day 5: Roses and the Dalí triangle (Figueres museum, Port Lligat house, Púbol castle). Day 6: slow drive back to Barcelona via Girona old city (don't skip it). The Costa Brava also works as a one-week standalone with Barcelona on either end." },
      { q: "The Dalí triangle", a: "Three Dalí sites within an hour of each other: the Dalí Theatre-Museum in Figueres (his most important work, the largest surrealist object in the world), his house at Port Lligat next to Cadaqués (book ahead — strictly limited entry), and the Púbol Castle he gave to Gala. All three together take two days. The house at Port Lligat is the essential one — you see exactly how the landscape shaped the work." },
      { q: "Money", a: "The Costa Brava spans a wide range. Cadaqués in July: €250–400 for a mid-range room. Off-season: €100–150. The central coast around Calella and Begur: €150–300 in peak season, €80–150 in shoulder. Lunch at a harbor restaurant: €25–45 per person. The gambas de Roses are expensive (€30–50 a portion) and worth every euro. Self-catering masia for a week: €1,500–3,000 depending on size." },
    ],
  },
];

// ─── CHILE REGIONS ─────────────────────────────────────────────────────────────
const chileRegions = [
  {
    name: "Santiago", country: "chile", tag: "City · Food · Andes Backdrop",
    hook: "Most people treat Santiago as a layover. That's a mistake they regret quickly.",
    img: "https://images.unsplash.com/photo-1588436706487-9d55d73a39e3?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("culture")) s+=3; if(a[3]?.includes("local")||a[3]?.includes("balanced")) s+=2; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("cities")||a[5]?.includes("mountains")) s+=2; if(a[6]?.includes("eat")||a[6]?.includes("wander")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("surprise")||a[8]?.includes("connection")) s+=2; if(a[9]?.includes("eat")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("article")||a[8]?.includes("people")) s+=1; if(a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=1; return s; },
    intro: "Santiago sits in a long narrow valley with the Andes rising directly behind it — on clear days the snowcapped peaks are visible from the city center, which is not something most major capitals can claim. The city itself is a genuine surprise: a serious food scene built around Chilean ingredients, a wine culture that rivals anything in Europe, and neighborhoods like Bellavista and Lastarria that have nothing to do with the South American capital you were picturing.",
    highlights: [
      { label: "Mercado Central", text: "The iron-and-glass covered market that's been feeding Santiago since 1872. The seafood is the point — congrio (conger eel), picorocos (giant barnacles), locos (abalone). Go for lunch at one of the central restaurants, order whatever they caught that morning." },
      { label: "Bellavista neighborhood", text: "La Chascona (one of Pablo Neruda's three houses) is here, and the street art is among the best in Latin America. Eat dinner at one of the restaurants on Constitución, drink in the bars on Pío Nono. The neighborhood goes until 3am." },
      { label: "Lastarria", text: "The design and arts district. Bookshops, galleries, coffee shops in old mansions, the best cocktail bars in the city. Walk it on a Saturday morning when the antique market sets up." },
      { label: "Cerro San Cristóbal", text: "The hill above the city, accessible by funicular. The view from the top — Santiago spread out below, the Andes rising behind — is the one that makes you understand the city's geography immediately." },
    ],
    eat: [
      { name: "Boragó", desc: "Rodolfo Guzmán's restaurant using only Chilean ingredients — many foraged, many from ecosystems most people don't know exist. One of the most important restaurants in Latin America. Book months ahead." },
      { name: "El Mercadito", desc: "The best empanadas in Santiago, from a tiny spot in Barrio Italia. The pino filling (beef, egg, olive, raisin) is the canonical Chilean version. Open only for lunch, cash only." },
      { name: "Azul Profundo", desc: "The best seafood restaurant in the city, near Mercado Central. The caldillo de congrio (Neruda wrote a poem about this soup) is what you order. The ceviche is made with Chilean-style citrus." },
      { name: "Bar The Clinic", desc: "Named after a famous satirical newspaper, this Bellavista bar has the best pisco sour in the city and a terrace that fills every Friday evening. The terremoto (pipeño wine with pineapple sorbet) is the house specialty." },
      { name: "Galindo", desc: "Old-school Chilean restaurant in Bellavista that's been open since 1978. Pastel de choclo (corn and meat casserole), cazuela (broth with meat and vegetables), Chilean country cooking at its most honest. Lunch only." },
    ],
    stay: [
      { name: "The Singular Santiago", tier: "High end", desc: "Converted 1920s industrial building in the Lastarria neighborhood. Extraordinary design, rooftop bar with Andes views, the best hotel in the city." },
      { name: "Hotel Magnolia", tier: "Mid range", desc: "Boutique hotel in a converted townhouse in Barrio Italia. Good rooms, excellent breakfast, great neighborhood for exploring on foot." },
      { name: "Lastarria Apartments", tier: "Good value", desc: "Staying in Lastarria puts you in the best neighborhood — walking distance to everything, best restaurants outside your door. Search Airbnb filtered by Lastarria." },,
      { name: "Lastarria Boutique Hotel", tier: "Mid range", desc: "A converted townhouse in the Lastarria neighbourhood — the best area in Santiago for restaurants, galleries, and bookshops. Seventeen rooms, a rooftop terrace, the neighbourhood outside the door." },
    ],
    logistics: [
      { q: "When to go", a: "October–April (Southern Hemisphere spring and summer). Santiago winters (June–August) are cold and smoggy — the city sits in a valley and the pollution gets trapped. September–November is beautiful: the Andes are still snowcapped, the city is green, and the vineyards are flowering. January–February is peak summer — warm, clear, and busy." },
      { q: "Getting there", a: "Arturo Merino Benítez Airport (SCL) is one of South America's main hubs with direct US connections (American, Delta, LATAM from Miami, New York, Dallas). The Centropuerto bus runs to the city center for $2,000 CLP (about $2). Uber works from the airport. The journey is 45–60 minutes depending on traffic." },
      { q: "Getting around", a: "The Metro is excellent — clean, safe, covers all the main neighborhoods. A Bip! card (rechargeable) costs 1,350 CLP and trips are 800–900 CLP each. Uber is cheap and reliable. Walking is the best option in Bellavista, Lastarria, and Barrio Italia. Avoid taxis from the street — use Uber or book through your hotel." },
      { q: "How long", a: "Three nights in Santiago as a base. Day one: Mercado Central for lunch, Lastarria, Cerro Santa Lucía. Day two: day trip to Casablanca Valley or Colchagua wine country. Day three: Bellavista, La Chascona, Cerro San Cristóbal. Santiago pairs naturally with Valparaíso (1.5 hours) and the wine valleys." },
      { q: "Money", a: "Chile is the most expensive country in South America but reasonable by international standards. A good lunch: 8,000–15,000 CLP ($8–15). Dinner at a serious restaurant: 30,000–60,000 CLP per person. The Singular Santiago: $300–500 USD. Mid-range hotels: $100–200. A pisco sour in a good bar: 5,000–8,000 CLP." },
      { q: "Spanish", a: "Chilean Spanish is notoriously fast and full of local slang (chilenismos). Even fluent Spanish speakers find Chileans hard to understand at first. Key phrases: po (softener added to everything), cachai? (you understand?), weon/wea (all-purpose words, context-dependent). English is limited outside tourist areas and top-end restaurants — Google Translate on camera mode is essential for menus." },
    ],
  },
  {
    name: "Elqui Valley", country: "chile", tag: "Pisco · Stargazing · Desert Mysticism",
    hook: "The valley where pisco is born, shamans moved for the energy, and the sky at night is the reason astronomers built observatories here. Nobody talks about it.",
    img: "https://images.unsplash.com/photo-1419242902214-272b3f66ee7a?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("countryside")||a[5]?.includes("desert")) s+=4; if(a[6]?.includes("nothing")||a[6]?.includes("wander")) s+=3; if(a[1]?.includes("partner")||a[1]?.includes("solo")) s+=2; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=2; if(a[9]?.includes("crowds")||a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=3; if(a[6]?.includes("spontaneous")||a[6]?.includes("fullday")) s+=2; return s; },
    intro: "The Elqui Valley runs east from the Pacific coast into the Andes in northern Chile — a narrow ribbon of green vineyards and fruit orchards cutting through bone-dry desert mountains. This is where pisco comes from: the grape distillate that Chile and Peru have been arguing about for centuries. The valley sits at altitude under some of the clearest skies in the world, which is why the European Southern Observatory built its telescopes here. New age communities moved here in the 1980s for reasons they describe as energetic. The pisco is real. The stars are extraordinary. The quiet is complete.",
    highlights: [
      { label: "Pisco distilleries", text: "The valley produces Chile's best pisco — Pisco Elqui, Mistral, and the artisan producers around Montegrande and Pisco Elqui village are the ones worth visiting. Tastings are informal and free at most small distilleries. The pisco sour made with freshly squeezed Elqui lemon at the source tastes nothing like what you've had before." },
      { label: "Stargazing", text: "The Elqui Valley has almost zero light pollution and 300+ clear nights a year — second only to the Atacama in Chile for astronomical conditions. The Observatorio Cerro Mamalluca outside Vicuña runs nightly tours with professional telescopes for non-specialists. The Milky Way is visible to the naked eye from anywhere in the valley on a clear night." },
      { label: "Montegrande", text: "The village where Gabriela Mistral was born — the first Latin American woman to win the Nobel Prize in Literature, whose face is on the Chilean 500-peso coin. Her childhood home is a small museum. The village itself is quiet, beautiful, and completely unchanged — 900 people, one square, one restaurant." },
      { label: "The valley drive", text: "Drive Route 41 from La Serena east into the valley — 90km of progressive transformation from coastal city to high Andean desert. The road follows the Elqui River through vineyards, through village squares, past roadside stalls selling papaya and pisco, into increasingly dramatic mountains. Stop wherever looks interesting. Nothing is far from anything else." },
    ],
    eat: [
      { name: "Restaurant El Tesoro de Elqui (Pisco Elqui)", desc: "The best restaurant in the valley, in the village of Pisco Elqui. Chilean country cooking using valley ingredients — goat stew, local vegetables, fresh papaya, homemade pisco sour. Terrace with views of the vineyards and the mountains." },
      { name: "Destilería Pisco Mistral (Vicuña)", desc: "The main Mistral distillery in Vicuña does tours and tastings in a beautiful colonial building. The Premium and Gran Pisco expressions are the ones to try — a serious spirit that bears no resemblance to the cheap pisco sold outside Chile." },
      { name: "Café del Pueblo (Montegrande)", desc: "The only restaurant in Montegrande. One menu, whatever was made that day, served on a terrace in the village square. Papaya juice, goat cheese, homemade bread. The best lunch in the valley costs 6,000 CLP." },
      { name: "El Durmiente Elquino (Pisco Elqui)", desc: "Organic café and restaurant run by one of the new age community families. Fresh juices, vegetarian food, homemade pisco-infused desserts. The algarrobina cocktail (carob syrup, pisco, egg white) is the valley's answer to the pisco sour." },
    ],
    stay: [
      { name: "Elqui Domos (Pisco Elqui)", tier: "High end", desc: "Geodesic domes with transparent ceilings on a hillside above the valley. Fall asleep watching the Milky Way through the roof. The most extraordinary accommodation in the valley and one of the most unusual in Chile. Book ahead — small property, sells out." },
      { name: "Hacienda Los Andes (Vicuña)", tier: "Mid range", desc: "A converted colonial hacienda with a pool, a pisco cellar, and mountain views. The owners run stargazing sessions from the terrace. The best mid-range option in the valley." },
      { name: "Valle Elqui Hostal (Pisco Elqui)", tier: "Good value", desc: "Family-run guesthouse in Pisco Elqui village. Simple rooms, excellent breakfast with valley fruit, the owners know every pisco producer personally and will arrange private tastings. Best value in the valley." },,
      { name: "Refugio del Ángel (Montegrande)", tier: "Good value", desc: "A small guesthouse in the village of Montegrande — four rooms, a terrace with valley and mountain views, breakfast with local fruit and homemade jam. The best base for the Gabriela Mistral pilgrimage and the small distilleries." },
    ],
    logistics: [
      { q: "When to go", a: "Year-round, but April–November is ideal. December–March is summer in northern Chile — the valley gets extremely hot (35–40°C) and the vineyards are dormant after harvest. April–June is harvest season — the pisco grapes come in and the distilleries are active. July–September is cool and clear with extraordinary night skies. The valley receives almost no rain regardless of season." },
      { q: "Getting there", a: "Fly into La Serena (LSC) from Santiago — LATAM and Sky Airline fly multiple times daily, 1.5 hours. From La Serena, the valley is 90km east on Route 41 — rent a car at the airport (essential for exploring the valley properly). Local buses run from La Serena to Vicuña and Pisco Elqui but frequency is limited. A car gives you freedom to stop at every distillery and village that catches your eye." },
      { q: "Getting around", a: "Car is essential. The valley is 90km long and the best places — the smaller distilleries, Montegrande, the high-altitude observatory — are spread along Route 41 and the side roads off it. The road is paved all the way to Pisco Elqui. Beyond that, towards the Argentine border, it becomes dirt and requires a 4WD. Fill up in Vicuña — petrol stations disappear quickly beyond there." },
      { q: "How long", a: "Three nights minimum. Day one: La Serena to Vicuña — arrive, Mistral distillery tour, settle in. Day two: drive the full valley to Pisco Elqui, stopping at Montegrande and small distilleries along the way. Night two: stargazing at Cerro Mamalluca observatory. Day three: slow morning in Pisco Elqui, roadside fruit stands, return to La Serena. The Elqui Valley pairs naturally with the Atacama — drive north on the Pan-American Highway for 3 hours." },
      { q: "The pisco question", a: "Chilean pisco and Peruvian pisco are genuinely different things — different grapes, different distillation methods, different character. Chilean pisco is smoother, more refined, higher alcohol. The best Chilean expressions (Gran Pisco, Premium grades) are world-class spirits. Buy bottles directly from the valley distilleries — prices are a fraction of what you'd pay in Santiago and most of the best small-batch productions never leave the valley." },
      { q: "Money", a: "The Elqui Valley is excellent value. Elqui Domos: $180–280 USD. Hacienda Los Andes: $90–150. Valle Elqui Hostal: $40–70. A full lunch at Café del Pueblo: 5,000–8,000 CLP. Pisco distillery tastings: free to 3,000 CLP. A bottle of excellent artisan pisco direct from the producer: 12,000–20,000 CLP ($12–20). The Cerro Mamalluca observatory tour: 7,000 CLP." },
    ],
  },
  {
    name: "Colchagua Valley", country: "chile", tag: "Wine · Carménère · Countryside",
    hook: "The grape variety that disappeared from Bordeaux in 1867 was found alive here in 1994. This is where it lives.",
    img: "https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("luxury")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("safe")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("eat")||a[6]?.includes("explore")) s+=2; if(a[1]?.includes("partner")) s+=2; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=2; if(a[8]?.includes("quiet")||a[8]?.includes("beauty")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("sit")) s+=2; if(a[8]?.includes("deep")||a[8]?.includes("people")) s+=2; if(a[9]?.includes("rushed")||a[9]?.includes("crowds")) s+=2; return s; },
    intro: "The Colchagua Valley is Chile's most important red wine region — home to Carménère, the Bordeaux grape variety that was thought extinct until it was identified growing wild here in 1994, and to some of the most beautiful winery estates in the Southern Hemisphere. The valley runs east from the coast into the foothills of the Andes, and the scenery — rolling vineyards, adobe farmhouses, snow-peaked mountains on the horizon — is as good as any wine country in the world.",
    highlights: [
      { label: "Carménère tastings", text: "The grape the French forgot. Carménère makes a deep, complex red wine with notes of green pepper and dark fruit. Viña Montes, Casa Lapostolle, and Viu Manent are the benchmark estates. All do excellent tastings and tours." },
      { label: "Santa Cruz town", text: "The valley's main town, two hours from Santiago. The Colchagua Museum has one of the best pre-Columbian and independence-era collections in Chile. The main square fills on weekends. Stay here as a base for the wine country." },
      { label: "The wine train", text: "A vintage steam train runs from San Fernando to Santa Cruz on weekends between September and April. Wine tastings on board, views of the valley. Book ahead — it sells out." },
      { label: "Hacienda Los Lingues", text: "A 400-year-old estate in the valley that accepts guests. Spanish colonial architecture, horses, organic gardens, wine from their own vineyards. One of the most extraordinary stays in Chile." },
    ],
    eat: [
      { name: "Viña Montes Restaurant", desc: "The restaurant at Montes winery designed by a Chilean architect to align with the cardinal points. The tasting menu pairs each course with a different Montes wine. The Purple Angel (Carménère) is the one to order." },
      { name: "Casa Lapostolle Residence", desc: "The French-Chilean estate does a full tasting lunch at the winery — cheese, charcuterie, multiple courses, extraordinary Apalta wines. Book directly with the winery well ahead." },
      { name: "Los Hornos de Barro (Santa Cruz)", desc: "Traditional Chilean asado (wood-fired barbecue) restaurant in Santa Cruz. The whole lamb and the empanadas from the clay oven are the reason people drive from Santiago." },
      { name: "Club Social de Santa Cruz", desc: "The old social club on the main square, converted to a restaurant. Cazuela, pastel de choclo, local wine. Lunch only, full of locals, exactly what a wine country lunch should be." },
    ],
    stay: [
      { name: "Casa Lapostolle Residence", tier: "High end", desc: "Six suites on the winery estate, with a private pool, cellar tastings, and meals prepared by the estate chef. One of the great wine country stays in the world. All inclusive." },
      { name: "Hotel Santa Cruz Plaza", tier: "Mid range", desc: "The best hotel in Santa Cruz town. Colonial-style building on the main square, good restaurant, wine bar, pool. Excellent base for winery visits." },
      { name: "Hacienda Los Lingues", tier: "High end", desc: "400-year-old colonial estate with guest rooms. Horses, organic gardens, polo, their own wine. Staying here is like being a guest of Chilean landed gentry. Book months ahead." },,
      { name: "Viu Manent Estate (Santa Cruz)", tier: "Mid range", desc: "The wine estate that does the Colchagua experience most completely — horseback rides through the Carménère vineyards, a pool in the estate garden, tastings of their top wines at sunset. Stay here and skip the hotel entirely." },
    ],
    logistics: [
      { q: "When to go", a: "September–April. Harvest (March–April) is the best time — the valley is alive with activity, the air smells of fermenting grapes, and most wineries run special harvest experiences. October–November is spring: wildflowers, green vineyards, uncrowded. July–August is cold and wet — many wineries reduce their hours." },
      { q: "Getting there", a: "Two hours from Santiago by car on the Route 5 Pan-American Highway south to San Fernando, then Route I-50 into the valley. The wine train from San Fernando is the most enjoyable option on weekends. There's no direct public bus to the wineries — you need a car or a tour from Santiago." },
      { q: "Getting around", a: "Car is essential. The wineries are spread across the valley and there's no public transport between them. Hire a driver for the day from Santa Cruz (local drivers know all the estates and won't charge you for tastings, unlike tour operators). Most wineries require advance booking for tastings — call ahead." },
      { q: "How long", a: "Two to three nights. Day one: drive from Santiago, check in, first winery visit in the afternoon. Day two: two or three winery visits with a proper lunch at one. Day three: Santa Cruz market, Colchagua Museum, slow departure. The valley combines naturally with Santiago and Valparaíso for a complete central Chile week." },
      { q: "Money", a: "Winery tasting fees: 8,000–25,000 CLP depending on the wines. Casa Lapostolle all-inclusive: $600–900 USD per night. Hotel Santa Cruz Plaza: $120–200. A winery lunch: 25,000–50,000 CLP per person. The quality-to-price ratio on the wines themselves is exceptional — bottles that cost $8 locally sell for $40 in the US." },
      { q: "Wine notes", a: "Carménère is the reason to be here — but Colchagua also produces excellent Cabernet Sauvignon, Syrah, and Malbec. The valley's best reds come from the Apalta sub-region (Casa Lapostolle, Montes, Neyen). Ask to taste the single-vineyard wines rather than the entry-level ranges. Buy bottles directly at the estates — you'll pay a fraction of export prices." },
    ],
  },
  {
    name: "Atacama Desert", country: "chile", tag: "Otherworldly · Salt Flats · Stars",
    hook: "The driest place on earth. Some parts haven't seen rain in recorded history. The stars look fake. They're not.",
    img: "https://images.unsplash.com/photo-1531761535209-180857e963b9?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=4; if(a[5]?.includes("mountains")||a[5]?.includes("desert")) s+=4; if(a[6]?.includes("explore")||a[6]?.includes("wander")) s+=3; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("beauty")||a[8]?.includes("surprise")) s+=3; if(a[9]?.includes("explore")||a[9]?.includes("walk")) s+=2; if(a[0]?.includes("beauty")) s+=3; if(a[8]?.includes("deep")||a[8]?.includes("article")) s+=1; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")) s+=2; if(a[6]?.includes("physical")||a[6]?.includes("fullday")) s+=2; return s; },
    intro: "The Atacama is the driest non-polar desert on earth — some weather stations have never recorded rain. It sits at 2,400 meters above sea level in northern Chile, framed by active volcanoes and the Andes to the east and the Pacific coastal range to the west. The landscape is so alien that NASA tests Mars rovers here. The salt flats turn pink at sunset. The flamingos are real. And the night sky — with zero light pollution and very little atmosphere — is the best stargazing on earth.",
    highlights: [
      { label: "Valle de la Luna", text: "The Valley of the Moon — salt and clay formations carved by wind into shapes that genuinely look like a lunar surface. Walk in the afternoon, stay for sunset when the salt crystals turn gold and then pink. The dunes at the end are good for sandboarding." },
      { label: "El Tatio geysers", text: "The highest geyser field in the world at 4,320 meters. Go at dawn (4:30am departure) when the geysers are most active — the steam shoots 10 meters against the dark sky as the sun rises over the volcanoes. Bring every layer you own — it's -10°C at that hour." },
      { label: "Salar de Atacama", text: "The third-largest salt flat in the world, 20 minutes south of San Pedro. The Laguna Chaxa at the edge hosts three species of flamingo, including the James flamingo. The salt crust at sunrise looks like a mirror." },
      { label: "Stargazing", text: "The Atacama has the highest concentration of astronomical observatories in the world for a reason — the sky is extraordinary. Book a night tour with Space (the best operator in San Pedro) for a guided session with professional telescopes. The Milky Way is visible to the naked eye." },
    ],
    eat: [
      { name: "Tierra Atacama Restaurant", desc: "The restaurant at the Tierra Atacama hotel, open to non-guests for dinner with a reservation. Contemporary Atacameño cuisine — quinoa, llama, local herbs and roots. The best cooking in the desert." },
      { name: "Adobe Restaurant", desc: "The most established restaurant in San Pedro. Chilean-Atacameño menu with good local wines and the best pisco sours in the region. The terrace fills at sunset." },
      { name: "La Estaka", desc: "Casual restaurant in San Pedro with good empanadas, cazuela, and grilled llama. The most honest local option at a fair price. Go for lunch when the kitchen is freshest." },
      { name: "Café Étnico", desc: "Coffee shop and breakfast spot in San Pedro. Fresh juice from local fruits (cherimoya, mango), good eggs, local cheese. The only decent coffee in the desert — go here before every early morning excursion." },
    ],
    stay: [
      { name: "Tierra Atacama", tier: "High end", desc: "The benchmark desert lodge. Thirty-two suites around a central pool, extraordinary architecture that blends into the landscape, all excursions included. One of the great hotels in Latin America." },
      { name: "Alto Atacama", tier: "High end", desc: "All-inclusive lodge at the foot of the Catarpe Valley. Adobe architecture, terraced pool with volcano views, all excursions included. The spa using local minerals and medicinal plants is extraordinary." },
      { name: "Hostal Sonchek", tier: "Mid range", desc: "The best mid-range option in San Pedro. Clean rooms, good breakfast, central location, staff who know the desert. A fraction of the all-inclusive lodge prices." },,
      { name: "Explora Atacama (San Pedro)", tier: "High end", desc: "The benchmark adventure lodge — all excursions included, outstanding guiding, the most comprehensive exploration program of any desert lodge in Chile. More activities-focused than Tierra or Alto Atacama." },
    ],
    logistics: [
      { q: "When to go", a: "Year-round, but the best months are March–May and September–November. Summer (December–February) brings the Bolivian winter — afternoon thunderstorms that flood the salt flats and close some excursions. June–August is cold at night (-10°C or below) but the skies are clearest. The desert is always extreme — plan for both heat (30°C+ days) and cold (below freezing at night) regardless of season." },
      { q: "Getting there", a: "Fly to Calama (CJC) from Santiago — LATAM and Sky Airline fly multiple times daily, about 2 hours. The all-inclusive lodges run transfers from Calama to San Pedro de Atacama (45 minutes). If staying in San Pedro independently, book a shared transfer (5,000–8,000 CLP) or rent a car at Calama airport." },
      { q: "Altitude", a: "San Pedro sits at 2,440 meters. El Tatio is at 4,320 meters. Altitude sickness is real — headache, nausea, and fatigue are common for the first 24 hours. Don't fly in and immediately go to El Tatio. Rest the first day, drink enormous amounts of water, avoid alcohol, and take the altitude seriously. The lodges all have oxygen available." },
      { q: "Getting around", a: "Most people do the Atacama through the all-inclusive lodges, which include all excursions and transport. Independent travelers based in San Pedro can rent a 4WD (essential — many roads require it) or book tours through local operators. The best excursions are El Tatio (dawn), Valle de la Luna (afternoon/sunset), Salar de Atacama (morning), and stargazing (night)." },
      { q: "How long", a: "Four nights minimum to do the Atacama properly. Night one: arrive, acclimatize. Night two: Valle de la Luna sunset, first stargazing. Night three: El Tatio geysers at dawn, Salar de Atacama afternoon. Night four: Laguna Miscanti and Miñiques (high-altitude lakes), another stargazing session. Any less and you'll feel rushed in a place that rewards slowness." },
      { q: "Money", a: "The Atacama has a wide range. Tierra Atacama and Alto Atacama all-inclusive: $500–900 USD per night (includes all excursions — expensive upfront but the excursions alone cost $50–120 each). Hostal Sonchek: $80–150. Eating in San Pedro: 8,000–18,000 CLP per meal. Private stargazing tours: 20,000–35,000 CLP. The desert is not cheap — budget accordingly." },
    ],
  },
  {
    name: "Lake District", country: "chile", tag: "Volcanoes · Lakes · German Settlers",
    hook: "Chilean Bavaria. Volcanoes reflected in lakes, smoked salmon in German-style smokehouses, and almost nobody from outside South America.",
    img: "https://images.unsplash.com/photo-1565967511849-76a60a516170?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("adventure")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("mountains")||a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("explore")||a[6]?.includes("wander")) s+=3; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("quiet")) s+=2; if(a[9]?.includes("explore")||a[9]?.includes("walk")) s+=2; if(a[8]?.includes("none")||a[8]?.includes("feel")) s+=2; if(a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=2; if(a[6]?.includes("physical")||a[6]?.includes("fullday")) s+=2; return s; },
    intro: "The Chilean Lake District runs from Temuco south to Puerto Montt — a landscape of perfect conical volcanoes reflecting in deep blue lakes, araucaria forests that look prehistoric, and small German-settler towns that arrived in the 1850s and never quite left Bavaria behind. Pucón, at the foot of the active Villarrica volcano, is the adventure capital. Frutillar, on the shore of Lake Llanquihue, looks directly at the perfectly symmetrical Osorno volcano and has a German cultural museum that explains exactly how this happened.",
    highlights: [
      { label: "Volcán Villarrica", text: "The most accessible active volcano in Chile — you can hike to the crater rim and look down into the active lava lake. A guided ascent takes 6–8 hours round trip and requires crampons and ice axe (all provided). One of the great hikes in South America. Book with a guide operator in Pucón." },
      { label: "Lake Llanquihue", text: "The second-largest lake in Chile. The view across the water to Osorno and Calbuco volcanoes is extraordinary — the classic image of the Lake District. Drive the lake circuit, stopping in Frutillar for kuchen (German-style cake) and smoked salmon." },
      { label: "Huerquehue National Park", text: "Old-growth araucaria (monkey puzzle) forest, glacial lakes, and one of the best day hikes in Chile — the Los Lagos trail. The araucaria trees are 1,500 years old and look like something from another era." },
      { label: "Termas Geometricas", text: "The most beautiful thermal hot springs in Chile — 60 pools in a red fern canyon, fed by geothermal water. Open until midnight. Going in winter when it's cold outside and the pools are steaming is extraordinary." },
    ],
    eat: [
      { name: "Club Alemán (Frutillar)", desc: "The German club restaurant on the lake in Frutillar. Smoked salmon, kuchen, regional cheeses, Kunstmann beer brewed locally in the German tradition. The view of Osorno volcano from the terrace is the best in the Lake District." },
      { name: "El Fogón de Pedro (Pucón)", desc: "Wood-fired asado restaurant in Pucón. The cordero al palo (whole lamb on a cross-spit over coals) takes 6 hours and is only available on weekends. The best meat you'll eat in Chile." },
      { name: "Casavalles (Valdivia)", desc: "The most serious restaurant in the Lake District. Chilean-European cuisine using regional ingredients — merluza (hake), local mushrooms, smoked meats. Valdivia is underrated and this is the reason to go." },
      { name: "Cuatro Estaciones (Pucón)", desc: "The lake trout (trucha) from Lake Villarrica is the regional fish. This restaurant on the lakefront does it simply — grilled or smoked — with local potatoes and salad. Lunch only." },
    ],
    stay: [
      { name: "antumalal Hotel (Pucón)", tier: "High end", desc: "A Frank Lloyd Wright-influenced hotel on a cliff above Lake Villarrica since 1950. The most architecturally interesting hotel in Chile. Queen Elizabeth II stayed here. Extraordinary views." },
      { name: "Hotel Esmeralda (Pucón)", tier: "Mid range", desc: "Comfortable hotel in Pucón town, good breakfast, walking distance to the lake and restaurants. The best mid-range option for the adventure base." },
      { name: "Frutillar Lakefront Cabañas", tier: "Good value", desc: "Rent a traditional wooden cabaña on the shore of Lake Llanquihue. Wake up to Osorno volcano reflected in the water. Search Airbnb filtered by Frutillar — book ahead in January–February." },,
      { name: "Puyuhuapi Lodge (Puyuhuapi)", tier: "High end", desc: "A remote thermal spa lodge on the Puyuhuapi fjord, accessible only by boat. Natural hot springs fed directly from the volcano. One of the most isolated and extraordinary stays in Chilean Patagonia." },
    ],
    logistics: [
      { q: "When to go", a: "November–March for hiking, kayaking, and volcano ascents. The Villarrica hike requires dry conditions — July–September the volcano is often cloud-covered and the hike is closed. December–February is peak summer — Pucón fills with Chileans and prices rise. November and March are the sweet spots: good weather, half the crowd. The thermal springs (Termas Geometricas) are extraordinary in winter — cold outside, steaming pools inside." },
      { q: "Getting there", a: "Fly to Temuco (ZCO) for Pucón (1.5 hours by bus or rental car) or Puerto Montt (PMC) for Frutillar and the southern lakes (45 minutes). Both have connections from Santiago. The overnight bus (Cruz del Sur, around $30) from Santiago to Pucón takes 9 hours — comfortable and a good option for saving a day's accommodation." },
      { q: "Getting around", a: "Car is the best option for the lake circuit, national parks, and thermal springs. Pucón town is walkable. Local buses connect the main towns but schedules are infrequent. From Pucón, guided excursions (volcano, whitewater rafting, mountain biking) are bookable directly in town — most operators are on O'Higgins street." },
      { q: "How long", a: "Five to six days. Days 1–2: Pucón — Huerquehue hike, Termas Geometricas, Villarrica ascent. Day 3: drive south via Villarrica lake to Frutillar. Days 4–5: lake circuit, Osorno volcano hike, Puerto Varas. Day 6: Puerto Montt, departure or continue south to Chiloé. The Lake District connects naturally to both Santiago (fly) and Patagonia (drive south or ferry)." },
      { q: "Adventure notes", a: "Pucón is Chile's adventure capital — whitewater rafting on the Trancura River (class IV), kayaking on Lake Villarrica, canopy, mountain biking, and the volcano ascent all operate out of the same few streets. The gear and guiding quality is high. The volcano hike is strenuous (6–8 hours, significant altitude gain) — only attempt it in good physical condition and with a certified guide." },
      { q: "Money", a: "The Lake District is good value. Antumalal Hotel: $200–350 USD. Mid-range hotels: $80–150. Lakefront cabañas: $60–120 per night. The Villarrica volcano guided ascent: $60–90 USD including all gear. Termas Geometricas entry: $30 USD. A meal in Pucón: 10,000–20,000 CLP. German kuchen and coffee in Frutillar: 3,000–5,000 CLP." },
    ],
  },
  {
    name: "Chiloé Island", country: "chile", tag: "Fog · Wooden Churches · Mythology",
    hook: "An island with its own mythology, its own architecture, and its own relationship with the Pacific fog. Nothing prepares you for it.",
    img: "https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("absorb")) s+=3; if(a[7]?.includes("budget")||a[7]?.includes("midrange")) s+=2; if(a[8]?.includes("surprise")||a[8]?.includes("connection")) s+=3; if(a[9]?.includes("walk")||a[9]?.includes("sit")) s+=2; if(a[8]?.includes("people")||a[8]?.includes("none")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; if(a[6]?.includes("spontaneous")||a[6]?.includes("fullday")) s+=2; return s; },
    intro: "Chiloé is an island off the coast of southern Chile that developed in isolation for centuries and came out the other side with its own mythology, its own architectural tradition, its own dialect, and its own relationship with the Pacific fog. The 16 UNESCO-listed wooden churches that dot the island were built by Jesuit missionaries in the 18th century using a technique brought from Europe but adapted to local materials. The curanto (a seafood stew cooked in a pit with hot stones) is one of the great dishes of the Americas. The brujos (local witches) are still a serious part of island culture.",
    highlights: [
      { label: "The wooden churches", text: "Sixteen of the island's old Jesuit churches are UNESCO World Heritage Sites. Each one is different — the colors, the proportions, the style of wooden shingles (tejuelas). The churches in Achao, Quinchao, and Chonchi are the most extraordinary. None of them feel like tourist sites because they're still active parish churches." },
      { label: "Castro's palafitos", text: "The capital Castro has the most photogenic street in Chile — a row of brightly painted houses built on stilts over the water of the estuary. At low tide they appear to float. At high tide they reflect in the water. Photograph them from the bridge at sunrise." },
      { label: "Parque Nacional Chiloé", text: "The western coast of the island — undeveloped Pacific beaches, native tepú and tineo forest, and the chance to see penguins, sea lions, and marine otters. The Cucao beach is 12km of untouched sand with no development." },
      { label: "The curanto", text: "The island's defining dish — clams, mussels, potatoes, smoked pork, and milcao (potato pancakes) cooked in a pit with hot stones covered with leaves. A genuine ceremony more than a meal. The best version is made by a family in their backyard. Ask your guesthouse to arrange it." },
    ],
    eat: [
      { name: "El Mercado (Castro)", desc: "The covered market in Castro's center. The marisquerías (seafood stalls) inside serve cazuela de mariscos, curanto en olla, and fresh centolla (king crab) at lunch. No atmosphere, extraordinary food, very cheap." },
      { name: "Travesía (Castro)", desc: "The most serious restaurant on the island. Contemporary Chilote cuisine — razor clams with local herbs, smoked salmon from the island's farms, milcao updated for a restaurant setting. Book ahead." },
      { name: "La Brújula de Oro (Castro)", desc: "Old-school seafood restaurant that's been on the waterfront since 1975. The chupe de mariscos (shellfish gratin) and the centolla are why people come back. Cash only." },
      { name: "Dalcahue Sunday market", desc: "The weekly artisan market in Dalcahue, 20km from Castro. Woolen goods, wicker baskets, dried seafood, homemade liqueurs. The food stalls outside serve empanadas de mariscos for 800 CLP. The best market in southern Chile." },
    ],
    stay: [
      { name: "Tierra Chiloé", tier: "High end", desc: "The island's only luxury lodge — 12 suites on the shore of the Dalcahue channel with views of the volcanoes across the water. All excursions included. The most extraordinary location of any hotel in Chile." },
      { name: "Hotel de Castro", tier: "Mid range", desc: "The best conventional hotel in the capital. Good rooms, lake views from the upper floors, walking distance to the palafitos and market." },
      { name: "Casas Chiloé Guesthouses", tier: "Good value", desc: "Renting a traditional Chiloé wooden house in a village outside Castro gives you the island experience. Look for guesthouses in Dalcahue, Quellón, or Chonchi — run by island families who cook breakfast." },,
      { name: "Palafito 1326 (Castro)", tier: "Mid range", desc: "A palafito — the traditional Chiloé stilt house built over the water — converted into a boutique hotel in Castro. Wake up with the tide beneath you, the coloured houses of the palafito district on either side." },
    ],
    logistics: [
      { q: "When to go", a: "November–March. Chiloé is rain and fog year-round — that's its character — but the summer months are the driest and the national park is accessible. The island is extraordinary in grey weather (the fog gives everything a dreamlike quality) but the Dalcahue market and outdoor activities require dry days. June–August is very wet and most guesthouses outside Castro close." },
      { q: "Getting there", a: "Fly to Puerto Montt (PMC) from Santiago (1.5 hours). From Puerto Montt, take the Ancud bus (2 hours) or drive south to Pargua for the ferry crossing to Chacao (30 minutes, runs every 30 minutes, 3,900 CLP for a car). From Chacao it's 90 minutes to Castro. Chiloé can also be reached from the Lake District by driving south from Puerto Varas." },
      { q: "Getting around", a: "Car is essential for exploring beyond Castro and Ancud. The island's main road is paved; the side roads to the best churches and beaches are dirt. The ferry system connects the main island to smaller islands like Quinchao and Lemuy — essential for the best wooden churches. In Castro, everything is walkable." },
      { q: "How long", a: "Four nights. Day one: arrive Castro, palafitos, market. Day two: drive the church circuit (Achao, Quinchao by ferry). Day three: Parque Nacional Chiloé and Cucao beach. Day four: Dalcahue Sunday market, curanto lunch. Day five: slow departure. Chiloé rewards slow travel — the fog lifts at different times, the light changes constantly, and the island reveals itself gradually." },
      { q: "The mythology", a: "Chiloé has one of the richest mythological traditions in the Americas. The Trauco (a forest dwarf who seduces women), the Pincoya (a water spirit who controls fish abundance), and the Caleuche (a ghost ship crewed by dead sailors) are not fairy tales here — they're still taken seriously by many islanders. Ask about the mythology at your guesthouse. It explains the island's relationship with the sea." },
      { q: "Money", a: "Chiloé is excellent value. Tierra Chiloé all-inclusive: $500–700 USD. Hotel de Castro: $80–130. Guesthouse rooms: $30–60. A full seafood lunch at the Castro market: 5,000–8,000 CLP. The Dalcahue market empanadas: 800 CLP each. King crab (centolla) in a restaurant: 12,000–18,000 CLP. The island is one of the most affordable destinations in this guide." },
    ],
  },
  {
    name: "Carretera Austral", country: "chile", tag: "Road Trip · Wilderness · Patagonia Edge",
    hook: "1,200km of road through wilderness that has no equivalent on earth. Paved for about a third of it.",
    img: "https://images.unsplash.com/photo-1544636331-e26879cd4d9b?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=4; if(a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=4; if(a[5]?.includes("mountains")||a[5]?.includes("countryside")||a[5]?.includes("desert")) s+=3; if(a[6]?.includes("explore")) s+=4; if(a[7]?.includes("midrange")||a[7]?.includes("budget")) s+=1; if(a[8]?.includes("freedom")||a[8]?.includes("surprise")) s+=3; if(a[9]?.includes("explore")||a[9]?.includes("walk")) s+=3; if(a[8]?.includes("none")||a[8]?.includes("feel")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("rushed")) s+=2; if(a[6]?.includes("physical")||a[6]?.includes("spontaneous")) s+=2; return s; },
    intro: "The Carretera Austral — Route 7 — is a 1,240km road that runs through the Patagonian wilderness from Puerto Montt in the north to Villa O'Higgins in the south. Augusto Pinochet built it to connect remote communities that had no other land access. It passes through old-growth temperate rainforest, hanging glaciers, turquoise rivers, marble caves, and fjords that see almost no traffic. Roughly a third of it is paved. You need a 4WD, three weeks, and either to be very comfortable with dust and mud or to genuinely not care about either.",
    highlights: [
      { label: "Queulat National Park", text: "The Ventisquero Colgante (Hanging Glacier) — a glacier suspended between two rock faces, calving icebergs into a turquoise lagoon below. The hike to the viewpoint is 4km round trip through southern beech forest. One of the most dramatic landscapes on the Carretera." },
      { label: "Marble Caves (Cavernas de Mármol)", text: "Blue marble caves eroded by water into extraordinary formations at the edge of General Carrera Lake — the second-largest lake in South America. Accessible only by boat from Puerto Río Tranquilo. The light inside the caves changes color with the lake level." },
      { label: "Cochamo Valley", text: "The Yosemite of South America — a valley of granite walls that rival anything in California, accessible by a 4-hour trail from the town of Cochamo. Rock climbers discovered it; few others have followed." },
      { label: "Villa O'Higgins", text: "The end of the road. A tiny village at the southern terminus of the Carretera, accessible only by driving the full route or by a combination of ferry and foot from Patagonia. The feeling of arriving here is genuinely unlike anything else." },
    ],
    eat: [
      { name: "Roadside family restaurants (throughout)", desc: "The Carretera is not a restaurant route. The best meals are in family homes (casas de familia) that put out a handwritten sign offering lunch. Lamb stew, fresh trout, homemade bread. Nothing costs more than 5,000 CLP and the food is always good." },
      { name: "El Mosco (Cochrane)", desc: "The best restaurant in the southern Carretera. Lamb roasted over wood, fresh-caught Patagonian trout, homemade everything. In a town of 3,000 people at the edge of the world." },
      { name: "Alma Sur (Coyhaique)", desc: "The most serious restaurant on the Carretera, in the regional capital Coyhaique. Chilean Patagonian ingredients — lamb, trout, wild mushrooms, local berries — in a contemporary context." },
      { name: "Camping and self-catering", desc: "The real Carretera experience is cooking your own food at campgrounds. Buy supplies at the supermarkets in Puerto Montt or Coyhaique before heading into the wilderness — the small towns have little. A camp stove, good olive oil, and fresh trout bought from a roadside fisherman is the defining meal of the route." },
    ],
    stay: [
      { name: "El Pangue Lodge (near Palena)", tier: "High end", desc: "The only luxury lodge on the Carretera. On a lake in the wilderness, fly fishing, hiking, exceptional food. Extremely remote. The most expensive accommodation on the route and completely worth it if budget allows." },
      { name: "Casas de familia (throughout)", desc: "Family homes throughout the route offer rooms and breakfast for 15,000–25,000 CLP. The best way to experience the Carretera — families along the route are extraordinarily hospitable and the home-cooked meals are the food of the trip." },
      { name: "Camping (throughout)", tier: "Good value", desc: "The Carretera has excellent wild camping — pull off the road, set up a tent beside a river, wake up to glaciers. Organized campgrounds cost 5,000–10,000 CLP. Bring a good sleeping bag; temperatures drop below 5°C at night year-round." },,
      { name: "El Puesto Lodge (Cochrane)", tier: "Mid range", desc: "A fly-fishing and wilderness lodge near Cochrane, deep in the southern Carretera. The Cochrane River runs past the property. Guided hiking, kayaking, and the best dinner in 200km radius." },
    ],
    logistics: [
      { q: "When to go", a: "November–March only. Outside these months the weather makes the unpaved sections impassable and many services close entirely. January–February is peak season — the road gets as busy as it ever gets (which is still quiet by any normal standard). November and March are the best months: fewer vehicles, the same scenery, and the wildflowers in November are extraordinary." },
      { q: "Getting there", a: "Start in Puerto Montt (fly from Santiago) and drive south. The road begins with a ferry from La Arena to Puelche (30 minutes). Alternatively, fly to Balmaceda/Coyhaique (BBA) and drive a section from the middle. The full route one-way takes 2–3 weeks. Most people return to Santiago by flying from Balmaceda or continuing south to Torres del Paine." },
      { q: "The car", a: "You need a 4WD with high clearance. Rental agencies in Puerto Montt (Hertz, Budget) have suitable vehicles but book months ahead in peak season. Specify that you're doing the Carretera — some rental contracts prohibit unpaved roads. A spare tire (ideally two) is essential. Fuel stations are 100–200km apart in some sections — always fill up when you can." },
      { q: "Planning", a: "Download offline maps (Maps.me or Gaia GPS) before leaving Puerto Montt — mobile coverage disappears for 500km at a stretch. The Carretera Austral travel forums (especially on Reddit's r/solotravel) have current road condition reports. Book ferries in advance — the Hornopirén to Caleta Gonzalo ferry (required to continue south) has limited capacity and books out in January–February." },
      { q: "How long", a: "Two weeks for the northern section (Puerto Montt to Coyhaique). Three weeks for the full route to Villa O'Higgins. Most people do 2 weeks and find it transformative — the wilderness accumulates, the silence accumulates, and by day ten you start to feel like a different person. The route cannot be rushed." },
      { q: "Money", a: "The Carretera is cheap by default — there's nowhere to spend money. Campgrounds: 5,000–10,000 CLP. Family home rooms: 15,000–25,000 CLP. Meals at roadside restaurants: 5,000–10,000 CLP. El Pangue Lodge: $400–600 USD per night (extreme outlier). Budget $60–80 USD per day for two people including fuel, food, and accommodation." },
    ],
  },
  {
    name: "Torres del Paine", country: "chile", tag: "Patagonia · Granite Towers · Trek",
    hook: "The most dramatic mountain scenery on earth. Yes, it lives up to it.",
    img: "https://images.unsplash.com/photo-1501854140801-50d01698950b?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")) s+=4; if(a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=3; if(a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=4; if(a[5]?.includes("mountains")) s+=4; if(a[6]?.includes("explore")) s+=3; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=1; if(a[8]?.includes("beauty")||a[8]?.includes("freedom")) s+=3; if(a[9]?.includes("explore")||a[9]?.includes("walk")) s+=3; if(a[8]?.includes("deep")||a[8]?.includes("article")) s+=2; if(a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=2; if(a[6]?.includes("physical")||a[6]?.includes("fullday")) s+=2; return s; },
    intro: "Torres del Paine is 2,400 square kilometers of Patagonian wilderness in southern Chile built around three granite towers that rise 2,800 meters from the steppe. The wind is extraordinary — 100km/h gusts are normal. The light changes every fifteen minutes. The towers turn pink at dawn for about eight minutes and the color is not reproducible in a photograph. The W trek (four to five days, hut-to-hut) is the most popular long-distance hike in South America. The full circuit (eight to ten days) is one of the great wilderness experiences on earth.",
    highlights: [
      { label: "The towers at dawn", text: "A 5am wake-up, a 2.5-hour hike in the dark, and the reward: standing at the mirador below the Torres as the sun rises and turns the granite pink-orange-gold over the course of eight minutes. Every photograph you've ever seen doesn't capture it. Go on your first morning — weather changes fast." },
      { label: "The W Trek", text: "Four to five days, hut-to-hut, covering the three main valleys of the park. Los Torres (the towers), Valle del Francés (hanging glaciers, condors), and Glaciar Grey (a 6km-wide glacier calving into a lake). The full W is achievable for anyone in reasonable fitness." },
      { label: "Glaciar Grey", text: "A glacier 6km wide and 30 meters high at its face. Icebergs calve off the front and float across the lake. You can kayak among them — one of the stranger and more beautiful experiences in Patagonia." },
      { label: "The Patagonian steppe", text: "Outside the park, the steppe stretches to Argentina. Guanacos (wild llamas), condors, rheas, and pumas live here. The Torres del Paine puma population is dense and habituated to people — a guided puma safari is the best wildlife experience in South America." },
    ],
    eat: [
      { name: "Refugio lodges (inside the park)", desc: "The hut network (Fantastico Sur and Vertice Patagonia) serves hot meals at each lodge — hearty Patagonian stew, pasta, grilled lamb. Not gourmet but deeply satisfying after a full day's hiking. Pre-book meals with your accommodation." },
      { name: "Singular Patagonia (Puerto Natales)", desc: "The best restaurant in the region, in the Singular hotel in Puerto Natales. Patagonian lamb, centolla, local vegetables, an extraordinary wine list of Chilean bottles. The tasting menu is the way to eat before or after a trek." },
      { name: "Afrigonia (Puerto Natales)", desc: "Chilean-African fusion restaurant run by a Kenyan-Chilean couple in Puerto Natales. Unusual, genuinely delicious, and the most interesting restaurant in southern Chile. Book ahead." },
      { name: "Asado at an estancia", desc: "The traditional Patagonian estancia (sheep farm) lunch: whole lamb slow-roasted on a cross-spit over a wood fire, eaten outside with a view of the steppe. Estancia Cerro Guido and Estancia Nibepo Aike both do this for guests." },
    ],
    stay: [
      { name: "EcoCamp Patagonia", tier: "High end", desc: "Geodesic dome tents inside the park with en-suite bathrooms, heating, and extraordinary views of the Torres. The most beautiful accommodation in the park. All excursions included." },
      { name: "Singular Patagonia (Puerto Natales)", tier: "High end", desc: "Converted cold-storage factory in Puerto Natales, 1.5 hours from the park. Extraordinary design, the best restaurant in the region, the best base for a non-camping Paine visit." },
      { name: "Refugio huts (W Trek)", tier: "Good value", desc: "The hut network inside the park — Chileno, Los Cuernos, Paine Grande, Grey. Dormitory beds and private rooms available. Book through Fantastico Sur and Vertice Patagonia websites 6–12 months ahead for peak season." },,
      { name: "Awasi Patagonia", tier: "High end", desc: "Eight private villas in the park with dedicated guides and vehicles for each group. The most personalised Torres del Paine experience — your own schedule, your own guide, no group tours. The puma safari here has the highest success rate in the park." },
    ],
    logistics: [
      { q: "When to go", a: "November–March. The park is open year-round but the huts and most lodges close April–October. Peak season is December–February — book accommodation 6–12 months ahead. November and March are the best months: fewer people, often better weather. The Patagonian weather is famously unpredictable — four seasons in one day is normal. Pack for everything." },
      { q: "Getting there", a: "Fly to Punta Arenas (PUQ) from Santiago (3.5 hours, multiple daily flights). From Punta Arenas, take the bus to Puerto Natales (3 hours, several daily). From Puerto Natales, buses to the park run twice daily in season (2.5 hours). Most people base in Puerto Natales and enter the park for the trek. Some fly directly to Puerto Natales (PMC) in season." },
      { q: "Booking the W Trek", a: "Book the refugio accommodation 6–12 months ahead for December–February. Fantastico Sur and Vertice Patagonia manage the hut network — book directly on their websites. A 5-day W trek costs $300–600 USD in accommodation alone depending on private vs dormitory rooms. Bring your own food (buy in Puerto Natales before entering) or pre-book meals at each hut." },
      { q: "What to pack", a: "The Patagonian wind will test every piece of gear you own. Essentials: a genuinely waterproof hardshell (not water-resistant), warm mid-layers, waterproof hiking boots that are broken in, trekking poles (essential on the terrain), a quality sleeping bag rated to -5°C, and buff/neck gaiter for the wind. Bring more layers than you think you need." },
      { q: "The puma safari", a: "Torres del Paine has one of the highest densities of pumas in the world and they're habituated to vehicles. Puma safari tours (Cascada Expediciones, Fantastico Sur) run 4–6 hours, usually at dawn or dusk, with a specialized tracker and guide. Sightings are not guaranteed but the success rate is extremely high in October–March. One of the great wildlife experiences on earth." },
      { q: "Money", a: "Park entry: $21,000 CLP ($21 USD). EcoCamp Patagonia: $500–900 USD per night all-inclusive. W Trek huts: $60–120 per night per person. Singular Patagonia: $400–700. Puerto Natales guesthouses: $40–90. Meals in Puerto Natales: 10,000–20,000 CLP. Budget $150–200 USD per day for the W Trek including accommodation and meals." },
    ],
  },
  {
    name: "Chilean Fjords", country: "chile", tag: "Remote · Glaciers · Almost No One Goes",
    hook: "One of the most remote and extraordinary landscapes on earth. Almost nobody goes. That's the point.",
    img: "https://images.unsplash.com/photo-1614728423169-3f65fd722b7e?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("adventure")) s+=4; if(a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("wild")) s+=5; if(a[5]?.includes("mountains")||a[5]?.includes("coast")||a[5]?.includes("desert")) s+=2; if(a[6]?.includes("explore")||a[6]?.includes("nothing")) s+=3; if(a[7]?.includes("flexible")||a[7]?.includes("open")) s+=2; if(a[8]?.includes("quiet")||a[8]?.includes("freedom")) s+=4; if(a[9]?.includes("sit")||a[9]?.includes("explore")) s+=2; if(a[8]?.includes("none")||a[8]?.includes("people")) s+=2; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=3; if(a[6]?.includes("physical")||a[6]?.includes("nothing")) s+=1; return s; },
    intro: "The Chilean fjords stretch for 1,500km from Puerto Montt in the north to Cape Horn in the south — a labyrinth of channels, glaciers, and islands that receives less than 1,000 visitors per year in its more remote sections. The Navimag ferry, which runs from Puerto Montt to Puerto Natales over four days, passes through the heart of the fjords and is one of the great slow travel experiences on earth. The Skorpios cruise lines offer more curated access to glaciers and hot springs that no road reaches. This is what the planet looks like when humans haven't touched it.",
    highlights: [
      { label: "The Navimag ferry", text: "A working cargo and passenger ferry that runs the full length of the fjords from Puerto Montt to Puerto Natales over four days. The scenery is extraordinary — hanging glaciers, sea lion colonies, dolphins in the bow wake. Not a cruise ship — a real ferry with cabins and a dining room. The experience of slow passage through complete wilderness is the point." },
      { label: "Laguna San Rafael", text: "A glacier that descends directly from the Northern Patagonian Ice Field into a sea lagoon — accessible only by boat or small plane. The glacier face is 70 meters high and 4km wide. Icebergs the size of houses float in the lagoon. The Skorpios II cruise visits it." },
      { label: "Hot springs at Quitralco", text: "Natural hot springs in a remote fjord that you can only reach by boat. The Skorpios cruises stop here — passengers soak in geothermal pools carved into the rock with glaciers visible from the water. One of the stranger and more beautiful experiences in Chile." },
      { label: "Cape Horn", text: "The southernmost point of South America, where the Pacific and Atlantic meet. A lighthouse keeper lives here with their family — one of the most remote postings on earth. Accessible by boat from Puerto Williams. Most visitors see it from a ship's deck." },
    ],
    eat: [
      { name: "Navimag dining room", desc: "The ferry has a dining room serving three meals a day — Chilean home cooking, local seafood, good simple food. Order the cazuela de centolla if it appears on the menu. The wine list is basic but adequate. Eat on the deck when the weather allows." },
      { name: "Skorpios cruise dining", desc: "The Skorpios cruises serve more refined Chilean cuisine — centolla, merluza austral (southern hake), local lamb, Chilean wines. The meals are part of the all-inclusive package and the quality is genuinely good." },
      { name: "Puerto Williams restaurant scene", desc: "Puerto Williams (the world's southernmost city) has a handful of restaurants serving end-of-the-world cooking — Patagonian lamb, fresh-caught southern fish, homemade everything. The Dientes de Navarino trek departs from here." },
    ],
    stay: [
      { name: "Skorpios III Cruise", tier: "High end", desc: "The premium way to see the fjords — a 7-day cruise with 70 passengers, visiting glaciers, fjords, and hot springs that no road reaches. All-inclusive, Chilean-crewed, extraordinary." },
      { name: "Navimag Ferry (cabin)", tier: "Mid range", desc: "Four days from Puerto Montt to Puerto Natales through the full length of the fjords. Cabins range from AAA (4-berth, shared bathroom) to AA (2-berth, private bathroom). Not glamorous — genuinely extraordinary. Book at navimag.com." },
      { name: "Puerto Williams Guesthouses", tier: "Good value", desc: "Simple guesthouses in the world's southernmost city. The base for the Dientes de Navarino circuit (the southernmost trek on earth, 5 days, no infrastructure). Ask at the Chilean Navy base about the trek conditions." },,
      { name: "Río Serrano Hotel (Torres del Paine border)", tier: "Mid range", desc: "A hotel on the Río Serrano at the western entrance to Torres del Paine — the arrival point for the Navimag ferry passengers. Hot tub overlooking the river, the park entrance 20 minutes away." },
    ],
    logistics: [
      { q: "When to go", a: "November–March. The Navimag runs year-round but the fjords are most accessible in summer. The Skorpios cruises run October–April. Outside these months the weather makes the southern fjords genuinely dangerous. November and March are less crowded than December–February." },
      { q: "Getting there", a: "Puerto Montt (PMC) is the gateway for the Navimag and Skorpios departures — fly from Santiago (1.5 hours). The Navimag departs Puerto Montt every Friday evening, arriving Puerto Natales on Tuesday morning. The Skorpios cruises depart from Puerto Montt and Quellón (Chiloé). Book both at least 3 months ahead in peak season." },
      { q: "Navimag vs Skorpios", a: "Navimag is a working ferry — basic cabins, mixed passengers, real Chile. The fjord scenery is extraordinary but you share it with cargo trucks. Cost: $400–800 USD per person one way depending on cabin class. Skorpios is a dedicated cruise — smaller ship, more comfort, curated glacier stops. Cost: $2,500–4,000 USD per person for 7 days. Both are completely different experiences and both are worth doing." },
      { q: "What to expect on the Navimag", a: "Four days at sea in the fjords. Bring books, warm layers, waterproofs, and sea sickness medication if needed. The ship sails through the open Pacific for one stretch (the Golfo de Penas) which can be rough. Most of the route is sheltered channels. The bar stays open until midnight. You will see glaciers, dolphins, albatrosses, and almost no other signs of human life." },
      { q: "How long", a: "The Navimag is four days one way. Skorpios cruises are 5–7 days. Most people combine the fjords with Torres del Paine — fly into Punta Arenas, trek, then take the Navimag north back to Puerto Montt. Or take the Navimag south as an entry to Patagonia and continue to the park." },
      { q: "Money", a: "Navimag cabin: $400–800 USD one way per person. Skorpios III cruise: $2,500–4,000 USD per person all-inclusive. Meals on the Navimag are included in the cabin price. Puerto Williams guesthouses: $30–60 per night. This is not a budget destination — the remoteness means everything costs more." },
    ],
  },
];

// ─── ICELAND REGIONS ───────────────────────────────────────────────────────────
const icelandRegions = [
  {
    name: "Reykjavík", country: "iceland", tag: "City · Northern Lights · Golden Circle",
    hook: "The world's most northerly capital. Smaller than you think, stranger than you expect, and the Golden Circle is right outside the door.",
    img: "https://images.unsplash.com/photo-1474690455603-a369ec1293a5?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=2; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("cities")||a[5]?.includes("mountains")) s+=2; if(a[6]?.includes("wander")||a[6]?.includes("eat")) s+=2; if(a[1]?.includes("partner")||a[1]?.includes("friends")) s+=1; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("article")||a[8]?.includes("people")) s+=1; if(a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=1; return s; },
    intro: "Reykjavík is a city of 130,000 people that somehow contains a world-class restaurant scene, a music culture completely disproportionate to its size, and the kind of bar life that starts at midnight and goes until the sun comes up — which in summer it barely sets. The Golden Circle (Þingvellir, Geysir, Gullfoss) is an hour away and worth doing on day one. But the city itself rewards staying — the Hallgrímskirkja at dawn, the Reykjanes Peninsula thermal pools, the harbour fish market at 8am. Most people treat Reykjavík as a transit stop. That's a mistake.",
    highlights: [
      { label: "Hallgrímskirkja and the view", text: "The brutalist Lutheran church that dominates the skyline. Take the elevator to the tower for the definitive Reykjavík view — the coloured rooftops, the harbour, the mountains across the bay. Go at dawn or in the blue hour before sunset." },
      { label: "The Golden Circle day trip", text: "Þingvellir (where the Eurasian and North American tectonic plates meet visibly above ground, and where Iceland's parliament was founded in 930 AD), Geysir (the geyser that gave all geysers their name, erupts every 5–10 minutes), and Gullfoss (a two-tiered waterfall of extraordinary power). Do it on your first full day, start early, be back by 3pm." },
      { label: "ION Adventure Hotel", text: "A modernist hotel built on a lava field 45 minutes from Reykjavík near Þingvellir. Floor-to-ceiling windows designed for northern lights viewing, a geothermal pool on the lava, extraordinary architecture that disappears into the landscape. Justin Bieber stayed here — that's how it got famous. The hotel earned that attention." },
      { label: "The food scene", text: "Reykjavík punches significantly above its weight. Dill (one Michelin star, New Nordic built entirely on Icelandic ingredients) is the landmark. Matur og Drykkur does traditional Icelandic food — hákarl, skyr, lamb head — made actually delicious. The Hlemmur Mathöll food hall is the daytime version." },
      { label: "Laugardalslaug", text: "The locals' outdoor swimming pool — geothermally heated, open year-round, multiple hot pots at different temperatures. Icelanders treat the pools as social infrastructure. Go early morning before work, sit in a hot pot at 44°C, watch the city wake up. €8 entry. The most Reykjavík thing you can do." },
    ],
    eat: [
      { name: "Dill", desc: "The only Michelin-starred restaurant in Iceland. Gunnar Karl Gíslason's New Nordic menu changes constantly and uses only Icelandic ingredients — lamb, skyr, arctic char, wild herbs, seaweed. The tasting menu is €120–150. Book months ahead." },
      { name: "Matur og Drykkur", desc: "Traditional Icelandic ingredients made into food people actually want to eat. The salted cod's head, the slow-roasted lamb, the skyr desserts. One of the most interesting restaurants in northern Europe." },
      { name: "Grillmarket", desc: "The best Icelandic lamb in Reykjavík, grilled over lava stones. Arctic char, langoustines, reindeer in season. The wine list is serious. Go for dinner on your last night." },
      { name: "Brauð & Co", desc: "The bakery that Reykjavík queues for every morning. The cinnamon rolls are what Instagram is for. Arrive at 7:30am — they sell out. On Skólavörðustígur, the street leading up to Hallgrímskirkja." },
      { name: "Hlemmur Mathöll", desc: "The converted bus station food hall. Langoustine soup, lamb tacos, Korean-Icelandic fusion, natural wine bar. The best lunch option in the city — go Thursday to Sunday when all the stalls are open." },
    ],
    stay: [
      { name: "ION Adventure Hotel", tier: "High end", desc: "45 minutes from the city on a lava field. The northern lights experience of Iceland — floor-to-ceiling windows, geothermal pool, extraordinary design. Worth the trip out of the city." },
      { name: "Hotel Borg", tier: "High end", desc: "The original Reykjavík grand hotel, opened 1930, on Austurvöllur square. Art Deco interiors, central location, the most characterful city hotel in Iceland." },
      { name: "Guesthouse Óðinn", tier: "Mid range", desc: "Clean, well-run guesthouse in the 101 district, walking distance to everything. The best mid-range option in central Reykjavík — book ahead in summer." },,
      { name: "Apotek Hotel", tier: "Mid range", desc: "A converted 1917 apothecary in central Reykjavík — original pharmacy fittings, exposed brick, the best location in the city for walking to everything. Significantly more character than the standard Reykjavík business hotel." },,
      { name: "Hilton Reykjavík Nordica", tier: "Mid range", desc: "The practical family choice in Reykjavík — spacious rooms, reliable service, a pool, parking, and easy access to both the city centre and the Ring Road north. Not the most atmospheric hotel in Iceland but it delivers everything a family needs without drama." },
    ],
    logistics: [
      { q: "When to go", a: "Depends entirely on what you want. Northern lights: September–March (dark enough to see them, but not guaranteed). Midnight sun: June–July (sun sets briefly or not at all, extraordinary light). Puffins: May–August (they nest on the Reykjanes cliffs and on Heimaey island). The Golden Circle and most day trips are year-round. July–August is peak season — prices spike 40–60% and accommodation books out months ahead." },
      { q: "Getting there", a: "Keflavík International Airport (KEF) is 45 minutes from Reykjavík. Flybus runs every 30 minutes to the BSÍ bus terminal in the city (€25 each way). Uber doesn't operate — taxis are expensive (€70–90 from the airport). Rent a car at the airport if you're planning to leave the city at any point — driving Iceland is the point." },
      { q: "Getting around Reykjavík", a: "The city is entirely walkable — the 101 district (the centre) is compact. Strætó buses cover the wider city. For day trips (Golden Circle, Reykjanes, Snæfellsnes) you need a car or a guided tour. Car rental is available at the airport and in the city — book ahead in summer. An SUV or 4WD is essential for anything off the Ring Road." },
      { q: "The northern lights", a: "Not guaranteed anywhere in Iceland at any time. The conditions required: clear sky, darkness, and solar activity (measured in Kp index). The Icelandic Met Office app (vedur.is) gives a 3-day aurora forecast. If the Kp index is above 3 and the sky is clear, drive 20 minutes from the city to escape light pollution and look north. October–February are the most reliable months. Patience is required." },
      { q: "How long", a: "Three nights in Reykjavík minimum. Day one: Golden Circle. Day two: city — Hallgrímskirkja, Laugardalslaug, dinner at Dill. Day three: Reykjanes Peninsula (the Blue Lagoon is nearby, book ahead, or the lesser-known Krýsuvík geothermal area for free). Day four: depart or continue to Snæfellsnes or the South Coast." },
      { q: "Money", a: "Iceland is expensive — one of the most expensive countries in Europe. A coffee: €5–6. A beer: €10–12. Dinner at a good restaurant: €60–100 per person. Dill tasting menu: €120–150. Hotel Borg: €200–350. Guesthouse Óðinn: €120–180. The Golden Circle self-drive: fuel + parking (free at most sites). Budget €250–350 per person per day for a mid-range Iceland trip." },
    ],
  },
  {
    name: "South Coast", country: "iceland", tag: "Glaciers · Black Sand · Jökulsárlón",
    hook: "A glacier lagoon where icebergs calve into the sea. Black sand beaches where the Atlantic tries to take you. Waterfalls you can walk behind. All on one road.",
    img: "https://images.unsplash.com/photo-1504829857797-ddff29c27927?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("beauty")||a[0]?.includes("escape")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("balanced")) s+=2; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("mountains")||a[5]?.includes("coast")||a[5]?.includes("desert")) s+=3; if(a[6]?.includes("explore")||a[6]?.includes("physical")) s+=3; if(a[7]?.includes("midrange")||a[7]?.includes("flexible")) s+=1; if(a[8]?.includes("feel")||a[8]?.includes("article")) s+=2; if(a[9]?.includes("rushed")||a[9]?.includes("generic")) s+=2; if(a[6]?.includes("fullday")) s+=2; return s; },
    intro: "The South Coast of Iceland runs 250km east from Reykjavík along the foot of the Vatnajökull ice cap — Europe's largest glacier — to Jökulsárlón, the lagoon where icebergs calve directly into the sea. Along the way: Skógafoss (a 60-metre waterfall with a path behind it), Reynisfjara (the black sand beach with basalt columns where the Atlantic arrives with genuine violence), and Seljalandsfoss (the waterfall you walk behind at dusk when the light turns gold). Most people do it as a long day trip from Reykjavík. Staying overnight lets you have the glacier lagoon at dawn before anyone else arrives.",
    highlights: [
      { label: "Jökulsárlón glacier lagoon", text: "The lagoon where Vatnajökull calves icebergs into a tidal lake before they drift to the sea. The icebergs are blue-white and translucent. Seals swim between them. Diamond Beach is immediately adjacent — the black sand beach where smaller icebergs wash up and melt. Go at dawn: the light turns the ice pink and the tour buses haven't arrived." },
      { label: "Skógafoss", text: "A 60-metre waterfall on the edge of the former Icelandic coastline. You can walk directly to the base and behind the curtain of water. In winter it freezes partially and ice climbers work the face. The 500-step staircase to the top leads to a hiking trail that goes east for days." },
      { label: "Reynisfjara black sand beach", text: "The most dangerous beach in Iceland — the sneaker waves here have killed people and the warning signs are serious. Stand back from the water. The basalt column formations (Reynisdrangar) rise from the sea like organ pipes. The black sand is volcanic and warm to the touch in summer. Extraordinary." },
      { label: "Vatnajökull glacier hikes", text: "The glacier that covers 8% of Iceland can be accessed from multiple points along the South Coast. Skaftafell is the main access point — guided glacier hikes last 2–3 hours and require crampons and ice axe (all provided). One of the most disorienting experiences in Iceland — standing on 1,000 metres of ice that's been there for 10,000 years." },
    ],
    eat: [
      { name: "Café Skógafoss", desc: "The café at the base of the falls. Lamb soup, skyr with berries, hot chocolate after the walk behind the waterfall. Nothing fancy — everything needed." },
      { name: "Foss Hotel Glacier Lagoon restaurant", desc: "The only serious restaurant near Jökulsárlón. Icelandic lamb, fresh-caught arctic char, local dairy. Go for dinner and request a window seat for the last of the evening light on the lagoon." },
      { name: "Víkurprjón (Vík)", desc: "The village of Vík is the only real stopping point on the South Coast. The bakery here does the best lamb soup in southern Iceland — thick, rich, served with dark bread. Eat it in the car with the rain on the windshield." },
    ],
    stay: [
      { name: "Fosshotel Glacier Lagoon", tier: "High end", desc: "The hotel closest to Jökulsárlón — modern, well-designed, aurora-watching from the rooms in winter. Being here at dawn before the lagoon fills with tour buses is the reason to stay." },
      { name: "Skógafoss Camping", tier: "Good value", desc: "The campsite directly at the foot of Skógafoss waterfall. Wake up to the mist and the sound of 60 metres of falling water. Geothermally heated showers. €15 per tent. The best campsite in Iceland." },
      { name: "Guesthouses in Vík", tier: "Mid range", desc: "The village of Vík has a cluster of guesthouses — Icelandair Hotel Vík and Puffin Hotel Vík are the most reliable. Base here for Reynisfjara in the morning before the day trippers from Reykjavík arrive." },,
      { name: "Hörgsland Guesthouse (Vík area)", tier: "Good value", desc: "A working farm guesthouse near Vík with mountain views and home-cooked dinners using the farm's own lamb. The most honest South Coast accommodation — wake up to sheep in the field, drive to Reynisfjara in 15 minutes." },
    ],
    logistics: [
      { q: "When to go", a: "Year-round but different seasons offer different things. Winter (November–February): northern lights over the glacier lagoon, ice climbing on Skógafoss, the beaches completely empty. Summer (June–August): midnight sun, puffins on the Reynisfjara cliffs, Vatnajökull accessible for glacier hiking. The South Coast road (Ring Road east) is open year-round but winter driving requires a 4WD and careful weather monitoring." },
      { q: "Getting there", a: "Drive east from Reykjavík on Route 1 (the Ring Road). Skógafoss is 1.5 hours, Reynisfjara 2 hours, Vík 2.5 hours, Jökulsárlón 4.5 hours. A car is the only practical option — there's a bus but it doesn't serve the smaller sites. Allow a full day minimum for Jökulsárlón; two days if you want the glacier hike and the lagoon at dawn." },
      { q: "Safety", a: "The South Coast has genuine hazards. Reynisfjara sneaker waves kill people — stay well back from the water and watch for the warning signs. Glacier hiking requires a certified guide — do not walk on Vatnajökull without one. South Coast weather changes fast — what starts as overcast can become a full storm in 30 minutes. Check vedur.is before driving." },
      { q: "How long", a: "One long day from Reykjavík gets you to Jökulsárlón and back but you'll be exhausted and rush everything. Two nights is right: night one in Vík (Reynisfjara, Skógafoss), night two near Jökulsárlón (glacier hike in the afternoon, lagoon at dawn). Then continue east to the East Fjords or return to Reykjavík." },
      { q: "Money", a: "Glacier hike with a guide: €60–80. Fosshotel Glacier Lagoon: €200–350. Skógafoss camping: €15. A bowl of lamb soup in Vík: €15–18. The glacier lagoon itself has no entry fee — boat tours on the lagoon cost €45–60. Petrol is expensive — fill up in Reykjavík and again in Vík." },
    ],
  },
  {
    name: "Snæfellsnes Peninsula", country: "iceland", tag: "Glacier · Fishing Villages · Verne's Iceland",
    hook: "Jules Verne set the entrance to the center of the earth here. The glacier that inspired him is still there, still active, and still almost empty.",
    img: "https://images.unsplash.com/photo-1476610182048-b716b8518aae?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=3; if(a[6]?.includes("explore")||a[6]?.includes("physical")) s+=3; if(a[1]?.includes("partner")||a[1]?.includes("solo")) s+=2; if(a[8]?.includes("feel")||a[8]?.includes("people")) s+=2; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("fullday")) s+=2; return s; },
    intro: "The Snæfellsnes Peninsula juts 90km into the Atlantic from the west coast of Iceland, crowned by the Snæfellsjökull glacier — the volcano Jules Verne used as the entrance to the center of the earth in his 1864 novel. The glacier is visible from Reykjavík on clear days, 120km away. The peninsula itself is a compressed version of everything Iceland does — black lava beaches, dramatic sea cliffs, hot springs, fishing villages that haven't changed since the 1950s, and almost none of the tourist infrastructure that crowds the South Coast. Arnarstapi and Hellnar are the two villages worth stopping in. Djúpalónssandur is the black pebble beach where you lift the weights the old fishermen used as strength tests to earn their place on a boat.",
    highlights: [
      { label: "Snæfellsjökull glacier", text: "A 700,000-year-old glacier sitting on top of an active volcano. The glacier has been retreating — scientists predict it will be gone by 2050. Summit hikes are available with guides from Arnarstapi. The walk around the base of the volcano through the lava field takes a full day. Snæfellsjökull National Park is free to enter." },
      { label: "Djúpalónssandur", text: "The black pebble beach at the base of the Snæfellsjökull lava field. Four lifting stones sit on the beach — Fullsterkur (full strength, 154kg), Hálfsterkur (half strength, 54kg), Hálfdrættingur (weakling, 23kg), Amlóði (useless, 18kg). Fishermen had to lift Hálfsterkur to earn a place on a boat. Try them. Rusting shipwreck debris from a 1948 British trawler is scattered across the beach." },
      { label: "Arnarstapi and Hellnar", text: "Two tiny fishing villages on the south coast of the peninsula, connected by a 2.5km coastal path along the cliffs. The path passes sea arches, nesting Arctic terns, basalt columns, and caves carved by the Atlantic. Walk it in either direction, take the other road back." },
      { label: "Kirkjufell mountain", text: "The most photographed mountain in Iceland — a conical peak rising from the coast near Grundarfjörður on the north side of the peninsula. The waterfall (Kirkjufellsfoss) in the foreground is what makes the composition. Game of Thrones filmed here. Go at dawn or blue hour. The short hike to the base of the falls takes 20 minutes." },
    ],
    eat: [
      { name: "Fjöruhúsið (Hellnar)", desc: "A café in a turf-roofed house on the cliff above the sea at Hellnar. The fish soup is made with whatever came off the boat. Arctic terns dive at your head outside. One of the most atmospheric lunch spots in Iceland." },
      { name: "Vegamót (Snæfellsbær)", desc: "The petrol station and grill that feeds most of the peninsula. Lamb burger, fish and chips, hot dog (the Icelandic hot dog with remoulade is a national institution). Order the hot dog." },
      { name: "Bjargarsteinn Mathús (Grundarfjörður)", desc: "The best restaurant on the peninsula, on the north coast near Kirkjufell. Fresh langoustines, local lamb, arctic char. Small room, book ahead in summer." },
    ],
    stay: [
      { name: "Hotel Búðir", tier: "High end", desc: "A black wooden hotel standing alone on a lava field, next to Iceland's oldest wooden church. No neighbours, no village — just the glacier, the lava, the sea, and the northern lights in winter. One of the most atmospheric hotels in Iceland." },
      { name: "Freezer Hostel (Hellissandur)", tier: "Good value", desc: "Converted fish freezing factory turned hostel and arts space on the western tip of the peninsula. Artists in residence, live music, the most interesting budget accommodation in western Iceland." },
      { name: "Arnarstapi Guesthouses", tier: "Mid range", desc: "Several family-run guesthouses in Arnarstapi. Simple rooms, home-cooked breakfasts, walking distance to the coastal path. The most honest mid-range experience on the peninsula." },,
      { name: "Hótel Hellissandur", tier: "Good value", desc: "A simple, clean guesthouse in the fishing village of Hellissandur on the western tip of the peninsula. Family-run, good breakfast, the Freezer Hostel arts programme next door, and the glacier visible from the window." },
    ],
    logistics: [
      { q: "When to go", a: "May–October for hiking and the coastal path. June–July for 24-hour daylight and puffins nesting on the sea cliffs. Winter (November–March) for northern lights — the peninsula's low light pollution makes it one of the best aurora-viewing spots in Iceland. The glacier is accessible year-round but summit hikes close in winter without specialist equipment." },
      { q: "Getting there", a: "2.5 hours from Reykjavík by car on Route 54. No public transport serves the peninsula adequately — a car is essential. The full circuit of the peninsula on Route 54 and Route 574 takes 4–5 hours without stops. Allow a full day minimum, two days to do it properly." },
      { q: "Getting around", a: "The peninsula road (Route 574) circumnavigates the entire thing — paved, manageable in a 2WD in summer, requires 4WD in winter. The F-roads into the interior of the national park require a 4WD. The coastal path between Arnarstapi and Hellnar is on foot only — 2.5km, flat, extraordinary." },
      { q: "How long", a: "Two nights. Day one: drive from Reykjavík, Djúpalónssandur, Arnarstapi to Hellnar coastal walk, Hotel Búðir check-in. Day two: glacier base hike or summit (with guide), Kirkjufell on the north coast, drive back to Reykjavík via Grundarfjörður. The peninsula also works as a one-night extension to a South Coast trip." },
      { q: "Money", a: "Hotel Búðir: €200–350. Arnarstapi guesthouses: €90–150. Freezer Hostel: €40–70. Fjöruhúsið lunch: €20–30. Glacier guide for summit: €80–120. Snæfellsjökull National Park entry: free. The peninsula is significantly cheaper than Reykjavík — accommodation and food costs drop noticeably once you leave the capital." },
    ],
  },
  {
    name: "Westfjords", country: "iceland", tag: "Remote · Dramatic · Almost No One Goes",
    hook: "The most dramatic fjords in Iceland. The worst roads in Iceland. The fewest tourists in Iceland. All three of those things are the point.",
    img: "https://images.unsplash.com/photo-1518459031867-a89b944bffe4?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("adventure")) s+=4; if(a[3]?.includes("explorer")) s+=5; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=5; if(a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=3; if(a[6]?.includes("explore")||a[6]?.includes("physical")) s+=3; if(a[1]?.includes("solo")||a[1]?.includes("partner")) s+=2; if(a[8]?.includes("none")||a[8]?.includes("people")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=4; if(a[6]?.includes("spontaneous")||a[6]?.includes("fullday")) s+=2; return s; },
    intro: "The Westfjords are a peninsula in the northwest of Iceland connected to the rest of the country by a 7km neck of land. The roads are gravel, the fjords are deep, the waterfalls come off the cliffs directly onto the beach, and the area receives roughly 10% of Iceland's total tourism. Látrabjarg is the westernmost point in Europe and one of the largest seabird cliffs on earth — puffins nest in the grass at your feet. Dynjandi is a waterfall that fans out in seven cascades before it hits the fjord. Ísafjörður is the only real town — 3,000 people, a fish factory, a surprisingly good restaurant, and a music festival in the winter when the sun doesn't rise for two months.",
    highlights: [
      { label: "Dynjandi waterfall", text: "The waterfall that defines the Westfjords — it fans out from a narrow top into a 100-metre wide base, dropping in seven named cascades down the cliff into the fjord. The path to the top passes all seven falls. No fence, no barrier, no queue. Walk directly behind the spray. The most extraordinary waterfall in Iceland." },
      { label: "Látrabjarg sea cliffs", text: "The westernmost point of Europe. A 14km cliff face rising 440 metres above the Atlantic, home to millions of seabirds — razorbills, guillemots, and puffins. The puffins nest in burrows in the grass at the cliff edge and will let you approach to within a metre. Don't go past the cliff edge — the drop is vertical." },
      { label: "Ísafjörður", text: "The Westfjords' only real town, in a fjord so narrow the mountains on both sides block the sun for two months in winter. The old timber merchant houses on the harbour are the best-preserved in Iceland. The Westfjords Heritage Museum explains exactly how isolated these communities were before roads were built in the 1970s." },
      { label: "The fjord drives", text: "The Westfjords roads cut in and out of fjord after fjord — each one a different shade of blue-grey, each with its own waterfall coming off the plateau above. There's no efficient route. That's the point. Drive without a destination and stop whenever the view earns it." },
    ],
    eat: [
      { name: "Tjöruhúsið (Ísafjörður)", desc: "A fish restaurant in a 200-year-old warehouse on the harbour. One sitting per night, one menu — whatever was caught. Communal tables, fish chowder, pan-fried catch, Icelandic bread. One of the great restaurant experiences in Iceland. Book the day before." },
      { name: "Húsið (Ísafjörður)", desc: "The town's main café and bar. Lamb soup, sandwiches, the only decent coffee in the Westfjords. Where everyone goes. Fills up at lunch — arrive early." },
      { name: "Seljalandslaug hot pot (Dynjandi)", desc: "A geothermal pool on the fjord shore near Dynjandi. Free, unsupervised, temperature varies by season. Soak in the pool while looking at the fjord. No facilities, no charge, no one around." },
    ],
    stay: [
      { name: "Hotel Ísafjörður", tier: "Mid range", desc: "The main hotel in the Westfjords' only town. Clean, comfortable, the base for exploring the northern Westfjords. The staff know the roads and the current conditions — ask them before driving anywhere remote." },
      { name: "Heydalur Guesthouse", tier: "Mid range", desc: "A farm guesthouse in the Westfjords interior with geothermal pools, horses, and absolute silence. One of the most remote guesthouses in Iceland. The family that runs it has been there for generations." },
      { name: "Wild camping", tier: "Good value", desc: "Wild camping is legal in Iceland on uncultivated land — pitch a tent on the fjord shore, wake up to the waterfall. The freedom is genuine. Bring everything you need — facilities don't exist in the remote Westfjords." },,
      { name: "Gamla Gistiheimilið (Ísafjörður)", tier: "Good value", desc: "A guesthouse in one of the original timber merchant houses in Ísafjörður's old harbour district. Basic rooms, extraordinary building, the harbour outside the window. The most atmospheric budget stay in the Westfjords." },
    ],
    logistics: [
      { q: "When to go", a: "June–August only for most visitors. The mountain roads (F-roads and many secondary roads) are closed October–May by snow. The Westfjords in winter are extraordinary but require 4WD, significant experience, and readiness for complete isolation. July is the sweet spot: puffins at Látrabjarg, Dynjandi accessible, long daylight hours. The Ísafjörður winter festival (Aldrei fór ég suður) in April is the exception — worth the difficulty." },
      { q: "Getting there", a: "Two options: fly into Ísafjörður (IFJ) from Reykjavík on Eagle Air (45 minutes, runs daily in summer, expensive at €150–300 each way) or drive — 5–6 hours from Reykjavík on Route 60, much of it gravel. The drive is part of the experience but not to be underestimated. The Brjánslækur ferry from Stykkishólmur (on the Snæfellsnes Peninsula) cuts driving time significantly — check the Seatours schedule." },
      { q: "Getting around", a: "4WD is strongly recommended — many of the best roads are gravel and the fjord crossings require it. Check Safetravel.is for current road conditions before driving anywhere. The F-roads in the interior require proper highland vehicles. Fuel is available in Ísafjörður and a few other points — fill up whenever possible. Download offline maps before leaving Reykjavík — mobile coverage disappears." },
      { q: "How long", a: "Four nights minimum to do the Westfjords properly. Day one: arrive Ísafjörður (fly or drive), harbour walk, Tjöruhúsið dinner. Day two: northern Westfjords drive — Ísafjörður fjords, Súðavík arctic fox centre. Day three: drive south to Dynjandi — the waterfall, fjord swimming. Day four: drive to Látrabjarg for puffins, Rauðisandur red sand beach (the only one in Iceland). Day five: depart south." },
      { q: "Money", a: "The Westfjords are cheaper than the rest of Iceland. Hotel Ísafjörður: €130–200. Heydalur Guesthouse: €100–160. Wild camping: free. Tjöruhúsið dinner: €50–70. Flying Reykjavík–Ísafjörður: €150–300. The ferry crossing Brjánslækur: €30 per person. Fill up on petrol in Ísafjörður — remote petrol is rare and expensive." },
    ],
  },
  {
    name: "North Iceland", country: "iceland", tag: "Akureyri · Mývatn · Siglufjörður",
    hook: "Iceland's second city has 20,000 people and thinks that's enough. Siglufjörður had 3,000 more and the herring left. Mývatn looks like it belongs on another planet.",
    img: "https://images.unsplash.com/photo-1531366936337-7c912a4589a7?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("mountains")||a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("explore")||a[6]?.includes("wander")) s+=3; if(a[1]?.includes("solo")||a[1]?.includes("partner")) s+=1; if(a[8]?.includes("people")||a[8]?.includes("none")) s+=2; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; if(a[6]?.includes("physical")||a[6]?.includes("fullday")) s+=2; return s; },
    intro: "North Iceland sits just below the Arctic Circle — Akureyri, the country's second city, is 100km south of it. The region centres on three things: Akureyri itself (a small city with a genuine food scene, botanical gardens that shouldn't work at this latitude, and a ski area 15 minutes away), Lake Mývatn (a geothermally active lake surrounded by pseudocraters, lava formations, and hot springs that makes no visual sense), and Siglufjörður (a herring fishing town that boomed, went completely bust when the herring disappeared in the 1960s, and has been quietly extraordinary ever since). The Arctic Circle is 40km north of Akureyri — the Grímsey island actually crosses it.",
    highlights: [
      { label: "Siglufjörður", text: "A town of 1,200 people at the end of a fjord that's only accessible through two tunnels bored through the mountains. In the 1940s it was the herring capital of the world — 10,000 people, constant activity, boats packed into the harbour. The herring disappeared in the late 1960s and most people left. The Herring Era Museum is the best museum in Iceland — three restored warehouses showing exactly what the boom looked and smelled like. The town itself is one of the most beautiful in Iceland." },
      { label: "Lake Mývatn", text: "A shallow lake surrounded by volcanic features that look designed rather than geological — pseudocraters (created when lava flowed over wetland and steam explosions punched craters through the surface), lava pillars rising from the water, the Hverfjall tephra crater, and the Dimmuborgir lava formations. The Mývatn Nature Baths (the northern equivalent of the Blue Lagoon, less famous, less crowded, equally hot) sit on the lake shore." },
      { label: "Akureyri", text: "Iceland's second city punches above its size. The botanical garden at 65° north somehow grows roses and trees. The Akureyri church sits above the town on a hill. The restaurant scene — Rub23, Strikið — is serious. The ski area at Hlíðarfjall (15 minutes from town) has night skiing December–April. The Christmas lights stay up year-round because the city voted to keep them." },
      { label: "Goðafoss waterfall", text: "The Waterfall of the Gods — named for the event in 1000 AD when Iceland officially converted to Christianity and the chieftain Þorgeir threw his Norse idols into the falls. A horseshoe of water 12 metres high and 30 metres wide, directly on Route 1 between Akureyri and Mývatn. One of the most accessible great waterfalls in Iceland." },
    ],
    eat: [
      { name: "Rub23 (Akureyri)", desc: "The best restaurant in north Iceland. A sushi and grill concept that sounds wrong and works perfectly — Arctic char sashimi, Icelandic lamb with a Japanese glaze, local seafood. The tasting menu is €80–100." },
      { name: "Bautinn (Akureyri)", desc: "The old-school Akureyri restaurant that's been feeding the city since 1975. Lamb soup, plokkfiskur (fish stew), Icelandic pancakes. Lunch only on weekdays. Where the city goes." },
      { name: "Sigló Hótel restaurant (Siglufjörður)", desc: "The hotel restaurant in Siglufjörður with the best herring plate in Iceland — multiple preparations of the fish that built the town. Local fish, Icelandic lamb, harbour view. Ask for the window table." },
      { name: "Mývatn Nature Baths café", desc: "The café attached to the thermal baths. Lamb soup, Icelandic bread, skyr. Eat after soaking — you'll be hungry and the soup is excellent." },
    ],
    stay: [
      { name: "Sigló Hótel (Siglufjörður)", tier: "High end", desc: "A boutique hotel in a converted fishing-era building on the harbour in Siglufjörður. Marina views, geothermal pool, extraordinary atmosphere. The best hotel in north Iceland." },
      { name: "Icelandair Hotel Akureyri", tier: "Mid range", desc: "The reliable city-centre option in Akureyri. Walking distance to the restaurants and the church staircase, parking, good breakfast. The base for the north Iceland road trip." },
      { name: "Vogafjós Farm Resort (Mývatn)", tier: "Mid range", desc: "A working dairy farm on the shore of Lake Mývatn. Watch the cows being milked through the restaurant window while eating fresh cheese made an hour ago. Geothermally heated rooms, extraordinary location." },,
      { name: "Gistihúsið Lake Hotel (Mývatn)", tier: "Good value", desc: "A guesthouse on the shore of Lake Mývatn with direct views across the water to the pseudocraters. Simple rooms, geothermally heated, the best value stay in the Mývatn area. Walk to the Nature Baths in 20 minutes." },
    ],
    logistics: [
      { q: "When to go", a: "June–August for the long days and the Mývatn landscapes at their best. October–March for northern lights — Akureyri and Siglufjörður have excellent dark skies and the city is fully operational year-round. April–May: the ski season at Hlíðarfjall ends, the roads clear, and the region is dramatically empty. Mývatn's midges (tiny flies that don't bite but swarm in clouds) peak in late June–July — bring a head net." },
      { q: "Getting there", a: "Fly into Akureyri (AEY) from Reykjavík on Icelandair or Eagle Air (45 minutes, multiple daily flights). Or drive — 4.5–5 hours from Reykjavík on Route 1 north, through the interior on Route 35 over the Kjölur highland route (4WD required, summer only, extraordinary). The drive is worth doing in one direction at least." },
      { q: "Getting around", a: "Car essential. Akureyri is walkable within the town. Mývatn is 100km east of Akureyri on Route 1. Siglufjörður is 45km northwest of Akureyri through two mountain tunnels. The Mývatn area requires a full day — drive the circuit of the lake, stopping at each geological feature. The Goðafoss waterfall is directly on Route 1 between Akureyri and Mývatn." },
      { q: "How long", a: "Four nights. Night one: arrive Akureyri, Rub23 dinner. Day two: Siglufjörður — Herring Museum, harbour walk, lunch at Sigló Hótel, return. Day three: drive to Mývatn — pseudocraters, Dimmuborgir, Mývatn Nature Baths, Vogafjós dinner. Day four: Goðafoss, Húsavík (whale watching capital of Iceland, 1 hour from Mývatn). Day five: return to Reykjavík or continue east." },
      { q: "The Arctic Circle", a: "Akureyri is 100km south of the Arctic Circle. To actually cross it, take the ferry to Grímsey island (3 hours from Dalvík, near Akureyri) — a small island community of 60 people that straddles the Circle. The crossing is marked by a concrete sphere. Puffins, Arctic terns, and the sense of being genuinely north of everywhere." },
      { q: "Money", a: "North Iceland is cheaper than Reykjavík. Sigló Hótel: €180–280. Icelandair Hotel Akureyri: €130–200. Vogafjós: €120–180. Rub23 tasting menu: €80–100. Mývatn Nature Baths entry: €45. Whale watching in Húsavík: €90–110. Flying Reykjavík–Akureyri: €80–150 each way booked ahead." },
    ],
  },
  {
    name: "Highlands / Landmannalaugar", country: "iceland", tag: "Rhyolite Mountains · Hot Springs · Laugavegur Trek",
    hook: "Mountains the colour of an oil painting. Hot springs in the middle of nowhere. A 4-day trek that people plan their entire year around. No roads in winter.",
    img: "https://images.unsplash.com/photo-1504870712357-65ea720bf122?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=4; if(a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=5; if(a[5]?.includes("mountains")||a[5]?.includes("desert")) s+=4; if(a[6]?.includes("physical")||a[6]?.includes("explore")) s+=4; if(a[7]?.includes("midrange")||a[7]?.includes("budget")) s+=1; if(a[8]?.includes("deep")||a[8]?.includes("none")) s+=2; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; if(a[6]?.includes("fullday")) s+=2; return s; },
    intro: "Landmannalaugar sits in the Icelandic Highlands at 600 metres above sea level, accessible only by 4WD river crossing from July to September, and closed completely by snow for eight months of the year. The landscape is rhyolite — a volcanic rock that comes in greens, yellows, reds, purples, and blacks — creating mountain colours that look digitally altered and aren't. A natural hot spring runs alongside the camp where you can swim regardless of weather. The Laugavegur trek, a 4-day hut-to-hut trail to Þórsmörk, is the most celebrated multi-day hike in Iceland and one of the best in the world. Everything about this place requires effort to reach and rewards it completely.",
    highlights: [
      { label: "The rhyolite mountains", text: "The mountains surrounding Landmannalaugar are coloured by rhyolite — a volcanic rock formed at high temperatures that oxidises into extraordinary colours. Walk the Brennisteinsalda trail (3–4 hours, circular, no guide needed) for the full range: yellow sulphur vents, black obsidian fields, red iron-stained ridges, green moss. The photos look fake. They aren't." },
      { label: "The natural hot spring", text: "A geothermal stream runs alongside the Landmannalaugar camp and pools into a natural bathing area. The temperature is perfect (38–42°C depending on rain). Soak in the hot water with cold rain on your face, looking up at rhyolite mountains. Free, always open, one of the great simple experiences in Iceland." },
      { label: "The Laugavegur Trek", text: "Four days, 55km, hut-to-hut from Landmannalaugar to Þórsmörk. Crosses highland deserts, active geothermal areas, glaciers, and river fords. The huts (run by Ferðafélag Íslands) provide sleeping bags, dinner, and breakfast. Book 6–12 months ahead — the huts fill completely in July and August. The full Fimmvörðuháls extension adds two more days to Skógar on the South Coast." },
      { label: "Kerlingarfjöll", text: "A highland rhyolite massif 90km from Reykjavík, less visited than Landmannalaugar but equally extraordinary. Active geothermal vents, steaming valleys, pink and orange mountains. The summer camp has basic accommodation. Accessible by 4WD on Route F35 (Kjölur highland road)." },
    ],
    eat: [
      { name: "Landmannalaugar camp kitchen", desc: "The camp has a basic canteen — hot soup, bread, coffee. It's not about the food here. Cook your own on a camp stove, eat outside looking at the mountains, drink the stream water (genuinely drinkable everywhere in the Highlands)." },
      { name: "Laugavegur hut dinners", desc: "Each hut on the Laugavegur trek serves a hot dinner and breakfast. Simple — pasta, lamb stew, skyr — but after a full day of hiking in the highland wind it's the best meal you'll eat. Included in the hut fee." },
      { name: "Hrauneyjar Highland Center", desc: "The last stop before the highlands on Route 26 — a hotel, petrol station, and restaurant serving Icelandic lamb and fish. Fill up here on fuel and a hot meal before heading into the interior." },
    ],
    stay: [
      { name: "Landmannalaugar Mountain Huts", tier: "Good value", desc: "The Ferðafélag Íslands huts at Landmannalaugar — sleeping bag accommodation in dorms, basic facilities, the hot spring outside. €60–80 per night. Book through fi.is months ahead for July–August." },
      { name: "Kerlingarfjöll Mountain Resort", tier: "Mid range", desc: "Basic hotel accommodation at the Kerlingarfjöll highland site. Not luxury — small rooms, shared facilities — but the location in the middle of the rhyolite mountains is irreplaceable." },
      { name: "Laugavegur Trek huts", tier: "Good value", desc: "Four huts along the trek route: Landmannalaugar, Hrafntinnusker, Álftavatn, Emstrur. Sleeping bag dorms, cook your own or buy dinner. The social experience of the huts — everyone comparing the day's terrain, drying gear, comparing blisters — is as much the point as the walking." },,
      { name: "Frost and Fire Hotel (Hveragerði)", tier: "Mid range", desc: "A hotel in Hveragerði — the geothermal town 45 minutes from Reykjavík and 2 hours from Landmannalaugar. Natural hot river runs through the property garden. The best base for highland day trips without camping." },
    ],
    logistics: [
      { q: "When to go", a: "July–September only. The F-roads (highland roads) are closed by snow outside these months — attempting them in spring or autumn is dangerous. July is peak season: the huts fill, the weather is best, the rhyolite colours are most vivid. August is slightly quieter. September brings autumn colours and the real possibility of snow — extraordinary but the window is narrow." },
      { q: "Getting there", a: "From Reykjavík, take Route F208 (requires 4WD and a river crossing — check current conditions at road.is) to Landmannalaugar: 3–4 hours. Or take the Reykjavík Excursions bus (runs daily July–September, no 4WD required, €70–90 each way). For the Laugavegur Trek, buses also run to Þórsmörk for the south trailhead. Book bus seats ahead — they sell out." },
      { q: "The 4WD requirement", a: "The F208 river crossing (Jökulkvísl) is mandatory and changes depth with rainfall and glacial melt. Never attempt a highland river crossing without a proper highland vehicle (not a standard rental SUV — a genuine F-road vehicle with high clearance and snorkel exhaust). Check road.is for current crossing conditions. The bus is a legitimate alternative that eliminates the risk entirely." },
      { q: "Laugavegur Trek booking", a: "Book hut accommodation through Ferðafélag Íslands (fi.is) 6–12 months ahead for peak season. The huts have limited capacity and fill completely. July–August dates go in January. Each night costs €60–80 including bedding. You can also camp at each hut for €20–30, but bring a four-season tent — highland conditions are serious." },
      { q: "How long", a: "Landmannalaugar day trip: 2.5 hours from Reykjavík by bus, full day in the highlands, back by 9pm. One or two nights in the huts for the full experience. Laugavegur Trek: 4 days hiking plus travel days on either end — minimum 6 days total from Reykjavík. Extend to Skógar for the full 6-day traverse." },
      { q: "Money", a: "Laugavegur hut: €60–80 per night. Highland bus return: €70–90. Landmannalaugar huts: €60–80. Kerlingarfjöll Mountain Resort: €120–180. Food in the highlands is whatever you bring plus hut dinners (€20–30 extra). This is one of the few parts of Iceland where the experience is genuinely affordable — the landscape costs nothing." },
    ],
  },
  {
    name: "East Iceland Fjords", country: "iceland", tag: "Reindeer · Fishing Villages · The Road Less Driven",
    hook: "Five hours from Reykjavík. Almost nobody drives that far. The people who do tend to come back quieter and more certain about things.",
    img: "https://images.unsplash.com/photo-1539066834195-ccc9e40d879e?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=4; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=4; if(a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=3; if(a[6]?.includes("explore")||a[6]?.includes("nothing")) s+=3; if(a[1]?.includes("solo")||a[1]?.includes("partner")) s+=2; if(a[8]?.includes("none")||a[8]?.includes("feel")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; if(a[6]?.includes("wander")||a[6]?.includes("physical")) s+=2; return s; },
    intro: "The East Fjords are the part of Iceland that Ring Road tourists see briefly from the car window on the way to Jökulsárlón and don't stop in. The roads cut in and out of a series of deep fjords — Berufjörður, Hamarsfjörður, Álftafjörður, Seyðisfjörður — each one narrower and quieter than the last. Egilsstaðir is the only real town. Seyðisfjörður is the exception to the east's anonymity — a Norwegian-founded village at the end of a fjord with a rainbow road, a functioning ferry terminal to Denmark, and the most arts activity per capita of anywhere in Iceland. Reindeer were introduced from Norway in the 18th century and now run wild in the highlands above the fjords.",
    highlights: [
      { label: "Seyðisfjörður", text: "A village of 700 people at the end of a mountain road, 27km from Egilsstaðir. Norwegian timber houses painted in primary colours, a rainbow pedestrian street, a converted fish factory (Skaftfell) that runs an arts centre year-round. The Smyril Line ferry to the Faroe Islands and Denmark departs from here every Thursday — some people arrive by ferry having never been to Iceland, discover the village, and stay. The drive in on Route 93 over the mountain pass with the fjord appearing below is one of the great road moments in Iceland." },
      { label: "Stórurð (The Giant Boulders)", text: "A hidden valley in the highland above Seyðisfjörður filled with enormous boulders — each one the size of a house — dropped by glacier movement and now sitting in a turquoise lake. The hike in takes 3–4 hours return through mountain scenery. Almost no one knows about it." },
      { label: "The fjord drives", text: "Route 1 east of Höfn cuts through the East Fjords on a road that is sometimes a single lane carved into the cliff face above the sea. Each fjord has a fishing village at its head — Djúpivogur, Breiðdalsvík, Fáskrúðsfjörður. Stop in all of them. The French fishing fleet used Fáskrúðsfjörður as a base for decades — the town still has French street signs alongside Icelandic ones." },
      { label: "Hengifoss waterfall", text: "The third-highest waterfall in Iceland — 128 metres — in a canyon with distinctive red and black layered basalt. The hike from the car park takes 1.5 hours return. Litlanesfoss, with its perfect basalt column formations, is passed on the way up and is arguably more beautiful." },
    ],
    eat: [
      { name: "Skaftfell Bistro (Seyðisfjörður)", desc: "The café inside the Skaftfell arts centre. Homemade soup, open sandwiches, Icelandic baking, local dairy. The best lunch in the East Fjords." },
      { name: "Café Nielssen (Seyðisfjörður)", desc: "A Norwegian-era timber building on the harbour serving fish soup, langoustines, and coffee. The most atmospheric lunch in eastern Iceland." },
      { name: "Salt (Egilsstaðir)", desc: "The only restaurant in the East with serious ambition. Local lamb and reindeer, east Iceland dairy, good wine list. Worth the stop in what is otherwise a functional transit town." },
    ],
    stay: [
      { name: "Hotel Aldan (Seyðisfjörður)", tier: "High end", desc: "Three buildings in the centre of Seyðisfjörður — a bank, a house, and a store — all converted into hotel rooms. Each building has its own character. The most charming hotel in eastern Iceland." },
      { name: "Wilderness Center (Skriðuklaustur)", tier: "High end", desc: "A remote highland farm converted into a wilderness experience — reindeer safaris, glacier hikes, horse riding, northern lights. 40km from Egilsstaðir. The most extraordinary stay in east Iceland." },
      { name: "Guesthouse Egilsstaðir", tier: "Good value", desc: "Simple, functional, cheap. Egilsstaðir is a transit hub — stay one night and use it as a base for Seyðisfjörður and Hengifoss." },,
      { name: "Tæknisetur (Seyðisfjörður)", tier: "Good value", desc: "A converted technical school in Seyðisfjörður run as a guesthouse by the local arts community. Large rooms in a historic building, a communal kitchen, walking distance to everything in the village. The most social stay in east Iceland." },
    ],
    logistics: [
      { q: "When to go", a: "June–September. The East Fjords are accessible year-round but the mountain road to Seyðisfjörður (Route 93) closes in winter snowfall. The aurora is exceptional in the East in October–February — very little light pollution and the fjords frame the lights. The Wilderness Center operates year-round for reindeer safaris and aurora viewing." },
      { q: "Getting there", a: "5 hours from Reykjavík by car on Route 1 east past Jökulsárlón. Or fly into Egilsstaðir (EGS) from Reykjavík on Icelandair (45 minutes, multiple weekly flights). The Smyril Line ferry from Denmark and the Faroe Islands arrives in Seyðisfjörður every Thursday — arriving by sea is extraordinary." },
      { q: "Getting around", a: "Car essential. The Ring Road passes through but the fjord roads (Routes 92, 93, 96) are what makes the East special. Standard 2WD is fine in summer. Seyðisfjörður is 27km from Egilsstaðir on a mountain road — straightforward in summer, can close overnight in bad weather. The Wilderness Center requires 4WD." },
      { q: "How long", a: "Three nights. Day one: arrive Egilsstaðir, drive to Seyðisfjörður, lunch at Café Nielssen, Stórurð hike. Day two: fjord circuit south — Fáskrúðsfjörður, Djúpivogur, Hengifoss. Day three: north fjords, Wilderness Center reindeer safari. Day four: depart west on Route 1 or fly from Egilsstaðir." },
      { q: "Reindeer", a: "Reindeer were brought from Norway in 1771 and released into the East Iceland highlands. The herd now numbers around 3,000 and roams freely — they're most visible in the highland areas above the fjords in summer and come down toward the farms in winter. The Wilderness Center runs guided reindeer safaris. Seeing a reindeer on the road is common — slow down, they don't move fast." },
      { q: "Money", a: "The East is the most affordable part of Iceland for accommodation. Hotel Aldan: €150–250. Wilderness Center: €200–350 all-inclusive. Guesthouse Egilsstaðir: €80–130. Lunch at Skaftfell Bistro: €20–30. Salt dinner: €60–80 per person. Flying Reykjavík–Egilsstaðir: €80–150. The East rewards those who drive it — the fjord roads are free and the landscape is extraordinary." },
    ],
  },
];

// ─── JAPAN REGIONS ────────────────────────────────────────────────────────────
const japanRegions = [
  {
    name: "Tokyo", country: "japan", tag: "Neighborhoods · Food · Energy",
    hook: "Tokyo has more Michelin-starred restaurants than any city on earth. That is not why you go. You go for the neighborhoods nobody tells you about.",
    img: "https://images.unsplash.com/photo-1540959733332-eab4deabeeaf?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("cities")) s+=4; if(a[6]?.includes("wander")||a[6]?.includes("eat")) s+=3; if(a[9]?.includes("generic")||a[9]?.includes("tourist")) s+=2; if(a[6]?.includes("fullday")) s+=2; return s; },
    intro: "Tokyo is the most organized chaos on earth — a city of 37 million people where the trains run to the second, the convenience store food is extraordinary, and entire neighborhoods exist that most visitors never find. Shibuya crossing is real and worth seeing once. But the Tokyo that stays with you is Yanaka — the old shitamachi district that survived the war and the earthquakes, where the streets are narrow and the temples are between the houses — and Shimokitazawa, the neighborhood of vintage clothing stores, jazz bars, and curry restaurants where Tokyo's musicians and writers actually live. The ramen here is the best food delivery system ever designed. The standing sushi bars charge a third of what a seated restaurant does and are often better.",
    highlights: [
      { label: "Yanaka", text: "The old Tokyo that survived. A low-rise neighborhood of wooden houses, family temples, a covered market street (Yanaka Ginza), and cats — dozens of them, on walls and in doorways. Walk here on a weekday morning. The cemetery is peaceful and worth entering. This is what the city looked like before the modern version arrived." },
      { label: "Shimokitazawa", text: "Tokyo's bohemian neighborhood — vinyl record shops, vintage clothing, tiny live music venues, and curry restaurants that take the dish seriously as a Japanese tradition (not an import). The streets are too narrow for most cars and the whole neighborhood exists at walking pace. Go on a Sunday afternoon." },
      { label: "Tsukiji Outer Market", text: "The inner market moved to Toyosu but the outer market is still operating — a dense grid of stalls selling fresh seafood, tamagoyaki (sweet rolled omelette), dried goods, and kitchen knives. Arrive by 7am. Eat tuna sashimi for breakfast. Buy a knife. The vendors have been here for generations." },
      { label: "Koenji", text: "The anti-Harajuku. Where Harajuku sells fashion to tourists, Koenji developed its own subculture over decades — punk, vintage, alternative. The covered shopping arcades mix record shops, secondhand kimono dealers, ramen counters, and izakayas. One of the most authentic Tokyo neighborhoods left." },
      { label: "The bullet train departure", text: "Take the Shinkansen somewhere — anywhere. The platform staff bow as the train arrives. The train is exactly on time. The seats are wider than economy class on any airline. The bento box from the station is better than most restaurant meals. Japan's domestic travel infrastructure is a feature of the trip, not a means to an end." },
    ],
    eat: [
      { name: "Ichiran Ramen (multiple locations)", desc: "The solo ramen experience — individual booths with bamboo screens, a paper form to customize your broth, a small hatch where the bowl arrives. Tonkotsu ramen done to exact specification. The booths are not antisocial — they are about complete focus on the bowl. Open 24 hours." },
      { name: "Sushi Saito (Minato)", desc: "The hardest reservation in Tokyo — arguably the best sushi in Japan. Chef Takashi Saito serves omakase to six people per seating. Book through your hotel concierge months ahead or accept that you won't get in. The alternative: any basement sushi counter in Ginza at 11pm." },
      { name: "Afuri (Harajuku)", desc: "Yuzu shio ramen — a clear, delicate broth with yuzu citrus, thin noodles, and perfect chashu pork. The opposite of the heavy tonkotsu. The Harajuku location has a line but moves fast. The best light ramen in Tokyo." },
      { name: "Depachika (any department store)", desc: "The basement food halls of Tokyo's department stores — Isetan in Shinjuku, Mitsukoshi in Ginza — are among the best food experiences in the world. Hundreds of counters selling wagashi (Japanese sweets), prepared foods, imported cheese, artisan sake. Go hungry. Buy everything." },
      { name: "Standing sushi bars (Ginza)", desc: "The small counter sushi bars around Ginza and Tsukiji that have no seats — you stand, the chef passes nigiri directly, you eat, you leave. A full meal costs ¥2,000–4,000 and the quality matches restaurants charging ten times more. The best value in Tokyo." },
    ],
    stay: [
      { name: "Trunk Hotel (Shibuya)", tier: "High end", desc: "A design hotel in Shibuya with a social mission — locally sourced food, community programming, the best rooftop bar in the neighborhood. The antithesis of the international business hotel." },
      { name: "Ryokan Sawanoya (Yanaka)", tier: "Mid range", desc: "A traditional ryokan in the Yanaka neighborhood — tatami rooms, futon bedding, a shared cypress bath, breakfast of miso soup and pickles. The family that runs it has hosted travelers for generations and knows the neighborhood intimately." },
      { name: "BnA Alter Museum (Akihabara)", tier: "Mid range", desc: "An art hotel where every room is designed by a different Japanese artist. No two rooms the same. Part hotel, part gallery, part bar. The most interesting mid-range stay in Tokyo." },
      { name: "Capsule Hotel Anshin Oyado (Shinjuku)", tier: "Good value", desc: "The capsule hotel done properly — individual pods with proper mattresses, blackout blinds, a locker for your bags, and a shared onsen bath on the top floor. Not for claustrophobics. For everyone else: an experience and a bargain at ¥4,000 a night." },
    ],
    logistics: [
      { q: "When to go", a: "March–April for cherry blossom (sakura) — the single most beautiful thing Japan does, lasts about two weeks, the exact dates shift by year. October–November for autumn foliage (koyo) — equally extraordinary, less crowded. Avoid Golden Week (late April–early May) and Obon (mid-August) when domestic travel peaks and prices spike. Summer (June–August) is humid and hot — manageable but not ideal." },
      { q: "Getting there", a: "Fly into Narita (NRT) or Haneda (HND) — Haneda is closer to the city (30 minutes by monorail) and increasingly has international routes. From Narita: the Narita Express (N'EX) to Shinjuku takes 90 minutes, ¥3,000. Buy a Suica card at the airport — it works on every train and subway in Japan and at most convenience stores." },
      { q: "Getting around", a: "The Tokyo Metro is the best urban transit system on earth. A Suica card covers everything. Taxis are clean and honest but expensive. Uber exists but is often slower than the train. Walking between neighborhoods is always worthwhile — the streets between stations are part of the experience. Google Maps works perfectly for transit navigation in Japan." },
      { q: "The IC card", a: "Buy a Suica or Pasmo card at any major station — load ¥5,000–10,000 and tap in and out of every train, subway, and bus in the country. It also works at 7-Eleven, FamilyMart, Lawson, and most vending machines. The single most useful object in Japan after your passport." },
      { q: "How long", a: "Tokyo alone deserves four nights minimum. Day one: arrive, Tsukiji breakfast, wander Ginza. Day two: Yanaka morning, Ueno museums, Akihabara evening. Day three: Shimokitazawa, Shinjuku at night (Golden Gai — a grid of tiny bars, each holding ten people). Day four: Harajuku, Omotesando, depachika dinner. Day five: Koenji, depart or take the Shinkansen to Kyoto." },
      { q: "Money", a: "Japan is less expensive than its reputation. A bowl of excellent ramen: ¥900–1,500. A standing sushi lunch: ¥2,000–4,000. A convenience store meal (genuinely good): ¥500–800. Ryokan Sawanoya: ¥12,000–18,000 per person including breakfast. The subway: ¥170–320 per journey. Budget ¥15,000–25,000 per day for a comfortable Tokyo trip excluding accommodation." },
    ],
  },
  {
    name: "Kyoto", country: "japan", tag: "Temples · Ryokan · Geisha Districts",
    hook: "1,600 temples. Two geisha districts. The best kaiseki cuisine in Japan. Go at 6am before anyone else arrives.",
    img: "https://images.unsplash.com/photo-1528360983277-13d401cdc186?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("stretch")||a[4]?.includes("bold")) s+=2; if(a[5]?.includes("countryside")||a[5]?.includes("cities")) s+=3; if(a[6]?.includes("absorb")||a[6]?.includes("nothing")) s+=3; if(a[9]?.includes("crowds")||a[9]?.includes("tourist")) s+=3; if(a[8]?.includes("deep")||a[8]?.includes("feel")) s+=2; return s; },
    intro: "Kyoto was Japan's imperial capital for over a thousand years and the city that the US specifically chose not to bomb in 1945 — it was too culturally significant to destroy. The result is the only major Japanese city where the old and new exist in genuine tension rather than the old having been entirely replaced. Fushimi Inari — the thousands of vermillion torii gates climbing the mountain — is genuinely extraordinary and genuinely overcrowded by 9am. Arrive at dawn. The Philosopher's Path in autumn when the maples turn is one of the most beautiful walks in the world. A traditional ryokan stay — tatami floor, kaiseki dinner served in your room, hinoki cypress bath — is the single most complete cultural experience Japan offers.",
    highlights: [
      { label: "Fushimi Inari at dawn", text: "The thousands of vermillion torii gates donated by businesses climbing Mount Inari. The bottom is always photographed — walk all the way to the top, two hours, and you leave the tourist trail entirely. The upper mountain has smaller shrines, fox statues, and almost nobody. Arrive before 7am." },
      { label: "Gion and Pontocho", text: "Gion is Kyoto's most famous geisha district — wooden machiya townhouses, cobblestone lanes, ochaya (teahouses) behind closed doors. Hanamikoji Street is the postcard. Walk it at dusk and you may see a maiko (apprentice geisha) moving between engagements. Pontocho is a narrow alley parallel to the Kamo River packed with restaurants — the best concentration of food in Kyoto." },
      { label: "Arashiyama", text: "The bamboo grove everyone photographs is real and worth it — the sound and light inside the grove are genuinely unusual. But the best of Arashiyama is the hour after: Tenryu-ji's garden, the riverside path west of the Togetsukyo bridge, the small temple of Jojakko-ji up the hill. Arrive early, stay for lunch, leave before 11am crowds peak." },
      { label: "Nishiki Market", text: "Kyoto's covered market — five blocks of stalls selling pickled vegetables, fresh tofu, wagashi sweets, grilled skewers, matcha everything. The vendors have been here for generations. Eat as you walk. The pickled plum onigiri from the stall halfway down is the best rice ball in Japan." },
      { label: "Kaiseki dinner", text: "Kyoto kaiseki — the multi-course Japanese haute cuisine built around seasonal ingredients and extraordinary precision — is the reason serious food travelers come to Kyoto over Tokyo. Each course is a small sculpture. The meal lasts three hours. The experience is unlike anything else in world dining. Book through your ryokan." },
    ],
    eat: [
      { name: "Kikunoi (Higashiyama)", desc: "Three Michelin stars, the benchmark kaiseki restaurant in Kyoto. Chef Murata's seasonal menus use ingredients from specific Kyoto farms and fishing boats. The lunch course (¥12,000) is the entry point — a full introduction to kaiseki at a fraction of the dinner price." },
      { name: "Nishiki Market stalls", desc: "Eat through the market rather than sitting anywhere. The dashimaki tamago (rolled omelette) from Murakami-ju, the yuba (tofu skin) from Tousuiro, the matcha soft serve from anywhere. A complete lunch for ¥1,500 while standing." },
      { name: "Pontocho alley restaurants", desc: "The narrow alley runs parallel to the Kamo River — in summer, the restaurants extend platforms (kawayuka) over the river. Reservations required at the serious places. Walk the full length first, choose based on what's visible through the door. Trust your instincts." },
      { name: "Ippudo Ramen (Shijo)", desc: "The Hakata-style tonkotsu chain that started in Fukuoka — this branch is one of the best in Japan. Rich, creamy pork broth, thin noodles, perfect chashu. The kaedama system lets you order additional noodles when your broth is still warm. ¥890 for a bowl." },
    ],
    stay: [
      { name: "Tawaraya Ryokan", tier: "High end", desc: "The finest ryokan in Japan — opened in 1708, still run by the same family. Guests have included Steve Jobs, the Rockefellers, and every Japanese prime minister. Sixteen rooms, kaiseki meals, a garden that has been tended for three centuries. The most complete traditional Japanese experience available." },
      { name: "Aman Kyoto", tier: "High end", desc: "A contemporary luxury ryokan hidden in a forest garden above the city near Kinkaku-ji. Stone paths, moss gardens, a spa with forest views. The most beautiful modern hotel in Kyoto." },
      { name: "Gion Hatanaka", tier: "Mid range", desc: "A traditional machiya townhouse ryokan in the heart of Gion. Eight rooms, tatami floors, kaiseki breakfast, and a location that puts you in the geisha district at dawn before any tourists arrive." },
      { name: "Len Kyoto Kawaramachi", tier: "Good value", desc: "A hostel and cafe hybrid in the Kawaramachi shopping district — private rooms available, excellent communal spaces, a ground floor bar that becomes a local hangout by 9pm. The best budget base in central Kyoto." },
    ],
    logistics: [
      { q: "When to go", a: "Cherry blossom (late March–early April) and autumn foliage (mid-November) are peak beauty and peak crowds — book accommodation six months ahead. May and October are excellent: good weather, fewer tourists. Avoid August (humid, hot, Gion Festival draws enormous crowds) and Golden Week." },
      { q: "Getting there", a: "Shinkansen from Tokyo takes 2 hours 15 minutes (¥13,600 on the Nozomi). From Osaka: 15 minutes by Shinkansen or 30 minutes on the Hankyu line (¥400). Kyoto station is the hub — most major sights are accessible by city bus or the two subway lines." },
      { q: "Getting around", a: "City buses cover most temples and neighborhoods — a day pass (¥700) covers unlimited rides. The Higashiyama area (Gion, Kiyomizudera) is best walked. Rent a bicycle for Arashiyama and the northern temples — flat roads, beautiful cycling. Google Maps is accurate for bus routes." },
      { q: "The 6am rule", a: "Every famous temple in Kyoto is extraordinary at 6am and overcrowded by 10am. Fushimi Inari, the Philosopher's Path, Arashiyama bamboo grove, Kinkaku-ji — all of them. Stay somewhere central, set your alarm, and walk to the nearest major sight before breakfast. You will have it almost entirely to yourself." },
      { q: "How long", a: "Three nights minimum, four nights ideal. Day one: Fushimi Inari at dawn, Nishiki Market lunch, Gion at dusk. Day two: Arashiyama morning, Ryoan-ji (the dry garden), Kinkaku-ji (the Golden Pavilion — genuinely worth seeing). Day three: Philosopher's Path, Nanzen-ji, kaiseki dinner. Day four: day trip to Nara (45 minutes by train) — the deer park, Todai-ji temple." },
      { q: "Money", a: "Temple entry: ¥500–1,000 each. Kikunoi lunch kaiseki: ¥12,000. Nishiki Market lunch: ¥1,500. Tawaraya Ryokan: ¥80,000–150,000 per person per night including meals. Gion Hatanaka: ¥25,000–45,000. Len Kyoto: ¥8,000–15,000. City bus day pass: ¥700. Kyoto is significantly more expensive than Tokyo for accommodation — book early." },
    ],
  },
  {
    name: "Kanazawa", country: "japan", tag: "Geisha · Samurai · Seafood",
    hook: "The Kyoto that survived the war completely intact. The seafood market that makes Tsukiji look small. The fact that almost nobody goes.",
    img: "https://images.unsplash.com/photo-1536098561742-ca998e48cbcc?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=4; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("cities")||a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("absorb")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=4; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=3; return s; },
    intro: "Kanazawa was Japan's wealthiest city outside Edo during the Edo period — the Maeda clan ruled it for 300 years and spent their wealth on arts and culture rather than wars. The result is a city with an intact geisha district, intact samurai neighborhoods, the third most visited garden in Japan, and a contemporary art museum that became one of the most attended in the world within a year of opening. And almost no foreign tourists. The Omicho Market has been running since the 18th century and the seafood — Kanazawa faces the Sea of Japan — is extraordinary. The city sits between the Japan Alps and the coast on the Noto Peninsula, which is the most undervisited coastline in Japan.",
    highlights: [
      { label: "Higashi Chaya geisha district", text: "The best-preserved geisha district in Japan — three chaya (teahouse) districts remain intact in Kanazawa, more than anywhere outside Kyoto. Higashi Chaya is the largest: two-storey wooden buildings with latticed facades, stone-paved lanes, the sound of shamisen practice from the upper floors in the afternoon. Several chaya are open as cafes and sake bars." },
      { label: "Kenroku-en Garden", text: "One of Japan's three great gardens, covering 11 hectares on a hill above the city. Designed to embody the six attributes of a perfect garden — spaciousness, seclusion, artifice, antiquity, water, and views. The plum trees bloom in February, the cherry trees in April, the irises in June. In snow it becomes something else entirely." },
      { label: "21st Century Museum of Contemporary Art", text: "SANAA's circular glass building opened in 2004 and immediately became one of the most visited museums in the world. The permanent collection includes Leandro Erlich's Swimming Pool installation (look up through the glass floor from below — you see people walking on water) and works by James Turrell. The building is as interesting as the art." },
      { label: "Omicho Market", text: "The covered market that has operated since 1721 — 180 shops selling live seafood, Kaga vegetables, local sake, and every ingredient the Kanazawa kitchen requires. The snow crab season (November–March) turns the market into something extraordinary. Eat at one of the small sushi counters inside the market at lunch." },
      { label: "Nagamachi samurai district", text: "The neighborhood where Kanazawa's samurai families lived — earthen walls, narrow lanes, and several restored samurai houses open to visitors. Nomura-ke is the most complete: a machiya townhouse with garden, tea room, and family artifacts. Walk Nagamachi in the morning before the tour groups from Kyoto arrive by bus." },
    ],
    eat: [
      { name: "Omicho Market sushi counters", desc: "The small sushi bars inside the Omicho Market serve the catch from that morning at a counter with eight seats. The omakase at lunch is ¥3,000–5,000 for ten pieces of the best seasonal fish available. No reservations — arrive at 11:30am before they open and join the line." },
      { name: "Miyoshian (Kenroku-en)", desc: "A traditional kaiseki restaurant in a thatched building inside the garden grounds. The seasonal lunch menu uses Kaga vegetables (Kanazawa's distinctive regional produce) and Sea of Japan seafood. Eating inside the garden is a specific experience." },
      { name: "Tamazushi", desc: "The most celebrated sushi restaurant in Kanazawa — chef Takahashi sources exclusively from the Omicho Market and the Sea of Japan. The omakase counter seats eight. The snow crab in winter is the reason serious food travelers come to Kanazawa specifically." },
      { name: "Fumuroya Cafe (Higashi Chaya)", desc: "A sake shop and cafe in a converted chaya in the geisha district. Amazake (sweet fermented rice drink), gold leaf soft serve (Kanazawa produces 99% of Japan's gold leaf), and sake from the Noto Peninsula producers. Sit in the tatami room upstairs." },
    ],
    stay: [
      { name: "Kanazawa Hakuchoan", tier: "High end", desc: "A ryokan in the Higashi Chaya district — seven rooms in a restored chaya building, seasonal kaiseki, a garden with a stone bath. The most atmospheric stay in Kanazawa." },
      { name: "Hotel Intergate Kanazawa", tier: "Mid range", desc: "A well-designed business hotel in the city center with free sake hour from 6–8pm, an excellent breakfast, and rooms that are significantly larger than Tokyo equivalents at the same price. The best mid-range option in the city." },
      { name: "Oyado Yutorelo Kanazawa", tier: "Good value", desc: "A small guesthouse in a traditional machiya townhouse near the Nagamachi samurai district. The owner speaks English, knows the city intimately, and provides the kind of local knowledge no guidebook has." },
      { name: "Kinjohro", tier: "High end", desc: "The most historic hotel in Kanazawa — a ryokan that has operated for 180 years, famous for its Kanazawa cuisine and a garden that turns extraordinary in autumn. The kaiseki here uses techniques specific to the Kaga region that exist nowhere else in Japan." },
    ],
    logistics: [
      { q: "When to go", a: "Year-round but each season is distinct. Spring (April): cherry blossom in Kenroku-en, the garden at its most photographed. Autumn (October–November): maple foliage, the best weather. Winter (November–March): snow crab season at Omicho Market — the single best reason to visit Kanazawa, and the market in snow is extraordinary. Summer is humid but festival season (Hyakumangoku Festival in June is one of Japan's largest)." },
      { q: "Getting there", a: "Shinkansen from Tokyo to Kanazawa: 2.5 hours on the Hokuriku Shinkansen (¥14,000). From Kyoto or Osaka: limited express train via Tsuruga (2.5–3 hours). The Kanazawa station is famous in Japan — the Tsuzumi-mon gate (a drumstick-shaped wooden gate) is one of the most photographed train stations in the world." },
      { q: "Getting around", a: "The city center is compact and walkable — Higashi Chaya, Kenroku-en, Nagamachi, and the 21st Century Museum are all within 30 minutes on foot. Loop buses (¥200 per ride, ¥500 day pass) connect the main sights. Rent a bicycle for the Noto Peninsula day trip." },
      { q: "The Noto Peninsula", a: "A long peninsula jutting into the Sea of Japan north of Kanazawa — dramatic coastline, fishing villages, the Wajima morning market (operating for 1,000 years), and sake breweries using water from the peninsula's wells. A full day trip by car or rental bicycle. The landscape on the west coast (Chirihama beach — you can drive on the sand) and the east coast (steep cliffs dropping to the sea) are completely different." },
      { q: "How long", a: "Two nights minimum, three ideally. Day one: Omicho Market breakfast, Nagamachi, Higashi Chaya afternoon, sake tasting. Day two: Kenroku-en early morning, 21st Century Museum, kaiseki dinner. Day three: Noto Peninsula day trip. Kanazawa works as a Shinkansen stop between Tokyo and Kyoto — most people do one night. Do two." },
      { q: "Money", a: "Kanazawa is cheaper than Tokyo and Kyoto. Omicho Market sushi lunch: ¥3,000–5,000. Kanazawa Hakuchoan: ¥40,000–80,000 per person including meals. Hotel Intergate: ¥12,000–20,000. Kenroku-en entry: ¥320. 21st Century Museum: ¥1,200 for ticketed exhibitions. A full day in Kanazawa with meals and museums: ¥8,000–15,000 excluding accommodation." },
    ],
  },
  {
    name: "Naoshima", country: "japan", tag: "Contemporary Art · Tadao Ando · Island",
    hook: "A fishing island in the Seto Inland Sea that became one of the most important contemporary art destinations in the world. The pumpkins are real.",
    img: "https://images.unsplash.com/photo-1578662996442-48f60103fc96?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("beauty")||a[0]?.includes("culture")) s+=4; if(a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=3; if(a[6]?.includes("absorb")||a[6]?.includes("nothing")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=4; if(a[8]?.includes("feel")||a[8]?.includes("article")) s+=3; return s; },
    intro: "Naoshima is a small island in the Seto Inland Sea between Honshu and Shikoku that transformed itself from a struggling industrial port into one of the most significant contemporary art destinations in the world. The Benesse Art Site — a collaboration between the Fukutake Foundation and architect Tadao Ando — embedded art directly into the island's landscape, its abandoned houses, and its coastline. Yayoi Kusama's yellow pumpkin on the pier is the image everyone knows. The reality is more extraordinary: the Chichu Art Museum buried underground so as not to disturb the view, James Turrell's light installations in rooms you book weeks in advance, Walter De Maria's sphere of Aji granite that you see by appointment only. The island has 3,000 residents, no traffic lights, and a bus system run on the honor system.",
    highlights: [
      { label: "Chichu Art Museum", text: "Tadao Ando's underground museum — entirely below ground to preserve the island's skyline — contains five works by three artists: Claude Monet's Water Lilies in a room lit only by natural light, James Turrell's Open Sky (a room where the ceiling is the sky), and Walter De Maria's Time/Timeless/No Time. Entry is timed and ticketed — book online weeks ahead. The most architecturally significant museum in Japan." },
      { label: "Art House Project", text: "Six traditional houses in the village of Honmura that have been converted into permanent artworks. Tatsuo Miyajima's Sea of Time '98 (LED counters embedded in the floor, counting at different speeds, reflected in shallow water), James Turrell's Backside of the Moon (complete darkness, pure color), and others. Each requires a separate ticket. Walk the village between them." },
      { label: "Benesse House Museum", text: "Tadao Ando's museum and hotel on the southern coast — the building is the museum, the artworks are installed throughout the structure and on the grounds. Bruce Nauman, Richard Serra, Jannis Kounellis. The outdoor pieces on the coastal path are the best. The pier with Kusama's yellow pumpkin is a five-minute walk." },
      { label: "Lee Ufan Museum", text: "A second Tadao Ando building on the island, dedicated to Korean-Japanese artist Lee Ufan — a founder of the Mono-ha movement. Ando designed the building to have almost no windows, so the art and the space are the only experience. Austere, precise, extraordinary." },
    ],
    eat: [
      { name: "Benesse House Restaurant", desc: "The restaurant at the Benesse House hotel — locally sourced Seto Inland Sea fish, Shodoshima olive oil, Kagawa udon. The terrace looks over the sea toward the mainland. Lunch only for non-guests; dinner is reserved for hotel guests." },
      { name: "Naka-oku (Honmura village)", desc: "A small restaurant in a renovated old house in Honmura run by an islander. The menu changes daily based on what came in — grilled fish, miso soup with clams, rice from the island's paddies. The most honest meal on Naoshima." },
      { name: "Shoya (near the ferry port)", desc: "Udon and curry rice served in a 100-year-old building near the Miyanoura ferry port. The inari sushi (fried tofu pouches filled with rice) is made every morning by the owner. Lunch only, closes when they run out." },
    ],
    stay: [
      { name: "Benesse House", tier: "High end", desc: "The only hotel on the island's art circuit — staying here means access to the museum after the day visitors leave, breakfast in the building Tadao Ando designed, and the Kusama pumpkin at dawn with nobody else around. Four building options; the Oval (connected to the museum by monorail) is the most extraordinary." },
      { name: "Naoshima International Villa", tier: "Mid range", desc: "Isozaki Arata-designed villas on a hill with sea views. Not as embedded in the art circuit as Benesse but architecturally significant in their own right. Self-catering, peaceful, the best value for overnight stays on the island." },
      { name: "Guesthouses in Honmura", tier: "Good value", desc: "Several islander-run guesthouses in the village of Honmura — simple rooms, shared baths, dinners cooked by the host family. Staying in the village puts you inside the Art House Project with no other tourists in the evening. Book directly." },
      { name: "Day trip from Okayama", tier: "Good value", desc: "Naoshima is 50 minutes by ferry from Uno port (Okayama). A day trip leaves enough time for Chichu and the Art House Project. Stay in Okayama (an underrated city with the third-best garden in Japan, excellent ramen) and take the early ferry." },
    ],
    logistics: [
      { q: "When to go", a: "Tuesday–Sunday only — all museums close Monday. Spring and autumn are ideal. The island is busiest on weekends and during the Setouchi Triennale (an international art festival held every three years in the Seto Inland Sea). Summer weekends in July–August are extremely crowded — go on a weekday. Winter is quiet and cold but all museums remain open." },
      { q: "Getting there", a: "From Osaka or Kyoto: Shinkansen to Okayama (45 minutes), then local train to Uno port (50 minutes), then ferry to Naoshima (20 minutes). Total journey: 2–2.5 hours. From Tokyo: Shinkansen to Okayama (3.5 hours). The Uno–Naoshima ferry runs multiple times daily; the slower car ferry (50 minutes) allows bicycle transport." },
      { q: "Getting around", a: "Rent a bicycle at the Miyanoura ferry port — ¥1,000 per day for a standard bike, ¥1,500 for electric. The island is 14km across; the main art sites are connected by a coastal road. A community bus runs between Miyanoura and Honmura. The Benesse House shuttle runs for guests. Walking between sites takes 20–40 minutes." },
      { q: "Booking museums", a: "The Chichu Art Museum requires advance online booking (book weeks ahead for weekends). The Art House Project requires separate tickets purchased at the Honmura Lounge. The Lee Ufan Museum and Benesse House Museum are ticketed at the door but sell out on busy days — arrive early. Walter De Maria's installation requires a separate appointment." },
      { q: "How long", a: "One full day is the minimum for Chichu and the Art House Project. Two days allows you to see everything properly and experience the island at dawn and dusk when the day visitors have left. Stay overnight if possible — the island changes completely after the ferries stop." },
      { q: "Money", a: "Chichu Art Museum: ¥2,100. Art House Project: ¥1,050 for all six houses. Lee Ufan Museum: ¥1,050. Benesse House Museum: ¥1,300. Benesse House hotel: ¥60,000–120,000 per person. Naoshima International Villa: ¥20,000–35,000. Guesthouses: ¥8,000–15,000 including dinner. Ferry: ¥1,220 return. Bicycle: ¥1,000 per day." },
    ],
  },
  {
    name: "Yakushima", country: "japan", tag: "Ancient Cedar · Wilderness · Princess Mononoke",
    hook: "The forest that Hayao Miyazaki used as the model for Princess Mononoke. The cedar trees are older than most civilizations. Almost nobody makes the journey.",
    img: "https://images.unsplash.com/photo-1501854140801-50d01698950b?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")||a[0]?.includes("adventure")) s+=4; if(a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=5; if(a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=3; if(a[6]?.includes("physical")||a[6]?.includes("explore")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=4; if(a[8]?.includes("none")||a[8]?.includes("feel")) s+=3; return s; },
    intro: "Yakushima is a round island 60km south of Kyushu, covered almost entirely in ancient cedar forest. The Yakusugi cedar trees — only those over 1,000 years old earn the name — are among the oldest living things on earth. Jomon Sugi, the oldest on the island, is estimated at between 2,170 and 7,200 years old and was growing before Rome was founded. The island receives rainfall measured in meters per month (it rains here 35 days in any given month, the locals say). The forest is consequently the most densely vegetated in Japan — moss covers every surface, the rivers run green, the deer and monkeys have never learned to fear humans. Studio Ghibli's Hayao Miyazaki spent weeks here before making Princess Mononoke. The island is a UNESCO World Heritage Site and receives a fraction of the visitors it deserves.",
    highlights: [
      { label: "Jomon Sugi trail", text: "The 22km return hike to the oldest cedar on the island — a full day, starting at 5am from the Arakawa trailhead by shuttle bus. The trail passes through forest that becomes progressively more ancient: first plantation cedar, then natural forest, then the towering Yakusugi that have been here for millennia. Jomon Sugi itself is enormous and behind a viewing platform — the scale becomes apparent slowly. One of the great hikes in Japan." },
      { label: "Shiratani Unsuikyo Ravine", text: "The ravine that Miyazaki walked repeatedly before designing the forest in Princess Mononoke. A 2–4 hour trail through mossy boulders, suspension bridges over rushing streams, and ancient cedar. The Taikoiwa viewpoint looks over the forest to the sea. More accessible than the Jomon Sugi trail and, in some ways, more beautiful." },
      { label: "Sea turtles (May–August)", text: "Yakushima's beaches — particularly Nagata Inakahama on the northwest coast — are one of the most important loggerhead sea turtle nesting sites in the Northern Hemisphere. Between May and August, females come ashore at night to lay eggs; the hatchlings emerge six weeks later. Guided night watching tours are organized by the island's conservation groups." },
      { label: "Onsen", text: "The island has several natural hot springs fed by Yakushima's geothermal activity. Hirauchi Kaichu Onsen is the most dramatic — a tidal pool onsen on the rocky coast that is only accessible at low tide. Soak in water that ranges from the sea to 40°C while watching the Pacific. Free entry, no facilities, extraordinary." },
    ],
    eat: [
      { name: "Shiosai (Miyanoura)", desc: "A small restaurant near the main port serving flying fish (tobiko) — Yakushima's signature ingredient — in multiple preparations: sashimi, fried, in ramen broth. The flying fish ramen is specific to the island and extraordinary." },
      { name: "Yakushima Brewery", desc: "A craft brewery using Yakushima spring water (some of the purest in Japan) and local ingredients. The cedar-smoked ale is brewed with Yakushima cedar shavings. Tastings in the brewery, bottles available to take." },
      { name: "Guesthouse meals", desc: "Most accommodation on Yakushima includes dinner — fresh fish from the surrounding waters, mountain vegetables from the island's farms, locally brewed shochu. The best meals on the island are served at guesthouses by islander families, not in restaurants." },
    ],
    stay: [
      { name: "Sankara Hotel & Spa", tier: "High end", desc: "A luxury resort in the forest on the south coast with private villas, a spa using Yakushima cedar oil treatments, and a restaurant sourcing exclusively from the island. The pool looks over the Pacific. The only world-class resort on the island." },
      { name: "Yakushima Youth Hostel", tier: "Good value", desc: "The best base for the Jomon Sugi trail — the hostel provides packed lunches, trail information, and shuttle bus tickets, and the other guests are almost all serious hikers. Family rooms available. The owner has hiked every trail on the island." },
      { name: "Guesthouses (minshuku)", desc: "The most authentic Yakushima experience — family-run guesthouses throughout the island, meals included, the host family as guide. Several in Yakusugi Land and near the Shiratani trailhead. Book direct; most require Japanese or basic English communication." },
      { name: "Hoshizuna-no-hama Camping", tier: "Good value", desc: "Camping on the north coast beach under the stars — Yakushima has almost no light pollution. The Perseid meteor shower in August is extraordinary from this beach. Facilities are basic but functional." },
    ],
    logistics: [
      { q: "When to go", a: "May–October for hiking (trails are open but wet year-round). Sea turtle nesting: May–August. Cherry blossom on the mountain: March–April while the coast is already in summer. The island receives 4,000–10,000mm of rain per year — pack waterproof everything regardless of season. The rainy season (June–July) is actually fine for hiking — the forest is at its most vivid and the crowds are lower." },
      { q: "Getting there", a: "Fly from Kagoshima (35 minutes, multiple daily flights on JAC) — the most practical option. Or ferry from Kagoshima: the high-speed Toppy takes 2 hours (¥10,000 one way), the overnight car ferry takes 10 hours (¥5,000). The ferry is the experience — arrive at the island by sea at dawn." },
      { q: "Getting around", a: "Rent a car at the ferry port or airport — essential for reaching trailheads and beaches on a flexible schedule. The island road circles the coast with mountain roads branching into the interior. The Jomon Sugi trailhead (Arakawa) is accessible only by shuttle bus from the Yakusugi Museum (April–November) — private cars are prohibited on this road during peak season." },
      { q: "The Jomon Sugi hike", a: "22km return, 1,400m elevation gain, 8–10 hours. Start at 5am from Yakusugi Museum by shuttle bus (¥440 each way, book ahead in spring). Bring: 2 liters of water, a packed lunch, waterproof layers, trekking poles, head torch. The trail is well maintained but long. The first 2km are on an old narrow-gauge railway track. Weekday departures are significantly less crowded than weekends." },
      { q: "How long", a: "Four nights minimum. Day one: arrive, Shiratani Unsuikyo Ravine (easier introduction to the forest). Day two: Jomon Sugi full day — this requires the whole day. Day three: rest, coast exploration, Hirauchi Kaichu Onsen at low tide. Day four: north coast beaches, turtle watching evening (seasonal). Day five: depart." },
      { q: "Money", a: "Sankara Hotel: ¥60,000–100,000 per person including meals. Yakushima Youth Hostel: ¥4,500–7,000 including dinner. Minshuku guesthouses: ¥8,000–15,000 including two meals. Flights Kagoshima–Yakushima: ¥8,000–15,000. Toppy ferry: ¥10,000 one way. Shuttle bus to Arakawa: ¥880 return. Car rental: ¥8,000–12,000 per day." },
    ],
  },
  {
    name: "Tohoku", country: "japan", tag: "Onsen · Cedar Forests · The Japan Nobody Visits",
    hook: "The north that most tourists skip entirely. Ancient cedar avenues, samurai castle towns, onsen buried in mountain gorges, and the most atmospheric winter in Japan.",
    img: "https://images.unsplash.com/photo-1545569341-9eb8b30979d9?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("culture")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=4; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=3; if(a[5]?.includes("mountains")||a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("nothing")||a[6]?.includes("wander")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=5; if(a[8]?.includes("none")||a[8]?.includes("people")) s+=3; return s; },
    intro: "Tohoku is the six prefectures of northern Honshu — the part of Japan that most visitors fly over on the way to Hokkaido. It was hit by the 2011 earthquake and tsunami and has been quietly rebuilding ever since, emerging as the most undervisited and, in many ways, most genuinely Japanese region in the country. The Oku-no-Hosomichi — Matsuo Basho's famous 17th-century journey through the north — passes through its most atmospheric places: Matsushima Bay (one of Japan's three most celebrated views), the mountain temples of Yamadera, the cedar avenue at Nikko, the castle town of Kakunodate with its samurai district intact. The Nyuto Onsen in Akita Prefecture is the most atmospheric hot spring resort in Japan — seven ryokan inns clustered around milky-white sulphurous pools in a mountain gorge, accessible by bus from a small station, snow-covered from November to April.",
    highlights: [
      { label: "Nyuto Onsen", text: "Seven ryokan clustered around a series of sulphurous hot springs in a mountain gorge in Akita — the most atmospheric onsen destination in Japan. The waters are milky white with minerals, the outdoor baths (rotenburo) are carved from rock, and the ryokan have been here for over 300 years. Tsurunoyu is the oldest and most beautiful — outdoor mixed bathing in a thatched-roof bath with the forest above. Book months ahead." },
      { label: "Kakunodate", text: "A former castle town in Akita Prefecture with the best-preserved samurai district in Japan — a street of old samurai residences, weeping cherry trees planted 300 years ago, and the quiet of a town that has not been turned into a tourist attraction. The cherry blossom here in late April is among the most beautiful in the country." },
      { label: "Yamadera", text: "The mountain temple (Risshakuji) that Basho visited in 1689 and wrote his most famous haiku about — 'silence, the cicada's cry penetrates the rocks.' 1,015 stone steps climb through ancient cedars to the main hall perched on the cliff. At dawn in autumn it sits in cloud. One of the most beautiful temple sites in Japan." },
      { label: "Matsushima Bay", text: "A bay scattered with 260 pine-covered islands, considered one of Japan's three most celebrated views. The Zuigan-ji temple was built in 828 and has been rebuilt by successive rulers — the carved cave shrines along the approach path are from the original construction. Take the sightseeing boat between the islands at dusk." },
    ],
    eat: [
      { name: "Wanko soba (Morioka/Hanamaki)", desc: "The Iwate Prefecture tradition of wanko soba — servers continuously top up your small bowl of buckwheat noodles until you put the lid on. The challenge is how many bowls you can eat (the average is 50; the record is over 500). A genuine regional experience." },
      { name: "Gyutan (Sendai)", desc: "Sendai's signature dish — grilled beef tongue, sliced thin, charcoal-grilled, served with barley rice and oxtail soup. Rikyu in Sendai is the original restaurant, open since 1948. Lunch queue starts at 11am." },
      { name: "Ryokan kaiseki (Nyuto Onsen)", desc: "Dinner at any of the Nyuto Onsen ryokan is the highlight of eating in Tohoku — mountain vegetables, freshwater fish from the Tazawa Lake, local sake from Akita's rice paddies. The meal is served in your tatami room." },
      { name: "Kiritanpo (Akita)", desc: "Akita's regional dish — pounded rice molded onto cedar skewers, grilled, then simmered in a chicken and burdock hot pot. Specific to Akita Prefecture, available October–March when the new rice harvest is in. The taste of the north." },
    ],
    stay: [
      { name: "Tsurunoyu Onsen (Nyuto)", tier: "Mid range", desc: "The oldest and most celebrated of the Nyuto Onsen ryokan — thatched roof, outdoor milky-white sulphur baths, winter snow. The rooms are traditional and simple; the experience is extraordinary. Book four months ahead for weekends." },
      { name: "Samurai residence guesthouses (Kakunodate)", tier: "Good value", desc: "Several of the old samurai houses in Kakunodate accept guests — simple rooms in buildings that are several hundred years old. The most authentic accommodation in Tohoku." },
      { name: "Kokeshi-themed guesthouses (Naruko Onsen)", tier: "Good value", desc: "Naruko Onsen in Miyagi is famous for kokeshi wooden dolls and has a cluster of family-run onsen guesthouses. The waters here are sulphurous and the landscape in autumn is extraordinary." },
      { name: "Sendai city hotels", tier: "Mid range", desc: "Sendai is the regional hub — use it as a base for day trips. Sendai Kokusai Hotel and Hotel Metropolitan are the reliable mid-range options, both walkable to the gyutan restaurants and the station." },
    ],
    logistics: [
      { q: "When to go", a: "Autumn (October–November) is the peak season — the foliage across Tohoku is extraordinary. Winter (December–March) for snow and the Nyuto Onsen experience at its most atmospheric. Spring for the Kakunodate cherry blossom (late April). Summer is festival season — the Nebuta Festival in Aomori (August) is one of the most spectacular in Japan." },
      { q: "Getting there", a: "Shinkansen from Tokyo to Sendai: 90 minutes (¥11,000). Sendai is the gateway to Tohoku. From Sendai, local trains and buses reach Matsushima (25 minutes), Yamadera (1 hour), and connections to the Nyuto Onsen bus (2.5 hours to Tazawako station, then 50 minutes by bus)." },
      { q: "The JR Pass", a: "The Japan Rail Pass (purchased before entering Japan) covers all Shinkansen and most express trains. For a two-week Japan trip covering Tokyo, Kyoto, Kanazawa, and Tohoku, the 14-day pass (¥50,000) pays for itself by the third Shinkansen journey. Buy it before you leave home." },
      { q: "Getting around Tohoku", a: "The Shinkansen connects Sendai, Morioka, Aomori, and Akita. Beyond the main cities, local trains and buses cover most destinations but schedules are infrequent — plan carefully or rent a car. A car is strongly recommended for the Nyuto Onsen area and rural Akita Prefecture." },
      { q: "How long", a: "Five nights covers the highlights. Night one in Sendai (gyutan dinner, Matsushima day trip). Nights two and three at Nyuto Onsen (book way ahead). Night four in Kakunodate (samurai district, sake brewery). Night five in Morioka (wanko soba, the city is underrated). Return Shinkansen to Tokyo." },
    ],
  },
  {
    name: "Kyushu", country: "japan", tag: "Fukuoka · Ramen · Nagasaki · Volcanic",
    hook: "The best ramen in Japan is in Fukuoka. The most moving memorial in Japan is in Nagasaki. The most active volcano in Japan is here. And almost nobody comes.",
    img: "https://images.unsplash.com/photo-1542051841857-5f90071e7989?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("culture")||a[0]?.includes("adventure")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=2; if(a[5]?.includes("coast")||a[5]?.includes("mountains")) s+=3; if(a[6]?.includes("eat")||a[6]?.includes("explore")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; if(a[8]?.includes("people")||a[8]?.includes("none")) s+=2; return s; },
    intro: "Kyushu is Japan's third-largest island and the least visited by foreign tourists. Fukuoka, its capital, is consistently rated among the most livable cities in Asia and is the origin of Hakata ramen — the rich tonkotsu broth that spawned an entire global category. The city's yatai (open-air food stalls) along the Naka River are the most atmospheric street food scene in Japan. Nagasaki — the city that was the second atomic bomb target on August 9, 1945 — has rebuilt itself into a port city of extraordinary character, Portuguese and Dutch heritage mixed into the Japanese fabric, the Peace Park and the Atomic Bomb Museum among the most affecting places in Japan. Mount Aso in the center of the island is one of the largest active calderas in the world, still smoking. Beppu is the onsen capital of Japan — 2,900 springs producing more hot water than anywhere except Yellowstone.",
    highlights: [
      { label: "Fukuoka yatai and ramen", text: "The yatai are open-air stalls that appear along the Naka River and in Nakasu from 6pm — small covered counters serving ramen, yakitori, and beer to a mix of salarymen and tourists. They have operated in Fukuoka for over a century. Sit at the counter, order Hakata ramen, add extra noodles (kaedama) when the broth is still hot. The stall culture disappears during rain." },
      { label: "Nagasaki Peace Park and Museum", text: "The hypocenter of the August 9, 1945 bomb is marked by a black monolith in a small park. The Peace Park above it has the iconic peace statue. The Atomic Bomb Museum below is the most carefully curated memorial museum in Japan — specific, personal, unsparing. Allow three hours. It is not like other museums." },
      { label: "Mount Aso caldera", text: "The active caldera of Mount Aso — one of the largest in the world — can be approached by road to within 100 metres of the crater rim when volcanic activity permits (the road closes when SO2 levels are high). The caldera is 25km across; five peaks ring it. The Kusasenri plateau inside the caldera with wild horses grazing is genuinely surreal." },
      { label: "Beppu hell springs", text: "The Beppu Jigoku (hells) — eight dramatically different hot springs, each a different color and temperature. Blood Pond Hell is red from iron oxide. Sea Hell is cobalt blue. Waterspout Hell erupts every 30 minutes. Not for bathing — for witnessing. The Beppu onsen city around them is for bathing: 2,900 springs and a culture that uses hot water for everything." },
      { label: "Kumamoto Castle", text: "The black castle — one of Japan's three greatest castles — was severely damaged in the 2016 Kumamoto earthquake and has been under meticulous reconstruction since. The scaffolded sections are open to visitors to watch the restoration in progress. The remaining original structures and the approach path through the cherry trees are extraordinary." },
    ],
    eat: [
      { name: "Shin-Shin (Fukuoka)", desc: "The most celebrated Hakata ramen restaurant in Fukuoka. Tonkotsu broth simmered for 18 hours, thin straight noodles, chashu pork, pickled ginger. The line forms before opening. Two locations in the city center. ¥750 for a bowl." },
      { name: "Fukuoka yatai", desc: "Pick any stall along the Naka River that has empty seats. The ramen at the yatai is not always the best in the city but the experience of eating under canvas beside the river at 11pm is not available anywhere else in Japan." },
      { name: "Tsuruya (Nagasaki)", desc: "A champon restaurant — Nagasaki's Chinese-Japanese noodle soup, thicker than ramen, with vegetables, seafood, and pork in a milky stock. Tsuruya has been making champon since 1899. The original Ringer Hut chain also started here; the Nagasaki champon is specific to the city." },
      { name: "Jidori chicken (Miyazaki)", desc: "Miyazaki Prefecture produces the best chicken in Japan — the free-range jidori birds are charcoal-grilled and served with yuzu pepper (another Kyushu specialty). Ozaki Beef (Miyazaki wagyu) is the local alternative to Kobe — less famous, equally extraordinary." },
    ],
    stay: [
      { name: "The Lively Fukuoka (Hakata)", tier: "Mid range", desc: "A well-designed hotel in the Hakata district — walking distance to the yatai, the ramen shops, and Fukuoka station. Excellent breakfast, roof terrace, the best mid-range base in the city." },
      { name: "Beppu Kamenoi Hotel", tier: "Mid range", desc: "An old-school onsen hotel in Beppu — multiple baths fed by different springs, tatami rooms, the full Beppu experience without the luxury hotel price. The sand bath (hot spring sand buried up to your chin) is on-site." },
      { name: "Nishikan (Nagasaki)", tier: "Mid range", desc: "A small ryokan in the Higashiyamate neighborhood above the harbor — the area that Portuguese and Dutch traders settled in the 17th century. Views over the port, tatami rooms, breakfast of Nagasaki champon." },
      { name: "Aso Base Backpackers", tier: "Good value", desc: "A hostel inside the Aso caldera run by a former guide who knows every trail on the volcano. Private rooms available. The most practical base for Mount Aso with shuttle runs to the crater and the Kusasenri plateau." },
    ],
    logistics: [
      { q: "When to go", a: "Year-round. Spring (March–April) for cherry blossom at Kumamoto Castle. Summer is hot and humid but the yatai operate year-round. Autumn (October–November) for foliage and comfortable hiking temperatures. Winter is mild compared to Honshu — Kyushu rarely gets snow below the mountains." },
      { q: "Getting there", a: "Fly into Fukuoka (FUK) — direct flights from most Asian hubs and from Tokyo (1.5 hours, ¥8,000–20,000). Or Shinkansen from Osaka to Fukuoka (2.5 hours, ¥15,000). Within Kyushu, the Kyushu Shinkansen connects Fukuoka to Kumamoto (35 minutes) and Kagoshima (1.5 hours). The Kyushu Rail Pass covers all local Shinkansen and limited express trains for 3, 5, or 7 days." },
      { q: "Getting around", a: "Fukuoka is compact and walkable/bikeable. Rent a car for Mount Aso, the rural onsen, and the Miyazaki coast — public transport covers the main cities but not the volcanic interior. The Beppu–Aso–Kumamoto drive is one of the best road trips in Japan." },
      { q: "Nagasaki from Fukuoka", a: "2 hours by limited express train (¥4,000). Worth a full day or an overnight. The Peace Park and Museum in the morning (three hours), champon lunch, Glover Garden (the 19th-century Western trader residence that inspired Puccini's Madame Butterfly) in the afternoon, Nagasaki night view from Mount Inasa in the evening." },
      { q: "How long", a: "Five nights covers Kyushu properly. Two nights in Fukuoka (yatai every evening, day trip to Nagasaki). One night at Beppu or Yufuin onsen. One night at Mount Aso caldera. One night in Kumamoto (the castle, Suizenji Garden, horse sashimi — a Kumamoto specialty). Fly home from Kagoshima or return to Fukuoka." },
    ],
  },
  {
    name: "Hokkaido", country: "japan", tag: "Niseko · Powder Snow · Sapporo · Wild North",
    hook: "The best powder snow in the world. A city with more ramen shops per capita than anywhere in Japan. Brown bears. Drift ice on the sea in February.",
    img: "https://images.unsplash.com/photo-1551244072-5d12893278bc?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("food")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("balanced")) s+=3; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=3; if(a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=3; if(a[6]?.includes("physical")||a[6]?.includes("explore")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=2; if(a[6]?.includes("fullday")) s+=2; return s; },
    intro: "Hokkaido is Japan's northernmost and second-largest island — a place that feels genuinely different from the rest of the country. The Ainu people were here for millennia before Japanese settlement in the 19th century, and their culture survives in place names, food traditions, and a new national museum in Shiraoi. Niseko, in the southwest, has become the most coveted ski destination in the world among serious skiers — the powder snow that falls from Siberian storm systems is uniquely dry and deep, and the runs from the Annupuri and Hirafu peaks are exceptional. Sapporo, the capital, has the best ramen in Japan (the Ramen Alley in Susukino has been operating since 1951), an annual snow festival in February that draws two million visitors, and a food culture built on corn, dairy, crab, and lamb. The Shiretoko Peninsula in the far northeast is a UNESCO World Heritage wilderness where brown bears fish the rivers and drift ice floats in from the Okhotsk Sea.",
    highlights: [
      { label: "Niseko powder skiing", text: "The combination of cold Siberian air and warm Sea of Japan moisture creates snow with a moisture content of 6–8% — the driest powder in the world outside Utah. The four interconnected resorts (Grand Hirafu, Hanazono, Niseko Village, Annupuri) offer 60 runs and extraordinary backcountry access. The après-ski village of Hirafu has the best sushi restaurants outside Tokyo at resort prices." },
      { label: "Sapporo Ramen Alley", text: "Nijo Ichiba (the covered market) in the morning for king crab breakfast and sea urchin on rice. The Ramen Alley (Ganso Sapporo Ramen Yokocho) in Susukino for miso ramen — Sapporo's specific regional style, developed in 1955, made with red miso and butter. The alley holds 17 restaurants in a space the width of a corridor." },
      { label: "Shiretoko Peninsula", text: "A UNESCO World Heritage wilderness in the far northeast of Hokkaido, accessible only by a single road that ends at a waterfall. Brown bears fish the rivers from late June through October — bear watching tours approach by boat along the coast. In February, drift ice (ryuhyo) arrives from the Okhotsk Sea and covers the water — icebreaker tours run from Abashiri." },
      { label: "Biei Blue Pond", text: "A pond created accidentally by a landslide mitigation project that turned intensely turquoise from the aluminum hydroxide in the spring water feeding it. The dead trees standing in the turquoise water create a scene that looks digital and isn't. In winter it freezes and is lit at night. In summer it reflects the surrounding forest." },
      { label: "Sapporo Snow Festival", text: "The Sapporo Snow Festival (February, one week) fills Odori Park with snow sculptures the size of buildings — detailed recreations of world landmarks, original sculptures, ice slides for children. Two million people attend. The city also runs an ice sculpture contest in Susukino simultaneously. Book accommodation eight months ahead." },
    ],
    eat: [
      { name: "Sapporo Ramen Alley (Susukino)", desc: "17 ramen restaurants in a narrow alley, each with its own broth and style. Ramen Santouka serves the shio (salt) ramen that defined Hokkaido light broth. Yume-ya serves the miso ramen with butter and corn. Go at 11pm when the salarymen arrive after drinks." },
      { name: "Nijo Market (Sapporo)", desc: "The covered market two blocks from Odori Park — fresh king crab, sea urchin (uni), salmon roe. The kaisendon (seafood rice bowls) served at the market counters are the best value seafood meal in Hokkaido. ¥2,000–4,000 for a bowl with three toppings." },
      { name: "Niseko sushi (Hirafu)", desc: "The concentration of high-quality sushi restaurants in the Hirafu ski village is extraordinary for a mountain resort — Niseko Yukoro and Sushi Bon are the serious counters. Fresh Hokkaido uni and crab available in season." },
      { name: "Lamb BBQ — Jingisukan (Sapporo)", desc: "Hokkaido's signature meat dish — lamb and vegetables grilled on a domed iron griddle named after the shape of Genghis Khan's helmet. The Sapporo Beer Garden runs the largest jingisukan restaurant in the city (all-you-can-eat, ¥2,600) in the original 1890s brewery." },
    ],
    stay: [
      { name: "Park Hyatt Niseko Hanazono", tier: "High end", desc: "The benchmark ski resort hotel in Niseko — ski-in/ski-out from the Hanazono lifts, onsen, the best restaurants in the resort. The peak season rooms are extraordinary and priced accordingly." },
      { name: "Niseko Northern Resort Annupuri", tier: "Mid range", desc: "The quieter side of the Niseko resort area — the Annupuri lifts are less crowded than Hirafu, the accommodation is significantly cheaper, and the onsen is fed by natural hot springs. The mountain experience without the Hirafu prices." },
      { name: "JR Tower Hotel Nikko Sapporo", tier: "Mid range", desc: "In the JR Tower above Sapporo station — central, views of the city and mountains, direct access to the subway. The most practical mid-range hotel in Sapporo for exploring the city and the Snow Festival." },
      { name: "Shiretoko Grand Hotel (Utoro)", tier: "Good value", desc: "A large onsen hotel in Utoro on the Shiretoko Peninsula — the base for bear watching boat tours and drift ice cruises. Basic rooms, enormous onsen with sea views, the best location for Shiretoko wildlife experiences." },
    ],
    logistics: [
      { q: "When to go", a: "Ski season: December–March for Niseko (peak powder January–February). Snow Festival: first or second week of February (Sapporo). Wildlife: June–October for Shiretoko brown bears. Drift ice: late January–March. Summer (June–August): lavender fields at Furano, green hills, mild temperatures — the most popular domestic tourism season. Autumn (September–October): Hokkaido foliage is earlier and more dramatic than Honshu." },
      { q: "Getting there", a: "Fly into New Chitose Airport (CTS) from Tokyo (1.5 hours, ¥10,000–30,000) or from abroad. The airport is 40 minutes from Sapporo by express train. For Niseko: train or bus from Sapporo (2.5 hours). For Shiretoko: fly to Memanbetsu Airport (60 minutes from New Chitose) then rent a car." },
      { q: "Niseko specifics", a: "The four Niseko resorts are connected by an all-mountain pass (¥7,000–10,000 per day). Grand Hirafu is the main village with the most accommodation and nightlife. Hanazono and Niseko Village are quieter. Annupuri has the least crowded runs. A hire car or shuttle bus connects them. Book accommodation in January–February a full year ahead." },
      { q: "Getting around Hokkaido", a: "Rent a car — Hokkaido is large (83,000 km², larger than Ireland) and the best experiences are away from the main cities. The drives are extraordinary in all seasons. The JR Hokkaido trains connect Sapporo to Hakodate (3.5 hours), Asahikawa (1.5 hours), and Kushiro for Shiretoko connections. A car is essential for Furano, Biei, and the Shiretoko Peninsula." },
      { q: "How long", a: "Five nights minimum. Two nights in Sapporo (Snow Festival in winter, food focus any season). Two nights in Niseko (ski season) or Furano/Biei (summer/autumn). One night in Shiretoko (wildlife) or Hakodate (the most beautiful night view in Japan from Mount Hakodate). Hokkaido rewards a full week." },
      { q: "Money", a: "Niseko ski pass: ¥7,000–10,000 per day. Park Hyatt Niseko: ¥80,000–200,000 per room in peak season. Niseko Northern Resort: ¥20,000–50,000. JR Tower Sapporo: ¥15,000–25,000. Sapporo ramen: ¥900–1,500. Nijo Market kaisendon: ¥2,000–4,000. Jingisukan all-you-can-eat: ¥2,600. Bear watching boat tour (Shiretoko): ¥8,000." },
    ],
  },
];
// ─── NEW ZEALAND REGIONS ─────────────────────────────────────────────────────
const newZealandRegions = [
  {
    name: "Queenstown & Fiordland", country: "newzealand", tag: "Fiords · Adventure · Remarkables",
    hook: "Milford Sound gets 7 metres of rain a year. Visit anyway. Especially in the rain.",
    img: "https://images.unsplash.com/photo-1507699622108-4be3abd695ad?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")) s+=4; if(a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=4; if(a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=4; if(a[6]?.includes("physical")||a[6]?.includes("explore")) s+=4; if(a[9]?.includes("generic")) s+=2; return s; },
    intro: "Queenstown sits on Lake Wakatipu with the Remarkables rising behind it — a town that has built an entire economy around the fact that the landscape is extraordinary. Bungee jumping was invented here. The skiing is world-class. But the real reason to come is Fiordland, 90 minutes west — a national park the size of a small country. Milford Sound is the most visited and still overwhelming: the 1,692m Mitre Peak rising vertically from the water, waterfalls that triple after rain, fur seals on the rocks. Go in the rain. Doubtful Sound is deeper, quieter, and requires an overnight — the most remote and extraordinary overnight boat journey in the Southern Hemisphere.",
    highlights: [
      { label: "Milford Sound", text: "The fiord everyone comes for and that still exceeds expectations. The drive in through the Homer Tunnel is half the experience. Take the first cruise of the morning before the day-trippers arrive from Queenstown. In heavy rain the waterfalls multiply from a handful to hundreds and the whole sound disappears into mist. The fur seals do not move regardless of weather." },
      { label: "Doubtful Sound overnight", text: "Three times the length of Milford Sound and a fraction of the visitors. Access by boat across Lake Manapouri, then bus over Wilmot Pass, then into the sound. The overnight cruise covers three arms of the fiord. The silence at night, broken only by Fiordland penguins and bottlenose dolphins, is the most complete wilderness experience in New Zealand." },
      { label: "Routeburn Track", text: "One of New Zealand's Great Walks — 32km through alpine valleys, over Harris Saddle, past Lake Harris. Three days hut-to-hut. The views from the saddle, with Fiordland on one side and the Humboldt Mountains on the other, are among the finest mountain views in the Southern Hemisphere. Book DOC huts months ahead." },
      { label: "Glenorchy", text: "45 minutes from Queenstown at the head of Lake Wakatipu — a small town where the Rees and Dart Rivers meet. Lord of the Rings was filmed here. Drive out at dawn, kayak the lake, walk the Paradise valley road. The most beautiful short drive from any tourist hub in New Zealand." },
      { label: "Coronet Peak & The Remarkables skiing", text: "Two ski fields above Queenstown with genuinely different personalities — Coronet Peak is more challenging, the Remarkables has the views. The Remarkables on a clear day looks over the lake and the mountains in every direction. Heli-skiing into the back country is available from both fields." },
    ],
    eat: [
      { name: "Rata (Queenstown)", desc: "Chef Josh Emett's flagship — New Zealand produce treated with real ambition. Central Otago lamb, Fiordland crayfish, locally grown vegetables. The best serious restaurant in Queenstown, in a converted stone building in the town center." },
      { name: "Fergburger (Queenstown)", desc: "The burger that built a reputation — open almost 24 hours, queues at 2am, genuinely extraordinary. The Big Al (double beef, bacon, cheese) is the order. Accept the line. It moves faster than it looks." },
      { name: "Amisfield Winery (Lake Hayes)", desc: "Central Otago pinot noir at the winery that makes some of the best of it. The Trust the Chef bistro menu changes seasonally. Drive out from Queenstown (20 minutes), eat lunch on the terrace, buy two bottles for the road." },
      { name: "Sherwood (Queenstown)", desc: "A restaurant and hotel with its own kitchen garden. The most thoughtful food in Queenstown — sourced from the property and from Central Otago farms. Sunday brunch on the lawn is the best meal in the region." },
    ],
    stay: [
      { name: "Blanket Bay Lodge (Glenorchy)", tier: "High end", desc: "A luxury lodge at the head of Lake Wakatipu — stone and timber buildings, a private jetty, guided walks into the surrounding wilderness. One of the great lodges of the Southern Hemisphere." },
      { name: "The Rees Hotel (Queenstown)", tier: "High end", desc: "On the lakefront with direct views of the Remarkables — apartments and suites, a serious restaurant, private boat available. The most complete luxury hotel in Queenstown." },
      { name: "Sherwood (Queenstown)", tier: "Mid range", desc: "A hotel, restaurant, and garden on the edge of town. Rooms are small but beautifully done; the communal spaces are the draw. The most thoughtfully designed mid-range stay in Queenstown." },
      { name: "Milford Sound Lodge", tier: "Good value", desc: "The only accommodation inside Milford Sound — riverside chalets, a riverside bar. Stay here to have the sound at dawn before any day-trippers arrive. Book months ahead." },
    ],
    logistics: [
      { q: "When to go", a: "Skiing: June-September (Coronet Peak and the Remarkables). Hiking: December-March — the Routeburn and Milford tracks fully open. Milford Sound year-round: summer clear and busy, winter quiet and sometimes snowy. Autumn (March-May) has the best light and fewest crowds. Avoid Christmas-January when domestic tourism peaks." },
      { q: "Getting there", a: "Fly into Queenstown Airport (ZQN) — direct flights from Sydney, Melbourne, Brisbane, Auckland. Car rental at the airport is essential. The drive to Milford Sound via Te Anau (280km each way) is one of the great road journeys in New Zealand." },
      { q: "Milford Sound logistics", a: "Drive from Queenstown via Te Anau (2 hours) then the Milford Road through the Homer Tunnel (1.5 hours). Total 3.5 hours each way. Book the earliest cruise available. Stay at Milford Sound Lodge to skip the drive entirely, or split the trip with a night in Te Anau." },
      { q: "How long", a: "Four nights. Nights one and two Queenstown (Glenorchy day trip, Amisfield lunch). Night three Te Anau. Night four Milford Sound Lodge or Doubtful Sound overnight. Return to Queenstown for flights." },
      { q: "Money", a: "Blanket Bay Lodge: NZ$2,000-4,000/night. The Rees: NZ$400-800. Sherwood: NZ$200-350. Milford Sound Lodge: NZ$180-300. Milford cruise: NZ$80-120. Routeburn huts: NZ$75/night. Fergburger: NZ$15-20. Budget NZ$250-400/person/day excluding accommodation." },
    ],
  },
  {
    name: "South Island Road Trip", country: "newzealand", tag: "Tekapo · Mount Cook · Mackenzie Basin",
    hook: "Lake Tekapo is that colour because of glacial flour suspended in the water. It looks fake. Drive here anyway.",
    img: "https://images.unsplash.com/photo-1469521669194-babb45599def?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")||a[0]?.includes("adventure")) s+=3; if(a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=3; if(a[5]?.includes("mountains")||a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("physical")||a[6]?.includes("spontaneous")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=3; return s; },
    intro: "The drive from Christchurch to Queenstown through the Mackenzie Basin is one of the great road journeys on earth. The landscape changes every 40 minutes. Lake Tekapo is turquoise from glacial flour ground from the mountains by the Tasman Glacier. Lake Pukaki is larger, less visited, and the reflection of Aoraki Mount Cook at dawn on a still morning is the defining image of the South Island. The Mackenzie Basin is also the largest Dark Sky Reserve in the Southern Hemisphere — the Milky Way is visible to the naked eye from the lake shore on any clear night.",
    highlights: [
      { label: "Lake Pukaki at dawn", text: "The largest Mackenzie glacial lake — turquoise water, the Southern Alps behind it, Aoraki at the far end. The highway viewpoint is everyone's stop; drive the lake road to the Mount Cook Village end for the reflection with nobody around. Dawn only — the wind picks up by 9am and the mirror surface disappears." },
      { label: "Aoraki Mount Cook", text: "New Zealand's highest peak at 3,724m. The Hooker Valley Track (3 hours return) walks to the Hooker Lake at the glacier's snout — on a clear day Aoraki fills the entire view. The Glacier Explorers boat tour navigates the Tasman Glacier lake, the largest glacier in Australasia, retreating visibly year on year." },
      { label: "Lake Tekapo stargazing", text: "The darkest skies in the Southern Hemisphere. The Church of the Good Shepherd on the lake's edge with the Milky Way above is the photograph that defines New Zealand travel. The Mt John Observatory runs guided tours with research telescope access. Book ahead in summer." },
      { label: "Lupin season (November-December)", text: "Wild lupins bloom along the lakeshores and roadsides of the Mackenzie Basin — purple, pink, yellow against the turquoise water. Technically invasive, ecologically complicated, visually extraordinary. The most photographed event in New Zealand." },
      { label: "Christchurch", text: "The city rebuilt after the 2011 earthquake into something genuinely interesting — the Transitional Cathedral (cardboard tubes, Shigeru Ban), the rebuilt arts precinct, punting on the Avon River still intact. Use it as the northern gateway to the road trip." },
    ],
    eat: [
      { name: "Kohan Restaurant (Lake Tekapo)", desc: "A Japanese restaurant on the lake run by a family that has been here for decades. The salmon comes from Mackenzie Basin river farms. Eating sashimi beside a turquoise glacial lake in the Southern Alps is a very specific experience." },
      { name: "Innate Cafe (Lake Tekapo)", desc: "The best breakfast in the Mackenzie Basin — good coffee, local salmon bagel, a view of the lake through the window. Opens early enough for a meal before the Mount Cook drive." },
      { name: "Christchurch restaurant scene", desc: "Post-earthquake Christchurch developed a genuine food culture. Gatherings, Roots, and the Riverside Market are the serious options. The best casual eating in the South Island's largest city." },
    ],
    stay: [
      { name: "Lake Tekapo Lodge", tier: "High end", desc: "Six rooms on the lakeshore with direct access to the dark sky reserve. The resident astronomer runs private stargazing sessions. Book the room with the outdoor bath facing the lake." },
      { name: "Peppers Bluewater Resort (Lake Tekapo)", tier: "Mid range", desc: "A well-positioned resort hotel on the lake edge — the views and location at a manageable price. The base for the observatory tours and the Tekapo hot springs." },
      { name: "Aoraki Court Motel (Mount Cook Village)", tier: "Good value", desc: "Basic but clean motel at the end of the road into Mount Cook Village — direct mountain views. Wake before dawn, walk to the Hooker trailhead. Steps from the start." },
      { name: "YHA Lake Tekapo", tier: "Good value", desc: "The hostel on the lake that has been sending travelers to the observatory for decades. Private rooms available. The best budget base in the Mackenzie Basin." },
    ],
    logistics: [
      { q: "The route", a: "Christchurch to Lake Tekapo (225km, 2.5 hours) — Lake Pukaki viewpoint (45 minutes) — Mount Cook Village (1 hour) — Queenstown via Lindis Pass (3.5 hours). Total 700km over 3-4 days. State Highway 8 through the Mackenzie Basin is one of the great drives in New Zealand." },
      { q: "When to go", a: "November-December for lupins. January-March for the best hiking weather at Mount Cook. April for autumn colour on the willows around Tekapo. Winter (June-August) for snow on the mountains and the clearest stargazing nights." },
      { q: "Getting there", a: "Fly into Christchurch (CHC) — international flights from Australia, Singapore, Dubai, and connections from Auckland. Pick up a rental car at the airport and the drive begins immediately. Or rent in Queenstown and do the route in reverse." },
      { q: "Stargazing logistics", a: "The Earth and Sky Observatory tours at Mt John run year-round — the two-hour evening session (NZ$175) includes telescope access and a guided tour of the Southern Hemisphere sky. Book ahead in summer. The Milky Way is visible to the naked eye from the lake shore on any clear night — no tour required." },
      { q: "How long", a: "Three nights covers the route well. Night one Christchurch. Night two Lake Tekapo (stargazing). Night three Mount Cook Village (Hooker Valley Track). Day four drive to Queenstown. Rushing it in two days is possible but the Mackenzie Basin rewards slowing down." },
    ],
  },
  {
    name: "Northland & Bay of Islands", country: "newzealand", tag: "Maori Culture · Ancient Kauri · Subtropical",
    hook: "The kauri trees here are 2,000 years old. The Treaty of Waitangi was signed here. The water is warm enough to swim in year-round.",
    img: "https://images.unsplash.com/photo-1504893524553-b855bce32c67?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("beauty")||a[0]?.includes("escape")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("wander")||a[6]?.includes("nothing")) s+=3; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=2; return s; },
    intro: "Northland is the subtropical peninsula reaching north from Auckland — almost entirely overlooked by international travelers who fly in and head straight to Queenstown. The Bay of Islands has 144 islands, clear water, and the Waitangi Treaty Grounds where New Zealand's founding document was signed in 1840. The Waipoua Forest holds the last significant stands of ancient kauri — Tane Mahuta, the largest living kauri, is 2,000 years old and 51 metres tall. Cape Reinga at the very tip is where, in Maori cosmology, the spirits of the dead depart for the underworld. The meeting of the Tasman Sea and the Pacific Ocean is visible from the lighthouse.",
    highlights: [
      { label: "Tane Mahuta", text: "The largest living kauri in New Zealand — 2,000 years old, 51 metres tall, 14 metres in circumference. A 10-minute walk from the road in Waipoua Forest. The kauri were almost entirely logged in the 19th century; this forest is one of the last remnants. Simply enormous in the way that very old living things are." },
      { label: "Bay of Islands sailing", text: "144 islands, protected water, consistent winds. Day trips from Paihia or Russell reach the Hole in the Rock (a natural arch you sail through), the dolphin feeding grounds, and outer islands with no road access. The Russell to Paihia ferry is the cheapest boat trip in the Bay and worth taking for the water alone." },
      { label: "Waitangi Treaty Grounds", text: "Where the Treaty of Waitangi was signed on February 6, 1840 — still contested, still central to New Zealand's identity. The Treaty House, the Maori meeting house, the waka taua (war canoe) that took three years to build. The guided tour is one of the most honest accounts of colonial history offered anywhere." },
      { label: "Cape Reinga", text: "The northern tip of New Zealand — the lighthouse looks over the meeting of the Tasman Sea and Pacific, two seas of different colours visibly colliding. In Maori tradition this is where the spirits of the dead slide down the roots of the ancient pohutukawa tree into the ocean." },
      { label: "Ninety Mile Beach", text: "A 90km stretch of hard flat beach on the west coast that functions as a road — legally. The Te Paki Stream mouth at the northern end has enormous sand dunes. No facilities, no crowds, extraordinary light in the late afternoon." },
    ],
    eat: [
      { name: "The Duke of Marlborough (Russell)", desc: "New Zealand's oldest licensed hotel on the Russell waterfront, operating since 1840. Fresh Bay of Islands snapper, green-lipped mussels, local oysters. Eat on the deck watching the water." },
      { name: "Alongside (Paihia)", desc: "The best breakfast in the Bay of Islands — local eggs, smoked fish, good coffee. The deck is directly over the water. Arrive early for a waterfront table." },
      { name: "Manuka Restaurant (Kerikeri)", desc: "The most ambitious kitchen in Northland — local Kerikeri citrus, Bay of Islands seafood, New Zealand beef. The region's serious dining option, 20 minutes from Paihia." },
    ],
    stay: [
      { name: "Lodge at Kauri Cliffs (Matauri Bay)", tier: "High end", desc: "18-hole golf course, private beach, and views over Matauri Bay and the Cavalli Islands. One of the finest lodges in New Zealand." },
      { name: "Paihia Beach Resort", tier: "Mid range", desc: "Right on the Paihia waterfront — the bay and islands from the room, walking distance to the ferry and boat tours. The most practical mid-range base in the Bay of Islands." },
      { name: "Omapere Tourist Hotel (Hokianga)", tier: "Good value", desc: "An old pub hotel near the Waipoua Forest on the Hokianga Harbour. Basic rooms, a bar that feels genuinely local, and the kauri forest 20 minutes away." },
    ],
    logistics: [
      { q: "When to go", a: "Year-round — Northland's subtropical climate means mild winters and warm summers. April-June and September-November are the sweet spots: warm enough for swimming, quiet enough to have beaches to yourself. The pohutukawa trees bloom crimson in December and January — New Zealand's Christmas tree." },
      { q: "Getting there", a: "Drive from Auckland: 3 hours to Paihia, 4.5 hours to the Waipoua Forest. Or fly to Kerikeri Airport (KKE, 45 minutes from Auckland on Air New Zealand). A car is essential — Northland has no meaningful public transport beyond tourist shuttles." },
      { q: "Cape Reinga logistics", a: "The Cape Reinga drive from Paihia is 200km each way — a full day. Tour buses drive Ninety Mile Beach on the way up and the road on the way down. Driving Ninety Mile Beach yourself requires a 4WD and tide awareness — tour buses do this confidently, standard rental cars less so." },
      { q: "How long", a: "Three nights minimum. Night one Paihia (Bay of Islands sailing day). Night two Omapere or Kauri Cliffs (Waipoua Forest and Tane Mahuta). Night three Paihia or Kerikeri (Cape Reinga day trip). Return to Auckland." },
    ],
  },
  {
    name: "Wellington", country: "newzealand", tag: "Museums · Coffee · Weta Workshop",
    hook: "The most underrated capital city in the Southern Hemisphere. The food scene is better than Sydney's. Nobody outside New Zealand talks about it.",
    img: "https://images.unsplash.com/photo-1589802829985-817e51171b92?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=4; if(a[3]?.includes("local")||a[3]?.includes("balanced")) s+=3; if(a[5]?.includes("cities")||a[5]?.includes("coast")) s+=4; if(a[6]?.includes("wander")||a[6]?.includes("eat")||a[6]?.includes("absorb")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; return s; },
    intro: "Wellington sits at the southern tip of the North Island, crammed between steep green hills and a harbour that faces the Cook Strait. 215,000 people with more cafes per capita than New York, Te Papa (the best national museum in the Southern Hemisphere), a craft beer and natural wine scene that punches far above its size, and Weta Workshop — Peter Jackson's effects company that built Middle-earth — running studio tours in Miramar. The cable car up to the Botanic Garden is one of the great five-minute urban experiences in the world.",
    highlights: [
      { label: "Te Papa Tongarewa", text: "New Zealand's national museum on the Wellington waterfront — one of the best in the world. The Maori taonga (treasure) collection is extraordinary. The giant squid — 4.2 metres, caught in the Ross Sea — is real. The exhibitions on New Zealand's geological history are the best science communication in any museum in the region. Free entry." },
      { label: "Weta Workshop tour", text: "Peter Jackson's practical effects studio in Miramar. The One Ring was forged here. The Orc costumes made here. The Helm's Deep miniatures built here at 1:72 scale. Working artists still on the floor. The guided tour is the most specific film nerd experience in the world." },
      { label: "Cuba Street", text: "Wellington's bohemian main street — the 1969 bucket fountain (kinetic, still running), independent bookshops, the best natural wine bars in New Zealand, vintage clothing. The kind of Saturday morning energy that only exists in compact cities where everyone knows each other." },
      { label: "Mount Victoria lookout", text: "A 15-minute walk from the city center — 196m summit looking over the harbour, the city, the Cook Strait, and the South Island mountains on a clear day. Lord of the Rings was filmed on this hill. Go at sunset." },
    ],
    eat: [
      { name: "Ortega Fish Shack (Te Aro)", desc: "The best seafood restaurant in New Zealand — a small room on a back street, whatever came off the boat that morning, natural wines from a serious list. Book weeks ahead. The kingfish crudo is the permanent fixture." },
      { name: "Loretta (Cuba Street)", desc: "The all-day cafe and restaurant that has defined Wellington's food scene for a decade. The brunch is the benchmark. Weekly changing dinner menu, natural wines." },
      { name: "Seashore Cabaret (Oriental Parade)", desc: "A natural wine bar and kitchen on the waterfront. The harbour in every window, the small plates among the most inventive cooking in Wellington." },
    ],
    stay: [
      { name: "QT Wellington", tier: "High end", desc: "A converted 1930s department store — art-filled rooms, rooftop bar with harbour views, a restaurant that takes New Zealand produce seriously." },
      { name: "Bolton Hotel", tier: "Mid range", desc: "Apartment-style suites in the city center — kitchens, proper sized rooms, Te Papa and Cuba Street within 15 minutes on foot. The most practical mid-range stay." },
      { name: "CityLife Wellington", tier: "Good value", desc: "Well-designed apartments near Courtenay Place. Self-catering for market meals. The best value extended-stay option in the city." },
    ],
    logistics: [
      { q: "When to go", a: "The Wellington Festival of the Arts (March, even years) and the Fringe Festival (February-March) are the cultural peaks. Summer (December-March) is warmest. Winter is genuinely cold and very windy but the museum and restaurant culture makes it work year-round." },
      { q: "Getting there", a: "Fly into Wellington Airport (WLG) — 30 minutes from the city center. Air New Zealand and Jetstar from Auckland (1 hour) and Australian cities. Or the Interislander ferry from Picton — 3.5 hours through the Marlborough Sounds, one of the great ferry journeys in the Southern Hemisphere." },
      { q: "How long", a: "Two to three nights. Day one: Te Papa, Cuba Street, Ortega dinner. Day two: Weta Workshop morning, Mount Victoria sunset. Day three: Zealandia wildlife sanctuary, Interislander ferry to Picton for the South Island road trip." },
    ],
  },
  {
    name: "Coromandel & East Coast", country: "newzealand", tag: "Hot Water Beach · Cathedral Cove · Pacific",
    hook: "Dig your own hot spring on a public beach. It is exactly as good as it sounds.",
    img: "https://images.unsplash.com/photo-1507699622108-4be3abd695ad?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=3; if(a[3]?.includes("balanced")||a[3]?.includes("explorer")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("nothing")||a[6]?.includes("wander")||a[6]?.includes("spontaneous")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=3; return s; },
    intro: "The Coromandel Peninsula is two hours east of Auckland and almost entirely unknown to international travelers — a forested peninsula of white sand beaches and geothermal springs that has attracted artists and people leaving cities behind for 50 years. Hot Water Beach is a thermal spring that surfaces under the sand at low tide — you dig a hole, the water fills it at 64 degrees, you adjust the walls until it is the right temperature, and you sit in your own private hot pool watching the Pacific. Cathedral Cove, a 45-minute walk through pohutukawa forest, is a natural rock arch connecting two white sand bays. The drive around the peninsula — single lane coast road, sea on one side, forest on the other — is one of the finest in the North Island.",
    highlights: [
      { label: "Hot Water Beach", text: "Rent a spade from the cafe (NZ$5). Walk to the spring zone at low tide. Dig until hot water fills the hole. Adjust the depth until the temperature is right. Sit in your own hot pool with the Pacific in front of you. Peak times have 400 people simultaneously digging. Go at the first low tide of the day — 6am if the tides cooperate." },
      { label: "Cathedral Cove", text: "A natural rock arch connecting two beaches, accessible by a 45-minute coastal walk through pohutukawa forest or by boat from Hahei. The cove appears suddenly at the bottom of the last flight of steps. No road access, no facilities. Arrive early or take the last boat of the afternoon." },
      { label: "Coromandel Peninsula drive", text: "State Highway 25 on the east coast takes four hours without stops. The highlights: Whangapoua, the lookout above Kuaotunu, Otama Beach (the most beautiful and least visited beach on the peninsula), and the descent into Whitianga. The driving is the destination." },
      { label: "Driving Creek Railway", text: "A narrow gauge railway built by potter Barry Brickell on his own property above Coromandel Town — climbing through regenerating native bush to the Eyefull Tower. Brickell spent 30 years building it by hand. A genuinely eccentric New Zealand institution." },
    ],
    eat: [
      { name: "The Pepper Tree (Coromandel Town)", desc: "The best restaurant on the peninsula — local seafood, seasonal vegetables, New Zealand wine. The whitebait fritters when whitebait is running (September-November) are extraordinary." },
      { name: "Eggsentric Cafe (Hot Water Beach)", desc: "The cafe that rents the spades and provides the best breakfast on the Coromandel — egg dishes, excellent coffee, the deck in the morning sun. Go before the hot spring crowd arrives." },
    ],
    stay: [
      { name: "The Church Accommodation (Coromandel Town)", tier: "Mid range", desc: "A converted 1923 church on the hill above town — four rooms, stained glass windows intact, a garden with harbour views. The most characterful accommodation on the peninsula." },
      { name: "Hahei Holiday Resort", tier: "Good value", desc: "Five minutes from Cathedral Cove. Holiday park accommodation — cabins and powered sites. The most practical base for the eastern Coromandel. Book months ahead in January." },
      { name: "Hot Water Beach TOP 10", tier: "Good value", desc: "Directly above Hot Water Beach — the first accommodation of the day at the thermal spring. Cabins, glamping tents. The view of the Pacific from the upper sites is the reason to come." },
    ],
    logistics: [
      { q: "When to go", a: "December-March for warm swimming. Hot Water Beach and Cathedral Cove are very crowded at Christmas and New Year — go late January or February. The whitebait season (September-November) is worth timing if you want the fritters. Autumn (March-May) has the best light and far fewer people." },
      { q: "Getting there", a: "Drive from Auckland: 2.5 hours to Thames (the gateway), then 1 hour to Hahei and Hot Water Beach. No meaningful public transport. A car is essential. The drive itself through the Hauraki Plains and into the Coromandel hills is part of the experience." },
      { q: "Tides", a: "Hot Water Beach only works at low tide — the thermal spring is covered at high tide. Check the tide tables before driving (the local council website has a dedicated Hot Water Beach tide calculator). Aim for two hours either side of low tide. Cathedral Cove is accessible at all tides but the beach is smaller at high tide." },
      { q: "How long", a: "Two nights minimum — one night Coromandel Town (Driving Creek Railway, the west coast road), one night Hahei (Cathedral Cove walk, Hot Water Beach at dawn low tide). Three nights to drive the full peninsula circuit." },
    ],
  },
];

// ─── OMAN REGIONS ─────────────────────────────────────────────────────────────
const omanRegions = [
  {
    name: "Muscat", country: "oman", tag: "Souqs · Grand Mosque · Mutrah",
    hook: "A Gulf capital that chose not to become Dubai. The old souq still works. The hospitality is genuine.",
    img: "https://images.unsplash.com/photo-1578895101408-1a36b834405b?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[5]?.includes("cities")||a[5]?.includes("coast")) s+=3; if(a[6]?.includes("wander")||a[6]?.includes("absorb")) s+=4; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; return s; },
    intro: "Muscat is the Gulf capital that chose not to become Dubai — no skyscrapers over seven stories, white paint and traditional architecture required on all new construction. The Sultan Qaboos Grand Mosque is one of the most beautiful in the world — the main prayer hall carpet was woven by 600 women over four years and is the second largest handwoven carpet on earth. The Mutrah Souq is one of the oldest working markets in the Arabian Peninsula — frankincense, silver Khanjar daggers, halwa, traders three generations deep. The Corniche at sunset, sea on one side and white buildings on the other, is the defining image of Oman.",
    highlights: [
      { label: "Sultan Qaboos Grand Mosque", text: "The main prayer hall carpet — 4,343 square metres, woven by 600 women in Iran over four years — is the second largest handwoven carpet in the world. The chandelier weighs 8 tonnes. Non-Muslims admitted Saturday through Thursday, 8am-11am. Dress modestly — abayas available to borrow at the entrance." },
      { label: "Mutrah Souq", text: "One of the oldest markets in the Arabian Peninsula — a covered labyrinth of stalls selling frankincense, silver Khanjar daggers, hand-embroidered textiles, halwa. The silver Bedouin jewelry section is the best in Oman. Bargain gently — the gap between opening and final price is smaller than you expect." },
      { label: "Mutrah Corniche at sunset", text: "The waterfront promenade along the old harbor — fishing boats moored beside the fort, the Al Jalali and Al Mirani forts on the headlands. The light at sunset turns everything gold. Walk from the souq entrance to the fish market and back." },
      { label: "Nizwa day trip", text: "An hour inland — the ancient capital of Oman. The Nizwa Fort and the adjacent date souq are the anchors. Friday morning is the weekly goat market — one of the most authentic traditional markets still operating in the Gulf." },
    ],
    eat: [
      { name: "Ubhar (Qurum)", desc: "The best Omani restaurant in Muscat. Shuwa (slow-cooked pit lamb), mashkak spiced skewers, Omani halwa. Traditional dishes given a contemporary treatment. The most complete introduction to Omani food culture." },
      { name: "Bait Al Luban (Mutrah)", desc: "A converted traditional house overlooking the Corniche. The mezze are the reason: hummus, fattoush, Omani khubz bread straight from the oven. The most atmospheric lunch in Muscat." },
      { name: "Al Angham (Royal Opera House)", desc: "Inside the Royal Opera House complex — Omani cuisine in a grand setting. Try the qahwa (cardamom and rosewater coffee) with dates. The long lunch is the local tradition here." },
    ],
    stay: [
      { name: "Chedi Muscat", tier: "High end", desc: "Long pools reflecting the surrounding mountains, a frankincense and rose spa, the best restaurant in the city. The most design-focused hotel in Oman." },
      { name: "Al Bustan Palace (Ritz-Carlton)", tier: "High end", desc: "Built for a Gulf summit in 1985 — the atrium lobby is nine stories high, the beach is private. The most historically significant luxury hotel in Oman." },
      { name: "Mutrah Hotel", tier: "Mid range", desc: "Directly on the Mutrah Corniche — steps from the souq and the waterfront. Simple rooms, extraordinary location. The most atmospheric mid-range stay in Muscat." },
      { name: "Muscat Hills Resort", tier: "Good value", desc: "Apartments in the hills above Muscat with Gulf of Oman views. Self-catering, quiet, significantly cheaper than city center hotels. 15 minutes to Mutrah by taxi." },
    ],
    logistics: [
      { q: "When to go", a: "October-March only. Temperatures 20-30C, sea warm, clear skies. Avoid May-August entirely — temperatures reach 45-50C. Ramadan (dates vary) is a unique experience — the city slows during daylight, the night markets and Iftar meals are extraordinary — but restaurants close during the day." },
      { q: "Getting there", a: "Fly into Muscat International (MCT) — Oman Air from London (7hrs), Dubai (1hr), Doha (1.5hrs). Taxi or Uber from airport to Mutrah (around 8 OMR). Car rental essential for anywhere beyond Muscat." },
      { q: "Dress and culture", a: "Oman is the most tolerant country in the Gulf for visitors — alcohol is available in licensed hotel bars and restaurants. Modest dress required for mosques and souqs. Women do not need to cover hair outside religious sites. Accepting coffee and dates when offered is good manners." },
      { q: "How long", a: "Two nights in Muscat before heading to the desert and wadis. Grand Mosque morning, Mutrah Souq afternoon and evening. Day two: Nizwa day trip. Muscat works as both gateway and destination." },
    ],
  },
  {
    name: "Wahiba Sands", country: "oman", tag: "Desert · Bedouin · Dunes at Dawn",
    hook: "The dunes are 200 metres high. The silence at night is absolute. The Bedouin camps have been here for 3,000 years.",
    img: "https://images.unsplash.com/photo-1509316785289-025f5b846b35?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("adventure")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=4; if(a[5]?.includes("desert")) s+=6; if(a[6]?.includes("nothing")||a[6]?.includes("explore")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=4; return s; },
    intro: "The Wahiba Sands is a 10,000 square kilometre sea of dunes in eastern Oman — some reaching 200 metres, the sand shading from pale gold at the edges to deep orange at the centre. The Bedouin who have lived here for millennia are still here. Several families now operate desert camps for visitors — actual family compounds where you sleep in traditional barastis, eat Omani food cooked on a fire, and wake before dawn to climb the dunes for sunrise. The desert sky at night has no light pollution for 200km in any direction — the Milky Way is visible to the naked eye and it is the most extraordinary thing about the Wahiba.",
    highlights: [
      { label: "Dunes at dawn", text: "Wake at 4:30am. Walk 20 minutes to the nearest high dune. Climb the crest — the sand is firm at dawn before the heat softens it. Watch the light change from grey to gold to orange, the shadows making the ridges three-dimensional. The first camel caravan of the day appears from nowhere. This is why you came." },
      { label: "Bedouin camp overnight", text: "The Bedouin families who operate camps in the Wahiba provide the most authentic desert experience in the Arabian Peninsula. Dinner is Omani — slow-cooked lamb, rice, flatbread, dates, qahwa. The beds are mattresses under a barasti or in a simple tent. Sleeping in silence with the stars overhead is disorienting in the best way." },
      { label: "Camel rides", text: "The Bedouin camels that work the Wahiba are working animals — used for transport, racing, milk. A morning ride into the dunes with a Bedouin guide covers terrain no vehicle can reach and forces a different relationship with the landscape." },
      { label: "Desert sky", text: "The Wahiba has almost no light pollution for 200km in every direction. The Milky Way is visible as a solid band. The constellations of the southern sky that most travelers have never seen are overhead. Lie on the dune crest at 9pm and look up for 20 minutes without moving." },
    ],
    eat: [
      { name: "Camp dinner", desc: "The meal at any Bedouin camp is the reason to eat here — shuwa, rice cooked with dried limes and spice, Omani flatbread, fresh dates from the family's grove, qahwa. Eating under the stars in the desert is the best meal in the Wahiba." },
      { name: "Roadside fish restaurants (Ibra)", desc: "The town of Ibra on the desert edge has good cheap fish restaurants — fresh hammour and kingfish from Sur on the coast, grilled or fried with rice. OMR 2-4 for a full meal." },
    ],
    stay: [
      { name: "Desert Nights Camp", tier: "High end", desc: "The most comfortable camp in the Wahiba — permanent tented suites with proper beds, an infinity pool facing the dunes, a Bedouin-trained chef. The polar opposite of roughing it, with the same extraordinary landscape." },
      { name: "1000 Nights Camp", tier: "Mid range", desc: "A mid-range Bedouin camp with traditional barasti accommodation, communal Omani meals, and guided dune walks. Run by an Omani family that has been in the desert for generations." },
      { name: "Sama Al Wasil Desert Camp", tier: "Good value", desc: "A simple family camp at the edge of the Wahiba — basic tents, shared facilities, Omani meals cooked by the family. The cheapest way to sleep in the Wahiba and still wake to the same dunes at dawn." },
    ],
    logistics: [
      { q: "When to go", a: "October-March only. The Wahiba in summer is 50C and uninhabitable. The best months are November-February when nights are cool (sometimes cold) and days are warm not hot. January occasionally gets rain — the desert blooms briefly and the dunes change colour." },
      { q: "Getting there", a: "A 4WD is mandatory — you cannot enter the dunes in a 2WD vehicle. Rent in Muscat (2.5 hours drive to the desert edge). The paved road ends at Al Mintirib; your camp will send a guide to lead you in. Do not attempt to drive the dunes alone." },
      { q: "Combining with Wadi Shab", a: "The Wahiba and Wadi Shab are an easy combination — Wadi Shab is 1.5 hours from the desert edge toward the coast. Do the desert first (overnight), then drive to Wadi Shab for the gorge swim." },
      { q: "What to bring", a: "Sunscreen and hat for daytime. A warm layer for evenings — desert nights drop quickly after sunset. A headtorch for the predawn dune walk. Sand gets into everything — keep your phone in a zip-lock bag." },
    ],
  },
  {
    name: "Wadi Shab & Wadi Nakhr", country: "oman", tag: "Gorges · Turquoise Pools · Grand Canyon of Arabia",
    hook: "Swim through a canyon to reach a waterfall hidden inside a cave. This is a real activity you can do tomorrow.",
    img: "https://images.unsplash.com/photo-1542401886-65d6c61db217?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=4; if(a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=3; if(a[6]?.includes("physical")||a[6]?.includes("explore")) s+=5; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=3; return s; },
    intro: "Oman has more wadis than any other country in the Arabian Peninsula. Wadi Shab is the most spectacular: a 2-hour walk along the canyon floor brings you to a turquoise pool, then a swim through a narrow canyon to a waterfall hidden inside a cave. The water is cold, clean, and the exact turquoise that photographs make it look. Wadi Nakhr, in the Hajar Mountains near Nizwa, is called the Grand Canyon of Arabia — a 1,000 metre deep gorge that appears without warning at the edge of the Saiq Plateau, ancient villages clinging to the opposite wall. The two wadis together form the best two-day combination in Oman.",
    highlights: [
      { label: "Wadi Shab cave swim", text: "Cross the river by small boat (OMR 0.5), walk 2 hours along the wadi floor, reach the pools. Swim across the first pool. A narrow opening in the canyon wall leads to a second pool and then a cave with a waterfall inside — the interior lit by the gap above. One of the most unusual swim experiences in the world." },
      { label: "Wadi Nakhr viewpoint", text: "Drive to the village of Ghul and walk to the canyon edge — 1,000 metres straight down. The villages on the opposite wall were accessible only by rope until the 1980s. Ancient falaj irrigation channels cut into the cliff face are still carrying water from the mountain springs." },
      { label: "Wadi Tiwi", text: "Adjacent to Wadi Shab and less visited — a longer canyon with multiple swimming pools, date palm groves inside the gorge, and villages with no road connection. The best half-day extension." },
      { label: "Ras al Jinz turtle reserve", text: "The green turtle nesting site near Sur (30 minutes from Wadi Shab) operates nightly guided tours when nesting turtles come ashore and dawn tours when hatchlings emerge. Watching a 150kg turtle lay eggs by moonlight is extraordinary." },
    ],
    eat: [
      { name: "Tiwi village restaurants", desc: "Simple restaurants at the wadi entrance — grilled fish, Omani flatbread, lime juice, dates. The fish comes from the coast 10 minutes away. Eat before the walk." },
      { name: "Sur waterfront (Al Nashama)", desc: "The best restaurant in Sur — fresh hammour, lobster when available, kingfish. The view of the old dhow harbor from the waterfront tables." },
    ],
    stay: [
      { name: "Al Sharqiyah Sands Hotel (Ibra)", tier: "Mid range", desc: "A small hotel at the crossroads between the Wahiba Sands and Wadi Shab — the most practical base for combining both. Simple rooms, Omani hospitality." },
      { name: "Camping in Wadi Tiwi", tier: "Good value", desc: "With permission from local families, camping in the wadi itself — the sound of the falaj through the night, stars above the canyon walls, no other tourists. Bring everything in and out." },
    ],
    logistics: [
      { q: "When to go", a: "October-April for wadi swimming. Never attempt wadis after rainfall — flash floods fill the canyon with no warning and are extremely dangerous. Check the forecast the evening before. Best months are November-March when pools are fullest." },
      { q: "Wadi Shab logistics", a: "Drive from Muscat: 2.5 hours to the Wadi Shab turnoff. Park at the boat crossing. Cross by boat (OMR 0.5). Walk 2 hours to the swim. A full day from Muscat — leave by 7am. Bring 2 litres of water, a dry bag for your phone, sandals that can get wet." },
      { q: "Wadi Nakhr logistics", a: "Drive from Muscat: 2 hours to Nizwa, then 45 minutes to Ghul village. The viewpoint is a 15-minute walk from the village. A 4WD is recommended for the Saiq Plateau road above." },
    ],
  },
  {
    name: "Musandam Peninsula", country: "oman", tag: "Fjords · Dhow · Telegraph Island",
    hook: "The Norway of Arabia. Technically an exclave. You need a new stamp in your passport to get there from Oman.",
    img: "https://images.unsplash.com/photo-1544551763-46a013bb70d5?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")) s+=5; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=4; if(a[5]?.includes("mountains")||a[5]?.includes("coast")) s+=4; if(a[6]?.includes("nothing")||a[6]?.includes("explore")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=5; if(a[8]?.includes("article")||a[8]?.includes("none")) s+=4; return s; },
    intro: "The Musandam Peninsula is a shard of Oman separated from the rest of the country by the UAE — a geographical exclave at the tip of the Arabian Peninsula where the Strait of Hormuz narrows to 33km. The landscape is the Norway of Arabia — the Hajar Mountains drop directly into the Khor ash Sham fjord, the water is so clear you can see 15 metres down, and the villages on the water's edge have no road connection. Telegraph Island, in the middle of the khor, was the British cable station for the Indo-European telegraph line in the 1860s — isolated postings here are said to have given English the phrase going round the bend. The Musandam is the least visited part of Oman and, arguably, the most extraordinary.",
    highlights: [
      { label: "Khor ash Sham dhow trip", text: "The full-day dhow tour of the main fjord — Khasab past the villages of Qanah and Kumzar, around Telegraph Island, snorkeling over reef, lunch on the boat. The mountain walls drop vertically into water with 70% visibility. Dolphins follow the boat through the Strait. The most dramatic boat journey in Arabia." },
      { label: "Telegraph Island", text: "A tiny island in the middle of the khor where the British built a cable relay station in 1864. The ruins are still there. The snorkeling around the island is the best in the Musandam — coral intact, fish dense." },
      { label: "Jebel Harim", text: "The highest peak in the Musandam at 2,087m. A road climbs to near the summit through villages where women still wear the traditional beaked leather mask of the Shihuh tribe. The views cover Iran, the UAE, and the Strait of Hormuz simultaneously. Marine fossils at the summit — this was once an ocean floor." },
      { label: "Kumzar village", text: "The most remote village in Oman, accessible only by boat. The 3,500 residents speak Kumzari — a language that mixes Farsi, Arabic, Portuguese, English, and Hindi, the linguistic legacy of every power that controlled the Strait of Hormuz." },
    ],
    eat: [
      { name: "Dhow lunch", desc: "The dhow operators provide a lunch on the boat — fresh fish caught that morning, rice, Omani flatbread, fruit, cold water. The setting makes it the best meal in Musandam." },
      { name: "Khasab town restaurants", desc: "Simple Omani restaurants around the Khasab center — grilled fish, harees, qahwa and dates. Honest food and the freshest fish in the Musandam." },
    ],
    stay: [
      { name: "Six Senses Zighy Bay", tier: "High end", desc: "A luxury resort in a secluded bay on the eastern Musandam coast — accessible only by boat, paraglider from the cliff above, or 4WD on a mountain track. One of the most isolated luxury resorts in the world." },
      { name: "Khasab Hotel", tier: "Mid range", desc: "The practical base for dhow trips — simple rooms, staff who book the boat tours, 10 minutes from the Khasab waterfront." },
      { name: "Day trip from Dubai", tier: "Good value", desc: "Khasab is 2 hours from Dubai by car. A day trip covers the dhow tour. Get the Oman visa on arrival at the Tibat border (USD 20)." },
    ],
    logistics: [
      { q: "Getting there", a: "The Musandam is separated from Oman by UAE territory. From Muscat: fly to Khasab Airport (50 minutes, Oman Air) or drive via the UAE (5 hours, two border crossings). From Dubai: drive via Ras al Khaimah to the Tibat crossing (2 hours). Bring your passport — a new stamp each way." },
      { q: "Dhow tours", a: "Book through the Khasab hotel or at the Khasab waterfront. Full day (8 hours): OMR 25-35 per person. Half day (4 hours): OMR 15-20. Private dhow: OMR 100-150 per boat per day. The full day is the right choice — Telegraph Island and the inner fjord are only reached on the full route." },
      { q: "When to go", a: "October-April. Summer is 40-45C with extreme Gulf humidity. Best months November-March when the sea is glassy and underwater visibility is maximum." },
    ],
  },
  {
    name: "Jebel Akhdar", country: "oman", tag: "Green Mountain · Rose Water · Ancient Villages",
    hook: "A mountain plateau at 2,000 metres in the middle of the Arabian desert, covered in terraced orchards producing roses, pomegranates, and apricots.",
    img: "https://images.unsplash.com/photo-1469521669194-babb45599def?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("culture")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=4; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=3; if(a[5]?.includes("mountains")||a[5]?.includes("countryside")) s+=5; if(a[6]?.includes("wander")||a[6]?.includes("absorb")||a[6]?.includes("nothing")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; return s; },
    intro: "Jebel Akhdar — the Green Mountain — is a plateau in the Hajar Mountains at 2,000 metres elevation where the altitude creates a microclimate completely unlike anything in Arabia. The plateau is covered in ancient terraced orchards: Damask roses harvested in April for rose water and rose oil, pomegranates, apricots, peaches. The ancient falaj irrigation system — channels cut into the mountain to carry water from springs — has operated for 3,000 years and is a UNESCO World Heritage site. The villages on the plateau edge cling to the rim of canyons with views that drop 1,000 metres. Almost no tourists, almost no infrastructure, and one of the most surprising places in the Arabian Peninsula.",
    highlights: [
      { label: "Wadi Bani Habib", text: "An abandoned village on the plateau edge — stone houses built into the cliff, rooftops now collapsed, the falaj still running past empty rooms. The villagers moved to Nizwa in the 1970s when the Sultan built the road. The terrace orchards are still tended by descendants who return each season." },
      { label: "Rose harvest (April)", text: "The Damask roses bloom for three weeks — families harvest before dawn, the petals must be picked before the heat opens them and releases the scent. Rose water is distilled in simple copper alembics in every house. The plateau smells of rose from first light until mid-morning. April only." },
      { label: "Diana's Point viewpoint", text: "Named after Princess Diana's 1986 visit — a viewpoint on the canyon rim at the edge of the Saiq Plateau. The Wadi Bani Awf below is 1,200 metres down. Arrive at dawn when the canyon fills with mist." },
      { label: "Village walks", text: "The plateau villages are connected by a ridge walk (3-4 hours, moderate) through orchards, along falaj channels, and around the canyon rim. The villagers have lived here for generations and hospitality is unforced — dates and qahwa offered freely." },
    ],
    eat: [
      { name: "Anantara Al Jabal Al Akhdar restaurant", desc: "The resort restaurant at the canyon rim — the terrace overhangs a 1,000 metre drop. Plateau produce: pomegranate, dried apricot, rose water in the desserts. The best setting for a meal in Oman." },
      { name: "Village guesthouses", desc: "Several plateau villages have informal guesthouses where the family serves Omani meals — shuwa on Fridays, harees in the evenings. Ask at your hotel for introductions." },
    ],
    stay: [
      { name: "Anantara Al Jabal Al Akhdar", tier: "High end", desc: "A resort built on the edge of a 1,000 metre canyon — the infinity pool appears to drop directly into the gorge. The most dramatically sited hotel in Oman. 4WD access only." },
      { name: "Sama Chalets Al Jabal Al Akhdar", tier: "Mid range", desc: "Simple chalets on the plateau with mountain views and access to the village walks. The most practical mid-range stay on the Green Mountain." },
      { name: "Rose Village Guesthouses", tier: "Good value", desc: "Family-run guesthouses in the plateau villages — basic rooms, home-cooked Omani meals, a window into mountain life no hotel provides." },
    ],
    logistics: [
      { q: "When to go", a: "October-March for cool temperatures and clear views. April specifically for the rose harvest. The summer months (June-August) are actually pleasant at 2,000m elevation (25-30C) when the rest of Oman is 45C — the mountain is a refuge." },
      { q: "Getting there", a: "Drive from Muscat: 2 hours to Nizwa, then 1.5 hours up the mountain road. A 4WD is mandatory — there is a checkpoint at the base that turns back 2WD vehicles. Rent a 4WD in Muscat." },
      { q: "How long", a: "One night on the plateau minimum — arrive by 3pm for the Diana's Point sunset, walk to Wadi Bani Habib in the morning, leave by noon. Two nights allows the full village walk circuit." },
    ],
  },
];

// ─── AUSTRALIA REGIONS ────────────────────────────────────────────────────────
const australiaRegions = [
  {
    name: "Uluru & The Red Centre", country: "australia", tag: "Sacred Rock · Desert · 60,000 Years",
    hook: "The oldest sacred site continuously inhabited on earth. The rock changes colour 27 times between sunrise and dark.",
    img: "https://images.unsplash.com/photo-1529108190281-9a4f620bc2d8?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("culture")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("desert")) s+=6; if(a[6]?.includes("nothing")||a[6]?.includes("absorb")) s+=4; if(a[8]?.includes("none")||a[8]?.includes("feel")) s+=4; return s; },
    intro: "Uluru is 348 metres high, 9.4 kilometres in circumference, and extends 2.5 kilometres underground. It is made of arkosic sandstone that turns from ochre to burning red to deep purple as the light moves across it. The Anangu people have lived here for at least 60,000 years and consider it one of the most sacred places on earth. The climbing of Uluru was closed permanently in 2019 at the Anangu's request. The base walk (10.6km) takes you around the entire rock past sacred sites, ancient cave paintings, and geology 550 million years old. Kata Tjuta — the 36 domed formations 40km west — is older and, many visitors say, more powerful. The Valley of the Winds walk through the domes at the midpoint, enclosed by rock on all sides, produces a silence that is absolute.",
    highlights: [
      { label: "Uluru at sunrise", text: "The viewing area fills from 45 minutes before sunrise. In the dark, the rock is a black silhouette. The first light turns the top edges red. The colour spreads down. By the time the sun is fully up, Uluru is burning orange. It continues to change for another hour. It is exactly as extraordinary as the photographs and completely different in person." },
      { label: "Kata Tjuta — Valley of the Winds", text: "The 36 domes cover a larger area than Uluru and receive fewer visitors. The Valley of the Winds walk (7.4km, 4 hours) enters between the domes, climbs to the Karingana lookout, and descends through a narrow gorge where the wind is audible from 200 metres away. More dramatic than Uluru on the right day." },
      { label: "Uluru base walk", text: "The 10.6km walk around the entire rock takes 3-4 hours. The south face is the tourist face. The north and west sides see almost nobody — ancient paintings, watering holes, caves. The Mutitjulu Waterhole on the southwest corner has sustained the Anangu for 60,000 years." },
      { label: "Anangu cultural experience", text: "The Anangu-run Dot Painting workshops, guided cultural tours, and the Uluru-Kata Tjuta Cultural Centre explain tjukurpa — the Anangu law and knowledge system — through the rock's features. Understanding the rock before walking around it changes everything about the walk." },
      { label: "Desert sky at night", text: "The Red Centre has almost no light pollution in any direction. The Milky Way is a solid band visible to the naked eye. The Sounds of Silence dinner — white tablecloths in the desert, a fine dining meal under the stars, an astronomer with a telescope — is a tourist product executed with genuine quality." },
    ],
    eat: [
      { name: "Sounds of Silence (Voyages)", desc: "Dinner under the stars in the desert — tables set in the sand, three courses using Australian bush ingredients, a sommelier, a resident astronomer with a telescope. Book through Ayers Rock Resort months ahead." },
      { name: "Tali Wiru (Voyages)", desc: "Private dining for four on a sand dune at sunset — degustation menu with native Australian ingredients, a sommelier, the dune to yourselves. The most exclusive outdoor dining experience in Australia." },
      { name: "Kulata Academy Cafe (Cultural Centre)", desc: "A cafe inside the cultural centre run by the Anangu community — bush tomato soup, quandong jam on damper bread. The most direct way to eat something specifically Anangu." },
    ],
    stay: [
      { name: "Longitude 131 (Voyages)", tier: "High end", desc: "15 tented pavilions on a sand dune facing Uluru — the rock fills the window at sunset. The most design-focused accommodation at the resort and the most direct relationship between your bed and the landscape." },
      { name: "Sails in the Desert (Voyages)", tier: "Mid range", desc: "The largest hotel at Ayers Rock Resort — the best pool in the desert, well-maintained rooms, access to all Voyages facilities and shuttle buses." },
      { name: "Ayers Rock Resort Campground", tier: "Good value", desc: "The only budget accommodation within the resort — powered and unpowered sites, access to the resort pool, shuttle buses to all sunrise and sunset viewing areas." },
    ],
    logistics: [
      { q: "When to go", a: "May-September — temperatures 15-25C, clear skies. October and April are shoulder months: warm but manageable. Never visit November-March: temperatures reach 47C in January, the flies are extreme, the ground is too hot for the base walk." },
      { q: "Getting there", a: "Fly into Ayers Rock Airport (AYQ) from Sydney (3.5hrs), Melbourne (3hrs), or Alice Springs (30 min). The airport is 5km from the resort. Or fly to Alice Springs and drive the 450km to Uluru — 5 extraordinary hours through the Red Centre." },
      { q: "The park", a: "Entry is AUD 38/person for 3 days covering both Uluru and Kata Tjuta. Do not climb Uluru. Do not remove rocks or sand. Photography of certain sacred sites is prohibited — signs are posted." },
      { q: "How long", a: "Two nights minimum. Day one: Cultural Centre, Kata Tjuta Valley of the Winds. Day two: Uluru sunrise, base walk, Field of Light evening. Day three: Kata Tjuta sunrise, depart." },
    ],
  },
  {
    name: "Queensland & Great Barrier Reef", country: "australia", tag: "Reef · Daintree · Coral Sea",
    hook: "The oldest tropical rainforest on earth meets the world's largest coral reef system. Be honest about what you will find on the reef — parts are extraordinary, parts are not what they were.",
    img: "https://images.unsplash.com/photo-1587139223877-04ea7b022ced?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("balanced")) s+=3; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("explore")||a[6]?.includes("physical")) s+=3; return s; },
    intro: "The Great Barrier Reef is 2,300km long and the only living structure visible from space. Coral bleaching events in 2016, 2017, 2020, 2022, and 2024 have significantly degraded sections — particularly the southern and central areas. The northern Coral Sea and the Outer Reef accessible from Port Douglas retain extraordinary coral health. The Daintree Rainforest north of Port Douglas is 135 million years old — older than the Amazon — and meets the reef at Cape Tribulation, one of the only places on earth where two UNESCO World Heritage sites share a coastline. Port Douglas is the right base: smaller than Cairns, less package-tourist, 30 minutes closer to the best reef sections.",
    highlights: [
      { label: "Outer Reef from Port Douglas", text: "The Outer Reef is 50-70km offshore — the coral here is significantly healthier than Inner Reef sections closer to shore. Quicksilver runs the best day trips to Agincourt Reef, with underwater observatories and genuinely extraordinary coral. The best coral is in the shallows — snorkeling is sufficient." },
      { label: "Daintree Rainforest", text: "135 million years old, home to plants and animals found nowhere else. The drive from Port Douglas to Cape Tribulation crosses the Daintree River by cable ferry — no bridge by deliberate choice — and enters a forest that was here before the dinosaurs died out. The Mossman Gorge, a sacred site of the Kuku Yalanji people, is the best swimming hole in Queensland." },
      { label: "Cape Tribulation", text: "Where the rainforest meets the reef — the beach has the Coral Sea on one side and 135-million-year-old rainforest on the other. Named by Captain Cook who nearly lost his ship on the reef here in 1770. Swimming not recommended (box jellyfish October-May, crocodiles year-round) but the forest walk to the beach is extraordinary." },
      { label: "Cod Hole and Lizard Island", text: "The Cod Hole near Lizard Island — accessible by liveaboard from Cairns or light aircraft to Lizard Island — is the best dive site in Australia. Giant potato cod approach divers, healthy coral, the Ribbon Reefs above. A liveaboard to the Coral Sea is the most complete reef experience available." },
    ],
    eat: [
      { name: "Salsa Bar and Grill (Port Douglas)", desc: "The best restaurant in Port Douglas — Queensland barramundi, reef fish, Daintree-grown tropical fruit. The outdoor tables on Macrossan Street catch the evening breeze." },
      { name: "On the Inlet (Port Douglas)", desc: "A dock restaurant directly over the inlet — the mud crabs are caught daily by the restaurant's own traps, cooked to order. The best crab in Queensland." },
      { name: "Ochre Restaurant (Cairns)", desc: "The longest-running native ingredient restaurant in Australia — kangaroo, emu, crocodile, wattleseed, finger lime, quandong. The most direct introduction to Australian native food culture." },
    ],
    stay: [
      { name: "Lizard Island Resort", tier: "High end", desc: "The most remote luxury resort on the Great Barrier Reef — 24 villas on a private island, direct access to the Cod Hole dive site, the best snorkeling beach in Queensland from the front door." },
      { name: "Silky Oaks Lodge (Mossman Gorge)", tier: "High end", desc: "Treehouse rooms suspended above the Mossman River at the edge of the Daintree. Pool looking into the rainforest, spa using Daintree botanicals. The most atmospheric luxury stay in tropical Queensland." },
      { name: "Peppers Beach Club (Port Douglas)", tier: "Mid range", desc: "A well-positioned resort in the heart of Port Douglas — pool, walking distance to Macrossan Street, shuttle to the marina for reef trips." },
      { name: "Daintree Ecolodge", tier: "Mid range", desc: "15 bungalows elevated in the rainforest canopy — wallabies visible from the deck at dawn, the sound of the rainforest all night." },
    ],
    logistics: [
      { q: "When to go", a: "June-October — clear water, calm seas, the best reef visibility (20-30 metres on the Outer Reef). November-May is wet season — box jellyfish in the water, lower visibility. Never go for reef snorkeling between November and May if you can avoid it." },
      { q: "Getting there", a: "Fly into Cairns (CNS) — international flights from Japan, China, Singapore, and connections from Sydney and Melbourne. Port Douglas is 70km north (1 hour). Car rental essential for the Daintree." },
      { q: "Reef operator selection", a: "Choose operators with advanced eco-certification and marine biologist staff. Quicksilver (Agincourt Reef, Port Douglas) and Calypso are the best day-trip operators. Coral Princess and Mike Ball Dive Expeditions run the best liveaboards. Ask specifically about coral health reports before booking." },
      { q: "How long", a: "Three nights minimum. Day one: arrive Port Douglas. Day two: Outer Reef day trip (full day). Day three: Daintree and Cape Tribulation self-drive. Day four: Mossman Gorge, depart Cairns." },
    ],
  },
  {
    name: "Margaret River", country: "australia", tag: "Wine · Surf · Cape to Cape",
    hook: "The most underrated wine region in the world, next to a surf coast professional surfers travel specifically to reach. Almost no one outside Australia knows it exists.",
    img: "https://images.unsplash.com/photo-1474540412665-1cdae210ae6b?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")||a[3]?.includes("balanced")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=5; if(a[6]?.includes("wander")||a[6]?.includes("nothing")||a[6]?.includes("physical")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=4; return s; },
    intro: "Margaret River is 280km south of Perth where the Indian Ocean meets the Southern Ocean. Despite producing less than 3% of Australia's wine output, it accounts for over 20% of premium wine exports. The Cabernet Sauvignon here mirrors Bordeaux almost exactly — among the best in the world. The surf breaks at Surfers Point, Injidup, and the Box attract professionals for their consistency and power. The karri forests behind the coast are among the tallest in the world — individual trees reaching 70 metres — and contain limestone cave systems forming for 35,000 years. Almost no international tourists, strong sense of place, and one of the most complete wine-and-coast combinations on earth.",
    highlights: [
      { label: "Wilyabrup cellar door drive", text: "The road between Cowaramup and Margaret River passes 40 cellar doors in 20km. The benchmark producers: Cullen, Vasse Felix, Leeuwin Estate, Voyager Estate, Moss Wood. Most open daily 10am-5pm, tasting for AUD 5-10 (waived on purchase). Focus on Margaret River Cabernet Sauvignon and Chardonnay." },
      { label: "Cape to Cape Track", text: "A 135km walk between Cape Naturaliste lighthouse and Cape Leeuwin lighthouse — 4-5 days of coastal heath, karri forest, cliff tops, and beaches entirely to yourself. The southern section (Hamelin Bay to Cape Leeuwin) is the most dramatic." },
      { label: "Surfers Point", text: "The main break at Prevelly — a consistent left-hander holding waves from 3 to 12 feet. The Margaret River Pro (WSL Championship Tour) is held here. The viewing area above the break is the best surfing theatre in Australia." },
      { label: "Lake Cave", text: "One of 150 limestone caves in the Leeuwin-Naturaliste National Park — Lake Cave has a permanent underground lake reflecting a chandelier of calcite formations that appear to float. The 75-minute tour is the best of the caves." },
    ],
    eat: [
      { name: "Vasse Felix (Cowaramup)", desc: "The original Margaret River winery (1967) has the best restaurant in the region — seasonal menu built around the estate garden and local producers. The wine pairing lunch is the benchmark experience. Book months ahead for weekends." },
      { name: "Leeuwin Estate Restaurant", desc: "The most celebrated winery restaurant in Western Australia — the Art Series Chardonnay with the seasonal menu is the definitive Margaret River dining experience." },
      { name: "Settlers Tavern (Margaret River town)", desc: "The live music venue that has been the social center of Margaret River for decades — local bands every weekend, an excellent burger, regional beers on tap. The least pretentious meal in the region." },
    ],
    stay: [
      { name: "Rosewood Cape Lodge", tier: "High end", desc: "The finest lodge in Western Australia — 22 suites overlooking a lake, a restaurant using the estate kitchen garden, a private beach club. The most complete luxury experience in Margaret River." },
      { name: "Injidup Spa Retreat", tier: "High end", desc: "12 private villas on the cliff above Injidup Beach — infinity pool facing the Southern Ocean, a spa, no children. The most romantic stay in Margaret River." },
      { name: "The Berry Farm Cottages", tier: "Mid range", desc: "Self-contained cottages on a working farm between the wine region and the coast. The farm produces berries, jams, and wines. The most characterful mid-range stay." },
    ],
    logistics: [
      { q: "When to go", a: "Autumn (March-May) — harvest season, vines turn gold, cellar doors buzzing, surf at its most powerful. Winter (June-August) — quieter, green, storm-watching from clifftops. Spring (September-November) — wildflowers across the cape heath. Summer (December-February) — warmest but busiest." },
      { q: "Getting there", a: "Fly into Perth (PER), rent a car, drive south on the Bussell Highway. 3.5 hours with no stops. No meaningful public transport in the wine region — a car is mandatory." },
      { q: "How long", a: "Three nights minimum. Day one: drive from Perth, first cellar door. Day two: Cape to Cape coastal walk section, Surfers Point sunset. Day three: Wilyabrup cellar door drive, Vasse Felix lunch. Day four: Lake Cave, Cape Leeuwin lighthouse, drive back to Perth." },
    ],
  },
  {
    name: "Tasmania", country: "australia", tag: "Wilderness · MONA · Dark MOFO",
    hook: "An island off an island — more wilderness per square kilometre than anywhere in Australia, a museum that changed Australian art, and a winter festival that turns the whole island dark and strange.",
    img: "https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")||a[0]?.includes("culture")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=4; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=4; if(a[5]?.includes("mountains")||a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("physical")||a[6]?.includes("absorb")||a[6]?.includes("nothing")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=4; return s; },
    intro: "Tasmania is an island the size of Ireland at 42 degrees south. Forty per cent of it is protected wilderness. The Overland Track is Australia's most celebrated multi-day hike. The food scene — built on the world's cleanest air, extraordinary Atlantic salmon, remarkable truffles and dairy — is the best in Australia outside Melbourne. MONA, the Museum of Old and New Art, is built into the sandstone cliffs beneath a private winery outside Hobart — the most extraordinary privately owned museum in the world. The Dark MOFO winter festival each June turns the island dark, strange, and worth traveling specifically for.",
    highlights: [
      { label: "MONA (Hobart)", text: "David Walsh's private museum built into the sandstone cliffs — accessible only by high-speed ferry from Hobart. The collection is Walsh's personal obsession: ancient antiquities, contemporary provocations, a pipe organ made of 45 decomposing cars. The building descends four levels below the cliff face. Free for Tasmanians. AUD 35 for visitors." },
      { label: "Overland Track", text: "The 65km hut-to-hut walk through Cradle Mountain-Lake St Clair National Park — 6 days, past glacial lakes, dolerite peaks, ancient pencil pine forests, and the summit of Mount Ossa (Tasmania's highest point). Limited to 34 walkers per day October through May. Book the moment bookings release." },
      { label: "Freycinet Peninsula", text: "The pink granite peninsula on the east coast — Wineglass Bay (the curved white sand beach visible from the Hazards lookout, 30 minutes walk) is the most photographed beach in Australia. Walk down to the beach itself (15 more minutes) and have it nearly to yourself." },
      { label: "Dark MOFO (June)", text: "MONA's winter festival — two weeks of art, music, ritual, and deliberate darkness. The Nude Solstice Swim. Giant bonfires on the waterfront. International artists. Hobart in winter filled with people from everywhere. Book accommodation a year ahead." },
      { label: "Bruny Island", text: "An hour south of Hobart by car and ferry — the island that feeds the island. The Bruny Island Cheese Company, Get Shucked oyster farm (self-shuck at the table), the abalone farm. The southern end is a nature reserve with little penguins and Cape Barren geese." },
    ],
    eat: [
      { name: "Franklin (Hobart)", desc: "Tasmania's most celebrated restaurant — a wood-fire kitchen using exclusively Tasmanian produce. The degustation showcases the island's extraordinary dairy, seafood, and vegetables. One of the best restaurants in Australia." },
      { name: "Get Shucked Oysters (Bruny Island)", desc: "Self-shuck at the farm table overlooking the Channel — AUD 2 per oyster, a tool provided, the best oysters in Australia. The Drive-Thru Oyster Bar opens at 9am." },
      { name: "Aloft (Hobart)", desc: "A rooftop bar and restaurant above the waterfront — Tasmanian natural wines, local oysters, and views of the Derwent River and the mountain." },
    ],
    stay: [
      { name: "Saffire Freycinet", tier: "High end", desc: "A luxury lodge on the Freycinet Peninsula — direct views of the Hazards mountains and Great Oyster Bay. 20 suites, guided wildlife experiences, an extraordinary dining room. The most spectacular hotel setting in Tasmania." },
      { name: "The Henry Jones Art Hotel (Hobart)", tier: "High end", desc: "A converted historic jam factory on the Hobart waterfront — the art collection is rotated regularly, the rooms are designed around specific works. The most atmospheric hotel in Tasmania." },
      { name: "Islington Hotel (Hobart)", tier: "Mid range", desc: "A boutique hotel in a Regency mansion in South Hobart — 11 rooms, a garden with outdoor pool, morning newspaper before breakfast." },
      { name: "Under Canvas (Freycinet)", tier: "Good value", desc: "Safari-style tents at wilderness locations — canvas with proper beds, wood fires. The Freycinet location wakes up to the pink granite of the Hazards." },
    ],
    logistics: [
      { q: "When to go", a: "Summer (December-February) for the Overland Track, Freycinet, east coast swimming. Autumn (March-May) for harvest produce and extraordinary light. Winter (June) for Dark MOFO — worth the cold specifically. Spring (September-November) for wildflowers and the track reopening." },
      { q: "Getting there", a: "Fly into Hobart (HBA) or Launceston (LST) — multiple daily flights from Melbourne (1.5hrs) and Sydney (2hrs). Or take the Spirit of Tasmania ferry from Melbourne overnight (11 hours) — the cheapest way to bring a car." },
      { q: "How long", a: "Five nights for the highlights. Two nights Hobart (MONA, Franklin dinner, Bruny Island day trip). Two nights Freycinet (Wineglass Bay, full circuit if fit). One night Bay of Fires (the most beautiful beach coast in Australia). Drive to Launceston for flights." },
    ],
  },
  {
    name: "The Kimberley", country: "australia", tag: "Ancient Rock Art · Horizontal Falls · Last Wild Place",
    hook: "The most remote landscape in Australia. Rock art that predates any cave painting in Europe. Horizontal waterfalls through rock gaps so narrow boats surf through them.",
    img: "https://images.unsplash.com/photo-1508193638397-1c4234db14d8?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")) s+=5; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=5; if(a[5]?.includes("mountains")||a[5]?.includes("coast")||a[5]?.includes("desert")) s+=4; if(a[6]?.includes("explore")||a[6]?.includes("physical")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=5; if(a[8]?.includes("none")||a[8]?.includes("article")) s+=4; return s; },
    intro: "The Kimberley is a 424,000 square kilometre wilderness in the far northwest of Australia — ancient sandstone ranges, vast rivers, waterfalls, and gorges inaccessible by road for six months of the year. The Bungle Bungle Range (Purnululu) — beehive-striped sandstone domes unknown to the outside world until 1983 — is one of the most extraordinary geological formations on earth. The Horizontal Falls — tidal water forced through two narrow rock gaps, creating standing waves — are so improbable that David Attenborough called them one of the great natural wonders of the world. The Gwion Gwion rock paintings found across the Kimberley cliff faces are estimated at 17,000-50,000 years old — predating the European cave paintings of Lascaux.",
    highlights: [
      { label: "Bungle Bungle Range (Purnululu)", text: "Beehive-shaped domes of banded sandstone — black bands are cyanobacteria, orange is oxidised iron. Inaccessible during wet season (November-April). Cathedral Gorge walk (3km return) enters a natural amphitheatre with perfect acoustics. Echidna Chasm is a slot canyon so narrow you turn sideways. Fly over in a helicopter first — the scale from the air is only comprehensible from above." },
      { label: "Horizontal Falls", text: "Tidal water forced through two narrow rock gaps in the McLarty Range — the difference in water level creates what looks like a waterfall on its side. Boats surf through the gaps at full throttle. Accessible by seaplane or helicopter from Broome, or on a live-aboard from Derby." },
      { label: "Mitchell Falls (Punamii-unpuu)", text: "A four-tiered waterfall in the remote northwest Kimberley — reached by a 10km return walk through spinifex and ancient sandstone. The valley below has rock art galleries and rock pools. The most effort-rewarded destination in the Kimberley." },
      { label: "Gwion Gwion rock art", text: "The most ancient rock paintings in Australia — graceful elongated figures painted on cliff faces across the Kimberley. The oldest estimates predate any European cave art. Accessible on guided tours from Broome and Kununurra. Sacred to the Worrorra, Ngarinyin, and Wunumbal peoples." },
      { label: "Gibb River Road", text: "The 660km dirt road connecting Derby and Kununurra through the heart of the Kimberley — the most significant 4WD journey in Australia. Passes through gorges, station homesteads, swimming holes, and landscapes with no equivalent. Open May-October only. Requires a 4WD with a full-size spare and a satellite communicator." },
    ],
    eat: [
      { name: "Cable Beach Club (Broome)", desc: "Dinner by the pool — Kimberley barramundi, Cone Bay barramundi specifically, and Broome's specialty mud crab. The sunset over Cable Beach from the lawn is the most cinematic meal setting in the Kimberley." },
      { name: "Aarli Bar (Broome)", desc: "The most local bar in Broome — Kimberley barramundi, pearl meat (the pearl industry's by-product), and the best mango anything in Australia." },
      { name: "Station homestead meals", desc: "The stations along the Gibb River Road — El Questro, Home Valley, Drysdale River — all provide meals. Station cooking is honest and generous: large cuts of beef, damper bread, strong tea." },
    ],
    stay: [
      { name: "El Questro Homestead (Gibb River Road)", tier: "High end", desc: "A luxury station stay in the heart of the Kimberley — helicopter excursions to Cockburn Range, private gorge access, a swimming hole 10 minutes walk. The most comfortable way to experience the Kimberley wilderness." },
      { name: "Home Valley Station", tier: "Mid range", desc: "A working cattle station on the Gibb River Road — rooms range from camping to homestead suites. Horse musters, helicopter tours, gorge swimming trips." },
      { name: "Gibb River Road gorge camping", tier: "Good value", desc: "The gorge campsites along the Gibb — Manning Gorge, Galvans Gorge, Bell Gorge — are among the finest free camps in Australia. Bring everything. Wake in a gorge with a natural swimming hole." },
    ],
    logistics: [
      { q: "When to go", a: "May-October only (dry season). The wet season (November-April) closes the Gibb River Road, floods access to Purnululu, and makes the Horizontal Falls inaccessible overland. Best months June-August when waterfalls still have flow and temperatures are 25-30C." },
      { q: "Getting there", a: "Fly into Broome (BME) from Perth (2.5hrs) or Darwin (2hrs). Broome is the western gateway. Kununurra (KNL) is the eastern gateway and base for Purnululu and the Horizontal Falls seaplane. The Gibb River Road connects both — one-way drive, fly in one end fly out the other." },
      { q: "4WD requirement", a: "A 4WD with a full-size spare tyre is mandatory for the Gibb River Road and all station tracks. Fuel up at every opportunity — some sections have 300km between stations. A satellite communicator is essential — no mobile coverage in the Kimberley interior." },
      { q: "How long", a: "Ten days minimum. Three nights Broome (Cable Beach, Horizontal Falls seaplane). Seven days Gibb River Road (Windjana Gorge, Bell Gorge swim, Manning Gorge, El Questro, Bungle Bungles). Fly out of Kununurra." },
    ],
  },
  {
    name: "Kangaroo Island", country: "australia", tag: "Sea Lions · Wildlife · Emu Ridge",
    hook: "45 minutes by ferry from the South Australian mainland. Sea lions that approach you on the beach. Koalas in every second eucalyptus. Virtually no international tourists.",
    img: "https://images.unsplash.com/photo-1559827260-dc66d52bef19?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")||a[0]?.includes("adventure")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("balanced")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("nothing")||a[6]?.includes("wander")||a[6]?.includes("spontaneous")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("crowds")||a[9]?.includes("generic")) s+=4; if(a[8]?.includes("feel")||a[8]?.includes("none")) s+=3; return s; },
    intro: "Kangaroo Island is Australia's third-largest island — 155km long, 60km wide, 45 minutes by ferry from Cape Jervis on the South Australian mainland, and home to wildlife populations that developed in genetic isolation for 10,000 years. The Kangaroo Island kangaroo, the Ligurian bee (the only pure strain in the world), the Cape Barren goose, and the New Zealand fur seal all live here in populations that make wildlife encounters a question of patience rather than luck. Seal Bay has the largest accessible sea lion colony in the world. The island's food culture — built on extraordinary honey, raw-milk cheese, the best oysters in South Australia, and eucalyptus oil — makes it simultaneously a wildlife destination and a serious eating one.",
    highlights: [
      { label: "Seal Bay sea lions", text: "The Australian sea lion colony at Seal Bay is the only place in the world where you can walk on a beach with these animals under ranger guidance. The colony rests between deep-sea dives that can reach 300m. The bulls weigh 300kg. The dawn tour leaves you on the beach with the sunrise and 200 sea lions before day visitors arrive." },
      { label: "Flinders Chase National Park", text: "The western end of the island — Remarkable Rocks (granite boulders sculpted into shapes that look deliberately artistic), Admirals Arch (a natural rock arch through which New Zealand fur seals swim), and the Cape du Couedic lighthouse. Koalas are visible in almost every second tree. The Remarkable Rocks at sunset turn from grey to gold to orange." },
      { label: "Hanson Bay koalas", text: "The Hanson Bay Wildlife Sanctuary koala walk is the most reliable koala encounter in South Australia. The morning walk (9am) finds them active and low in the trees. Watch one move between branches and understand immediately why they sleep 20 hours a day." },
      { label: "Island food producers", text: "Kangaroo Island Spirits (gin from local botanicals), Emu Ridge Eucalyptus Distillery (the largest eucalyptus oil distillery in the Southern Hemisphere), Clifford's Honey Farm (Ligurian bees, only pure strain in the world), False Cape Wines (southernmost vineyard in South Australia), and the shellfish farm (Pacific oysters from the American River inlet). A full producer day." },
    ],
    eat: [
      { name: "Rockpool Restaurant (Southern Ocean Lodge)", desc: "The restaurant at the island's flagship lodge — entirely Kangaroo Island produce. Sea urchin from the cove below, lamb from the island's farms, honey from the Ligurian bees." },
      { name: "Kangaroo Island Oyster Bar (Penneshaw)", desc: "Fresh Pacific oysters from the island's farms shucked at the bar. AUD 25 for a dozen, shucked to order. The American River inlet produces extraordinary oysters." },
      { name: "Dudley Wines cellar door (Penneshaw)", desc: "The oldest winery on the island and the closest to the ferry terminal. The KI Pinot Gris is the best in South Australia. Taste before deciding where to spend your evenings." },
    ],
    stay: [
      { name: "Southern Ocean Lodge", tier: "High end", desc: "Rebuilt after the 2020 bushfires and reopened in 2023 — 15 suites cantilevered over the Southern Ocean cliff, exclusively island produce, naturalist guides for all excursions. One of the finest wilderness lodges in Australia." },
      { name: "Lifetime Private Retreats", tier: "Mid range", desc: "Self-contained cottages and farmhouses around the island — private, well-equipped. The Seal Bay Road and Flinders Chase properties are best positioned for wildlife." },
      { name: "Kangaroo Island YHA (Kingscote)", tier: "Good value", desc: "The only hostel on the island — clean, private rooms available, a kitchen for self-catering from the island's produce shops. Kingscote is the largest town and practical base." },
    ],
    logistics: [
      { q: "When to go", a: "Year-round. Summer (December-February) for sea lion pups and best beach weather. Winter (June-August) quieter and cooler — fur seals most active at Admirals Arch. Spring (September-November) for wildflowers and nesting birds. Avoid Christmas-January when the island fills with South Australian families." },
      { q: "Getting there", a: "Ferry from Cape Jervis to Penneshaw: 45 minutes, Sealink runs multiple daily crossings (AUD 55-75 per person, AUD 100-180 per vehicle). Drive from Adelaide to Cape Jervis: 1.5 hours. Or fly from Adelaide to Kingscote (35 minutes, REX Airlines). Bring your car — 155km long with no public transport." },
      { q: "Wildlife etiquette", a: "Seal Bay ranger tours are mandatory for beach access (AUD 42 per adult). Maintain ranger-instructed distance from sea lions. Do not touch koalas. Do not feed any wildlife. The island's unique ecosystems survived through isolation — check boots for seeds, report any unusual sightings." },
      { q: "How long", a: "Three nights minimum. Day one: ferry, Seal Bay afternoon. Day two: Flinders Chase (Remarkable Rocks, Admirals Arch), Hanson Bay koalas. Day three: producer tour (honey, gin, oysters, wine). Day four: ferry back. Four nights rewards the slower pace." },
    ],
  },
];


// ─── GEORGIA REGIONS ─────────────────────────────────────────────────────────
const georgiaRegions = [
  {
    name: "Tbilisi", country: "georgia", tag: "Wine · Soviet Architecture · Old Town",
    hook: "A city that was building wine bars while the rest of the world was still figuring out what natural wine was. The architecture is falling apart beautifully. The food is extraordinary.",
    img: "https://images.unsplash.com/photo-1565008576549-57569a49371d?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=5; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("bold")||a[4]?.includes("wild")) s+=3; if(a[5]?.includes("cities")) s+=5; if(a[6]?.includes("eat")||a[6]?.includes("absorb")||a[6]?.includes("wander")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; return s; },
    intro: "Tbilisi is one of the great undiscovered cities of the world — a place where crumbling 19th century balconies overhang cobblestone streets, where Soviet modernist architecture sits next to Persian-era bathhouses, where the natural wine bars serving amber wine from clay qvevri vessels are some of the best in the world, and where the food (khinkali dumplings, khachapuri cheese bread, churchkhela walnut candy) is so good that chefs from London and New York fly in to eat it. The old town Abanotubani district is built over natural sulphur springs — the bathhouses have been operating for 1,500 years. Nobody from your social circle has been here. That is the entire point.",
    highlights: [
      { label: "Abanotubani sulphur baths", text: "The old town district built over natural sulphur springs — the domed bathhouses have operated for 1,500 years. The private bathing rooms (book ahead, around GEL 50/hour) have stone pools fed by 37-degree mineral water with a distinctive sulphur smell that you stop noticing after five minutes. The Orbeliani Baths have the most beautiful facade — blue and white Islamic tilework on a 19th century building." },
      { label: "Narikala Fortress and the old town", text: "The 4th century fortress above the old town — walk up through the old town's crumbling balcony streets, past the Metekhi Church on the cliff, to the fortress walls above. The view over the old town, the Mtkvari River, and the new city is the defining image of Tbilisi. Go at dusk when the old town lights up." },
      { label: "Natural wine bars", text: "Georgia invented wine — the 8,000-year-old qvevri clay vessel tradition is the origin of all winemaking. The natural wine scene in Tbilisi is the best in the world for amber and skin-contact wines. Vino Underground, G.Vino, and Wine Factory No. 1 are the anchors. The Rkatsiteli amber wine and Saperavi red are the indigenous varieties to focus on." },
      { label: "Dry Bridge Market", text: "A weekend flea market on the bridge over the Mtkvari River — Soviet memorabilia, Georgian silver jewelry, old icons, vintage cameras, Stalin-era coins, hand-painted ceramics. The most concentrated antique market in the Caucasus. Arrive at 9am before the serious buyers leave." },
      { label: "Georgian food culture", text: "Khinkali (large soup dumplings — hold by the knot, bite a small hole, drink the broth, eat the filling, leave the knot) at Cafe Littera or Zakhar Zakharich. Khachapuri adjaruli (bread boat filled with cheese and egg) for breakfast. Badrijani nigvzit (fried aubergine with walnut paste). The Georgian table is one of the great undiscovered food cultures in the world." },
    ],
    eat: [
      { name: "Cafe Littera (Vera)", desc: "Inside the Writers House of Georgia, in a garden — the most beautiful restaurant in Tbilisi. Modern Georgian cooking using traditional ingredients: jonjoli (pickled bladdernut flowers), tkemali (plum sauce), churchkhela. Book well ahead." },
      { name: "Barbarestan (Chugureti)", desc: "A restaurant based on a 19th century Georgian cookbook discovered in a market. Every dish is a recipe from the book, updated with contemporary technique. The duck with cherry sauce and the stuffed peppers are the permanent fixtures." },
      { name: "Shavi Lomi (Vera)", desc: "The restaurant that defined the Tbilisi food revival — a narrow room, natural Georgian wines, creative small plates based on Georgian ingredients. Still the most interesting food in the city." },
      { name: "Vino Underground (Old Town)", desc: "The natural wine bar that put Tbilisi on the international wine map — a basement room, 100+ Georgian natural wines by the glass, no food. Come after dinner. The Rkatsiteli from Kakheti at whatever price the staff recommend." },
    ],
    stay: [
      { name: "Stamba Hotel (Vake)", tier: "High end", desc: "A converted Soviet printing house — the most design-focused hotel in the Caucasus. The 9-metre ceilings in the former press hall, the best breakfast in Tbilisi, a roof terrace with the city below." },
      { name: "Fabrika (Chugureti)", tier: "Mid range", desc: "A converted Soviet sewing factory — hostel rooms, apartments, and a courtyard with 15 independent bars and restaurants. The social center of the Tbilisi creative scene." },
      { name: "Vinotel (Old Town)", tier: "Mid range", desc: "A small wine-focused boutique hotel in the old town — each room designed around a Georgian wine region, a cellar with 500+ Georgian wines, 5 minutes from the sulphur baths." },
      { name: "Old Metekhi (Old Town)", tier: "Good value", desc: "A guesthouse on the cliff above the Mtkvari River with direct views of the old town and the Narikala Fortress. Basic rooms, extraordinary location, breakfast included." },
    ],
    logistics: [
      { q: "When to go", a: "April-June and September-November are the ideal months — warm, clear, the city at its most alive. July-August is hot (35C+) and crowded with domestic tourists. Winter (December-February) is cold but atmospheric — the sulphur baths are at their best." },
      { q: "Getting there", a: "Fly into Tbilisi International Airport (TBS) — direct flights from London Heathrow (4.5hrs on Georgian Airways/British Airways), Istanbul (2hrs), Vienna, Warsaw, Tel Aviv. No direct flights from the US — connect through Istanbul, Amsterdam, or Frankfurt. The airport is 20 minutes from the old town by taxi (around GEL 30)." },
      { q: "Getting around", a: "The old town, Abanotubani, Rustaveli Avenue, and the Vera and Vake neighborhoods are all walkable or short taxi rides. Bolt (the Eastern European Uber) is extremely cheap — GEL 5-8 for most city journeys. The metro works but is less useful for tourists." },
      { q: "Money", a: "Georgia uses the Lari (GEL). 1 USD = approximately 2.7 GEL. Tbilisi is extremely cheap by Western standards — a full dinner with wine at a good restaurant is GEL 80-120 (USD 30-45) per person. The sulphur baths: GEL 50/hour for a private room. Stamba Hotel: GEL 400-600/night. Fabrika hostel dorms: GEL 40-60." },
      { q: "How long", a: "Three nights minimum. Day one: old town, Narikala at dusk, sulphur baths. Day two: Dry Bridge Market, Cafe Littera lunch, wine bars in the evening. Day three: day trip to Mtskheta (the ancient capital, 20 minutes away), Barbarestan for the final dinner." },
    ],
  },
  {
    name: "Kazbegi & The Military Highway", country: "georgia", tag: "Caucasus · Gergeti Trinity · High Mountains",
    hook: "A 14th century church on a 2,170 metre peak with the Greater Caucasus behind it. The drive to get there is one of the great mountain roads in the world.",
    img: "https://images.unsplash.com/photo-1589182337358-2cb63099350c?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")) s+=4; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=5; if(a[5]?.includes("mountains")) s+=6; if(a[6]?.includes("physical")||a[6]?.includes("explore")||a[6]?.includes("nothing")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; return s; },
    intro: "Kazbegi is a small town at 1,700 metres in the Greater Caucasus, 150km north of Tbilisi on the Georgian Military Highway — the road that connects Georgia to Russia through the Dariali Gorge. The Gergeti Trinity Church sits on a 2,170 metre peak above the town, with the 5,047 metre Mount Kazbek behind it — one of the most dramatic church positions in the world. The hike up takes 2-3 hours. The Military Highway itself passes the Ananuri Fortress on the Zhinvali Reservoir, the Gudauri ski resort, the Jvari Pass at 2,379 metres, and the valley descent into Kazbegi — a drive that is extraordinary in every season. In winter the road closes in snowstorms; in summer it is clogged with marshrutka minibuses. The shoulder seasons are when the mountains are at their best.",
    highlights: [
      { label: "Gergeti Trinity Church", text: "The 14th century church on the 2,170 metre peak above Kazbegi — a 2-3 hour hike from the town or a 4WD track (hire a local driver for GEL 40-60 return). The view from the churchyard: Kazbegi town below, the Terek River valley, and Mount Kazbek's glacier above. Arrive before 9am to have it without the tour groups." },
      { label: "Mount Kazbek summit attempt", text: "The 5,047 metre dormant volcano above Kazbegi is a serious mountaineering objective — the standard route from Betlemi hut requires crampons, ice axe, and experience. The acclimatization hike to the Betlemi Hut (3,650m) is accessible to fit hikers without technical equipment and provides the best close-up view of Kazbek's glacier. Two days from Kazbegi town." },
      { label: "The Military Highway drive", text: "The Georgian Military Highway from Tbilisi to Kazbegi (150km, 3 hours) passes: the Mtskheta ancient capital junction, the Ananuri Fortress rising from the Zhinvali Reservoir, Gudauri ski resort, the Jvari Pass at 2,379 metres with a view north into Russia. Drive it slowly, stop constantly. One of the great mountain roads in the world." },
      { label: "Truso Valley", text: "A high valley east of Kazbegi accessible by 4WD — abandoned Ossetian villages, mineral springs that have dyed the rocks orange and red, a glacial lake at the valley head. Almost no visitors. Half a day from Kazbegi with a local driver." },
    ],
    eat: [
      { name: "Rooms Hotel Kazbegi restaurant", desc: "The best food in the region — Georgian mountain cooking with the Gergeti Trinity Church visible through the floor-to-ceiling windows. Lamb stew, fresh trout from the Terek River, churchkhela for dessert. Worth staying at the hotel for the view alone." },
      { name: "Local guesthouses (Kazbegi town)", desc: "Every family in Kazbegi runs a guesthouse and every guesthouse serves the same meal: fresh bread, cheese, beans, meat stew, homemade chacha (Georgian grape spirit). GEL 20-30 for a full dinner. The best food in Kazbegi is not in any restaurant." },
    ],
    stay: [
      { name: "Rooms Hotel Kazbegi", tier: "High end", desc: "A Soviet sanatorium converted into the most dramatic hotel in Georgia — floor-to-ceiling windows facing the Gergeti Trinity Church and Mount Kazbek. The most extraordinary view from any hotel lobby in the Caucasus." },
      { name: "Guesthouse Nino (Kazbegi town)", tier: "Good value", desc: "The guesthouse model that defines Kazbegi hospitality — a family home with spare rooms, home-cooked dinners, local knowledge freely given. GEL 60-80 per person including dinner and breakfast." },
    ],
    logistics: [
      { q: "Getting there", a: "Marshrutka minibuses from Didube station in Tbilisi to Kazbegi (GEL 10, 3 hours, leaves when full from 9am). Taxi from Tbilisi: GEL 150-200 one way, or hire a driver for the day (GEL 200-250 return including stops). Renting a car in Tbilisi and driving yourself is straightforward — the road is paved all the way." },
      { q: "When to go", a: "May-June and September-October for the clearest mountain views and manageable crowds. July-August is the peak season — Gergeti Trinity is crowded, guesthouses book out. Winter (December-March) for skiing at Gudauri (30 minutes below Kazbegi on the highway) — the Gergeti hike is possible with proper footwear." },
      { q: "How long", a: "Two nights. Day one: drive from Tbilisi (stops at Mtskheta and Ananuri Fortress), arrive Kazbegi, evening in town. Day two: Gergeti Trinity Church hike (early start), afternoon Truso Valley 4WD. Day three: return to Tbilisi." },
    ],
  },
  {
    name: "Kakheti Wine Region", country: "georgia", tag: "Qvevri Wine · Telavi · Alazani Valley",
    hook: "The oldest wine culture on earth. 8,000 years of unbroken winemaking tradition. The wine is made in clay pots buried in the ground and it tastes like nothing else in the world.",
    img: "https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("food")||a[0]?.includes("culture")||a[0]?.includes("escape")) s+=4; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=4; if(a[5]?.includes("countryside")) s+=5; if(a[6]?.includes("eat")||a[6]?.includes("wander")||a[6]?.includes("nothing")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=3; return s; },
    intro: "Kakheti is Georgia's main wine region in the Alazani River valley east of Tbilisi — a landscape of vineyards, fortress monasteries, and 19th century merchant towns backed by the Greater Caucasus. Georgia invented wine approximately 8,000 years ago in this valley — the qvevri clay vessel tradition (grapes fermented with their skins in buried clay pots, producing the amber and orange wines that the world's natural wine scene has discovered) is a UNESCO Intangible Cultural Heritage. The family wineries that line the valley road between Telavi and Sighnaghi are not the polished tasting rooms of Napa or Bordeaux — they are family homes where the grandparents press the grapes by foot in October and the wine is sold by the litre from a plastic jug.",
    highlights: [
      { label: "Qvevri winery visits", text: "The small family wineries of Kakheti — Pheasant's Tears in Sighnaghi, Alaverdi Monastery winery (monks have made wine here since the 6th century), Jakeli Wines in Telavi — offer the most direct access to the qvevri tradition. The amber Rkatsiteli, skin-contact fermented for six months in buried clay, is the wine to taste. Most wineries welcome unannounced visitors; a call ahead is appreciated." },
      { label: "Sighnaghi", text: "The most beautiful town in Kakheti — a hilltop town with a complete 18th century defensive wall enclosing cobblestone streets, Armenian and Georgian churches, a small museum with Niko Pirosmani paintings, and the Alazani Valley and Greater Caucasus visible from the ramparts. Two hours from Tbilisi. The town runs on wine tourism and does it with genuine charm." },
      { label: "Bodbe Monastery", text: "A 9th century monastery just below Sighnaghi containing the tomb of Saint Nino, who brought Christianity to Georgia in the 4th century. One of the most sacred sites in the country. The monastery garden looks over the Alazani Valley. The nuns here make preserves and candles sold at the entrance gate." },
      { label: "Alaverdi Cathedral", text: "An 11th century cathedral in the Alazani Valley — the tallest medieval building in Georgia (50 metres) and one of the most significant religious sites in the Caucasus. The working monastery attached to the cathedral has made wine in its cellar since the 6th century. The grape harvest festival here in October is one of the great Georgian cultural events." },
    ],
    eat: [
      { name: "Pheasant's Tears (Sighnaghi)", desc: "John Wurdeman's legendary restaurant attached to his natural winery — the most famous table in Georgian wine country. Traditional Georgian dishes, exclusively qvevri wines, a garden setting. Book weeks ahead in summer. The mtsvadi (grilled meat skewers) and the lobiani (bean-filled bread) are the standards." },
      { name: "Tamada (Telavi)", desc: "A family restaurant in Telavi's old town doing the most honest Georgian table in the region — supra (Georgian feast) format, local wines poured continuously, the tamada (toastmaster) tradition observed. The long lunch here is the Kakheti experience." },
    ],
    stay: [
      { name: "Rooms Hotel Kokhta (near Kvareli)", tier: "High end", desc: "A wine resort in the foothills of the Greater Caucasus — vineyard views, a cellar with 200+ Georgian wines, guided harvest experiences in October." },
      { name: "Bina 36 (Sighnaghi)", tier: "Mid range", desc: "A boutique guesthouse inside the Sighnaghi walls — the best-positioned rooms in town, a wine bar with local producers, breakfast using Kakheti dairy and preserves." },
      { name: "Family guesthouses (Sighnaghi)", tier: "Good value", desc: "The guesthouses inside the Sighnaghi walls are mostly family homes with spare rooms — GEL 80-120 per person including dinner and breakfast. The hosts are invariably winemakers." },
    ],
    logistics: [
      { q: "Getting there", a: "Marshrutka from Tbilisi's Samgori station to Sighnaghi (GEL 8, 2 hours). Taxi from Tbilisi: GEL 80-100 one way. Car rental from Tbilisi gives the most freedom — the valley road between Telavi and Sighnaghi (80km) has a winery every 5km. A driver-guide for the day from Tbilisi costs USD 80-120." },
      { q: "When to go", a: "September-October for the Rtveli grape harvest — the most important event in the Georgian calendar. The entire valley is harvesting, pressing, and celebrating simultaneously. April-June for the spring vineyards. Avoid July-August when the valley is hot (38C+)." },
      { q: "How long", a: "Two nights in the region. Night one Sighnaghi (Pheasant's Tears dinner, the ramparts at sunset). Day two: Alaverdi Cathedral and the valley winery drive. Night two at a Telavi guesthouse. Return to Tbilisi day three." },
    ],
  },
  {
    name: "Svaneti", country: "georgia", tag: "Medieval Towers · Glaciers · Mestia",
    hook: "A highland region that was so isolated it developed its own language, its own alphabet, and its own medieval defensive tower tradition. The glaciers are retreating. Go now.",
    img: "https://images.unsplash.com/photo-1567942712661-82b9b407abbf?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")) s+=5; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=5; if(a[5]?.includes("mountains")) s+=6; if(a[6]?.includes("physical")||a[6]?.includes("explore")||a[6]?.includes("nothing")) s+=5; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=5; if(a[8]?.includes("none")||a[8]?.includes("article")) s+=5; return s; },
    intro: "Svaneti is a highland region in the Greater Caucasus at 1,500-2,200 metres elevation, accessible by a spectacular road through the Enguri Gorge or by a 45-minute flight from Tbilisi. The Svans — the people of Svaneti — developed in near-total isolation for centuries and have their own language (Svan, spoken by around 30,000 people), their own distinct culture, and a tradition of building defensive towers (koshkebi) beside their houses that produced some of the most extraordinary medieval architecture in the world. The village of Ushguli, at 2,200 metres, is the highest continuously inhabited settlement in Europe — four villages with 200 stone towers visible simultaneously, the 5,201 metre Mount Shkhara glacier in the background.",
    highlights: [
      { label: "Ushguli", text: "The highest continuously inhabited settlement in Europe — four villages at 2,200 metres with 200 medieval stone towers visible simultaneously. A UNESCO World Heritage site. The road from Mestia (45km) is unpaved and requires a 4WD — 2.5 hours each way, impassable in winter. The village has 70 permanent residents and is completely extraordinary." },
      { label: "Mestia towers", text: "The regional center of Svaneti — a small town with its own forest of medieval defensive towers, a good museum of Svan icons and artifacts, and the trailhead for most Svaneti hikes. The towers here are in better condition than Ushguli and the town has enough infrastructure to be a genuine base." },
      { label: "Koruldi Lakes hike", text: "A 4-5 hour hike from Mestia to three alpine lakes at 2,700 metres — the view from the lakes takes in the entire Svaneti valley and the Caucasus ridge including Ushba (2,695m, the most technically demanding peak in the Caucasus). No special equipment needed, just fitness. The most rewarding half-day hike in Georgia." },
      { label: "Chalaadi Glacier", text: "A 45-minute walk from the Mestia-Ushguli road to the snout of the Chalaadi Glacier — one of the most accessible glaciers in the Caucasus, retreating visibly each year. The glacier snout is a 20-minute walk from the parking area. Combine with the Mestia towers for a full day." },
    ],
    eat: [
      { name: "Laila Restaurant (Mestia)", desc: "The best restaurant in Svaneti — kubdari (Svan meat pie, the regional speciality, completely different from anything in the rest of Georgia), local beer, the Caucasus peaks from the terrace." },
      { name: "Guesthouse dinners (Mestia and Ushguli)", desc: "Every guesthouse in Svaneti serves kubdari, bean soup, and homemade Svan salt (a spiced condiment unique to the region) — the food here is distinct from lowland Georgia. The chacha (grape spirit) is stronger and the welcome is warmer than anywhere else in the country." },
    ],
    stay: [
      { name: "Guesthouse Nino Ratiani (Mestia)", tier: "Mid range", desc: "The most recommended guesthouse in Mestia — the tower room looks directly at the Svan towers, the dinners are the best in town, the family provides local hiking guides." },
      { name: "Ushguli guesthouses", tier: "Good value", desc: "Staying in Ushguli itself — there are four small guesthouses in the village — means waking at 2,200 metres with the towers and the glacier before any day-trippers from Mestia arrive. The most extraordinary overnight in Georgia." },
    ],
    logistics: [
      { q: "Getting there", a: "Fly Tbilisi to Mestia (45 minutes, Vanilla Sky Airlines, GEL 150-200 each way — book well ahead, limited seats). Or marshrutka from Tbilisi's Didube station (9 hours, GEL 35) or Zugdidi (3 hours, GEL 15). The drive through the Enguri Gorge is extraordinary but very long." },
      { q: "When to go", a: "June-October. The Ushguli road is closed by snow November-May. July and August are the busiest months — June and September are the sweet spots. Winter in Mestia (December-March) is for skiing on the small local ski field — the towers in snow are extraordinary." },
      { q: "How long", a: "Three nights minimum. Night one Mestia (towers, museum). Day two: Koruldi Lakes hike. Day three: Ushguli 4WD day trip (full day). Night three Mestia or Ushguli. Fly back to Tbilisi day four." },
    ],
  },
  {
    name: "Tbilisi to Black Sea — Adjara", country: "georgia", tag: "Batumi · Subtropical Coast · Mountains",
    hook: "A subtropical Georgian coast with a casino skyline on one end and cloud forests on the other. The contrast is completely insane and completely Georgian.",
    img: "https://images.unsplash.com/photo-1578662996442-48f60103fc96?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")||a[0]?.includes("adventure")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("balanced")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("mountains")) s+=4; if(a[6]?.includes("wander")||a[6]?.includes("spontaneous")||a[6]?.includes("nothing")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; return s; },
    intro: "Adjara is Georgia's autonomous southwestern region on the Black Sea coast — a subtropical zone where the Caucasus mountains rise directly from the sea and the cloud forests of the Mtirala National Park receive 4,500mm of rain a year. Batumi is the regional capital: a 19th century Ottoman-era old town with ornate balconied buildings, a Soviet-era seaside promenade, and a bizarre new skyline of casino towers built for the post-Soviet nouveau riche. The combination is uniquely Georgian. The Machakhela Valley behind the coast — terraced tea plantations, wooden guesthouses, waterfalls — is the opposite of Batumi and one of the most beautiful valleys in the Caucasus.",
    highlights: [
      { label: "Batumi old town", text: "The Ottoman-era old town with its ornate wrought-iron balconied buildings — entirely different from Tbilisi. The Piazza square, the Alphabetic Tower (a rotating structure with the Georgian and Adjaran alphabets spiraling up it), the botanical garden above the city on the cliff. Walk the old town at night when the casino lights are reflected in the Black Sea." },
      { label: "Machakhela Valley", text: "The valley behind Batumi climbing into the Caucasus — terraced tea plantations (Georgia produces tea here, a Soviet-era industry that survived), wooden guesthouses, waterfalls, and the Mtirala cloud forest at the top. A full day from Batumi by car or a two-day hike. The most beautiful landscape in Adjara." },
      { label: "Black Sea coast", text: "The Georgian Black Sea coast north of Batumi — Kobuleti, Ureki (magnetic black sand), Gonio fortress (a Roman fort that contained one of the earliest Christian communities in the world, according to tradition). The coast road north is a slow, beautiful drive." },
    ],
    eat: [
      { name: "Adjarian Wine House (Batumi)", desc: "The best restaurant in Batumi — Adjaran dishes that differ from mainstream Georgian cooking (the region was Ottoman for centuries). The Adjaran khachapuri (the original boat-shaped cheese and egg bread, made here better than anywhere in Georgia)." },
      { name: "Machakhela valley guesthouses", desc: "The guesthouses in the Machakhela Valley serve the most isolated and genuine Georgian mountain cooking — corn bread, bean dishes, smoked meats, homemade wine and chacha. The ingredients come from the farm outside the window." },
    ],
    stay: [
      { name: "Paragraph Resort (Batumi)", tier: "High end", desc: "The best resort hotel on the Georgian Black Sea — a full beach club, the cleanest pool on the coast, and enough buffer from the casino chaos to feel like a genuine resort." },
      { name: "Old Town Boutique Hotel (Batumi)", tier: "Mid range", desc: "Inside the Ottoman old town — restored balconied building, the best location in Batumi, walking distance to the waterfront and the night market." },
      { name: "Machakhela guesthouses", tier: "Good value", desc: "The family guesthouses in the valley — GEL 50-70 per person including dinner and breakfast. The most genuine hospitality in Adjara." },
    ],
    logistics: [
      { q: "Getting there", a: "Fly Tbilisi to Batumi (1 hour, GEL 80-150). Or overnight train from Tbilisi (6 hours, GEL 30-80 depending on class — the most scenic train journey in Georgia). Car from Tbilisi: 5.5 hours via the main highway." },
      { q: "When to go", a: "May-October for the coast. The Black Sea is warm (24-26C) July-September. The Machakhela Valley is beautiful year-round but the cloud forest is most dramatic in spring (April-May) when the waterfalls are at full flow." },
      { q: "How long", a: "Two nights. Day one Batumi (old town, waterfront, Adjarian Wine House). Day two: Machakhela Valley day trip. Return to Tbilisi day three or fly home from Batumi Airport." },
    ],
  },
];

// ─── COLOMBIA REGIONS ─────────────────────────────────────────────────────────
const colombiaRegions = [
  {
    name: "Cartagena", country: "colombia", tag: "Walled City · Caribbean · Colonial Color",
    hook: "The most beautiful colonial city in the Americas. The walls have been standing since 1586. The heat is part of it.",
    img: "https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("balanced")||a[3]?.includes("local")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("cities")) s+=4; if(a[6]?.includes("wander")||a[6]?.includes("eat")||a[6]?.includes("absorb")) s+=4; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=3; return s; },
    intro: "Cartagena de Indias is a walled colonial city on the Caribbean coast of Colombia — the best-preserved Spanish colonial architecture in South America, a UNESCO World Heritage Site, and a city that operates at a specific pace dictated by the Caribbean heat. The Ciudad Amurallada (walled city) is a maze of cobblestone streets, bougainvillea-draped balconies, painted colonial buildings in yellow and ochre and terracotta, and plazas where everyone eventually ends up. Outside the walls, the Getsemaní neighborhood — once considered dangerous, now the most interesting part of the city — has the best street art, the most local bars, and the cheapest, best food in Cartagena.",
    highlights: [
      { label: "The walled city at dusk", text: "The Ciudad Amurallada is the reason Cartagena exists on every travel list — the 11km of city walls completed in 1796 after 200 years of construction, the Clock Tower gate, the Plaza de los Coches, the Cathedral. Walk the walls at sunset when the Caribbean light turns everything gold and the heat finally breaks." },
      { label: "Getsemaní", text: "The neighborhood outside the walls that has become the most interesting part of Cartagena — murals covering every surface, local bars spilling onto the streets, the Trinidad Square filling up at night with families and vendors and music. The locals who have lived here for generations and the artists and travelers who followed them coexist in a way that still works." },
      { label: "Islas del Rosario", text: "A 90-minute boat ride from Cartagena — a coral archipelago of 27 islands in the Caribbean with clear water, good snorkeling, and beaches that look exactly like the Caribbean should. Day trips leave from the Muelle Turistico daily. The furthest islands have the clearest water. Bring sunscreen." },
      { label: "Castillo San Felipe de Barajas", text: "The largest Spanish colonial fortress in the Americas — built on a 40-metre hill, a network of tunnels that allowed troops to move invisibly between positions, never successfully stormed. The view over the city and the Caribbean from the ramparts is the best in Cartagena." },
      { label: "Palenque day trip", text: "San Basilio de Palenque — 50km from Cartagena, the first free African town in the Americas (founded by escaped slaves in 1603, never reconquered by the Spanish) and still home to a living culture with its own Creole language, music, and traditions. The most historically significant day trip from Cartagena." },
    ],
    eat: [
      { name: "La Cevicheria (Walled City)", desc: "The ceviche that put Cartagena on the culinary map — a tiny room on a back street, fresh Caribbean fish prepared with Colombian and Peruvian technique. The coconut ceviche and the octopus are the permanent orders. Queue outside or arrive at opening." },
      { name: "El Boliche Ceviche Bar (Getsemaní)", desc: "The Getsemaní version of La Cevicheria — cheaper, more local, equally good. The shrimp ceviche in coconut milk is specific to the Caribbean coast. Eat at the plastic tables on the street." },
      { name: "Carmen (Walled City)", desc: "The most ambitious kitchen in Cartagena — Caribbean ingredients treated with genuine technique. The tasting menu uses ingredients from the surrounding coast and the interior. The most complete fine dining experience in the city." },
      { name: "Street food (Getsemaní)", desc: "The arepas de huevo (deep-fried corn cakes with egg inside), the empanadas from the corner vendors, the fresh fruit with salt and lime from the market women. The best eating in Cartagena costs almost nothing and happens on the street." },
    ],
    stay: [
      { name: "Casa San Agustin (Walled City)", tier: "High end", desc: "A colonial mansion converted into the finest hotel in Cartagena — three adjoined houses, a pool in the central courtyard, original frescoes in the hallways. The most atmospheric luxury stay in Colombia." },
      { name: "Tcherassi Hotel (Walled City)", tier: "High end", desc: "A converted colonial house by Colombian fashion designer Silvia Tcherassi — the rooms are small but exquisitely designed, the rooftop pool looks over the terracotta rooftops of the walled city." },
      { name: "Hotel Casa del Curato (Walled City)", tier: "Mid range", desc: "A converted 17th century convent in the heart of the walled city — high ceilings, a central patio, the best-value colonial stay in Cartagena." },
      { name: "Casa Lola (Getsemaní)", tier: "Good value", desc: "A boutique guesthouse in Getsemaní — the neighborhood's energy outside the door, a rooftop with walled city views, the most interesting location in Cartagena for significantly less than the walled city hotels." },
    ],
    logistics: [
      { q: "When to go", a: "December-April is the dry season — the best weather, the most visitors, the highest prices. May-November is the wet season with afternoon thunderstorms that clear quickly. The city operates year-round. The heat (30-35C) is constant regardless of season — it is part of the experience." },
      { q: "Getting there", a: "Fly into Rafael Nunez International Airport (CTG) — direct flights from Miami (3hrs), New York JFK (4.5hrs), Bogota (1hr), Medellin (1hr). The airport is 20 minutes from the walled city by taxi (COP 25,000-35,000)." },
      { q: "Safety", a: "The walled city and Getsemaní are both safe for tourists in 2024-2025. Standard urban precautions apply: don't display expensive cameras or jewelry after dark, use registered taxis or apps (InDriver, Cabify), avoid deserted streets late at night. Cartagena has transformed significantly in the past decade." },
      { q: "How long", a: "Three nights. Day one: walled city orientation, walls at sunset, Getsemaní evening. Day two: Castillo San Felipe, Islas del Rosario boat trip. Day three: Palenque day trip, final dinner at La Cevicheria. Cartagena connects easily with Medellin (1hr flight)." },
    ],
  },
  {
    name: "Medellín", country: "colombia", tag: "Transformation · Coffee · Eternal Spring",
    hook: "The most improved city on earth over the past 30 years. From the murder capital of the world in 1991 to a city that makes urban planners travel specifically to study it.",
    img: "https://images.unsplash.com/photo-1583001931096-959e9a1a6223?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")||a[0]?.includes("adventure")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=5; if(a[4]?.includes("bold")||a[4]?.includes("stretch")) s+=4; if(a[5]?.includes("cities")) s+=5; if(a[6]?.includes("absorb")||a[6]?.includes("wander")||a[6]?.includes("eat")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; return s; },
    intro: "Medellín sits in a narrow Andean valley at 1,495 metres elevation — the altitude gives it the eternal spring climate (22-25C year round) that makes it the most pleasant large city in Colombia. In 1991 it was the murder capital of the world. The story of what happened next — the urban cable cars connecting hillside comunas that had no road access, the escalators built into the steepest slopes, the libraries in the most violent neighborhoods, the complete redesign of public space — is the most remarkable urban transformation in modern history. The city now hosts architecture conferences, the food scene is extraordinary, and the Laureles and El Poblado neighborhoods have become one of the most livable urban environments in South America.",
    highlights: [
      { label: "Metrocable and the comunas", text: "The urban cable car system that connected the hillside comunas to the metro — ride Line K to the top of Santo Domingo and walk down through a neighborhood where people who had never left their barrio suddenly had access to the entire city. The view over Medellin from the cable car is extraordinary. The transformation visible between the bottom and top stations is the entire story of the city." },
      { label: "Plaza Botero and the Museo de Antioquia", text: "Fernando Botero donated 23 of his monumental bronze sculptures to his home city — they fill the plaza in front of the Museo de Antioquia, which holds the largest Botero collection in the world (over 100 paintings). The museum is the best in Colombia and entry costs almost nothing." },
      { label: "El Poblado and Laureles food scene", text: "Medellín's restaurant culture has developed faster than almost any other city in South America over the past decade. El Cielo (molecular Colombian), Carmen (traditional Antioquian updated), Alambique (Cartagena seafood in the mountains), and the market at Mercado del Rio are the anchors. The coffee culture is the best in Colombia — you are in the coffee region." },
      { label: "Guatapé day trip", text: "80km from Medellín — the Piedra del Penol (a 220-metre granite monolith with 740 steps to the top and a view over the reservoir and the 200 islands below it) and the village of Guatapé itself (every building painted with colorful zocalos — bas-relief panels on the lower facade, each depicting something about the building's owner or history). The best day trip from Medellín." },
    ],
    eat: [
      { name: "El Cielo (El Poblado)", desc: "Colombia's most famous restaurant — chef Juan Manuel Barrientos's molecular Colombian tasting menu. The most technically adventurous meal in the country. Book weeks ahead." },
      { name: "Alambique (El Poblado)", desc: "Caribbean coastal Colombian cooking in the mountains — the best ceviche in Medellín, fresh fish from the coast arriving daily, the coconut rice a permanent fixture." },
      { name: "Mercado del Rio", desc: "A two-story food market in the city center — 45 vendors covering every Colombian regional cuisine. The most efficient way to eat a lot of good food in Medellín. Lunch only." },
      { name: "Pergamino Cafe (El Poblado)", desc: "The best specialty coffee shop in Colombia — single origin Colombian beans, exceptional technique, the coffee education you came to the country for. The flat white here is the benchmark." },
    ],
    stay: [
      { name: "The Charlee (El Poblado)", tier: "High end", desc: "The rooftop pool with the best view of the Medellin valley, a restaurant that takes Colombian produce seriously, the most design-forward hotel in the city." },
      { name: "Casa Dann Carlton (El Poblado)", tier: "Mid range", desc: "A well-run hotel in the heart of El Poblado — the restaurant, the pool, and the location are all strong. The most practical mid-range base in the city." },
      { name: "Selina Medellin (Laureles)", tier: "Good value", desc: "The Selina in the Laureles neighborhood — the better side of Medellin for a more local experience. Pool, coworking, a social scene that connects solo travelers." },
    ],
    logistics: [
      { q: "Getting there", a: "Fly into Jose Maria Cordova Airport (MDE) — direct from Miami (3hrs), New York (5hrs), Madrid (10hrs), Bogota (1hr), Cartagena (1hr). The airport is 45 minutes from El Poblado by taxi (COP 70,000-90,000) or airport bus." },
      { q: "When to go", a: "Year-round — the eternal spring climate (22-25C) makes Medellin one of the most weather-consistent cities in the world. December and January are slightly drier and busier. April-May and October-November have more rain (afternoon showers, not all-day rain)." },
      { q: "Safety", a: "El Poblado and Laureles are both safe and well-patrolled tourist neighborhoods. The comunas (hillside neighborhoods) are worth visiting on a guided tour — operators like Zippy Tours run responsible community tourism. Standard urban precautions apply everywhere. The transformation is real but uneven." },
      { q: "How long", a: "Three nights. Day one: Metrocable and Santo Domingo, Plaza Botero. Day two: Guatape day trip (full day). Day three: El Poblado food tour, Pergamino coffee, El Cielo dinner." },
    ],
  },
  {
    name: "Coffee Region (Eje Cafetero)", country: "colombia", tag: "Coffee Farms · Wax Palms · Valle del Cocora",
    hook: "The valley where Colombia's coffee comes from. Wax palms 60 metres tall in the clouds. Coffee picked by hand on hillside farms that have been in the same family for five generations.",
    img: "https://images.unsplash.com/photo-1501555088652-021faa106b9b?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")||a[0]?.includes("food")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=4; if(a[5]?.includes("mountains")||a[5]?.includes("countryside")) s+=5; if(a[6]?.includes("nothing")||a[6]?.includes("wander")||a[6]?.includes("absorb")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=3; return s; },
    intro: "The Eje Cafetero — the Coffee Axis — is the Andean heartland of Colombian coffee production, centered on the departments of Caldas, Quindio, and Risaralda. The landscape is extraordinary: steep Andean ridges covered in coffee and banana, colorful colonial towns (pueblos patrimonios) with painted facades and elaborate balconies, and the Valle del Cocora — a cloud forest valley with the wax palm, Colombia's national tree, growing to 60 metres and visible through the mist as you hike up. The hacienda coffee farms offer the most direct experience of how the coffee you drink is grown, processed, and prepared — from the red cherry on the tree to the cup in your hand in one continuous operation.",
    highlights: [
      { label: "Valle del Cocora hike", text: "The 10km circular hike from Salento through the Valle del Cocora — the most photographed landscape in Colombia. The wax palms emerge from the cloud forest at 2,400 metres, 60 metres tall, impossibly thin. The hike takes 4-5 hours and passes through the cloud forest to a hummingbird sanctuary before descending back through the palms." },
      { label: "Coffee hacienda tour", text: "The haciendas around Salento and Filandia offer farm-to-cup tours — walk the coffee rows at harvest (October-February), learn to identify ripe cherries, watch the wet milling and drying process, cup the finished coffee. Hacienda Venecia (near Manizales) and Finca El Ocaso (near Salento) are the most complete experiences." },
      { label: "Salento", text: "The most visited pueblo patrimonio in the coffee region — a hilltop colonial town with painted balconies, a main street lined with coffee shops and restaurants, and the Valle del Cocora trailhead 15 minutes away by jeep. The Sunday market and the evening on the main square are the two reasons to arrive on a Saturday." },
      { label: "Filandia and Buenavista", text: "The quieter alternatives to Salento — Filandia has the same painted colonial architecture with a fraction of the visitors, and Buenavista is the craft town of the region (basket weaving, leather, ceramics). The view from the Filandia mirador over the coffee ridges is the best in the Eje Cafetero." },
    ],
    eat: [
      { name: "Brunch (Salento)", desc: "The best restaurant in Salento — Colombian ingredients treated with care. The trucha (fresh trout from the cold Andean streams), the bandeja paisa (the full traditional Antioquian plate), the freshly ground coffee. Arrive early for a window seat." },
      { name: "El Balcon (Salento)", desc: "On the main plaza, balcony overlooking the square — simple Colombian food, the best people-watching in town, the most reliable cup of coffee in Salento. The order is the fresh juice, the arepa, and the tinto." },
      { name: "Hacienda farm lunch", desc: "Most hacienda coffee tours include a traditional finca lunch — red beans, white rice, chicharron, avocado, fresh juice, and coffee from the farm. The most Colombian meal in the region." },
    ],
    stay: [
      { name: "Hacienda Venecia (near Manizales)", tier: "High end", desc: "A working coffee hacienda with guestrooms — wake to the sound of the coffee farm, the most complete immersion in coffee culture available in Colombia. The farm tour and breakfast are included." },
      { name: "Finca El Paraiso (near Salento)", tier: "Mid range", desc: "A family finca on the hillside above Salento — rooms with Valle del Cocora views, a working coffee farm, the family cooking breakfast on a wood fire." },
      { name: "Plantation House (Salento)", tier: "Good value", desc: "The most social hostel in the coffee region — run by a Colombian family, guided farm visits available, the best base for meeting other travelers in Salento." },
    ],
    logistics: [
      { q: "Getting there", a: "Fly into Pereira (PEI) or Armenia (AXM) — both have connections from Bogota (1hr) and Medellin (30min). From Pereira: taxi to Salento (1.5hrs, COP 60,000). From Medellin by road: 3.5 hours through spectacular Andean scenery." },
      { q: "When to go", a: "Year-round — the coffee region is green in all seasons. October-February is the main harvest season — the haciendas are at their most active, the coffee cherries bright red on the trees. March-May is the mitaca (smaller) harvest. December-January is peak tourist season — book accommodation ahead." },
      { q: "How long", a: "Two nights minimum. Day one: arrive Salento, main square, coffee shop tour. Day two: Valle del Cocora hike (full day). Day three: hacienda coffee farm tour, depart for Medellin or Cartagena." },
    ],
  },
  {
    name: "Bogotá", country: "colombia", tag: "La Candelaria · Gold Museum · Altitude",
    hook: "A capital city at 2,600 metres that takes 24 hours to stop making you breathless. The Gold Museum has 55,000 pre-Columbian objects. The street art is the best in South America.",
    img: "https://images.unsplash.com/photo-1562516155-e0c1ee44059b?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=4; if(a[3]?.includes("explorer")||a[3]?.includes("local")) s+=3; if(a[5]?.includes("cities")) s+=5; if(a[6]?.includes("absorb")||a[6]?.includes("wander")||a[6]?.includes("eat")) s+=4; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=3; if(a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=3; return s; },
    intro: "Bogotá sits on a high Andean plateau at 2,600 metres — the third highest capital city in the world. The altitude hits immediately and the city's energy compounds it: 8 million people, the best museum in South America (the Gold Museum, with 55,000 pre-Columbian gold and ceramic objects), a street art scene centered on La Candelaria that has produced some of the most significant murals in the world, a food revolution driven by chefs who trained in Europe and returned to cook Colombian ingredients, and the Ciclovía — every Sunday 120km of city roads are closed to cars and given to cyclists and pedestrians. Bogotá is the gateway to Colombia and most visitors spend too little time here.",
    highlights: [
      { label: "Museo del Oro (Gold Museum)", text: "The best museum in South America — 55,000 gold and pre-Columbian objects from the cultures that preceded the Spanish conquest. The Muisca raft (the solid gold ritual raft that gave rise to the El Dorado legend), the emerald collection, the ceramic anthropomorphic vessels. Free on Sundays. Allow three hours minimum." },
      { label: "La Candelaria street art", text: "The historic colonial center has become the canvas for the most significant street art in South America — the work of Stinkfish, DJ Lu, Lesivo, and dozens of other Colombian and international artists covering entire building faces. The Bogotá Graffiti Tour (free, tip-based) runs twice daily and covers the political and artistic history of each work." },
      { label: "Monserrate", text: "The 3,152 metre peak above Bogotá with a white church at the summit — cable car or funicular (COP 27,000 return) or a 90-minute hike up the steep path (free, with crowds on weekends). The view over the city spreading across the Sabana de Bogotá is the best urban panorama in South America." },
      { label: "Usaquén Sunday market", text: "The most pleasant Sunday in Bogotá — a colonial village neighborhood absorbed by the city with a weekly antique and craft market in the square, brunch restaurants filling the old houses, the Ciclovía riders passing outside. The best of Bogotá without the intensity of the center." },
    ],
    eat: [
      { name: "Leo (Zona Rosa)", desc: "Chef Leonor Espinosa's flagship — the most celebrated Colombian chef in the world, cooking with ingredients sourced from indigenous and Afro-Colombian communities across the country. The tasting menu is the most important meal in Colombia." },
      { name: "Masa (Chapinero)", desc: "The restaurant that redefined Colombian baking — sourdough made with native Colombian grains, sandwiches that use local charcuterie, the best coffee in Bogotá. The most visited brunch in the city." },
      { name: "Andres Carne de Res (Chia)", desc: "30 minutes from Bogotá — the most famous restaurant in Colombia, a 3,500-person capacity palace of Colombian excess, open for lunch on weekends only. Not fine dining but an experience unlike any other restaurant in the world." },
    ],
    stay: [
      { name: "Casa Medina (Chapinero)", tier: "High end", desc: "A 1946 Spanish colonial mansion converted into a luxury hotel — the most elegant small hotel in Bogotá. The afternoon tea in the salon, the bar with Colombian whisky, the garden courtyard." },
      { name: "Click Clack Hotel (Zona Rosa)", tier: "Mid range", desc: "A design hotel in the Zona Rosa with a rooftop bar and one of the best views of the Andes from a hotel pool in Bogotá." },
      { name: "Selina Bogota (La Candelaria)", tier: "Good value", desc: "In the heart of the colonial center — the street art outside the door, the Gold Museum walkable, a rooftop with the Monserrate above. The best budget base for a first visit to Bogotá." },
    ],
    logistics: [
      { q: "Getting there", a: "Fly into El Dorado International Airport (BOG) — the main hub for Colombia. Direct from Miami (4hrs), New York (5.5hrs), Madrid (10hrs), London (11hrs). The airport is 45 minutes from La Candelaria and Chapinero by taxi (COP 40,000-60,000)." },
      { q: "Altitude", a: "Bogotá is at 2,600 metres — altitude sickness (headache, shortness of breath, fatigue) affects some visitors for the first 24-48 hours. Drink water constantly, avoid alcohol on the first night, eat lightly. Most people acclimatize within a day." },
      { q: "Safety", a: "La Candelaria, Chapinero, Zona Rosa, and Usaquén are all navigable for tourists with standard precautions. Don't walk alone late at night in La Candelaria. Use Cabify or InDriver apps rather than hailing taxis on the street. Bogotá is significantly safer than its reputation suggests." },
      { q: "How long", a: "Two nights as a gateway. Day one: Gold Museum, La Candelaria street art tour, Monserrate at sunset. Day two: Usaquén Sunday market (if Sunday), Leo dinner. Bogotá connects to everywhere else in Colombia — it works as the first or last stop on a Colombia itinerary." },
    ],
  },
  {
    name: "Tayrona & The Caribbean Coast", country: "colombia", tag: "Lost City · Jungle · Caribbean",
    hook: "A jungle that drops directly into the Caribbean. A 650-year-old lost city that required a 4-day trek to reach. The most biodiverse national park in Colombia.",
    img: "https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")) s+=5; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=5; if(a[5]?.includes("coast")||a[5]?.includes("mountains")||a[5]?.includes("countryside")) s+=4; if(a[6]?.includes("physical")||a[6]?.includes("explore")) s+=5; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; return s; },
    intro: "Tayrona National Park is a 150 square kilometre protected area on the Caribbean coast where the Sierra Nevada de Santa Marta mountains — the highest coastal mountain range in the world, rising from sea level to 5,700 metres in 42km — drop directly into the Caribbean. The beaches inside the park (Cabo San Juan, La Piscina, Arrecifes) are the most beautiful in Colombia: white sand, jungle to the water's edge, no roads. The Ciudad Perdida (Lost City) is a 650-year-old Tairona ceremonial site in the Sierra Nevada, reached by a 4-day jungle trek — pre-dating Machu Picchu by 650 years and known to the outside world only since 1972.",
    highlights: [
      { label: "Cabo San Juan", text: "The most beautiful beach in Tayrona National Park — a white sand bay enclosed by jungle headlands, accessible only on foot (2 hours from the park entrance) or by boat. The hammock camp on the headland between the two beaches is the most famous budget stay in Colombia." },
      { label: "Ciudad Perdida trek", text: "The 4-day return trek to the Lost City — 46km through jungle and river crossings, sleeping in open-sided camps, climbing 1,200 stone steps to the Tairona ceremonial terraces at 1,300 metres. All tours are operated by licensed guides from Santa Marta. The most physically demanding and rewarding trek in Colombia." },
      { label: "Palomino", text: "A small town east of Tayrona — a river that flows cold from the Sierra Nevada mountains into the warm Caribbean, tubing available. The most relaxed beach town on the Caribbean coast, not yet overrun. Black sand beach, hammock accommodation, the best sunset on the coast." },
      { label: "Minca", text: "A mountain village in the Sierra Nevada above Santa Marta — coffee farms, endemic birds (the Sierra Nevada is one of the most biodiverse areas on earth), waterfalls, and a temperature that makes it a refuge from the Caribbean heat. 45 minutes from Santa Marta by moto-taxi." },
    ],
    eat: [
      { name: "Ouzo (Santa Marta)", desc: "The best restaurant in Santa Marta — Mediterranean-Caribbean fusion using local fish and produce. The grilled snapper with Caribbean spices and the seafood rice are the permanent orders." },
      { name: "Tayrona park camps", desc: "The food at the Tayrona camps (Cabo San Juan, El Paraiso) is simple but sufficient — fried fish, rice and beans, fresh juice, coconut water from the palms. The Cabo San Juan hammock camp also has the best sunset bar in the park." },
      { name: "Minca coffee farms", desc: "Several coffee farms above Minca serve farm-to-cup coffee in their gardens — the coffee from the Sierra Nevada foothills (grown at 900-1,200 metres) is lighter and fruitier than Eje Cafetero coffee. The breakfast here (eggs, arepa, fresh juice, farm coffee) is the best in the region." },
    ],
    stay: [
      { name: "Teyuna Lodge (Tayrona)", tier: "High end", desc: "The only proper hotel inside Tayrona National Park — eco-bungalows in the jungle, a 10-minute walk to Arrecifes beach, a swimming pool fed by a mountain stream." },
      { name: "Casa del Pez (Palomino)", tier: "Mid range", desc: "A boutique hotel on the Palomino beach — the most designed accommodation on the Caribbean coast outside Cartagena. The river-to-sea tubing trip is organized from here." },
      { name: "Cabo San Juan hammocks (Tayrona)", tier: "Good value", desc: "The hammock camp on the headland between the two Cabo San Juan beaches — the most famous budget sleep in Colombia, entirely worth the hype. Book ahead in December-January." },
    ],
    logistics: [
      { q: "Getting there", a: "Fly into Simon Bolivar Airport, Santa Marta (SMR) from Bogota (1.5hrs) or Medellin (1.5hrs). Santa Marta is the gateway. Tayrona park entrance is 34km from Santa Marta (45 minutes by taxi or bus). Ciudad Perdida tours depart from Santa Marta — all licensed operators are based there." },
      { q: "Tayrona park rules", a: "The park closes in February for environmental recovery. Camping requires booking through the Aviatur concessionaire. No cars inside the park — everything is on foot or by horse. The Arrecifes beach has a dangerous current — swim at La Piscina and Cabo San Juan only. Bring cash — no ATMs inside the park." },
      { q: "When to go", a: "December-April is the dry season — the trails are dry, the water is clearest, the park is most crowded. May-November has more rain but fewer tourists. Avoid the February park closure." },
      { q: "How long", a: "Three nights minimum. Two nights inside the park (Cabo San Juan). One night Santa Marta (Minca day trip). Add four days for the Ciudad Perdida trek if fitness allows — it is worth the physical effort." },
    ],
  },
];

// ─── VIETNAM REGIONS ──────────────────────────────────────────────────────────
const vietnamRegions = [
  {
    name: "Hanoi", country: "vietnam", tag: "Old Quarter · Pho · Street Life",
    hook: "A city that has been continuously inhabited for 1,000 years and looks like it. The traffic does not stop for anyone. The pho is the best in the world.",
    img: "https://images.unsplash.com/photo-1509030450996-dd1a26dda07a?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")) s+=5; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=4; if(a[5]?.includes("cities")) s+=5; if(a[6]?.includes("eat")||a[6]?.includes("absorb")||a[6]?.includes("wander")) s+=5; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; return s; },
    intro: "Hanoi is a city of 8 million people and 6 million motorbikes — a place where the Old Quarter's 36 ancient guild streets are so intact that you can still find the street that sold paper, the street that sold tin, the street that sold bamboo, all operating essentially as they have for 600 years. The French colonial architecture (the Opera House, the Presidential Palace, the covered market halls) overlays the Vietnamese on top of the Chinese on top of the ancient Cham. The food is the reason the rest comes second: pho bo (beef noodle soup, eaten at 6am on a plastic stool on the pavement) is the breakfast, bun cha (grilled pork with noodles in broth) is the lunch, and bia hoi (fresh draft beer, brewed daily, 20 cents a glass) is the evening.",
    highlights: [
      { label: "Old Quarter at dawn", text: "Walk the Old Quarter before 7am — before the motorbikes, before the tourists, when the streets belong to the people who live here. The incense smoke from the morning temple offerings, the pho vendors setting up their stools, the flower sellers cycling in from the countryside with bicycles stacked three metres high with blooms. The most cinematic hour in Hanoi." },
      { label: "Pho and street food culture", text: "Hanoi pho (northern style — clear, deep beef broth, minimal garnish, no bean sprouts or basil, the broth is the point) at Pho Gia Truyen on Bat Dan Street (queue from 6am, closes when the pot runs out). Bun cha at Bun Cha Huong Lien (where Obama ate with Anthony Bourdain in 2016). Banh mi at any cart outside the covered market. The best food in Vietnam costs almost nothing." },
      { label: "Hoan Kiem Lake and the Temple of the Jade Mountain", text: "The lake in the center of Hanoi with the 15th century Ngoc Son Temple on a small island connected by a red bridge. The giant softshell turtles that once lived in the lake are gone (the last one died in 2016) but the legend — that a turtle appeared to return a magic sword to a king — is the founding myth of Hanoi. Walk the lake at dusk when the city comes outside." },
      { label: "Train Street and the Old Quarter cafes", text: "The narrow street where a working railway line runs between residential buildings so close that residents fold their balconies in when the train passes. The cafes on the upper floors looking over the track. The street was briefly closed to tourists and has reopened — go early morning before the crowd arrives." },
      { label: "Ho Chi Minh Mausoleum complex", text: "The Soviet-built mausoleum containing Ho Chi Minh's preserved body — a morning vigil that moves quickly and is quietly extraordinary. The surrounding complex includes the Presidential Palace (where Ho Chi Minh refused to live), his simple house on stilts above the carp pond, and one of the most significant museums in Vietnam." },
    ],
    eat: [
      { name: "Pho Gia Truyen (Bat Dan Street)", desc: "The most famous pho in Hanoi — the broth has been simmering since 1955. Opens at 6am, closes when the pot runs out (usually by 10am). Queue outside, eat at the communal table, leave quickly. The definitive pho bo experience." },
      { name: "Bun Cha Huong Lien (Dong Da)", desc: "The bun cha restaurant where Obama and Bourdain ate in 2016 — the table is now preserved as a monument. The bun cha is exactly what it should be: grilled pork patties in a sweet-sour broth with vermicelli noodles and herbs. COP 50,000 (USD 2)." },
      { name: "Cha Ca Thang Long (Old Quarter)", desc: "The most Hanoi-specific dish: cha ca (turmeric and dill fish, cooked at the table in a sizzling pan, eaten with rice noodles, peanuts, and shrimp paste). The dish has its own street named after it. This restaurant does the definitive version." },
      { name: "Bia Hoi corner (Hoan Kiem)", desc: "The intersection of Luong Ngoc Quyen and Ta Hien Streets at dusk — hundreds of plastic stools, bia hoi (fresh daily-brewed lager at 20 cents a glass), street food vendors, the entire city seeming to compress into one corner. The best evening in Hanoi." },
    ],
    stay: [
      { name: "Sofitel Legend Metropole (Hoan Kiem)", tier: "High end", desc: "A French colonial hotel that opened in 1901 — the most historically significant hotel in Vietnam. Graham Greene wrote The Quiet American here. The wartime bunker under the hotel is open for tours. The best address in Hanoi." },
      { name: "Hanoi La Siesta Hotel (Old Quarter)", tier: "Mid range", desc: "A well-run boutique hotel in the heart of the Old Quarter — the best mid-range location in Hanoi, small spa, roof terrace with Old Quarter views." },
      { name: "Hanoi Backpacker Hostel (Old Quarter)", tier: "Good value", desc: "The social center of budget Hanoi — well run, private rooms available, the rooftop bar is a genuine gathering point. The best base for independent exploration of the Old Quarter." },
    ],
    logistics: [
      { q: "When to go", a: "October-April is the best season — cool and dry (Hanoi winters can be surprisingly cold, 15-18C in January, bring a layer). May-September is hot (35C+) and the rainy season. The Old Quarter floods in heavy rain. October and November are the sweet spot: pleasant temperatures, low tourist numbers." },
      { q: "Getting there", a: "Fly into Noi Bai International Airport (HAN) — direct from London (11hrs on Vietnam Airlines), Bangkok (2hrs), Singapore (3hrs), Hong Kong (2.5hrs), Seoul (4hrs). The airport is 45 minutes from the Old Quarter by taxi (VND 350,000-450,000) or the express bus (VND 40,000)." },
      { q: "Getting around", a: "The Old Quarter is walkable. Grab (the Southeast Asian Uber) works throughout the city. Motorbike taxis (xe om) are cheaper and faster through traffic. Cycling is possible in the Old Quarter in the early morning. Avoid the city bus system." },
      { q: "How long", a: "Three nights. Day one: Old Quarter dawn walk, Hoan Kiem Lake, pho breakfast at Bat Dan. Day two: Ho Chi Minh complex, Temple of Literature, bia hoi evening. Day three: day trip to Ha Long Bay or depart for Hoi An." },
    ],
  },
  {
    name: "Ha Long Bay & the North", country: "vietnam", tag: "Limestone Karsts · Junk Boats · Ha Giang",
    hook: "2,000 limestone islands rising from emerald water. The overnight junk boat is one of the great travel experiences in Asia. The Ha Giang Loop in the far north is the motorcycle road that changes people.",
    img: "https://images.unsplash.com/photo-1528360983277-13d401cdc186?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("adventure")||a[0]?.includes("escape")||a[0]?.includes("beauty")) s+=4; if(a[3]?.includes("explorer")) s+=5; if(a[4]?.includes("wild")||a[4]?.includes("bold")) s+=5; if(a[5]?.includes("coast")||a[5]?.includes("mountains")) s+=5; if(a[6]?.includes("physical")||a[6]?.includes("explore")||a[6]?.includes("nothing")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=4; return s; },
    intro: "Ha Long Bay is a UNESCO World Heritage Site in the Gulf of Tonkin — 2,000 limestone karst islands rising from emerald water in configurations that look like something out of a Chinese scroll painting. The bay is most experienced from an overnight junk boat cruise that anchors among the islands, kayaks into sea caves, and wakes up in silence surrounded by the karsts. Bai Tu Long Bay (adjacent to Ha Long but a third of the visitors) and Lan Ha Bay (near Cat Ba Island) offer the same landscape with more solitude. The Ha Giang province in the far north — a 10-hour drive from Hanoi — is where the motorcycle loop through the Dong Van Karst Plateau (a UNESCO Global Geopark) has become one of the defining adventure travel experiences in Southeast Asia.",
    highlights: [
      { label: "Ha Long Bay overnight cruise", text: "The 2-night junk boat cruise is the right call — one night is not enough to reach the quieter sections of the bay away from the day-trip boats. The sunrise from the boat deck at 5:30am, the kayaking into dark sea caves where the ceiling drips and bats move overhead, the squid fishing off the stern at midnight. Choose a boat carefully — the quality range is extreme. Indochina Junk and Paradise Cruises are the benchmark operators." },
      { label: "Bai Tu Long Bay", text: "The northern extension of Ha Long Bay with a third of the visitors — the same karst landscape with more solitude. Fewer day-trip boats, more wildlife, overnight cruises on smaller, more intimate vessels. The island villages and floating fishing communities that have largely disappeared from the Ha Long tourist circuit still exist here." },
      { label: "Ha Giang Loop", text: "A 3-4 day motorcycle circuit through the Dong Van Karst Plateau in the far north near the Chinese border. The Nho Que River valley (the turquoise river in the limestone gorge seen on every Vietnam travel photo), the Lung Cu flag tower at the northernmost point of Vietnam, the Dong Van ancient town. Rent a motorbike or hire an Easy Rider guide in Ha Giang town. The most physically demanding and visually extraordinary road in Vietnam." },
      { label: "Ninh Binh (inland Ha Long)", text: "150km south of Hanoi — limestone karsts but inland, rising from rice paddies and rivers. The Trang An boat tour through cave systems and valley scenery, the Bai Dinh pagoda complex (the largest Buddhist complex in Southeast Asia), the ancient Vietnamese capital at Hoa Lu. An extraordinary day trip or overnight from Hanoi." },
    ],
    eat: [
      { name: "Boat dinner (Ha Long overnight)", text: "The onboard dinner on the overnight cruise is the meal — fresh seafood pulled from the bay, grilled squid, steamed clams, fish cooked simply with ginger. The quality depends entirely on the operator. Paradise Cruises and Indochina Junk both have chefs who take it seriously." },
      { name: "Ninh Binh local food (com chay)", desc: "Ninh Binh's specific dish is com chay — burnt rice scraped from the bottom of the pot, deep-fried until crispy, served with goat meat or pork and a fermented shrimp dipping sauce. Found only in Ninh Binh province. The street restaurants around the Hoa Lu ancient capital are the best." },
    ],
    stay: [
      { name: "Paradise Elegance Cruise (Ha Long)", tier: "High end", desc: "The benchmark overnight cruise operator in Ha Long Bay — the most careful balance of comfort and genuine bay experience. The cooking class on the sundeck and the kayaking program are the best in the bay." },
      { name: "Cat Ba Island hostels", tier: "Good value", desc: "Stay on Cat Ba Island and do day trips into Lan Ha Bay by local boat — significantly cheaper than the overnight cruises and gives you a base with actual Vietnamese island life rather than a floating hotel." },
    ],
    logistics: [
      { q: "Getting there", a: "Ha Long is 180km from Hanoi (3.5 hours by road). Most overnight cruises include round-trip transfer from Hanoi hotels. Cat Ba Island is reached by ferry from Ha Long City or direct hydrofoil from Haiphong. Ha Giang is 10 hours from Hanoi by overnight bus or 1.5 hours by flight to Tuyen Quang." },
      { q: "Choosing a cruise", a: "The Ha Long cruise market has hundreds of operators at wildly different quality levels. Budget junks (under USD 100/night) are generally disappointing — overcrowded, poor food, no real bay access. Mid-range (USD 150-250/night) includes operators like Indochina Junk and Peony Cruises. Premium (USD 300+/night): Paradise Cruises. The extra cost buys genuine solitude in the bay." },
      { q: "When to go", a: "March-May and September-November for calm seas and decent visibility. June-August is hot and the bay can be foggy. December-February is cold (15C) but the bay is often mist-covered which creates extraordinary atmosphere on the boat." },
    ],
  },
  {
    name: "Hoi An", country: "vietnam", tag: "Ancient Town · Lanterns · Tailors",
    hook: "A 15th century trading port that survived every war intact because everyone agreed it was too beautiful to bomb. The lanterns come on at dusk and the entire town glows.",
    img: "https://images.unsplash.com/photo-1540611025311-01df3cef54b5?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("beauty")||a[0]?.includes("food")) s+=4; if(a[3]?.includes("balanced")||a[3]?.includes("local")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("cities")) s+=4; if(a[6]?.includes("wander")||a[6]?.includes("eat")||a[6]?.includes("absorb")||a[6]?.includes("nothing")) s+=4; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=3; return s; },
    intro: "Hoi An is a UNESCO World Heritage ancient town on the Thu Bon River in central Vietnam — a 15th century trading port where Japanese merchants, Chinese traders, and Vietnamese artisans all built their quarter and then blended into each other over 400 years. The result is an architecture that exists nowhere else: Chinese assembly halls, Japanese covered bridges, Vietnamese tube houses, French colonial overlays, all in extraordinary preservation. The town survived the American War because both sides agreed it was too historically significant to bomb. At dusk the electric lights are switched off and the silk lanterns light up — the most romantic hour in Southeast Asia.",
    highlights: [
      { label: "Ancient town at dusk", text: "Walk the ancient town from the Japanese Covered Bridge to the Phung Hung Old House as the sun goes down. The silk lanterns light up, the river fills with paper lanterns released by tourists, and the streets — which have been this way for 500 years — fill with the specific light that every photographer comes to Hoi An for. The Full Moon Lantern Festival (14th of each lunar month) amplifies this tenfold." },
      { label: "White Rose dumplings and Cao Lau", text: "Hoi An has its own dishes that exist nowhere else in Vietnam. White Rose (banh bao vac) — translucent steamed shrimp dumplings, made exclusively by one family who supplies all the restaurants in town. Cao Lau — thick rice noodles with pork, herbs, and crispy croutons, prepared with water from a specific ancient well. Eat both at Morning Glory restaurant." },
      { label: "An Bang Beach", text: "4km from the ancient town — the most low-key beach on the central Vietnam coast. The beach restaurants serve fresh seafood directly from the boats, the water is warm and relatively calm, and the development is minimal compared to Da Nang. Rent a bicycle from the ancient town and cycle out through the rice paddies." },
      { label: "Tailors and the market", text: "Hoi An has been a tailoring town since the 15th century — there are 400 tailors in a town of 120,000 people. Custom suits in 24-48 hours at a fraction of Western prices. The Hoi An market in the morning (5am-9am) has the best fresh ingredients in central Vietnam: local herbs, river fish, the rice paper used for everything. A cooking class that starts with the market and ends at the table is the most complete Hoi An experience." },
    ],
    eat: [
      { name: "Morning Glory (Ancient Town)", desc: "The restaurant that put Hoi An's food culture on the map — chef Vy's menu covers every Hoi An-specific dish. The white rose dumplings, the cao lau, the banh mi from the original family recipe. The most important meal in Hoi An." },
      { name: "The Streets (Ancient Town)", desc: "A social enterprise restaurant training disadvantaged youth — the cooking is some of the most refined Vietnamese food in central Vietnam. The set menus change seasonally. Book ahead." },
      { name: "Banh Mi Phuong", desc: "The banh mi that Anthony Bourdain called the best in the world — a specific Hoi An-style banh mi with more filling and a different bread than the Hanoi or Saigon versions. The queue starts at 7am." },
    ],
    stay: [
      { name: "Anantara Hoi An Resort", tier: "High end", desc: "On the Thu Bon River with the ancient town visible across the water — the riverside pool, the cooking school using the morning market produce, the best location of any luxury hotel in Hoi An." },
      { name: "Vinh Hung Emerald Resort (An Bang Beach)", tier: "Mid range", desc: "The best mid-range option at An Bang Beach — pool, 5 minutes to the beach, bicycle hire for the ancient town ride. The most relaxed location in Hoi An." },
      { name: "Hoi An Backpackers Hostel", tier: "Good value", desc: "In the ancient town buffer zone — close enough to walk, far enough for a quiet night. Pool, the free bicycle hire, the best budget base in central Vietnam." },
    ],
    logistics: [
      { q: "Getting there", a: "Fly into Da Nang Airport (DAD) — 30 minutes from Hoi An by taxi (VND 250,000-350,000). Da Nang has direct flights from Hanoi (1hr), Ho Chi Minh City (1hr), Bangkok (1.5hrs), Singapore (2hrs). The overnight train from Hanoi to Da Nang (15hrs) passes through the Hai Van Pass — one of the great train journeys in Southeast Asia." },
      { q: "When to go", a: "February-August for the best weather. September-November is typhoon season — the town has flooded significantly in recent years (2016, 2020). December-January is the cooler dry season — less beach weather but the ancient town is at its most atmospheric. The Full Moon Lantern Festival is worth timing for." },
      { q: "How long", a: "Three nights minimum. Day one: ancient town exploration, Morning Glory dinner, lanterns at dusk. Day two: cooking class (market to table), An Bang Beach afternoon. Day three: bicycle to the My Son Hindu temple ruins (10km, the best day trip from Hoi An). Hoi An connects easily with Da Nang and is the gateway to Ho Chi Minh City." },
    ],
  },
  {
    name: "Ho Chi Minh City (Saigon)", country: "vietnam", tag: "Energy · War History · Rooftop Bars",
    hook: "The city that doesn't stop. 10 million people and 9 million motorbikes. The war ended 50 years ago and the city has been building upward ever since.",
    img: "https://images.unsplash.com/photo-1583417319070-4a69db38a482?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("culture")||a[0]?.includes("food")||a[0]?.includes("adventure")) s+=4; if(a[3]?.includes("local")||a[3]?.includes("explorer")) s+=4; if(a[5]?.includes("cities")) s+=5; if(a[6]?.includes("eat")||a[6]?.includes("absorb")||a[6]?.includes("wander")) s+=5; if(a[8]?.includes("people")||a[8]?.includes("feel")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")) s+=2; return s; },
    intro: "Ho Chi Minh City — still called Saigon by everyone who lives here — is the economic capital of Vietnam and the most kinetic city in Southeast Asia. 10 million people, 9 million motorbikes, a skyline that has tripled in height since 2010, and a street food culture that operates 24 hours a day across the city's 19 districts. The War Remnants Museum is the most confrontational museum in Asia — an unflinching account of the American War from the Vietnamese perspective. The Ben Thanh Market area, District 1, and the Bui Vien backpacker street give you three completely different cities within walking distance. The rooftop bar scene is the best in Southeast Asia.",
    highlights: [
      { label: "War Remnants Museum", text: "The most important museum in Vietnam — American tanks, aircraft, and weapons in the courtyard outside; inside, photographic documentation of the conflict from the Vietnamese perspective. The photographs by Larry Burrows, Nick Ut, and Eddie Adams are here alongside images that never left Vietnam. The most emotionally significant 3 hours in Ho Chi Minh City." },
      { label: "Cho Lon (Chinatown)", text: "The largest Chinatown in Southeast Asia in District 5 — the Binh Tay Market (the real wholesale market where Cho Ben Thanh sources its stock), the Thien Hau Temple with its incense coils hanging from the ceiling, the medicinal herb stalls, the banh mi cart outside the market at dawn. The most sensory neighborhood in Saigon." },
      { label: "Mekong Delta day trip", text: "The river system that feeds Vietnam — the boat trip through the delta canals (Ben Tre province, 70km from the city) passes through coconut palm forests, floating markets, and rice paddies that have been farmed the same way for 2,000 years. The best one-day escape from the city's intensity." },
      { label: "Bui Vien and the rooftop bars", text: "The Bui Vien walking street is the most intense street in Asia after dark — 200 metres of neon, beer, and music. One block east, the rooftop bars of the Bitexco Tower and the Chill Skybar look over the entire city. The contrast between street level and rooftop captures Saigon's character completely." },
    ],
    eat: [
      { name: "Banh Mi 37 Nguyen Trai", desc: "The definitive Saigon banh mi — a specific, completely different bread and filling combination from the Hoi An version. Open from 6am. The paté, the cold cuts, the fresh herbs, the chili. Queue, eat standing up, move on." },
      { name: "Cuc Gach Quan (Binh Thanh)", desc: "A French colonial villa converted into the most atmospheric restaurant in Saigon — traditional Vietnamese home cooking using seasonal produce, served in a crumbling garden setting. The most complete Vietnamese meal in the city." },
      { name: "Nha Hang Ngon (District 1)", desc: "A French villa with 20+ street food stalls in the courtyard — every regional Vietnamese dish cooked by specialists. The most efficient way to eat across the whole country in one sitting." },
      { name: "Pho Hoa Pasteur (District 3)", desc: "The most famous pho in Saigon — open since 1960, the broth richer and darker than Hanoi pho, the garnish table loaded with bean sprouts and basil. The southern pho vs northern pho debate is real. This is the southern benchmark." },
    ],
    stay: [
      { name: "Park Hyatt Saigon (District 1)", tier: "High end", desc: "The most elegant hotel in Ho Chi Minh City — on Lam Son Square facing the Opera House, the best pool in the city center, a breakfast that covers every Vietnamese regional morning dish." },
      { name: "The Reverie Saigon (District 1)", tier: "High end", desc: "The most visually extravagant hotel in Vietnam — Italian marble, gold fixtures, a design that is simultaneously overwhelming and extraordinary. The pool on the 26th floor." },
      { name: "The Common Room Project (District 3)", tier: "Mid range", desc: "A design hotel in District 3 — away from the tourist center, more local neighborhood, a roof terrace and the best breakfast in the mid-range category." },
      { name: "Chez Mimosa (District 1)", tier: "Good value", desc: "A French colonial guesthouse on a quiet street in District 1 — the most charming budget stay in central Saigon. The roof terrace and the coffee are the reasons." },
    ],
    logistics: [
      { q: "When to go", a: "December-April is the dry season — the best weather, 25-30C, low humidity. May-November is the wet season — afternoon thunderstorms, high humidity, but the city is less crowded and accommodation is cheaper. The rain usually lasts 2 hours and then stops." },
      { q: "Getting there", a: "Fly into Tan Son Nhat International Airport (SGN) — direct from London (12hrs), Bangkok (1.5hrs), Singapore (2hrs), Hong Kong (2.5hrs), Sydney (8hrs). The airport is 20 minutes from District 1 by Grab taxi (VND 100,000-150,000)." },
      { q: "Getting around", a: "Grab is the essential app — motorcycle taxis are faster and cheaper than cars through traffic (VND 30,000-60,000 for most District 1 journeys). The city is too spread out and traffic too intense for walking between neighborhoods. Do not rent a motorbike without significant experience." },
      { q: "How long", a: "Two to three nights. Day one: War Remnants Museum, Ben Thanh market, rooftop bar at sunset. Day two: Cho Lon Chinatown, Mekong Delta day trip. Day three: Cu Chi Tunnels (the Viet Cong tunnel network 70km from the city — a full morning) or depart." },
    ],
  },
  {
    name: "Mekong Delta & Phu Quoc", country: "vietnam", tag: "River Life · Island · Pepper Farms",
    hook: "The river that feeds half of Southeast Asia. An island off the coast of Cambodia that was a secret until 10 years ago. Still worth going despite what happened next.",
    img: "https://images.unsplash.com/photo-1559592413-7cbb6490d877?w=800&q=80",
    match: (a) => { let s=0; if(a[0]?.includes("escape")||a[0]?.includes("beauty")||a[0]?.includes("adventure")) s+=3; if(a[3]?.includes("explorer")||a[3]?.includes("balanced")) s+=3; if(a[5]?.includes("coast")||a[5]?.includes("countryside")) s+=5; if(a[6]?.includes("nothing")||a[6]?.includes("wander")||a[6]?.includes("spontaneous")) s+=4; if(a[9]?.includes("tourist")||a[9]?.includes("generic")||a[9]?.includes("crowds")) s+=3; if(a[8]?.includes("feel")||a[8]?.includes("none")) s+=3; return s; },
    intro: "The Mekong Delta is the vast river system in southern Vietnam where the Mekong splits into nine tributaries before reaching the South China Sea — a landscape of coconut palm forests, water hyacinth, rice paddies, floating markets, and canal villages where life is conducted almost entirely by boat. The floating markets at Cai Rang and Phong Dien (Ben Tre province) operate at dawn, vendors lashing their speciality produce to a pole so buyers can identify them from a distance. Phu Quoc is an island off the southwest coast of Vietnam in the Gulf of Thailand — 40km long, undeveloped forested interior, the white sand beaches of the west coast, and a fish sauce and pepper production tradition that has been running for centuries. The casino resort development of the past decade has changed the north of the island — the south and interior are still extraordinary.",
    highlights: [
      { label: "Cai Rang floating market", text: "The largest floating market in the Mekong Delta — 400+ boats trading wholesale produce at dawn. The boat sellers identify their goods by hanging a sample on a tall pole (a dai hang): pineapples, watermelons, sweet potato. Hire a small boat from Can Tho at 5am. The market winds down by 8am. The most specific Vietnamese experience outside a city." },
      { label: "Ben Tre canal village", text: "The Ben Tre province (70km from Ho Chi Minh City) is the coconut province — coconut candy factories, coconut shell craft workshops, and the canal boat trips through coconut palm forests that look like the Vietnam of 1970. The most atmospheric Mekong Delta experience accessible from the city as a day trip or overnight." },
      { label: "Phu Quoc south coast", text: "The development on Phu Quoc has concentrated in the north (Vinpearl casino resort, night market, tourist strip). The south — An Thoi fishing village, Sao Beach (the most beautiful beach on the island, fine white sand, clear water), the pepper and fish sauce farms of the Duong Dong hinterland — is still the island that travelers discovered 15 years ago." },
      { label: "Phu Quoc fish sauce and pepper farms", text: "Phu Quoc produces the most celebrated fish sauce in Vietnam (nuoc mam Phu Quoc, protected designation of origin) — the fish sauce factories in Duong Dong town are open for visits. The pepper farms in the island's interior grow Kampot-adjacent pepper in red laterite soil. A morning visiting both is the most specific food tourism experience in southern Vietnam." },
    ],
    eat: [
      { name: "Floating market breakfast (Can Tho)", desc: "Buy directly from the boats at Cai Rang — banh mi, fresh fruit, com tam (broken rice with pork), hot coffee in a plastic bag. The most unusual breakfast setting in Vietnam." },
      { name: "Truc Lam (Phu Quoc)", desc: "The best seafood restaurant on Phu Quoc — whole fish grilled over charcoal, river prawns, squid with chili and lemongrass. The restaurant is on the water in An Thoi fishing village. Arrive before sunset." },
      { name: "Pepper farm lunch (Phu Quoc)", desc: "Several pepper farms on Phu Quoc serve lunch using their own produce — dishes built around green, red, and dried pepper. The freshly ground Phu Quoc pepper on a grilled fish is a specific flavor that no restaurant outside the island replicates." },
    ],
    stay: [
      { name: "Mango Bay Resort (Phu Quoc)", tier: "High end", desc: "An eco-resort on a private beach in the north of Phu Quoc — built entirely from natural materials, no air conditioning (designed so none is needed), the most sustainable and design-forward resort on the island." },
      { name: "Idle Hands (Phu Quoc south)", tier: "Mid range", desc: "A small boutique hotel near Sao Beach in the south — the part of Phu Quoc that still feels like an island. Pool, bicycle hire, the fish sauce factory a 10-minute ride away." },
      { name: "Can Tho riverside guesthouses", tier: "Good value", desc: "The guesthouses along the Can Tho riverfront give direct morning access to the boat dock for the floating market. Basic rooms, the Ninh Kieu wharf outside the door." },
    ],
    logistics: [
      { q: "Getting there", a: "Can Tho (Mekong Delta): 3.5 hours from Ho Chi Minh City by road, or 1-hour flight. Phu Quoc: 45-minute flight from Ho Chi Minh City (VND 800,000-2,000,000 on Vietjet or Bamboo), or the ferry from Ha Tien on the mainland (2 hours). The island has an international airport with direct flights from Singapore, Bangkok, and Kuala Lumpur." },
      { q: "Phu Quoc north vs south", a: "Stay south if you want the island experience. Stay north if you want resort amenities. The Vinpearl Casino development has changed the north completely. Sao Beach in the south is genuinely beautiful. The Duong Dong night market (in the north) is worth visiting once — it is specifically designed for tourists but the seafood is fresh." },
      { q: "When to go", a: "November-April is the dry season on Phu Quoc and in the Mekong Delta — the sea is calm, the water clear, the floating markets fully operational. May-October is the wet season — Phu Quoc gets heavy rain (it is one of the wettest places in Vietnam), the sea is rough, and some resorts close." },
      { q: "How long", a: "Two nights Phu Quoc (Sao Beach, fish sauce factory, pepper farm, An Thoi seafood). One night Can Tho (4am departure for Cai Rang floating market, Ben Tre canal afternoon). Return to Ho Chi Minh City." },
    ],
  },
];


function DestinationPage({ dest, onBack, startRegion = 0, openDest }) {
  const [activeRegion, setActiveRegion] = useState(startRegion);
  const [activeTab, setActiveTab] = useState("explore");

  const isPortugal = dest === "portugal";
  const isSpain = dest === "spain";
  const isChile = dest === "chile";
  const isIceland = dest === "iceland";
  const isJapan = dest === "japan";
  const isNewZealand = dest === "newzealand";
  const isOman = dest === "oman";
  const isAustralia = dest === "australia";
  const isGeorgia = dest === "georgia";
  const isColombia = dest === "colombia";
  const isVietnam = dest === "vietnam";
  const regions = isPortugal ? portugalRegions : isSpain ? spainRegions : isChile ? chileRegions : isIceland ? icelandRegions : isJapan ? japanRegions : isNewZealand ? newZealandRegions : isOman ? omanRegions : isAustralia ? australiaRegions : isGeorgia ? georgiaRegions : isColombia ? colombiaRegions : isVietnam ? vietnamRegions : italyRegions;
  const destData = destinations[dest];
  const region = regions[activeRegion];
  const logistics = region.logistics;

  const tabs = [
    { id: "explore", label: "Explore" },
    { id: "eat", label: "Eat & Drink" },
    { id: "stay", label: "Where to Stay" },
    { id: "logistics", label: "How to Do It" },
  ];

  function switchRegion(idx) {
    setActiveRegion(idx);
    if (activeTab !== "logistics") setActiveTab("explore");
  }

  return (
    <div style={{ minHeight: "100vh", background: c.cream, fontFamily: "Georgia, serif" }}>
      {/* NAV */}
      <div style={{ background: c.bark, padding: "1.25rem 3rem", display: "flex", alignItems: "center", justifyContent: "space-between", position: "sticky", top: 0, zIndex: 20 }}>
        <button onClick={onBack} style={{ background: "none", border: "none", color: c.tan, fontFamily: "system-ui, sans-serif", fontSize: "0.7rem", letterSpacing: "0.2em", textTransform: "uppercase", cursor: "pointer" }}>
          ← Back
        </button>
        <div style={{ fontFamily: "system-ui, sans-serif", fontWeight: 200, fontSize: "1.1rem", letterSpacing: "0.3em", textTransform: "uppercase", color: c.cream }}>Deriva</div>
        <div style={{ width: 60 }} />
      </div>

      {/* COUNTRY HERO */}
      <div style={{ position: "relative", height: 420, overflow: "hidden" }}>
        <img src={destData.img} alt={destData.name} style={{ width: "100%", height: "100%", objectFit: "cover" }} />
        <div style={{ position: "absolute", inset: 0, background: "linear-gradient(to top, rgba(30,28,24,0.9) 0%, rgba(30,28,24,0.2) 60%, transparent 100%)" }} />
        <div style={{ position: "absolute", bottom: 0, left: 0, right: 0, padding: "3rem" }}>
          <div style={{ fontSize: "0.6rem", letterSpacing: "0.3em", textTransform: "uppercase", color: c.tan, marginBottom: "0.5rem", fontFamily: "system-ui, sans-serif" }}>{destData.region}</div>
          <div style={{ fontSize: "clamp(2.5rem, 6vw, 4.5rem)", fontWeight: "normal", color: c.white, lineHeight: 1, marginBottom: "0.75rem" }}>{destData.name}</div>
          <div style={{ fontSize: "0.85rem", color: c.sand, fontFamily: "system-ui, sans-serif", fontWeight: 300, fontStyle: "italic", maxWidth: 600 }}>"{destData.hook}"</div>
        </div>
      </div>

      {/* REGION SELECTOR */}
      <div style={{ background: c.bark, borderBottom: `1px solid rgba(200,184,154,0.15)` }}>
        <div style={{ display: "flex", overflowX: "auto", padding: "0 2rem" }}>
          {regions.map((r, i) => (
            <button key={i} onClick={() => switchRegion(i)} style={{ background: "none", border: "none", borderBottom: activeRegion === i ? `2px solid ${c.gold}` : "2px solid transparent", padding: "1.1rem 1.5rem", fontFamily: "system-ui, sans-serif", fontSize: "0.72rem", letterSpacing: "0.12em", textTransform: "uppercase", color: activeRegion === i ? c.gold : c.mid, cursor: "pointer", whiteSpace: "nowrap", transition: "all 0.2s", flexShrink: 0 }}>
              {r.name}
            </button>
          ))}
        </div>
      </div>

      {/* REGION HERO */}
      <div style={{ position: "relative", height: 320, overflow: "hidden" }}>
        <img src={region.img} alt={region.name} style={{ width: "100%", height: "100%", objectFit: "cover" }} />
        <div style={{ position: "absolute", inset: 0, background: "linear-gradient(to top, rgba(30,28,24,0.85) 0%, rgba(30,28,24,0.1) 70%, transparent 100%)" }} />
        <div style={{ position: "absolute", bottom: 0, left: 0, right: 0, padding: "2.5rem 3rem" }}>
          <div style={{ fontSize: "0.58rem", letterSpacing: "0.25em", textTransform: "uppercase", color: c.tan, marginBottom: "0.4rem", fontFamily: "system-ui, sans-serif" }}>{region.tag}</div>
          <div style={{ fontSize: "clamp(1.8rem, 4vw, 3rem)", fontWeight: "normal", color: c.white, lineHeight: 1 }}>{region.name}</div>
        </div>
      </div>

      {/* CONTENT TABS — scoped to active region */}
      <div style={{ background: c.parchment, borderBottom: `1px solid ${c.sand}`, position: "sticky", top: "57px", zIndex: 10 }}>
        <div style={{ display: "flex", padding: "0 3rem" }}>
          {tabs.map((tab) => (
            <button key={tab.id} onClick={() => setActiveTab(tab.id)} style={{ background: "none", border: "none", borderBottom: activeTab === tab.id ? `2px solid ${c.gold}` : "2px solid transparent", padding: "1.1rem 1.5rem", fontFamily: "system-ui, sans-serif", fontSize: "0.68rem", letterSpacing: "0.15em", textTransform: "uppercase", color: activeTab === tab.id ? c.gold : c.mid, cursor: "pointer", transition: "all 0.2s" }}>
              {tab.label}
            </button>
          ))}
        </div>
      </div>

      <div style={{ maxWidth: 900, margin: "0 auto", padding: "3rem" }}>

        {/* EXPLORE TAB */}
        {activeTab === "explore" && (
          <div>
            <p style={{ fontSize: "0.95rem", lineHeight: 1.9, color: c.mid, fontFamily: "system-ui, sans-serif", fontWeight: 300, marginBottom: "2.5rem", maxWidth: 720 }}>{region.intro}</p>
            <div style={{ display: "flex", flexDirection: "column", gap: "1rem" }}>
              {region.highlights.map((h, i) => (
                <div key={i} style={{ background: c.parchment, padding: "1.5rem 2rem", borderLeft: `3px solid ${c.tan}` }}>
                  <div style={{ fontSize: "0.8rem", fontWeight: 600, color: c.charcoal, marginBottom: "0.4rem", fontFamily: "system-ui, sans-serif" }}>{h.label}</div>
                  <div style={{ fontSize: "0.85rem", lineHeight: 1.75, color: c.mid, fontFamily: "system-ui, sans-serif", fontWeight: 300 }}>{h.text}</div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* EAT & DRINK TAB — region specific */}
        {activeTab === "eat" && (
          <div>
            <div style={{ display: "flex", alignItems: "center", gap: "0.75rem", marginBottom: "2rem" }}>
              <div style={{ width: 20, height: 1, background: c.tan }} />
              <span style={{ fontSize: "0.6rem", letterSpacing: "0.25em", textTransform: "uppercase", color: c.mid, fontFamily: "system-ui, sans-serif" }}>Where to eat in {region.name}</span>
            </div>
            <div style={{ display: "flex", flexDirection: "column", gap: "0" }}>
              {region.eat.map((place, i) => (
                <div key={i} style={{ padding: "1.5rem 0", borderBottom: i < region.eat.length - 1 ? `1px solid ${c.sand}` : "none", display: "grid", gridTemplateColumns: "1fr 2fr", gap: "2rem", alignItems: "start" }}>
                  <div style={{ fontFamily: "Georgia, serif", fontSize: "1rem", color: c.ink, lineHeight: 1.3 }}>{place.name}</div>
                  <div style={{ fontSize: "0.85rem", lineHeight: 1.8, color: c.mid, fontFamily: "system-ui, sans-serif", fontWeight: 300 }}>{place.desc}</div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* WHERE TO STAY TAB — region specific */}
        {activeTab === "stay" && (
          <div>
            <div style={{ display: "flex", alignItems: "center", gap: "0.75rem", marginBottom: "2rem" }}>
              <div style={{ width: 20, height: 1, background: c.tan }} />
              <span style={{ fontSize: "0.6rem", letterSpacing: "0.25em", textTransform: "uppercase", color: c.mid, fontFamily: "system-ui, sans-serif" }}>Where to stay in {region.name}</span>
            </div>
            <div style={{ display: "flex", flexDirection: "column", gap: "1rem" }}>
              {region.stay.map((hotel, i) => (
                <div key={i} style={{ background: i === 0 ? c.bark : c.parchment, padding: "1.75rem 2rem" }}>
                  <div style={{ fontSize: "0.55rem", letterSpacing: "0.2em", textTransform: "uppercase", color: i === 0 ? c.tan : c.gold, marginBottom: "0.4rem", fontFamily: "system-ui, sans-serif" }}>{hotel.tier}</div>
                  <div style={{ fontFamily: "Georgia, serif", fontSize: "1.1rem", color: i === 0 ? c.cream : c.ink, marginBottom: "0.6rem" }}>{hotel.name}</div>
                  <div style={{ fontSize: "0.83rem", lineHeight: 1.75, color: i === 0 ? c.tan : c.mid, fontFamily: "system-ui, sans-serif", fontWeight: 300 }}>{hotel.desc}</div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* LOGISTICS TAB — country level (same across all regions) */}
        {activeTab === "logistics" && (
          <div>
            <div style={{ display: "flex", alignItems: "center", gap: "0.75rem", marginBottom: "2rem" }}>
              <div style={{ width: 20, height: 1, background: c.tan }} />
              <span style={{ fontSize: "0.6rem", letterSpacing: "0.25em", textTransform: "uppercase", color: c.mid, fontFamily: "system-ui, sans-serif" }}>How to do {destData.name}</span>
            </div>
            <div style={{ maxWidth: 720 }}>
              {logistics.map((item, i) => (
                <div key={i} style={{ display: "grid", gridTemplateColumns: "180px 1fr", gap: "2rem", padding: "2rem 0", borderBottom: i < logistics.length - 1 ? `1px solid ${c.sand}` : "none", alignItems: "start" }}>
                  <div style={{ fontFamily: "Georgia, serif", fontSize: "1rem", color: c.ink, lineHeight: 1.3 }}>{item.q}</div>
                  <div style={{ fontSize: "0.88rem", lineHeight: 1.85, color: c.charcoal, fontFamily: "system-ui, sans-serif", fontWeight: 300 }}>{item.a}</div>
                </div>
              ))}
            </div>
          </div>
        )}
      </div>

      {/* FOOTER */}
      <div style={{ background: c.bark, padding: "4rem 3rem", textAlign: "center", marginTop: "2rem" }}>
        <div style={{ fontFamily: "Georgia, serif", fontSize: "1.8rem", color: c.cream, marginBottom: "1rem", fontStyle: "italic" }}>Ready to actually go?</div>
        <div style={{ fontSize: "0.85rem", color: c.tan, fontFamily: "system-ui, sans-serif", fontWeight: 300, marginBottom: "2rem" }}>Retake the quiz or explore another destination.</div>
        <button onClick={onBack} style={{ background: "none", border: `1px solid ${c.tan}`, color: c.cream, fontFamily: "system-ui, sans-serif", fontSize: "0.7rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "0.9rem 2.5rem", cursor: "pointer" }}>
          Back to Deriva
        </button>
      </div>
    </div>
  );
}


function DirectPlanInput({ onStart, onBack, c }) {
  const [val, setVal] = useState("");
  return (
    <div style={{ minHeight: "calc(100vh - 60px)", background: c.bark, display: "flex", alignItems: "center", justifyContent: "center", padding: "4rem 2rem" }}>
      <div style={{ maxWidth: 560, width: "100%", textAlign: "center" }}>
        <div style={{ fontSize: "0.58rem", letterSpacing: "0.35em", textTransform: "uppercase", color: c.gold, marginBottom: "1.5rem", fontFamily: "system-ui, sans-serif" }}>I know where I want to go</div>
        <div style={{ fontSize: "clamp(1.8rem, 5vw, 3rem)", color: c.cream, lineHeight: 1.15, marginBottom: "1rem" }}>Tell us about your trip</div>
        <div style={{ width: 30, height: 1, background: c.gold, margin: "0 auto 1.5rem" }} />
        <div style={{ fontSize: "0.88rem", color: c.tan, fontFamily: "system-ui, sans-serif", fontWeight: 300, lineHeight: 1.8, marginBottom: "2.5rem" }}>
          Destination, rough dates, who is going, anything you already know. Deriva builds the rest.
        </div>
        <textarea
          value={val}
          onChange={e => setVal(e.target.value)}
          placeholder="10 days in Patagonia, late March, flying from NYC..."
          style={{ width: "100%", minHeight: 140, background: "rgba(255,255,255,0.06)", border: "1px solid rgba(200,184,154,0.3)", padding: "1.25rem 1.5rem", fontFamily: "system-ui, sans-serif", fontSize: "0.9rem", color: c.cream, fontWeight: 300, resize: "none", outline: "none", lineHeight: 1.7, boxSizing: "border-box", marginBottom: "1.5rem" }}
        />
        <div style={{ display: "flex", gap: "1rem", justifyContent: "center" }}>
          <button onClick={onBack} style={{ background: "none", border: "1px solid rgba(200,184,154,0.3)", color: c.tan, fontFamily: "system-ui, sans-serif", fontSize: "0.7rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "1rem 2rem", cursor: "pointer" }}>
            Back
          </button>
          <button
            onClick={() => val.trim() && onStart(val.trim())}
            disabled={!val.trim()}
            style={{ background: val.trim() ? c.gold : "rgba(200,184,154,0.2)", border: "none", color: val.trim() ? c.ink : c.mid, fontFamily: "system-ui, sans-serif", fontSize: "0.72rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "1rem 2.5rem", cursor: val.trim() ? "pointer" : "not-allowed" }}
          >
            Build my itinerary
          </button>
        </div>
      </div>
    </div>
  );
}

// ─── MAIN APP ─────────────────────────────────────────────────────────────────
export default function Deriva() {
  const [view, setView] = useState("home");
  const [step, setStep] = useState(0);
  const [answers, setAnswers] = useState({});   // { [stepIdx]: string[] }
  const [notes, setNotes] = useState({});        // { [stepIdx]: string }
  const [result, setResult] = useState(null);
  const [destPage, setDestPage] = useState(null);
  const [destStartRegion, setDestStartRegion] = useState(0);
  const [aiNote, setAiNote] = useState(null);
  const [aiLoading, setAiLoading] = useState(false);
  const [planMessages, setPlanMessages] = useState([]);
  const [planInput, setPlanInput] = useState("");
  const [planLoading, setPlanLoading] = useState(false);
  const [itinerary, setItinerary] = useState(null);
  const [directMode, setDirectMode] = useState(false);
  const [tripIdea, setTripIdea] = useState("");

  function startQuiz() { setView("quiz"); setStep(0); setAnswers({}); setNotes({}); setResult(null); setAiNote(null); setAiLoading(false); setPlanMessages([]); setItinerary(null); setPlanInput(""); setDirectMode(false); setTripIdea(""); }

  function startDirectPlan(idea) {
    setTripIdea(idea);
    setDirectMode(true);
    setPlanMessages([{
      role: "assistant",
      content: "Love it — a few quick things before I build your itinerary:\n\nWho is going? (solo, partner, group, family)\n\nWhat is the vibe? (packed days, slower pace, somewhere in between)\n\nWhere are you flying from?"
    }]);
    setItinerary(null);
    setPlanInput("");
    setResult({ name: "Your trip", country: null, hook: "", intro: "" });
    setView("plan");
  }

  function buildRegionContext(region) {
    const eat = region.eat?.map(e => `- ${e.name}: ${e.desc}`).join("\n") || "";
    const stay = region.stay?.map(s => `- ${s.name} (${s.tier}): ${s.desc}`).join("\n") || "";
    const logistics = region.logistics?.map(l => `${l.q}: ${l.a}`).join("\n") || "";
    const highlights = region.highlights?.map(h => `- ${h.label}: ${h.text}`).join("\n") || "";
    return `DESTINATION: ${region.name}\nINTRO: ${region.intro}\n\nHIGHLIGHTS:\n${highlights}\n\nWHERE TO EAT:\n${eat}\n\nWHERE TO STAY:\n${stay}\n\nLOGISTICS:\n${logistics}`;
  }

  function buildQuizContext() {
    return questions.map((q, i) => {
      const sel = answers[i] || [];
      const opts = sel.map(v => q.opts.find(o => o.val === v)?.text).filter(Boolean).join(", ");
      const note = notes[i] ? ` — "${notes[i]}"` : "";
      return `${q.label}: ${opts || "—"}${note}`;
    }).join("\n");
  }

  async function startPlanner() {
    setView("plan");
    setPlanMessages([]);
    setItinerary(null);
    setPlanInput("");
    const regionContext = buildRegionContext(result);
    const quizContext = buildQuizContext();
    const openingMsg = {
      role: "assistant",
      content: `You've been matched to **${result.name}**.\n\nI already know what kind of traveler you are. Three quick things and I'll build your full itinerary:\n\n**When are you thinking of going?**\n\n**How many nights?**\n\n**Where are you flying from?** (city or region is fine — e.g. "NYC area", "Chicago", "London")`
    };
    setPlanMessages([openingMsg]);
    // Store context for later use in the system prompt
    window._derivaContext = { regionContext, quizContext, regionName: result.name };
  }

  async function sendPlanMessage() {
    if (!planInput.trim() || planLoading) return;
    const userMsg = { role: "user", content: planInput };
    const newMessages = [...planMessages, userMsg];
    setPlanMessages(newMessages);
    setPlanInput("");
    setPlanLoading(true);

    const { regionContext, quizContext, regionName } = window._derivaContext || {};

    const systemPrompt = directMode
      ? "You are Deriva trip planning assistant. The traveler wants: " + tripIdea + ". Ask who is going, the vibe, and where flying from if not provided. Then build a specific day-by-day itinerary. Use real hotel and restaurant names. Write in Deriva voice: direct, specific, slightly literary. Output itinerary as JSON wrapped in <ITINERARY> tags with structure: {days:[{day,title,morning,afternoon,evening,stay}],notes:[],bestFor:string}. When user requests changes output full updated itinerary in <ITINERARY> tags again."
      : `You are Deriva's trip planning assistant — opinionated, specific, and knowledgeable. You've matched this traveler to ${regionName}.

TRAVELER PROFILE (from their quiz):
${quizContext}

DESTINATION KNOWLEDGE BASE:
${regionContext}

YOUR ROLE:
- You need three things before building: (1) when they're going, (2) how many nights, (3) where they're flying from
- Once you have all three, build the itinerary FIRST — get them excited about the destination
- Weave routing naturally INTO the itinerary. Day 1 might read "Fly into Reykjavík, pick up a car, drive the South Coast — Skógafoss and Reynisfjara break up the journey east beautifully. Sleep in Vík." That's how you make a long drive feel like part of the adventure, not a warning
- Never lead with logistics warnings. If an airport is small or a drive is long, frame it as part of the experience or show how the itinerary handles it gracefully
- Use ONLY specific places from the knowledge base above — real restaurant names, real hotel names, real highlights
- Write in Deriva's voice: direct, slightly literary, confident, never generic
- Output the itinerary in this exact JSON format wrapped in <ITINERARY> tags:

<ITINERARY>
{
  "days": [
    {
      "day": 1,
      "title": "Short evocative title",
      "morning": "What to do and where",
      "afternoon": "What to do and where",
      "evening": "Where to eat and what to order",
      "stay": "Hotel name and one line why"
    }
  ],
  "notes": ["Practical tips woven as insider knowledge, not warnings"],
  "bestFor": "One line on who this itinerary is perfect for"
}
</ITINERARY>

After the itinerary, add 1-2 sentences inviting them to adjust anything — different pace, swap a hotel, add a day somewhere.
When the user asks to change something, output the FULL updated itinerary in <ITINERARY> tags again plus a brief note on what changed.
If you don't have all three pieces yet, ask — but keep it light and conversational, never clinical.`;

    try {
      const apiMessages = newMessages.map(m => ({
        role: m.role === "assistant" ? "assistant" : "user",
        content: m.content.replace(/<ITINERARY>[\s\S]*?<\/ITINERARY>/g, "[itinerary updated]")
      }));

      const response = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 4000,
          system: systemPrompt,
          messages: apiMessages
        })
      });

      const data = await response.json();
      const fullText = data.content?.[0]?.text || "";

      // Extract itinerary JSON if present
      const itineraryMatch = fullText.match(/<ITINERARY>([\s\S]*?)<\/ITINERARY>/);
      if (itineraryMatch) {
        try {
          const parsed = JSON.parse(itineraryMatch[1].trim());
          setItinerary(parsed);
        } catch(e) { console.error("Itinerary parse error", e); }
      }

      // Strip itinerary tags from chat display
      const chatText = fullText.replace(/<ITINERARY>[\s\S]*?<\/ITINERARY>/g, "").trim();
      const assistantMsg = { role: "assistant", content: chatText || "Itinerary updated — take a look on the right." };
      setPlanMessages(prev => [...prev, assistantMsg]);

    } catch(e) {
      console.error(e);
      setPlanMessages(prev => [...prev, { role: "assistant", content: "Something went wrong. Try again." }]);
    } finally {
      setPlanLoading(false);
    }
  }

  function toggleOption(val) {
    const cur = answers[step] || [];
    const next = cur.includes(val) ? cur.filter(v => v !== val) : [...cur, val];
    setAnswers(prev => ({ ...prev, [step]: next }));
  }

  function setNote(text) {
    setNotes(prev => ({ ...prev, [step]: text }));
  }

  async function generateAiNote(matchedRegion, allAnswers, allNotes) {
    const hasNotes = Object.values(allNotes).some(n => n && n.trim());
    if (!hasNotes) return;
    setAiLoading(true);
    try {
      const questionSummary = questions.map((q, i) => {
        const sel = allAnswers[i] || [];
        const opts = sel.map(v => q.opts.find(o => o.val === v)?.text).filter(Boolean).join(", ");
        const note = allNotes[i] ? ` (they added: "${allNotes[i]}")` : "";
        return `${q.label}: ${opts || "—"}${note}`;
      }).join("\n");
      const response = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 1000,
          system: `You are Deriva, a travel platform that surfaces underrated destinations with intent. You've matched a traveler to a specific region. Write a short personal 2-3 sentence note (no headers, no lists) connecting their specific written notes to why this destination is their match. Be specific, evocative, confident. Deriva voice: direct, knowledgeable, slightly literary. Don't repeat the destination name more than once. Don't be sycophantic. Only reference what they actually wrote — ignore blank notes.`,
          messages: [{ role: "user", content: `Matched to: ${matchedRegion.name} (${matchedRegion.country})\n\nQuiz answers with their notes:\n${questionSummary}\n\nWrite the personalized note.` }]
        })
      });
      const data = await response.json();
      const text = data.content?.[0]?.text;
      if (text) setAiNote(text);
    } catch (e) { console.error(e); }
    finally { setAiLoading(false); }
  }

  function goNext() {
    if (step < questions.length) {
      if (step < questions.length - 1) { setStep(step + 1); }
      else { setStep(questions.length); } // go to final free text step
    } else {
      const matched = getMatch(answers);
      setResult(matched);
      setView("result");
      generateAiNote(matched, answers, notes);
    }
  }

  function goBack() {
    if (step === questions.length) { setStep(questions.length - 1); }
    else if (step > 0) { setStep(step - 1); }
    else setView("home");
  }

  function openDest(key, startRegionIdx = 0) {
    if (key === "portugal" || key === "italy" || key === "spain" || key === "chile" || key === "iceland" || key === "japan" || key === "newzealand" || key === "oman" || key === "australia" || key === "georgia" || key === "colombia" || key === "vietnam") {
      setDestPage(key);
      setDestStartRegion(startRegionIdx);
      setView("dest");
    }
  }

  function openResultDest() {
    if (!result) return;
    const regions = result.country === "portugal" ? portugalRegions : result.country === "spain" ? spainRegions : result.country === "chile" ? chileRegions : result.country === "iceland" ? icelandRegions : result.country === "japan" ? japanRegions : result.country === "newzealand" ? newZealandRegions : result.country === "oman" ? omanRegions : result.country === "australia" ? australiaRegions : result.country === "georgia" ? georgiaRegions : result.country === "colombia" ? colombiaRegions : result.country === "vietnam" ? vietnamRegions : italyRegions;
    const idx = regions.findIndex(r => r.name === result.name);
    openDest(result.country, idx >= 0 ? idx : 0);
  }

  function backFromDest() { setDestPage(null); setDestStartRegion(0); setView(result ? "result" : "home"); }


  const destList = Object.entries(destinations).map(([key, d]) => ({ key, ...d }));

  if (view === "dest") return <DestinationPage dest={destPage} startRegion={destStartRegion} onBack={backFromDest} openDest={openDest} />;

  return (
    <div style={{ minHeight: "100vh", background: c.cream, fontFamily: "Georgia, serif" }}>
      {/* NAV */}
      <nav style={{ background: c.bark, padding: "1.25rem 3rem", display: "flex", alignItems: "center", justifyContent: "space-between" }}>
        <button onClick={() => setView("home")} style={{ background: "none", border: "none", fontFamily: "system-ui, sans-serif", fontWeight: 200, fontSize: "1.1rem", letterSpacing: "0.3em", textTransform: "uppercase", color: c.cream, cursor: "pointer" }}>Deriva</button>
        <div style={{ display: "flex", gap: "2rem", alignItems: "center" }}>
          <div style={{ position: "relative" }} onMouseEnter={e => e.currentTarget.querySelector(".dropdown").style.display="block"} onMouseLeave={e => e.currentTarget.querySelector(".dropdown").style.display="none"}>
            <button style={{ background: "none", border: "none", fontFamily: "system-ui, sans-serif", fontSize: "0.65rem", letterSpacing: "0.15em", textTransform: "uppercase", color: c.tan, cursor: "pointer" }}>Explore ▾</button>
            <div className="dropdown" style={{ display: "none", position: "absolute", top: "100%", left: "50%", transform: "translateX(-50%)", background: c.ink, padding: "0.75rem 0", minWidth: 160, zIndex: 100, marginTop: "0.75rem" }}>
              {[["Portugal","portugal"],["Italy","italy"],["Spain","spain"],["Chile","chile"],["Iceland","iceland"],["Japan","japan"],["New Zealand","newzealand"],["Oman","oman"],["Australia","australia"],["Georgia","georgia"],["Colombia","colombia"],["Vietnam","vietnam"]].map(([name, key]) => (
                <button key={key} onClick={() => openDest(key)} style={{ display: "block", width: "100%", background: "none", border: "none", fontFamily: "system-ui, sans-serif", fontSize: "0.65rem", letterSpacing: "0.15em", textTransform: "uppercase", color: c.tan, cursor: "pointer", padding: "0.6rem 1.25rem", textAlign: "left" }}
                  onMouseEnter={e => e.currentTarget.style.color = c.cream}
                  onMouseLeave={e => e.currentTarget.style.color = c.tan}
                >{name}</button>
              ))}
            </div>
          </div>
          <a href="https://substack.com/@derivatravel" target="_blank" rel="noopener noreferrer" style={{ fontFamily: "system-ui, sans-serif", fontSize: "0.65rem", letterSpacing: "0.15em", textTransform: "uppercase", color: c.tan, textDecoration: "none" }}
            onMouseEnter={e => e.currentTarget.style.color = c.cream}
            onMouseLeave={e => e.currentTarget.style.color = c.tan}
          >Newsletter ↗</a>
        </div>
      </nav>

      {/* HOME */}
      {view === "home" && (
        <div>
          <div style={{ background: c.bark, padding: "6rem 3rem", textAlign: "center" }}>
            <div style={{ fontSize: "0.6rem", letterSpacing: "0.35em", textTransform: "uppercase", color: c.gold, marginBottom: "1.5rem", fontFamily: "system-ui, sans-serif" }}>Travel with intent</div>
            <div style={{ fontSize: "clamp(2.5rem, 7vw, 5rem)", fontWeight: "normal", color: c.cream, lineHeight: 1.05, marginBottom: "1.5rem" }}>
              Be the first one in your<br /><em style={{ color: c.tan }}>friend group to go.</em>
            </div>
            <div style={{ width: 40, height: 1, background: c.gold, margin: "0 auto 1.5rem" }} />
            <div style={{ fontSize: "1rem", color: c.sand, fontFamily: "system-ui, sans-serif", fontWeight: 300, lineHeight: 1.8, maxWidth: 560, margin: "0 auto 3rem" }}>
              Deriva surfaces the destinations that look impossible to plan, makes them feel doable, and gives you the inside knowledge to actually go.
            </div>
            <div style={{ display: "flex", flexDirection: "column", alignItems: "center", gap: "1rem" }}>
              <button onClick={startQuiz} style={{ background: c.gold, border: "none", color: c.ink, fontFamily: "system-ui, sans-serif", fontSize: "0.72rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "1.1rem 3rem", cursor: "pointer" }}>
                Find your destination
              </button>
              <div style={{ display: "flex", alignItems: "center", gap: "1rem", width: "100%", maxWidth: 300 }}>
                <div style={{ flex: 1, height: 1, background: "rgba(200,184,154,0.2)" }} />
                <span style={{ fontSize: "0.6rem", letterSpacing: "0.2em", textTransform: "uppercase", color: c.mid, fontFamily: "system-ui, sans-serif" }}>or</span>
                <div style={{ flex: 1, height: 1, background: "rgba(200,184,154,0.2)" }} />
              </div>
              <button onClick={() => setView("directplan")} style={{ background: "none", border: "1px solid " + c.tan, color: c.cream, fontFamily: "system-ui, sans-serif", fontSize: "0.72rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "1.1rem 3rem", cursor: "pointer" }}>
                I know where I want to go
              </button>
            </div>
          </div>

          <div style={{ padding: "5rem 3rem" }}>
            <div style={{ textAlign: "center", marginBottom: "3rem" }}>
              <div style={{ fontSize: "0.58rem", letterSpacing: "0.3em", textTransform: "uppercase", color: c.gold, marginBottom: "0.75rem", fontFamily: "system-ui, sans-serif" }}>Where Deriva goes</div>
              <div style={{ fontSize: "2rem", color: c.ink }}>Destinations</div>
            </div>
            <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(280px, 1fr))", gap: "1.5rem", maxWidth: 1000, margin: "0 auto" }}>
              {destList.map((d) => (
                <div key={d.key} onClick={() => openDest(d.key)} style={{ position: "relative", overflow: "hidden", cursor: (d.key === "portugal" || d.key === "italy" || d.key === "spain" || d.key === "chile" || d.key === "iceland" || d.key === "japan" || d.key === "newzealand" || d.key === "oman" || d.key === "australia" || d.key === "georgia" || d.key === "colombia" || d.key === "vietnam") ? "pointer" : "default" }}>
                  <img src={d.img} alt={d.name} style={{ width: "100%", aspectRatio: "4/3", objectFit: "cover", display: "block" }} />
                  <div style={{ position: "absolute", inset: 0, background: "linear-gradient(to top, rgba(30,28,24,0.8) 0%, transparent 60%)" }} />
                  <div style={{ position: "absolute", bottom: 0, left: 0, right: 0, padding: "1.5rem" }}>
                    <div style={{ fontSize: "1.2rem", color: c.white, marginBottom: "0.25rem" }}>{d.name}</div>
                    <div style={{ fontSize: "0.65rem", color: c.tan, fontFamily: "system-ui, sans-serif", letterSpacing: "0.1em" }}>{d.tag}</div>
                    <div style={{ fontSize: "0.55rem", letterSpacing: "0.15em", textTransform: "uppercase", color: (d.key === "portugal" || d.key === "italy" || d.key === "spain" || d.key === "chile" || d.key === "iceland" || d.key === "japan" || d.key === "newzealand" || d.key === "oman" || d.key === "australia" || d.key === "georgia" || d.key === "colombia" || d.key === "vietnam") ? c.gold : c.mid, marginTop: "0.5rem", fontFamily: "system-ui, sans-serif" }}>
                      {(d.key === "portugal" || d.key === "italy" || d.key === "spain" || d.key === "chile" || d.key === "iceland" || d.key === "japan" || d.key === "newzealand" || d.key === "oman" || d.key === "australia" || d.key === "georgia" || d.key === "colombia" || d.key === "vietnam") ? "View guide →" : "Coming soon"}
                    </div>
                  </div>
                </div>
              ))}
            </div>
          </div>

          <div style={{ background: c.parchment, padding: "5rem 3rem", textAlign: "center" }}>
            <div style={{ maxWidth: 700, margin: "0 auto" }}>
              <div style={{ fontSize: "0.58rem", letterSpacing: "0.3em", textTransform: "uppercase", color: c.gold, marginBottom: "1rem", fontFamily: "system-ui, sans-serif" }}>Why Deriva</div>
              <div style={{ fontSize: "1.8rem", color: c.ink, lineHeight: 1.3, marginBottom: "1.5rem" }}>The trip you keep putting off<br />is more reachable than you think.</div>
              <div style={{ fontSize: "0.9rem", color: c.mid, fontFamily: "system-ui, sans-serif", fontWeight: 300, lineHeight: 1.9 }}>
                Everyone has that place saved in their phone — the trulli houses in Puglia, the cliffs above a Sicilian town, a Douro Valley vineyard at sunrise. The reason you haven't gone isn't money or time. It's that nobody has made it feel possible yet. That's what Deriva does.
              </div>
            </div>
          </div>
        </div>
      )}

      {view === "directplan" && (
        <DirectPlanInput
          onStart={startDirectPlan}
          onBack={() => setView("home")}
          c={c}
        />
      )}

      {/* QUIZ */}
      {view === "quiz" && (
        <div style={{ maxWidth: 700, margin: "0 auto", padding: "4rem 3rem" }}>
          {/* Progress bar */}
          <div style={{ marginBottom: "3rem" }}>
            <div style={{ display: "flex", justifyContent: "space-between", marginBottom: "0.75rem" }}>
              <span style={{ fontSize: "0.62rem", letterSpacing: "0.2em", textTransform: "uppercase", color: c.gold, fontFamily: "system-ui, sans-serif" }}>
                {step < questions.length ? questions[step].label : "Almost there"}
              </span>
              <span style={{ fontSize: "0.62rem", color: c.mid, fontFamily: "system-ui, sans-serif" }}>{step + 1} / {questions.length + 1}</span>
            </div>
            <div style={{ height: 2, background: c.sand, borderRadius: 2 }}>
              <div style={{ height: "100%", background: c.gold, width: `${((step + 1) / (questions.length + 1)) * 100}%`, transition: "width 0.3s ease", borderRadius: 2 }} />
            </div>
          </div>

          {step < questions.length ? (() => {
            const q = questions[step];
            const sel = answers[step] || [];
            const note = notes[step] || "";
            const canContinue = q.opts.length === 0 || sel.length > 0 || note.trim().length > 0;
            return (
              <>
                <div style={{ marginBottom: "0.5rem", fontSize: "clamp(1.4rem, 3.5vw, 2rem)", color: c.ink, lineHeight: 1.25 }}>{q.q}</div>
                <div style={{ fontSize: "0.78rem", color: c.mid, fontFamily: "system-ui, sans-serif", fontWeight: 300, marginBottom: "2rem" }}>{q.sub}</div>
                {q.opts.length > 0 && (
                  <div style={{ display: "flex", flexDirection: "column", gap: "0.6rem", marginBottom: "1.5rem" }}>
                    {q.opts.map((opt) => {
                    const active = sel.includes(opt.val);
                    return (
                      <button key={opt.val} onClick={() => toggleOption(opt.val)} style={{ background: active ? c.bark : c.white, border: `1px solid ${active ? c.bark : c.sand}`, padding: "0.95rem 1.5rem", textAlign: "left", cursor: "pointer", transition: "all 0.15s", display: "flex", alignItems: "center", gap: "1rem" }}>
                        <div style={{ width: 14, height: 14, border: `1px solid ${active ? c.tan : c.sand}`, background: active ? c.tan : "transparent", flexShrink: 0, transition: "all 0.15s", display: "flex", alignItems: "center", justifyContent: "center" }}>
                          {active && <span style={{ color: c.bark, fontSize: "0.65rem", fontWeight: 700, lineHeight: 1 }}>✓</span>}
                        </div>
                        <span style={{ fontFamily: "system-ui, sans-serif", fontSize: "0.88rem", color: active ? c.cream : c.charcoal, fontWeight: 300 }}>{opt.text}</span>
                      </button>
                    );
                  })}
                  </div>
                )}
                <div style={{ marginBottom: "2.5rem" }}>
                  <div style={{ fontSize: "0.7rem", letterSpacing: "0.1em", textTransform: "uppercase", color: c.mid, fontFamily: "system-ui, sans-serif", marginBottom: "0.5rem" }}>{q.prompt}</div>
                  <textarea
                    value={note}
                    onChange={(e) => setNote(e.target.value)}
                    placeholder="Optional — add your own answer or context"
                    style={{ width: "100%", minHeight: 60, background: c.white, border: `1px solid ${note ? c.tan : c.sand}`, padding: "0.8rem 1rem", fontFamily: "system-ui, sans-serif", fontSize: "0.85rem", color: c.charcoal, fontWeight: 300, resize: "none", outline: "none", boxSizing: "border-box", lineHeight: 1.6 }}
                  />
                </div>
                <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
                  <button onClick={goBack} style={{ background: "none", border: "none", color: c.mid, fontFamily: "system-ui, sans-serif", fontSize: "0.7rem", letterSpacing: "0.15em", textTransform: "uppercase", cursor: "pointer" }}>← Back</button>
                  <button onClick={goNext} disabled={!canContinue} style={{ background: canContinue ? c.bark : c.sand, border: "none", color: canContinue ? c.cream : c.mid, fontFamily: "system-ui, sans-serif", fontSize: "0.72rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "1rem 2.5rem", cursor: canContinue ? "pointer" : "not-allowed", transition: "all 0.2s" }}>
                    Continue →
                  </button>
                </div>
              </>
            );
          })() : (
            <>
              {/* Final step — anything else */}
              <div style={{ marginBottom: "0.75rem", fontSize: "clamp(1.4rem, 3.5vw, 2rem)", color: c.ink, lineHeight: 1.25 }}>Anything else before we match you?</div>
              <div style={{ fontSize: "0.8rem", color: c.mid, fontFamily: "system-ui, sans-serif", fontWeight: 300, marginBottom: "2.5rem" }}>Optional — a vibe, a past trip, something you're chasing. We'll use it to personalize your result.</div>
              <textarea
                value={notes[questions.length] || ""}
                onChange={(e) => setNotes(prev => ({ ...prev, [questions.length]: e.target.value }))}
                placeholder={`"I want to eat my way through a coastal town nobody's heard of"\n"Last trip that got me was the Amalfi Coast but I want something less obvious"\n"I just need to switch off completely for a week"`}
                style={{ width: "100%", minHeight: 140, background: c.white, border: `1px solid ${notes[questions.length] ? c.tan : c.sand}`, padding: "1rem 1.1rem", fontFamily: "system-ui, sans-serif", fontSize: "0.88rem", color: c.charcoal, fontWeight: 300, resize: "none", outline: "none", boxSizing: "border-box", lineHeight: 1.7, marginBottom: "2.5rem" }}
              />
              <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
                <button onClick={goBack} style={{ background: "none", border: "none", color: c.mid, fontFamily: "system-ui, sans-serif", fontSize: "0.7rem", letterSpacing: "0.15em", textTransform: "uppercase", cursor: "pointer" }}>← Back</button>
                <div style={{ display: "flex", gap: "1rem", alignItems: "center" }}>
                  <button onClick={goNext} style={{ background: "none", border: "none", color: c.mid, fontFamily: "system-ui, sans-serif", fontSize: "0.7rem", letterSpacing: "0.15em", textTransform: "uppercase", cursor: "pointer" }}>Skip →</button>
                  <button onClick={goNext} style={{ background: c.bark, border: "none", color: c.cream, fontFamily: "system-ui, sans-serif", fontSize: "0.72rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "1rem 2.5rem", cursor: "pointer" }}>
                    Find my match →
                  </button>
                </div>
              </div>
            </>
          )}
        </div>
      )}

      {/* RESULT */}
      {view === "result" && result && (
        <div>
          <div style={{ position: "relative", height: 500, overflow: "hidden" }}>
            <img src={result.img} alt={result.name} style={{ width: "100%", height: "100%", objectFit: "cover" }} />
            <div style={{ position: "absolute", inset: 0, background: "linear-gradient(to top, rgba(30,28,24,0.9) 0%, rgba(30,28,24,0.3) 60%, transparent 100%)" }} />
            <div style={{ position: "absolute", bottom: 0, left: 0, right: 0, padding: "3rem", textAlign: "center" }}>
              <div style={{ fontSize: "0.6rem", letterSpacing: "0.35em", textTransform: "uppercase", color: c.gold, marginBottom: "0.5rem", fontFamily: "system-ui, sans-serif" }}>Your Deriva match</div>
              <div style={{ fontSize: "0.65rem", letterSpacing: "0.2em", textTransform: "uppercase", color: c.tan, marginBottom: "0.75rem", fontFamily: "system-ui, sans-serif" }}>{destinations[result.country]?.name}</div>
              <div style={{ fontSize: "clamp(2.5rem, 8vw, 5rem)", color: c.white, fontWeight: "normal", lineHeight: 1 }}>{result.name}</div>
              <div style={{ fontSize: "0.85rem", color: c.tan, fontFamily: "system-ui, sans-serif", fontWeight: 300, letterSpacing: "0.1em", marginTop: "0.5rem" }}>{result.tag}</div>
            </div>
          </div>
          <div style={{ background: c.bark, padding: "3rem", textAlign: "center" }}>
            <div style={{ maxWidth: 650, margin: "0 auto" }}>
              <div style={{ fontSize: "1.1rem", color: c.cream, fontStyle: "italic", lineHeight: 1.7, marginBottom: "1rem" }}>"{result.hook}"</div>
              <div style={{ width: 30, height: 1, background: c.gold, margin: "0 auto 1.5rem" }} />
              <div style={{ fontSize: "0.88rem", color: c.tan, fontFamily: "system-ui, sans-serif", fontWeight: 300, lineHeight: 1.9, marginBottom: "2rem" }}>{result.intro}</div>
              {(aiLoading || aiNote) && (
                <div style={{ borderTop: `1px solid rgba(200,184,154,0.2)`, paddingTop: "1.5rem", marginBottom: "2rem" }}>
                  {aiLoading ? (
                    <div style={{ fontSize: "0.78rem", color: c.mid, fontFamily: "system-ui, sans-serif", fontStyle: "italic", letterSpacing: "0.05em" }}>Personalizing your match…</div>
                  ) : (
                    <div style={{ fontSize: "0.9rem", color: c.cream, fontStyle: "italic", lineHeight: 1.8, borderLeft: `2px solid ${c.gold}`, paddingLeft: "1rem" }}>{aiNote}</div>
                  )}
                </div>
              )}
              <div style={{ display: "flex", gap: "1rem", justifyContent: "center", flexWrap: "wrap" }}>
                <button onClick={startPlanner} style={{ background: c.gold, border: "none", color: c.ink, fontFamily: "system-ui, sans-serif", fontSize: "0.72rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "1rem 2.5rem", cursor: "pointer" }}>
                  Plan this trip →
                </button>
                <button onClick={openResultDest} style={{ background: "none", border: `1px solid ${c.tan}`, color: c.cream, fontFamily: "system-ui, sans-serif", fontSize: "0.72rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "1rem 2.5rem", cursor: "pointer" }}>
                  Explore {result.name}
                </button>
                <button onClick={startQuiz} style={{ background: "none", border: `1px solid rgba(200,184,154,0.3)`, color: c.tan, fontFamily: "system-ui, sans-serif", fontSize: "0.72rem", letterSpacing: "0.2em", textTransform: "uppercase", padding: "1rem 2.5rem", cursor: "pointer" }}>
                  Retake quiz
                </button>
              </div>
            </div>
          </div>
          <div style={{ padding: "4rem 3rem", background: c.cream }}>
            <div style={{ textAlign: "center", marginBottom: "2.5rem" }}>
              <div style={{ fontSize: "0.58rem", letterSpacing: "0.3em", textTransform: "uppercase", color: c.gold, fontFamily: "system-ui, sans-serif" }}>Also on Deriva</div>
            </div>
            <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(220px, 1fr))", gap: "1rem", maxWidth: 900, margin: "0 auto" }}>
              {destList.filter((d) => d.key !== result.key).map((d) => (
                <div key={d.key} onClick={() => openDest(d.key)} style={{ position: "relative", overflow: "hidden", cursor: (d.key === "portugal" || d.key === "italy" || d.key === "spain" || d.key === "chile" || d.key === "iceland" || d.key === "japan" || d.key === "newzealand" || d.key === "oman" || d.key === "australia" || d.key === "georgia" || d.key === "colombia" || d.key === "vietnam") ? "pointer" : "default" }}>
                  <img src={d.img} alt={d.name} style={{ width: "100%", aspectRatio: "3/2", objectFit: "cover", display: "block" }} />
                  <div style={{ position: "absolute", inset: 0, background: "linear-gradient(to top, rgba(30,28,24,0.75) 0%, transparent 60%)" }} />
                  <div style={{ position: "absolute", bottom: 0, left: 0, right: 0, padding: "1rem" }}>
                    <div style={{ fontSize: "1rem", color: c.white }}>{d.name}</div>
                    {(d.key !== "portugal" && d.key !== "italy" && d.key !== "spain" && d.key !== "chile" && d.key !== "iceland" && d.key !== "japan" && d.key !== "newzealand" && d.key !== "oman" && d.key !== "australia" && d.key !== "georgia" && d.key !== "colombia" && d.key !== "vietnam") && <div style={{ fontSize: "0.55rem", color: c.mid, fontFamily: "system-ui, sans-serif", letterSpacing: "0.15em", textTransform: "uppercase" }}>Coming soon</div>}
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>
      )}

      {/* PLAN VIEW */}
      {view === "plan" && result && (
        <div style={{ display: "flex", height: "calc(100vh - 60px)", overflow: "hidden" }}>

          {/* LEFT — Chat */}
          <div style={{ width: "38%", minWidth: 320, borderRight: `1px solid ${c.sand}`, display: "flex", flexDirection: "column", background: c.white }}>
            <div style={{ padding: "1.25rem 1.5rem", borderBottom: `1px solid ${c.sand}`, background: c.bark, display: "flex", alignItems: "center", justifyContent: "space-between" }}>
              <div>
                <div style={{ fontSize: "0.58rem", letterSpacing: "0.25em", textTransform: "uppercase", color: c.gold, fontFamily: "system-ui, sans-serif", marginBottom: "0.2rem" }}>Planning</div>
                <div style={{ fontSize: "0.95rem", color: c.cream }}>{directMode ? "Your trip" : result.name}</div>
              </div>
              <button onClick={() => setView(directMode ? "directplan" : "result")} style={{ background: "none", border: "none", color: c.tan, fontFamily: "system-ui, sans-serif", fontSize: "0.65rem", letterSpacing: "0.15em", textTransform: "uppercase", cursor: "pointer" }}>← Back</button>
            </div>
            <div style={{ flex: 1, overflowY: "auto", padding: "1.5rem", display: "flex", flexDirection: "column", gap: "1.25rem" }}>
              {planMessages.map((msg, i) => (
                <div key={i} style={{ display: "flex", flexDirection: "column", alignItems: msg.role === "user" ? "flex-end" : "flex-start" }}>
                  {msg.role === "assistant" && (
                    <div style={{ fontSize: "0.55rem", letterSpacing: "0.15em", textTransform: "uppercase", color: c.gold, fontFamily: "system-ui, sans-serif", marginBottom: "0.4rem" }}>Deriva</div>
                  )}
                  <div style={{ maxWidth: "88%", background: msg.role === "user" ? c.bark : c.cream, padding: "0.9rem 1.1rem", fontSize: "0.85rem", fontFamily: "system-ui, sans-serif", fontWeight: 300, color: msg.role === "user" ? c.cream : c.charcoal, lineHeight: 1.7, whiteSpace: "pre-wrap" }}>
                    {msg.content}
                  </div>
                </div>
              ))}
              {planLoading && (
                <div style={{ display: "flex", flexDirection: "column", alignItems: "flex-start" }}>
                  <div style={{ fontSize: "0.55rem", letterSpacing: "0.15em", textTransform: "uppercase", color: c.gold, fontFamily: "system-ui, sans-serif", marginBottom: "0.4rem" }}>Deriva</div>
                  <div style={{ background: c.cream, padding: "0.9rem 1.1rem", fontSize: "0.85rem", fontFamily: "system-ui, sans-serif", color: c.mid, fontStyle: "italic" }}>Building your itinerary…</div>
                </div>
              )}
            </div>
            <div style={{ padding: "1rem 1.5rem", borderTop: `1px solid ${c.sand}`, display: "flex", gap: "0.75rem", alignItems: "flex-end" }}>
              <textarea
                value={planInput}
                onChange={e => setPlanInput(e.target.value)}
                onKeyDown={e => { if (e.key === "Enter" && !e.shiftKey) { e.preventDefault(); sendPlanMessage(); } }}
                placeholder="Type your answer or request..."
                style={{ flex: 1, minHeight: 44, maxHeight: 120, background: c.cream, border: `1px solid ${c.sand}`, padding: "0.6rem 0.8rem", fontFamily: "system-ui, sans-serif", fontSize: "0.85rem", color: c.charcoal, fontWeight: 300, resize: "none", outline: "none", lineHeight: 1.5 }}
              />
              <button onClick={sendPlanMessage} disabled={planLoading || !planInput.trim()} style={{ background: planInput.trim() ? c.bark : c.sand, border: "none", color: planInput.trim() ? c.cream : c.mid, fontFamily: "system-ui, sans-serif", fontSize: "0.65rem", letterSpacing: "0.15em", textTransform: "uppercase", padding: "0.75rem 1.25rem", cursor: planInput.trim() ? "pointer" : "not-allowed", flexShrink: 0 }}>
                Send
              </button>
            </div>
          </div>

          {/* RIGHT — Itinerary */}
          <div style={{ flex: 1, overflowY: "auto", background: c.cream }}>
            {!itinerary ? (
              <div style={{ display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center", height: "100%", padding: "3rem", textAlign: "center" }}>
                <div style={{ width: 40, height: 1, background: c.gold, margin: "0 auto 2rem" }} />
                <div style={{ fontSize: "1.5rem", color: c.ink, marginBottom: "0.75rem" }}>Your itinerary will appear here</div>
                <div style={{ fontSize: "0.82rem", color: c.mid, fontFamily: "system-ui, sans-serif", fontWeight: 300, lineHeight: 1.8, maxWidth: 380 }}>Tell Deriva when you're going and how many nights — it'll build a full day-by-day plan using the best {result.name} has to offer. Ask it to change anything.</div>
              </div>
            ) : (
              <div style={{ padding: "3rem" }}>
                <div style={{ marginBottom: "2.5rem" }}>
                  <div style={{ fontSize: "0.58rem", letterSpacing: "0.3em", textTransform: "uppercase", color: c.gold, fontFamily: "system-ui, sans-serif", marginBottom: "0.5rem" }}>Your Deriva itinerary</div>
                  <div style={{ fontSize: "2rem", color: c.ink, marginBottom: "0.5rem" }}>{result.name}</div>
                  {itinerary.bestFor && <div style={{ fontSize: "0.85rem", color: c.mid, fontFamily: "system-ui, sans-serif", fontWeight: 300, fontStyle: "italic" }}>{itinerary.bestFor}</div>}
                  <div style={{ width: 30, height: 1, background: c.gold, marginTop: "1.5rem" }} />
                </div>
                {itinerary.days?.map((day, i) => (
                  <div key={i} style={{ marginBottom: "2.5rem", paddingBottom: "2.5rem", borderBottom: i < itinerary.days.length - 1 ? `1px solid ${c.sand}` : "none" }}>
                    <div style={{ display: "flex", alignItems: "baseline", gap: "1rem", marginBottom: "1.25rem" }}>
                      <div style={{ fontSize: "0.6rem", letterSpacing: "0.2em", textTransform: "uppercase", color: c.gold, fontFamily: "system-ui, sans-serif", flexShrink: 0 }}>Day {day.day}</div>
                      <div style={{ fontSize: "1.2rem", color: c.ink }}>{day.title}</div>
                    </div>
                    {[["Morning", day.morning], ["Afternoon", day.afternoon], ["Evening", day.evening], ["Stay", day.stay]].map(([label, text]) => text && (
                      <div key={label} style={{ marginBottom: "1rem", display: "flex", gap: "1rem" }}>
                        <div style={{ fontSize: "0.58rem", letterSpacing: "0.15em", textTransform: "uppercase", color: c.tan, fontFamily: "system-ui, sans-serif", paddingTop: "0.2rem", width: 64, flexShrink: 0 }}>{label}</div>
                        <div style={{ fontSize: "0.85rem", color: c.charcoal, fontFamily: "system-ui, sans-serif", fontWeight: 300, lineHeight: 1.7 }}>{text}</div>
                      </div>
                    ))}
                  </div>
                ))}
                {itinerary.notes?.length > 0 && (
                  <div style={{ background: c.bark, padding: "1.5rem 2rem" }}>
                    <div style={{ fontSize: "0.58rem", letterSpacing: "0.2em", textTransform: "uppercase", color: c.gold, fontFamily: "system-ui, sans-serif", marginBottom: "1rem" }}>Good to know</div>
                    {itinerary.notes.map((note, i) => (
                      <div key={i} style={{ fontSize: "0.82rem", color: c.tan, fontFamily: "system-ui, sans-serif", fontWeight: 300, lineHeight: 1.7, marginBottom: "0.5rem" }}>— {note}</div>
                    ))}
                  </div>
                )}
              </div>
            )}
          </div>
        </div>
      )}
    </div>
  );
}
