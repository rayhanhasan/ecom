# Résumé du projet — 07/11/2026

## Projet
- Marque de veste de pluie qui change de couleur, vendue en **drop** : précommande de 4 jours, stock réel limité, ≤ 119 € TTC.
- **Une seule page de vente.**
- DA : nuit / néon, étoile inspirée de Meridian.
- Cible (hypothèse, non validée) : 2-roues urbains de 20 à 35 ans, arrivée depuis TikTok sur mobile.

## Logistique (décision de Rayhan)
Précommandes → une commande groupée livrée chez Rayhan → expédition aux clients par Rayhan.
- Il faut un numéro **EORI** (gratuit, douane).
- À l'import : droits ≈ 12 % (à confirmer, TARIC 6201/6202) + TVA d'import. Les forfaits 3 € + 2 € ne concernent que les petits colis envoyés au client.
- Envoi en France : ≈ 5–8 € par colis (estimation).
- Coûts à recalculer avec un devis de fret.

## Produit
| | Fluo « splash » | Léopard |
|---|---|---|
| Déclencheur | Température (thermochrome) | Eau (hydrochrome) |
| Effet | Néon vif sur noir, très fort en vidéo | Net sur kaki, discret sur noir |
| Risque | Peut changer de couleur par temps froid sans pluie | — |

- **Choix : fluo, si elle passe le test de froid.** La léopard est le plan B ou le drop 02.
- Imperméabilité prouvée sur aucune des deux : ne pas écrire « imperméable » sans test.

## Fournisseurs (liens : `LIENS.md`)
- **Fluo** : 1688, de 165 à 188 ¥ (≈ 22–25 €) dès 1 pièce (钻意, 红头船…). Ou Alibaba Yuehao, 21,20 € dès 50 pièces.
- **Léopard** : 1688 款款爆, 95 ¥ (12,75 €) dès 1 pièce.
- **AliExpress** : revendeurs, ≈ 53 € + 15 € de port. À éviter.
- Achat via **Superbuy** (1688) ; **Jingsourcing** à partir de 150 pièces ou avec logo.

## Import en gros chez Rayhan (estimations, à confirmer par devis)
- Express UPS/FedEx/DHL, taxes payées à l'arrivée, avec ta société comme importatrice (EORI + n° TVA). **12 % de droits + TVA.** Les forfaits 3 € + 2 € ne s'appliquent pas.
- Coût livré chez toi : léopard ≈ 26 € ; fluo Alibaba ≈ 33 € (50 pièces).
- Envoi au client : Mondial Relay 5,99 € TTC.
- Démarches : EORI, n° de TVA, adhésion Refashion (≈ 0,58 € par pièce), étiquettes conformes, test sans PFAS.
- Délai réel de 3 à 4 semaines à afficher en précommande.

## Marge à 119 € TTC (modèle envoi direct, estimations)
- Fluo usine : ≈ 41 € livrée → ≈ 50 € de marge par veste.
- Léopard : ≈ 34 € → ≈ 58 €.
- AliExpress : ≈ 73 € → ≈ 19 €.

## Légal (à valider par un juriste)
- Compteur et stock réels.
- Prix barré = prix le plus bas des 30 derniers jours.
- Date de livraison affichée en précommande.
- Pas de « protection », « CE » ni « homologué ».
- PFAS interdits.
- Composition sur l'étiquette.

## Site
Boutique : **Shopify Basic + thème une page sur mesure** (pas de Google Pay en France chez Shopify). Coût fixe ≈ 27 €/mois, ≈ 100 € le mois d'un drop. Détails : `research/stack/stack-ecom.md`.

Une page avec, dans l'ordre :
1. Hero : vidéo de nuit.
2. Compteur de temps et stock réel.
3. Slider sèche / mouillée.
4. Fiche technique.
5. Tailles.
6. Date de livraison.
7. FAQ.
8. Bouton collant.

Planches dans `research/sections/planches/`. En attente de validation, section par section.

## Prochaines étapes (priorité : produit)
1. Commander les échantillons : fluo AliExpress, léopard, échantillon Yuehao.
2. Test : 5 °C à sec pendant 30 min, eau à 15 °C, eau à 25 °C, 3 lavages.
3. Messages fournisseurs (Yuehao, agent 1688) : Claude les rédige.
4. Devis de fret groupé vers chez Rayhan, EORI, n° de TVA, Refashion.
5. Ensuite : stratégie de contenu.

## Fichiers
- `research/simulateur-cout-veste.xlsx`
- `research/sourcing/` (fluo, léopard, annonces)
- `research/produit/`
- `research/moodboard/`
- `research/sections/`
