![logo jpg](https://github.com/user-attachments/assets/5bae5cb6-c434-49aa-842e-1a5be52f0df5)
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>JS Motors Lyon</title>
    <link rel="icon" type="image/jpeg" href="logo.jpg">
    <link rel="apple-touch-icon" href="logo.jpg">
    <style>
        body { font-family: 'Segoe UI', Roboto, sans-serif; background: #f0f2f5; margin: 0; padding: 10px; }
        .container { max-width: 500px; margin: auto; }
        .header { background: white; padding: 15px; border-radius: 20px; text-align: center; margin-bottom: 20px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
        .header img { width: 100%; max-width: 300px; height: auto; }
        
        .form-group { background: white; padding: 20px; border-radius: 20px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); margin-bottom: 20px; }
        .section-title { color: #b22222; font-size: 16px; font-weight: bold; margin-bottom: 15px; text-transform: uppercase; border-bottom: 2px solid #f0f0f0; padding-bottom: 5px; }
        
        input { width: 100%; padding: 12px; margin-bottom: 10px; border: 1px solid #ddd; border-radius: 10px; box-sizing: border-box; font-size: 16px; background: #fafafa; }
        .main-btn { background: #1a1a1a; color: white; border: none; padding: 16px; width: 100%; border-radius: 12px; font-weight: bold; font-size: 16px; margin-top: 10px; }
        
        .or-card { background: white; padding: 15px; margin-top: 10px; border-radius: 15px; border-left: 6px solid #b22222; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .or-header { display: flex; justify-content: space-between; align-items: center; cursor: pointer; }
        .details { display: none; margin-top: 15px; padding-top: 15px; border-top: 1px solid #eee; font-size: 14px; }
        .info-row { margin-bottom: 8px; display: flex; align-items: center; }
        .info-row i { margin-right: 10px; width: 20px; text-align: center; }
        .delete-btn { color: #d63031; background: #fff0f0; border: 1px solid #ffcccc; padding: 10px; width: 100%; border-radius: 8px; margin-top: 15px; font-weight: bold; }
    </style>
</head>
<body>
<div class="container">
   <div class="header">
    <img src="https://github.com/user-attachments/assets/5bae5cb6-c434-49aa-842e-1a5be52f0df5" alt="JS MOTORS LYON">
</div> 

    <div class="form-group">
        <div class="section-title">Nouveau Dossier</div>
        <input type="text" id="nom" placeholder="👤 Nom & Prénom">
        <input type="tel" id="tel" placeholder="📞 Téléphone">
        <input type="email" id="email" placeholder="📧 Email">
        <input type="text" id="adresse" placeholder="🏠 Adresse postale">
        <input type="text" id="marque" placeholder="🚗 Véhicule (Marque/Modèle)">
        <input type="number" id="km" placeholder="🛣️ Kilométrage">
        <input type="text" id="panne" placeholder="🛠️ Travaux à faire">
        <button class="main-btn" onclick="creerOR()">CRÉER L'ORDRE DE RÉPARATION</button>
    </div>

    <div class="section-title">Dossiers en cours</div>
    <div id="listeOR"></div>
</div>

<script>
    window.onload = () => {
        const d = localStorage.getItem('jsDataV3');
        if(d) document.getElementById('listeOR').innerHTML = d;
    };

    function save() { localStorage.setItem('jsDataV3', document.getElementById('listeOR').innerHTML); }

    function creerOR() {
        const fields = ['nom', 'tel', 'email', 'adresse', 'marque', 'km', 'panne'];
        const v = {};
        fields.forEach(f => v[f] = document.getElementById(f).value);
        if(!v.nom || !v.marque) return alert("Nom et Véhicule requis");

        const id = "OR-" + Math.floor(1000 + Math.random() * 9000);
        const card = document.createElement('div');
        card.className = 'or-card';
        card.innerHTML = `
            <div class="or-header" onclick="this.nextElementSibling.style.display = (this.nextElementSibling.style.display === 'block' ? 'none' : 'block')">
                <div><strong>${id}</strong> | ${v.marque}</div>
                <div style="font-size:12px; color:#b22222; font-weight:bold;">OUVERT</div>
            </div>
            <div class="details">
                <div class="info-row">👤 <b>Client :</b> ${v.nom}</div>
                <div class="info-row">📞 <b>Tél :</b> ${v.tel}</div>
                <div class="info-row">📧 <b>Email :</b> ${v.email}</div>
                <div class="info-row">🏠 <b>Adresse :</b> ${v.adresse}</div>
                <div class="info-row">🚗 <b>Véhicule :</b> ${v.marque}</div>
                <div class="info-row">🛣️ <b>KM :</b> ${v.km} km</div>
                <div class="info-row">🛠️ <b>Travaux :</b> ${v.panne}</div>
                <button class="delete-btn" onclick="if(confirm('Supprimer ?')){this.closest('.or-card').remove();save();}">SUPPRIMER</button>
            </div>`;
        document.getElementById('listeOR').prepend(card);
        fields.forEach(f => document.getElementById(f).value = '');
        save();
    }
</script>
</body>
</html>![logo jpg](https://github.com/user-attachments/assets/fe77ddb4-b2f0-4230-b959-d64cd63d3595)
