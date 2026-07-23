# AAURSI // Terminal d'accès

Terminal ARG fond noir / police blanche pour la saga. Comptes en mode démo
(stockage local, un seul appareil), et VX (l'IA du lore) qui répond
vraiment, via Groq, à travers une Netlify Function.

## Structure

```
index.html                   Page du terminal
style.css                    Style (thème terminal)
script.js                    Logique : commandes, comptes locaux, appel à VX
netlify/functions/vx.js      Fonction serveur qui appelle Groq (clé API cachée)
netlify.toml                 Config Netlify
```

## Déploiement sur Netlify

1. Pousse ce dossier sur un repo GitHub (ou glisse-dépose le dossier
   directement sur app.netlify.com → "Deploy manually").
2. Sur Netlify : **Site settings → Environment variables**, ajoute :
   - `GROQ_API_KEY` = ta clé API Groq (`gsk_...`)
3. Déploie. Netlify détecte automatiquement `netlify.toml` et publie
   `netlify/functions/vx.js` comme fonction serverless sur
   `/.netlify/functions/vx`.

Aucune autre configuration n'est nécessaire : pas de base de données,
pas de build step.

## Tester en local

Avec la CLI Netlify (recommandé, pour que la fonction fonctionne aussi) :

```bash
npm install -g netlify-cli
netlify dev
```

Puis exporte ta clé avant de lancer, ou crée un fichier `.env` à la racine :

```
GROQ_API_KEY=gsk_xxxxxxxxxxxxxxxx
```

`netlify dev` sert le site sur `http://localhost:8888` et proxy les appels
vers `/.netlify/functions/vx`.

> ⚠️ Si tu ouvres juste `index.html` dans le navigateur (sans `netlify dev`
> ni déploiement), les commandes du terminal fonctionnent mais `msg VX`
> échouera : il n'y a pas de fonction serveur qui tourne pour appeler Groq.

## Commandes du terminal

| Commande | Effet |
|---|---|
| `sinn [email] -u [utilisateur] -psw [mdp]` | Crée un compte local (1 par appareil) |
| `login -u [utilisateur] -psw [mdp]` | Se reconnecter |
| `logout` | Se déconnecter |
| `whoami` | Affiche la session active |
| `msg VX "message"` | Parle à VX (connexion requise) |
| `surveillance` | Affiche le niveau de suspicion et le journal des dernières commandes |
| `clear` | Efface l'écran |
| `help` | Liste les commandes |

## Surveillance VX

Chaque commande tapée est journalisée localement (dans `localStorage`,
100 dernières entrées) et fait légèrement grimper un "niveau de
suspicion" (0 à 100) :

- une commande inconnue, ou `clear`, ou un mot lié au lore classifié
  (`paradoxe`, `access`, `p-r`, `delta`, etc.) fait monter le niveau
  plus vite ;
- au-delà d'un certain seuil, VX peut **intervenir sans qu'on lui parle**,
  avec un message discret préfixé `[VX — SURVEILLANCE]`, dont le ton
  devient de plus en plus froid à mesure que la suspicion augmente ;
- la commande `surveillance` permet à l'utilisateur de voir ce que VX a
  concrètement enregistré sur lui (transparence volontaire du "jeu") ;
- quand on parle à VX avec `msg VX`, le niveau de suspicion et les
  dernières commandes tapées sont transmis à Groq comme contexte, pour
  que VX les mentionne naturellement et adapte son ton en conséquence.

Rien de tout ça n'est envoyé où que ce soit sauf au moment d'un `msg VX`
(et uniquement vers ta propre fonction Netlify → Groq).

## Personnaliser VX

Le "caractère" de VX (ton, ce qu'elle sait, ce qu'elle refuse de dire) est
entièrement défini dans `VX_SYSTEM_PROMPT` en haut de
`netlify/functions/vx.js`. Modifie ce texte pour affiner sa personnalité
ou ajouter des éléments de lore au fur et à mesure que la saga avance.

## Sécurité

- Les mots de passe sont hashés (SHA-256) avant stockage dans le
  `localStorage` du navigateur — c'est un mode démo, pas un vrai système
  d'authentification, ne pas réutiliser pour des données sensibles.
- La clé Groq ne quitte jamais le serveur : le navigateur appelle
  uniquement `/.netlify/functions/vx`, qui elle-même appelle Groq.
