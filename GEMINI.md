# PLAN.md - Amsterdam LocationSearch Component

**Projekt:** Aplikacja Mapowa Amsterdamu
**Komponent:** LocationSearch
**Data Utworzenia:** [Wstaw dzisiejszą datę]
**Wersja:** 1.0

## 1. Cel (Objective)

Stworzenie interaktywnego komponentu `LocationSearch` dla aplikacji React + TypeScript + Tailwind CSS, umożliwiającego użytkownikom wyszukiwanie zabytków, adresów i wypożyczalni rowerów w Amsterdamie. Komponent będzie zintegrowany z mapą Leaflet, dynamicznie wyświetlając wyniki, centrując mapę i wyróżniając pobliskie wypożyczalnie rowerów.

## 2. Kluczowe Funkcjonalności (Key Features / Scope)

*   **[F1] Interaktywna Mapa:** Wyświetlanie mapy Amsterdamu za pomocą Leaflet.
*   **[F2] Pole Wyszukiwania:** Implementacja pola input dla zapytań użytkownika.
*   **[F3] Autouzupełnianie:** Dynamiczne sugestie (zabytki, adresy, wypożyczalnie) podczas pisania, z debouncingiem.
*   **[F4] Wyszukiwanie Lokalizacji:** Obsługa wyszukiwania różnych typów miejsc (POI, adresy, nazwy/dzielnice wypożyczalni).
*   **[F5] Centrowanie Mapy:** Automatyczne przesuwanie i zoomowanie mapy do wybranej lokalizacji z sugestii.
*   **[F6] Znacznik Centrum Wyszukiwania:** Wyświetlanie dedykowanego znacznika w punkcie centralnym wyszukiwania.
*   **[F7] Identyfikacja Pobliskich Wypożyczalni:** Obliczanie odległości i znajdowanie wypożyczalni w zdefiniowanym promieniu od centrum wyszukiwania.
*   **[F8] Wyróżnianie Wyników:**
    *   Specjalne, animowane znaczniki dla pobliskich wypożyczalni.
    *   Podniesienie wyróżnionych znaczników na wierzch (`zIndex`).
    *   Potencjalnie inne wyróżnienie, jeśli wyszukana lokalizacja jest *bezpośrednio* wypożyczalnią.
*   **[F9] Responsywność:** Zapewnienie poprawnego działania i wyglądu na różnych urządzeniach (mobile, tablet, desktop).
*   **[F10] UI/UX:** Czysty interfejs, umiejscowienie paska wyszukiwania na górze mapy, wizualne wskazówki (ładowanie, brak wyników), płynne animacje mapy i znaczników.

## 3. Technologia (Technology Stack)

*   **Frontend:** React (`create-react-app` lub Vite)
*   **Język:** TypeScript
*   **Styling:** Tailwind CSS
*   **Mapy:** Leaflet + React-Leaflet (lub bezpośrednia integracja Leaflet)
*   **Dane Statyczne:** JSON lub TS/JS moduły (dla wypożyczalni, zabytków)
*   **API Zewnętrzne (Potencjalnie):** API Geokodowania/Wyszukiwania Miejsc (np. OpenStreetMap Nominatim, Mapbox Geocoding, Pelias - do ustalenia, uwzględniając limity/koszty)

## 4. Architektura i Struktura Plików (Architecture & File Structure)

Zgodnie z propozycją:
Używaj kodu ostrożnie .
Obniżka cen
źródło/
├── składniki/
│
│ ├── indeks.tsx # Eksportuj komponentu
│ ├── LocationSearch.tsx # Gł
│ ├── SearchInput.tsx # Komponent pola wejściowego + autouzupełnianie
│ ├── MapView.tsx # Komponent mapy Ulotka
│ └── MarkerStyles.ts # Definicje/komponenty stylów
├── haki/
│ ├── useSearch.ts # Logika wyszukiwania, fetchowanie sugestii, obalanie
│ └── useMapInteractions.ts # Logika związana z mapą (centrowanie, powiększanie, znacznikowanie)
├── dane/
│ ├── lokalizacje.
│ ├── bikeRentals.ts # Dane rower rowerowy (np. w GeoJSON/JSON)
│ └── charakterystyczne obiekty.ts # Dane zabytków/POI (np. w GeoJSON
├── typy/
│ ├── Location.ts # Typy dla lokalizacji, POI
│ ├── BikeRental.ts # Typ dla wypożyczalni
│ └── SearchResult.ts # Typ dla wyników/sugestii wyszukiwania
└── narzędzia/
├──
└── mapHelpers.ts # Funkcje zastosowania dla Leaflet (np. tworzenie ikon)
*(Założenie: utrzymanie plików poniżej 300 linii kodu poprzez dekompozycję)*

## 5. Wymagane Dane (Data Requirements)

*   **[D1] Dane Wypożyczalni Rowerów:** Ustrukturyzowany plik (JSON/TS) z listą wypożyczalni: `id`, `name`, `latitude`, `longitude`, opcjonalnie `address`, `district`.
*   **[D2] Dane Zabytków/POI:** Podobny ustrukturyzowany plik dla kluczowych zabytków/atrakcji: `id`, `name`, `latitude`, `longitude`, `type: 'landmark'`.
*   **[D3] API Geokodowania/Wyszukiwania:** Endpoint API (lub biblioteka kliencka) do wyszukiwania adresów i potencjalnie innych POI nie zawartych w danych statycznych. Wymaga ewaluacji dostawców (OSM/Nominatim, Mapbox itp.).

## 6. Główne Zadania Implementacyjne (Implementation Tasks)

*   **[T1] Setup Podstawowy:**
    *   `[ ]` Stworzenie struktury folderów i plików zgodnie z planem.
    *   `[ ]` Instalacja zależności (Leaflet, React-Leaflet, typy).
    *   `[ ]` Podstawowa konfiguracja React + TypeScript + Tailwind.
*   **[T2] Komponent Mapy (`MapView.tsx`):**
    *   `[ ]` Inicjalizacja mapy Leaflet skoncentrowanej na Amsterdamie.
    *   `[ ]` Dodanie warstwy kafelków (np. OpenStreetMap).
    *   `[ ]` Zdefiniowanie podstawowych typów znaczników (`MarkerTypes.ts`).
    *   `[ ]` Implementacja funkcji do dodawania/usuwania/aktualizowania znaczników.
*   **[T3] Ładowanie Danych:**
    *   `[ ]` Zdefiniowanie struktur danych (`types/`).
    *   `[ ]` Stworzenie plików z danymi (`data/bikeRentals.ts`, `data/landmarks.ts`).
    *   `[ ]` Załadowanie danych i wyświetlenie *wszystkich* wypożyczalni i zabytków na mapie ze standardowymi znacznikami.
*   **[T4] Komponent Wyszukiwania (`SearchInput.tsx`):**
    *   `[ ]` Stworzenie pola input.
    *   `[ ]` Implementacja hooka `useSearch` (`hooks/useSearch.ts`) z logiką debouncingu.
    *   `[ ]` Logika pobierania sugestii (początkowo z danych statycznych, później z API).
    *   `[ ]` Wyświetlanie rozwijanej listy sugestii pod polem input.
    *   `[ ]` Obsługa wyboru sugestii (kliknięcie, klawiatura).
*   **[T5] Integracja Wyszukiwania z Mapą (`LocationSearch.tsx`, `useMapInteractions.ts`):**
    *   `[ ]` Po wybraniu sugestii, wywołanie funkcji z `useMapInteractions`.
    *   `[ ]` Implementacja funkcji centrowania mapy (`flyTo` lub `setView`) w `useMapInteractions`.
    *   `[ ]` Dodanie znacznika "centrum wyszukiwania" na wybranej lokalizacji.
*   **[T6] Logika Pobliskich Wypożyczalni:**
    *   `[ ]` Implementacja funkcji obliczania odległości (`utils/distance.ts`).
    *   `[ ]` W `LocationSearch` lub `useMapInteractions`, po wycentrowaniu mapy, obliczenie odległości od centrum do wszystkich wypożyczalni.
    *   `[ ]` Zdefiniowanie promienia wyszukiwania (np. 1km) i filtrowanie pobliskich wypożyczalni.
*   **[T7] Wyróżnianie Znaczników:**
    *   `[ ]` Zdefiniowanie stylów/ikon dla wyróżnionych (pobliskich) znaczników (`MarkerTypes.ts`, `mapHelpers.ts`).
    *   `[ ]` Implementacja logiki dynamicznej zmiany ikon/stylów znaczników na mapie w `MapView` na podstawie danych o bliskości.
    *   `[ ]` Implementacja animacji CSS (Tailwind) dla wyróżnionych znaczników.
    *   `[ ]` Zarządzanie `zIndex` (lub użycie `Pane` w Leaflet) dla wyróżnionych znaczników.
*   **[T8] Integracja API Zewnętrznego (Opcjonalnie/Później):**
    *   `[ ]` Wybór i konfiguracja dostawcy API geokodowania.
    *   `[ ]` Aktualizacja `useSearch` do pobierania sugestii adresów/POI z API.
    *   `[ ]` Obsługa odpowiedzi API i mapowanie na wewnętrzny format `SearchResult`.
*   **[T9] Styling i UI/UX:**
    *   `[ ]` Dopracowanie wyglądu komponentu wyszukiwania i sugestii (Tailwind).
    *   `[ ]` Implementacja wizualnych wskazówek (ładowanie, brak wyników).
    *   `[ ]` Zapewnienie responsywności layoutu.
    *   `[ ]` Użycie zdefiniowanej palety kolorów (#F97316, #3B82F6 itp.).
*   **[T10] Testowanie i Refaktoryzacja:**
    *   `[ ]` Testy jednostkowe (np. `distance.ts`, logika filtrowania).
    *   `[ ]` Testy manualne interakcji użytkownika.
    *   `[ ]` Przegląd kodu, refaktoryzacja, optymalizacja.
    *   `[ ]` Dodanie komentarzy i dokumentacji w kodzie.

## 7. Design (UI/UX Considerations)

*   **Paleta Kolorów:** Główny pomarańczowy (#F97316), wtórny niebieski (#3B82F6), neutralne szarości, kolory statusów (success, warning, error).
*   **Typografia:** Czytelna czcionka (np. Inter, systemowa) z odpowiednim kontrastem.
*   **Interfejs:** Minimalistyczny, intuicyjny. Pasek wyszukiwania z ikoną, wyraźna lista sugestii.
*   **Animacje:** Subtelne animacje dla wyróżnionych znaczników (pulsowanie?), płynne przejścia mapy (`flyTo`).
*   **Markery:** Wizualnie odróżnialne ikony dla wypożyczalni, zabytków i znacznika centrum wyszukiwania. Wyróżnione znaczniki powinny być wyraźnie większe/jaśniejsze/animowane.
*   **Responsywność:** Adaptacja layoutu paska wyszukiwania i mapy do różnych szerokości ekranu.

## 8. Potencjalne Wyzwania (Potential Challenges & Risks)

*   **Wydajność:** Obliczanie odległości dla wielu (setek?) wypożyczalni przy każdym wyszukiwaniu. Optymalizacja może być potrzebna (np. użycie Web Workers, ograniczenie obliczeń do widocznego obszaru mapy).
*   **API Zewnętrzne:** Limity zapytań, koszty, niezawodność i dokładność danych geokodowania.
*   **Zarządzanie Stanem:** Utrzymanie spójności stanu między wyszukiwaniem, mapą a danymi.
*   **Leaflet/React-Leaflet:** Potencjalne niuanse integracji i zarządzania cyklem życia komponentów mapowych w React.
*   **Jakość Danych:** Kompletność i dokładność danych statycznych o wypożyczalniach i zabytkach.

## 9. Przyszłe Rozszerzenia (Future Enhancements)

*   Filtrowanie wypożyczalni (godziny otwarcia, typ rowerów).
*   Wyświetlanie szczegółów po kliknięciu znacznika (Popup/Panel).
*   Integracja z nawigacją.
*   Wyszukiwanie "w pobliżu mnie" (geolokalizacja).
*   Zapisywanie ostatnich/ulubionych wyszukiwań.
