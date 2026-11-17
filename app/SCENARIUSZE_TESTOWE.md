# Scenariusze testowe

Weryfikowano w Chromium z automatyzacją przeglądarki na desktopie i mobilnym viewport 390 px. Środowisko testowe wstrzykuje pliki do osadzonej strony, gdyż lokalna nawigacja przeglądarki jest ograniczona.

| Scenariusz | Wynik |
|---|---|
| Render pulpitu i grafiki branżowej | OK |
| Zmiana roli na magazyniera i filtracja widocznych modułów | OK |
| PZ +45 szt. cementu | OK |
| Nowe PO i przyjęcie na stan | OK |
| Zlecenie tartaku, rozchód surowca i przyjęcie wyrobu | OK |
| Edycja wynagrodzenia HDS i przeliczenie kosztów płac | OK |
| Zamówienie z dwiema pozycjami w różnych działach | OK |
| Dostawa HDS: planowanie, załadunek, WZ, w trasie, doręczenie | OK |
| Rozliczenie dostarczonego zamówienia i powiększenie należności inwestora | OK |
| Eksport CSV | OK |
| Brak widoczności finansów dla kierowcy | OK |
| Menu mobilne i zmiana modułu | OK |
| Błędy wykonywania JavaScript w testach | 0 |

Testy nie obejmowały jeszcze wieloosobowej współbieżności, rzeczywistego backendu, księgowania podatkowego ani instalacji na urządzeniach produkcyjnych.


## Import i migracja (wersja 1.5)

1. Włącz rolę Zarząd, otwórz **Import / migracja danych** i pobierz wzór CSV.
2. Wgraj CSV z przykładowymi produktami. Zweryfikuj automatyczne przypisanie kolumn i kliknij **Importuj**. Towary pojawią się w **Magazynach**.
3. Zmień kartotekę na **Inwestorzy**, wybierz odpowiedni plik i sprawdź mapowanie. Niepoprawne/ujemne kwoty powinny wstrzymać import.
4. Analogicznie sprawdź XLSX i pierwszą tabelę HTML. PDF nie jest importem kartotekowym, ale może być załącznikiem dostawy.
5. Pobierz kopię JSON, przywróć dane początkowe i wczytaj kopię.

## Dokumenty HDS / biuro

1. Przełącz widok na **Kierowca HDS**, otwórz Transport i HDS, wybierz dokument przy dostawie i dołącz PDF albo zdjęcie, ustaw typ **POD**.
2. Otwórz **Dokumenty dostaw**, sprawdź wpis **Do weryfikacji**.
3. Przełącz na **Finanse**, zaakceptuj POD. Jeżeli dokument jest nieczytelny, odrzuć go z podaniem przyczyny. Kierowca powinien widzieć informację o poprawce.
4. Dopóki nie zostanie zaakceptowany POD dla dostawy, rozliczenie zamówienia powinno być zablokowane.
5. Wyłącz połączenie i sprawdź, że już zapisane pliki działają na tym samym urządzeniu. Brak wspólnej bazy oznacza brak automatycznej transmisji do innego komputera.

## Obieg dokumentów 2.0, test automatyczny

Przetestowano w Chromium na danych symulacyjnych oraz w pamięciowym środowisku przeglądarki (polityka środowiska blokowała lokalne adresy WWW). Wszystkie kroki w teście podstawowym przeszły bez błędów JavaScript:

1. Wyświetlenie kolejki zadań z etapów zamówienia i PO.
2. Automatyczne pojawienie się PO w rejestrze oraz pobranie roboczego wydruku HTML.
3. Dodanie manualnego zadania do działu, a następnie zamknięcie go po potwierdzeniu.
4. Realizacja dostawy przez załadunek, wydanie WZ i doręczenie.
5. Zgłoszenie szkody w dostawie.
6. Dodanie POD w widoku kierowcy i brak uprawnień kierowcy do zatwierdzania dokumentu.
7. Akceptacja POD w widoku finansowym i zablokowanie rozliczenia przy otwartej szkodzie.
8. Dodanie protokołu, akceptacja przez biuro, zamknięcie wyjątku i rozliczenie zamówienia.
9. Automatyczne pojawienie się WZ oraz zestawienia rozliczeniowego w rejestrze.
10. Eksport CSV i ograniczenie widoczności dokumentów rozliczeniowych w widoku kierowcy.

Dodatkowy test integracji na rzeczywistych urządzeniach pozostaje do wykonania po uruchomieniu serwera i współdzielonej bazy. Obsługa załączników w teście była emulowana pamięciowo; dlatego test **nie zastępuje** kontroli rzeczywistego IndexedDB, odporności na utratę danych ani zachowania PWA po instalacji.
