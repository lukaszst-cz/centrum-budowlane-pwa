# Publikacja Centrum Budowlane PWA

## Stan projektu (17.11.2026)

Repozytorium [centrum-budowlane-pwa](https://github.com/lukaszst-cz/centrum-budowlane-pwa) jest publiczne. Zawiera 43 pliki projektu, w tym stronę prezentacyjną, aplikację PWA, dokumentację, grafiki i model finansowy XLSX.

### GitHub Pages

- [Strona prezentacyjna](https://lukaszst-cz.github.io/centrum-budowlane-pwa/)
- [Aplikacja PWA](https://lukaszst-cz.github.io/centrum-budowlane-pwa/app/)
- [Model finansowy Excel](https://lukaszst-cz.github.io/centrum-budowlane-pwa/downloads/Centrum_Budowlane_Model_Finansowy_2026.xlsx)

Po aktywowaniu Pages ponowiono [workflow publikacyjny](https://github.com/lukaszst-cz/centrum-budowlane-pwa/actions/workflows/pages.yml). Druga próba uruchomienia [przebiegu #44063294909](https://github.com/lukaszst-cz/centrum-budowlane-pwa/actions/runs/44063294909) zakończyła się sukcesem. Strona, aplikacja i plik XLSX zwracały HTTP 200 w kontroli 17.11.2026. Wcześniejsze błędy dotyczyły nieaktywnej usługi Pages, a nie błędu kompilacji aplikacji.

### Vercel

- [Strona prezentacyjna](https://centrum-budowlane-pwa.vercel.app/)
- [Aplikacja](https://centrum-budowlane-pwa.vercel.app/app/)
- [Model finansowy Excel](https://centrum-budowlane-pwa.vercel.app/downloads/Centrum_Budowlane_Model_Finansowy_2026.xlsx)

Vercel jest połączony z gałęzią `main` i automatycznie publikuje zmiany. Obie publikacje są publiczne i nie wymagają logowania.

## Aktualizowanie publikacji

1. Zapisz zatwierdzone zmiany w gałęzi `main`.
2. Vercel i GitHub Pages opublikują je automatycznie. Workflow Pages działa po wypchnięciu zmian do `main`.
3. Możesz również uruchomić Pages ręcznie przez [Actions: Publikacja GitHub Pages](https://github.com/lukaszst-cz/centrum-budowlane-pwa/actions/workflows/pages.yml) i `Run workflow`.
4. Po zakończeniu sprawdź osobno stronę, aplikację i pobieranie pliku XLSX.

Publikacja GitHub Pages wykorzystuje wyzwalacze `push` dla `main` i `workflow_dispatch`, bez dodatkowych harmonogramów.

## Ograniczenia demonstracji

Aplikacja korzysta z danych symulacyjnych i lokalnego zapisu w przeglądarce. Przełączanie ról nie jest bezpiecznym uwierzytelnianiem. Przed wdrożeniem dla rzeczywistych pracowników wymagane są backend, serwerowe uprawnienia, wspólna baza danych i bezpieczny obieg dokumentów. Projekt nie jest wdrożeniem dla klienta.
