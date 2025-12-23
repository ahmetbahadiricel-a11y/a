<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8" />
  <title>Boost Akademi | Koçluk Paneli</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- Font & Icons -->
  <link rel="stylesheet"
        href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

  <!-- Chart.js -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: radial-gradient(circle at top, #1e1e1e 0, #050505 55%, #000 100%);
      color: #f5f5f5;
      min-height: 100vh;
    }

    a { color: inherit; text-decoration: none; }

    .app {
      max-width: 1280px;
      margin: 24px auto;
      padding: 16px;
    }

    /* HEADER */
    .header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 12px 18px;
      border-radius: 18px;
      background: linear-gradient(135deg, #111, #181818);
      box-shadow: 0 16px 40px rgba(0, 0, 0, 0.7);
      border: 1px solid #262626;
      margin-bottom: 18px;
    }

    .header-left {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .logo-circle {
      width: 48px;
      height: 48px;
      border-radius: 50%;
      overflow: hidden;
      border: 2px solid #ff8800;
      background: radial-gradient(circle at 30% 20%, #ffb84d, #ff7a00 55%, #b34700 100%);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .logo-circle img {
      width: 60px;
      height: auto;
      object-fit: contain;
      mix-blend-mode: screen;
    }

    .brand-title {
      display: flex;
      flex-direction: column;
      gap: 2px;
    }

    .brand-title span:first-child {
      font-weight: 700;
      letter-spacing: 0.06em;
      font-size: 0.9rem;
      color: #ffb84d;
      text-transform: uppercase;
    }

    .brand-title span:last-child {
      font-weight: 500;
      font-size: 0.78rem;
      color: #bbbbbb;
    }

    .header-right {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .coach-name {
      font-size: 0.85rem;
      color: #e5e5e5;
    }

    .pill {
      font-size: 0.75rem;
      padding: 6px 10px;
      border-radius: 999px;
      background: rgba(255, 136, 0, 0.1);
      border: 1px solid rgba(255, 136, 0, 0.4);
      color: #ffb84d;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    /* TOP BAR (STUDENT SELECT & QUICK INFO) */
    .top-bar {
      display: flex;
      gap: 12px;
      margin-bottom: 12px;
      flex-wrap: wrap;
    }

    .card {
      background: radial-gradient(circle at top left, #1a1a1a, #090909 70%);
      border-radius: 18px;
      border: 1px solid #242424;
      padding: 14px 16px;
      box-shadow: 0 12px 30px rgba(0, 0, 0, 0.7);
    }

    .top-bar .card {
      flex: 1;
      min-width: 220px;
    }

    .card-title {
      font-size: 0.82rem;
      font-weight: 600;
      color: #bbbbbb;
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .card-title i {
      color: #ff8800;
      font-size: 0.9rem;
    }

    .select-input, .text-input, .number-input, .time-input, .date-input, .textarea-input {
      width: 100%;
      padding: 8px 10px;
      border-radius: 10px;
      border: 1px solid #333;
      background: #111;
      color: #f5f5f5;
      font-size: 0.85rem;
      outline: none;
    }

    .select-input:focus,
    .text-input:focus,
    .number-input:focus,
    .time-input:focus,
    .date-input:focus,
    .textarea-input:focus {
      border-color: #ff8800;
      box-shadow: 0 0 0 1px rgba(255, 136, 0, 0.35);
    }

    .select-input {
      cursor: pointer;
    }

    .subtext {
      font-size: 0.78rem;
      color: #888888;
      margin-top: 4px;
    }

    .badge {
      padding: 4px 8px;
      border-radius: 999px;
      font-size: 0.70rem;
      background: rgba(255, 255, 255, 0.03);
      border: 1px solid rgba(255, 255, 255, 0.06);
      color: #bbbbbb;
      display: inline-flex;
      align-items: center;
      gap: 4px;
    }

    .badge i {
      font-size: 0.75rem;
    }

    .badge-orange {
      background: rgba(255, 136, 0, 0.12);
      border-color: rgba(255, 136, 0, 0.4);
      color: #ffcc7a;
    }

    /* NAV TABS */
    .tabs-nav {
      display: flex;
      gap: 8px;
      margin: 10px 0 16px;
      border-bottom: 1px solid #222;
      overflow-x: auto;
      padding-bottom: 4px;
    }

    .tab-button {
      position: relative;
      border: none;
      background: transparent;
      color: #aaaaaa;
      padding: 8px 14px;
      border-radius: 999px;
      cursor: pointer;
      font-size: 0.8rem;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      white-space: nowrap;
    }

    .tab-button i {
      font-size: 0.9rem;
    }

    .tab-button.active {
      background: linear-gradient(135deg, #ff8800, #ffb84d);
      color: #151515;
      font-weight: 600;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.7);
    }

    .tab-button.active i {
      color: #151515;
    }

    .tab-button:not(.active):hover {
      background: rgba(255, 255, 255, 0.04);
    }

    /* TABS CONTENT */
    .tabs-container {
      border-radius: 18px;
      border: 1px solid #242424;
      background: radial-gradient(circle at top, #151515, #050505);
      box-shadow: 0 16px 40px rgba(0, 0, 0, 0.8);
      padding: 16px;
      min-height: 260px;
    }

    .tab-panel { display: none; }
    .tab-panel.active { display: block; }

    /* GRID HELPERS */
    .grid-2 {
      display: grid;
      grid-template-columns: 1.7fr 1.3fr;
      gap: 14px;
    }
    .grid-3 {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 12px;
    }

    @media (max-width: 900px) {
      .grid-2 { grid-template-columns: 1fr; }
      .grid-3 { grid-template-columns: 1fr; }
      .header { flex-direction: column; align-items: flex-start; gap: 10px; }
      .header-right { align-self: stretch; justify-content: space-between; }
    }

    /* BUTTONS */
    .btn {
      border: none;
      border-radius: 999px;
      padding: 7px 14px;
      font-size: 0.78rem;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-weight: 500;
    }

    .btn-primary {
      background: linear-gradient(135deg, #ff8800, #ffb84d);
      color: #151515;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.8);
    }

    .btn-primary:hover {
      filter: brightness(1.05);
    }

    .btn-outline {
      background: transparent;
      border: 1px solid #333;
      color: #dddddd;
    }

    .btn-outline:hover {
      border-color: #ff8800;
      color: #ffcc7a;
    }

    /* TABLES */
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.78rem;
    }

    th, td {
      padding: 6px 8px;
      border-bottom: 1px solid #222;
      text-align: left;
      vertical-align: middle;
    }

    th {
      font-weight: 600;
      color: #c5c5c5;
      background: rgba(255, 255, 255, 0.02);
    }

    tr:nth-child(even) td {
      background: rgba(255, 255, 255, 0.01);
    }

    .tag {
      display: inline-flex;
      align-items: center;
      gap: 4px;
      padding: 4px 8px;
      border-radius: 999px;
      font-size: 0.7rem;
      border: 1px solid rgba(255, 255, 255, 0.15);
      background: rgba(255, 255, 255, 0.03);
    }

    .tag.tyt { border-color: rgba(0, 191, 255, 0.6); color: #7fd5ff; }
    .tag.ayt { border-color: rgba(140, 255, 160, 0.7); color: #a0ffb1; }

    /* COLOR LEGEND FOR SCHEDULE */
    .legend {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-top: 6px;
    }

    .legend-item {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-size: 0.75rem;
      color: #bbbbbb;
    }

    .legend-color {
      width: 14px;
      height: 14px;
      border-radius: 4px;
      border: 1px solid rgba(0, 0, 0, 0.5);
    }

    .legend-color-topic { background: linear-gradient(135deg, #ff8800, #ffb84d); }
    .legend-color-questions { background: linear-gradient(135deg, #5c6fff, #8695ff); }

    /* SCHEDULE CELLS */
    .schedule-grid {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.78rem;
      margin-top: 6px;
    }

    .schedule-grid th, .schedule-grid td {
      border: 1px solid #262626;
      text-align: center;
      padding: 6px 4px;
    }

    .schedule-slot {
      min-height: 34px;
      border-radius: 8px;
      padding: 4px;
      font-size: 0.7rem;
      line-height: 1.2;
      text-align: left;
      color: #f9f9f9;
      cursor: pointer;
    }

    .slot-topic {
      background: linear-gradient(135deg, #ff8800, #ffb84d);
      color: #151515;
    }

    .slot-questions {
      background: linear-gradient(135deg, #5c6fff, #8695ff);
    }

    /* ALERT / INFO TEXT */
    .info {
      font-size: 0.8rem;
      color: #bbbbbb;
      margin-top: 4px;
    }

    .info-strong {
      color: #ffcc7a;
      font-weight: 500;
    }

    .muted {
      font-size: 0.74rem;
      color: #777777;
    }

    .pill-small {
      padding: 2px 7px;
      border-radius: 999px;
      border: 1px solid rgba(255,255,255,0.18);
      font-size: 0.68rem;
      color: #cccccc;
      display: inline-flex;
      align-items: center;
      gap: 4px;
    }

    .status-dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: #2ecc71;
    }

    .status-dot.red { background: #ff4d4d; }

    .textarea-input {
      min-height: 70px;
      resize: vertical;
    }

    /* CHART CONTAINER */
    .chart-box {
      padding: 8px;
      border-radius: 14px;
      border: 1px solid #222;
      background: radial-gradient(circle at top left, #1a1a1a, #050505);
      height: 210px;
    }

    canvas {
      width: 100% !important;
      height: 100% !important;
    }
    ...
            /* senin şu anki 460 satırlık css kodların */
        ...
        ...
        /* BURAYA KADAR SENİN ESKİ KODLARIN VAR */

        /* === DERS PROGRAMI SLOT RENKLERİ === */
        .schedule-slot {
            transition: background-color 0.2s ease, color 0.2s ease, border-color 0.2s ease;
        }

        .slot-type-konu { ... }
        .slot-type-soru { ... }
        .slot-type-deneme { ... }
        .slot-type-paragraf { ... }
        .slot-type-problem { ... }
        .slot-type-okuma { ... }
        .slot-type-tekrar { ... }
        .slot-type-mola { ... }
        .slot-type-uyku { ... }
        .slot-type-gorusme { ... }
/* == SAAT PANELİ YENİ STİLLER == */
.time-editor {
  background:#1a1a1a;
  padding:12px;
  border-radius:10px;
  margin-bottom:20px;
}
.time-editor h3 {
  margin:0 0 10px 0;
  font-size:16px;
  color:#ff8c32;
}
.time-list {
  display:flex;
  flex-wrap:wrap;
  gap:8px;
  margin-bottom:10px;
}
.time-tag {
  background:#222;
  border:1px solid #444;
  padding:5px 10px;
  border-radius:6px;
  cursor:pointer;
}
.time-tag:hover {
  background:#333;
}
.time-actions {
  display:flex;
  gap:10px;
}
.btn-orange {
  background:#ff8c32;
  color:white;
  border:none;
  padding:5px 10px;
  border-radius:6px;
  cursor:pointer;
}
.btn-orange:hover {
  background:#ff7a00;
}
/* Saat editörü kutusu */
.time-editor {
    background:#1a1a1a;
    padding:12px;
    border-radius:10px;
    margin-bottom:20px;
}

/* Başlık */
.time-editor h3 {
    margin:0 0 10px 0;
    font-size:16px;
    color:#ff8c32;
}

/* Mevcut saat etiketleri */
.time-list {
    display:flex;
    flex-wrap:wrap;
    gap:8px;
    margin-bottom:10px;
}

.time-tag {
    background:#222;
    border:1px solid #444;
    padding:5px 10px;
    border-radius:6px;
    cursor:pointer;
}

.time-tag:hover {
    background:#333;
}

/* Saat ekleme input + buton */
.time-actions {
    display:flex;
    gap:10px;
}

    </style>
</head>

<body>
<div class="app">
  <!-- HEADER -->
  <header class="header">
    <div class="header-left">
      <div class="logo-circle">
		<!-- Logonun bulunduğu dosya yolunu kendine göre güncelle -->
        <img src="/images/logo.jpg" alt="Boost Akademi Logo">
      </div>
      <div class="brand-title">
        <span>BOOST AKADEMİ</span>
        <span>Online Koçluk Sistemi</span>
      </div>
    </div>
    <div class="header-right">
      <div class="coach-name">
        <span id="coachNameLabel">Koç Paneli</span>
      </div>
      <div class="pill">
        <i class="fa-solid fa-bolt"></i>
        Koçluk Modülü
      </div>
    </div>
  </header>

  <!-- TOP BAR -->
  <div class="top-bar">
    <!-- STUDENT SELECT -->
    <div class="card">
      <div class="card-title">
        <i class="fa-solid fa-user-graduate"></i>
        Öğrenci Seç
      </div>
      <select id="studentSelect" class="select-input">
        <option value="">Öğrenci seçiniz...</option>
      </select>
      <div class="subtext">
        <span id="studentInfoText">Önce öğrenciyi seçin, tüm veri girişleri o öğrenciye kayıt edilecek.</span>
      </div>
    </div>

    <!-- PROGRAM START & MEETING DAY -->
    <div class="card">
      <div class="card-title">
        <i class="fa-solid fa-calendar-week"></i>
        Program Başlangıcı & Toplantı Günü
      </div>
      <div style="display: flex; gap: 8px; margin-bottom: 6px;">
        <div style="flex:1;">
          <input type="date" id="programStartDate" class="date-input">
          <div class="subtext">Program başlangıç tarihi</div>
        </div>
        <div style="flex:1;">
          <select id="meetingWeekday" class="select-input">
            <option value="">Toplantı günü...</option>
            <option value="Pazartesi">Pazartesi</option>
            <option value="Salı">Salı</option>
            <option value="Çarşamba">Çarşamba</option>
            <option value="Perşembe">Perşembe</option>
            <option value="Cuma">Cuma</option>
            <option value="Cumartesi">Cumartesi</option>
            <option value="Pazar">Pazar</option>
          </select>
          <div class="subtext">Haftalık görüşme günü</div>
        </div>
      </div>
      <div style="display:flex; gap:8px; align-items:center;">
        <div style="flex:1;">
          <input type="time" id="meetingTime" class="time-input">
          <div class="subtext">Toplantı saati</div>
        </div>
        <button class="btn btn-outline" id="saveProgramSettingsBtn">
          <i class="fa-regular fa-floppy-disk"></i>
          Kaydet
        </button>
      </div>
      <div class="subtext" id="programSettingsLabel"></div>
    </div>

    <!-- WEEK SUMMARY -->
    <div class="card">
      <div class="card-title">
        <i class="fa-solid fa-chart-line"></i>
        Haftalık Özet
      </div>
      <div class="info">
        <span class="muted">Bu hafta hedef tamamlama: </span>
        <span class="info-strong" id="weeklyCompletionLabel">%0</span>
      </div>
      <div class="info" style="margin-top:4px;">
        <span class="muted">Haftalık ortalama günlük çalışma: </span>
        <span class="info-strong" id="weeklyAvgStudyLabel">0s 0dk</span>
      </div>
      <div style="margin-top:6px;">
        <span class="badge badge-orange">
          <i class="fa-solid fa-circle-notch fa-spin"></i>
          Haftalık trend grafikte
        </span>
      </div>
    </div>
  </div>

  <!-- NAV TABS -->
  <nav class="tabs-nav">
    <button class="tab-button active" data-tab="tab-study">
      <i class="fa-solid fa-clipboard-list"></i> Veri Girişi
    </button>
    <button class="tab-button" data-tab="tab-exams">
      <i class="fa-solid fa-book-open-reader"></i> Deneme Girişi
    </button>
    <button class="tab-button" data-tab="tab-reports">
      <i class="fa-solid fa-note-sticky"></i> Raporlar
    </button>
    <button class="tab-button" data-tab="tab-schedule">
      <i class="fa-solid fa-calendar-days"></i> Ders Programı
    </button>
    <button class="tab-button" data-tab="tab-meetings">
      <i class="fa-solid fa-video"></i> Görüşmeler
    </button>
    <button class="tab-button" data-tab="tab-guidance">
      <i class="fa-solid fa-heart-pulse"></i> Rehberlik
    </button>
  </nav>

  <!-- TABS CONTENT -->
  <div class="tabs-container">
    <!-- TAB: STUDY DATA -->
    <section id="tab-study" class="tab-panel active">
      <div class="grid-2">
        <!-- LEFT: DAILY ENTRY FORM -->
        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-pen-to-square"></i>
            Günlük Çalışma Verisi
          </div>

          <div style="display:flex; gap:8px; margin-top:6px;">
            <div style="flex:1;">
              <label class="muted">Tarih</label>
              <input type="date" id="studyDate" class="date-input">
            </div>
            <div style="flex:1;">
              <label class="muted">Ders</label>
              <select id="studySubject" class="select-input">
                <option value="">Ders seç...</option>
                <option value="Matematik">Matematik</option>
                <option value="Geometri">Geometri</option>
                <option value="Türkçe">Türkçe</option>
                <option value="Edebiyat">Edebiyat</option>
                <option value="Tarih">Tarih</option>
                <option value="Coğrafya">Coğrafya</option>
                <option value="Felsefe">Felsefe</option>
                <option value="Din">Din Kültürü</option>
                <option value="Biyoloji">Biyoloji</option>
                <option value="Fizik">Fizik</option>
                <option value="Kimya">Kimya</option>
                <option value="Diğer">Diğer</option>
              </select>
            </div>
          </div>

          <div style="margin-top:8px;">
            <label class="muted">Ünite / Konu</label>
<select id="studyTopic" class="select-input">
    <option value="">Konu seç...</option>
</select>

          </div>

          <div style="display:flex; gap:8px; margin-top:8px;">
            <div style="flex:1;">
              <label class="muted">Çözülen Soru Sayısı</label>
              <input type="number" id="studyQuestions" class="number-input" min="0" step="1" placeholder="Örn: 40">
            </div>
            <div style="flex:1;">
              <label class="muted">Günlük Toplam Çalışma Süresi</label>
              <div style="display:flex; gap:6px;">
                <input type="number" id="studyHours" class="number-input" min="0" step="1" placeholder="Saat">
                <input type="number" id="studyMinutes" class="number-input" min="0" max="59" step="1" placeholder="Dakika">
              </div>
              <div class="subtext">
                Bu süre <strong>günün toplam çalışma süresi</strong>dir, matematikten bağımsız.
              </div>
            </div>
          </div>

          <div style="margin-top:10px; display:flex; justify-content:space-between; align-items:center;">
            <button class="btn btn-primary" id="addStudyEntryBtn">
              <i class="fa-solid fa-plus"></i> Çalışmayı Kaydet
            </button>
            <span class="muted" id="studySaveStatus"></span>
          </div>

          <div style="margin-top:10px;">
            <div class="badge">
              <i class="fa-solid fa-circle-info"></i>
              Haftalar, program başlangıç tarihinden itibaren 7 günlük bloklar olarak hesaplanır.
            </div>
          </div>
        </div>

        <!-- RIGHT: TABLE + WEEKLY STUDY CHART -->
        <div class="card">
          <div class="card-title" style="justify-content:space-between;">
            <span>
              <i class="fa-solid fa-clock-rotate-left"></i>
              Son Çalışmalar & Haftalık Çalışma Trendi
            </span>
          </div>

          <div style="max-height:150px; overflow:auto; margin-bottom:8px;">
            <table>
              <thead>
                <tr>
                  <th>Tarih</th>
                  <th>Ders</th>
                  <th>Konu</th>
                  <th>Soru</th>
                  <th>Top. Süre</th>
                  <th>Hafta</th>
                </tr>
              </thead>
              <tbody id="studyTableBody">
                <!-- JS dolduracak -->
              </tbody>
            </table>
          </div>

          <div class="chart-box">
            <canvas id="weeklyStudyChart"></canvas>
          </div>
        </div>
      </div>
    </section>

    <!-- TAB: EXAMS (TYT & AYT) -->
    <section id="tab-exams" class="tab-panel">
      <div class="grid-2">
        <!-- LEFT: TYT FORM & TABLE -->
        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-book-open"></i>
            TYT Denemesi
          </div>

          <div style="display:flex; gap:8px; margin-top:6px;">
            <div style="flex:1;">
              <label class="muted">Tarih</label>
              <input type="date" id="tytDate" class="date-input">
            </div>
            <div style="flex:1; text-align:right;">
              <span class="tag tyt"><i class="fa-solid fa-bolt"></i> TYT</span>
            </div>
          </div>

          <!-- Dersler: Türkçe, Coğrafya, Tarih, Felsefe, Din, Matematik, Fizik, Kimya, Biyoloji -->
          <div style="margin-top:8px; max-height:180px; overflow:auto;">
            <table>
              <thead>
                <tr>
                  <th>Ders</th>
                  <th>Doğru</th>
                  <th>Yanlış</th>
                  <th>Net</th>
                </tr>
              </thead>
              <tbody id="tytTableBodyForm">
                <!-- JS ile ders satırları eklenecek -->
              </tbody>
            </table>
          </div>

          <div style="margin-top:8px; display:flex; justify-content:space-between; align-items:center;">
            <div>
              <span class="muted">Toplam Net: </span>
              <span class="info-strong" id="tytTotalNetLabel">0.00</span>
            </div>
            <button class="btn btn-primary" id="saveTytExamBtn">
              <i class="fa-solid fa-floppy-disk"></i> TYT Denemesini Kaydet
            </button>
          </div>

          <div style="margin-top:6px; max-height:110px; overflow:auto;">
            <table>
              <thead>
                <tr>
                  <th>Tarih</th>
                  <th>Toplam Net</th>
                </tr>
              </thead>
              <tbody id="tytExamListBody"></tbody>
            </table>
          </div>
        </div>

        <!-- RIGHT: AYT FORM & CHARTS -->
        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-book"></i>
            AYT Denemesi
          </div>

          <div style="display:flex; gap:8px; margin-top:6px;">
            <div style="flex:1;">
              <label class="muted">Tarih</label>
              <input type="date" id="aytDate" class="date-input">
            </div>
            <div style="flex:1; text-align:right;">
              <span class="tag ayt"><i class="fa-solid fa-fire"></i> AYT</span>
            </div>
          </div>

          <!-- AYT Bölümleri & Dersler -->
          <div style="margin-top:8px; max-height:180px; overflow:auto;">
            <table>
              <thead>
                <tr>
                  <th>Bölüm / Ders</th>
                  <th>Doğru</th>
                  <th>Yanlış</th>
                  <th>Net</th>
                </tr>
              </thead>
              <tbody id="aytTableBodyForm">
                <!-- JS ile satırlar eklenecek -->
              </tbody>
            </table>
          </div>

          <div style="margin-top:8px; display:flex; flex-wrap:wrap; gap:6px; align-items:center; justify-content:space-between;">
            <div style="display:flex; flex-direction:column; gap:2px;">
              <span class="muted">Toplam Net: <span class="info-strong" id="aytTotalNetLabel">0.00</span></span>
              <span class="muted">
                Sayısal: <span class="info-strong" id="aytSayisalNetLabel">0.00</span> |
                Sözel: <span class="info-strong" id="aytSozelNetLabel">0.00</span> |
                EA: <span class="info-strong" id="aytEANetLabel">0.00</span>
              </span>
            </div>
            <button class="btn btn-primary" id="saveAytExamBtn">
              <i class="fa-solid fa-floppy-disk"></i> AYT Denemesini Kaydet
            </button>
          </div>

          <div style="margin-top:8px;" class="grid-2">
            <div class="chart-box">
              <canvas id="tytTrendChart"></canvas>
            </div>
            <div class="chart-box">
              <canvas id="aytTrendChart"></canvas>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- TAB: REPORTS -->
    <section id="tab-reports" class="tab-panel">
      <div class="grid-2">
        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-comment-dots"></i>
            Öğrenci Raporu Oluştur
          </div>
          <div style="margin-top:6px;">
            <label class="muted">Başlık</label>
            <input type="text" id="reportTitle" class="text-input" placeholder="Örn: 3. Hafta Değerlendirmesi">
          </div>
          <div style="margin-top:8px;">
            <label class="muted">Rapor Metni</label>
            <textarea id="reportContent" class="textarea-input"
                      placeholder="Çalışma düzeni, ilerleme, deneme performansı, eksikler ve öneriler..."></textarea>
          </div>
          <div style="margin-top:8px; display:flex; justify-content:space-between; align-items:center;">
            <button class="btn btn-primary" id="saveReportBtn">
              <i class="fa-solid fa-paper-plane"></i>
              Raporu Kaydet
            </button>
            <span class="muted" id="reportSaveStatus"></span>
          </div>
          <div style="margin-top:6px;">
            <span class="badge">
              <i class="fa-solid fa-link"></i>
              Raporlar admin panelindeki <strong>reports.php</strong> ile entegre edilebilir.
            </span>
          </div>
        </div>

        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-folder-open"></i>
            Önceki Raporlar
          </div>
          <div style="max-height:240px; overflow:auto; margin-top:6px;">
            <table>
              <thead>
                <tr>
                  <th>Tarih</th>
                  <th>Başlık</th>
                </tr>
              </thead>
              <tbody id="reportsTableBody"></tbody>
            </table>
          </div>
        </div>
      </div>
    </section>

    <!-- TAB: SCHEDULE -->
    <section id="tab-schedule" class="tab-panel">
      <div class="grid-2">
        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-calendar-plus"></i>
            Haftalık Ders Programı
          </div>
			<!-- ============================
     SAAT YÖNETİMİ PANELİ
============================= -->
<div class="time-editor">
    <h3>Ders Saati Yönetimi</h3>

    <div class="time-list" id="timeList"></div>

    <div class="time-actions">
        <input type="text" id="newTimeInput" placeholder="09:20-10:05">
        <button id="addTimeBtn" class="btn-orange">Saat Ekle</button>
    </div>

    <small style="color:#bbb">
        * Saat listesi öğrenciye özeldir. Seçilen öğrenci değişince saatler değişir.
    </small>

    <hr style="border-color:#444; margin:15px 0;">
</div>

          <div class="info">
            Konu atandığında <span class="legend-color legend-color-topic"></span> <span class="muted">turuncu</span>,
            soru çözümü atandığında <span class="legend-color legend-color-questions"></span> <span class="muted">mavi</span> blok görünür.
          </div>
          <div class="legend">
            <div class="legend-item">
              <div class="legend-color legend-color-topic"></div> Konu Çalışması
            </div>
            <div class="legend-item">
              <div class="legend-color legend-color-questions"></div> Soru Çözümü
            </div>
          </div>

          <div style="margin-top:8px; overflow:auto;">
            <table class="schedule-grid" id="scheduleGrid">
              <!-- JS ile doldurulacak: günler x saat dilimleri -->
            </table>
          </div>

          <div class="subtext" style="margin-top:6px;">
            Ders programı student bazlı kaydedilir. Bir konu birden fazla slot’a atanabilir.
          </div>
        </div>

        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-sparkles"></i>
            Slot Detayı
          </div>
          <div class="info">
            Program alanına tıkladığında, ilgili slotu buradan düzenleyebilirsin.
          </div>

          <div style="margin-top:8px;">
            <label class="muted">Gün & Saat</label>
            <div id="selectedSlotLabel" class="subtext">Henüz bir slot seçilmedi.</div>
          </div>

          <div style="margin-top:8px;">
            <label class="muted">Etkinlik Türü</label>
            <select id="slotType" class="select-input">
              <option value="">Seç...</option>
              <option value="konu">Konu Çalışması</option>
              <option value="soru">Soru Çözümü</option>
              <option value="deneme">Deneme</option>
              <option value="paragraf">Paragraf</option>
              <option value="problem">Problem</option>
              <option value="okuma">Okuma</option>
              <option value="mola">Mola</option>
              <option value="görüşme">Görüşme</option>
              <option value="tekrar">Tekrar</option>
              <option value="uyku">Uyku</option>
            </select>
          </div>

          <div style="margin-top:8px;">
            <label class="muted">Konu / Not</label>
            <input type="text" id="slotNote" class="text-input" placeholder="Örn: Temel Kavramlar test 1-2">
          </div>

          <div style="margin-top:8px;">
            <button class="btn btn-primary" id="saveSlotBtn">
              <i class="fa-solid fa-check"></i> Slotu Kaydet
            </button>
            <button class="btn btn-outline" id="clearSlotBtn" style="margin-left:6px;">
              <i class="fa-solid fa-eraser"></i> Slotu Temizle
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- TAB: MEETINGS -->
    <section id="tab-meetings" class="tab-panel">
      <div class="grid-2">
        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-video"></i>
            Haftalık Görüşmeler (Jitsi)
          </div>
          <div class="info">
            Bu liste, admin panelinden planlanan görüşmeleri gösterir
            (<span class="muted">meetings.php</span>).
          </div>

          <div style="margin-top:8px; max-height:260px; overflow:auto;">
            <table>
              <thead>
                <tr>
                  <th>Öğrenci</th>
                  <th>Gün</th>
                  <th>Saat</th>
                  <th>Link</th>
                </tr>
              </thead>
              <tbody id="meetingsTableBody"></tbody>
            </table>
          </div>
        </div>

        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-arrow-up-right-from-square"></i>
            Görüşmeye Katıl
          </div>
          <div style="margin-top:8px;">
            <div class="muted">
              Görüşmeler varsayılan olarak <span class="info-strong">yeni sekmede</span> açılır.
              Böylece koç paneli açık kalır; öğrenci verilerini aynı anda görebilirsin.
            </div>
          </div>
          <div style="margin-top:10px;">
            <label class="muted">Seçili Görüşme</label>
            <div id="selectedMeetingLabel" class="subtext">Tablodan bir görüşme seçin.</div>
          </div>
          <div style="margin-top:12px;">
            <button class="btn btn-primary" id="joinMeetingBtn" disabled>
              <i class="fa-solid fa-video"></i>
              Görüşmeye Katıl
            </button>
          </div>
          <div style="margin-top:10px;">
            <span class="badge">
              <i class="fa-solid fa-circle-info"></i>
              Linkler <strong>https://meet.jit.si/ROOM</strong> formatında tutulabilir.
            </span>
          </div>
        </div>
      </div>
    </section>

    <!-- TAB: GUIDANCE / REHBERLİK -->
    <section id="tab-guidance" class="tab-panel">
      <div class="grid-2">
        <!-- LEFT: MOOD TRACKING -->
        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-heart-pulse"></i>
            Duygu / Durum Takibi
          </div>

          <div style="display:flex; gap:8px; margin-top:6px;">
            <div style="flex:1;">
              <label class="muted">Tarih</label>
              <input type="date" id="moodDate" class="date-input">
            </div>
            <div style="flex:1;">
              <label class="muted">Duygu</label>
              <select id="moodSelect" class="select-input">
                <option value="">Seç...</option>
                <option value="Rahat">Rahat</option>
                <option value="Huzursuz">Huzursuz</option>
                <option value="Kaygılı">Kaygılı</option>
                <option value="Motivasyonlu">Motivasyonlu</option>
                <option value="Yorgun">Yorgun</option>
                <option value="Karışık">Karışık</option>
              </select>
            </div>
          </div>

          <div style="margin-top:8px;">
            <label class="muted">Kısa Not</label>
            <textarea id="moodNote" class="textarea-input"
                      placeholder="Bugün seni en çok ne zorladı, ne iyi geldi?"></textarea>
          </div>

          <div style="margin-top:8px;">
            <label class="muted">Haftayı Puanla (0 - 10)</label>
            <input type="number" id="weekScore" class="number-input" min="0" max="10" step="1" placeholder="Örn: 7">
          </div>

          <div style="margin-top:8px; display:flex; justify-content:space-between; align-items:center;">
            <button class="btn btn-primary" id="saveMoodBtn">
              <i class="fa-solid fa-face-smile"></i>
              Duyguyu Kaydet
            </button>
            <span class="muted" id="moodSaveStatus"></span>
          </div>

          <div style="margin-top:8px;">
            <span class="badge">
              <i class="fa-solid fa-wand-magic-sparkles"></i>
              Seçilen duyguya göre mini öneriler otomatik üretilir.
            </span>
          </div>

          <div style="margin-top:8px;">
            <label class="muted">Mini Öneri</label>
            <div id="moodSuggestion" class="subtext">Henüz bir duygu seçilmedi.</div>
          </div>
        </div>

        <!-- RIGHT: MOOD TREND -->
        <div class="card">
          <div class="card-title">
            <i class="fa-solid fa-wave-square"></i>
            Duygu Trendi & Haftalık Değerlendirme
          </div>
          <div class="chart-box" style="height:220px;">
            <canvas id="moodTrendChart"></canvas>
          </div>
          <div style="margin-top:8px;">
            <span class="pill-small">
              <span class="status-dot"></span>
              Akademik motivasyon
            </span>
            <span class="pill-small" style="margin-left:6px;">
              <span class="status-dot red"></span>
              Kaygı yoğunluğu (testler entegre edilebilir)
            </span>
          </div>
        </div>
      </div>

      <div style="margin-top:12px;" class="card">
        <div class="card-title">
          <i class="fa-solid fa-vial-circle-check"></i>
          Kaygı Testi & Öğrenme Stili Testi (İskelet)
        </div>
        <div class="info">
          Bu alana, daha sonra ekleyeceğimiz <span class="info-strong">Kaygı Testi</span> ve
          <span class="info-strong">Öğrenme Stili Testi</span> entegre edilebilir.
          Testler tamamlandığında sonuçlar otomatik okunup “Rehberlik Raporu” olarak raporlara eklenebilir.
        </div>
      </div>
    </section>
  </div>
</div>

<script>
/* =========================================================
   GLOBAL STATE
   Her öğrenci için veriler localStorage üzerinden tutulur.
   Ana anahtar: BOOST_COACH_DATA_<studentId>
   ========================================================= */

// Grafik referansları
let weeklyStudyChart = null;
let tytTrendChart = null;
let aytTrendChart = null;
let moodTrendChart = null;

// TYT & AYT ders listeleri
const TYT_SUBJECTS = [
  "Türkçe",
  "Coğrafya",
  "Tarih",
  "Felsefe",
  "Din Kültürü",
  "Matematik",
  "Fizik",
  "Kimya",
  "Biyoloji"
];

const AYT_STRUCTURE = [
  { section: "Türk Dili ve Edebiyatı - Sosyal 1", subject: "Edebiyat", key: "EDEBIYAT" },
  { section: "Türk Dili ve Edebiyatı - Sosyal 1", subject: "Coğrafya-1", key: "COG1" },
  { section: "Türk Dili ve Edebiyatı - Sosyal 1", subject: "Tarih-1", key: "TAR1" },

  { section: "Sosyal Bilimler-2", subject: "Coğrafya-2", key: "COG2" },
  { section: "Sosyal Bilimler-2", subject: "Tarih-2", key: "TAR2" },
  { section: "Sosyal Bilimler-2", subject: "Felsefe", key: "FELS" },
  { section: "Sosyal Bilimler-2", subject: "Din Kültürü", key: "DINK" },

  { section: "Matematik", subject: "Matematik", key: "MAT" },

  { section: "Fen Bilimleri", subject: "Fizik", key: "FIZ" },
  { section: "Fen Bilimleri", subject: "Kimya", key: "KIM" },
  { section: "Fen Bilimleri", subject: "Biyoloji", key: "BIYO" }
];

function buildScheduleGrid() {
	console.log("buildScheduleGrid çalıştı", currentStudentId);
    const table = document.getElementById("scheduleGrid");
    if (!table) return;

    table.innerHTML = "";

    // Öğrenci seçili değilse tabloyu çizme
    if (!currentStudentId) return;

    // Bu öğrenciye ait saat aralıkları
    const HOURS = getStudentTimes(currentStudentId) || [];

    // Saat listesi boşsa uyarı göster
    if (HOURS.length === 0) {
        table.innerHTML = `
            <tr>
                <td colspan="8" class="muted">Saat listesi boş. Öğrenci için saat ekleyin.</td>
            </tr>`;
        return;
    }

    // Günler
    const thead = document.createElement("thead");
    const headRow = document.createElement("tr");
    headRow.innerHTML =
        `<th>Saat / Gün</th>` +
        WEEKDAYS.map(d => `<th>${d}</th>`).join("");
    thead.appendChild(headRow);
    table.appendChild(thead);

    // Saat x gün tablo gövdesi
    const tbody = document.createElement("tbody");

    HOURS.forEach(hour => {
        const tr = document.createElement("tr");

        tr.innerHTML =
            `<td>${hour}</td>` +
            WEEKDAYS.map(day => {
                const key = `${day}-${hour}`;
                return `<td><div class="schedule-slot" data-slot="${key}"></div></td>`;
            }).join("");

        tbody.appendChild(tr);
    });

    table.appendChild(tbody);
}

/* ===== SCHEDULE TIME CORE ===== */
const DEFAULT_TIMES = [
  "08:00-09:00",
  "09:00-10:00",
  "10:00-11:00",
  "11:00-12:00",
  "13:00-14:00",
  "14:00-15:00",
  "15:00-16:00"
];

function getStudentTimes(studentId) {
  if (!studentId) return [];
  const raw = localStorage.getItem("STUDENT_TIMES_" + studentId);
  if (!raw) return [...DEFAULT_TIMES];
  try {
    return JSON.parse(raw);
  } catch {
    return [...DEFAULT_TIMES];
  }
}

function saveStudentTimes(studentId, times) {
  localStorage.setItem(
    "STUDENT_TIMES_" + studentId,
    JSON.stringify(times)
  );
}

function renderTimeList(studentId) {
  const box = document.getElementById("timeList");
  if (!box) return;

  box.innerHTML = "";
  const times = getStudentTimes(studentId);

  times.forEach(t => {
    const el = document.createElement("div");
    el.className = "time-tag";
    el.textContent = t;
    el.onclick = () => {
      const filtered = times.filter(x => x !== t);
      saveStudentTimes(studentId, filtered);
      renderTimeList(studentId);
      buildScheduleGrid();
    };
    box.appendChild(el);
  });
}


const WEEKDAYS = [
  "Pazartesi",
  "Salı",
  "Çarşamba",
  "Perşembe",
  "Cuma",
  "Cumartesi",
  "Pazar"
];

/* =========================================================
   UTILS
   ========================================================= */
	function getStudentTimes(studentId) {
  if (!studentId) return [];
  const key = "BOOST_COACH_TIMES_" + studentId;
  const raw = localStorage.getItem(key);
  if (!raw) return [];
  try {
    return JSON.parse(raw);
  } catch {
    return [];
  }
}

function saveStudentTimes(studentId, times) {
  const key = "BOOST_COACH_TIMES_" + studentId;
  localStorage.setItem(key, JSON.stringify(times));
}
function renderTimeList(studentId) {
  const listDiv = document.getElementById("timeList");
  listDiv.innerHTML = "";

  if (!studentId) return;

  const times = getStudentTimes(studentId);

  if (times.length === 0) {
    listDiv.innerHTML = `<span class="muted">Henüz saat eklenmedi.</span>`;
    return;
  }

  times.forEach((time, index) => {
    const tag = document.createElement("div");
    tag.className = "time-tag";
    tag.textContent = time;

    tag.addEventListener("click", () => {
      if (!confirm(time + " saatini silmek istiyor musun?")) return;
      times.splice(index, 1);
      saveStudentTimes(studentId, times);
      renderTimeList(studentId);
      buildScheduleGrid();
    });

    listDiv.appendChild(tag);
  });
}
document.getElementById("addTimeBtn").addEventListener("click", () => {
  if (!currentStudentId) {
    alert("Önce öğrenci seçmelisiniz.");
    return;
  }

  const input = document.getElementById("newTimeInput");
  const value = input.value.trim();

  if (!value) {
    alert("Saat giriniz. Örn: 09:20-10:05");
    return;
  }

  const times = getStudentTimes(currentStudentId);

  if (times.includes(value)) {
    alert("Bu saat zaten ekli.");
    return;
  }

  times.push(value);
  times.sort(); // kronolojik dursun
  saveStudentTimes(currentStudentId, times);

  input.value = "";
  renderTimeList(currentStudentId);
  buildScheduleGrid();
});


function getStorageKeyForStudent(studentId) {
  return "BOOST_COACH_DATA_" + studentId;
}

function getStudentData(studentId) {
  const key = getStorageKeyForStudent(studentId);
  const raw = localStorage.getItem(key);
  if (!raw) {
    return {
      programStartDate: null,
      meetingWeekday: null,
      meetingTime: null,
      studyEntries: [],         // {date, subject, topic, questions, totalMinutes}
      dailyStudyMinutes: {},    // { 'YYYY-MM-DD': minutes }
      tytExams: [],             // {date, subjects:{}, totalNet}
      aytExams: [],             // {date, subjects:{}, totalNet, say, soz, ea}
      reports: [],              // {date, title, content}
      schedule: {},             // { 'Gun-Saat': { type, note } }
      moodEntries: [],          // {date, mood, note, weekScore}
      meetings: []              // (backendten doldurulabilir)
    };
  }
  try {
    return JSON.parse(raw);
  } catch(e) {
    console.error("Bad JSON in student data", e);
    return {
      programStartDate: null,
      meetingWeekday: null,
      meetingTime: null,
      studyEntries: [],
      dailyStudyMinutes: {},
      tytExams: [],
      aytExams: [],
      reports: [],
      schedule: {},
      moodEntries: [],
      meetings: []
    };
  }
}

function saveStudentData(studentId, data) {
  const key = getStorageKeyForStudent(studentId);
  localStorage.setItem(key, JSON.stringify(data));
}

function dateToWeekIndex(dateStr, programStartDateStr) {
  if (!dateStr || !programStartDateStr) return null;
  const d = new Date(dateStr + "T00:00:00");
  const start = new Date(programStartDateStr + "T00:00:00");
  const diffMs = d - start;
  const diffDays = diffMs / (1000 * 60 * 60 * 24);
  const weekIndex = Math.floor(diffDays / 7) + 1;
  if (weekIndex < 1) return 1;
  return weekIndex;
}

function minutesToLabel(minutes) {
  if (!minutes || minutes <= 0) return "0s 0dk";
  const h = Math.floor(minutes / 60);
  const m = minutes % 60;
  return h + "s " + m + "dk";
}

function calcNet(correct, wrong) {
  const c = Number(correct) || 0;
  const w = Number(wrong) || 0;
  return c - w * 0.25;
}

/* =========================================================
   TAB NAVIGATION
   ========================================================= */
document.querySelectorAll(".tab-button").forEach(btn => {
  btn.addEventListener("click", () => {
    document.querySelectorAll(".tab-button").forEach(b => b.classList.remove("active"));
    document.querySelectorAll(".tab-panel").forEach(p => p.classList.remove("active"));
    btn.classList.add("active");
    const target = btn.getAttribute("data-tab");
    document.getElementById(target).classList.add("active");
  });
});

/* =========================================================
   INITIAL UI SETUP
   ========================================================= */

// TYT ve AYT form tablolarını doldur
function buildTytFormTable() {
  const tbody = document.getElementById("tytTableBodyForm");
  tbody.innerHTML = "";
  TYT_SUBJECTS.forEach(sub => {
    const tr = document.createElement("tr");
    tr.innerHTML = `
      <td>${sub}</td>
      <td><input type="number" min="0" step="1" data-tyt-correct="${sub}" class="number-input"></td>
      <td><input type="number" min="0" step="1" data-tyt-wrong="${sub}" class="number-input"></td>
      <td><span data-tyt-net="${sub}">0.00</span></td>
    `;
    tbody.appendChild(tr);
  });
}

function buildAytFormTable() {
  const tbody = document.getElementById("aytTableBodyForm");
  tbody.innerHTML = "";
  AYT_STRUCTURE.forEach(row => {
    const tr = document.createElement("tr");
    tr.innerHTML = `
      <td>
        <div>${row.section}</div>
        <div class="muted">${row.subject}</div>
      </td>
      <td><input type="number" min="0" step="1" data-ayt-correct="${row.key}" class="number-input"></td>
      <td><input type="number" min="0" step="1" data-ayt-wrong="${row.key}" class="number-input"></td>
      <td><span data-ayt-net="${row.key}">0.00</span></td>
    `;
    tbody.appendChild(tr);
  });
}

// Ders programı gridini oluştur


/* =========================================================
   STUDENT SELECTION (backend: members.php)
   ========================================================= */

async function loadStudentsFromBackend() {
  const select = document.getElementById("studentSelect");
  select.innerHTML = `<option value="">Öğrenci seçiniz...</option>`;

  try {
    // Burayı kendi admin_api yapına göre düzenle:
    // Öneri: members.php, session'daki koça göre sadece kendi öğrencilerini döndürsün.
    const response = await fetch("/coach/api/students.php");
    if (!response.ok) throw new Error("HTTP " + response.status);
    const data = await response.json();

    // Beklenen format:
    // data = [{ id: 5, name: "Mehmet", ... }, ...]
    (data || []).forEach(st => {
      const opt = document.createElement("option");
      opt.value = st.id;
      opt.textContent = st.name || (st.first_name + " " + st.last_name) || "Öğrenci #" + st.id;
      select.appendChild(opt);
    });

  } catch(e) {
    console.warn("Öğrenciler yüklenemedi, örnek veri kullanılabilir.", e);
    // Backend hazır olmayabilir; örnek 2 öğrenci:
    const example = [
      { id: "1", name: "Mehmet Örnek" },
      { id: "2", name: "Veli Örnek" }
    ];
    example.forEach(st => {
      const opt = document.createElement("option");
      opt.value = st.id;
      opt.textContent = st.name;
      select.appendChild(opt);
    });
  }
}

/* =========================================================
   UI REFRESH (Student-based)
   ========================================================= */

function refreshAllForStudent() {
  if (!currentStudentId) {
    document.getElementById("studentInfoText").textContent =
      "Önce öğrenciyi seçin, tüm tablolar ve grafikler öğrenciye göre güncellenecek.";
    return;
  }

  const data = getStudentData(currentStudentId);

  // Program ayarları
  document.getElementById("programStartDate").value = data.programStartDate || "";
  document.getElementById("meetingWeekday").value = data.meetingWeekday || "";
  document.getElementById("meetingTime").value = data.meetingTime || "";

  if (data.programStartDate) {
    document.getElementById("programSettingsLabel").textContent =
      `Program başlangıcı: ${data.programStartDate}${
        data.meetingWeekday ? " | Haftalık görüşme: " + data.meetingWeekday + " " + (data.meetingTime || "") : ""
      }`;
  } else {
    document.getElementById("programSettingsLabel").textContent = "";
  }

  document.getElementById("studentInfoText").textContent =
    `Seçili öğrenci: ${currentStudentName}. Tüm veriler bu öğrenciye kaydedilir ve gösterilir.`;

  refreshStudyTableAndCharts(data);
  refreshExamListsAndCharts(data);
  refreshReportsTable(data);
  refreshScheduleView(data);
  refreshMeetingsTable(data);
  refreshMoodView(data);
}

/* =========================================================
   STUDY DATA: TABLE & WEEKLY STUDY CHART
   ========================================================= */

function refreshStudyTableAndCharts(data) {
  const tbody = document.getElementById("studyTableBody");
  tbody.innerHTML = "";

  const entries = data.studyEntries || [];
  const programStartDate = data.programStartDate;

  // Son girişler (tarihe göre sıralı)
  const sorted = [...entries].sort((a, b) => (a.date > b.date ? -1 : 1));
  sorted.forEach(entry => {
    const weekIndex = dateToWeekIndex(entry.date, programStartDate);
    const tr = document.createElement("tr");
    tr.innerHTML = `
      <td>${entry.date || "-"}</td>
      <td>${entry.subject || "-"}</td>
      <td>${entry.topic || "-"}</td>
      <td>${entry.questions || 0}</td>
      <td>${minutesToLabel(entry.totalMinutes || 0)}</td>
      <td>${weekIndex ? "Hafta " + weekIndex : "-"}</td>
    `;
    tbody.appendChild(tr);
  });

  // Haftalık ortalama günlük çalışma süresi (dakika bazlı)
  const weeklyMinutesMap = {}; // {weekIndex: totalMinutesWeek}
  if (data.programStartDate) {
    for (const [dateStr, mins] of Object.entries(data.dailyStudyMinutes || {})) {
      const w = dateToWeekIndex(dateStr, data.programStartDate);
      if (!w) continue;
      weeklyMinutesMap[w] = (weeklyMinutesMap[w] || 0) + mins;
    }
  }

  const weeks = Object.keys(weeklyMinutesMap)
    .map(k => Number(k))
    .sort((a, b) => a - b);

  const avgMinutesPerWeek = weeks.map(weekIndex => {
    // "Hafta hafta günlük ortalama çalışma süresi":
    // Her hafta için toplam dakika / 7
    const totalMinutes = weeklyMinutesMap[weekIndex];
    return totalMinutes / 7;
  });

  // Haftalık ortalama bilgisini üstte göster
  if (weeks.length > 0) {
    const lastWeekIndex = weeks[weeks.length - 1];
    const lastAvg = avgMinutesPerWeek[avgMinutesPerWeek.length - 1];
    document.getElementById("weeklyAvgStudyLabel").textContent =
      minutesToLabel(Math.round(lastAvg));
  } else {
    document.getElementById("weeklyAvgStudyLabel").textContent = "0s 0dk";
  }

  // Grafik
  const ctx = document.getElementById("weeklyStudyChart").getContext("2d");
  if (weeklyStudyChart) weeklyStudyChart.destroy();
  weeklyStudyChart = new Chart(ctx, {
    type: "line",
    data: {
      labels: weeks.map(w => "Hafta " + w),
      datasets: [{
        label: "Haftalık Ortalama Günlük Çalışma Süresi (dk)",
        data: avgMinutesPerWeek.map(x => Math.round(x)),
        tension: 0.3,
        fill: false,
        borderWidth: 2,
        pointRadius: 3
      }]
    },
    options: {
      plugins: { legend: { display: false } },
      scales: {
        x: { ticks: { color: "#cccccc" }, grid: { color: "#222" } },
        y: {
          ticks: {
            color: "#cccccc",
            callback: val => val + " dk"
          },
          grid: { color: "#222" }
        }
      }
    }
  });

  // Haftalık hedef tamamlama yüzdesi (şimdilik dummy: son haftanın ortalamasına göre)
  if (avgMinutesPerWeek.length > 0) {
    const last = avgMinutesPerWeek[avgMinutesPerWeek.length - 1];
    // Örnek: 4 saat/gün (240 dk) hedef = %100
    const percent = Math.min(100, Math.round((last / 240) * 100));
    document.getElementById("weeklyCompletionLabel").textContent = "%" + percent;
  } else {
    document.getElementById("weeklyCompletionLabel").textContent = "%0";
  }
}

/* =========================================================
   EXAMS: LISTS & CHARTS
   ========================================================= */

function refreshExamListsAndCharts(data) {
  // TYT
  const tytListBody = document.getElementById("tytExamListBody");
  tytListBody.innerHTML = "";
  const tytExams = (data.tytExams || []).sort((a, b) => (a.date > b.date ? 1 : -1));
  tytExams.forEach(ex => {
    const tr = document.createElement("tr");
    tr.innerHTML = `<td>${ex.date}</td><td>${ex.totalNet.toFixed(2)}</td>`;
    tytListBody.appendChild(tr);
  });

  // TYT Trend Chart
  const tytCtx = document.getElementById("tytTrendChart").getContext("2d");
  if (tytTrendChart) tytTrendChart.destroy();
  tytTrendChart = new Chart(tytCtx, {
    type: "line",
    data: {
      labels: tytExams.map(e => e.date),
      datasets: [{
        label: "TYT Toplam Net",
        data: tytExams.map(e => e.totalNet),
        tension: 0.3,
        fill: false,
        borderWidth: 2,
        pointRadius: 3
      }]
    },
    options: {
      plugins: { legend: { display: false } },
      scales: {
        x: { ticks: { color: "#cccccc" }, grid: { color: "#222" } },
        y: {
          ticks: { color: "#cccccc" },
          grid: { color: "#222" }
        }
      }
    }
  });

  // AYT
  const aytExams = (data.aytExams || []).sort((a, b) => (a.date > b.date ? 1 : -1));

  const aytCtx = document.getElementById("aytTrendChart").getContext("2d");
  if (aytTrendChart) aytTrendChart.destroy();
  aytTrendChart = new Chart(aytCtx, {
    type: "line",
    data: {
      labels: aytExams.map(e => e.date),
      datasets: [{
        label: "AYT Toplam Net",
        data: aytExams.map(e => e.totalNet),
        tension: 0.3,
        fill: false,
        borderWidth: 2,
        pointRadius: 3
      }]
    },
    options: {
      plugins: { legend: { display: false } },
      scales: {
        x: { ticks: { color: "#cccccc" }, grid: { color: "#222" } },
        y: {
          ticks: { color: "#cccccc" },
          grid: { color: "#222" }
        }
      }
    }
  });
}

/* =========================================================
   REPORTS
   ========================================================= */

function refreshReportsTable(data) {
  const tbody = document.getElementById("reportsTableBody");
  tbody.innerHTML = "";
  const reports = (data.reports || []).sort((a, b) => (a.date > b.date ? -1 : 1));
  reports.forEach(r => {
    const tr = document.createElement("tr");
    tr.innerHTML = `<td>${r.date}</td><td>${r.title}</td>`;
    tbody.appendChild(tr);
  });
}

/* =========================================================
   SCHEDULE VIEW
   ========================================================= */

function refreshScheduleView(data) {
  const schedule = data.schedule || {};
  document.querySelectorAll("[data-slot]").forEach(div => {
    const key = div.getAttribute("data-slot");
    const entry = schedule[key];
    if (!entry) {
      div.textContent = "";
      div.className = "schedule-slot";
    } else {
      div.textContent = entry.note || "";
      div.className = "schedule-slot " +
        (entry.type === "konu" ? "slot-topic" :
         entry.type === "soru" ? "slot-questions" :
         "slot-topic");
    }
  });
}

/* =========================================================
   MEETINGS (backend: meetings.php)
   ========================================================= */

async function loadMeetingsFromBackend() {
    if (!currentStudentId) return;

    try {
        const resp = await fetch("/coach/api/meetings.php?coach_id=" + COACH_ID);
        const meetings = await resp.json();

        const data = getStudentData(currentStudentId);
        data.meetings = meetings || [];
        saveStudentData(currentStudentId, data);

        refreshMeetingsTable(data);

    } catch (e) {
        console.error("Meetings API okunamadı:", e);

        const data = getStudentData(currentStudentId);
        refreshMeetingsTable(data);
    }
}


function refreshMeetingsTable(data) {
    const tbody = document.getElementById("meetingsTableBody");
    tbody.innerHTML = "";

    const meetings = data.meetings || [];

    if (meetings.length === 0) {
        tbody.innerHTML = `<tr><td colspan="4" class="muted">Bu öğrenciye ait görüşme bulunmuyor.</td></tr>`;
        document.getElementById("selectedMeetingLabel").textContent =
            "Bu öğrenci için görüşme bulunmuyor.";
        document.getElementById("joinMeetingBtn").disabled = true;
        return;
    }

    meetings.forEach(m => {
        const tr = document.createElement("tr");
        tr.innerHTML = `
            <td>${m.student_name}</td>
            <td>${m.weekday}</td>
            <td>${m.time}</td>
            <td><span class="badge"><i class="fa-solid fa-link"></i> Aç</span></td>
        `;
        tr.dataset.link = m.link;

        tr.addEventListener("click", () => {
            tbody.querySelectorAll("tr").forEach(x => x.style.background = "");
            tr.style.background = "rgba(255,255,255,0.08)";

            document.getElementById("selectedMeetingLabel").textContent =
                `${m.student_name} – ${m.weekday} ${m.time}`;

            const btn = document.getElementById("joinMeetingBtn");
            btn.disabled = false;
            btn.onclick = () => window.open(m.link, "_blank");
        });

        tbody.appendChild(tr);
    });
}


/* =========================================================
   MOOD / GUIDANCE
   ========================================================= */

function refreshMoodView(data) {
  const entries = (data.moodEntries || []).sort((a, b) => (a.date > b.date ? 1 : -1));

  // Son kaydın mini önerisi:
  if (entries.length > 0) {
    const last = entries[entries.length - 1];
    document.getElementById("moodSuggestion").textContent = makeMoodSuggestion(last.mood, last.weekScore);
  } else {
    document.getElementById("moodSuggestion").textContent = "Henüz bir duygu kaydı yok.";
  }

  // Mood trend grafiği (hafta puanı)
  const ctx = document.getElementById("moodTrendChart").getContext("2d");
  if (moodTrendChart) moodTrendChart.destroy();
  moodTrendChart = new Chart(ctx, {
    type: "line",
    data: {
      labels: entries.map(e => e.date),
      datasets: [{
        label: "Haftayı Puanla (0-10)",
        data: entries.map(e => e.weekScore || 0),
        tension: 0.3,
        fill: false,
        borderWidth: 2,
        pointRadius: 3
      }]
    },
    options: {
      plugins: { legend: { display: false } },
      scales: {
        x: { ticks: { color: "#cccccc" }, grid: { color: "#222" } },
        y: {
          min: 0,
          max: 10,
          ticks: { color: "#cccccc" },
          grid: { color: "#222" }
        }
      }
    }
  });
}

function makeMoodSuggestion(mood, score) {
  if (!mood) return "Duygu seçildiğinde burada küçük bir öneri göreceksin.";
  score = Number(score);
  if (mood === "Kaygılı") {
    if (score <= 4) {
      return "Kaygı düzeyi yüksek görünüyor. Nefes egzersizleri, küçük ve ulaşılabilir günlük hedefler ve daha sık mini görüşmeler planlamak faydalı olabilir.";
    } else {
      return "Kaygın var ama yönetilebilir görünüyor. Çözdüğün denemelerdeki gelişim noktasına odaklan, hata listesi tut ve 'neden yapamadım' değil 'nasıl geliştirebilirim' sorusunu sormaya çalış.";
    }
  }
  if (mood === "Huzursuz" || mood === "Karışık") {
    return "Duygular biraz karışık. Bugünlük hedeflerini sadeleştir; 1-2 küçük işi bitir, sonrasında dinlenmeye alan aç. Eksikleri düşünmek yerine, bugün attığın adımları not et.";
  }
  if (mood === "Yorgun") {
    return "Yorgun hissediyorsun, bu çok doğal. Uyku düzenini ve beslenmeni gözden geçirmek, çalışma bloklarını 25-30 dakikalık parçalara bölmek seni rahatlatabilir.";
  }
  if (mood === "Motivasyonlu") {
    return "Motivasyonlu olduğun bu dönem, yeni alışkanlık inşa etmek için çok değerli. Özellikle zorlandığın derslerde kısa, odaklı çalışma blokları ekleyerek bu ivmeyi pekiştirebilirsin.";
  }
  if (mood === "Rahat") {
    return "Rahat bir moddasın; bunu hafife alma. Rahatlık, verimli bir çalışma rutini kurmak için iyi bir zemindir. Günün başında 2-3 net hedef belirleyip bittikçe yanına ✔ işareti koy.";
  }
  return "Duygunu görmek değerli. Onu değiştirmeye çalışmaktan önce, nedenini sakin sakin anlamaya çalışmak en sağlıklı adım olur.";
}

/* =========================================================
   EVENT HANDLERS
   ========================================================= */
	document.getElementById("addTimeBtn").addEventListener("click", () => {
  if (!currentStudentId) {
    alert("Önce öğrenci seç");
    return;
  }

  const input = document.getElementById("newTimeInput");
  const val = input.value.trim();
  if (!val) return;

  const times = getStudentTimes(currentStudentId);
  if (!times.includes(val)) {
    times.push(val);
    times.sort();
    saveStudentTimes(currentStudentId, times);
    renderTimeList(currentStudentId);
    buildScheduleGrid();
  }

  input.value = "";
});

// Öğrenci seçimi
document.getElementById("studentSelect").addEventListener("change", e => {
  const val = e.target.value;
  if (!val) {
    currentStudentId = null;
    currentStudentName = null;
    refreshAllForStudent();
    return;
  }
  currentStudentId = String(val);
  currentStudentName = e.target.options[e.target.selectedIndex].textContent;
  refreshAllForStudent();
	renderTimeList(currentStudentId);
buildScheduleGrid();
  // Öğrencinin meetings'lerini backendten de çek
  loadMeetingsFromBackend();
});

// Program ayarlarını kaydet
document.getElementById("saveProgramSettingsBtn").addEventListener("click", () => {
  if (!currentStudentId) {
    alert("Önce öğrenci seçmelisiniz.");
    return;
  }
  const data = getStudentData(currentStudentId);
  data.programStartDate = document.getElementById("programStartDate").value || null;
  data.meetingWeekday = document.getElementById("meetingWeekday").value || null;
  data.meetingTime = document.getElementById("meetingTime").value || null;
  saveStudentData(currentStudentId, data);
  refreshAllForStudent();
});

// Günlük çalışma kaydı
document.getElementById("addStudyEntryBtn").addEventListener("click", () => {
  if (!currentStudentId) {
    alert("Önce öğrenci seçmelisiniz.");
    return;
  }

  const date = document.getElementById("studyDate").value;
  const subject = document.getElementById("studySubject").value;
  const topic = document.getElementById("studyTopic").value.trim();
  const questions = Number(document.getElementById("studyQuestions").value) || 0;
  const hours = Number(document.getElementById("studyHours").value) || 0;
  const minutes = Number(document.getElementById("studyMinutes").value) || 0;
  const totalMinutes = hours * 60 + minutes;

  if (!date) { alert("Tarih seçmelisiniz."); return; }
  if (!subject) { alert("Ders seçmelisiniz."); return; }

  const data = getStudentData(currentStudentId);
  data.studyEntries.push({ date, subject, topic, questions, totalMinutes });

  // Günlük toplam çalışma süresi, MATEMATİKTEN BAĞIMSIZ; son girilen değeri gün için yazarız.
  if (!data.dailyStudyMinutes) data.dailyStudyMinutes = {};
  data.dailyStudyMinutes[date] = totalMinutes;

  saveStudentData(currentStudentId, data);
  document.getElementById("studySaveStatus").textContent = "Kaydedildi.";
  setTimeout(() => {
    document.getElementById("studySaveStatus").textContent = "";
  }, 1500);

  refreshStudyTableAndCharts(data);
});

// TYT net hesaplamaları (anlık)
document.getElementById("tytTableBodyForm").addEventListener("input", () => {
  let totalNet = 0;
  TYT_SUBJECTS.forEach(sub => {
    const cInput = document.querySelector(`[data-tyt-correct="${sub}"]`);
    const wInput = document.querySelector(`[data-tyt-wrong="${sub}"]`);
    const netSpan = document.querySelector(`[data-tyt-net="${sub}"]`);
    const net = calcNet(cInput.value, wInput.value);
    netSpan.textContent = net.toFixed(2);
    totalNet += net;
  });
  document.getElementById("tytTotalNetLabel").textContent = totalNet.toFixed(2);
});

// TYT kaydet
document.getElementById("saveTytExamBtn").addEventListener("click", () => {
  if (!currentStudentId) { alert("Önce öğrenci seçiniz."); return; }
  const date = document.getElementById("tytDate").value;
  if (!date) { alert("TYT deneme tarihi seçiniz."); return; }

  const subjects = {};
  let totalNet = 0;
  TYT_SUBJECTS.forEach(sub => {
    const cInput = document.querySelector(`[data-tyt-correct="${sub}"]`);
    const wInput = document.querySelector(`[data-tyt-wrong="${sub}"]`);
    const net = calcNet(cInput.value, wInput.value);
    subjects[sub] = {
      correct: Number(cInput.value) || 0,
      wrong: Number(wInput.value) || 0,
      net
    };
    totalNet += net;
  });

  const data = getStudentData(currentStudentId);
  data.tytExams.push({ date, subjects, totalNet });
  saveStudentData(currentStudentId, data);
  refreshExamListsAndCharts(data);
});

// AYT net hesaplamaları (anlık)
document.getElementById("aytTableBodyForm").addEventListener("input", () => {
  let totalNet = 0;

  let sayNet = 0;
  let sozNet = 0;
  let eaNet = 0;

  AYT_STRUCTURE.forEach(row => {
    const cInput = document.querySelector(`[data-ayt-correct="${row.key}"]`);
    const wInput = document.querySelector(`[data-ayt-wrong="${row.key}"]`);
    const netSpan = document.querySelector(`[data-ayt-net="${row.key}"]`);
    const net = calcNet(cInput.value, wInput.value);
    netSpan.textContent = net.toFixed(2);
    totalNet += net;

    // Bölüm bazlı netler
    if (row.section === "Fen Bilimleri" || row.section === "Matematik") {
      sayNet += net;
    }
    if (row.section === "Türk Dili ve Edebiyatı - Sosyal 1" || row.section === "Sosyal Bilimler-2") {
      sozNet += net;
    }
    if (row.section === "Türk Dili ve Edebiyatı - Sosyal 1" || row.section === "Matematik") {
      eaNet += net;
    }
  });

  document.getElementById("aytTotalNetLabel").textContent = totalNet.toFixed(2);
  document.getElementById("aytSayisalNetLabel").textContent = sayNet.toFixed(2);
  document.getElementById("aytSozelNetLabel").textContent = sozNet.toFixed(2);
  document.getElementById("aytEANetLabel").textContent = eaNet.toFixed(2);
});

// AYT kaydet
document.getElementById("saveAytExamBtn").addEventListener("click", () => {
  if (!currentStudentId) { alert("Önce öğrenci seçiniz."); return; }
  const date = document.getElementById("aytDate").value;
  if (!date) { alert("AYT deneme tarihi seçiniz."); return; }

  const subjects = {};
  let totalNet = 0;
  let sayNet = 0;
  let sozNet = 0;
  let eaNet = 0;

  AYT_STRUCTURE.forEach(row => {
    const cInput = document.querySelector(`[data-ayt-correct="${row.key}"]`);
    const wInput = document.querySelector(`[data-ayt-wrong="${row.key}"]`);
    const net = calcNet(cInput.value, wInput.value);
    subjects[row.key] = {
      section: row.section,
      subject: row.subject,
      correct: Number(cInput.value) || 0,
      wrong: Number(wInput.value) || 0,
      net
    };
    totalNet += net;

    if (row.section === "Fen Bilimleri" || row.section === "Matematik") {
      sayNet += net;
    }
    if (row.section === "Türk Dili ve Edebiyatı - Sosyal 1" || row.section === "Sosyal Bilimler-2") {
      sozNet += net;
    }
    if (row.section === "Türk Dili ve Edebiyatı - Sosyal 1" || row.section === "Matematik") {
      eaNet += net;
    }
  });

  const data = getStudentData(currentStudentId);
  data.aytExams.push({
    date,
    subjects,
    totalNet,
    sayNet,
    sozNet,
    eaNet
  });
  saveStudentData(currentStudentId, data);
  refreshExamListsAndCharts(data);
});

// Rapor kaydı
document.getElementById("saveReportBtn").addEventListener("click", () => {
  if (!currentStudentId) { alert("Önce öğrenci seçiniz."); return; }

  const title = document.getElementById("reportTitle").value.trim();
  const content = document.getElementById("reportContent").value.trim();
  if (!title || !content) {
    alert("Rapor başlık ve içeriği boş olamaz.");
    return;
  }

  const today = new Date();
  const dateStr = today.toISOString().split("T")[0];

  const data = getStudentData(currentStudentId);
  data.reports.push({ date: dateStr, title, content });
  saveStudentData(currentStudentId, data);

  document.getElementById("reportSaveStatus").textContent = "Kaydedildi.";
  setTimeout(() => { document.getElementById("reportSaveStatus").textContent = ""; }, 1500);

  document.getElementById("reportTitle").value = "";
  document.getElementById("reportContent").value = "";
  refreshReportsTable(data);
});

// Programdaki slot seçimi & kaydı
let selectedSlotKey = null;
document.getElementById("scheduleGrid").addEventListener("click", e => {
  const slotDiv = e.target.closest("[data-slot]");
  if (!slotDiv) return;
  selectedSlotKey = slotDiv.getAttribute("data-slot");
  document.getElementById("selectedSlotLabel").textContent = selectedSlotKey;
});

// Slot kaydet
document.getElementById("saveSlotBtn").addEventListener("click", () => {
  if (!currentStudentId) { alert("Önce öğrenci seçiniz."); return; }
  if (!selectedSlotKey) { alert("Önce ders programından bir alan seçiniz."); return; }

  const type = document.getElementById("slotType").value;
  const note = document.getElementById("slotNote").value.trim();
  if (!type || !note) {
    alert("Etkinlik türü ve not alanı boş bırakılamaz.");
    return;
  }

  const data = getStudentData(currentStudentId);
  if (!data.schedule) data.schedule = {};
  data.schedule[selectedSlotKey] = { type, note };
  saveStudentData(currentStudentId, data);
  refreshScheduleView(data);
});

// Slot temizle
document.getElementById("clearSlotBtn").addEventListener("click", () => {
  if (!currentStudentId) { alert("Önce öğrenci seçiniz."); return; }
  if (!selectedSlotKey) { alert("Önce ders programından bir alan seçiniz."); return; }

  const data = getStudentData(currentStudentId);
  if (data.schedule && data.schedule[selectedSlotKey]) {
    delete data.schedule[selectedSlotKey];
    saveStudentData(currentStudentId, data);
    refreshScheduleView(data);
  }
});

// Mood kaydı
document.getElementById("saveMoodBtn").addEventListener("click", () => {
  if (!currentStudentId) { alert("Önce öğrenci seçiniz."); return; }

  const date = document.getElementById("moodDate").value;
  const mood = document.getElementById("moodSelect").value;
  const note = document.getElementById("moodNote").value.trim();
  const weekScore = Number(document.getElementById("weekScore").value);

  if (!date || !mood) {
    alert("Tarih ve duygu alanları zorunludur.");
    return;
  }

  const data = getStudentData(currentStudentId);
  if (!data.moodEntries) data.moodEntries = [];
  data.moodEntries.push({ date, mood, note, weekScore });
  saveStudentData(currentStudentId, data);

  document.getElementById("moodSaveStatus").textContent = "Kaydedildi.";
  setTimeout(() => { document.getElementById("moodSaveStatus").textContent = ""; }, 1500);

  document.getElementById("moodSuggestion").textContent = makeMoodSuggestion(mood, weekScore);
  refreshMoodView(data);
});

/* =========================================================
   INITIAL LOAD
   ========================================================= */

buildTytFormTable();
buildAytFormTable();
buildScheduleGrid();
loadStudentsFromBackend();

// Koç ismini header'a yazmak istersen PHP'den şu ID'yi gömebilirsin:
// document.getElementById("coachNameLabel").textContent = "Koç: <?php echo $_SESSION['user_name']; ?>";

</script>
</body>
</html>
