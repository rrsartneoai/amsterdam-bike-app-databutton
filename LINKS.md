## 1. https://readdy.site/share/a2e390c88078ee0099acb214ff42cf83

<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BLACK BIKES - Wypożyczalnia rowerów</title>
<script src="https://cdn.tailwindcss.com/3.4.16"></script>
<script>tailwind.config={theme:{extend:{colors:{primary:'#ff5252',secondary:'#333333'},borderRadius:{'none':'0px','sm':'8px',DEFAULT:'12px','md':'16px','lg':'20px','xl':'24px','2xl':'28px','3xl':'32px','full':'9999px','button':'12px'}}}}</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700&family=Pacifico&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/remixicon/4.6.0/remixicon.min.css">
<style>
:where([class^="ri-"])::before { content: "\f3c2"; }
body {
background-color: #1a1a1a;
color: #ffffff;
font-family: 'Montserrat', sans-serif;
}
.shadow-custom {
box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
}
.glass-effect {
background: rgba(26, 26, 26, 0.8);
backdrop-filter: blur(12px);
border: 1px solid rgba(255, 255, 255, 0.1);
}
.map-container {
height: 600px;
background-size: cover;
background-position: center;
transition: background-image 0.3s ease;
}
.map-view {
background-image: url('https://readdy.ai/api/search-image?query=A%20detailed%20map%20of%20Amsterdam%20city%20center%20with%20streets%2C%20canals%2C%20and%20landmarks%20visible.%20The%20map%20has%20a%20clean%2C%20modern%20design%20with%20light%20background%20and%20dark%20street%20lines.%20Red%20pin%20markers%20are%20scattered%20across%20the%20map%20indicating%20bike%20rental%20locations.%20The%20map%20shows%20the%20detailed%20street%20network%20of%20Amsterdam&width=800&height=600&seq=1&orientation=landscape');
}
.satellite-view {
background-image: url('https://readdy.ai/api/search-image?query=A%20satellite%20view%20of%20Amsterdam%20city%20center%20showing%20the%20actual%20aerial%20photography%20of%20the%20city.%20The%20image%20clearly%20shows%20buildings%2C%20canals%2C%20and%20streets%20from%20above.%20The%20image%20has%20high%20resolution%20and%20shows%20real-world%20details%20of%20Amsterdams%20urban%20landscape&width=800&height=600&seq=2&orientation=landscape');
}
.location-marker {
position: relative;
width: 40px;
height: 40px;
cursor: pointer;
display: flex;
align-items: center;
justify-content: center;
}
.location-marker i {
font-size: 24px;
color: #ff5252;
filter: drop-shadow(0 0 8px rgba(255, 82, 82, 0.4));
animation: markerPulse 2s infinite;
}
@keyframes markerPulse {
0% { transform: scale(1); filter: drop-shadow(0 0 8px rgba(255, 82, 82, 0.4)); }
50% { transform: scale(1.2); filter: drop-shadow(0 0 12px rgba(255, 82, 82, 0.6)); }
100% { transform: scale(1); filter: drop-shadow(0 0 8px rgba(255, 82, 82, 0.4)); }
}
.table-row-alt:nth-child(odd) {
background-color: #2a2a2a;
}
.table-row-alt:nth-child(even) {
background-color: #333333;
}
</style>
</head>
<body class="min-h-screen">
<!-- Header -->
<header class="bg-black text-white py-4 border-b border-gray-800">
<div class="container mx-auto px-4 flex justify-between items-center">
<div class="flex items-center">
<div class="w-16 h-16 bg-primary rounded-full flex items-center justify-center mr-4">
<i class="ri-bike-line ri-2x text-white"></i>
</div>
<h1 class="text-2xl font-bold">BLACK BIKES<span class="text-primary">.</span></h1>
</div>
<div class="flex items-center">
<div class="flex items-center mr-6">
<div class="flex">
<i class="ri-star-fill text-yellow-400"></i>
<i class="ri-star-fill text-yellow-400"></i>
<i class="ri-star-fill text-yellow-400"></i>
<i class="ri-star-fill text-yellow-400"></i>
<i class="ri-star-half-fill text-yellow-400"></i>
</div>
<span class="ml-2">1 454 opinii</span>
</div>
<div class="flex items-center">
<button class="bg-gray-800 px-4 py-2 rounded-l-button">
<img src="https://readdy.ai/api/search-image?query=Polish%20flag%2C%20rectangular%20shape%2C%20red%20and%20white%20colors%2C%20simple%20design&width=24&height=16&seq=2&orientation=landscape" alt="Polski" class="w-6 h-4">
</button>
<button class="bg-gray-700 px-4 py-2 rounded-r-button">
<img src="https://readdy.ai/api/search-image?query=UK%20flag%2C%20rectangular%20shape%2C%20red%2C%20white%20and%20blue%20colors%2C%20simple%20design&width=24&height=16&seq=3&orientation=landscape" alt="English" class="w-6 h-4">
</button>
</div>
</div>
</div>
</header>
<!-- Navigation -->
<nav class="bg-black text-white py-3 border-b border-gray-800">
<div class="container mx-auto px-4 flex justify-between items-center">
<div class="flex space-x-6">
<a href="#" class="hover:text-primary">DOM</a>
<div class="relative group" id="bikesDropdown">
<button class="flex items-center hover:text-primary">
ROWERY
<i class="ri-arrow-down-s-line ml-1"></i>
</button>
<div class="dropdown-menu hidden absolute left-0 mt-2 w-72 bg-gray-800 border border-gray-700 rounded-lg shadow-lg z-50">
<div class="py-2">
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-bike-line"></i>
<span>Rowery miejskie</span>
</a>
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-flashlight-line"></i>
<span>Rowery elektryczne</span>
</a>
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-parent-line"></i>
<span>Rowery dziecięce</span>
</a>
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-truck-line"></i>
<span>Rowery cargo</span>
</a>
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-group-line"></i>
<span>Rowery tandem</span>
</a>
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-road-map-line"></i>
<span>Rowery trekkingowe</span>
</a>
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-mountain-line"></i>
<span>Rowery górskie</span>
</a>
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-run-line"></i>
<span>Rowery wyścigowe</span>
</a>
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-wheelchair-line"></i>
<span>Rowery adaptacyjne</span>
</a>
<a href="#" class="block px-4 py-2 text-sm hover:bg-gray-700 hover:text-primary flex items-center gap-3">
<i class="ri-tools-line"></i>
<span>Akcesoria rowerowe</span>
</a>
</div>
</div>
</div>
<a href="https://readdy.ai/home/15b4db5b-f8fe-46b9-8c58-6de162b8a278/5d083560-d978-4fe6-9dc7-ee9bc09e6fff" data-readdy="true" class="hover:text-primary">20 LOKALIZACJI</a>
</div>
<div class="flex space-x-6">
<a href="#" class="hover:text-primary">CZĘSTO ZADAWANE PYTANIA</a>
<a href="#" class="hover:text-primary">PRACA</a>
<a href="#" class="hover:text-primary">SKONTAKTUJ SIĘ Z NAMI</a>
</div>
</div>
</nav>
<!-- Breadcrumbs -->
<div class="bg-gray-900 py-2">
<div class="container mx-auto px-4">
<div class="flex items-center text-sm">
<a href="#" class="text-primary">Dom</a>
<span class="mx-2 text-gray-500">|</span>
<span class="text-gray-400">Lokalizacje</span>
</div>
</div>
</div>
<!-- Main Content -->
<main class="container mx-auto px-4 py-6">
<h1 class="text-3xl font-bold mb-6">LOKALIZACJE WYPOŻYCZALNI ROWERÓW</h1>
<div class="flex flex-col lg:flex-row gap-6">
<!-- Map Section -->
<div class="w-full lg:w-1/2">
<div class="bg-gray-800 rounded-lg overflow-hidden shadow-custom">
<div class="flex border-b border-gray-700 p-1 m-2 bg-gray-900 rounded-button">
<button id="mapViewBtn" class="flex-1 px-4 py-2 text-white bg-gray-700 rounded-button transition-all duration-300 hover:bg-gray-600">Karta</button>
<button id="satelliteViewBtn" class="flex-1 px-4 py-2 text-gray-400 rounded-button transition-all duration-300 hover:bg-gray-700">Sputantnik</button>
</div>
<div id="mapContainer" class="relative map-container">
<!-- Map markers -->
<div class="location-marker absolute" style="top: 45%; left: 40%"><i class="ri-bike-fill"></i></div>
<div class="location-marker absolute" style="top: 35%; left: 50%"><i class="ri-bike-fill"></i></div>
<div class="location-marker absolute" style="top: 55%; left: 60%"><i class="ri-bike-fill"></i></div>
<div class="location-marker absolute" style="top: 30%; left: 30%"><i class="ri-bike-fill"></i></div>
<div class="location-marker absolute" style="top: 60%; left: 45%"><i class="ri-bike-fill"></i></div>
<div class="location-marker absolute" style="top: 50%; left: 70%"><i class="ri-bike-fill"></i></div>
<div class="location-marker absolute" style="top: 40%; left: 65%"><i class="ri-bike-fill"></i></div>
<!-- Map controls -->
<div class="absolute top-2 right-2 flex flex-col space-y-2">
<button class="w-8 h-8 bg-white rounded-button flex items-center justify-center text-black">
<i class="ri-add-line"></i>
</button>
<button class="w-8 h-8 bg-white rounded-button flex items-center justify-center text-black">
<i class="ri-subtract-line"></i>
</button>
<button class="w-8 h-8 bg-white rounded-button flex items-center justify-center text-black">
<i class="ri-fullscreen-line"></i>
</button>
</div>
<!-- Location popup -->
<div class="absolute glass-effect text-white p-4 rounded-lg shadow-custom" style="top: 35%; left: 50%; transform: translate(-50%, -120%); min-width: 240px;">
<div class="flex items-center gap-2 mb-2">
<i class="ri-map-pin-2-fill text-primary"></i>
<div class="text-sm font-semibold">Wypożyczalnia rowerów Vondelpark</div>
</div>
<div class="text-xs text-gray-300">Eerste Constantijn Huygensstraat 88 (róg Overtoom)</div>
<div class="mt-3 flex justify-between items-center">
<span class="text-xs bg-primary/20 text-primary px-2 py-1 rounded-full">Otwarte</span>
<button class="text-xs text-primary hover:underline">Zobacz szczegóły →</button>
</div>
<div class="absolute bottom-0 left-1/2 transform translate-x(-50%) translate-y(100%) w-0 h-0 border-l-8 border-r-8 border-t-8 border-transparent border-t-[rgba(26,26,26,0.8)]"></div>
</div>
</div>
</div>
</div>
<!-- Locations Table -->
<div class="w-full lg:w-1/2">
<div class="bg-gray-800 rounded overflow-hidden">
<table class="w-full">
<thead>
<tr class="bg-gray-900/50 text-left border-b border-gray-700">
<th class="px-6 py-4 text-sm font-medium text-gray-300">Sklep</th>
<th class="px-6 py-4 text-sm font-medium text-gray-300">Adres</th>
<th class="px-6 py-4 text-sm font-medium text-gray-300">Kod pocztowy</th>
<th class="px-6 py-4 text-sm font-medium text-gray-300">Połączyć</th>
</tr>
</thead>
<tbody>
<tr class="table-row-alt border-b border-gray-700">
<td class="px-4 py-3">
<div>Wypożyczalnia rowerów Amsterdam</div>
<div class="text-sm text-gray-400">Sloterdijk</div>
</td>
<td class="px-4 py-3">Droga rowerowa 472</td>
<td class="px-4 py-3">1043 NV</td>
<td class="px-6 py-4">
<button class="px-4 py-2 bg-primary/10 text-primary rounded-button text-sm font-medium hover:bg-primary/20 transition-all duration-300 flex items-center gap-2">
<span>Szczegóły</span>
<i class="ri-arrow-right-line"></i>
</button>
</td>
</tr>
<tr class="table-row-alt border-b border-gray-700">
<td class="px-4 py-3">
<div>Wypożyczalnia rowerów Amsterdam</div>
<div class="text-sm text-gray-400">Centraal Station</div>
</td>
<td class="px-4 py-3">Książę Hendrikkade 14</td>
<td class="px-4 py-3">1012 TK</td>
<td class="px-6 py-4">
<button class="px-4 py-2 bg-primary/10 text-primary rounded-button text-sm font-medium hover:bg-primary/20 transition-all duration-300 flex items-center gap-2">
<span>Szczegóły</span>
<i class="ri-arrow-right-line"></i>
</button>
</td>
</tr>
<tr class="table-row-alt border-b border-gray-700">
<td class="px-4 py-3">
<div>Wypożyczalnia rowerów Amsterdam Dam</div>
<div class="text-sm text-gray-400">Square</div>
</td>
<td class="px-4 py-3">Nieuwezijds Voorburgwal 146 (w pobliżu Placu Dam)</td>
<td class="px-4 py-3">1012 SJ</td>
<td class="px-6 py-4">
<button class="px-4 py-2 bg-primary/10 text-primary rounded-button text-sm font-medium hover:bg-primary/20 transition-all duration-300 flex items-center gap-2">
<span>Szczegóły</span>
<i class="ri-arrow-right-line"></i>
</button>
</td>
</tr>
<tr class="table-row-alt border-b border-gray-700">
<td class="px-4 py-3">
<div>Wypożyczalnia rowerów Dzielnica</div>
<div class="text-sm text-gray-400">czerwonych latarń</div>
</td>
<td class="px-4 py-3">Oudezijdsplein 62 (róg Oudezijds Voorburgwal)</td>
<td class="px-4 py-3">1012 HA</td>
<td class="px-6 py-4">
<button class="px-4 py-2 bg-primary/10 text-primary rounded-button text-sm font-medium hover:bg-primary/20 transition-all duration-300 flex items-center gap-2">
<span>Szczegóły</span>
<i class="ri-arrow-right-line"></i>
</button>
</td>
</tr>
<tr class="table-row-alt border-b border-gray-700">
<td class="px-4 py-3">
<div>Wypożyczalnia rowerów „J Ulic"</div>
</td>
<td class="px-4 py-3">Wolvenstraat 18 („9 Stocznia" / „9 Ulic")</td>
<td class="px-4 py-3">1016 EP</td>
<td class="px-6 py-4">
<button class="px-4 py-2 bg-primary/10 text-primary rounded-button text-sm font-medium hover:bg-primary/20 transition-all duration-300 flex items-center gap-2">
<span>Szczegóły</span>
<i class="ri-arrow-right-line"></i>
</button>
</td>
</tr>
<tr class="table-row-alt border-b border-gray-700">
<td class="px-4 py-3">
<div>Wypożyczalnia rowerów Vondelpark</div>
</td>
<td class="px-4 py-3">Eerste Constantijn Huygensstraat 88 (róg Overtoom)</td>
<td class="px-4 py-3">1054 BX</td>
<td class="px-6 py-4">
<button class="px-4 py-2 bg-primary/10 text-primary rounded-button text-sm font-medium hover:bg-primary/20 transition-all duration-300 flex items-center gap-2">
<span>Szczegóły</span>
<i class="ri-arrow-right-line"></i>
</button>
</td>
</tr>
<tr class="table-row-alt border-b border-gray-700">
<td class="px-4 py-3">
<div>Wypożyczalnia rowerów Leidseplein</div>
</td>
<td class="px-4 py-3">Lijnbaansgracht 283 (róg Spiegelgracht)</td>
<td class="px-4 py-3">1087 MA</td>
<td class="px-6 py-4">
<button class="px-4 py-2 bg-primary/10 text-primary rounded-button text-sm font-medium hover:bg-primary/20 transition-all duration-300 flex items-center gap-2">
<span>Szczegóły</span>
<i class="ri-arrow-right-line"></i>
</button>
</td>
</tr>
<tr class="table-row-alt border-b border-gray-700">
<td class="px-4 py-3">
<div>Wypożyczalnia rowerów De Pijp</div>
</td>
<td class="px-4 py-3">Ferdinand Bolstraat 8</td>
<td class="px-4 py-3">1072 LJ</td>
<td class="px-6 py-4">
<button class="px-4 py-2 bg-primary/10 text-primary rounded-button text-sm font-medium hover:bg-primary/20 transition-all duration-300 flex items-center gap-2">
<span>Szczegóły</span>
<i class="ri-arrow-right-line"></i>
</button>
</td>
</tr>
<tr class="table-row-alt">
<td class="px-4 py-3">
<div>Wypożyczalnia rowerów Amsterdam</div>
<div class="text-sm text-gray-400">Muiderpoort</div>
</td>
<td class="px-4 py-3">Teren od Czociejgińskich 1a</td>
<td class="px-4 py-3">1093 Uwaga</td>
<td class="px-6 py-4">
<button class="px-4 py-2 bg-primary/10 text-primary rounded-button text-sm font-medium hover:bg-primary/20 transition-all duration-300 flex items-center gap-2">
<span>Szczegóły</span>
<i class="ri-arrow-right-line"></i>
</button>
</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</main>
<script>
document.addEventListener('DOMContentLoaded', function() {
const bikesDropdown = document.getElementById('bikesDropdown');
const dropdownButton = bikesDropdown.querySelector('button');
const dropdownMenu = bikesDropdown.querySelector('.dropdown-menu');
let isDropdownOpen = false;
dropdownButton.addEventListener('click', (e) => {
e.preventDefault();
isDropdownOpen = !isDropdownOpen;
if (isDropdownOpen) {
dropdownMenu.classList.remove('hidden');
} else {
dropdownMenu.classList.add('hidden');
}
});
document.addEventListener('click', (e) => {
if (!bikesDropdown.contains(e.target) && isDropdownOpen) {
dropdownMenu.classList.add('hidden');
isDropdownOpen = false;
}
});
const mapViewBtn = document.getElementById('mapViewBtn');
const satelliteViewBtn = document.getElementById('satelliteViewBtn');
const mapContainer = document.getElementById('mapContainer');
mapContainer.classList.add('map-view');
mapViewBtn.addEventListener('click', function() {
mapViewBtn.classList.remove('text-gray-400');
mapViewBtn.classList.add('text-white', 'bg-gray-700');
satelliteViewBtn.classList.remove('text-white', 'bg-gray-700');
satelliteViewBtn.classList.add('text-gray-400');
mapContainer.classList.remove('satellite-view');
mapContainer.classList.add('map-view');
});
satelliteViewBtn.addEventListener('click', function() {
satelliteViewBtn.classList.remove('text-gray-400');
satelliteViewBtn.classList.add('text-white', 'bg-gray-700');
mapViewBtn.classList.remove('text-white', 'bg-gray-700');
mapViewBtn.classList.add('text-gray-400');
mapContainer.classList.remove('map-view');
mapContainer.classList.add('satellite-view');
});
const markers = document.querySelectorAll('.location-marker');
markers.forEach(marker => {
marker.addEventListener('mouseenter', function() {
this.style.transform = 'scale(1.5)';
this.style.zIndex = '10';
});
marker.addEventListener('mouseleave', function() {
this.style.transform = 'scale(1)';
this.style.zIndex = '1';
});
marker.addEventListener('click', function() {
// Tutaj można dodać funkcjonalność wyświetlania szczegółów lokalizacji
});
});
});
</script>
</body>
</html>



