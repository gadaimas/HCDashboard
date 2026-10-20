<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HC Dashboard - PT Gadai MAS Nusantara</title>
    
    <!-- Memanggil Font Poppins dari Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Memanggil Ikon dari FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Memanggil library Chart.js untuk membuat grafik -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        /* ================= KUMPULAN WARNA (VARIABEL) ================= */
        :root {
            --navy-blue: #0B2447;
            --blue: #19376D;
            --gold: #F29F05;
            --white: #FFFFFF;
            --bg-light: #F5F7F8;
            --card-bg: #FFFFFF;
            --text-dark: #333333;
            --text-muted: #6c757d;
            --green: #198754;
            --orange: #FD7E14;
            --red: #DC3545;
            --border-color: #e0e0e0;
        }

        /* ================= PENGATURAN DASAR ================= */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background-color: var(--bg-light);
            color: var(--text-dark);
            display: flex;
            min-height: 100vh;
        }

        /* ================= SIDEBAR ================= */
        .sidebar {
            width: 250px;
            background-color: var(--navy-blue);
            color: var(--white);
            display: flex;
            flex-direction: column;
            position: fixed;
            height: 100vh;
            transition: all 0.3s;
        }

        .sidebar-header {
            padding: 24px;
            text-align: center;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .sidebar-header h2 {
            font-size: 18px;
            color: var(--gold);
            font-weight: 700;
        }

        .sidebar-menu {
            list-style: none;
            padding: 20px 0;
        }

        .sidebar-menu li a {
            display: flex;
            align-items: center;
            padding: 15px 24px;
            color: var(--white);
            text-decoration: none;
            transition: 0.2s;
            font-size: 14px;
        }

        .sidebar-menu li a:hover, .sidebar-menu li a.active {
            background-color: var(--blue);
            border-left: 4px solid var(--gold);
        }

        .sidebar-menu li a i {
            margin-right: 15px;
            width: 20px;
            text-align: center;
        }

        /* ================= KONTEN UTAMA ================= */
        .main-content {
            flex: 1;
            margin-left: 250px;
            padding: 24px;
            width: calc(100% - 250px);
        }

        .demo-badge {
            background-color: var(--red);
            color: var(--white);
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
            display: inline-block;
            margin-bottom: 15px;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.7; }
            100% { opacity: 1; }
        }

        /* ================= BANNER ================= */
        .banner {
            background: linear-gradient(135deg, #ffffff 0%, #e6f0fa 100%);
            border-radius: 12px;
            padding: 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            margin-bottom: 24px;
            border-left: 6px solid var(--navy-blue);
        }

        .banner-text h1 {
            color: var(--navy-blue);
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .banner-text h1 span {
            color: var(--gold);
        }

        .banner-text p {
            color: var(--text-muted);
            font-size: 14px;
            margin-bottom: 10px;
        }

        .banner-text .tagline {
            font-style: italic;
            color: var(--blue);
            font-weight: 500;
        }

        .banner-illustration {
            font-size: 60px;
            color: var(--blue);
            opacity: 0.8;
        }

        /* ================= FILTER ================= */
        .filter-section {
            display: flex;
            gap: 15px;
            margin-bottom: 24px;
            align-items: center;
            background: var(--card-bg);
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.03);
        }

        .filter-section select {
            padding: 8px 15px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            font-family: 'Poppins', sans-serif;
            color: var(--text-dark);
            outline: none;
        }

        .btn-reset {
            background-color: var(--gold);
            color: var(--navy-blue);
            border: none;
            padding: 9px 20px;
            border-radius: 6px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.2s;
        }

        .btn-reset:hover {
            background-color: #d98d04;
        }

        /* ================= KPI CARDS ================= */
        .kpi-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
            margin-bottom: 24px;
        }

        .kpi-card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.03);
            display: flex;
            flex-direction: column;
            transition: transform 0.2s;
        }

        .kpi-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.08);
        }

        .kpi-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .kpi-title {
            font-size: 14px;
            font-weight: 600;
            color: var(--navy-blue);
        }

        .kpi-icon {
            background: rgba(25, 55, 109, 0.1);
            color: var(--blue);
            width: 40px;
            height: 40px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
        }

        .kpi-value-container {
            display: flex;
            align-items: flex-end;
            gap: 10px;
            margin-bottom: 15px;
        }

        .kpi-value {
            font-size: 32px;
            font-weight: 700;
            color: var(--navy-blue);
            line-height: 1;
        }

        .kpi-trend {
            font-size: 12px;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .trend-up { color: var(--green); }
        .trend-down { color: var(--red); }

        .kpi-details {
            font-size: 12px;
            color: var(--text-muted);
            border-top: 1px solid var(--border-color);
            padding-top: 10px;
            margin-top: auto;
        }

        .detail-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 4px;
        }
        
        .dot {
            height: 8px;
            width: 8px;
            border-radius: 50%;
            display: inline-block;
            margin-right: 5px;
        }

        /* ================= CHARTS GRID ================= */
        .chart-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            margin-bottom: 24px;
        }

        .chart-card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.03);
        }

        .chart-title {
            font-size: 16px;
            font-weight: 600;
            color: var(--navy-blue);
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid var(--border-color);
        }

        .chart-container {
            position: relative;
            height: 250px;
            width: 100%;
        }

        .chart-container-double {
            display: flex;
            justify-content: space-around;
            height: 250px;
        }

        .half-chart {
            width: 45%;
            position: relative;
        }

        /* ================= TABLE SECTION ================= */
        .table-card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.03);
            margin-bottom: 24px;
        }

        .table-header-flex {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .search-box {
            padding: 6px 12px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            outline: none;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 13px;
        }

        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid var(--border-color);
        }

        th {
            background-color: rgba(11, 36, 71, 0.05);
            color: var(--navy-blue);
            font-weight: 600;
        }

        .status-badge {
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
            color: var(--white);
        }

        .bg-red { background-color: var(--red); }
        .bg-orange { background-color: var(--orange); }
        .bg-green { background-color: var(--green); }

        /* ================= RESPONSIVE DESIGN ================= */
        @media (max-width: 1024px) {
            .kpi-grid { grid-template-columns: repeat(2, 1fr); }
            .chart-grid { grid-template-columns: 1fr; }
        }

        @media (max-width: 768px) {
            .sidebar { transform: translateX(-100%); }
            .main-content { margin-left: 0; width: 100%; }
            .kpi-grid { grid-template-columns: 1fr; }
            .banner { flex-direction: column; text-align: center; }
            .banner-illustration { display: none; }
            .chart-container-double { flex-direction: column; height: 500px; }
            .half-chart { width: 100%; height: 250px; }
            .filter-section { flex-wrap: wrap; }
        }
    </style>
</head>
<body>

    <!-- SIDEBAR NAVIGASI -->
    <aside class="sidebar">
        <div class="sidebar-header">
            <h2>Gadai MAS Nusantara</h2>
        </div>
        <ul class="sidebar-menu">
            <li><a href="#"><i class="fas fa-home"></i> Beranda</a></li>
            <li><a href="#" class="active"><i class="fas fa-chart-pie"></i> HC Dashboard</a></li>
        </ul>
    </aside>

    <!-- KONTEN UTAMA -->
    <main class="main-content">
        
        <div class="demo-badge">
            <i class="fas fa-exclamation-triangle"></i> MODE DEMO — DATA SIMULASI
        </div>

        <!-- BANNER -->
        <div class="banner">
            <div class="banner-text">
                <p>Selamat Datang di</p>
                <h1>HC <span>DASHBOARD</span></h1>
                <p>Satu Portal untuk Informasi, Layanan dan Pengembangan Human Capital.</p>
                <p class="tagline">People Today, Stronger Tomorrow.</p>
            </div>
            <div class="banner-illustration">
                <i class="fas fa-users-cog"></i>
            </div>
        </div>

        <!-- FILTER SECTION -->
        <div class="filter-section">
            <select id="filterPeriode">
                <option value="okt2026">Oktober 2026</option>
                <option value="sep2026">September 2026</option>
            </select>
            <select id="filterArea">
                <option value="all">Seluruh Indonesia</option>
                <option value="jakarta">Jakarta</option>
                <option value="jabar">Jawa Barat</option>
                <option value="jatim">Jawa Timur</option>
            </select>
            <button class="btn-reset" onclick="resetFilters()"><i class="fas fa-sync-alt"></i> Reset Filter</button>
        </div>

        <!-- KPI CARDS -->
        <div class="kpi-grid">
            <!-- KPI 1 -->
            <div class="kpi-card">
                <div class="kpi-header">
                    <span class="kpi-title">Total SDM Selindo</span>
                    <div class="kpi-icon"><i class="fas fa-users"></i></div>
                </div>
                <div class="kpi-value-container">
                    <span class="kpi-value" id="val-sdm">1.248</span>
                    <span class="kpi-trend trend-up"><i class="fas fa-caret-up"></i> 3%</span>
                </div>
                <div class="kpi-details">
                    <div class="detail-row"><span><span class="dot" style="background:var(--blue)"></span>Tetap</span> <span id="val-tetap">820</span></div>
                    <div class="detail-row"><span><span class="dot" style="background:var(--gold)"></span>Kontrak</span> <span id="val-kontrak">320</span></div>
                    <div class="detail-row"><span><span class="dot" style="background:#ccc"></span>Lainnya</span> <span id="val-lainnya">108</span></div>
                </div>
            </div>

            <!-- KPI 2 -->
            <div class="kpi-card">
                <div class="kpi-header">
                    <span class="kpi-title">TDP (Talent Dev. Program)</span>
                    <div class="kpi-icon"><i class="fas fa-graduation-cap"></i></div>
                </div>
                <div class="kpi-value-container">
                    <span class="kpi-value" id="val-tdp">86</span>
                    <span class="kpi-trend trend-up"><i class="fas fa-caret-up"></i> 12%</span>
                </div>
                <div class="kpi-details">
                    <div class="detail-row"><span><span class="dot" style="background:var(--green)"></span>Selesai</span> <span id="val-tdp-selesai">40</span></div>
                    <div class="detail-row"><span><span class="dot" style="background:var(--gold)"></span>Proses</span> <span id="val-tdp-proses">28</span></div>
                    <div class="detail-row"><span><span class="dot" style="background:var(--red)"></span>Tertunda</span> <span id="val-tdp-tunda">18</span></div>
                </div>
            </div>

            <!-- KPI 3 -->
            <div class="kpi-card">
                <div class="kpi-header">
                    <span class="kpi-title">GMDP</span>
                    <div class="kpi-icon"><i class="fas fa-chart-line"></i></div>
                </div>
                <div class="kpi-value-container">
                    <span class="kpi-value" id="val-gmdp">64</span>
                    <span class="kpi-trend trend-up"><i class="fas fa-caret-up"></i> 8%</span>
                </div>
                <div class="kpi-details">
                    <div class="detail-row"><span><span class="dot" style="background:var(--green)"></span>Selesai</span> <span id="val-gmdp-selesai">28</span></div>
                    <div class="detail-row"><span><span class="dot" style="background:var(--gold)"></span>Proses</span> <span id="val-gmdp-proses">24</span></div>
                    <div class="detail-row"><span><span class="dot" style="background:var(--red)"></span>Tertunda</span> <span id="val-gmdp-tunda">12</span></div>
                </div>
            </div>

            <!-- KPI 4 -->
            <div class="kpi-card">
                <div class="kpi-header">
                    <span class="kpi-title">PJS & PJP</span>
                    <div class="kpi-icon"><i class="fas fa-briefcase"></i></div>
                </div>
                <div class="kpi-value-container">
                    <span class="kpi-value" id="val-pjs">42</span>
                    <span class="kpi-trend trend-up"><i class="fas fa-caret-up"></i> 5%</span>
                </div>
                <div class="kpi-details">
                    <div class="detail-row"><span><span class="dot" style="background:var(--blue)"></span>PJS Aktif</span> <span id="val-pjs-aktif">22</span></div>
                    <div class="detail-row"><span><span class="dot" style="background:var(--gold)"></span>PJP Aktif</span> <span id="val-pjp-aktif">20</span></div>
                    <div class="detail-row"><span><span class="dot" style="background:var(--red)"></span>Menunggu</span> <span id="val-pjs-tunda">14</span></div>
                </div>
            </div>
        </div>

        <!-- CHARTS ROW 1 -->
        <div class="chart-grid">
            <!-- Chart Distribusi -->
            <div class="chart-card">
                <div class="chart-title">Distribusi Total SDM Selindo</div>
                <div class="chart-container">
                    <canvas id="distribusiChart"></canvas>
                </div>
            </div>

            <!-- Chart TDP & GMDP (Donuts) -->
            <div class="chart-card">
                <div class="chart-title">Status Program TDP & GMDP</div>
                <div class="chart-container-double">
                    <div class="half-chart">
                        <canvas id="tdpChart"></canvas>
                    </div>
                    <div class="half-chart">
                        <canvas id="gmdpChart"></canvas>
                    </div>
                </div>
            </div>
        </div>

        <!-- CHARTS ROW 2 -->
        <div class="chart-grid">
            <!-- Chart Tren -->
            <div class="chart-card">
                <div class="chart-title">Tren Total SDM Selindo</div>
                <div class="chart-container">
                    <canvas id="trenChart"></canvas>
                </div>
            </div>
            
            <!-- Chart Kebutuhan -->
            <div class="chart-card">
                <div class="chart-title">Ringkasan Kebutuhan SDM per Area</div>
                <div class="chart-container">
                    <canvas id="kebutuhanChart"></canvas>
                </div>
            </div>
        </div>

        <!-- TABLE -->
        <div class="table-card">
            <div class="table-header-flex">
                <div class="chart-title" style="border:none; margin:0; padding:0;">Ringkasan Tindak Lanjut HC</div>
                <input type="text" id="searchInput" class="search-box" placeholder="Cari area atau program..." onkeyup="searchTable()">
            </div>
            <div style="overflow-x:auto;">
                <table id="tindakLanjutTable">
                    <thead>
                        <tr>
                            <th>Area</th>
                            <th>Program</th>
                            <th>Prioritas</th>
                            <th>Ringkasan Tindak Lanjut</th>
                            <th>Status</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Jakarta</td>
                            <td>Pengisian Jabatan</td>
                            <td>Tinggi</td>
                            <td>Pemenuhan posisi Manajer Area yang kosong</td>
                            <td><span class="status-badge bg-red">Perlu Tindakan</span></td>
                        </tr>
                        <tr>
                            <td>Jawa Barat</td>
                            <td>TDP</td>
                            <td>Sedang</td>
                            <td>Review presentasi akhir peserta batch 4</td>
                            <td><span class="status-badge bg-orange">Dalam Proses</span></td>
                        </tr>
                        <tr>
                            <td>Sumatera</td>
                            <td>GMDP</td>
                            <td>Rendah</td>
                            <td>Orientasi awal peserta baru</td>
                            <td><span class="status-badge bg-green">Sesuai Jadwal</span></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

    </main>

    <!-- SCRIPT JAVASCRIPT UNTUK INTERAKSI DAN GRAFIK -->
    <script>
        // Konfigurasi Warna Standar
        const colors = {
            navy: '#0B2447',
            blue: '#19376D',
            gold: '#F29F05',
            green: '#198754',
            orange: '#FD7E14',
            red: '#DC3545',
            gray: '#e0e0e0'
        };

        // Objek untuk menyimpan instance grafik agar bisa di-update/dihapus
        let charts = {};

        // Data Simulasi (Bisa diubah-ubah)
        const mockData = {
            okt2026: {
                sdmTotal: "1.248", sdmTetap: "820", sdmKontrak: "320", sdmLain: "108",
                tdpTotal: "86", tdpSelesai: 40, tdpProses: 28, tdpTunda: 18,
                gmdpTotal: "64", gmdpSelesai: 28, gmdpProses: 24, gmdpTunda: 12,
                distribusi: [312, 256, 210, 184, 168, 118] // Jkt, Jabar, Jatim, Sum, Jateng, Lain
            },
            sep2026: {
                sdmTotal: "1.210", sdmTetap: "800", sdmKontrak: "310", sdmLain: "100",
                tdpTotal: "80", tdpSelesai: 35, tdpProses: 30, tdpTunda: 15,
                gmdpTotal: "60", gmdpSelesai: 25, gmdpProses: 25, gmdpTunda: 10,
                distribusi: [300, 250, 200, 180, 160, 120]
            }
        };

        // Fungsi Utama untuk menggambar semua grafik
        function initCharts(dataKey = 'okt2026') {
            const data = mockData[dataKey];

            // 1. Distribusi SDM (Horizontal Bar)
            const ctxDist = document.getElementById('distribusiChart').getContext('2d');
            if(charts.dist) charts.dist.destroy(); // Hapus yang lama jika ada
            charts.dist = new Chart(ctxDist, {
                type: 'bar',
                data: {
                    labels: ['Jakarta', 'Jawa Barat', 'Jawa Timur', 'Sumatera', 'Jawa Tengah', 'Lainnya'],
                    datasets: [{
                        label: 'Total Karyawan',
                        data: data.distribusi,
                        backgroundColor: colors.blue,
                        borderRadius: 4
                    }]
                },
                options: {
                    indexAxis: 'y', // Membuat bar menjadi horizontal
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } }
                }
            });

            // 2. Status TDP (Doughnut)
            const ctxTdp = document.getElementById('tdpChart').getContext('2d');
            if(charts.tdp) charts.tdp.destroy();
            charts.tdp = new Chart(ctxTdp, {
                type: 'doughnut',
                data: {
                    labels: ['Selesai', 'Dalam Proses', 'Tertunda'],
                    datasets: [{
                        data: [data.tdpSelesai, data.tdpProses, data.tdpTunda],
                        backgroundColor: [colors.green, colors.gold, colors.red]
                    }]
                },
                options: {
                    responsive: true, maintainAspectRatio: false,
                    plugins: { 
                        legend: { position: 'bottom', labels: { boxWidth: 12 } },
                        title: { display: true, text: 'TDP' }
                    }
                }
            });

            // 3. Status GMDP (Doughnut)
            const ctxGmdp = document.getElementById('gmdpChart').getContext('2d');
            if(charts.gmdp) charts.gmdp.destroy();
            charts.gmdp = new Chart(ctxGmdp, {
                type: 'doughnut',
                data: {
                    labels: ['Selesai', 'Dalam Proses', 'Tertunda'],
                    datasets: [{
                        data: [data.gmdpSelesai, data.gmdpProses, data.gmdpTunda],
                        backgroundColor: [colors.green, colors.gold, colors.red]
                    }]
                },
                options: {
                    responsive: true, maintainAspectRatio: false,
                    plugins: { 
                        legend: { position: 'bottom', labels: { boxWidth: 12 } },
                        title: { display: true, text: 'GMDP' }
                    }
                }
            });

            // 4. Tren SDM (Line)
            const ctxTren = document.getElementById('trenChart').getContext('2d');
            if(charts.tren) charts.tren.destroy();
            charts.tren = new Chart(ctxTren, {
                type: 'line',
                data: {
                    labels: ['Mei', 'Jun', 'Jul', 'Agt', 'Sep', 'Okt'],
                    datasets: [{
                        label: 'Total SDM',
                        data: [1000, 1050, 1100, 1180, 1210, parseInt(data.sdmTotal.replace('.',''))],
                        borderColor: colors.blue,
                        backgroundColor: 'rgba(25, 55, 109, 0.1)',
                        fill: true,
                        tension: 0.3,
                        pointBackgroundColor: colors.gold
                    }]
                },
                options: {
                    responsive: true, maintainAspectRatio: false,
                    plugins: { legend: { display: false } }
                }
            });

            // 5. Kebutuhan SDM per Area (Grouped Bar)
            const ctxKeb = document.getElementById('kebutuhanChart').getContext('2d');
            if(charts.keb) charts.keb.destroy();
            charts.keb = new Chart(ctxKeb, {
                type: 'bar',
                data: {
                    labels: ['Jakarta', 'Jawa Barat', 'Jawa Tengah', 'Jawa Timur', 'Sumatera', 'Lainnya'],
                    datasets: [
                        { label: 'Total SDM', data: data.distribusi, backgroundColor: colors.navy },
                        { label: 'Kebutuhan Tambahan', data: [28, 24, 18, 22, 16, 12], backgroundColor: colors.gold }
                    ]
                },
                options: {
                    responsive: true, maintainAspectRatio: false,
                    plugins: { legend: { position: 'top' } }
                }
            });
        }

        // Fungsi Update Nilai KPI saat Filter berubah
        function updateKPIs(dataKey) {
            const data = mockData[dataKey];
            document.getElementById('val-sdm').innerText = data.sdmTotal;
            document.getElementById('val-tetap').innerText = data.sdmTetap;
            document.getElementById('val-kontrak').innerText = data.sdmKontrak;
            document.getElementById('val-lainnya').innerText = data.sdmLain;

            document.getElementById('val-tdp').innerText = data.tdpTotal;
            document.getElementById('val-tdp-selesai').innerText = data.tdpSelesai;
            document.getElementById('val-tdp-proses').innerText = data.tdpProses;
            document.getElementById('val-tdp-tunda').innerText = data.tdpTunda;
        }

        // Listener untuk Filter Periode
        document.getElementById('filterPeriode').addEventListener('change', function(e) {
            const selectedVal = e.target.value;
            updateKPIs(selectedVal);
            initCharts(selectedVal);
        });

        // Fungsi Reset Filter
        function resetFilters() {
            document.getElementById('filterPeriode').value = 'okt2026';
            document.getElementById('filterArea').value = 'all';
            updateKPIs('okt2026');
            initCharts('okt2026');
        }

        // Fungsi Pencarian di Tabel
        function searchTable() {
            let input = document.getElementById("searchInput");
            let filter = input.value.toLowerCase();
            let table = document.getElementById("tindakLanjutTable");
            let tr = table.getElementsByTagName("tr");

            for (let i = 1; i < tr.length; i++) {
                let tdArea = tr[i].getElementsByTagName("td")[0];
                let tdProgram = tr[i].getElementsByTagName("td")[1];
                if (tdArea || tdProgram) {
                    let textArea = tdArea.textContent || tdArea.innerText;
                    let textProgram = tdProgram.textContent || tdProgram.innerText;
                    if (textArea.toLowerCase().indexOf(filter) > -1 || textProgram.toLowerCase().indexOf(filter) > -1) {
                        tr[i].style.display = "";
                    } else {
                        tr[i].style.display = "none";
                    }
                }       
            }
        }

        // Jalankan saat halaman pertama kali dibuka
        window.onload = function() {
            initCharts('okt2026');
        };
    </script>
</body>
</html>