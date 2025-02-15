<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nouvelle-France : Aventure Abénakise</title>
    <style>
        body { 
            font-family: 'Old Standard TT', serif;
            text-align: center; 
            background: url('background.jpg') no-repeat center center fixed;
            background-size: cover;
            color: #3e2f1b;
            margin: 0;
            padding: 0;
        }
        #game { 
            width: 80%; 
            max-width: 800px;
            margin: 20px auto; 
            padding: 20px; 
            background: rgba(244, 225, 210, 0.9); 
            border-radius: 10px; 
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
            border: 3px solid #8c5a3a;
        }
        button { 
            margin: 10px; 
            padding: 12px 24px; 
            font-size: 18px; 
            cursor: pointer; 
            background-color: #6f4229; 
            color: white; 
            border: none; 
            border-radius: 5px;
            transition: 0.3s;
        }
        button:hover {
            background-color: #4b2e2e;
            transform: scale(1.05);
        }
        img { 
            max-width: 100%; 
            border-radius: 10px; 
            margin-top: 10px; 
            border: 2px solid #3e2f1b;
        }
        h1 {
            font-family: 'Cinzel', serif;
            font-size: 2.5em;
            color: #4b2e2e;
        }
        p {
            font-size: 1.2em;
            line-height: 1.6;
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Old+Standard+TT&family=Cinzel&display=swap" rel="stylesheet">
</head>
<body>
    <div id="game">
        <h1>Bienvenue dans votre aventure en Nouvelle-France</h1>
        <p>Vous incarnez Jacques Dumont, un explorateur français en l’an 1700, en mission pour découvrir un village abénaquis.</p>
        <button onclick="startGame()">Commencer l'aventure</button>
    </div>

    <script>
        function startGame() {
            document.getElementById("game").innerHTML = `
                <h1>Bienvenue, Jacques Dumont !</h1>
                <p id="story">Après plusieurs jours de marche à travers la forêt dense, vous apercevez enfin les habitations du village abénaquis. Une fumée s’élève des foyers et des voix résonnent au loin.</p>
                <img id="scene" src="village_abenakis.jpg" alt="Village Abénaquis">
                <div id="choices"></div>
            `;
            addChoices([
                { text: "Entrer dans le village", action: "entrer_village" },
                { text: "Observer discrètement", action: "observer_cache" }
            ]);
        }

        function addChoices(choices) {
            let choicesDiv = document.getElementById("choices");
            choicesDiv.innerHTML = "";
            choices.forEach(choice => {
                let button = document.createElement("button");
                button.textContent = choice.text;
                button.onclick = () => choix(choice.action);
                choicesDiv.appendChild(button);
            });
        }

        function choix(action) {
            let story = document.getElementById("story");
            let scene = document.getElementById("scene");
            
            const scenarios = {
                "entrer_village": {
                    text: `Un guerrier abénaquis vous aperçoit. "Qui es-tu, étranger ?" demande-t-il, la main sur son tomahawk.`,
                    img: "scene_accueil.jpg",
                    choices: [
                        { text: "Répondre avec respect", action: "repondre_amicalement" },
                        { text: "Rester silencieux", action: "rester_silencieux" }
                    ]
                },
                "repondre_amicalement": {
                    text: `"Je suis Jacques Dumont, un voyageur venu en paix," répondez-vous calmement. Le guerrier, après un instant d'observation, hoche la tête et vous conduit auprès du chef du village.`,
                    img: "scene_chef.jpg",
                    choices: [
                        { text: "Écouter le chef", action: "ecouter_chef" }
                    ]
                },
                "ecouter_chef": {
                    text: `Le chef se présente : "Je suis Atohi, leader de ce village. Nous vivons en harmonie avec la nature et nos ancêtres nous guident dans nos décisions." Il vous propose une visite du village, expliquant l'importance de chaque lieu.`,
                    img: "village_abenakis.jpg",
                    choices: [
                        { text: "Explorer le marché", action: "aller_marche" },
                        { text: "Visiter les artisans", action: "visiter_forge" }
                    ]
                },
                "aller_marche": {
                    text: `Vous découvrez un marché vibrant où les habitants échangent du poisson, des peaux et des outils. Un ancien vous raconte des histoires sur les échanges avec les colons.`,
                    img: "scene_marche.jpg",
                    choices: [
                        { text: "Retourner voir le chef", action: "retourner_chef" }
                    ]
                },
                "visiter_forge": {
                    text: `Un artisan vous montre la fabrication d'outils et d'armes à partir de métal et de bois. Il vous explique comment leur savoir-faire est transmis de génération en génération.`,
                    img: "scene_forge.jpg",
                    choices: [
                        { text: "Retourner voir le chef", action: "retourner_chef" }
                    ]
                },
                "retourner_chef": {
                    text: `De retour auprès du chef Atohi, il vous demande : "Jacques Dumont, que penses-tu de notre mode de vie et de notre peuple ?"`,
                    img: "scene_chef.jpg",
                    choices: [
                        { text: "Répondre avec admiration", action: "fin_positive" },
                        { text: "Donner des conseils", action: "fin_conseils" }
                    ]
                },
                "fin_positive": {
                    text: `"Votre culture est fascinante et mérite d'être protégée. Vos traditions et votre sagesse sont une richesse immense." Le chef Atohi sourit et vous invite à partager un repas avec eux.`,
                    img: "scene_fin.jpg",
                    choices: []
                },
                "fin_conseils": {
                    text: `"Vos techniques sont impressionnantes, mais peut-être pourriez-vous apprendre quelques méthodes européennes pour améliorer votre quotidien ?" Le chef Atohi écoute attentivement, son regard empli de réflexion.`,
                    img: "scene_fin.jpg",
                    choices: []
                },
                "observer_cache": {
                    text: `Vous décidez de rester caché dans les buissons pour observer le village sans être vu. Vous remarquez des enfants qui jouent près d'une rivière, des femmes qui tissent des paniers, et des hommes qui préparent des outils de chasse. Soudain, vous entendez des pas derrière vous...`,
                    img: "scene_cache.jpg",
                    choices: [
                        { text: "Rester immobile", action: "rester_immobile" },
                        { text: "Fuir rapidement", action: "fuir_cache" }
                    ]
                },
                "rester_immobile": {
                    text: `Vous restez immobile, retenant votre souffle. Un jeune garçon abénaquis passe près de vous, mais il ne vous voit pas. Il semble chercher quelque chose dans les buissons. Vous réalisez qu'il a perdu un objet précieux.`,
                    img: "scene_garçon.jpg",
                    choices: [
                        { text: "L'aider à chercher", action: "aider_garçon" },
                        { text: "Rester caché", action: "rester_cache_2" }
                    ]
                },
                "aider_garçon": {
                    text: `Vous sortez de votre cachette et dites doucement : "Je peux t'aider ?" Le garçon sursaute, mais voyant que vous êtes amical, il accepte votre aide. Vous trouvez ensemble un collier de perles qu'il avait perdu. Il vous sourit et vous invite à le suivre au village.`,
                    img: "scene_collier.jpg",
                    choices: [
                        { text: "Suivre le garçon", action: "suivre_garçon" }
                    ]
                },
                "suivre_garçon": {
                    text: `Le garçon vous conduit au village et vous présente à sa famille. Ils vous accueillent avec curiosité et bienveillance. Vous apprenez que le collier que vous avez aidé à retrouver est un héritage familial.`,
                    img: "village_abenakis.jpg",
                    choices: [
                        { text: "Discuter avec la famille", action: "discuter_famille" }
                    ]
                },
                "discuter_famille": {
                    text: `La famille vous raconte des histoires sur leur mode de vie, leurs traditions et leurs croyances. Vous réalisez à quel point leur culture est riche et complexe. Ils vous offrent même un repas traditionnel en signe de gratitude.`,
                    img: "scene_repas.jpg",
                    choices: [
                        { text: "Accepter leur hospitalité", action: "fin_positive" },
                        { text: "Leur donner un conseil", action: "fin_conseils" }
                    ]
                },
                "rester_cache_2": {
                    text: `Vous restez caché, observant le garçon qui finit par abandonner sa recherche et retourner au village. Vous décidez de continuer à explorer les alentours, mais vous tombez sur un piège à animaux. Vous êtes maintenant coincé...`,
                    img: "scene_piège.jpg",
                    choices: [
                        { text: "Appeler à l'aide", action: "appeler_aide" },
                        { text: "Essayer de se libérer seul", action: "se_liberer" }
                    ]
                },
                "appeler_aide": {
                    text: `Vous appelez à l'aide, et un groupe de chasseurs abénaquis vous trouve. Ils vous libèrent et vous interrogent sur votre présence. Vous expliquez votre mission, et ils décident de vous emmener au village pour en parler au chef.`,
                    img: "scene_chasseurs.jpg",
                    choices: [
                        { text: "Suivre les chasseurs", action: "ecouter_chef" }
                    ]
                },
                "se_liberer": {
                    text: `Vous parvenez à vous libérer du piège, mais vous vous blessez légèrement. Vous décidez de retourner à votre campement pour soigner votre blessure, mais vous gardez en tête ce que vous avez observé du village abénaquis.`,
                    img: "scene_blessure.jpg",
                    choices: [
                        { text: "Retourner au village plus tard", action: "retourner_village" }
                    ]
                },
                "retourner_village": {
                    text: `Après avoir soigné votre blessure, vous retournez au village avec des cadeaux pour montrer vos bonnes intentions. Les Abénaquis vous accueillent chaleureusement, et vous commencez à établir des liens avec eux.`,
                    img: "village_abenakis.jpg",
                    choices: [
                        { text: "Échanger des connaissances", action: "fin_positive" }
                    ]
                },
                "fuir_cache": {
                    text: `Vous décidez de fuir rapidement, mais dans votre précipitation, vous trébuchez et faites du bruit. Un groupe de guerriers abénaquis vous retrouve et vous encercle, méfiants.`,
                    img: "scene_guerriers.jpg",
                    choices: [
                        { text: "Expliquer votre présence", action: "expliquer_presence" },
                        { text: "Tenter de fuir à nouveau", action: "fuir_encore" }
                    ]
                },
                "expliquer_presence": {
                    text: `Vous expliquez calmement que vous êtes un explorateur venu en paix. Les guerriers, bien que méfiants, décident de vous emmener au chef du village pour qu'il décide de votre sort.`,
                    img: "scene_chef.jpg",
                    choices: [
                        { text: "Parler au chef", action: "ecouter_chef" }
                    ]
                },
                "fuir_encore": {
                    text: `Vous tentez de fuir à nouveau, mais les guerriers sont plus rapides. Ils vous capturent et vous emmènent au village, où vous êtes présenté au chef.`,
                    img: "scene_capture.jpg",
                    choices: [
                        { text: "Expliquer votre mission", action: "ecouter_chef" }
                    ]
                }
            };
            
            if (scenarios[action]) {
                story.innerHTML = scenarios[action].text;
                scene.src = scenarios[action].img;
                addChoices(scenarios[action].choices);
            }
        }
    </script>
</body>
</html>
