# Portfolio Flaura.dev

Site vitrine one-page de Laura, développeuse web freelance (Flaura.dev), basée dans le Var et en remote partout en France. Le site doit donner envie aux TPE, indépendants et petites entreprises de réserver un appel. Direction artistique validée : « Yozakura », sombre par défaut avec un mode clair.

## Comment travailler avec moi

- La sécurité du site passe avant tout. Sur les points critiques (formulaire, envoi d'e-mails, variables d'environnement, headers, dépendances, déploiement), tu proposes d'abord et tu attends mon accord. Sur l'anodin (styles, textes, composants d'affichage), tu codes directement.
- Tu me tiens toujours au courant de ce que tu as fait, sans rien cacher : fichiers touchés, choix faits, ce qui reste à faire.
- Si tu n'es pas d'accord avec une de mes demandes, dis-le franchement et explique pourquoi.
- Réponses courtes, sauf si le sujet le mérite.

## Stack (validée le 7 octobre 2026)

- Next.js 16 (App Router) + TypeScript, npm
- Tailwind CSS 4
- Polices via `next/font/google` : Big Shoulders (police variable, axe `opsz` fixé à 72 = l'ancienne « Display »), Geist, Geist Mono. Le guillemet du témoignage est le glyphe d’Abril Fatface vectorisé en SVG (la police n’est pas chargée)
- Thème : **sombre par défaut** pour tout le monde, bouton pour passer en clair, choix du visiteur retenu, sans flash au chargement
- Réservation : widget Calendly intégré (lien à fournir par moi)
- Formulaire de contact : validation côté serveur (zod), honeypot anti-spam, limitation de débit, envoi par un service d'e-mail à choisir ensemble. Aucune clé en dur dans le code.
- Hébergement : Hostinger, offre Business Web Hosting (web app Node.js, déploiement depuis GitHub)
- Domaine : https://flaura-dev.com/, adresse de contact `hello@flaura-dev.com` (Hostinger, redirigée vers Gmail)
- Dépôt : https://github.com/Flaura-98/flaura-dev.com

## Référence visuelle

`maquette/maquette-yozakura.html` est la maquette validée (fichier local, volontairement hors du dépôt Git car il contient des coordonnées personnelles). C'est un fichier d'un outil de maquettage : la syntaxe `<x-dc>`, `{{...}}`, `<sc-for>`, `<sc-if>` et la classe `Component extends DCLogic` ne sont PAS à réutiliser. Sers-t'en uniquement comme référence pour la structure, les textes exacts, les espacements, les tailles et les couleurs, et reconstruis tout proprement en composants React.

## Charte

Couleurs (variables CSS, une palette par thème) :

| Rôle | Sombre | Clair |
|---|---|---|
| fond | #0E0C11 | #F7F2EE |
| surface (cartes) | #17141B | #FFFFFF |
| bordures | #2A2530 | #E7DDD9 |
| texte | #F3EDF0 | #1B1720 |
| texte secondaire | #A79FAA | #625A68 |
| texte discret | #5C5560 | #A0959F |
| rose accent | #F07FA2 | #C2386B |
| rose survol | #FFB3C8 | #9E2552 |
| vert « disponible » | #6BD49A | #6BD49A |

Le rose est plus foncé en clair pour garder un contraste lisible. Le texte des boutons roses utilise la couleur de fond.

Typo : titres de section en Big Shoulders Display 900, capitales, 110 px sur desktop (72 px mobile), numéro de section en Geist Mono rose à gauche, aligné en bas. Texte courant en Geist. Étiquettes, filtres, petites mentions en Geist Mono.

Interdits : aucun caractère japonais (kanji, kana) nulle part, pas de pétales décoratifs (seule exception, demandée le 7 octobre 2026 : une chute discrète de pétales en arrière-plan, désactivable par le visiteur et coupée si l'animation est réduite), pas de bandeau défilant. Le site vouvoie le visiteur partout.

## Structure de la page

1. Barre de navigation : fleur sakura + « FLAURA » (Big Shoulders) + « .dev_ » (Geist Mono rose), aligné sur le bord gauche du contenu. Au survol, la fleur fait un tour complet une seule fois. Menu en pilule au centre, avec une bulle rose translucide posée sur la section en cours qui suit le lien survolé. À droite : bouton thème (soleil/lune) puis « Réserver un appel » avec une icône téléphone (même icône sur le bouton de l'accueil et du menu mobile).
2. Accueil : « FLAURA.dev_ » géant, photo détourée devant avec halo rose et fondu vers le bas, accroche « Créative dans le design. Rigoureuse dans le code. », bouton Réserver un appel, carte « disponible » à droite (point vert qui clignote lentement).
3. Comment on travaille ensemble : 4 étapes (On en parle, Je conçois, Je développe, On met en ligne), cliquables. Sans interaction, la frise avance seule (5 s par étape, en boucle), avec un bouton pause ; elle s'arrête au survol et dès qu'on clique sur une étape. L'étape choisie est mise en avant, les autres passent en retrait (toujours lisibles), et la ligne de progression se remplit jusqu'à l'étape choisie.
4. 01 Hello World : bento avec photo devant l'ordi (effet bichromie rose/nuit), présentation, « Var, France », parcours (dessinatrice-projeteuse → chargée d'études → cheffe de projets → développeuse web).
5. 02 Projets : 3 cartes projets, sans filtres sur l'accueil. La carte de Léa Grondin contient un comparateur avant/après glissable. Les étiquettes parlent du type de site, jamais de la techno. Bandeau rose pleine largeur « Le vôtre ? ». Le bouton « voir tous les projets » n'apparaît qu'au-delà de 6 projets. Témoignage en dessous. La flèche de chaque carte mène à une page `/projets` qui regroupe tous les projets ; cette page n'est pas dans le menu, on y accède uniquement par ces boutons. C'est sur `/projets` que se trouvent les filtres (tous, création, refonte, site vitrine, application web), avec leur état dans l'URL (`/projets?type=refonte`) et un bouton pour copier le lien.
6. 03 Offres : Création de site, Refonte, Suivi et maintenance (tarifs à compléter).
7. 04 FAQ : 5 questions en accordéon.
8. 05 Parlons-en : bloc Calendly à gauche (2/3), formulaire à droite (nom et prénom, e-mail, type de projet, message, bouton pleine largeur) + lien LinkedIn. Appel découverte : 30 minutes, en visio uniquement (lien envoyé à la prise de rendez-vous).
9. Footer : logo long avec slogan, accroche, disponibilité, navigation, contact, réseaux, mentions légales, confidentialité, interrupteur des pétales, retour en haut.
10. Fil conducteur à droite : il remplace la barre de défilement native (masquée sur desktop, conservée sur mobile). Fixé sur toute la hauteur de l'écran, le point lumineux est à X % du rail quand on est à X % de la page ; on peut le glisser, cliquer sur le rail pour y sauter, ou cliquer sur le repère numéroté d'une section. Pendant le défilement, une étiquette « 02 — Projets » accompagne le point. Masqué sur mobile.

Toutes les animations respectent `prefers-reduced-motion`.

## Assets

- `assets/logos/` : logo long sans slogan (nav si besoin) et avec slogan (footer), en blanc pour le thème sombre et en noir pour le clair, plus la fleur `sakura-accueil.webp`.
- `assets/photos/` : `laura-hero-detouree.webp` (accueil, déjà détourée et fondue), `laura-ordi.jpg` (bento), `laura-portrait-bleu.jpg` (avatar du bloc Calendly).
- Favicon (fond bleu) : déjà prêt dans `../0_D.A Flaura.dev/favicon/`.
- Les SVG d'origine dans `0_D.A Flaura.dev` sont des exports Canva très lourds (jusqu'à 12 Mo) : ne pas les utiliser tels quels sur le site.

## Contenu à compléter (ne rien inventer)

Tout ce qui est entre crochets dans la maquette reste à fournir : tarifs, durée de l'appel découverte, lien Calendly, adresse e-mail, SIRET, lien GitHub, témoignage de Léa, problème et résultat de chaque projet, captures avant/après du site de Léa, visuels des projets. Tant que ce n'est pas fourni, garde un emplacement visible, n'invente ni chiffre ni avis client.

## SEO / accessibilité

Balises sémantiques, un seul `h1`, métadonnées et Open Graph, données structurées (LocalBusiness / Person), textes alternatifs sur les images, contrastes AA, navigation au clavier, cibles tactiles d'au moins 44 px.
