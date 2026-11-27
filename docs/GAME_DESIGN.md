# PANTIN — Document de game design

> Jeu couloir / plateforme-énigme d'horreur, pour Halloween.
> Nom de travail : **Pantin** (poupée de chiffon / marionnette).
> Statut : pré-production. Base technique = copie de Space Rocks (assets jetables, à remplacer).

## 1. Pitch

Un petit clown maladroit, fait de chiffon, se réveille seul dans un lieu
clos et nocturne qui semble le retenir. Pour avancer, il doit résoudre les
énigmes gravées dans le décor, garder l'équilibre sur un corps qui ne lui
obéit pas tout à fait, et se faire oublier de ce qui rôde. Chaque salle
franchie révèle un fragment de pourquoi il est là — et pourquoi il ne
devrait peut-être pas chercher à sortir.

## 2. Piliers (ne jamais trahir ces 3 points)

1. **Huis clos exigu et suffocant.** Une seule enceinte, de nuit. Pas de
   grands espaces ouverts. L'air manque, les murs sont proches.
2. **Fragilité attachante = peur amplifiée.** Le perso est mignon, mou,
   maladroit (poupée de chiffon). Plus on s'y attache, plus le danger fait mal.
   Réf. de ton : Little Nightmares, Ori, Hollow Knight.
3. **Énigmes diégétiques.** Aucune énigme ne s'ouvre en plein écran comme une
   appli. Tout est un objet du monde (voir §5). L'immersion ne se brise jamais.

## 3. Personnage

- **Le Pantin** : petit clown en chiffon, museau rond, collerette, bonnet
  pointu, l'air un peu paumé et mélancolique (cf. planches de refs fournies).
- **Corps instable** : il ne court pas net, il titube. Son mouvement par
  défaut porte un léger ballant → le pilier « équilibre » vient de là.
- **Pas de combat.** Il ne se bat pas, il subit, évite, résout. Vulnérabilité
  constante.
- **Expressivité muette** : il ne parle pas. Tout passe par la posture, le
  tremblement, les petits sons (voir §6). Comme ses inspirations.

## 4. Mécaniques

Le jeu alterne volontairement **tension motrice** (corps) et **tension
cérébrale** (énigme) pour que le joueur ne respire jamais vraiment.

- **Plateforme** : saut, accroche, chute. Base du déplacement.
- **Équilibre** : dans certaines salles, le corps du Pantin oscille ; il faut
  contre-corriger (entrée gauche/droite ou maintien) pour ne pas tomber d'une
  poutre / passerelle. Échec = chute, bruit, danger.
- **Furtivité (fufu)** : salles où il faut rester silencieux. Se déplacer
  lentement, se cacher, ne pas déclencher ce qui écoute. Courir = mourir.
- **QTE** : moments scénarisés courts (se rattraper, forcer une porte,
  échapper à une main). Rares, pour ponctuer, pas pour spammer.

## 5. Énigmes (chacune devient un OBJET du décor)

Règle d'or : jamais de pop-up « appli ». L'énigme est physique, dans la salle.

- **Cryptogramme** → inscriptions gravées sur un mur / une pierre tombale /
  un panneau de foire décrépit. Le Pantin éclaire ou frotte pour révéler.
- **Wordle** → serrure à molettes de lettres sur une malle / une porte. On
  tourne les rouleaux, le feedback (lettre bien placée / mal placée) se montre
  par des pastilles qui s'allument sur le mécanisme.
- **Mot en chaîne** → enseignes lumineuses d'une fête foraine morte : relier
  les mots de pancarte en pancarte pour rallumer un chemin / un pont.
- **Hashtag (#)** → grille de symboles type morpion gravée au sol ; aligner /
  activer les bonnes cases (dalles sensibles) pour ouvrir un passage.

Chaque énigme résolue → **débloque une pièce ou un objet** → permet d'avancer
→ révèle **un fragment d'histoire**.

## 6. Direction artistique & son

- **Visuel** : palette pastel délavée (le Pantin lui-même), posée sur des
  décors nocturnes désaturés, bleutés, étouffants. Contraste mignon/menaçant.
- **Lumière** : sources rares et chaudes (bougie, loupiote de foire) qui
  mangent peu l'obscurité. L'obscurité est un personnage.
- **Son** : nappes basses continues (pression), silences longs, petits
  couinements du chiffon quand il bouge. Le son fait 50 % de la peur,
  surtout dans les salles de furtivité.

## 7. Structure : une salle = une room GameMaker

Le huis clos se découpe en salles successives (couloir). Modèle de salle :
**1 mécanique dominante + 1 énigme → débloque 1 objet/passage + 1 fragment.**

Rythme cible (alterne corps / cerveau) :

| # | Salle | Mécanique | Énigme | Débloque |
|---|-------|-----------|--------|----------|
| 1 | L'éveil | plateforme simple | — (tuto mouvement) | la porte |
| 2 | La passerelle | équilibre | cryptogramme mural | la clé |
| 3 | La fête morte | furtivité | mot en chaîne (enseignes) | le pont |
| 4 | La malle | plateforme | wordle (serrure) | l'objet-histoire |
| 5 | Le seuil | furtivité + QTE | hashtag (dalles) | la sortie ? |

(Ordre indicatif — à ajuster au playtest.)

## 8. Scope : vertical slice D'ABORD

Ne PAS tout construire d'un coup. Objectif 1 = **2 salles jouables de bout en
bout** prouvant la boucle :

- **Salle 1 (L'éveil)** : le Pantin marche, saute, titube ; on sort par une porte.
- **Salle 2 (La passerelle)** : équilibre sur une poutre + un cryptogramme
  mural qui donne la clé de la porte suivante.

Quand cette boucle (bouger → résoudre → avancer → fragment) est fun et solide,
on duplique le patron pour les salles 3, 4, 5. C'est aussi le mode de travail
le plus efficace avec Claude Code : un patron clair à répliquer.

## 9. Pour plus tard (ne pas s'éparpiller maintenant)

- Système de sauvegarde / checkpoints par salle.
- Écran-titre, menu, options.
- Vrais sprites du Pantin (remplacer spr_player), tilesets de décor, sons.
- Narration/fragments (forme exacte à décider : images, objets, murmures).

## 10. Bible d'horreur

Registre : horreur **analogique / liminale / cryptique**. On vise le *dread*,
jamais le jumpscare. La peur vient de l'ambiance et du déchiffrage.
Réfs : Iron Lung, Petscop, Feldup, Backrooms, Oldest View, Dead Plate,
La Maison des feuilles, Strange Pictures / Strange House (Uketsu).

**Les 5 principes :**

1. **L'espace est le monstre.** Le huis clos se réarrange : la porte d'où l'on
   vient disparaît, un couloir s'allonge au retour, une pièce « de trop »
   apparaît sur un plan. Une énigme peut être *la lecture d'un plan* (façon
   Strange House / Maison des feuilles) : l'architecture fait peur avant la chose.
2. **On ne voit jamais la chose en face.** Le Pantin voit mal (yeux-boutons,
   noir). La menace se devine : cercle d'une bougie, reflet, présence visible
   seulement quand on regarde ailleurs. Peur par la médiation et le hors-champ.
3. **Le mignon qui ment.** Boîte à musique qui ralentit et se désaccorde,
   comptine qui dérape, poupées pastel adorables qu'il ne faut pas réveiller.
   Ce qui est fait pour rassurer un enfant est ce qui cloche.
4. **Comprendre = avoir peur.** Résoudre l'énigme et découvrir une vérité pire,
   c'est le même geste. Chaque fragment débloqué doit refroidir, pas rassurer.
5. **Slow-burn, jamais jumpscare.** Silences longs, nappes basses, wrongness qui
   s'installe, l'air qui manque. La pression monte et ne retombe pas.

**Règles dures :**
- Aucun jumpscare bon marché.
- Lumière rare et chaude ; l'obscurité est un personnage à part entière.
- Le son = 50 % de la peur (surtout dans les salles de furtivité).
- Pas de gore gratuit : l'horreur est psychologique et cryptique.
- Chaque énigme résolue doit refroidir, pas rassurer.
