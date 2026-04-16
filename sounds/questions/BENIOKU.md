# Ses Dosyaları

Bu klasöre soru ve konuşma balonu ses dosyalarını (.mp3) ekleyin.

---

## Dosya İsimlendirme

| Dosya adı | Ne için |
|-----------|---------|
| `q1.mp3` | 1. sorunun sesli okunması |
| `q2.mp3` | 2. sorunun sesli okunması |
| `q7.mp3` | 7. sorunun sesli okunması (varsa) |
| `q7-qs1.mp3` | 7. sorudaki 1. konuşma balonunun sesi |
| `q7-qs2.mp3` | 7. sorudaki 2. konuşma balonunun sesi |

Genel kural: `q{soruNo}.mp3` ve `q{soruNo}-qs{balonNo}.mp3`

---

## questions.json Kullanımı

### Tek sesli soru (hoparlör ikonu çıkar)

```json
{
  "id": 1,
  "text": "Soru metni...",
  "audio": "sounds/questions/q1.mp3",
  "audio_parts": null,
  "answers": [...]
}
```

### Konuşma balonlu soru — sadece ses (🔊 Mert, 🔊 Selin gibi görünür)

```json
{
  "id": 7,
  "text": "Soru metni...",
  "audio": "sounds/questions/q7.mp3",
  "audio_parts": [
    "sounds/questions/q7-qs1.mp3",
    "sounds/questions/q7-qs2.mp3",
    "sounds/questions/q7-qs3.mp3"
  ],
  "audio_parts_labels": ["Mert", "Selin", "Tuna"],
  "answers": [...]
}
```

> `audio_parts_labels` eklenmezse butonlar `🔊 1`, `🔊 2`, `🔊 3` şeklinde görünür.

### Konuşma balonlu soru — ses + görsel (resim ve isim birlikte görünür)

```json
{
  "id": 7,
  "text": "Soru metni...",
  "audio": "sounds/questions/q7.mp3",
  "audio_parts": [
    "sounds/questions/q7-qs1.mp3",
    "sounds/questions/q7-qs2.mp3",
    "sounds/questions/q7-qs3.mp3"
  ],
  "audio_parts_labels": ["Mert", "Selin", "Tuna"],
  "audio_parts_images": [
    "images/mert.png",
    "images/selin.png",
    "images/tuna.png"
  ],
  "answers": [...]
}
```

> Görsel dosyalarını istediğiniz klasöre koyabilirsiniz, yolu doğru yazmanız yeterli.
> `audio_parts_images` eklenmezse sadece isim+hoparlör ikonu görünür, görsel olmadan çalışır.

### Cevap sesi (şıkların yanında hoparlör ikonu çıkar)

```json
"answers": [
  { "text": "Mert", "audio": "sounds/questions/q7-a1.mp3", "correct": true },
  { "text": "Selin", "audio": null, "correct": false }
]
```

> `audio` alanı `null` olan şıklarda ses ikonu çıkmaz.

---

## Ses yoksa

`audio` ve `audio_parts` alanlarını `null` bırakın. Ses butonu hiç görünmez.

```json
"audio": null,
"audio_parts": null
```

---

## Soru Süresi (Zamanlayıcı)

Zamanlayıcı süresi otomatik olarak hesaplanır: ses dosyasının/dosyalarının toplam uzunluğu + düşünme süresi.

### Genel düşünme süresi (tüm sorular için)

`questions.json` dosyasının en üstüne ekleyin:

```json
{
  "thinking_time": 3,
  "questions": [...]
}
```

### Soru bazında farklı düşünme süresi

İlgili sorunun içine ekleyin:

```json
{
  "id": 7,
  "thinking_time": 5,
  ...
}
```

> Soru bazında `thinking_time` varsa o kullanılır, yoksa üstteki genel değer devreye girer.
> Ses dosyası hiç yoksa varsayılan olarak 10 saniye kullanılır.

---

## Özet: Hangi alanlar zorunlu, hangileri opsiyonel?

| Alan | Zorunlu mu? | Açıklama |
|------|------------|----------|
| `audio` | Hayır | Tek ses butonu için |
| `audio_parts` | Hayır | Birden fazla konuşma balonu için |
| `audio_parts_labels` | Hayır | Butonlarda isim göstermek için |
| `audio_parts_images` | Hayır | Butonlarda görsel göstermek için |
| `thinking_time` | Hayır | Ses bittikten sonra eklenen düşünme süresi (saniye) |
