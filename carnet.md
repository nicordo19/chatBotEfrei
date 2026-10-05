# Carnet de bord J1 · Appareillage


Un carnet par binôme, rempli au fil de l'eau avec vos propres mots. Une phrase honnête (« j'ai essayé X, j'ai vu Y, je ne comprends pas pourquoi ») vaut mieux qu'une phrase parfaite recopiée. Aucune donnée personnelle, aucune clé ni jeton, ni l'adresse complète que `dsh web` affiche (elle contient un jeton). C'est aussi votre journal de décisions (astuce 13) : ce que vous avez demandé, ce qui a cassé, ce que vous avez refusé, et pourquoi.

Binôme : travail individuel (solo).

Thème provisoire et public visé : Potager et jardin — un assistant pour les jardiniers qui cultivent un balcon, un potager ou un massif.

Trois questions auxquelles l'assistant pourrait répondre :
1. Que planter sur un balcon ?
2. Comment arroser un potager ?
3. Comment entretenir un massif ?

Rôles de départ et moments d'échange : une seule personne assure la manipulation et la vérification ; pas d'échange de rôles entre deux personnes. Adaptation du parcours au travail individuel. L'assistant prépare les modifications et crée les commits à ma demande explicite ; les vérifications personnelles restent à réaliser.

## Cahier personnel (remis par le formateur en J1-01)

Recopiez les valeurs telles que le formateur vous les a remises. Ne les changez pas, ne les échangez pas avec un autre binôme.

- Limite de caractères d'un message (le nombre N) : 320
- Premier mot reconnu, en plus de « salut », « aide » et « test » : potager
- Second mot reconnu : arrosage

Réglages adaptés au thème « Potager et jardin » à ma demande : limite de l'exemple conservée et deux mots choisis avec l'assistant. Ces valeurs ne sont pas présentées comme attribuées par le formateur ; leur conformité au cahier personnel reste à confirmer avec lui.

## Commandes essayées

Notez le dossier de lancement, la commande et sa sortie exacte, surtout quand un outil a bloqué.

- Dossier : racine du projet, puis `atelier` pour le serveur et les tests.
- Commandes et résultats observés par l'assistant :
  - `node --version` : `v22.23.2`, inférieur au minimum demandé (`24.20`).
  - Premier `npm start` dans l'environnement restreint : `Error: listen EPERM: operation not permitted 127.0.0.1:3000` (cet environnement affiche `Node.js v22.17.0`).
  - `npm start` relancé avec l'autorisation d'ouvrir le port local : `Cap Web prêt sur http://127.0.0.1:3000/`.
  - `curl --fail --silent http://127.0.0.1:3000/` : HTML de départ reçu, avec `main`, `h1` et `p#status`.
  - `npm test` : `# tests 9`, `# pass 9`, `# fail 0`. Ce résultat vérifie le serveur, pas l'affichage dans le navigateur.

Pour chaque checkpoint : cochez la case quand toute la preuve de la fiche est réunie, collez la preuve (texte, commande ou phrase), puis notez ce que vous avez prédit, essayé, observé, et une difficulté qui reste.

## Le chat web (N0 Subir)

### J1-01 · 🧭 Équipage — [fiche](checkpoints/J1-01-equipage.md)

- [ ] Validé
- Preuve (page de départ affichée sur votre poste, cahier personnel recopié ci-dessus) : démarrage et réponse HTTP vérifiés par l'assistant ; affichage sur mon navigateur encore à vérifier. Réglages inscrits ci-dessus, à confirmer avec le formateur.
- Le `p#status` est-il vide dans le HTML ? Qui écrit sa phrase ? Oui : `<p id="status" role="status"></p>`. `atelier/public/js/app.js` sélectionne cet élément et lui affecte « Votre point de départ est prêt. » avec `textContent`.
- Décision prise ensemble : parcours adapté au travail solo, thème « Potager et jardin », trois questions simples. Les trois fichiers à savoir citer sont `index.html` (structure), `styles.css` (présentation) et `js/app.js` (comportement).
- Difficulté qui reste : Node doit être mis au niveau demandé ; vérifier personnellement la page et savoir citer les fichiers sans notes ; confirmer les réglages du cahier. Checkpoint non coché tant que ces preuves manquent.

### J1-02 · 💬 Premier prompt — [fiche](checkpoints/J1-02-premier-prompt.md)

- [x] Validé
- Preuve : réponse fournie par l’étudiant et conservée ci-dessous ; HTML extrait sans correction dans `essais-n0/chatbot-v1.html`. Page ouverte dans le navigateur ; trois messages essayés et réponses rapportées par l’étudiant. Réponse fournie relue : aucune clé ni donnée personnelle identifiée.
- Mon prompt, envoyé tel quel selon ma confirmation dans cette conversation : « Fais-moi un chatbot sur le potager et le jardin pour les jardiniers sur balcon, au potager ou dans un massif, dans une seule page HTML que j'ouvre dans mon navigateur. »
- La première réponse du chat (texte et code), telle quelle :

````python
from pathlib import Path

html = r'''<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JardiBot 🌱 — Assistant potager & jardin</title>
<style>
:root{
  --green:#24543a; --green2:#397554; --leaf:#dcebdc; --cream:#f7f3e8;
  --card:#fffdf8; --text:#20332a; --muted:#66776e; --accent:#e99a56;
  --shadow:0 14px 40px rgba(32,51,42,.12);
}
*{box-sizing:border-box}
body{
  margin:0; min-height:100vh; font-family:Inter,system-ui,-apple-system,Segoe UI,sans-serif;
  color:var(--text); background:
  radial-gradient(circle at 10% 0%,#e1efdc 0,transparent 32%),
  radial-gradient(circle at 90% 100%,#f3ddc3 0,transparent 28%),var(--cream);
}
.app{max-width:1100px;margin:auto;padding:28px 18px}
header{display:flex;align-items:center;justify-content:space-between;gap:20px;margin-bottom:22px}
.brand{display:flex;align-items:center;gap:13px}.logo{width:52px;height:52px;border-radius:17px;background:var(--green);display:grid;place-items:center;font-size:28px;box-shadow:var(--shadow)}
h1{font-size:25px;margin:0}.subtitle{color:var(--muted);font-size:14px;margin-top:3px}
.badge{background:#fff8;border:1px solid #d8e2d5;border-radius:99px;padding:9px 13px;font-size:13px}
.layout{display:grid;grid-template-columns:270px 1fr;gap:18px}
.sidebar,.chat{background:rgba(255,253,248,.88);border:1px solid #e3e5d9;border-radius:25px;box-shadow:var(--shadow);backdrop-filter:blur(8px)}
.sidebar{padding:20px}.sidebar h2{font-size:15px;margin:0 0 12px}
.mode{width:100%;border:1px solid #dfe4db;background:white;border-radius:14px;padding:12px;margin:5px 0;text-align:left;cursor:pointer;font-size:14px;color:var(--text);transition:.2s}
.mode:hover,.mode.active{background:var(--leaf);border-color:#aac6ad;transform:translateY(-1px)}
.tip{margin-top:20px;padding:14px;border-radius:16px;background:#f4eadc;font-size:13px;line-height:1.5}
.chat{height:720px;display:flex;flex-direction:column;overflow:hidden}
.chat-head{padding:18px 22px;border-bottom:1px solid #e7e8df;display:flex;align-items:center;gap:11px}
.online{width:10px;height:10px;border-radius:50%;background:#59a96a;box-shadow:0 0 0 4px #e3f3e5}
.messages{flex:1;overflow:auto;padding:22px;scroll-behavior:smooth}
.msg{display:flex;margin:10px 0}.msg.user{justify-content:flex-end}
.bubble{max-width:78%;padding:13px 16px;border-radius:18px;line-height:1.52;font-size:14px;white-space:pre-wrap}
.bot .bubble{background:#edf4ea;border-bottom-left-radius:5px}.user .bubble{background:var(--green);color:white;border-bottom-right-radius:5px}
.quick{padding:0 22px 12px;display:flex;gap:8px;overflow:auto}
.chip{white-space:nowrap;border:1px solid #d9dfd5;background:white;border-radius:99px;padding:8px 12px;cursor:pointer;color:var(--green);font-size:12px}
.chip:hover{background:var(--leaf)}
.composer{display:flex;gap:10px;padding:15px;border-top:1px solid #e7e8df;background:#fff}
input{flex:1;border:1px solid #d9ded5;border-radius:16px;padding:14px 16px;font-size:14px;outline:none;background:#fafbf8}
input:focus{border-color:#7fa88a;box-shadow:0 0 0 3px #e6f0e5}
button.send{border:0;background:var(--green);color:white;border-radius:16px;padding:0 19px;cursor:pointer;font-size:18px}
button.send:hover{background:var(--green2)}
footer{text-align:center;color:var(--muted);font-size:11px;margin-top:15px}
@media(max-width:750px){.layout{grid-template-columns:1fr}.sidebar{padding:14px}.modes{display:flex;gap:6px}.mode{font-size:12px;text-align:center}.tip{display:none}.chat{height:72vh}.badge{display:none}.bubble{max-width:90%}}
</style>
</head>
<body>
<div class="app">
<header>
  <div class="brand"><div class="logo">🌱</div><div><h1>JardiBot</h1><div class="subtitle">Ton compagnon pour cultiver, planter et prendre soin du jardin.</div></div></div>
  <div class="badge">🌿 Conseils naturels & pratiques</div>
</header>

<div class="layout">
<aside class="sidebar">
  <h2>Où jardines-tu ?</h2>
  <div class="modes">
    <button class="mode active" data-mode="balcon">🪴 Sur mon balcon</button>
    <button class="mode" data-mode="potager">🥕 Au potager</button>
    <button class="mode" data-mode="massif">🌸 Dans un massif</button>
  </div>
  <div class="tip"><b>Conseil du moment 🍂</b><br>En automne, protège le sol avec des feuilles mortes ou du paillage : il restera vivant et résistera mieux au froid.</div>
</aside>

<main class="chat">
  <div class="chat-head"><span class="online"></span><div><b>JardiBot</b><div style="font-size:12px;color:var(--muted)">Assistant jardinier • disponible</div></div></div>
  <div class="messages" id="messages"></div>
  <div class="quick" id="quick">
    <button class="chip">Que planter maintenant ?</button>
    <button class="chip">Mes feuilles jaunissent</button>
    <button class="chip">Comment arroser ?</button>
    <button class="chip">Plantes faciles</button>
  </div>
  <form class="composer" id="form">
    <input id="input" autocomplete="off" placeholder="Pose ta question sur ton jardin…">
    <button class="send" aria-label="Envoyer">➜</button>
  </form>
</main>
</div>
<footer>JardiBot donne des conseils généraux : adapte-les à ton climat, ton exposition et à tes plantes.</footer>
</div>

<script>
let mode="balcon";
const messages=document.getElementById("messages");
const input=document.getElementById("input");

function add(text,who="bot"){
 const row=document.createElement("div"); row.className="msg "+who;
 const b=document.createElement("div"); b.className="bubble"; b.textContent=text;
 row.appendChild(b); messages.appendChild(row); messages.scrollTop=messages.scrollHeight;
}
add("Bonjour 👋 Je suis JardiBot. Je peux t’aider à choisir tes plantations, diagnostiquer un problème, organiser ton potager ou entretenir tes fleurs.\n\nTu jardines où et qu’aimerais-tu faire ?");

document.querySelectorAll(".mode").forEach(btn=>btn.onclick=()=>{
 document.querySelectorAll(".mode").forEach(x=>x.classList.remove("active")); btn.classList.add("active");
 mode=btn.dataset.mode;
 const names={balcon:"🪴 balcon",potager:"🥕 potager",massif:"🌸 massif"};
 add("Je jardine côté "+names[mode]+".","user");
 setTimeout(()=>add(contextReply()),350);
});

function contextReply(){
 if(mode==="balcon") return "Parfait ! Pour un balcon, je tiendrai compte de l’espace limité, des pots, de l’exposition et de l’arrosage plus fréquent. Que veux-tu cultiver ?";
 if(mode==="potager") return "Super ! Au potager, on peut parler rotations, associations, semis, récoltes, sol et ravageurs. Que souhaites-tu préparer ?";
 return "Très bien ! Pour ton massif, je peux t’aider sur les vivaces, les floraisons, les couleurs, l’exposition et l’entretien. Quel est ton objectif ?";
}

function answer(q){
 const s=q.toLowerCase();
 const place={balcon:"sur ton balcon",potager:"dans ton potager",massif:"dans ton massif"}[mode];

 if(/planter|semer|maintenant|octobre|automne/.test(s)){
   if(mode==="balcon") return "En automne "+place+", tu peux miser sur 🌱 mâche, épinards, radis d’hiver et aromatiques rustiques. Côté fleurs : pensées, bruyères et petits bulbes de printemps. Vérifie surtout que les pots sont bien drainés.";
   if(mode==="potager") return "En automne "+place+", pense à l’ail, aux fèves selon le climat, aux épinards, à la mâche et aux engrais verts. C’est aussi un excellent moment pour pailler les parcelles libres et enrichir le sol avec du compost mûr.";
   return "Pour un massif d’automne, c’est une très bonne période pour installer des vivaces, arbustes et bulbes de printemps 🌷. Le sol encore doux aide les racines à s’installer avant l’hiver.";
 }
 if(/jaune|jaunissent|feuille/.test(s)) return "Des feuilles jaunes peuvent venir de plusieurs choses : trop d’eau, manque d’eau, manque de nutriments ou vieillissement naturel. "+(mode==="balcon"?"En pot, commence par vérifier que l’eau s’écoule bien sous le contenant.":"Vérifie l’humidité du sol à quelques centimètres de profondeur.")+" Dis-moi quelle plante est concernée et si les feuilles jaunes sont plutôt en bas ou en haut.";
 if(/arroser|arrosage|eau/.test(s)) return "Le bon réflexe : touche la terre avant d’arroser 💧. Arrose profondément plutôt que souvent et superficiellement, de préférence le matin. "+(mode==="balcon"?"Les pots sèchent vite : surveille-les davantage lors des journées chaudes ou venteuses.":"Un paillage limite fortement l’évaporation.");
 if(/facile|début|debut/.test(s)){
   if(mode==="balcon") return "Pour débuter sur un balcon : ciboulette, menthe en pot séparé, radis, laitue, fraisiers et tomates cerises si tu as assez de soleil ☀️.";
   if(mode==="potager") return "Pour un potager facile : radis, courgettes, haricots, laitues, tomates cerises et aromatiques. Commence petit : quelques cultures bien suivies valent mieux qu’un grand potager difficile à entretenir.";
   return "Pour un massif facile, regarde les géraniums vivaces, sauges, heuchères, sedums et graminées. Le choix précis dépend surtout du soleil et de ton type de sol.";
 }
 if(/puceron|limace|insecte|ravageur/.test(s)) return "Avant de traiter, identifie le ravageur 🐞. Pour les pucerons, un jet d’eau et la présence d’auxiliaires peuvent suffire. Pour les limaces, privilégie barrières, ramassage et refuges à auxiliaires. Évite les traitements systématiques.";
 if(/tomate/.test(s)) return "Pour les tomates 🍅 : beaucoup de lumière, un sol riche, un arrosage régulier au pied sans mouiller le feuillage et un bon espace autour de la plante. En pot, vise un contenant généreux avec drainage.";
 if(/compost|terre|sol/.test(s)) return "Un sol vivant est la base 🌍. Apporte du compost mûr en surface, évite de laisser la terre nue et utilise un paillage organique. Pour aller plus loin, dis-moi si ta terre est plutôt argileuse, sableuse ou inconnue.";
 return "Je peux t’aider avec ça "+place+" 🌿. Pour te donner un conseil vraiment utile, précise-moi la plante concernée, son exposition (soleil / mi-ombre / ombre) et ce que tu observes.";
}

function submit(text){
 if(!text.trim())return; add(text.trim(),"user"); input.value="";
 setTimeout(()=>add(answer(text)),300);
}
document.getElementById("form").onsubmit=e=>{e.preventDefault();submit(input.value)};
document.querySelectorAll(".chip").forEach(c=>c.onclick=()=>submit(c.textContent));
</script>
</body>
</html>'''

path = Path("/mnt/data/jardibot.html")
path.write_text(html, encoding="utf-8")
print(f"Créé : {path}")
````

- Extraction : seul le contenu de la chaîne Python `html` est copié dans le fichier HTML, sans correction. Le script Python fourni n’a pas été exécuté.
- Trois lignes d'observation (essais dans le navigateur, rapportés par l’étudiant) :
  1. « Comment arroser mon potager ? » reçoit des conseils d’arrosage, mais la réponse parle des pots : écrire « potager » ne change pas le mode « balcon » sélectionné par défaut.
  2. « Mes feuilles jaunissent » reçoit plusieurs causes possibles et une demande de précisions sur la plante et la position des feuilles jaunes ; la réponse reste adaptée aux pots.
  3. « Qui a gagné le match » reçoit la réponse générique « Je peux t’aider avec ça sur ton balcon 🌿 », puis une demande de précisions sur une plante. Le bot ne reconnaît pas explicitement que la question est hors sujet.
- Difficulté qui reste : le contexte dépend du bouton sélectionné et le repli reste trompeur hors sujet. Ces observations sont conservées sans corriger la version 1. Garder la conversation web pour J1-03.

### J1-03 · 💥 Ça marche… jusqu'à quand — [fiche](checkpoints/J1-03-jusqua-quand.md)

- [ ] Validé
- Liste de contrôle de la version 1 (cinq à huit comportements essayés) :
  - [x] Une question sur l’arrosage reçoit une réponse ; en mode balcon, elle parle des pots même si la question mentionne le potager.
  - [x] « Mes feuilles jaunissent » reçoit des causes possibles et une demande de précisions.
  - [x] Une question sur un match reçoit le repli générique sur le jardinage, sans signalement explicite du hors-sujet.
  - [x] Un message vide n’est pas envoyé, y compris avec la touche Entrée.
  - [x] Le bouton « Au potager » affiche « Je jardine côté 🥕 potager. », puis « Super ! Au potager, on peut parler rotations, associations, semis, récoltes, sol et ravageurs. Que souhaites-tu préparer ? ».
  - [x] Recharger la page fait perdre toute la conversation.
  - Ces constats proviennent des essais rapportés par l’étudiant. Les cases indiquent un comportement observé, pas nécessairement souhaitable. L’envoi par Entrée avec un texte non vide n’a pas été confirmé sur la version 1 ; il a ensuite été vérifié sur la version 2.
- Journal des régressions, une entrée par modification : ce que j'ai demandé · ce qui marche maintenant · ce qui marchait et ne marche plus · ce que je n'avais pas vu, et comment je l'ai trouvé.
  - Modification 1 — `essais-n0/chatbot-v2.html` (réponse HTML conservée à l’identique, version 1 conservée) :
    - Demande : « Ajoute un bouton « Effacer la conversation » qui vide les messages et redonne-moi le fichier HTML complet. » Première réponse reçue : script Python de modification, pas le HTML complet. Relance demandée : « Tu m’as donné un script Python. Donne-moi le fichier HTML complet mis à jour, de `<!DOCTYPE html>` à `</html>`, en un seul bloc, sans Python. »
    - Ce qui marche maintenant : l’étudiant a envoyé un message puis effacé la conversation ; seul le message d’accueil reste. Les questions sur l’arrosage, les feuilles jaunes et le match reçoivent encore leurs réponses ; le bouton « Au potager » affiche bien le changement de contexte. Le rechargement perd toujours les échanges et ne laisse que l’accueil.
    - Ce qui marchait et ne marche plus : aucune perte de fonctionnalité rapportée sur les essais ci-dessus. Les listes et sauts de ligne ajoutés dans les réponses sont visibles dans les résultats fournis : changements de présentation non demandés. Deux essais complémentaires confirmés par l’étudiant sur la version 2 : cliquer sur Envoyer avec le champ vide ne fait rien ; saisir « salut » puis appuyer sur Entrée envoie le message. Les six comportements de la liste initiale ont donc été revérifiés, et l’envoi par Entrée avec du texte est ajouté aux contrôles des versions suivantes.
    - Ce que je n’avais pas vu et comment je l’ai cherché : l’assistant a repéré dans le code des réponses différées non annulées par Effacer. L’étudiant a essayé d’envoyer puis d’effacer immédiatement : seul l’accueil est resté, aucune réponse tardive rapportée. Le risque repéré dans le code n’a donc pas été reproduit pendant cet essai ; il n’est pas présenté comme un bug observé.
  - Modification 2 — `essais-n0/chatbot-v3.html` (HTML reçu conservé à l’identique ; versions 1 et 2 conservées) :
    - Demande préparée pour le chat, suivie de la réponse transmise par l’étudiant : « Garde la conversation après un rechargement de la page et redonne-moi le fichier HTML complet en un seul bloc, sans Python. »
    - Ce qui marche maintenant : l’étudiant confirme que les messages sont conservés après rechargement. Après effacement puis rechargement, seul l’accueil reste ; les anciens échanges ne reviennent pas. Le code utilise la clé `jardibot_messages` dans `localStorage`.
    - Ce qui marchait et ne marche plus : le message vide est toujours ignoré et Entrée envoie le texte (texte réellement rapporté : « salt »). « qui a gagner le matche » reçoit toujours le repli générique, ici dans le contexte potager. Aucune régression confirmée sur ces essais. Le nouvel essai exact « Mes feuilles jaunissent » reçoit bien les quatre causes possibles (trop d’eau, manque d’eau, manque de nutriments, vieillissement naturel), le conseil de vérifier l’humidité du sol et une demande de précisions sur les feuilles. Réponse spécialisée confirmée dans le contexte potager ; le repli précédent concernait la formulation différente « mes feuils jeunisse ». La conservation des messages remplace désormais leur perte au rechargement, comme demandé.
    - Ce que je n’avais pas vu et comment je l’ai cherché : l’étudiant confirme que le mode Potager et les messages restent après rechargement, et que les anciens échanges ne reviennent pas après effacement. L’essai « mes feuils jeunisse » reçoit le repli générique au lieu de la réponse sur les feuilles jaunes : limite observée avec cette orthographe, pas une régression démontrée entre versions. Le code mémorise aussi le mode sous `jardibot_mode`, au-delà des seuls messages demandés.
  - Modification 3 :
- Chasse à l'angle mort (ce qui a été trouvé, et par qui) :
- Deux phrases de conclusion :
- Difficulté qui reste :

### J1-04 · 🎲 Même prompt, autre réponse — [fiche](checkpoints/J1-04-meme-prompt.md)

- [ ] Validé
- Le prompt de référence (identique aux trois essais) :
- Le tableau des écarts (trois colonnes A, B, C ; au moins quatre critères ; des faits, pas des impressions) :
- Une phrase de conclusion (ce que ces écarts autorisent, ce qu'ils interdisent de supposer) :
- Difficulté qui reste :

## L'agent (N1 Demander)

### J1-05 · 🛠 dsh en main — [fiche](checkpoints/J1-05-dsh-en-main.md)

- [ ] Validé
- Preuve (`dsh --version`, mode Read Only, modèle `capweb-ia`, `git status -- atelier` propre ; **jamais la clé**) :
- La consigne exacte envoyée à l'agent et sa réponse :
- Pour chaque fichier cité : existe ou non, description juste ou fausse, pourquoi ; et un fichier qu'il n'a pas cité :
- Difficulté qui reste :

### J1-06 · 🧱 Anatomie d'un prompt — [fiche](checkpoints/J1-06-anatomie-dun-prompt.md)

- [ ] Validé
- Preuve (deux prompts, deux résultats, grille remplie, commit du squelette) :
- Prompt vague et ce que montre la page (trois lignes, fichiers touchés) :
- Prompt structuré, en six parties, tel qu'envoyé :
- Les hypothèses de l'agent, et ma réponse :
- La grille (✔ ou ✘ et un mot, pour « vague » puis « structuré ») :
- Une phrase : entre les deux résultats, ce qui a le plus changé, c'est… parce que la partie… de mon prompt disait…
- Difficulté qui reste :

### J1-07 · 👣 Petits pas — [fiche](checkpoints/J1-07-petits-pas.md)

- [ ] Validé
- Preuve (découpage écrit avant la première demande, trois diffs relus, un refus écrit, un commit par étape acceptée, trois boutons de questions qui fonctionnent) :
- La tâche, mes trois questions et mon découpage en trois étapes (écrit avant la première demande d'écriture) :
- Ce que l'agent a proposé comme découpage, ce que j'ai gardé, pourquoi :
- Mon refus écrit : ce que l'agent avait fait, pourquoi je le refuse, ce que j'ai demandé à la place :
- Difficulté qui reste :

**Journal des décisions.** Une ligne par demande faite à l'agent, de J1-07 à J1-09 (les trois étapes de J1-07, puis la correction de J1-08, puis les six demandes de J1-09) : la demande copiée, le diff relu (fichiers, nombre de lignes, une chose que je n'avais pas demandée ?), le verdict et pourquoi.

| N° | Demande | Diff relu | Verdict et pourquoi |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 | | | |
| 8 | | | |
| 9 | | | |
| 10 | | | |

### J1-08 · 🔎 Revue de la page — [fiche](checkpoints/J1-08-revue-de-la-page.md)

- [ ] Validé
- Preuve (trois défauts, un corrigé avec son avant et son après, diff relu, revue adverse vérifiée) :
- Mes défauts, un par ligne :

  | Lentille (structure, clavier, écrans) | Où (élément ou fichier) | Comment je l'ai vu |
  |---|---|---|
  | | | |
  | | | |
  | | | |

- La revue adverse : trois affirmations de l'agent, la référence qu'il a donnée (fichier, ligne), mon verdict (vrai, faux, rejeté sans référence) et comment j'ai vérifié :
- Le défaut corrigé : l'avant (capture ou valeur), ma demande ciblée (copiée), le diff relu (fichiers, lignes, changement non demandé ?), l'après (même geste, même mesure) :
- Difficulté qui reste :

### J1-09 · 🧠 Un cerveau à règles, par prompts — [fiche](checkpoints/J1-09-cerveau-a-regles.md)

- [ ] Validé
- Preuve (comportements vérifiés : « Vous : … », message vide, `<b>gras</b>`, mes deux mots, ma limite ; `/js/brain.js` et `/js/view.js` affichés ; F5 ; « Effacer ») :
- Mes six demandes et leurs verdicts : dans le journal des décisions ci-dessus.
- Le rôle de chaque fichier, en une phrase chacun :
  - `app.js` :
  - `brain.js` :
  - `view.js` :
- Ce que j'ai vu quand j'ai mis `{pas du json` dans la mémoire :
- Difficulté qui reste :

### J1-10 · 🧪 Épreuve de l'explication — [fiche](checkpoints/J1-10-epreuve-explication.md)

- [ ] Validé
- Preuve (`npm test` vert avec cinq tests dont ma limite, commit de sauvegarde, remise faite) :
- Le test rouge : son nom, son message exact, et ce qu'il m'a appris :
- Épreuve de l'explication, éditeur fermé :
  - Ce que je n'ai pas su expliquer :
  - Ce que mon binôme n'a pas su expliquer :
- Difficulté qui reste :

## Quatre questions pour finir

1. Pourquoi `textContent` et pas `innerHTML` ?
2. Pourquoi trois fichiers plutôt qu'un seul ?
3. L'agent a écrit le code : comment savez-vous qu'il est juste, et qu'est-ce qui l'a vu échouer ?
4. Quelle astuce avez-vous le plus utilisée aujourd'hui, et laquelle avez-vous oubliée ?

## Aides utilisées

- Indices, aide-mémoire, voisins :
- Ce que j'ai demandé à une IA, et comment j'ai vérifié sa réponse :

## Notes personnelles (chacun)

Pour préparer l'explication de votre part du code. Chacun écrit avec ses mots.

- Nom :
- Ce que j'ai compris :
- Ce que je n'ai pas encore compris :

- Nom :
- Ce que j'ai compris :
- Ce que je n'ai pas encore compris :

Git sert à sauvegarder chaque étape acceptée : lisez les différences et nommez les fichiers à enregistrer, jamais `git add -A`. Attendez la consigne du formateur avant tout envoi vers un dépôt commun.

[README du jour](README.md) · [Aide-mémoire HTML/CSS](ressources/aide-memoire.md) · [Aide-mémoire JavaScript](ressources/aide-memoire-js.md) · [Notice dsh](ressources/dsh.md)
