# APEX BIO 3D (dailygym77) — Texniki Audit və Baza Analizi (Phase 0)

Tarix: 9 Sentyabr 2026  
Status: Phase 0 Tamamlandı (Phase 1 üçün təsdiq gözlənilir)

---

## 1. Layihənin Fayl və Qovluq Strukturu

```
/Users/anargadirli/Desktop/gemsite/
├── .git/                      # Git versiya nəzarəti
├── .gitignore                 # Git ignore qaydaları (node_modules, .DS_Store və s.)
├── .vercel/                   # Vercel layihə meta-məlumatları (dailygym77)
├── .vercelignore              # Vercel deployment filtrləri
├── vercel.json                # Vercel konfiqurasiyası ("name": "dailygym77", "cleanUrls": true)
├── README.md                  # Mövcud sistemin xüsusiyyətlər təsviri
├── index.html                 # Əsas, canlı və Vercel-ə yayımlanan tək-səhifəlik tətbiq (~4048 sətir, 204 KB)
├── index_before_redesign.html # Əvvəlki redesign backup-ı (161 KB)
├── index_gym_biomechanics.html# İlkin biomexanika prototipi (75 KB)
├── index_legacy_backup.html   # Tailwind əsaslı köhnə versiya backup-ı (127 KB)
└── node_modules/              # Əvvəlki sınaqlardan qalmış lokal paketlər (istehsalatda istifadə olunmur)
```

> **Qeyd:** Canlı production mühitində (Vercel) çalışan yeganə və əsas fayl birbaşa `index.html` faylıdır. Bütün köməkçi və backup faylları `.vercelignore` daxilində bloklanıb.

---

## 2. Texnologiya Stack-i

| Sahə | Mövcud Yanaşma | Detallar |
| :--- | :--- | :--- |
| **Bundler / Build Tool** | **Heç biri (Zero-build)** | Sayt birbaşa statik HTML/JS kimi işləyir. NPM build tələb olunmur; Vercel-ə dərhal və sıfır xəta riski ilə deploy olunur. |
| **Framework** | **Saf JavaScript (Vanilla ES6+)** | React/Vue/Svelte kimi kənar runtime kitabxanalar yoxdur. DOM manipulyasiyası birbaşa və sürətlidir. |
| **3D Qrafika Mühərriki** | **Three.js r128 + OrbitControls** | CDN vasitəsilə yüklənir (`cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`). WebGL renderer, kölgə xəritələri (PCFSoftShadowMap) və OrbitControls daxildir. |
| **CSS və Stillər** | **Vanilla CSS (Design Tokens)** | Xüsusi CSS dəyişənləri (`--bg-base`, `--accent-cyan`, `--accent-emerald`, `--border-subtle` və s.) ilə qurulmuş Glassmorphism dizayn sistemi. Tailwind CDN keçmiş nüsxələrdən təmizlənib. |
| **Səs Mühərriki** | **Web Audio API** | Brauzerin daxili audio sintezatoru ilə kabel sürtünməsi, çəki plitələrinin dəmir klik səsi və ritmik nəfəsvermə sintez olunur (heç bir böyük MP3/WAV faylı yüklənmir). |
| **Hostinq** | **Vercel** | Layihə adı: `dailygym77`. Statik `index.html` birbaşa təqdim olunur. |

---

## 3. Mövcud 3D Səhnə, Kamera və Animasiya Sistemi (Baza Xətti)

### A. Səhnə və İşıqlandırma
- `THREE.Scene()` tünd fon rəngi (`0x0a0e18`) və `FogExp2` ilə yaradılıb.
- Çoxnöqtəli studiya işığı:
  - **AmbientLight:** Ümumi yumşaq baza işığı (0.55 intensivlik).
  - **Key Directional Light (0x38bdf8):** Sol-ön bucaqdan əzələ relyefini vuran əsas işıq + yumşaq kölgələr.
  - **Rim Directional Light (0x34d399):** Sağ-arxadan kontur işığı (idmançının siluetini fondan ayırır).
  - **Warm Fill Light (0xfbbf24):** İsti kölgə doldurma işığı.

### B. Kamera İdarəetməsi
- `THREE.PerspectiveCamera` (FOV: 42°, Near: 0.1, Far: 50).
- `OrbitControls` həm siçanla, həm də toxunma (touch) ilə 360° sərbəst fırlanma, yaxınlaşdırma və fırlatma təmin edir.
- Hazır kamera mövqeləri: `Hero (45°)`, `Ön (Front)`, `Profil (Side)` və avtomatik `360° Orbit`.

### C. 3D Atlet və Avadanlıq Anatomiyası
- **Atlet:** Procedural BufferGeometry ilə qurulub (Körpücük sümükləri, sternum, ayrılmış döş lifləri, 3 başlı deltoid, bicep/tricep/brachialis, skapulalar, VMO göz yaşı formalı kvadriseps, baldır və Axill vətəri).
- **Stansiya və Sərbəst Çəkilər:** Polad çərçivə, bələdçi relslər, fiziki qalxan çəki plitələri, çəkili kabellər, V-bar, Lat bar, oturacaq və altlıqlar, habelə qantellər.
- **Dinamik Deformasiya:** Yığılma fazasında hədəf əzələlərin radial qalınlaşması (bulging) və gərilmə fazasında uzanması.

### D. Kinematika və Animasiya Mühərriki
- `requestAnimationFrame` dövrəsi ilə saat (`THREE.Clock`) əsasında işləyir.
- **3-1-1-1 Rep Tempi:**
  1. Eksentrik (3.0s — aramla endirmə)
  2. Gərilmə izometrik pauzası (0.8s)
  3. Konsentrik sürücü (1.2s — partlayıcı itələmə/çəkmə)
  4. Zirvə sıxılma pauzası (1.0s)
- **13 Məşqin Riyazi Kinematikası:**
  - Gün 1 (Push): Chest Press, Pec Fly, Shoulder Press, Triceps Pushdown
  - Gün 2 (Pull): Lat Pulldown, Seated Cable Row, Biceps Curl, Hammer Curl
  - Gün 3 (Legs): Goblet Squat, Leg Extension, Romanian Deadlift (RDL), Walking Lunge
  - Gün 4 (Upper Volume): Chest Press, Lateral Raise, Lat Pulldown, Hammer Curl
- **Düzgün vs Səhv Rejimi:** Hər hərəkət üçün həm biomekanik optimal trayektoriya, həm də tipik zədələyici səhv bucaqları proqramlaşdırılıb.

### E. 3D Analiz Qatı (Pro Alətlər)
- **3D Oynaq Bucaqları:** Real vaxtda dərəcə hesablayan qövs şleyfləri.
- **Kinovea Trayektoriya Lenti:** Hərəkətin havada cızdığı xətti qeyd edən 3D lent.
- **Canlı EMG Göstəriciləri:** Əzələ aktivasiya faizləri.

---

## 4. 3D Modelin Qiymətləndirilməsi (Procedural vs Xarici Rigged Model)

*Master Brief-də qeyd olunan sual:* **"Manken" hissini necə azaltmaq olar — xarici rigged GLTF model lazımdırmı?**

- **Xarici Rigged GLTF Modelin Riskləri:**
  1. Xarici FBX/GLTF insan modeli 15–40 MB həcm yaradır; mobil şəbəkələrdə gec yüklənir.
  2. 13 fərqli hərəkətin həm "Düzgün", həm də "Səhv" kinematikası üçün xarici modeldə sümük riqqinqinin (skeletal rigging) və kabel/qantel tutuşlarının eyni dəqiqliklə kodlanması inanılmaz dərəcədə qırılqandır və animasiyaların hərəkət stansiyasına toxunma (clipping) xətaları yaradır.
- **Tövsiyə Olunan Optimal Həll:**
  Mövcud sıfır-yüklənmə gecikməli procedural insan modelini saxlamaq, lakin **"manken" soyuqluğunu aradan qaldırmaq üçün**:
  1. Materiallara insan dərisi və idmançı estetikası verən yumşaq Subsurface/PBR işıqlanması əlavə etmək.
  2. Boşdayanma (idle) və hərəkət zamanı zərif təbii nəfəsalma və tarazlıq mikrosallanması gətirmək.
  3. Mərhələli şəkildə bütün bucaq/EMG xətlərini **Pro Mode** arxasına gizlətmək ki, adi görünüşdə model qabağa çıxsın.

---

## 5. Phase 0 Nəticəsi və Sprint 1 Yol Xəritəsi

Baza auditimiz təsdiq edir ki, **3D mühərriki texniki cəhətdən çox güclüdür və heç bir kənar ağır asılılığı yoxdur.**  
Əsas problem arxitekturadır: tətbiq indiyə qədər **"tək ekranlı mühəndislik aləti"** kimi təqdim olunub.

Hibrid arxitekturaya keçid üçün növbəti addımlar:
- **Phase 1:** Sayt Xəritəsi və Çox-Səhifəli Naviqasiya (Ana Səhifə / 4-Günlük Proqram Kartları / Məşq Detalı / Tərəqqi / Parametrlər).
- **Phase 2:** Yeni Dizayn Sistemi (Gözoxşayan tünd palitra, elektrik aksent `#B6FF3C`, təmiz müasir tipografiya, glass kartlar).
- **Phase 3:** 3D Simulyatorun Default (Sadə/İsti) və Pro/Coach rejimlərinə bölünməsi.
