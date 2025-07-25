<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>BIHAR | Basis Informasi Harian Ancaman dan Respon</title>

  <!-- ✅ Tailwind & Leaflet -->
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/leaflet@1.9.4/dist/leaflet.css"/>
  <script src="https://cdn.jsdelivr.net/npm/leaflet@1.9.4/dist/leaflet.js"></script>

  <style>
    #map, #map-parameter { height: 500px; }
    .active-tab {
      background-color: #f97316;
      color: white;
      font-weight: bold;
      border-radius: 0.25rem;
    }
  </style>
</head>
<body class="bg-gradient-to-r from-green-50 to-orange-50 font-sans">
  <div class="flex min-h-screen">
    <!-- ========== SIDEBAR ========== -->
    <aside class="w-60 bg-green-900 text-white p-4">
      <h1 class="text-2xl font-bold mb-8">BIHAR<br><span class="text-xs">Basis Informasi Harian Ancaman dan Respon</span></h1>
      <nav class="space-y-4">
        <a href="#" id="tab-beranda" onclick="showSection('beranda')" class="block px-3 py-2">Beranda</a>
        <a href="#" id="tab-ParameterBencana" onclick="showSection('ParameterBencana')" class="block px-3 py-2">Parameter Bencana</a>
        <a href="#" id="tab-infografis" onclick="showSection('infografis')" class="block px-3 py-2">Infografis</a>
        <a href="#" id="tab-jalurEvakuasi" onclick="showSection('jalurEvakuasi')" class="block px-3 py-2">Jalur Evakuasi</a>
      </nav>
    </aside>

    <!-- ========== MAIN CONTENT ========== -->
    <main class="flex-1 p-6">
      <!-- 🔸 BERANDA -->
<div id="beranda" class="page-section block">
  <!-- 🔶 Hero Section -->
  <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-8">
    <div class="max-w-xl">
      <h2 class="text-3xl font-bold text-orange-600">Kenali Ancaman, Siapkan Perlindungan.</h2>
      <p class="mt-2 text-sm text-gray-600">
        <strong>BIHAR</strong> (Basis Informasi Harian Ancaman dan Respon) adalah sistem WebGIS yang menyajikan informasi spasial terkini mengenai potensi dan kejadian bencana di Daerah Istimewa Yogyakarta. Akses peta parameter, jalur evakuasi, dan infografis harian untuk mendukung kesiapsiagaan masyarakat.
      </p>
      <button class="mt-4 px-4 py-2 bg-orange-500 text-black rounded shadow hover:bg-orange-600 transition">Lihat Peta Sekarang</button>
    </div>
    <img src="longsor1.jpg" alt="Longsor" class="w-40 h-40 object-contain mx-auto" />
  </div>

  <!-- 🧭 Fitur Utama -->
  <div class="mt-6">
    <h3 class="text-lg font-semibold mb-4">Fitur Utama</h3>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
      <div class="bg-white shadow rounded p-4 text-center">
        <p class="font-bold text-orange-600">Peta Parameter</p>
        <p class="text-sm text-gray-600">Visualisasi spasial seperti kelerengan, curah hujan, dan tutupan lahan.</p>
      </div>
      <div class="bg-white shadow rounded p-4 text-center">
        <p class="font-bold text-orange-600">Infografis Terkini</p>
        <p class="text-sm text-gray-600">Statistik visual dampak bencana berdasarkan parameter harian.</p>
      </div>
      <div class="bg-white shadow rounded p-4 text-center">
        <p class="font-bold text-orange-600">Jalur Evakuasi</p>
        <p class="text-sm text-gray-600">Rute aman untuk evakuasi bencana berbasis lokasi dan jenis bahaya.</p>
      </div>
      <div class="bg-white shadow rounded p-4 text-center">
        <p class="font-bold text-orange-600">Kejadian Harian</p>
        <p class="text-sm text-gray-600">Update harian peristiwa bencana di wilayah DIY dan sekitarnya.</p>
      </div>
    </div>
  </div>

  <!-- ⚠️ Fakta Mitigasi -->
  <div class="mt-10 bg-yellow-100 p-4 rounded shadow">
    <p class="text-sm text-gray-700 italic">“Sebagian wilayah Daerah Istimewa Yogyakarta memiliki kerentanan tinggi terhadap bencana longsor, terutama saat musim hujan. Kenali tingkat risiko longsor di sekitar Anda dan rencanakan jalur evakuasi sedini mungkin”</p>
  </div>

  <!-- 🔵 Sumber Data & Logo UNDIP -->
  <div class="mt-10 flex flex-col md:flex-row items-center justify-between gap-4 border-t pt-4">
    <div class="text-sm text-gray-600 text-center md:text-left">
      <p><strong>Sumber Data:</strong> BIG, BMKG, BNPB, BPS, PUSDALOPS BPBD DIY</p>
      <p><strong>Dikembangkan oleh:</strong> Nadia Retdianti Aprilia Putri (2110122130064), Fadhila meisyahra (21110122130076)</p>
    </div>
    <img src="logo-undip.png" alt="Logo UNDIP" class="h-16 object-contain">
  </div>
</div>


<!-- 🔸 PARAMETER BENCANA -->
<div id="ParameterBencana" class="page-section hidden">
  <h2 class="text-2xl font-bold text-orange-600 mb-4">Peta Parameter Bencana</h2>

  <!-- 🔸 Filter Atas -->
  <div class="mb-4 flex flex-col md:flex-row md:items-end md:space-x-4">
    <div class="flex-1">
      <label for="paramSelect" class="block font-medium text-gray-700 mb-1">Pilih Parameter:</label>
      <select id="paramSelect" class="border p-2 rounded w-full">
        <option value="kelerengan">Kelerengan</option>
        <option value="jenis_tanah">Jenis Tanah</option>
        <option value="curahhujan">Curah Hujan</option>
        <option value="tuplah150">Tutupan Lahan</option>
        <option value="pemukiman">Pemukiman</option>
        <option value="kepadatanpenduduk">Kepadatan Penduduk</option>
        <option value="kepadatan_bangunan">Kepadatan Bangunan</option>
      </select>
    </div>

    <div class="flex-1">
      <label for="kabupatenSelect" class="block font-medium text-gray-700 mb-1">Pilih Kabupaten:</label>
      <select id="kabupatenSelect" class="border p-2 rounded w-full">
        <option value="">-- Pilih --</option>
        <option value="Bantul">Bantul</option>
        <option value="Sleman">Sleman</option>
        <option value="Gunung Kidul">Gunung Kidul</option>
        <option value="Kulon Progo">Kulon Progo</option>
        <option value="Kota Yogyakarta">Kota Yogyakarta</option>
      </select>
    </div>

    <div class="mt-2">
      <label class="inline-flex items-center">
        <input type="checkbox" id="toggleKabupaten" class="form-checkbox text-green-600 mr-2">
        <span class="text-sm text-gray-700">Tampilkan Batas Kabupaten</span>
      </label>
    </div>
  </div>

  <!-- 🔸 Peta Parameter -->
  <div id="map-parameter" class="rounded shadow" style="height: 500px;"></div>

  <!-- 🔸 Judul Bawah Peta -->
  <h3 class="text-2xl font-bold text-orange-600 mb-4 mt-6">PETA PARAMETER BENCANA DIY</h3>

  <!-- 🔸 Filter Bawah & Ilustrasi -->
  <div class="mb-4 flex flex-col space-y-4">
    <div class="flex-1">
      <label for="paramSelectbawah" class="block font-medium text-gray-700 mb-1">Pilih Parameter:</label>
      <select id="paramSelectbawah" class="border p-2 rounded w-full">
        <option value="kelerengan">Kelerengan</option>
        <option value="jenis_tanah">Jenis Tanah</option>
        <option value="curahhujan">Curah Hujan</option>
        <option value="tuplah150">Tutupan Lahan</option>
        <option value="pemukiman">Pemukiman</option>
        <option value="kepadatanpenduduk">Kepadatan Penduduk</option>
        <option value="kepadatan_bangunan">Kepadatan Bangunan</option>
      </select>
    </div>

    <!-- 🔸 Gambar Ilustrasi -->
    <img src="PetaEvakuasi.jpg_large" alt="Ilustrasi Jalur Evakuasi" class="w-full h-auto max-w-7xl mx-auto rounded shadow" />
  </div>
</div>


      <!-- 🔸 INFOGRAFIS & JALUR EVAKUASI -->
      <div id="jalurEvakuasi" class="page-section hidden">
  <!-- 🔸 Judul Atas -->
  <h2 class="text-2xl font-bold text-orange-600 mb-4">PETA INTERAKTIF</h2>

  <!-- 🔸 Dropdown Filter Kabupaten -->
  <div class="mb-4">
    <label for="kabupatenSelectEvakuasi" class="block mb-1 text-sm font-semibold text-gray-700">Pilih Kabupaten:</label>
    <select id="kabupatenSelectEvakuasi" class="border p-2 rounded w-full md:w-1/2">
      <option value="">-- Pilih Kabupaten --</option>
      <option value="Bantul">Bantul</option>
      <option value="Sleman">Sleman</option>
      <option value="Gunung Kidul">Gunung Kidul</option>
      <option value="Kulon Progo">Kulon Progo</option>
      <option value="Kota Yogyakarta">Kota Yogyakarta</option>
    </select>
  </div>

  <!-- 🔸 Peta -->
  <div id="map" class="rounded shadow overflow-hidden mb-6" style="height: 500px;"></div>

  <!-- 🔸 Judul Bawah Peta -->
  <h3 class="text-xl font-semibold text-gray-800 mb-4">PETA JALUR EVAKUASI DIY</h3>

  <!-- 🔸 Gambar Ilustrasi -->
    <img src="PetaEvakuasi.jpg_large" alt="Ilustrasi Jalur Evakuasi" class="w-full h-auto max-w-7xl mx-auto rounded shadow" />
  </div>


  <!-- ✅ SCRIPT -->
  <script>
    const kabupatenCoords = {
      "Bantul": [-7.89, 110.36],
      "Sleman": [-7.68, 110.38],
      "Gunung Kidul": [-8.03, 110.62],
      "Kulon Progo": [-7.85, 110.13],
      "Kota Yogyakarta": [-7.8014, 110.3649]
    };

    let map = L.map('map').setView([-7.7956, 110.3695], 9);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: 'Map data © OpenStreetMap contributors'
    }).addTo(map);
    L.marker([-7.7956, 110.3695]).addTo(map).bindPopup('Yogyakarta');

    let mapParameterBencana = null;
    let parameterLayers = {};
    let kabupatenLayer = null;

    function loadKabupatenLayer() {
      fetch('./batas_kabupaten_diy.geojson')
        .then(res => res.json())
        .then(data => {
          kabupatenLayer = L.geoJSON(data, {
            style: {
              color: '#16a34a', weight: 2, fillOpacity: 0
            }
          });
          if (document.getElementById('toggleKabupaten').checked) {
            kabupatenLayer.addTo(mapParameterBencana);
          }
        });
    }

    document.getElementById('toggleKabupaten').addEventListener('change', function () {
      if (!kabupatenLayer) return;
      if (this.checked) {
        kabupatenLayer.addTo(mapParameterBencana);
      } else {
        mapParameterBencana.removeLayer(kabupatenLayer);
      }
    });

    document.getElementById("paramSelect").addEventListener("change", function () {
      const selectedParam = this.value;
      Object.values(parameterLayers).forEach(layer => {
        if (mapParameterBencana.hasLayer(layer)) {
          mapParameterBencana.removeLayer(layer);
        }
      });

      fetch(`./${selectedParam}.geojson`)
  .then(response => response.json())
  .then(data => {
    const layer = L.geoJSON(data, {
      style: function (feature) {
        const code = feature.properties.gridcode;
        let fillColor = '#ccc'; // default abu-abu jika gridcode tidak ada
        if (code === 1) fillColor = '#d73027'; // merah
        else if (code === 2) fillColor = '#fc8d59'; // oranye
        else if (code === 3) fillColor = '#a6d96a'; // hijau muda
        else if (code === 4) fillColor = '#1a9850'; // hijau tua

        return {
          fillColor: fillColor,
          weight: 1,
          color: 'cyan',
          fillOpacity: 0.7
        };
      },
      onEachFeature: function (feature, layer) {
        const props = feature.properties;
        layer.bindPopup(
          Object.entries(props).map(([key, val]) => `<b>${key}</b>: ${val}`).join('<br>')
        );
      }
    }).addTo(mapParameterBencana);
    parameterLayers[selectedParam] = layer;
  });
  });

  document.getElementById("paramSelect").addEventListener("change", function () {
  const selectedParam = this.value;

  Object.values(parameterLayers).forEach(layer => {
    if (mapParameterBencana.hasLayer(layer)) {
      mapParameterBencana.removeLayer(layer);
    }
  });

  fetch(`./${selectedParam}.geojson`)
    .then(response => response.json())
    .then(data => {
      let layer;

      if (selectedParam === "tuplah150") {
  function getColorTutupanLahan(code) {
    switch (code) {
      case 1: return '#90ee90'; // Hijau muda
      case 2: return '#ff0000'; // Merah
      case 3: return '#006400'; // Hijau tua
      case 4: return '#f5f5dc'; // Beige
      default: return '#cccccc'; // Warna default kalau tidak ada
    }
  }

  layer = L.geoJSON(data, {
    style: function (feature) {
      const code = feature.properties.gridcode;
      return {
        fillColor: getColorTutupanLahan(code),
        color: '#ffffff',
        weight: 1,
        fillOpacity: 0.7
      };
    },
    onEachFeature: function (feature, layer) {
      const props = feature.properties;
      layer.bindPopup(
        Object.entries(props)
          .map(([k, v]) => `<b>${k}</b>: ${v}`)
          .join("<br>")
      );
    }
  });
}

      // === 🟠 Spesifik untuk Kepadatan Penduduk ===
      if (selectedParam === "kepadatanpenduduk") {
        function getColorKEP_PEND(d) {
          return d <= 730.937218 ? '#1a9641' :
                d <= 1464.453124 ? '#a6d96a' :
                d <= 2550.18635  ? '#ffffbf' :
                d <= 4150.391293 ? '#fdae61' :
                                       '#d7191c';
        }

        layer = L.geoJSON(data, {
          style: function (feature) {
            const d = feature.properties.KEP_PEND;
            return {
              fillColor: getColorKEP_PEND(d),
              weight: 1,
              color: 'white',
              fillOpacity: 0.9
            };
          },
          onEachFeature: function (feature, layer) {
            const props = feature.properties;
            layer.bindPopup(
              Object.entries(props).map(([k, v]) => `<b>${k}</b>: ${v}`).join("<br>")
            );
          }
        });

      } else {
        // === 🌱 Default styling untuk layer lain ===
        layer = L.geoJSON(data, {
          style: function (feature) {
            const code = feature.properties.gridcode;
            let fillColor = '#ccc';
            if (code === 1) fillColor = '#d73027';
            else if (code === 2) fillColor = '#fc8d59';
            else if (code === 3) fillColor = '#a6d96a';
            else if (code === 4) fillColor = '#1a9850';

            return {
              fillColor: fillColor,
              weight: 1,
              color: 'cyan',
              fillOpacity: 0.9
            };
          },
          onEachFeature: function (feature, layer) {
            const props = feature.properties;
            layer.bindPopup(
              Object.entries(props).map(([k, v]) => `<b>${k}</b>: ${v}`).join("<br>")
            );
          }
        });
      }

      layer.addTo(mapParameterBencana);
      parameterLayers[selectedParam] = layer;
    });
});



    document.getElementById("kabupatenSelect").addEventListener("change", function () {
      const selectedKab = this.value;
      if (selectedKab && kabupatenCoords[selectedKab]) {
        mapParameterBencana.setView(kabupatenCoords[selectedKab], 11);
      }
    });

    function showSection(id) {
      document.querySelectorAll('.page-section').forEach(s => s.classList.add('hidden'));
      document.getElementById(id).classList.remove('hidden');
      ["beranda", "ParameterBencana", "infografis", "jalurEvakuasi"].forEach(tab => {
        document.getElementById(`tab-${tab}`).classList.remove('active-tab');
      });
      document.getElementById(`tab-${id}`).classList.add('active-tab');

      if (id === 'ParameterBencana' && mapParameterBencana === null) {
        setTimeout(() => {
          mapParameterBencana = L.map('map-parameter').setView([-7.8, 110.4], 9);
          L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; OpenStreetMap contributors'
          }).addTo(mapParameterBencana);

          loadKabupatenLayer();
          document.getElementById("paramSelect").dispatchEvent(new Event("change"));
        }, 10);
      }
    }

    // Default tab
    showSection('beranda');
  </script>
</body>
</html>
