# Sprawozdanie — Laboratorium 3

## Temat
Dane obrazowe i wideo: potok i własny zbiór — **Drone vs Bird**.

## Cel ćwiczenia
Przygotowanie dwuklasowego mini-zbioru fotografii przedstawiających ptaki i drony, opracowanie transformacji ewaluacyjnych i treningowych, wczytanie obrazów przez `ImageFolder` i `DataLoader` oraz wizualizacja danych.

## Źródło danych
Zbiór: [Drone vs Bird, Kaggle](https://www.kaggle.com/datasets/muhammadsaoodsarwar/drone-vs-bird). Notebook pobiera oryginalne fotografie przez `kagglehub` (albo korzysta z plików pobranych ręcznie). Warunki wykorzystywania i redystrybucji należy sprawdzić na stronie autora; nie zostały niezależnie zweryfikowane.

## Przebieg ćwiczenia
1. Wyszukanie obrazów w katalogach `bird` i `drone`.
2. Weryfikacja poprawności plików i losowy wybór 60 obrazów na klasę, ziarno 42.
3. Skopiowanie/konwersja obrazów do struktury `dane_drone_bird/bird/` i `dane_drone_bird/drone/` oraz zapis pochodzenia w `lista_obrazow.csv`.
4. Zdefiniowanie potoku ewaluacyjnego: `Resize(128,128)`, `ToTensor`, `Normalize([0.5]*3, [0.5]*3)`.
5. Zdefiniowanie potoku treningowego: powyższe operacje oraz `RandomHorizontalFlip(0.5)`, `RandomRotation(15)` i `ColorJitter(brightness=0.2, contrast=0.2)`.
6. Zbudowanie `ImageFolder`, `DataLoader(batch_size=12, shuffle=True)` i przygotowanie wizualizacji.

## Statystyki i wyniki

| Miara | Wartość |
|---|---|
| Liczba klas | 2 (założenie i kontrola w kodzie) |
| Liczba obrazów na klasę | 60 na `bird`, 60 na `drone` (docelowa liczba wybierana przez kod) |
| Razem w mini-zbiorze | 120 (po skutecznym wykonaniu) |
| Rozmiar obrazu po transformacji | `(3, 128, 128)` |
| Rozmiar paczki | do `(12, 3, 128, 128)` |
| `class_to_idx` | `{'bird': 0, 'drone': 1}` dla tak nazwanych katalogów |

**Status pomiarów:** W tym środowisku nie udało się pobrać danych z Kaggle, dlatego powyższe wielkości są parametrami i oczekiwanymi wynikami implementacji, a **nie wynikami pomiaru po wykonaniu programu na zdjęciach**. Notebook zapisze potwierdzone wyniki w `sprawozdanie_lab3_wyniki.md` po uruchomieniu z dostępem do zdjęć.

## Wizualizacje

![Schemat potoku](obrazy_lab3/schemat_potoku.png)

Po wykonaniu notebooka zostaną zapisane obrazy oparte na **rzeczywistych fotografiach**:
- `obrazy_lab3/01_siatka_paczki.png` — siatka 12 obrazów z jednej paczki,
- `obrazy_lab3/02_augmentacje.png` — oryginał, wariant ewaluacyjny i losowe augmentacje jednego zdjęcia,
- `obrazy_lab3/03_liczebnosc_klas.png` — słupkowy wykres liczebności klas.

## Wnioski
`ImageFolder` buduje jednoznaczne mapowanie klas, a `DataLoader` dostarcza obrazy jako tensory gotowe do analizy. Wariant treningowy zwiększa zróżnicowanie obrazów bez zmieniania etykiet. 

## Narzędzia
Python, PyTorch, torchvision, Pillow, matplotlib, kagglehub.
