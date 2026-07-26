# Automatyzacja wdrożenia za pomocą GitHub Actions

## Cel projektu

Celem projektu jest automatyzacja procesu budowania i wdrażania strony internetowej za pomocą GitHub Actions.

Po wykonaniu operacji `push` do repozytorium GitHub automatycznie uruchamiany jest workflow.

## Schemat działania

1. Użytkownik wykonuje `push` do repozytorium.
2. GitHub Actions uruchamia workflow.
3. Job `build` pobiera kod źródłowy.
4. Tworzony jest katalog `build`.
5. Plik `index.html` zostaje skopiowany do katalogu `build`.
6. Utworzony build zostaje zapisany jako artefakt.
7. Job `deploy` pobiera przygotowany artefakt.
8. Przygotowane pliki są wdrażane na serwer VPS przez SSH.

## Struktura workflow

Workflow składa się z dwóch jobów:

### Build

Job `build`:
- pobiera kod z repozytorium za pomocą `actions/checkout@v4`,
- tworzy katalog `build`,
- kopiuje plik `index.html`,
- zapisuje wynik jako artefakt za pomocą `actions/upload-artifact@v4`.

### Deploy

Job `deploy`:
- uruchamia się dopiero po pomyślnym zakończeniu `build`,
- wykorzystuje zależność `needs: build`,
- pobiera artefakt za pomocą `actions/download-artifact@v4`,
- przygotowuje pliki do wdrożenia na serwer VPS.

## Trigger

Workflow uruchamiany jest automatycznie po wykonaniu operacji:

`push`

Dzięki temu każda zmiana wysłana do repozytorium może zostać automatycznie zbudowana i wdrożona.

## Technologie

- GitHub
- GitHub Actions
- YAML
- Linux
- SSH
- VPS
