    button{background:#2e7d32; color:white; border:none; padding:13px; width:100%; border-radius:6px; font-weight:bold; font-size:16px; margin-top:8px; cursor:pointer;}
    button:active{background:#27662b;}
    #info{margin-top:15px; padding:12px; border-radius:6px; display:none; text-align:center; font-weight:bold;}
  </style>
</head>
<body>
  <h2>📦 OPEN PO PCB V2</h2>
  <div class="stok">Sisa Stok Tersedia: <span id="sisa">500</span> Unit</div>
  <div class="info-barang">Barang: PCB V2</div>

  <form id="formPesan">
    <input type="text" name="nama" placeholder="Nama Lengkap" required>
    <input type="tel" name="nowa" placeholder="Nomor WA Aktif (0812xxx)" required>
    <textarea name="alamat" placeholder="Alamat Lengkap Pengiriman" required></textarea>
    <input type="hidden" name="barang" value="PCB V2">
    <input type="number" name="jumlah" min="1" placeholder="Jumlah Pesan" required>
    <button type="submit">✅ KIRIM PESANAN</button>
  </form>
  <div id="info"></div>

  <script>
    const URL = "https://script.googleusercontent.com/macros/echo?user_content_key=AUkAhnR0VZcbu8Wkq8UG_oY6gWzQCU0t7kdBNvjnwqQh8ZAtbUcYIUzlpg4vHdX5YSk7_0zBtEsofMfZatMY4HzlMIGqRUIi2J4GcaOL2zFbmUQr63TQXnw4XHf78beptGmHdeFW7jqOJK3CaG96WMkAVk6ltKbGGICOdCIz8tUcdAsZDvvVN3ssTjE8HprusduSBheITZ6lhQ0fBuQr1HRAXh4x0ihTeZOUUKVLJ6K-TtV0RTa7fDseBLfbGQ9Hug0pRhF1nMq4p40ZdQvTMQ2cu1fpmphvVw&lib=McaMVEh9yOrocE2CI7ZdkTE-HkZssSrq4";

    const elSisa = document.getElementById("sisa");
    const elForm = document.getElementById("formPesan");
    const elInfo = document.getElementById("info");

    fetch(URL)
      .then(r => r.json())
      .then(d => elSisa.textContent = d.sisa || 500)
      .catch(() => elInfo.textContent = "⚠️ Sedang memuat...");

    elForm.addEventListener("submit", e => {
      e.preventDefault();
      elInfo.style.display = "block";
      elInfo.style.background = "#fff3cd";
      elInfo.style.color = "#856404";
      elInfo.textContent = "⏳ Sedang mencatat pesanan...";

      fetch(URL, {
        method: "POST",
        body: new FormData(elForm)
      })
      .then(r => r.json())
      .then(d => {
        elSisa.textContent = d.sisa;
        elInfo.style.background = "#d4edda";
        elInfo.style.color = "#155724";
        elInfo.textContent = "✅ BERHASIL TERCATAT! Sisa stok: " + d.sisa + " unit";
        elForm.reset();
      })
      .catch(() => {
        elInfo.style.background = "#f8d7da";
        elInfo.style.color = "#721c24";
        elInfo.textContent = "❌ Gagal simpan, coba ulangi sebentar ya";
      });
    });
  </script>
</body>
</html>
