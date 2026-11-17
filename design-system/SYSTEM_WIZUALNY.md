# Centrum Budowlane | System wizualny 1.0

**Podstawa:** załączona grafika referencyjna przedstawiająca górny baner centrum budowlanego, granatową nawigację, cztery karty KPI, sekcje operacyjne i cztery fotograficzne kafle działów. Specyfikacja obejmuje działającą aplikację PWA i osobną stronę prezentacji projektu.

## 1. Idea i reguły

Interfejs wygląda jak środowisko pracy profesjonalnej hurtowni budowlanej, nie jak strona reklamowa. Ma być zwarty, czytelny, funkcjonalny i konsekwentny: mocny granat, czysta wyrazista czerwień, białe panele, realna fotografia branżowa i uporządkowane oznaczenia procesów. Jeden zestaw komponentów działa dla zarządu, sprzedaży, magazynu, tartaku, logistyki, kierowcy, zakupów, finansów i kadr.

**Zasada hierarchii:** kontekst procesu > zadanie do wykonania > tabela lub formularz > informacje dodatkowe. Wszystkie elementy aktywne mają rzeczywiste działanie, a przy braku uprawnień są niedostępne. Żaden dekoracyjny kafel nie powinien udawać przycisku.

## 2. Kolory i ich zastosowanie

| Token | Wartość | Użycie |
|---|---|---|
| `--cb-navy-950` | `#06152B` | Sidebar, tło stopki, głęboki baner |
| `--cb-navy-900` | `#0A203B` | Topbar, nagłówki segmentów |
| `--cb-navy-800` | `#0D2C4F` | Karty KPI, nagłówki informacyjne |
| `--cb-navy-700` | `#17446C` | Aktywne filtry i obramowania na ciemnym tle |
| `--cb-red-600` | `#E30620` | Główne CTA, aktywny moduł, akcent marży |
| `--cb-red-700` | `#B90D25` | Hover i aktywacja głównej czerwieni |
| `--cb-red-050` | `#FFF1F3` | Delikatne tło stanu wymagającego działania |
| `--cb-blue-500` | `#0877D2` | Dane na wykresie i stan informacyjny |
| `--cb-paper` | `#FFFFFF` | Tła formularzy, tabel, paneli |
| `--cb-canvas` | `#F2F5F9` | Główny obszar roboczy |
| `--cb-ink` | `#10263F` | Główny tekst |
| `--cb-muted` | `#64788E` | Tekst pomocniczy |
| `--cb-border` | `#DCE5EF` | Linie podziału |
| `--cb-success` | `#15805E` | Tylko pozytywne statusy |
| `--cb-warning` | `#D18A00` | Tylko ostrzeżenia |

Czerwony służy do wskazywania głównych działań, ważnych podsumowań i aktywnej pozycji menu. Nie stosować czerwonego do każdego panelu. Wykres sprzedaży może pozostać niebieski, aby oddzielić dane od akcji. Wartości alarmowe muszą zawierać również etykietę tekstową, nie sam kolor.

## 3. Typografia

- Inter: teksty interfejsu, tabele, formularze, komunikaty.
- Roboto Condensed: krótkie etykiety modułów, liczby KPI, nagłówki kart, nawiązanie do zwartej typografii grafiki.
- Nagłówek strony: 28 do 32 px, 750 do 800, ciemny granat.
- Nagłówek panelu: 16 do 18 px, 700.
- Kluczowa liczba KPI: 28 do 34 px, 800, cyfry tabularne.
- Tekst główny: 13 do 15 px, interlinia 1,5.
- Tekst pomocniczy: 12 do 13 px. Etykiety nie powinny być mniejsze niż 11 px na telefonie.
- Nie wyrównywać kwot w tabelach spacjami. Korzystać z CSS i tabularnych cyfr.

## 4. Siatka i wymiary

- Desktop 1440 px+: lewa nawigacja 240 do 252 px, content 24 do 32 px od brzegów, maksymalna szerokość 1600 px; cztery KPI w rzędzie; cztery kafle działów poniżej.
- Desktop 1100 do 1439 px: cztery KPI w rzędzie przy zmniejszonych odstępach, panel zadań pod wskaźnikami, jeśli szerokość jest niewystarczająca.
- Tablet 768 do 1099 px: menu w drawer, dwa KPI na rząd, dwa moduły fotograficzne na rząd; tabele przewijane poziomo z widocznymi nazwami kolumn.
- Telefon do 767 px: menu zwijane, pojedyncza kolumna główna, KPI po dwa przy dostatecznej szerokości, duże przyciski min. 44 px, formularze bez poziomego przepełnienia.
- Odstępy: skala 4, 8, 12, 16, 24, 32 px. Zaokrąglenia: 6 px dla akcji, 10 px dla kart, 14 px dla dużych paneli. Unikać zbyt dużych zaokrągleń.

## 5. Komponenty

| Komponent | Wzór | Działanie |
|---|---|---|
| Sidebar | Granat #06152B, białe ikony, aktywny czerwony pasek | Przejście między modułami, zmiana kontekstu |
| Topbar | Granat #0A203B, wyszukiwanie, rola, alarmy | Wyszukiwarka powinna faktycznie wyszukiwać |
| Karta KPI | Granat, biała liczba, podpis; jedna ważna karta czerwona | Przejście do właściwego raportu, jeśli klikalna |
| Kafel działu | Fotografia, granatowy gradient i wyraźna nazwa | Otworzenie modułu |
| Panel | Biała powierzchnia, cienka granatowo-szara ramka | Widok z akcjami i filtrowaniem |
| Tabela | Jasny nagłówek, czytelne kolumny, wyrównane liczby | Sortowanie, filtr, wyszukiwanie, eksport według uprawnień |
| Główne CTA | Czerwone, biały tekst, wysokość co najmniej 42 px | Zapis, zatwierdzenie, nowy dokument |
| CTA drugorzędne | Granatowe lub białe z ciemną ramką | Podgląd, filtr, cofnięcie |
| Status | Etykieta oraz subtelny kolor semantyczny | Jednoznaczna informacja o etapie |
| Alert | Ikona, informacja, właściciel i następny krok | Szybkie przejście do zadania |
| Załącznik | Nazwa pliku, typ, rozmiar, data, status | Przekazanie do weryfikacji, przyjęcie lub odrzucenie |
| Modal | Maksymalna szerokość 720 px, wyraźny nagłówek i stopka | Działający formularz z walidacją |

## 6. Poszczególne ekrany

| Ekran | Pierwsza informacja | Główna akcja i charakterystyczny element |
|---|---|---|
| Pulpit | Sprzedaż, marża, dostawy, zamówienia i alerty | KPI, zdjęcie centrum, fotograficzne moduły |
| Sprzedaż / zamówienia | Rejestr, wartości, status i marża | Nowe zamówienie, filtry, dokumenty |
| Inwestorzy | Limit, należność, budowa, ryzyko | Akceptacja lub wstrzymanie wydania |
| Magazyn budowlany | Dostępność, rezerwacja, minimum | PZ, WZ, skaner w przyszłym etapie |
| Hurtownia elektryczna | Stany kabli, osprzętu, ceny i braki | Dostępność i marża kategorii |
| Zakupy | Niedobory, zamówienia PO, przyjęcia | Zamówienie dostawcy, następnie PZ |
| Tartak | Surowiec, uzysk i koszt m3 | Nowe zlecenie produkcji |
| Transport i HDS | Dostawy, pojazdy, terminy i konflikty | Przydziel trasę, otwórz dokument POD |
| Kierowca HDS | Najbliższa dostawa i adres | Oznacz status, dodaj dokument, zgłoś problem |
| Obieg dokumentów | Brakujące pliki i kolejka akceptacji | Akceptuj, odrzuć, wezwij do uzupełnienia |
| Finanse | Wynik działów, koszty, VAT, marże | Zmień scenariusz, eksportuj raport |
| Kadry | Etaty, koszty pracodawcy, stanowiska | Aktualizuj stawki i założenia |
| Raporty / ryzyka | Blokady, trendy, zaległości, awarie | Przypisz zadanie, monitoruj odchylenie |
| Import danych | Typ kartoteki i podgląd kolumn | Zmapuj, sprawdź, zatwierdź import |
| Ustawienia | Rola prezentacyjna, lokalny zapis i PWA | Eksport danych, przywrócenie kopii |

## 7. Strona prezentacyjna projektu

1. Hero fotograficzny lub wyraźnie oznaczona fotorealistyczna wizualizacja centrum budowlanego, z granatowym gradientem i czerwonym znakiem graficznym.
2. Nad hero główna nawigacja, przyciski "Uruchom demo" oraz "Zobacz funkcje".
3. Sekcja zrzutu ekranu aplikacji. Prawdziwy screenshot wdrożonego widoku, nie wygenerowana makieta podawana jako działająca aplikacja.
4. Cztery działy na fotograficznych kaflach, zgodnie z pulpitem.
5. Obieg zamówienia od zapytania przez PZ/WZ i HDS po POD i rozliczenie.
6. Galeria desktop/mobile, role i uprawnienia, bezpieczeństwo i ograniczenia wersji lokalnej.
7. Informacje techniczne, dokumentacja, instrukcja instalacji PWA, przycisk demo i repozytorium.

## 8. Materiały fotograficzne i uczciwe oznaczenia

Główny baner aplikacji jest fotorealistyczną wizualizacją fikcyjnego centrum budowlanego. Nie wolno opisywać go jako fotografii prawdziwego obiektu. Kafle działów mają korzystać z fotografii branżowych z Pexels albo z legalnie pozyskanych zdjęć firmy, z awaryjną grafiką dostępną offline. Zdjęcia i licencje opisuje `app/FOTOGRAFIE_I_LICENCJE.md`.

## 9. Dostępność i zachowanie

- Kontrast co najmniej WCAG AA w tekście roboczym, z widocznym fokusem klawiatury.
- Ikony z podpisami, szczególnie w działach: Magazyn, Tartak, HDS, Dokumenty i Finanse.
- Przyciski wyłączone z wyjaśnieniem uprawnienia lub niekompletnego dokumentu.
- Desktop i mobile mają te same dane i procesy, ale z inną hierarchią zawartości.
- PWA offline nie udaje zsynchronizowanej bazy firmowej. Aktualna wersja działa lokalnie, a role służą do prezentacji.
- Dane, firmy, kwoty i liczby na demo są symulacją.

## 10. Kryteria odbioru

1. Główne kolory, rozmiary i stany komponentów są zgodne na wszystkich ekranach.
2. Dashboard i cztery kafle branżowe są zbliżone kompozycyjnie do grafiki wzorcowej.
3. Wszystkie podstawowe formularze mają walidację, komunikat i zapis danych.
4. Przeglądy i eksporty pozostają spójne z rolami.
5. Ekrany 390 px i 1440 px zachowują czytelność i bezpieczne pola kliknięcia.
6. Publiczna strona projektu nie przedstawia demonstracji jako gotowego wdrożenia produkcyjnego.
7. Zrzuty ekranu w dokumentacji pochodzą z działającej aplikacji.
