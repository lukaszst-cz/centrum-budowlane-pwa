# Publikacja na GitHubie · instrukcja dla właściciela

**Stan:** pliki gotowe do udostępnienia. Repozytorium projektu nie zostało jeszcze utworzone ani opublikowane.

1. Otwórz <https://github.com/new> będąc zalogowanym na swoim koncie.
2. Nazwa repozytorium: `centrum-budowlane-pwa`. Widoczność: **Public**. Możesz nie dodawać automatycznego README, ponieważ projekt już zawiera kompletne README.
3. Prześlij zawartość paczki ZIP (po rozpakowaniu) do `main`, nie wgrywaj samego pliku ZIP. Foldery `app`, `screens`, `.github` muszą leżeć obok głównego `index.html`.
4. Otwórz **Settings > Pages**. Zmień **Source** na **GitHub Actions** i zapisz. Plik `.github/workflows/pages.yml` uruchamia publikację.
5. Wejdź do **Actions**, sprawdź wykonanie `Publikacja GitHub Pages`. Po zakończeniu odwiedź adres podany w Settings > Pages.
6. Otwórz link na komputerze i telefonie, przetestuj przycisk **Uruchom demo**, rolę Kierowca HDS, obieg dokumentów, import i instalację PWA.
7. Uzupełnij link `Profil GitHub` w `index.html` konkretnym linkiem do nowego repozytorium i dodaj adres strony do repozytorium w sekcji About.

**Wariant terminalowy (gdy repozytorium jest już utworzone):**

```bash
git init
git add .
git commit -m "feat: launch construction center PWA showcase"
git branch -M main
git remote add origin https://github.com/TWOJE-KONTO/centrum-budowlane-pwa.git
git push -u origin main
```

GitHub Pages udostępnia statyczną aplikację i landing page. Nie uruchamia backendu, logowania wielostanowiskowego ani wspólnej bazy danych.
