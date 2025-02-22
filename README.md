<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulaire d'inscription - AFECI MarketPlace</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            text-align: center;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 90%;
            max-width: 600px;
            margin: 50px auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.2);
        }
        img {
            width: 100px;
            margin-bottom: 20px;
        }
        h2 {
            color: #004080;
            margin-bottom: 20px;
        }
        form {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        input, select {
            width: 100%;
            max-width: 500px;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
            border: 1px solid #ccc;
            font-size: 16px;
        }
        input:focus, select:focus {
            border-color: #004080;
            outline: none;
            box-shadow: 0 0 5px rgba(0, 64, 128, 0.5);
        }
        button {
            background-color: #004080;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 10px;
        }
        button:hover {
            background-color: #002060;
        }
        #autreCompetence {
            display: none;
        }
        .error {
            color: red;
            font-size: 14px;
            margin-top: -5px;
            margin-bottom: 10px;
            display: none;
        }
    </style>
</head>
<body>

    <div class="container">
        <img src="logo_afeci.jpg" alt="AFECI LOGO"> <!-- Remplacez par le chemin correct de votre logo -->
        <h2>Formulaire d'inscription - AFECI MarketPlace</h2>

        <form id="afeciForm" onsubmit="return envoyerWhatsApp(event)">
            <input type="text" id="nom" placeholder="Nom & Prénoms" required>
            <span id="nomError" class="error">Veuillez entrer votre nom et prénoms.</span>

            <input type="tel" id="whatsapp" placeholder="Numéro WhatsApp" required pattern="[0-9]+" title="Entrez un numéro valide">
            <span id="whatsappError" class="error">Veuillez entrer un numéro WhatsApp valide.</span>

            <select id="competence" required onchange="afficherChampAutre()">
                <option value="">Sélectionnez votre compétence</option>
                <option value="Développement Web">Développement Web</option>
                <option value="Développement Mobile">Développement Mobile</option>
                <option value="UI/UX Design">UI/UX Design</option>
                <option value="Marketing Digital">Marketing Digital</option>
                <option value="Gestion de projet">Gestion de projet</option>
                <option value="Autre">Autre</option>
            </select>
            <span id="competenceError" class="error">Veuillez sélectionner une compétence.</span>

            <input type="text" id="autreCompetence" placeholder="Précisez votre compétence">
            <span id="autreCompetenceError" class="error">Veuillez préciser votre compétence.</span>

            <button type="submit">Envoyer l'inscription</button>
        </form>
    </div>

    <script>
        function afficherChampAutre() {
            const competence = document.getElementById("competence").value;
            const autreCompetence = document.getElementById("autreCompetence");

            if (competence === "Autre") {
                autreCompetence.style.display = "block";
                autreCompetence.setAttribute("required", "true");
            } else {
                autreCompetence.style.display = "none";
                autreCompetence.removeAttribute("required");
                autreCompetence.value = "";
            }
        }

        function envoyerWhatsApp(event) {
            event.preventDefault(); // Empêche le rechargement de la page

            // Récupération des valeurs
            const nom = document.getElementById("nom").value.trim();
            const whatsapp = document.getElementById("whatsapp").value.trim();
            const competence = document.getElementById("competence").value;
            const autreCompetence = document.getElementById("autreCompetence").value.trim();

            // Réinitialisation des messages d'erreur
            document.getElementById("nomError").style.display = "none";
            document.getElementById("whatsappError").style.display = "none";
            document.getElementById("competenceError").style.display = "none";
            document.getElementById("autreCompetenceError").style.display = "none";

            // Validation des champs
            let isValid = true;

            if (nom === "") {
                document.getElementById("nomError").style.display = "block";
                isValid = false;
            }
            if (whatsapp === "" || !/^[0-9]+$/.test(whatsapp)) {
                document.getElementById("whatsappError").style.display = "block";
                isValid = false;
            }
            if (competence === "") {
                document.getElementById("competenceError").style.display = "block";
                isValid = false;
            }
            if (competence === "Autre" && autreCompetence === "") {
                document.getElementById("autreCompetenceError").style.display = "block";
                isValid = false;
            }

            if (!isValid) return;

            // Préparation du message WhatsApp
            const competenceFinale = (competence === "Autre") ? autreCompetence : competence;
            const message = `Nouvelle inscription AFECI :%0A👤 Nom : ${nom}%0A📱 WhatsApp : ${whatsapp}%0A💼 Compétence : ${competenceFinale}`;
            const numeroWhatsApp = "2250787052416";

            // Redirection vers WhatsApp
            const lienWhatsApp = `https://wa.me/${numeroWhatsApp}?text=${message}`;
            window.location.href = lienWhatsApp;
        }
    </script>

</body>
</html>