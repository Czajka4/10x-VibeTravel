# Narzędzia do Lintingu i Formatowania Kodu

## Pre-commit
Pre-commit to framework do zarządzania i utrzymywania git hooks. Pozwala na automatyczne uruchamianie skryptów przed każdym commitem, co pomaga w utrzymaniu jakości kodu i spójności stylu.

## Black
Black to automatyczny formatter kodu Python, który:
- Formatuje kod zgodnie z ustalonymi zasadami
- Usuwa zbędne spacje i znaki
- Standaryzuje formatowanie stringów
- Automatycznie formatuje importy
- Jest "niekompromisowy" - nie oferuje opcji konfiguracji stylu

Konfiguracja w projekcie:
- Długość linii: 88 znaków
- Wersja Pythona: 3.10
- Formatuje pliki .py i .pyi

## isort
isort to narzędzie do sortowania importów w kodzie Python:
- Grupuje importy w logiczne sekcje
- Sortuje importy alfabetycznie
- Automatycznie usuwa nieużywane importy
- Jest kompatybilne z Black

Konfiguracja w projekcie:
- Profil: black (kompatybilność z Black)
- Długość linii: 88 znaków
- Format wyjściowy: 3 (wieloliniowy)

## Flake8
Flake8 to linter, który łączy kilka narzędzi:
- pycodestyle (dawniej pep8) - sprawdza zgodność z PEP 8
- pyflakes - wykrywa błędy w kodzie
- mccabe - sprawdza złożoność kodu

Konfiguracja w projekcie:
- Maksymalna długość linii: 88 znaków
- Ignorowane błędy: E203 (konflikt z Black)
- Wykluczone katalogi: .git, __pycache__, migrations, venv, env

## djLint
djLint to narzędzie do formatowania i sprawdzania szablonów Django:
- Formatuje szablony HTML
- Sprawdza poprawność składni
- Wspiera szablony Django
- Automatycznie poprawia formatowanie

Konfiguracja w projekcie:
- Profil: django
- Ignorowane błędy: H031
- Rozszerzenie plików: html
- Wcięcia: 2 spacje

## GitHub Actions
W projekcie skonfigurowany jest workflow GitHub Actions, który:
- Uruchamia się przy każdym pushu i pull requeście
- Używa Ubuntu jako systemu operacyjnego
- Konfiguruje Pythona 3.10
- Instaluje pre-commit
- Uruchamia wszystkie hooki pre-commit na wszystkich plikach

## Jak używać

### Lokalnie
1. Zainstaluj zależności:
```bash
pip install -r requirements.txt
```

2. Zainstaluj hooki pre-commit:
```bash
pre-commit install
```

3. Możesz ręcznie uruchomić wszystkie hooki:
```bash
pre-commit run --all-files
```

### W GitHub Actions
Workflow uruchamia się automatycznie przy:
- Pushu do repozytorium
- Utworzeniu pull requesta

Wyniki lintingu są widoczne w zakładce "Actions" na GitHubie. 