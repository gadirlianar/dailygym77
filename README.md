# APEX BIO 3D (dailygym77)

İnteraktiv 3D Məşq & Biomexanika Təlimatçısı, 4-Günlük Fərdi Məşq Proqramı və Tərəqqi İzləmə Sistemi.

---

## 🚀 Əsas Funksiyalar və Memarlıq

### 1. Çox-Səhifəli Tətbiq Quruluşu (5 Görünüş)
- 🏠 **Ana Səhifə (`#view-landing`):** İnteraktiv hero təqdimatı, 4 split xülasəsi, əsas xüsusiyyət kartları və 1-kliklə sürətli məşqə başlama.
- 📋 **4-Günlük Proqram (`#view-programs`):** Bütün 4 günün (İtələmə, Çəkmə, Ayaq, Üst Bədən Həcmi) hərəkət siyahısı, hədəf əzələləri və müddəti.
- ⚡ **3D Məşq Zalı (`#view-workout`):** 360° interaktiv WebGL səhnəsi, canlı insan anatomiyası, 3-1-1-1 atletik rep tempi, təkrar sayğacı və set qeydiyyatı.
- 📊 **Tərəqqi & Gündəlik (`#view-progress`):** 4 açar statistika kartı, 7-günlük dinamik həcm sütun qrafiki, sessiya tarixçəsi, əllə məşq əlavə etmə və `kg`/`lb` vahid dəstəyi.
- ⚙️ **Parametrlər (`#view-settings`):** Çəki vahidi (kq / lb), 3D qrafika keyfiyyəti (Ultra / Eko) və audio tənzimləmələri.

### 2. Hibrid İstifadəçi Təcrübəsi (Default vs Pro Mode)
- **Default Sadə Rejim (İlkin):** Təmiz, gözoxşayan və motivasiyaedici interfeys. Mürəkkəb mühəndislik qrafikləri gizlədilir, diqqət hərəkətin düzgün icrasına və "3 Qızıl Qayda"ya yönəldilir.
- **Pro / Coach Mode (`🔬 Pro Analitika`):** Bir toxunuşla Kinovea tipli 3D trayektoriya lenti, real vaxt dərəcə qövsləri (Protractor) və % EMG əzələ aktivasiya qrafikləri aktivləşir.

### 3. İsti Məşqçi Tonu & "3 Qızıl Qayda"
- 13 hərəkətin hamısı üçün qayğıkeş, aydın və motivasiyaedici məşqçi dili.
- Alarmlı zədə xəbərdarlıqları əvəzinə konstruktiv **"💡 Məşqçi Məsləhəti: Diqqət Yetir"** kartı və dostyana 3D oynaq bələdçisi.

### 4. Real Vaxt Məşq Zamanı Set Qeydiyyatı (Workout Logger)
- Hərəkət zamanı çəki və təkrar stepperi (`−` / `+`).
- Seti qeyd etmə, avtomatik fasilə taymerinin işə düşməsi və tamamlanmış məşqin ümumi tonnajının hesablanaraq `localStorage`-a yazılması.

### 5. Mobil-First Responsivlik & 60 FPS Performans
- **Off-Canvas HUD:** Mobil ekranlarda (`<= 768px`) 3D model maneəsiz qalır; üzən `📋 Hərəkətlər & Setlər` düyməsi ilə idarəetmə çəkməcəsi açılır və bağlanır.
- **Toxunma Jestləri:** `touch-action: none;` sayəsində mobil telefonlarda 1 barmaqla 360° fırlanma və 2 barmaqla böyütmə sıçrayışsız işləyir.
- **Canlı FPS & Ultra/Eko Keçidi:** Real vaxt kadr tezliyi sayğacı və 1-kliklə kölgəsiz Eko / batareya qənaəti rejiminə keçid.

---

## 🏋️ 4-Günlük Balanslaşdırılmış Proqram (13 Hərəkət)

1. **GÜN 1: İtələmə (Push)**
   - Stansiyada Chest Press
   - Stansiyada Pec Deck Fly (Kəpənək)
   - Dumbbell Shoulder Press
   - Stansiyada Triceps Pushdown
2. **GÜN 2: Çəkmə (Pull)**
   - Stansiyada Lat Pulldown
   - Stansiyada Seated Cable Row
   - Dumbbell Biceps Curl
   - Dumbbell Hammer Curl
3. **GÜN 3: Ayaq & Baza (Legs)**
   - Dumbbell Goblet Squat
   - Stansiyada Leg Extension
   - Dumbbell Romanian Deadlift (RDL)
   - Dumbbell Walking Lunge
4. **GÜN 4: Üst Bədən İxtisaslaşması (Upper Volume)**
   - Stansiyada Chest Press
   - Dumbbell Lateral Raise
   - Stansiyada Lat Pulldown
   - Dumbbell Hammer Curl

---

## 🛠 Texnoloji Stack
- **Frontend:** Pure Static Vanilla HTML5, CSS3, JavaScript (ES6+).
- **3D Mühərrik:** Three.js r128 (OrbitControls, PBR Materiallar, Deformasiya Kinematikası).
- **Audio:** Web Audio API (İdman zalı mühiti, metronom və kontakt səsləri).
- **Deployment:** Vercel (Zero-build deployment, sıfır npm asılılığı).

