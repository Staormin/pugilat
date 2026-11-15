# Pugilat

Jeu de combat en plateforme, simple et nerveux, dans une seule page HTML.

- **Local** : 2 joueurs sur le même clavier ou manettes, ou contre l'ordinateur.
- **En ligne** : jusqu'à 4 joueurs en pair-à-pair (WebRTC via [PeerJS](https://peerjs.com)), sans serveur de jeu.
  Entrez le même nom de salon, ou partagez le lien `…/#nom-du-salon`.

## Contrôles

| Action | Joueur 1 / en ligne | Joueur 2 | Manette |
|---|---|---|---|
| Bouger | Q D (A D en QWERTY) | ← → | Stick / croix |
| Sauter (×2) | Z (W) | ↑ | A |
| Descendre / chute rapide | S | ↓ | Bas |
| Attaque (+ direction) | F | K | X |
| Spécial : smash, ↑ remontée, ↓ piqué | G | L | B / Y |
| Esquive | H | M | Gâchettes |

## Réseau

Le premier joueur d'un salon prend l'identifiant `pugilat-v1-<salon>` sur le serveur PeerJS public et sert
d'annuaire ; chaque nouveau joueur se connecte ensuite directement à tous les autres. Chacun simule son propre
personnage (aucune latence sur ses commandes) et diffuse son état ~30 fois par seconde ; l'attaquant détecte
ses coups, la victime calcule son éjection avec ses propres dégâts.

Limites connues : sur certains réseaux stricts (entreprise, certains partages 4G) la connexion directe échoue
faute de serveur relais TURN ; si le premier joueur quitte, les nouveaux arrivants ne retrouvent plus le salon
(tout le monde doit le rejoindre à nouveau).

## Lancer en local

```bash
python3 -m http.server 8765
```
