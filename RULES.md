Instrukcja Kodowania Roo: Tworzenie Wysokiej Jakości Oprogramowania
Cześć! Jestem Roo. Przez lata pracy w branży widziałem wiele kodu – dobrego i złego. Celem tej instrukcji jest pomoc w pisaniu kodu, który jest nie tylko funkcjonalny, ale także czytelny, bezpieczny, łatwy w utrzymaniu i elastyczny. Stosowanie się do tych zasad pozwoli tworzyć lepsze oprogramowanie i ułatwi współpracę w zespole.
1. Czytelność Kodu (Readability)
Kod jest czytany znacznie częściej, niż jest pisany. Optymalizuj pod kątem osoby, która będzie go czytać w przyszłości (może to być Twój przyszły ja!).
Znaczące Nazewnictwo:
Używaj pełnych, opisowych nazw dla zmiennych, funkcji, klas i metod. Unikaj skrótów (chyba że są powszechnie znane i akceptowane w danym kontekście, np. i dla iteratora pętli).
Nazwa powinna jasno komunikować intencję i rolę danego elementu. calculateTotalPriceWithTax jest lepsze niż calc.
Stosuj spójne konwencje nazewnicze (np. camelCase dla zmiennych i funkcji, PascalCase dla klas).
Konsekwentne Formatowanie:
Używaj spójnych wcięć (np. 4 spacje), odstępów i stylu zapisu.
Korzystaj z automatycznych narzędzi do formatowania (linters/formatters) jak Prettier, Black, Checkstyle, aby zapewnić jednolitość w całym projekcie.
Krótkie Funkcje i Metody:
Funkcje/metody powinny robić jedną rzecz i robić ją dobrze (patrz: Zasada Pojedynczej Odpowiedzialności - SRP).
Staraj się, aby były jak najkrótsze. Jeśli funkcja staje się zbyt długa, rozważ jej podział na mniejsze, pomocnicze funkcje.
Komentarze Wyjaśniające "Dlaczego", a Nie "Co":
Dobry kod często sam się dokumentuje dzięki czytelnym nazwom i strukturze.
Komentarze powinny wyjaśniać dlaczego coś zostało zrobione w określony sposób (np. złożona logika biznesowa, obejście problemu), a nie co kod robi (np. // Inkrementacja i jest złym komentarzem).
Dbaj o aktualność komentarzy – nieaktualny komentarz jest gorszy niż jego brak.
Unikaj Magicznych Wartości:
Nie używaj "magicznych" liczb czy napisów bezpośrednio w kodzie. Zamiast tego definiuj nazwane stałe (constants) lub enumeracje (enums). MAX_LOGIN_ATTEMPTS = 3 jest lepsze niż używanie 3 w wielu miejscach.
2. Bezpieczeństwo (Security)
Bezpieczeństwo nie jest dodatkiem, lecz fundamentalnym wymogiem. Należy o nim myśleć na każdym etapie tworzenia oprogramowania.
Ochrona przed Wstrzykiwaniem (Injection Prevention):
SQL Injection: Nigdy nie buduj zapytań SQL przez konkatenację stringów z danymi wejściowymi od użytkownika. Zawsze używaj zapytań parametryzowanych (prepared statements) lub sprawdzonych bibliotek ORM (Object-Relational Mapping), które robią to za Ciebie.
Cross-Site Scripting (XSS): Zawsze oczyszczaj (escape/sanitize) dane pochodzące od użytkownika przed wyświetleniem ich w interfejsie (np. na stronie HTML). Używaj mechanizmów dostarczanych przez frameworki (np. React, Angular, Vue, Django, Rails) lub dedykowanych bibliotek. Zwracaj uwagę na kontekst (HTML body, atrybut HTML, JavaScript).
Command Injection: Unikaj wykonywania poleceń systemowych na podstawie danych wejściowych użytkownika. Jeśli jest to absolutnie konieczne, bardzo rygorystycznie waliduj i oczyszczaj te dane. Najlepiej korzystać z funkcji API, które nie wymagają wywoływania zewnętrznej powłoki.
Walidacja Danych Wejściowych:
Waliduj wszystkie dane przychodzące z zewnątrz systemu (od użytkowników, z innych API, z plików). Sprawdzaj typ, format, długość, zakres wartości. Waliduj zarówno po stronie klienta (dla lepszego UX), jak i koniecznie po stronie serwera (dla bezpieczeństwa).
Nie ufaj żadnym danym przychodzącym z zewnątrz.
Zarządzanie Zależnościami:
Regularnie aktualizuj biblioteki i frameworki, z których korzystasz. Stare wersje mogą zawierać znane luki bezpieczeństwa.
Używaj narzędzi do skanowania zależności pod kątem znanych podatności (np. npm audit, pip check, OWASP Dependency-Check).
Zasada Najmniejszych Uprawnień (Principle of Least Privilege):
Procesy i użytkownicy powinni mieć tylko te uprawnienia, które są absolutnie niezbędne do wykonania ich zadań. Dotyczy to zarówno uprawnień w systemie operacyjnym, bazie danych, jak i w samej aplikacji.
Bezpieczne Przechowywanie Danych Wrażliwych:
Nigdy nie przechowuj haseł w postaci jawnego tekstu. Używaj silnych, powolnych algorytmów haszujących z solą (np. bcrypt, Argon2, scrypt).
Nie przechowuj kluczy API, haseł do baz danych itp. bezpośrednio w kodzie źródłowym. Używaj zmiennych środowiskowych, systemów zarządzania sekretami (np. HashiCorp Vault, AWS Secrets Manager).
3. Zasady SOLID
SOLID to akronim pięciu fundamentalnych zasad projektowania obiektowego, które pomagają tworzyć kod bardziej zrozumiały, elastyczny i łatwy w utrzymaniu.
S - Zasada Pojedynczej Odpowiedzialności (Single Responsibility Principle - SRP):
Klasa (lub moduł, funkcja) powinna mieć tylko jeden powód do zmiany, czyli jedną odpowiedzialność.
Przykład: Klasa User nie powinna jednocześnie zarządzać danymi użytkownika i wysyłać e-maili powitalnych. Wysyłanie e-maili to osobna odpowiedzialność.
O - Zasada Otwarte/Zamknięte (Open/Closed Principle - OCP):
Oprogramowanie (klasy, moduły, funkcje) powinno być otwarte na rozszerzenia, ale zamknięte na modyfikacje.
Osiąga się to często przez użycie abstrakcji (interfejsów, klas abstrakcyjnych) i polimorfizmu. Nową funkcjonalność dodaje się przez tworzenie nowych klas implementujących istniejące interfejsy, a nie przez modyfikację istniejącego, działającego kodu.
L - Zasada Podstawienia Liskov (Liskov Substitution Principle - LSP):
Funkcje, które używają wskaźników lub referencji do klas bazowych, muszą być w stanie używać obiektów klas pochodnych bez wiedzy o tym. Innymi słowy, obiekty klas pochodnych muszą być w pełni zastępowalne przez obiekty klas bazowych.
Przykład: Jeśli masz klasę Ptak z metodą lec(), to klasa Pingwin dziedzicząca po Ptak narusza LSP, jeśli Pingwin.lec() rzuca wyjątek lub nic nie robi.
I - Zasada Segregacji Interfejsów (Interface Segregation Principle - ISP):
Lepiej jest mieć wiele małych, specyficznych interfejsów niż jeden duży, ogólny. Klienci (klasy używające interfejsu) nie powinni być zmuszani do zależności od metod, których nie używają.
Przykład: Zamiast jednego interfejsu Pracownik z metodami pracuj(), jedz(), zarzadzajZespolem(), lepiej mieć interfejsy IPracujacy, IJedzacy, IZarzadzajacy.
D - Zasada Odwrócenia Zależności (Dependency Inversion Principle - DIP):
Moduły wysokiego poziomu (np. logika biznesowa) nie powinny zależeć od modułów niskiego poziomu (np. szczegóły implementacji dostępu do danych). Oba powinny zależeć od abstrakcji (np. interfejsów).
Abstrakcje nie powinny zależeć od szczegółów. Szczegóły powinny zależeć od abstrakcji.
Często realizowane za pomocą Wstrzykiwania Zależności (Dependency Injection).
4. Dobre Praktyki Ogólne
Testowanie: Pisz testy (jednostkowe, integracyjne, E2E). Testy są siatką bezpieczeństwa podczas refaktoryzacji i dodawania nowych funkcji, a także dokumentują działanie kodu.
Kontrola Wersji (np. Git): Używaj systemu kontroli wersji. Twórz małe, atomowe commity z jasnymi komunikatami opisującymi co i dlaczego zostało zmienione. Pracuj na gałęziach (branches).
Refaktoryzacja: Nie bój się ulepszać istniejącego kodu. Regularnie poświęcaj czas na refaktoryzację, aby kod pozostał czysty i łatwy do zarządzania (tzw. "zasada skauta" - zostaw kod czystszym, niż go zastałeś).
Obsługa Błędów: Implementuj solidną i przewidywalną obsługę błędów. Nie ukrywaj wyjątków. Loguj błędy w sposób użyteczny do diagnozy. Informuj użytkownika w sposób zrozumiały, nie ujawniając potencjalnie wrażliwych szczegółów implementacji.
Unikaj Przedwczesnej Optymalizacji: Pisz kod najpierw czytelny i poprawny. Optymalizuj dopiero wtedy, gdy jest to konieczne i poparte profilowaniem.
Podsumowanie
Tworzenie wysokiej jakości oprogramowania to proces ciągły, wymagający dyscypliny i uwagi. Stosowanie się do powyższych zasad – dbanie o czytelność, priorytetyzowanie bezpieczeństwa i przestrzeganie SOLID – znacząco podniesie jakość Twojego kodu, ułatwi jego utrzymanie i rozwój oraz sprawi, że praca nad nim będzie bardziej efektywna i przyjemna.
