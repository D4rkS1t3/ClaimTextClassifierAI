# ClaimTextClassifierAI

System wspierający proces likwidacji szkód ubezpieczeniowych (InsurTech). Aplikacja łączy techniki przetwarzania języka naturalnego (NLP) ze strukturami Scikit-Learn Pipeline w celu automatycznej kategoryzacji spraw, szacowania priorytetów oraz wykrywania anomalii finansowych (Antifraud).

## Główne Funkcjonalności

1. **Automatyczna Klasyfikacja Tekstu (NLP)**: Model `LinearSVC` analizuje surowy tekst zgłoszenia klienta (oczyszczony uprzednio z szumu i stop-words za pomocą wyrażeń regularnych `re`) i przypisuje sprawę do jednej z kategorii taryfowych: `AUTO`, `DOM`, `ZDROWIE`.
2. **Wielozadaniowe Szacowanie Priorytetów**: Model regresji logistycznej (`LogisticRegression`), zaimplementowany wewnątrz zaawansowanego kontenera `ColumnTransformer`, jednocześnie analizuje wektory tekstowe (TF-IDF) oraz znormalizowaną kwotę roszczenia (`StandardScaler`), decydując o nadaniu flagi wysokiego priorytetu sprawom krytycznym.
3. **Moduł Detekcji Anomalii (Wstępny Antyfraud)**: Silnik regułowy porównuje przewidzianą klasę zdarzenia z żądaną kwotą odszkodowania, automatycznie flagując próby wyłudzenia (np. żądanie rażąco wysokich kwot za drobne uszkodzenia parkingowe).
4. **Interaktywny Konsolowy Panel Operatora**: Pętla operacyjna (CLI) umożliwiająca testowanie systemu w czasie rzeczywistym z walidacją danych wejściowych (`try-except`).

## Architektura Technologiczna

- **Python 3.x**
- **Pandas & NumPy** - inżynieria cech, symulacja danych ubezpieczeniowych i budowanie struktur logicznych.
- **Scikit-Learn**:
  - `TfidfVectorizer` (Ekstrakcja cech tekstowych)
  - `StandardScaler` (Skalowanie cech numerycznych)
  - `ColumnTransformer` & `Pipeline` (Automatyzacja potoku przetwarzania)
  - `LinearSVC` & `LogisticRegression` (Algorytmy predykcyjne)
- **Regular Expressions (`re`)** - autorski preprocessing i czyszczenie danych tekstowych.
