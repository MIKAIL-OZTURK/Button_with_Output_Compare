# ⏱️ STM32 - Output Compare ile Gecikmeli LED Yakma

Bu proje, **STM32F4 serisi** bir mikrodenetleyici kullanarak, **Output Compare** modu ile butona basıldıktan sonra belirli bir süre gecikmeyle LED yakma uygulamasını gerçekleştirmektedir. `HAL` kütüphanesi kullanılarak kesme tabanlı bir çözüm uygulanmıştır.

## 🎯 Proje Amacı

- Zamanlama işlemlerini `HAL_Delay` gibi bloklayıcı fonksiyonlar yerine, donanım zamanlayıcısı ile gerçekleştirmek.
- `Output Compare` modunu kullanarak **gerçek zamanlı kesmelerle** gecikmeli bir işlem yapmak.

## 🧰 Kullanılan Donanım

- STM32F4 Discovery kartı
- PA5: LED
- PA0: Yerleşik USER Buton

## ⚙️ Timer Ayarları

| Parametre   | Değer        |
|-------------|--------------|
| Timer       | TIM2         |
| Mod         | Output Compare (TIMING mode) |
| Prescaler   | 8399         |
| Timer Clock | 10 kHz (0.1 ms çözünürlük) |
| ARR         | 0xFFFFFFFF (maksimum sayaç) |
| Kanal       | TIM2_CH1     |

## 🚀 Uygulama Akışı

1. Butona basıldığında anlık sayaç değeri alınır.
2. 2 saniyelik (20.000 tick) gecikme hesaplanır.
3. Output Compare değeri olarak `şu an + 20000` ayarlanır.
4. Timer değeri bu eşleşmeye ulaştığında kesme oluşur.
5. Kesme fonksiyonu içinde LED yakılır.

## 🧠 Teknik Detaylar

- **Kesme yönetimi:** `HAL_TIM_OC_DelayElapsedCallback` fonksiyonu ile yapılır.
- **Gecikme hassasiyeti:** Timer clock çözünürlüğüne bağlıdır (bu örnekte 0.1ms).
- **Buton debounce:** Basit `HAL_Delay(300)` ile çözülmüştür.


## Uygulama Videosu

https://github.com/user-attachments/assets/209609f2-adf3-4669-97ae-772e08fa7506


