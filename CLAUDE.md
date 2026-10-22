# Portfolio Flaura.dev

Site vitrine one-page de Laura, développeuse web freelance (Flaura.dev), basée dans le Var et en remote partout en France. Le site doit donner envie aux TPE, indépendants et petites entreprises de réserver un appel. Direction artistique validée : « Yozakura », en sombre et en clair : chaque visiteur a celui de son système et peut changer.

## Comment travailler avec moi

- La sécurité du site passe avant tout. Sur les points critiques (formulaire, envoi d'e-mails, variables d'environnement, headers, dépendances, déploiement), tu proposes d'abord et tu attends mon accord. Sur l'anodin (styles, textes, composants d'affichage), tu codes directement.
- Tu me tiens toujours au courant de ce que tu as fait, sans rien cacher : fichiers touchés, choix faits, ce qui reste à faire.
- Si tu n'es pas d'accord avec une de mes demandes, dis-le franchement et explique pourquoi.
- Réponses courtes, sauf si le sujet le mérite.

## Stack (validée le 7 octobre 2026)

- Next.js 16 (App Router) + TypeScript, npm
- Tailwind CSS 4
- Polices via `next/font/google` : Big Shoulders (police variable, axe `opsz` fixé à 72 = l'ancienne « Display »), Geist, Geist Mono. Le guillemet du témoignage est le glyphe d’Abril Fatface vectorisé en SVG (la police n’est pas chargée)
- Thème : **suit le réglage clair/sombre du système du visiteur** (choix du 14 octobre 2026, à la place du sombre imposé à tous), bouton pour passer à l’autre, choix retenu (revenir au thème du système efface l’exception), sans flash au chargement. Sans JavaScript : sombre. Les deux thèmes reçoivent le même soin.
- Réservation : widget Calendly intégré (lien à fournir par moi)
- Formulaire de contact (choix du 22 octobre 2026) : Server Action `app/actions/contact.ts` (fonctionne sans JavaScript), validation côté serveur avec zod, champ piège, limite de 3 messages par IP en 10 minutes et 50 par jour (`lib/rate-limit.ts`, en mémoire). Envoi par le relais SMTP de **Brevo** (serveurs dans l'UE) avec nodemailer (`lib/mail.ts`) : e-mail en texte seul, de `formulaire@flaura-dev.com` (alias de hello@ chez Hostinger, expéditeur authentifié dans Brevo) à `hello@flaura-dev.com`, réponse directe au visiteur, aucun e-mail automatique au visiteur. Identifiants dans `BREVO_SMTP_LOGIN` et `BREVO_SMTP_KEY` (`.env.local` en local, hPanel en production, noms dans `.env.example`) : une **clé SMTP**, jamais une clé API (qui ouvrirait tout le compte). La clé expire le 22 octobre 2027 **et après 90 jours sans envoi** : tester le formulaire au moins une fois par mois. Textes et types de projet dans `content/contact.ts`. Rien du message n'est écrit dans les journaux du serveur. Aucune clé en dur dans le code.
- Hébergement : Hostinger, offre Business Web Hosting (web app Node.js, déploiement depuis GitHub)
- Domaine : https://flaura-dev.com/, adresse de contact `hello@flaura-dev.com` (Hostinger, redirigée vers Gmail)
- Dépôt : https://github.com/Flaura-dev/flaura-dev.com

## Référence visuelle

`maquette/maquette-yozakura.html` est la maquette validée (fichier local, volontairement hors du dépôt Git car il contient des coordonnées personnelles). C'est un fichier d'un outil de maquettage : la syntaxe `<x-dc>`, `{{...}}`, `<sc-for>`, `<sc-if>` et la classe `Component extends DCLogic` ne sont PAS à réutiliser. Sers-t'en uniquement comme référence pour la structure, les textes exacts, les espacements, les tailles et les couleurs, et reconstruis tout proprement en composants React.

## Charte

Couleurs (variables CSS, une palette par thème) :

| Rôle | Sombre | Clair |
|---|---|---|
| fond | #0D0817 | #F7F2EE |
| surface (cartes) | #160F21 | #FFFFFF |
| bordures | #282036 | #E7DDD9 |
| contour des champs de formulaire (3:1) | #746D83 | #8A808C |
| texte | #F3EDF0 | #1B1720 |
| texte secondaire | #ADA8B9 | #625A68 |
| texte discret | #5F586F | #A0959F |
| rose accent | #F07FA2 | #C2386B |
| rose survol | #FFB3C8 | #9E2552 |
| vert « disponible » | #6BD49A | #6BD49A |

Le fond sombre est le « violet abysse » (choix du 18 octobre 2026, à la place du noir #0E0C11 de la maquette) : aussi profond que l’ancien noir, mais nettement violet ; toute la palette sombre a été déclinée dans cette teinte. Le rose est plus foncé en clair pour garder un contraste lisible. Le texte des boutons roses utilise la couleur de fond.

Typo : titres de section en Big Shoulders Display 900, capitales, 110 px sur desktop (72 px mobile), numéro de section en Geist Mono rose à gauche, aligné en bas. Texte courant en Geist. Étiquettes, filtres, petites mentions en Geist Mono.

Interdits : aucun caractère japonais (kanji, kana) nulle part, pas de pétales décoratifs (seule exception, demandée le 7 octobre 2026 : une chute discrète de pétales en arrière-plan, désactivable par le visiteur et coupée si l'animation est réduite), pas de bandeau défilant. Le site tutoie le visiteur partout (choix du 7 octobre 2026, à la place du vouvoiement).

## Structure de la page

1. Barre de navigation : fleur sakura + « FLAURA » (Big Shoulders) + « .dev_ » (Geist Mono rose), aligné sur le bord gauche du contenu. Au survol, la fleur fait un tour complet une seule fois. Menu en pilule au centre, avec une bulle rose translucide posée sur la section en cours qui suit le lien survolé. À droite : bouton thème (soleil/lune) puis « Réserver un appel » avec une icône téléphone (même icône sur le bouton de l'accueil et du menu mobile).
2. Accueil : « FLAURA.dev_ » géant, photo détourée devant avec halo rose et fondu vers le bas, accroche « Tes clients doivent pouvoir te trouver, ton site doit leur donner envie de te choisir. » (l’ancien slogan « Créative dans le design… » est abandonné depuis le 14 octobre 2026), bouton Réserver un appel, carte « disponible » à droite (point vert qui clignote lentement).
3. Comment on travaille ensemble : 4 étapes (On en parle, Je conçois, Je développe, On met en ligne), cliquables. Sans interaction, la frise avance seule (5 s par étape, en boucle) ; elle s'arrête uniquement avec le bouton pause ou dès qu'on clique sur une étape (pas de pause au survol). L'étape choisie est mise en avant, les autres passent en retrait (toujours lisibles), et la ligne de progression se remplit jusqu'à l'étape choisie.
4. 01 Hello World : bento avec photo devant l'ordi (effet bichromie rose/nuit), présentation, « Var, France », parcours (dessinatrice-projeteuse → chargée d'études → cheffe de projets → développeuse web).
5. 02 Projets : jusqu'à 3 cartes projets, sans filtres sur l'accueil. Seulement des projets concrets : Ailleurs (carnet de voyage au globe 3D, en pause pour une durée indéterminée) a été retiré le 22 octobre 2026. Tant qu'il y a moins de 3 projets, la grille passe à 2 colonnes, sur l'accueil comme sur `/projets` (`components/projects/grid.ts`, qui règle aussi la taille des captures). La carte de Léa Grondin contient un comparateur avant/après glissable. Les cartes sans comparateur montrent une capture pleine page qui défile jusqu'en bas du site au survol du visuel (indice « survole »), et au rythme de la page sur écran tactile (choix du 18 octobre 2026, inspiré de fabianteichmann.fr ; composant `ScrollingShot`). Les étiquettes parlent du type de site, jamais de la techno. Bandeau rose pleine largeur « Le vôtre ? ». Un petit bouton « voir tous les projets », discret et toujours visible, est placé en bas à droite du titre « Projets » et mène à la page /projets. Témoignage en dessous. Les cartes n'ont pas de flèche vers `/projets` (doublon avec le bouton) ; quand un projet a un site en ligne, un lien ↗ vers ce site apparaît sur sa carte. La page `/projets` regroupe tous les projets ; elle n'est pas dans le menu, on y accède par le bouton « voir tous les projets ». C'est sur `/projets` que se trouvent les filtres (tous, création, refonte, site vitrine ; « application web » retiré avec Ailleurs, faute de projet, à remettre dans `content/projects.ts` quand il y en aura un), avec leur état dans l'URL (`/projets?type=refonte`) et un bouton pour copier le lien.
6. 03 Offres : grand « Offres » décoratif + `h2` « Tarifs de création de site internet » (comme la FAQ). Pas de texte d'intro. Quatre cartes Essentiel, Visibilité (mise en avant, en rose, badge « Recommandée » à cheval sur le bord haut), Pro et Refonte (module ajouté à la formule), dont les lignes s'alignent d'une carte à l'autre à partir de 1280 px (subgrid ; deux par ligne en dessous). Tous les titres de cartes sont en Big Shoulders, en capitales, précédés de « // » rose (sans sous-titre « site vitrine… », choix de Laura du 21 octobre 2026). Puis la Maintenance en longueur (Sérénité, Évolution). Les Options à la carte et le Renfort freelance pour les agences ont été retirés le 22 octobre 2026 (« ça fait trop »). Prix affichés « à partir de », HT, avec le TTC en italique dessous (TVA 20 % dès le lancement du 1er janvier 2027). Plus de tarif de lancement ni d'offre Sur mesure depuis le 21 octobre 2026 (les gros projets vont vers Pro). Tous les prix sont dans `content/offers.ts`, d'où sont tirés les cartes, les prix cités dans la FAQ et les données structurées `OfferCatalog` : ne jamais les écrire ailleurs à la main.
7. 04 FAQ : 7 questions en accordéon (`<details>`), sur une colonne, toutes fermées au chargement (choix du 21 octobre 2026, à la place de la première ouverte : la section reste courte). Le grand « FAQ » est décoratif ; le `h2` « Questions fréquentes sur la création de site internet » est à sa droite (en dessous quand la place manque). Textes dans `content/faq.ts`, d'où sont aussi générées les données structurées `FAQPage` (une seule sur le site) : ne jamais les écrire à la main. Pas de bouton sous la FAQ (le bouton « Réserver mon café virtuel » a été retiré le 21 octobre 2026, comme les questions sur le référencement, la modification du site par le client et le démarrage d'un projet).
8. 05 Parlons-en : bloc Calendly à gauche (2/3), formulaire à droite (nom et prénom, e-mail, type de projet, message, bouton pleine largeur) + lien LinkedIn (en bas de la présentation du bloc Calendly). L'appel découverte s'appelle « Café virtuel » partout, comme l'événement Calendly (choix du 14 octobre 2026) : 30 minutes, en visio uniquement (lien envoyé à la prise de rendez-vous). Calendly (https://calendly.com/flaura-devweb/cafe, offre gratuite) ne se charge qu'au clic du visiteur, et sans le bandeau cookies de Calendly (choix de Laura du 14 octobre 2026, à mentionner dans la page confidentialité).
9. Footer : logo long avec slogan, accroche, disponibilité, navigation, contact, réseaux, mentions légales, confidentialité, interrupteur des pétales, retour en haut.
10. Fil conducteur à droite : il remplace la barre de défilement native (masquée sur desktop, conservée sur mobile). Fixé sur toute la hauteur de l'écran, le point lumineux est à X % du rail quand on est à X % de la page ; on peut le glisser, cliquer sur le rail pour y sauter, ou cliquer sur le repère numéroté d'une section. Pendant le défilement, une étiquette « 02 — Projets » accompagne le point. Masqué sur mobile.

Toutes les animations respectent `prefers-reduced-motion`. Tout ce qui se touche réagit dès l’appui (utilitaires `press` et `press-text` de `globals.css`, à la place de `transition-colors`). Contraste élevé et transparence réduite sont pris en charge (palette renforcée, variante `opaque:`). Tailles de texte en rem, pour suivre la taille de police choisie par le visiteur.

## Assets

- `assets/logos/` : logo long avec slogan (footer), en blanc pour le thème sombre et en noir pour le clair, plus la fleur `sakura-accueil.webp`. Les versions sans slogan, inutilisées, ont été retirées du dépôt le 20 octobre 2026 (récupérables dans l'historique Git). Version en place : **logo v3** (« FLAURA » en Big Shoulders, « .dev_ » et slogan en Geist Mono rose), tirée des PNG de `D:\Flaura.dev\0_D.A Flaura.dev\Logo v3 (polices du site)\` (bords rognés, 1600 px de large).
- Favicons (`app/favicon.ico`, `app/icon.png`, `app/apple-icon.png`) : « favicon abysse » v3, du même dossier. Le `favicon.ico` (16, 32, 48 px) prend la variante « petit » (fleur seule, lisible en tout petit) ; `icon.png` (192 px) et `apple-icon.png` (180 px) gardent les circuits.
- `assets/photos/` : `laura-hero-detouree.webp` (accueil, déjà détourée et fondue), `laura-ordi.jpg` (bento), `laura-portrait-bleu.jpg` (avatar du bloc Calendly).
- Les SVG d'origine dans `0_D.A Flaura.dev` sont des exports Canva très lourds (jusqu'à 12 Mo) : ne pas les utiliser tels quels sur le site.

## Contenu à compléter (ne rien inventer)

Tout ce qui est entre crochets dans la maquette reste à fournir : tarifs, adresse e-mail, SIRET, lien GitHub, témoignage de Léa, problème et résultat de chaque projet. Les captures (1440 × 900, double résolution, dans `assets/projects/`) sont affichées dans un cadre navigateur commun (`BrowserFrame`) ; la capture « après » de Léa est provisoire, à refaire une fois son nouveau site terminé. Tant que ce n'est pas fourni, garde un emplacement visible, n'invente ni chiffre ni avis client.

## SEO / accessibilité

Balises sémantiques, un seul `h1`, métadonnées et Open Graph, données structurées (LocalBusiness / Person), textes alternatifs sur les images, contrastes AA, navigation au clavier, cibles tactiles d'au moins 44 px.

Données structurées de l'accueil : un seul graphe JSON-LD, généré par `lib/structured-data.ts` (entreprise `ProfessionalService`, `OfferCatalog`, `FAQPage`) depuis `content/site.ts`, `content/offers.ts` et `content/faq.ts`, et affiché par le composant `JsonLd`. Les sections n'écrivent pas de JSON-LD elles-mêmes.

Typographie des textes : apostrophes ’ et espaces insécables devant « ? », « : », « % », « € » et « HT », et entre un nombre et son unité.
