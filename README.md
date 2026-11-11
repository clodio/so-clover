# So Clover !

Version web française de So Clover, jouable à deux joueurs dans un salon partagé par code ou lien.

## Jouer en local

Ouvrez `index.html` dans un navigateur. Le mode **Tester la phase résolution (debug)** permet de tester le plateau sans second joueur ni connexion Supabase.

## Déployer sur GitHub Pages

Le workflow `.github/workflows/deploy-pages.yml` publie automatiquement `index.html` sur GitHub Pages à chaque push sur `main` (ou manuellement depuis l’onglet **Actions**).

Dans **Settings → Pages**, choisissez **GitHub Actions** comme source de déploiement. Une fois le workflow terminé, GitHub affiche l’URL du site dans **Settings → Pages**.

## Multijoueur et Supabase

Les joueurs utilisent Supabase Realtime Broadcast et Presence sur un canal public nommé à partir du code du salon. Aucune table ni migration SQL n’est nécessaire. Un salon est considéré actif tant que son créateur est connecté ; les liens vers un salon absent ou fermé sont refusés. Les propositions sont renvoyées jusqu’à ce que l’autre joueur les reçoive, afin de tolérer une course de connexion. Après l’envoi de son plateau, un joueur est ramené à l’accueil si l’autre plateau n’arrive pas en 10 minutes.

Les plateaux envoyés et reçus sont sauvegardés dans le stockage local du navigateur. Le bouton **Rejouer un plateau sauvegardé** sur l’accueil ouvre l’historique ; pendant la résolution, **Passer cette énigme** charge un autre plateau sauvegardé. Une victoire propose également de résoudre une autre énigme ou de retourner à l’accueil. L’historique reste propre au navigateur et n’est pas synchronisé entre appareils.

La clé utilisée dans le navigateur doit être une clé publique `publishable` (ou `anon`) ; ne placez jamais de clé `secret` ou `service_role` dans le site. Les personnes ayant le code du salon peuvent rejoindre et recevoir les plateaux de cette partie.