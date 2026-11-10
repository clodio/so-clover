# So Clover !

Version web française de So Clover, jouable à deux joueurs dans un salon partagé par code ou lien.

## Jouer en local

Ouvrez `index.html` dans un navigateur. Le mode **Tester la phase résolution (debug)** permet de tester le plateau sans second joueur ni connexion Supabase.

## Déployer sur GitHub Pages

Le workflow `.github/workflows/deploy-pages.yml` publie automatiquement `index.html` sur GitHub Pages à chaque push sur `main` (ou manuellement depuis l’onglet **Actions**).

Dans **Settings → Pages**, choisissez **GitHub Actions** comme source de déploiement. Une fois le workflow terminé, GitHub affiche l’URL du site dans **Settings → Pages**.

## Multijoueur et Supabase

Les joueurs utilisent Supabase Realtime Broadcast et Presence sur un canal public nommé à partir du code du salon. Aucune table ni migration SQL n’est nécessaire. Les propositions sont conservées uniquement en mémoire pendant la session et renvoyées jusqu’à ce que l’autre joueur les reçoive, afin de tolérer une course de connexion.

La clé utilisée dans le navigateur doit être une clé publique `publishable` (ou `anon`) ; ne placez jamais de clé `secret` ou `service_role` dans le site. Les personnes ayant le code du salon peuvent rejoindre et recevoir les plateaux de cette partie.