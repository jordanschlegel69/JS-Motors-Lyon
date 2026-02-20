<![logo jpg](https://github.com/user-attachments/assets/13571658-0a73-445a-8659-cbf08c772c5f)
!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JS Motors Lyon - Gestion</title>
    
    <link rel="icon" type="image/jpeg" href="logo.jpg">
    <link rel="apple-touch-icon" href="logo.jpg">

    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 600px; margin: auto; }
        
        /* En-tête avec ton logo */
        .header { background: #ffffff; padding: 15px; border-radius: 20px; text-align: center; margin-bottom: 20px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); border: 1px solid #ddd; }
        .header img { max-width: 100%; height: auto; border-radius: 10px; }
        
        /* Sections et Formulaires */
        .section-title { color: #1a1a1a; font-size: 18px; margin: 20px 0 10px 0; border-left: 5px solid #b22222; padding-left: 12px; font-weight: bold; text-transform: uppercase; }
        .form-group { background: white; padding: 20px; border-radius: 15px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); }
        
        label { font-size: 12px; font-weight: bold; color: #666; text-transform: uppercase; display: block; margin-top: 10px; }
        input { width: 100%; padding: 12px; margin: 5px 0 15px 0; border: 1px solid #ccc; border-radius: 8px; box-sizing: border-box; font-size: 16px; background: #f9f9f9; }
        input:focus { border-color: #b22222; outline: none; background: #fff; }
        
        button.main-btn { background: #1a1a1a; color: white; border: none; padding: 18px; width: 100%; border-radius: 10px; font-weight: bold; font-size: 16px; cursor: pointer; transition: 0.3s; margin-top: 10px; }
        button.main-btn:active { transform: scale(0.98); background: #333; }
        
        /* Cartes Dossier OR */
        .or-card { background: white; padding: 15px; margin-top: 12px; border-radius: 15px; border-left: 8px solid #b22222; box-shadow: 0 3px 6px rgba(0,0,0,0.08); }
        .or-header { display: flex; justify-content: space-between; align-items: center; cursor: pointer; }
        .or-header strong { font-size: 17px; color: #1a1a1a; }
        
        .status-badge { background: #b22222; color: white; padding: 4px 10px; border-radius: 20px; font-size: 11px; font-weight: bold; }
        
        .details { display: none; margin-top: 15px; padding-top: 15px; border-top: 1px solid #eee; font-size: 14px; color: #333; line-height: 1.6; }
        .details b { color: #000; }
        
        .info-block { background: #f8f9fa; padding: 10px; border-radius: 8px; margin-bottom: 10px; }
        
        .btn-red { background: #ffeded; color: #d63031; border: 1px solid #ffcccc; padding: 10px; width: 100%; border-radius: 8px; font-weight: bold; margin-top: 15px; cursor: pointer; }
        
        hr { border: 0; border-top: 1px solid #eee; margin: 20px 0; }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <img src="logo.jpg" alt="JS MOTORS LYON">
    </div>

    <div class="form-group">
        <div class="section-title">Nouvel Ordre de Réparation</div>
        
        <label>Informations Client</label>
        <input type="text" id="nom" placeholder="Nom & Prénom">
        <input type="tel" id="tel" placeholder="N° de téléphone">
        <input type="email" id="email" placeholder="Adresse Email">
        <input type="text" id="adresse" placeholder="Adresse postale">
        
        <hr>
        
        <label>Informations Véhicule</label>
        <input type="text" id="marque" placeholder="Marque & Modèle (ex: Renault Master)">
        <input type="text" id="km" placeholder="Kilométrage actuel">
        <input type="text" id="panne" placeholder="Description des travaux">
        
        <button class="main-btn" onclick="creerOR()">CRÉER LE DOSSIER OR</button>
    </div>

    <div class="section-title">Dossiers en cours</div>
    <div id="listeOR"></div>
</div>

<script>
    // Chargement des dossiers sauvegardés
    window.onload = function() {
        const savedData = localStorage.getItem('jsMotorsStorage');
        if (savedData) {
            document.getElementById('listeOR').innerHTML = savedData;
        }
    };

    function sauvegarder() {
        const contenu = document.getElementById('listeOR').innerHTML;
        localStorage.setItem('jsMotorsStorage', contenu);
    }

    function creerOR() {
        const fields = ['nom', 'tel', 'email', 'adresse', 'marque', 'km', 'panne'];
        const v = {};
        fields.forEach(f => v[f] = document.getElementById(f).value);

        if(!v.nom || !v.marque) {
            alert("Merci de remplir au moins le nom du client et le modèle du véhicule.");
            return;
        }

        const orId = "OR-" + Math.floor(1000 + Math.random() * 9000);
        const liste = document.getElementById('listeOR');
        
        const card = document.createElement('div');
        card.className = 'or-card';
        card.innerHTML = `
            <div class="or-header" onclick="toggleDetails(this)">
                <div>
                    <strong>${orId} : ${v.marque}</strong><br>
                    <small style="color:#666">${v.nom}</small>
                </div>
                <span class="status-badge">OUVERT</span>
            </div>
            <div class="details">
                <div class="info-block">
                    <b>👤 CLIENT</b><br>
                    ${v.nom}<br>
                    📞 ${v.tel}<br>
                    📧 ${v.email}<br>
                    🏠 ${v.adresse}
                </div>
                
                <div class="info-block">
                    <b>🚗 VÉHICULE</b><br>
                    Modèle: ${v.marque}<br>
                    KM: ${v.km} km<br>
                    🛠️ Travaux: ${v.panne}
                </div>
                
                <button class="btn-red" onclick="supprimer(this)">SUPPRIMER LE DOSSIER</button>
            </div>
        `;

        liste.prepend(card);
        
        // Vider le formulaire
        fields.forEach(f => document.getElementById(f).value = '');
        sauvegarder();
    }

    function toggleDetails(header) {
        const details = header.nextElementSibling;
        details.style.display = (details.style.display === 'block') ? 'none' : 'block';
    }

    function supprimer(btn) {
        if(confirm("Voulez-vous vraiment supprimer ce dossier de réparation ?")) {
            btn.closest('.or-card').remove();
            sauvegarder();
        }
    }
</script>

</body>
</html>
