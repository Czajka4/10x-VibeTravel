# Statyczna Analiza Kodu w VibeTravel

## 1. Narzędzia Formatowania

### Black
- Automatyczny formatter kodu Python
- Wymusza spójny styl kodu w całym projekcie
- Konfiguracja w `pyproject.toml`:
  ```toml
  [tool.black]
  line-length = 88
  target-version = ['py310']
  include = '\.pyi?$'
  ```

### isort
- Sortuje i organizuje importy w kodzie Python
- Zapewnia spójny układ importów
- Konfiguracja w `pyproject.toml`:
  ```toml
  [tool.isort]
  profile = "black"
  line_length = 88
  multi_line_output = 3
  ```

### djLint
- Formatuje szablony Django
- Sprawdza poprawność składni HTML
- Konfiguracja w `pyproject.toml`:
  ```toml
  [tool.djlint]
  profile = "django"
  ignore = "H031"
  extension = "html"
  indent = 2
  ```

## 2. Linting

### Flake8
- Łączy kilka narzędzi do sprawdzania kodu:
  - pycodestyle (PEP 8)
  - pyflakes (wykrywanie błędów)
  - mccabe (złożoność kodu)
- Konfiguracja w `.flake8`:
  ```ini
  [flake8]
  max-line-length = 88
  extend-ignore = E203
  exclude = .git,__pycache__,migrations,venv,env
  ```

### django-check-migration
- Sprawdza poprawność migracji Django
- Wykrywa potencjalne problemy z migracjami
- Zintegrowany z pre-commit

## 3. Statyczna Analiza Typów

### Mypy
- Sprawdza typy w kodzie Python
- Wymusza adnotacje typów
- Konfiguracja w `mypy.ini`:
  ```ini
  [mypy]
  python_version = 3.10
  warn_return_any = True
  warn_unused_configs = True
  disallow_untyped_defs = True
  disallow_incomplete_defs = True
  check_untyped_defs = True
  disallow_untyped_decorators = True
  no_implicit_optional = True
  warn_redundant_casts = True
  warn_unused_ignores = True
  warn_no_return = True
  warn_unreachable = True
  ```

### django-stubs
- Dodaje typy dla Django
- Integruje się z Mypy
- Konfiguracja w `mypy.ini`:
  ```ini
  [mypy.plugins.django-stubs]
  django_settings_module = "vibetravel.settings"
  ```

## 4. Pre-commit Hooks

Wszystkie narzędzia są zintegrowane z pre-commit w `.pre-commit-config.yaml`:
```yaml
repos:
-   repo: https://github.com/psf/black-pre-commit-mirror
    rev: 23.9.1
    hooks:
    -   id: black

-   repo: https://github.com/pycqa/isort
    rev: 5.12.0
    hooks:
    -   id: isort

-   repo: https://github.com/pycqa/flake8
    rev: 6.1.0
    hooks:
    -   id: flake8

-   repo: https://github.com/Riverside-Healthcare/djLint
    rev: v1.32.0
    hooks:
    -   id: djlint-reformat-django
    -   id: djlint-django

-   repo: https://github.com/pre-commit/mirrors-mypy
    rev: v1.8.0
    hooks:
    -   id: mypy
        additional_dependencies: [django-stubs, types-requests]

-   repo: https://github.com/django-check-migration/django-check-migration
    rev: 0.1.0
    hooks:
    -   id: django-check-migration

-   repo: https://github.com/commitizen-tools/commitizen
    rev: v3.20.0
    hooks:
    -   id: commitizen
        stages: [commit-msg]
```

## 5. Jak to działa?

1. **Przed commitem**:
   - Pre-commit uruchamia wszystkie hooki
   - Każdy hook sprawdza odpowiedni aspekt kodu
   - Commit jest blokowany, jeśli którykolwiek hook nie przejdzie

2. **Proces sprawdzania**:
   - Black formatuje kod Python
   - isort sortuje importy
   - Flake8 sprawdza styl i błędy
   - djLint formatuje szablony
   - Mypy sprawdza typy
   - django-check-migration weryfikuje migracje
   - commitizen sprawdza format commitów

3. **W GitHub Actions**:
   - Wszystkie sprawdzenia są uruchamiane automatycznie
   - Wyniki są widoczne w zakładce "Actions"
   - Pull requesty są blokowane, jeśli sprawdzenia nie przejdą

## 6. Korzyści

1. **Jakość kodu**:
   - Spójny styl w całym projekcie
   - Wczesne wykrywanie błędów
   - Lepsze typowanie

2. **Produktywność**:
   - Automatyczne formatowanie
   - Szybsze code review
   - Mniej błędów w produkcji

3. **Utrzymanie**:
   - Łatwiejsze wprowadzanie zmian
   - Lepsza dokumentacja kodu
   - Mniej problemów z integracją

## 7. Jak używać?

1. **Instalacja**:
```bash
pip install -r requirements.txt
pre-commit install
```

2. **Ręczne uruchomienie**:
```bash
pre-commit run --all-files
```

3. **Sprawdzenie typów**:
```bash
mypy .
```

4. **Formatowanie kodu**:
```bash
black .
isort .
djlint --reformat .
``` 