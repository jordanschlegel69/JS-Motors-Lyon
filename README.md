<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>JS Motors Lyon</title>
    
    <link rel="icon" type="image/jpeg" href="https://github.com/user-attachments/assets/5bae5cb6-c434-49aa-842e-1a5be52f0df5">
    <link rel="apple-touch-icon" href="https://github.com/user-attachments/assets/5bae5cb6-c434-49aa-842e-1a5be52f0df5">

    <style>
        body { font-family: 'Segoe UI', Helvetica, Arial, sans-serif; background: #f0f2f5; margin: 0; padding: 10px; color: #333; }
        .container { max-width: 500px; margin: auto; }
        
        /* En-tête avec ton logo */
        .header { background: white; padding: 15px; border-radius: 20px; text-align: center; margin-bottom: 20px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
        .header img { width: 100%; max-width: 350px; height: auto; display: block; margin: 0 auto; }
        
        /* Formulaire */
        .form-group { background: white; padding: 20px; border-radius: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.05); }
        .section-title { color: #b22222; font-size: 16px; font-weight: bold; margin: 20px 0 10px 5px; text-transform: uppercase; display: flex; align-items: center; }
        .section-title::before { content: ""; width: 4px; height: 18px; background: #b22222; margin-right: 10px; border-radius: 2px; }
        
        label { font-size: 11px; font-weight: bold; color: #888; margin-left: 5px; text-transform: uppercase; }
        input { width: 100%; padding: 14px; margin: 5px 0 15px 0; border: 1px solid #ddd; border-radius: 12px; box-sizing: border-box; font-size: 16px; background: #fafafa; }
        input:focus { border-color: #b22222; outline: none; background: #fff; }
        
        .main-btn { background: #1a1a1a; color: white; border: none; padding: 18px; width: 100%; border-radius: 15px; font-weight: bold; font-size: 16px; cursor: pointer; margin-top: 10px; box-shadow: 0 4px 10px rgba(0,0,0,0.2); }
        
        /* Liste des Dossiers */
        .or-card { background: white; padding: 15px; margin-top: 12px; border-radius: 18px; border-left: 6px solid #b22222; box-shadow: 0 3px 10px rgba(0,0,0,0.05); }
        .or-header { display: flex; justify-content: space-between; align-items: center; cursor: pointer; }
        .or-header strong { font-size: 18px; color: #000; }
        
        .details { display: none; margin-top: 15px; padding-top: 15px; border-top: 1px solid #eee; }
        .info-block { background: #f9f9f9; padding: 12px; border-radius: 12px; margin-bottom: 10px; border: 1px solid #f0f0f0; line-height: 1.6; font-size: 14px; }
        .info-block b { color: #b22222; }
        
        .btn-delete { background: #fff5f5; color: #e03131; border: 1px solid #ffc9c9; padding: 12px; width: 100%; border-radius: 10px; font-weight: bold; margin-top: 10px; cursor: pointer; }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <img src="https://github.com/user-attachments/assets/5bae5cb6-c434-49aa-842e-1a5be52f0df5" alt="JS MOTORS LYON">
    </div>

    <div class="form-group">
        <div class="section-title">Nouvel Ordre de Réparation</div>
        
        <label>👤 Client</label>
        <input type="text" id="nom" placeholder="Nom & Prénom">
        <input type="tel" id="tel" placeholder="Téléphone">
        <input type="email" id="email" placeholder="Email">
        <input type="text" id="adresse" placeholder="Adresse postale">
        
        <label>🚗 Véhicule</label>
        <input type="text" id="marque" placeholder="Marque & Modèle">
        <input type="number" id="km" placeholder="Kilométrage">
        <input type="text" id="panne" placeholder="Travaux à effectuer">
        
        <button class="main-btn" onclick="creerOR()">CRÉER LE DOSSIER</button>
    </div>

    <div class="section-title">Dossiers en cours</div>
    <div id="listeOR"></div>
</div>

<script>
    // Chargement auto
    window.onload = function() {
        const data = localStorage.getItem('jsMotorsFinal');
        if (data) document.getElementById('listeOR').innerHTML = data;
    };

    function save() {
        localStorage.setItem('jsMotorsFinal', document.getElementById('listeOR').innerHTML);
    }

    function creerOR() {
        const fields = ['nom', 'tel', 'email', 'adresse', 'marque', 'km', 'panne'];
        const v = {};
        fields.forEach(f => v[f] = document.getElementById(f).value);

        if(!v.nom || !v.marque) return alert("Remplir au moins le Nom et le Véhicule");

        const id = "OR-" + Math.floor(1000 + Math.random() * 9000);
        const card = document.createElement('div');
        card.className = 'or-card';
        card.innerHTML = `
            <div class="or-header" onclick="this.nextElementSibling.style.display = (this.nextElementSibling.style.display === 'block') ? 'none' : 'block'">
                <div><strong>${id}</strong><br><small>${v.marque}</small></div>
                <div style="font-size:11px; font-weight:bold; color:#b22222;">OUVERT</div>
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
                    Modèle : ${v.marque}<br>
                    KM : ${v.km} km<br>
                    🛠️ Travaux : ${v.panne}
                </div>
                <button class="btn-delete" onclick="if(confirm('Supprimer ce dossier ?')){this.closest('.or-card').remove(); save();}">SUPPRIMER LE DOSSIER</button>
            </div>
        `;

        document.getElementById('listeOR').prepend(card);
        fields.forEach(f => document.getElementById(f).value = '');
        save();
    }
</script>

</body>
</html>
