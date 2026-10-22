# Traffic Sign Detection (YOLOv8 vs OpenCV)

Projekt porównuje skuteczność nowoczesnego podejścia opartego na Głębokich Sieciach Neuronowych (YOLOv8) z klasycznym pipelinem wizyjnym w OpenCV. Dodatkowo bada wpływ 3 różnych technik preprocessingu obrazu na ostateczną skuteczność detekcji znaków drogowych.

> **Podsumowanie:** YOLOv8 z preprocessingiem CLAHE osiąga znacznie lepsze wyniki niż klasyczne podejście, osiągając **mAP@0.5 na poziomie 0.96**.

![Przykładowa detekcja](
<p align="center">
<img width="300"" alt="obraz" src="https://github.com/user-attachments/assets/40a03bf4-383c-4512-bffe-7c0cf8823194" />
<img width="300" alt="obraz" src="https://github.com/user-attachments/assets/bba16ac8-564c-4d18-b5f6-7d0ea2b2392d" />
<img width="300" alt="obraz" src="https://github.com/user-attachments/assets/5aec1ef3-877c-445d-ba6c-3a4373985b4b" />
</p>)



## Zakres projektu
- **Klasyczne OpenCV:** Próba detekcji znaków za pomocą progowania, detekcji krawędzi i konturów (jako baseline).
- **Preprocessing:** Przetestowanie 3 wariantów przygotowania obrazu, ze szczególnym uwzględnieniem algorytmu **CLAHE** (Contrast Limited Adaptive Histogram Equalization) do radzenia sobie ze słabym oświetleniem.
- **Deep Learning (YOLOv8):** Zbudowanie i ewaluacja modelu detekcji obiektów.

## Wyniki eksperymentów
Porównanie wpływu preprocessingu na skuteczność modelu YOLOv8 (próg ufności: 0.25). 

| Wersja Modelu | Preprocessing | Precyzja (P) | Czułość (Recall) | mAP@50 | mAP@50-95 |
|---|---|---|---|---|---|
| V1 (Bazowy) | Brak | 1.000 | 0.771 | 0.767 | 0.620 |
| V2 | equalizeHist | 1.000 | 0.704 | 0.701 | 0.547 |
| **V3** | **CLAHE** | **1.000** | **0.960** | **0.955** | **0.766** |

**Kluczowy wniosek:** Zwykłe wyrównanie histogramu (V2) wręcz pogorszyło wyniki bazowe. Dopiero zastosowanie algorytmu CLAHE (V3) pozwoliło modelowi skutecznie radzić sobie z cieniami i prześwietleniami, podnosząc czułość (Recall) z 77% aż do 96%. Pełne zestawienie wyników dla poszczególnych znaków znajduje się w notatniku.

## Wnioski
- Klasyczne metody OpenCV są zbyt wrażliwe na zmienne warunki (takie jak oświetlenie czy perspektywa), by sprawdzić się w rzeczywistych sytuacjach drogowych.
- Zastosowanie CLAHE jako preprocessingu przed podaniem obrazu do YOLOv8 stabilizuje predykcje i zauważalnie podnosi recall, szczególnie na niedoświetlonych zdjęciach.
- Zoptymalizowany próg ufności (confidence threshold = 0.25) zapewnia optymalny balans między precyzją a czułością.

## Stack technologiczny
Python, YOLOv8 (Ultralytics), OpenCV, matplotlib

## Zbiór danych
Model został wytrenowany na autorskim zbiorze danych. Zdjęcia znaków drogowych wykonałem samodzielnie, celowo uwzględniając różne warunki drogowe, zmiany oświetlenia (np. mocne słońce, cień) oraz różne kąty nachylenia, aby przetestować odporność (robustness) modelu w rzeczywistych, trudnych sytuacjach, z którymi nie radziło sobie klasyczne podejście OpenCV.

## Uruchomienie
Projekt jest w pełni udokumentowany w notatniku Jupyter. Możesz go uruchomić bezpośrednio w Google Colab.
