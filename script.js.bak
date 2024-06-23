document.addEventListener("DOMContentLoaded", () => {
    const commandInput = document.getElementById("commandInput");
    const outputDiv = document.getElementById("output");
    const nameDiv = document.getElementById("name");

    const commands = {
        help: "Liste des commandes disponibles :\n\n\nhelp             Affiche toutes les commandes possibles\nwhois            Qui suis-je ?\ndate             Affiche la date\nclear            Efface toutes les commandes du terminal actuel\ngithub           Lien vers mon github",
        whois: "Je m'appelle Sacha Besser, j'ai 18 ans et je suis étudiant passionné par la cybersécurité.\nAspirant à devenir pentester, j'ai plongé dans le monde fascinant des réseaux, des systèmes et du codage.\nMon parcours est un mélange d'apprentissage autodidacte et de formation académique, avec une préférence marquée pour les défis de la sécurité informatique.\nJ'adore explorer les failles potentielles des systèmes pour les renforcer, et je passe souvent mon temps libre à expérimenter avec divers outils de sécurité et à coder des solutions innovantes.\nMon objectif est de transformer cette passion en une carrière, en aidant les entreprises à protéger leurs données et à sécuriser leurs infrastructures contre les cybermenaces.\n\n",
        date: () => new Date().toString(),
        clear: () => {
            outputDiv.innerHTML = "";
            return "";
        },
        macron: () => {
            window.open("https://macron.fun", "_blank");
            return ""; // Retourne une chaîne vide pour ne pas afficher de sortie dans le terminal
        },
        secret: "aXAgOiA5Ny4xNTMuMjUuNzg=",
        github: () => {
            window.open("https://github.com/BeletteALongueQueue", "_blank");
            return ""; // Retourne une chaîne vide pour ne pas afficher de sortie dans le terminal
        },
        ping: (ip) => {
            return new Promise((resolve) => {
                let count = 0;
                const maxCount = 4;
                const interval = 1000;
                const pingText = `PING ${ip} (97.153.25.78) 56(84) bytes of data.\n`;
                const pingResponse = `64 bytes from ${ip}: icmp_seq=1 ttl=64 time=0.026 ms\n`;

                const commandOutputDiv = document.createElement("div");
                commandOutputDiv.innerHTML = `<div><span class="prompt">┌──(<span class="username">sacha㉿DESKTOP-07ZXXUP</span>)-[~]</span><br><span class="prompt2">└─$</span> ping ${ip}</div>`;
                outputDiv.appendChild(commandOutputDiv);

                const pingDiv = document.createElement("div");
                pingDiv.classList.add("ping-animation");
                commandOutputDiv.appendChild(pingDiv);

                const printPingLine = () => {
                    if (count >= maxCount) {
                        pingDiv.innerHTML += `--- ${ip} ping statistics ---\n${maxCount} packets transmitted, ${maxCount} received, 0% packet loss, time ${maxCount * interval}ms\n`;
                        resolve(); // Résoudre la promesse une fois terminé
                        outputDiv.scrollTop = outputDiv.scrollHeight; // Fait défiler automatiquement vers le bas
                        return;
                    }
                    pingDiv.innerHTML += count === 0 ? pingText : pingResponse.replace("icmp_seq=1", `icmp_seq=${count}`);
                    count++;
                    outputDiv.scrollTop = outputDiv.scrollHeight; // Fait défiler automatiquement vers le bas
                    setTimeout(printPingLine, interval);
                };

                printPingLine();
            });
        },
    };

    // Fonction pour afficher du texte progressivement
    const displayProgressiveText = (element, text, interval) => {
        let index = 0;
        const printText = () => {
            if (index < text.length) {
                element.innerHTML += text[index] === '\n' ? '<br>' : text[index];
                index++;
                outputDiv.scrollTop = outputDiv.scrollHeight; // Fait défiler automatiquement vers le bas
                setTimeout(printText, interval); // Appel récursif avec l'intervalle donné
            } else {
                // Focus sur le champ de saisie après l'animation
                commandInput.focus();
            }
        };

        printText(); // Démarrer l'affichage progressif
    };

    // Générer l'ASCII art
    const asciiArt = `
  ____                   _                 ____                                   
 / ___|    __ _    ___  | |__     __ _    | __ )    ___   ___   ___    ___   _ __ 
 \\___ \\   / _\` |  / __| | '_ \\   / _\` |   |  _ \\   / _ \\ / __| / __|  / _ \\ | '__|
  ___) | | (_| | | (__  | | | | | (_| |   | |_) | |  __/ \\__ \\ \\__ \\ |  __/ | |   
 |____/   \\__,_|  \\___| |_| |_|  \\__,_|   |____/   \\___| |___/ |___/  \\___| |_|   
`;

    // Appel de la fonction pour afficher l'ASCII art progressivement
    displayProgressiveText(nameDiv, asciiArt, 5); // 50 est l'intervalle en millisecondes entre chaque caractère

    // Afficher le texte de la commande help après l'ASCII art
    setTimeout(() => {
        displayProgressiveText(outputDiv, commands.help, 20); // 20 est l'intervalle en millisecondes entre chaque caractère
    }, asciiArt.length * 7 + 1000); // Délai après l'ASCII art (plus 1000 millisecondes)

    // Focus sur le champ de saisie au chargement de la page
    commandInput.focus();

    // Fonction pour afficher un achievement
    const displayAchievement = (id) => {
        const achievement = document.getElementById(id);
        achievement.style.display = "flex";

        // Masquer l'achievement après 5 secondes
        setTimeout(() => {
            achievement.style.display = "none";
        }, 5000);
    };

    commandInput.addEventListener("keydown", async (event) => {
        if (event.key === "Enter") {
            const input = commandInput.value;
            commandInput.value = "";
            if (input.startsWith("<script>")) {
                outputDiv.innerHTML += `<div><span class="prompt">┌──(<span class="username">sacha㉿DESKTOP-07ZXXUP</span>)-[~]</span><br><span class="prompt2">└─$</span> ${input}</div><div>Pas de faille XSS sur ce site, jeune hacker !<br>arrête...<br>c'est pas très gentil<br>prend quand même ça, ça pourrait servir --> <span id="cookie">🍪</span></div>`;

                document.getElementById("cookie").addEventListener("click", () => {
                    // Définir le cookie
                    document.cookie = "Cookie=Tu devrais saisir la commande secret !";
                    // Afficher le cookie dans la console
                    console.log("Voici ton cookie spécial: ", document.cookie);

                    // Afficher l'achievement
                    displayAchievement("achievement");
                });

            } else {
                const [command, ...args] = input.split(" ");
                if (commands[command]) {
                    const output = typeof commands[command] === "function" ? await commands[command](...args) : commands[command];
                    if (output) {
                        const commandOutputDiv = document.createElement("div");
                        commandOutputDiv.innerHTML = `<div><span class="prompt">┌──(<span class="username">sacha㉿DESKTOP-07ZXXUP</span>)-[~]</span><br><span class="prompt2">└─$</span> ${input}</div><div>${output}</div>`;
                        outputDiv.appendChild(commandOutputDiv);
                        outputDiv.scrollTop = outputDiv.scrollHeight;
                    }
                } else {
                    const commandOutputDiv = document.createElement("div");
                    commandOutputDiv.innerHTML = `<div><span class="prompt">┌──(<span class="username">sacha㉿DESKTOP-07ZXXUP</span>)-[~]</span><br><span class="prompt2">└─$</span> ${input}</div><div>Commande non trouvée : ${input}</div>`;
                    outputDiv.appendChild(commandOutputDiv);
                    outputDiv.scrollTop = outputDiv.scrollHeight;
                }
            }
        }
    });
});
