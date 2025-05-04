# PLAN.md - Komponent Wyszukiwania Lokalizacji (LocationSearch)

## 1. Cel i Zakres

**Cel:** Stworzenie komponentu `LocationSearch` w aplikacji mapowej, który umożliwi użytkownikom efektywne wyszukiwanie różnych typów lokalizacji w Amsterdamie (zabytki, atrakcje, adresy, wypożyczalnie rowerów) i natychmiastowe wizualizowanie powiązanych (pobliskich) wypożyczalni rowerów na mapie.

**Zakres:**
*   Implementacja pola wyszukiwania z funkcją autouzupełniania.
*   Integracja z API geokodowania/wyszukiwania miejsc.
*   Obsługa wyszukiwania:
    *   Zabytków i atrakcji turystycznych (POI - Points of Interest).
    *   Konkretnych adresów.
    *   Wypożyczalni rowerów (po nazwie lub dzielnicy - jeśli dane na to pozwalają).
*   Dynamiczne centrowanie mapy na wybranej lokalizacji.
*   Wyświetlanie znacznika wskazującego centrum wyszukiwania.
*   Identyfikacja i wizualne wyróżnienie wypożyczalni rowerów w pobliżu centrum wyszukiwania.
*   Specjalne wyróżnienie znacznika, jeśli wyszukiwana lokalizacja jest *bezpośrednio* wypożyczalnią rowerów.
*   Umiejscowienie komponentu wyszukiwania w górnej części interfejsu mapy.

## 2. Kluczowe Funkcjonalności (Szczegółowo)

1.  **Pole Wyszukiwania z Autouzupełnianiem:**
    *   Pojedyncze pole tekstowe (`<input type="text">`).
    *   Podczas wpisywania przez użytkownika, zapytania są wysyłane (z debouncing'iem) do API geokodowania/wyszukiwania.
    *   Wyświetlanie rozwijanej listy sugestii pod polem wyszukiwania.
    *   Sugestie powinny zawierać nazwę miejsca i ewentualnie dodatkowy kontekst (np. typ: "Zabytk", "Adres", "Wypożyczalnia rowerów", "Dzielnica").
    *   Obsługa wyboru sugestii myszką lub klawiaturą (strzałki, Enter).

2.  **Integracja API Wyszukiwania:**
    *   Wykorzystanie zewnętrznego API (np. Mapbox Geocoding, OpenStreetMap Nominatim, Pelias, Google Places API - z uwzględnieniem kosztów i limitów) lub wewnętrznego endpointu API.
    *   API musi wspierać wyszukiwanie POI, adresów i potencjalnie nazw firm (dla wypożyczalni).
    *   API powinno zwracać co najmniej: nazwę, współrzędne geograficzne (szerokość, długość), typ miejsca i ewentualnie granice (bounding box).

3.  **Centrowanie Mapy i Znacznik Centrum:**
    *   Po wybraniu sugestii, mapa powinna płynnie przesuwać się i powiększać (`flyTo` lub `setView`) do współrzędnych zwróconych przez API.
    *   Na dokładnych współrzędnych wybranej lokalizacji powinien pojawić się dedykowany, wyraźny znacznik ("Search Center Marker"), aby użytkownik wiedział, co stanowiło centrum wyszukiwania.

4.  **Wyszukiwanie Pobliskich Wypożyczalni Rowerów:**
    *   Po wycentrowaniu mapy na wyniku wyszukiwania (lub wybraniu lokalizacji), komponent musi przetworzyć ten wynik.
    *   Pobranie współrzędnych centrum wyszukiwania.
    *   Iteracja po liście *wszystkich* dostępnych wypożyczalni rowerów (załadowanych wcześniej lub pobranych z API).
    *   Obliczenie odległości (np. za pomocą formuły Haversine'a lub wbudowanych funkcji biblioteki mapowej) między centrum wyszukiwania a każdą wypożyczalnią.
    *   Zdefiniowanie promienia wyszukiwania (np. 1 km, 1.5 km - do ustalenia).
    *   Identyfikacja wypożyczalni znajdujących się w zdefiniowanym promieniu.

5.  **Wizualne Wyróżnienie Wypożyczalni:**
    *   **Wypożyczalnie w pobliżu:** Znaczniki zidentyfikowanych pobliskich wypożyczalni powinny zostać wizualnie wyróżnione:
        *   Użycie specjalnej ikony (np. większa, inny kolor, ikona z animacją pulsowania).
        *   Zwiększenie `zIndex` znacznika, aby był widoczny nad innymi (jeśli się pokrywają).
    *   **Bezpośrednio wyszukana wypożyczalnia:** Jeśli użytkownik wyszukał *konkretną* wypożyczalnię (np. po nazwie) i wybrał ją z sugestii, jej znacznik (który jest jednocześnie "Search Center Marker") powinien być również specjalnie oznaczony, ale potencjalnie inaczej niż tylko "pobliskie".
    *   Znaczniki wypożyczalni *nie* pasujących do kryteriów (za daleko) powinny pozostać w standardowym stylu lub zostać stonowane.

6.  **Pozycjonowanie UI:**
    *   Komponent wyszukiwania (pole tekstowe i lista sugestii) powinien być umieszczony jako nakładka na mapę, w górnej części ekranu (np. górny środek, górny lewy róg), aby był łatwo dostępny bez zasłaniania kluczowych obszarów mapy.

## 3. Implementacja Techniczna (Propozycje)

*   **Framework/Biblioteki:** React (lub inny wybrany framework), biblioteka mapowa (Leaflet, Mapbox GL JS, Google Maps API).
*   **Zarządzanie Stanem:** Lokalny stan komponentu (`useState`, `useReducer`) lub globalny (Context API, Redux, Zustand) do przechowywania wyników wyszukiwania, statusu ładowania, współrzędnych centrum, listy pobliskich wypożyczalni.
*   **Debouncing:** Użycie `lodash.debounce` lub implementacja własna (np. z `setTimeout`/`clearTimeout`) dla zapytań API podczas pisania w polu wyszukiwania, aby uniknąć nadmiernych żądań.
*   **Dane Wypożyczalni:** Prawdopodobnie statyczny plik JSON lub dedykowany endpoint API dostarczający listę wypożyczalni (nazwa, adres, współrzędne, ew. dzielnica). Dane te powinny być dostępne w komponencie mapy.
*   **Obliczanie Odległości:** Funkcja pomocnicza implementująca formułę Haversine'a lub wykorzystanie wbudowanych funkcji biblioteki mapowej (np. `distanceTo` w Leaflet).
*   **Styling Znaczników:** Dynamiczne przypisywanie klas CSS lub stylów inline do znaczników w zależności od tego, czy są "pobliskie", "centrum wyszukiwania", czy "standardowe". Wykorzystanie CSS do animacji (np. `@keyframes` dla pulsowania).
*   **Interakcja z Mapą:** Wykorzystanie API biblioteki mapowej do:
    *   Dodawania/usuwania/aktualizowania znaczników.
    *   Zmiany ikon/stylów znaczników.
    *   Manipulacji widokiem mapy (`setView`, `flyTo`).
    *   Zarządzania `zIndex` znaczników (lub użycia warstw/paneli w Leaflet/Mapbox).

## 4. Wymagane Dane

*   **API Geokodowania/Wyszukiwania:** Klucz API (jeśli wymagany), dokumentacja punktów końcowych.
*   **Lista Wypożyczalni Rowerów:** Ustrukturyzowany format (np. GeoJSON, JSON) zawierający co najmniej:
    *   `id`: Unikalny identyfikator.
    *   `name`: Nazwa wypożyczalni.
    *   `latitude`: Szerokość geograficzna.
    *   `longitude`: Długość geograficzna.
    *   `address` (opcjonalnie): Adres tekstowy.
    *   `district` (opcjonalnie): Dzielnica (do filtrowania/wyszukiwania).

## 5. Interfejs Użytkownika (UI) / Doświadczenie Użytkownika (UX)

*   **Wygląd:** Czysty i intuicyjny design pola wyszukiwania i listy sugestii, spójny z resztą aplikacji.
*   **Feedback:** Wskazanie stanu ładowania podczas zapytań API (np. spinner w polu wyszukiwania). Komunikat, gdy nie znaleziono wyników lub brak pobliskich wypożyczalni.
*   **Płynność:** Animacje przejścia mapy (`flyTo`) i wyróżnienia znaczników powinny być płynne.
*   **Dostępność:** Obsługa nawigacji klawiaturą w liście sugestii, odpowiednie atrybuty ARIA.
*   **Responsywność:** Komponent musi dobrze wyglądać i działać na różnych rozmiarach ekranu.

## 6. Potencjalne Wyzwania i Uwagi

*   **Wydajność:** Obliczanie odległości dla dużej liczby wypożyczalni przy każdym wyszukiwaniu może być kosztowne. Optymalizacja może być konieczna (np. wstępne filtrowanie po bounding box). Animowanie wielu znaczników może wpłynąć na wydajność.
*   **Jakość Danych API:** Dokładność i kompletność danych z API geokodowania (czy zawiera wszystkie POI, czy dobrze rozpoznaje adresy?).
*   **Limity i Koszty API:** Zewnętrzne API często mają limity użycia lub są płatne. Należy monitorować użycie i zaimplementować odpowiednie strategie (debouncing, caching po stronie klienta - jeśli dozwolone).
*   **Obsługa Wieloznaczności:** Co jeśli wyszukiwanie pasuje do wielu typów miejsc (np. nazwa ulicy i nazwa zabytku są takie same)? Jak prezentować sugestie?
*   **Aktualność Danych Wypożyczalni:** Proces aktualizacji listy wypożyczalni.
*   **Definicja "Pobliża":** Dobór odpowiedniego promienia wyszukiwania może wymagać testów i dostosowań.

## 7. Przyszłe Rozszerzenia (Opcjonalnie)

*   Filtrowanie wypożyczalni (np. po typie rowerów, godzinach otwarcia - jeśli dane dostępne).
*   Wyświetlanie szczegółów wypożyczalni po kliknięciu znacznika (popup/panel boczny).
*   Integracja z nawigacją (wyznaczanie trasy do wybranej wypożyczalni).
*   Wyszukiwanie "blisko mnie" na podstawie lokalizacji użytkownika.
*   Zapisywanie ulubionych/ostatnich wyszukiwań.

## 8. Zadania / Kamienie Milowe

1.  **Setup:** Utworzenie struktury komponentu `LocationSearch`. Integracja z podstawową mapą.
2.  **UI:** Implementacja pola wyszukiwania i statycznej listy sugestii (placeholder).
3.  **Dane:** Załadowanie i wyświetlenie *wszystkich* wypożyczalni rowerów na mapie ze standardowymi znacznikami.
4.  **API:** Integracja z wybranym API geokodowania/wyszukiwania.
5.  **Autouzupełnianie:** Implementacja dynamicznego pobierania i wyświetlania sugestii z API (wraz z debouncingiem).
6.  **Interakcja:** Obsługa wyboru sugestii -> centrowanie mapy (`flyTo`) -> wyświetlenie znacznika centrum wyszukiwania.
7.  **Logika Pobliża:** Implementacja funkcji obliczania odległości i identyfikacji pobliskich wypożyczalni (na podstawie zdefiniowanego promienia).
8.  **Wyróżnianie:** Implementacja dynamicznej zmiany stylów/ikon znaczników dla pobliskich wypożyczalni i bezpośrednio wyszukanej wypożyczalni. Zarządzanie `zIndex`.
9.  **Styling i UX:** Dopracowanie wyglądu, animacji, feedbacku dla użytkownika, responsywności.
10. **Testy:** Testy jednostkowe (np. funkcja obliczania odległości), testy integracyjne (komponent + mapa + API mock), testy E2E (symulacja akcji użytkownika).
11. **Refaktoryzacja i Dokumentacja:** Czyszczenie kodu, dodanie komentarzy, aktualizacja dokumentacji.
