# Scan-colis-UPS.INDEX.HTML
 Scan colis UPS 
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Tri colis UPS</title>

  <!-- Manifest PWA -->
  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#00c853">

  <!-- OCR -->
  <script src="[cdn.jsdelivr.net](https://cdn.jsdelivr.net/npm/tesseract.js@4/dist/tesseract.min.js)"></script>

  <style>
    body { 
      font-family: Arial, sans-serif; 
      margin:0; padding:20px; 
      background:#111; color:#fff; 
    }
    .box { max-width:720px; margin:auto; position:relative; z-index:5; }
    h1 { font-size:26px; }
    input { width:100%; padding:16px; box-sizing:border-box; font-size:18px; border-radius:8px; border:0; margin:12px 0; }
    button { width:100%; padding:16px; font-size:18px; border-radius:8px; border:0; background:#00c853; color:#fff; font-weight:bold; cursor:pointer; }
    #result { margin-top:18px; padding:18px; border-radius:10px; background:#222; font-size:20px; min-height:50px; }
    .ok { background:#103d20 !important; }
    .err { background:#4a1515 !important; }

    video {
      position: fixed; top: 0; left: 0;
      width: 100%; height: 100%;
      object-fit: cover;
      z-index: 1;
    }
    #scanZone {
      display:none;
      position: fixed;
      top: 15%; left: 8%;
      width: 84%; height: 28%;
      border: 3px solid #00ff00;
      border-radius: 12px;
      z-index: 2;
      pointer-events:none;
    }
    #infoMessage {
      display:none;
      position: fixed;
      bottom: 20px;
      left: 50%; transform: translateX(-50%);
      background: rgba(0,0,0,0.8);
      padding: 10px 18px;
      border-radius: 18px;
      font-size: 16px;
      z-index: 3;
    }
  </style>
</head>

<body>

<div id="scanZone"></div>

<div class="box">
  <h1>Scan / Saisie Adresse</h1>
  <input id="address" placeholder="Ex : 15 rue des Arceaux Montpellier" />
  <button onclick="startScan()">📸 Scanner l'adresse</button>
  <div id="result">En attente d'une adresse.</div>
</div>

<div id="infoMessage"></div>

<script>
