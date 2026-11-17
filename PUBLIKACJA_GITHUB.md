# Publikacja Centrum Budowlane PWA

## Aktualny stan

Aplikacja i strona prezentacyjna są już opublikowane na Vercelu:

- Strona projektu: https://centrum-budowlane-pwa.vercel.app/
- Aplikacja: https://centrum-budowlane-pwa.vercel.app/app/
- Excel: https://centrum-budowlane-pwa.vercel.app/downloads/Centrum_Budowlane_Model_Finansowy_2026.xlsx

Repozytorium źródłowe: https://github.com/lukaszst-cz/centrum-budowlane-pwa. Jest obecnie prywatne. Vercel jest podłączony do gałęzi `main` i publikuje jej zmiany.

## Jeśli w przyszłości chcesz uruchomić GitHub Pages

1. W GitHub `Settings → General → Danger Zone` zmień repozytorium na publiczne, jeśli chcesz udostępniać też źródła.
2. W `Settings → Pages` wybierz `Source: GitHub Actions`, jeżeli taka opcja jest dostępna.
3. Uruchom ręcznie workflow `Publikacja GitHub Pages` w zakładce Actions.
4. Sprawdź wynik oraz linki do strony, aplikacji i Excela.

GitHub Pages nie jest obecnie potrzebny do demonstracji. Automatyczne próby uruchamiania Pages na prywatnym repozytorium zostały wyłączone.

## Ograniczenia demonstracji

Dane pozostają lokalnie w przeglądarce. Przełączanie ról nie jest uwierzytelnianiem. Przed wdrożeniem dla rzeczywistych pracowników wymagane są backend, role serwerowe, wspólna baza danych i bezpieczny obieg dokumentów.
