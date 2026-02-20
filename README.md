![logo jpg](https://github.com/user-attachments/assets/b709764c-c5df-4876-833f-722efecbf6e9)
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>JS Motors Lyon</title>
    
    <link rel="apple-touch-icon" href="https://raw.githubusercontent.com/user-attachments/assets/5bae5cb6-c434-49aa-842e-1a5be52f0df5">
    <link rel="icon" type="image/png" href="https://raw.githubusercontent.com/user-attachments/assets/5bae5cb6-c434-49aa-842e-1a5be52f0df5">

    <style>
        body { font-family: sans-serif; background: #f0f2f5; margin: 0; padding: 10px; }
        .container { max-width: 500px; margin: auto; }
        .header { background: white; padding: 15px; border-radius: 20px; text-align: center; margin-bottom: 20px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
        .header img { width: 100%; max-width: 300px; height: auto; }
        .form-group { background: white; padding: 20px; border-radius: 20px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); }
        .section-title { color: #b22222; font-size: 16px; font-weight: bold; margin: 15px 0; text-transform: uppercase; border-left: 4px solid #b22222; padding-left: 10px; }
        input { width: 100%; padding: 12px; margin-bottom: 10px; border: 1px solid #ddd; border-radius: 10px; box-sizing: border-box; font-size: 16px; }
        .main-btn { background: #1a1a1a; color: white; border: none; padding: 16px; width: 100%; border-radius: 12px; font-weight: bold; font-size: 16px; }
        .or-card { background: white; padding: 15px; margin-top: 10px; border-radius: 15px; border-left: 6px solid #b22222; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .details { display: none; margin-top: 15px; padding-top: 15px; border-top: 1px solid #eee; font-size: 14px; line-height: 1.6; }
        .info-block { background: #f9f9f9; padding: 10px; border-radius: 10px; margin-bottom: 10px; }
    </style>
</head>
<body>
<div class="container">
    <div class="header">
        <img src="https://github.com/user-attachments/assets/5bae5cb6-c434-49aa-842e-1a5be52f0df5" alt="JS MOTORS LYON">
    </div>

    <div class="form-group">
        <div class="section-title">Nouveau Dossier</div>
        <input type="text" id="nom" placeholder="👤 Nom du Client">
        <input type="tel" id="tel" placeholder="📞 Téléphone">
        <input type="text" id="marque" placeholder="🚗 Véhicule">
        <input type="text" id="panne" placeholder="🛠️ Travaux">
        <button class="main-btn" onclick="creerOR()">CRÉER LE DOSSIER</button>
    </div>

    <div class="section-title">Dossiers en cours</div>
    <div id="listeOR"></div>
</div>

<script>
    window.onload = () => {
        const d = localStorage.getItem('jsDataV4');
        if(d) document.getElementById('listeOR').innerHTML = d;
    };
    function save() { localStorage.setItem('jsDataV4', document.getElementById('listeOR').innerHTML); }
    function creerOR() {
        const n = document.getElementById('nom').value;
        const m = document.getElementById('marque.').value;
        if(!n || !m) return alert("Nom et Véhicule requis");
        const id = "OR-" + Math.floor(1000 + Math.random() * 9000);
        const card = document.createElement('div');
        card.className = 'or-card';
        card.innerHTML = `<div onclick="this.nextElementSibling.style.display = (this.nextElementSibling.style.display === 'block' ? 'none' : 'block')">
            <strong>${id}</strong> | ${document.getElementById('marque').value}</div>
            <div class="details">
                <div class="info-block">👤 ${document.getElementById('nom').value}<br>📞 ${document.getElementById('tel').value}</div>
                <div>🛠️ ${document.getElementById('panne').value}</div>
                <button style="color:red; background:none; border:none; margin-top:10px;" onclick="this.closest('.or-card').remove();save();">Supprimer</button>
            </div>`;
        document.getElementById('listeOR').prepend(card);
        save();
    }
</script>
</body>
</html>
