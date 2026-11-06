Formule Notion qui affiche l'XP gagné dans le niveau en cours, le palier à atteindre et une barre de progression visuelle. Les niveaux suivent une courbe progressive : plus on monte, plus chaque palier demande d'XP.

### Rendu

```
✨ XP: 120 / 200
▰▰▰▰▰▰▱▱▱▱ 60 %
```

### Courbe de niveaux
Capture barre d'XP.jpg
Niveau = `floor(sqrt(raw_xp / 200)) + 1`

| Niveau | XP total requis | XP à gagner pour ce palier |
|---|---|---|
| 1 | 0 | 200 |
| 2 | 200 | 600 |
| 3 | 800 | 1 000 |
| 4 | 1 800 | 1 400 |
| 5 | 3 200 | 1 800 |

Chaque niveau demande 400 XP de plus que le précédent.

### Fonctionnement

1. **Palier du niveau** : `200 * (2 * raw_level - 1)`, soit l'XP nécessaire pour passer au niveau suivant.
2. **XP du niveau courant** : `raw_xp` (XP total cumulé) moins l'XP des niveaux précédents, `200 * (raw_level - 1)²`.
3. **Pourcentage** : XP du niveau divisé par le palier, plafonné à 100 %.
4. **Barre** : 10 cases, chacune valant 10 % (`▰` pleine, `▱` vide).

### Formule

```
lets(
  palier, 200 * (2 * raw_level - 1),
  xp, raw_xp - 200 * pow(raw_level - 1, 2),
  pct, min(xp /

