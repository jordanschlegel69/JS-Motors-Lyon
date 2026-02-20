# JS-Motors-Lyon<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JS Motors Lyon - Gestion</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; background: #f0f2f5; margin: 0; padding: 15px; }
        .header { background: #000; color: white; padding: 20px; border-radius: 15px; text-align: center; margin-bottom: 20px; }
        .logo-text { font-size: 24px; font-weight: bold; color: #fff; text-transform: uppercase; }
        
        .section-title { color: #2c3e50; font-size: 18px; margin-bottom: 10px; border-left: 4px solid #000; padding-left: 10px; }
        
        .form-group { background: white; padding: 15px; border-radius: 15px; margin-bottom: 20px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        input { width: 100%; padding: 10px; margin: 5px 0; border: 1px solid #ddd; border-radius: 8px; box-sizing: border-box; font-size: 14px; }
        
        button.main-btn { background: #000; color: white; border: none; padding: 15px; width: 100%; border-radius: 8px; font-weight: bold; margin-top: 10px; }
        
        .or-card { background: white; padding: 15px; margin-top: 10px; border-radius: 12px; border-left: 6px solid #e67e22; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
        .or-header { display: flex; justify-content: space-between; align-items: center; cursor: pointer; }
        
        .details { display: none; margin-top: 15px; padding-top: 15px; border-top: 1px dashed #ccc; font-size: 14px; line-height: 1.6; }
        .details b { color: #555; }
        
        .status-badge { background: #e67e22; color: white; padding: 2px 8px; border-radius: 5px; font-size: 12px; }
        .btn-red { background: #c0392b; color: white; border: none; padding: 5px 10px; border-radius: 5px; margin-top: 10px; }
    </style>
</head>
<body>

<div class="header">
    <div class="logo-text">JS MOTORS LYON</div>
    <div style="font-size: 12px; opacity: 0.8;">CARS & TRUCKS</div>
</div>

<div class="form-group">
    <div class="section-title">Nouvel Ordre de Réparation (OR)</div>
    
    <small><b>CLIENT :</b></small>
    <input type="text" id="nom" placeholder="Nom & Prénom">
    <input type="tel" id="tel" placeholder="Téléphone">
    <input type="email" id="email" placeholder="Email">
    <input type="text" id="adresse" placeholder="Adresse postale">
    
    <hr>
    <small><b>VÉHICULE :</b></small>
    <input type="text" id="marque" placeholder="Marque & Modèle">
    <input type="number" id="km" placeholder="Kilométrage">
    <input type="text" id="panne" placeholder="Travaux / Panne">
    
    <button class="main-btn" onclick="creerOR()">Créer le dossier</button>
</div>

<div class="section-title">Dossiers en cours</div>
<div id="listeOR"></div>

<script>
    window.onload = function() {
        const data = localStorage.getItem('jsMotorsData');
        if (data) document.getElementById('listeOR').innerHTML = data;
    };

    function sauvegarder() {
        localStorage.setItem('jsMotorsData', document.getElementById('listeOR').innerHTML);
    }

    function creerOR() {
        const fields = ['nom', 'tel', 'email', 'adresse', 'marque', 'km', 'panne'];
        const values = {};
        fields.forEach(f => values[f] = document.getElementById(f).value);

        if(!values.nom || !values.marque) return alert("Veuillez remplir au moins le nom et le véhicule");

        const orId = "OR-" + Math.floor(Math.random() * 10000);
        const liste = document.getElementById('listeOR');
        
        const card = document.createElement('div');
        card.className = 'or-card';
        card.innerHTML = `
            <div class="or-header" onclick="toggleDetails(this)">
                <div>
                    <strong>${orId} : ${values.marque}</strong><br>
                    <small>${values.nom}</small>
                </div>
                <span class="status-badge">En attente</span>
            </div>
            <div class="details">
                <p><b>📍 Client :</b> ${values.nom}<br>
                <b>📞 Tél :</b> ${values.tel}<br>
                <b>📧 Email :</b> ${values.email}<br>
                <b>🏠 Adresse :</b> ${values.adresse}</p>
                
                <p><b>🚗 Véhicule :</b> ${values.marque}<br>
                <b>🛣️ KM :</b> ${values.km} km<br>
                <b>🛠️ Panne :</b> ${values.panne}</p>
                
                <button class="btn-red" onclick="supprimer(this)">Supprimer le dossier</button>
            </div>
        `;

        liste.prepend(card);
        fields.forEach(f => document.getElementById(f).value = '');
        sauvegarder();
    }

    function toggleDetails(header) {
        const details = header.nextElementSibling;
        details.style.display = (details.style.display === 'block') ? 'none' : 'block';
    }

    function supprimer(btn) {
        if(confirm("Confirmer la suppression du dossier ?")) {
            btn.closest('.or-card').remove();
            sauvegarder();
        }
    }
</script>

</body>
</html>
