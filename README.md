![logo jpg](https://github.com/user-attachments/assets/77664afc-ce6e-450c-865f-361bdcd34c11)
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>JS Motors Lyon</title>
    
    <link rel="icon" type="image/jpeg" href="logo.jpg">
    <link rel="apple-touch-icon" sizes="180x180" href="logo.jpg">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black">

    <style>
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background: #f4f7f6; margin: 0; padding: 10px; color: #333; }
        .container { max-width: 500px; margin: auto; }
        
        /* En-tête avec Logo Large */
        .header { background: #ffffff; padding: 20px 10px; border-radius: 20px; text-align: center; margin-bottom: 20px; box-shadow: 0 4px 15px rgba(0,0,0,0.08); }
        .header img { width: 100%; max-width: 350px; height: auto; display: block; margin: 0 auto; }
        
        /* Formulaire */
        .section-title { color: #000; font-size: 16px; margin: 25px 0 10px 5px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; display: flex; align-items: center; }
        .section-title::before { content: ""; width: 4px; height: 18px; background: #b22222; margin-right: 10px; border-radius: 2px; }
        
        .form-group { background: white; padding: 15px; border-radius: 18px; box-shadow: 0 2px 10px rgba(0,0,0,0.03); border: 1px solid #eee; }
        input { width: 100%; padding: 14px; margin: 8px 0; border: 1px solid #ddd; border-radius: 12px; box-sizing: border-box; font-size: 16px; background: #fafafa; transition: 0.2s; }
        input:focus { border-color: #b22222; background: #fff; outline: none; box-shadow: 0 0 0 3px rgba(178, 34, 34, 0.1); }
        
        button.main-btn { background: #000; color: white; border: none; padding: 18px; width: 100%; border-radius: 14px; font-weight: bold; font-size: 16px; cursor: pointer; margin-top: 15px; box-shadow: 0 4px 10px rgba(0,0,0,0.2); }
        
        /* Liste des OR */
        .or-card { background: white; padding: 18px; margin-top: 12px; border-radius: 16px; border-left: 6px solid #b22222; box-shadow: 0 3px 10px rgba(0,0,0,0.05); }
        .or-header { display: flex; justify-content: space-between; align-items: center; }
        .or-header strong { font-size: 18px; color: #000; }
        
        .status-badge { background: #fdf2f2; color: #b22222; padding: 5px 12px; border-radius: 8px; font-size: 11px; font-weight: bold; border: 1px solid #f9dcdc; }
        
        .details { display: none; margin-top: 15px; padding-top: 15px; border-top: 1px solid #f0f0f0; }
        .info-block { background: #f9f9f9; padding: 12px; border-radius: 12px; margin-bottom: 10px; border: 1px solid #f0f0f0; line-height: 1.5; }
        .info-label { font-size: 11px; color: #888; text-transform: uppercase; font-weight: bold; display: block; margin-bottom: 4px; }
        
        .btn-red { background: #fff5f5; color: #e03131; border: 1px solid #ffc9c9; padding: 12px; width: 100%; border-radius: 10px; font-weight: bold; margin-top: 10px; }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <img src="logo.jpg" alt="JS MOTORS LYON">
    </div>

    <div class="form-group">
        <div class="section-title">Nouveau Dossier</div>
        <input type="text" id="nom" placeholder="Nom du Client">
        <input type="tel" id="tel" placeholder="Téléphone">
        <input type="text" id="marque" placeholder="Véhicule (ex: Renault Master)">
        <input type="text" id="panne" placeholder="Travaux à effectuer">
        <button class="main-btn" onclick="creerOR()">CRÉER L'ORDRE DE RÉPARATION</button>
    </div>

    <div class="section-title">Réparations en cours</div>
    <div id="listeOR"></div>
</div>

<script>
    window.onload = function() {
        const saved = localStorage.getItem('jsMotorsPro');
        if (saved) document.getElementById('listeOR').innerHTML = saved;
    };

    function sauvegarder() {
        localStorage.setItem('jsMotorsPro', document.getElementById('listeOR').innerHTML);
    }

    function creerOR() {
        const fields = ['nom', 'tel', 'marque', 'panne'];
        const v = {};
        fields.forEach(f => v[f] = document.getElementById(f).value);
        if(!v.nom || !v.marque) return alert("Remplir Nom et Véhicule");

        const orId = "OR-" + Math.floor(1000 + Math.random() * 9000);
        const card = document.createElement('div');
        card.className = 'or-card';
        card.innerHTML = `
            <div class="or-header" onclick="this.nextElementSibling.style.display = (this.nextElementSibling.style.display === 'block') ? 'none' : 'block'">
                <div><strong>${orId}</strong><br><small>${v.marque}</small></div>
                <span class="status-badge">EN COURS</span>
            </div>
            <div class="details">
                <div class="info-block"><span class="info-label">Client</span><b>${v.nom}</b><br>📞 ${v.tel}</div>
                <div class="info-block"><span class="info-label">Détails Travaux</span>${v.panne}</div>
                <button class="btn-red" onclick="if(confirm('Supprimer ?')) {this.closest('.or-card').remove(); sauvegarder();}">Supprimer le dossier</button>
            </div>
        `;
        document.getElementById('listeOR').prepend(card);
        fields.forEach(f => document.getElementById(f).value = '');
        sauvegarder();
    }
</script>

</body>
</html>![logo jpg](https://github.com/user-attachments/assets/a60cf8aa-cde6-410e-b826-1e9245eaaa28)
