# Sonde externe d'OncoIDE

Une vérification toutes les dix minutes, hébergée par GitHub, donc en dehors
des deux hébergeurs d'OncoIDE (Vercel et Supabase) :

| Vérification | Adresse | Attendu |
|---|---|---|
| Application | `https://app.oncoide.fr/` | la page et sa racine `#root` |
| API | `https://app.oncoide.fr/api/health?leger=1` | `"status":"ok"` |
| Site public | `https://www.oncoide.fr/` | la page d'accueil |
| Authentification | `https://urirsoxmuhadrpjyhjlq.supabase.co/auth/v1/health` | réponse du service |

Chaque vérification est rejouée une fois, vingt secondes plus tard, avant de
compter comme un échec. En cas d'échec, la tâche échoue et **GitHub envoie un
courriel au propriétaire du dépôt** (réglage par défaut : *Settings →
Notifications → Actions → failed workflows*).

Elle complète, sans la remplacer, la surveillance décrite sur
[www.oncoide.fr/statut](https://www.oncoide.fr/statut) : celle-ci mesure la
disponibilité et la publie ; cette sonde ne sert qu'à prévenir quand Vercel et
Supabase tombent en même temps, le seul cas que les deux autres chemins
d'alerte ne couvrent pas.

Aucun secret : la clé Supabase utilisée est la clé publiable, servie
publiquement par le site. Les horaires de GitHub Actions ne sont pas garantis :
un passage peut être retardé de quelques minutes.

Éditeur : ONCOIDE SASU — support@oncoide.fr
