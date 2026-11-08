# Stack e-commerce : drop en précommande (veste qui change de couleur)

Recherche du 08/11/2026. Prix relevés ce jour sauf mention contraire.
**(E)** = estimation. **(NV)** = non vérifié sur une source officielle.
Note proxy : la connexion sortait hors de France. Les pages officielles Shopify, Klaviyo, Brevo, Omnisend et Axeptio affichaient des **USD**. Pour Shopify et Brevo en euros, les montants viennent de sources françaises datées. Stripe (`/fr`), Alma, Sendcloud et La Poste affichaient des euros.

---

## 1. Recommandation

**Shopify Basic avec un thème Liquid one-page fait sur mesure. Pas de headless.**

- Le paiement par carte coûte autant que Stripe (1,5 % + 0,25 €). En plus, tu as la gestion des commandes, les remboursements, les e-mails, les étiquettes, Klarna, PayPal 4X, Apple Pay, Shop Pay, et Meta CAPI en natif.
- Le thème Liquid laisse une liberté totale sur la page de vente. Le headless n'apporte rien de plus pour une page unique : le checkout reste celui de Shopify et tu paies Vercel en plus.
- Limite principale : **Google Pay n'est pas disponible pour les marchands Shopify situés en France** (centre d'aide Shopify). Or Android pèse environ 67 % du trafic mobile en France (StatCounter, juin 2026). Les visiteurs Android paient par carte, avec le remplissage automatique de Chrome, ou par PayPal.
- **Plan B** si Google Pay, un stock partagé entre toutes les tailles ou un early access verrouillé côté serveur deviennent indispensables : Next.js + Stripe Checkout + Supabase (voir §4).

| Brique | Outil | Prix |
|---|---|---|
| Boutique | Shopify Basic | 36 €/mois en mensuel, 27 €/mois en annuel (relevé Kanal du 29/09/2026). Offre de lancement : 1 €/mois pendant 3 mois |
| Thème | Thème custom basé sur [Skeleton theme](https://shopify.dev/changelog/skeleton-theme-is-now-available) (officiel, MIT) | 0 € (ton temps) |
| Paiement | Shopify Payments : CB/Visa/MC/Amex, Apple Pay, Shop Pay, PayPal (4X inclus), Klarna | Voir §8 |
| Précommande | Natif (stock + propriété de ligne « Livraison prévue ») ; STOQ Lite ou Timesact si besoin d'acompte | 0 $ / 10 $ / 23 $ par mois |
| E-mail + SMS | Klaviyo (formulaires de liste d'attente, segment early access, retour en stock pour le drop 02) | Gratuit jusqu'à 250 profils, puis 30 $ (1 000) / 60 $ (2 500) / 100 $ (5 000) par mois + SMS ≈ 0,07 $ (E) |
| Livraison | Shopify Shipping (Mondial Relay, Colissimo). Alternatives : Boxtal, Sendcloud Free | 0 € d'abonnement |
| Cookies (CMP) | Consentmo Standard (Consent Mode v2 + consentement des pixels Meta et TikTok) | 10 $/mois (offre gratuite possible) |
| Pixels + CAPI | Apps Facebook & Instagram (partage « Maximum »), TikTok, Google & YouTube | 0 € |
| Avis | Judge.me Free, **après la première livraison** (aucun avis possible pendant le drop 01) | 0 € |
| Analytics | Shopify Analytics + GA4 + Microsoft Clarity (avec consentement) | 0 € |
| Légal | Générateur de CGV + relecture par un juriste, médiateur de la consommation | Générateur dès 4,90 € par document ou 34,90 € HT ; médiateur ≈ 40-50 €/an (NV) |

**Coût fixe pendant un mois de drop** (2 500 profils) : **36 € + ~80 $** (Shopify, Klaviyo, Consentmo, STOQ), soit environ **105-110 €/mois (E, taux de change non vérifié)**, plus les SMS consommés.
**Coût variable par commande à 119 €** : environ **2,04 €** en carte ou wallet, **3,80 €** en PayPal, **6,29 €** en Klarna. Avec Mondial Relay au tarif public de 5,99 €, ça donne **≈ 9-10 € par commande, emballage compris (E)**.

---

## 2. Comparatif des architectures

| Critère | A. Shopify + thème Liquid custom | B. Headless (Next.js/Vercel + Storefront API, checkout Shopify) | C. Next.js + Stripe Checkout + Supabase |
|---|---|---|---|
| Conversion et confiance au checkout | Checkout Shopify : Shop Pay, Apple Pay, PayPal (4X), Klarna. **Pas de Google Pay en France** | Identique à A | Stripe Checkout : Apple Pay, **Google Pay**, Link, PayPal, Klarna, Alma. Pas de Shop Pay |
| Vitesse mobile | Bonne : CDN Shopify, page légère si tu maîtrises le thème | Très bonne sur la page, puis redirection vers le checkout Shopify | Très bonne |
| Liberté de design | Totale sur la page. Checkout : branding seulement (« Limitée » hors Plus) | Totale sur la page. Checkout comme A | Totale. Checkout hébergé = branding Stripe (Elements = 100 % custom, mais plus de travail) |
| Gestion des commandes | Native : commandes, remboursements, étiquettes, retours, e-mails | Native (admin Shopify) | **À construire** : Stripe Dashboard + table Supabase + export vers l'outil d'étiquettes |
| Conformité précommande | Date de livraison via propriété de ligne (visible dans le checkout et les e-mails), stock natif, retours en libre-service comme base du bouton de rétractation | Idem A, mais les widgets d'apps ne s'affichent pas : tout passe par API | Tout à coder (date, e-mails, bouton de rétractation, accusé de réception), avec contrôle total |
| Stock réel (150) | Stock par variante : allocation par taille, ou astuce « taille en propriété de ligne » pour un pool unique par couleur | Idem A | Pool atomique dans Postgres, réservation pendant la session Checkout |
| Early access 24 h | Mot de passe boutique envoyé à la liste d'attente (simple ; fuite possible) | Verrouillage serveur possible (token privé côté serveur) | Liens signés et limite par e-mail |
| Effort | Faible à moyen | Moyen à élevé | Élevé : environ 2-4 semaines à temps partiel (E) |
| Fixe mensuel | 27-36 € + apps | 27-36 € + Vercel Pro 20 $ + apps | Vercel Pro 20 $ + Supabase Pro 25 $ (Free possible, avec risque de pause) + outil e-mail |
| Variable (carte EEE) | 1,5 % + 0,25 € = 2,04 € | 2,04 € | 1,5 % + 0,25 € = 2,04 € (premium EEE : 2,8 % + 0,25 € = 3,58 €) |

Verdict : **A**. B coûte plus cher et demande plus de travail sans gain au checkout. C ne se justifie que si Google Pay, le pool unique ou un early access étanche priment sur le temps de construction et d'exploitation.

---

## 3. Shopify en détail

### Forfaits (France)
| Forfait | Mensuel | Annuel (par mois) | Carte EEE (Shopify Payments) | Amex / carte internationale | Frais si passerelle tierce |
|---|---|---|---|---|---|
| Basic | 36 € | 27 € | 1,5 % + 0,25 € | 2,7 % + 0,25 € | 2 % |
| Grow | 105 € | 79 € | 1,3 % + 0,25 € | 2,6 % + 0,25 € | 1 % |
| Advanced | 384 € | 289 € | 1,1 % + 0,25 € | 2,4 % + 0,25 € | 0,6 % |

- Prix en euros : relevé Kanal du 29/09/2026 d'après shopify.com/fr/tarifs. HT ou TTC non précisé. La page officielle, vue via le proxy le 08/11/2026, affiche 39 $ en mensuel et 29 $ en annuel pour Basic.
- Taux Shopify Payments FR : Kanal, relevé du 07/10/2026. PayPal (wallet) : à partir de 2,9 % + 0,35 €. Klarna : 4,99 % + 0,35 € (Basic à Advanced). Rétrofacturation : 15 €. Versements à J+3.
- Basic suffit (Grow ne devient rentable qu'au-delà d'environ 300-400 k€/an de CA en carte : 0,2 point d'écart contre 624 à 828 €/an de surcoût, (E)). Basic inclut 1 boutique headless et la personnalisation du checkout « Limitée » (page tarifs officielle).
- **Starter** : « n'est pas disponible pour les nouvelles boutiques ». Avec ce forfait : thème Spotlight uniquement, pas de collections, pas de nouveaux modèles de page (centre d'aide, 08/11/2026). **Inutilisable ici.**
- **Shop Pay Installments** : non disponible en France (Kanal, 19/10/2026). Le paiement en plusieurs fois passe par Klarna ou PayPal 4X.
- **Google Pay** : « n'est pas disponible pour les marchands situés en France » (centre d'aide Shopify, page Moyens de paiement France, 08/11/2026).
- **Shopify Tax** : franchise d'environ 100 k€ de ventes, puis 0,25 % plafonné à 0,99 € par commande (NV ; les sources divergent pour les boutiques créées après le 13/05/2026). Sans impact au volume d'un drop.
- **Pause and Build** : 9 $/mois, vitrine en ligne mais checkout désactivé. Utile entre deux drops (conditions d'éligibilité à vérifier).

### Apps de précommande (App Store, 08/11/2026, prix en USD)
| App | Prix | Acompte / paiement partiel | Date de livraison | Limite de quantité | Coût pour 150 précommandes à 119 € |
|---|---|---|---|---|---|
| PreProduct (4,9/5, 108 avis) | Starter gratuit **+ 5 % du CA précommandé** ; Scale 99,99 $/mois (0 % jusqu'à 5 k$ par mois, puis 0,5 %) | Oui (débit maintenant, plus tard sur carte enregistrée, ou acompte) | Oui (« Availability date ») | Oui (« Order limits »), headless supporté | Starter : **892,50 €** ; Scale : ≈ 160 $ (E) |
| Timesact (5,0/5, 2 136 avis) | Gratuit pour 20 commandes/mois ; CORE Flex 5 $ + 0,20 $ par commande au-delà de 30 ; CORE Fixed 23 $/mois en illimité (tarif Basic) | Oui (CORE et plus) | Oui (« shipping dates ») | Oui (« presale order limits ») | 23 $ (Fixed) ou ≈ 29 $ (Flex) |
| STOQ (5,0/5, 3 915 avis) | Gratuit pour 10 précommandes/mois ; Lite 10 $ (100 précommandes, puis 0,25 $ l'unité) ; Pro 29 $ (400) ; Unlimited 69 $ | Oui (acompte, paiement partiel) | Oui (« ship dates ») | Oui (« limits ») | 22,50 $ (Lite) ou 29 $ (Pro) |
| PreOrder Globo, Amp, Dibs, Purple Dot… | Non vérifiés | | | | |

Mon avis :
- **Encaisse 100 % à la commande, sans acompte.** En droit français, une somme versée d'avance est un acompte, sauf mention « arrhes ». Le paiement partiel complique la vente, les remboursements et les litiges.
- **Dans ce cas, pas besoin d'app.** Configuration :
  - stock suivi et « Continuer à vendre en cas de rupture » désactivé ;
  - ajout au panier en AJAX avec la propriété `Livraison prévue : JJ/MM/AAAA`, qui s'affiche dans le panier, le checkout, la commande et l'e-mail ;
  - modèle d'e-mail de confirmation modifié en Liquid ;
  - tag « précommande » posé par Shopify Flow.
- **Si tu veux un acompte ou un débit à l'expédition** : Timesact CORE Fixed ou STOQ. **Évite PreProduct Starter** : sa commission de 5 % est bien trop chère à ce volume.

### Compte à rebours et compteur de stock réel
- Compte à rebours : en JS dans le thème, gratuit. Il doit correspondre à la vraie date de fin. Annoncer à tort qu'un produit ne sera disponible que très peu de temps est une pratique réputée trompeuse (art. L121-4 C. conso).
- Compteur : somme `variant.inventory_quantity` en Liquid, rafraîchie toutes les 10-15 s par la Section Rendering API (`/?sections=stock-counter`). Autre option : Storefront API `quantityAvailable`, qui demande le scope `unauthenticated_read_product_inventory`.
- Shopify ne réserve pas le stock au panier. Le contrôle se fait au paiement : à 0, le checkout refuse la vente, donc pas de survente.
- **Stock partagé de 150 pièces** : le stock Shopify est géré par variante. Deux options :
  - (a) allouer un stock par taille (XS-XXL) ;
  - (b) une variante par couleur, avec stock 150, et la taille en propriété de ligne obligatoire : vrai pool unique, mais tailles absentes des rapports natifs.
  Comme la commande usine est groupée après le drop, (b) colle mieux au modèle.

### Faisabilité du thème Liquid custom
- Online Store 2.0 : sections JSON, page unique en `index.json`.
- Partir du Skeleton theme officiel avec Shopify CLI (`shopify theme init` / `theme dev`). Vidéo hero sur le CDN Shopify Files.
- Bouton collant : ajout AJAX puis redirection directe vers `/checkout` pour sauter le panier.
- Checkout : logo, couleurs et polices via l'éditeur (pas de `checkout.liquid` hors Plus).

---

## 4. Headless et option sans Shopify

### B. Next.js sur Vercel + Storefront API (ou Hydrogen/Oxygen)
- Pour : DX React, contrôle fin du rendu, early access verrouillable côté serveur.
- Contre :
  - le checkout reste Shopify, donc mêmes moyens de paiement et toujours pas de Google Pay ;
  - les extensions de thème des apps (widgets de précommande, Judge.me, formulaires) ne s'affichent pas, il faut tout intégrer par API ;
  - les pixels du site sont à poser toi-même (les apps Meta et TikTok couvrent surtout le checkout) ;
  - Vercel Hobby est **interdit en usage commercial** (« restricted to non-commercial personal use only », Vercel, fair use au 14/09/2026), donc Vercel Pro à **20 $/mois**.
- Hydrogen/Oxygen : inclus dans les forfaits, mais Remix plutôt que Next, et même contrainte sur le checkout.
- Verdict : **pas rentable pour une seule page.**

### C. Next.js + Stripe Checkout + Supabase
**Frais Stripe France** (stripe.com/fr/pricing, en euros, 08/11/2026) :

| Moyen | Frais |
|---|---|
| Carte EEE standard | 1,5 % + 0,25 € |
| Carte EEE premium | 2,8 % + 0,25 € |
| Carte britannique | 2,5 % + 0,25 € |
| Carte internationale | 3,15 % + 0,25 € |
| Klarna (France) | 4,99 % + 0,40 € |
| Alma 2x / 3x / 4x | 3,9 % / 4,5 % / 5,85 % + 0,30 € |
| PayPal | 0,2 % + 0,10 € **en plus** des frais PayPal |
| Litige | 20 € |
| Checkout et Payment Links | Inclus. Domaine personnalisé : 10 $/mois |

**Ce que tu gagnes :**
- Google Pay ;
- un pool de stock atomique (réservation en transaction Postgres, libération sur `checkout.session.expired`, la session expire au minimum après 30 min) ;
- un early access par lien signé ;
- une limite par client ;
- 0 abonnement e-commerce.

**Ce que tu perds, donc à construire ou à brancher :**
- un back-office de commandes (statuts, export vers Sendcloud ou Boxtal) ;
- les e-mails transactionnels (confirmation avec date de livraison, expédition, retard) ;
- le **bouton de rétractation** et son accusé de réception ;
- les retours et remboursements (Stripe Dashboard, à la main) ;
- les factures (Stripe post-paiement à 0,4 %, plafonné à 2 $, ou génération maison) ;
- l'export comptable et TVA ;
- l'écosystème d'apps (avis, CMP) et le CAPI côté serveur, à coder depuis les webhooks Stripe.

**Fixe** : Vercel Pro 20 $ + Supabase Pro 25 $. Supabase Free met les projets en pause après 1 semaine d'inactivité et se limite à 2 projets actifs.

---

## 5. Autres pistes 2026 (crédibles)
- **Storefront Web Components** (`<shopify-store>`, `<shopify-cart>`, `<shopify-checkout>`) : panier et checkout Shopify intégrables dans n'importe quelle page (par ex. une landing Next.js) sans écrire de requêtes Storefront API. `shopify-checkout` est en **Developer Preview** et n'est pas couvert par le support Shopify. Pas pour un premier drop.
- **Shopify Email** : 10 000 e-mails/mois gratuits sur Basic. Mais **pas de SMS vers la France** via Shopify Messaging (Kanal, 07/10/2026).
- **Starter** : fermé aux nouvelles boutiques (voir §3).

---

## 6. Outils recommandés (France)

### E-mail et SMS (liste d'attente de 1 000 à 5 000 contacts)
| | Klaviyo | Brevo | Omnisend |
|---|---|---|---|
| Prix pour 1 000 / 2 500 / 5 000 | E-mail : **30 / 60 / 100 $** par mois (profils actifs ; slider officiel, 08/11/2026). Gratuit : 250 profils, 500 e-mails, 5 $ de SMS | Starter 14 / 21 / 35 € HT ; Standard 29 / 41 / 62 € HT (Kanal, 29/10/2026, 5 e-mails par contact et par mois) | Standard : 44 $ à 2 500 ; Pro : 59 $ jusqu'à 2 500 (Kanal, 24/10/2026) |
| SMS France | Tarif par message visible seulement dans le compte depuis juillet 2026. Blog Klaviyo : « ≈ 0,07 $US (≈ 0,065 €) » par SMS (03/08/2026) | 4,5 crédits par SMS ≈ **0,045 €** (packs sans expiration ; Kanal, 24/10/2026) | 0,063 à 0,049 $ selon le volume. **SMS réservé à Pro** pour les comptes créés depuis le 04/05/2026 |
| Intégration Shopify | Native et bidirectionnelle (4,7/5, 3 421 avis au 29/10/2026) | Via l'app PushOwl by Brevo (l'app « Brevo » était indisponible au 06/11/2026) | Native |

- **Choix : Klaviyo.** Une seule base de consentement e-mail + SMS, segment « liste d'attente → early access » propre, flows de retour en stock pour le drop 02, et synchronisation des audiences Meta et TikTok plus tard.
- **Alternative économique** : Shopify Email (gratuit) + crédits SMS Brevo (≈ 0,045 €).
- Budget SMS (E) : 1 500 abonnés SMS × 2 envois (ouverture early access et dernières 24 h) = 3 000 SMS, soit ≈ 210 $ chez Klaviyo ou ≈ 135 € chez Brevo.
- SMS marketing : consentement préalable obligatoire et mention STOP.

### Paiement en 3 ou 4 fois (pour 119 €)
| Solution | Frais commerçant | Coût par commande |
|---|---|---|
| **PayPal 4X** | Inclus dans le tarif PayPal : 2,90 % + 0,35 € (grille FR du 15/07/2026). Via Shopify : « à partir de 2,9 % + 0,35 € » | **3,80 €** |
| **Klarna** (via Shopify Payments) | 4,99 % + 0,35 € | **6,29 €** |
| Klarna (via Stripe) | 4,99 % + 0,40 € | 6,34 € |
| Alma en direct | 3x : 3,80 % HT ; 4x : 4,80 % HT (almapay.com, 08/11/2026). Sur Shopify, c'est une app de paiement tierce : **+2 % de frais Shopify sur Basic** | 3x : 4,52 € HT + 2,38 € = **6,90 €** ; 4x : 8,09 € |
| Alma (via Stripe) | 3x : 4,5 % + 0,30 € ; 4x : 5,85 % + 0,30 € | 5,66 € / 7,26 € |

- **Choix : PayPal (4X inclus) + Klarna** via Shopify Payments. Pas d'Alma sur Shopify Basic, à cause des 2 % de frais tiers.
- **Attention au 20/11/2026** : le paiement fractionné et le BNPL entrent dans les règles du crédit à la consommation (directive 2023/2225). Demande par écrit à Klarna et PayPal les mentions à afficher avant de mettre en avant le « 3x/4x ».

### Livraison depuis chez toi (veste de 0,7 kg + emballage = tranche ≤ 1 kg)
| Service | Tarif public TTC 2026 |
|---|---|
| **Mondial Relay, point relais** | 500 g : 4,15 € ; **1 kg : 5,99 €** (en vigueur depuis le 15/06/2026) |
| Mondial Relay, domicile | 1 kg : 9,49 € |
| Colissimo, domicile (sans signature) | 750 g : **9,29 €** ; 1 kg : 9,59 € (laposte.fr) |
| Colissimo, point de retrait | 750 g : 8,59 € ; 1 kg : 8,89 € |
| Chronopost Shop2Shop | 0-1 kg : 4,50 € |
| Chrono Relais 13 / Chrono 13 domicile | 10,80 € / 23,40 € |

Sources : ShippyPro (28/08/2026, d'après les grilles officielles) et La Poste.

| Outil d'étiquettes | Prix |
|---|---|
| **Shopify Shipping** | Inclus. Mondial Relay France uniquement, dépôt en relais, couverture 23 €/kg plafonnée à 750 € ; Colissimo et Chronopost aussi |
| **Boxtal** | Pas d'abonnement, tarifs négociés « dès le premier envoi » (prix visibles après création de compte, non fait). « Relais dès 2,99 € HT » selon Leptidigital (NV) |
| **Sendcloud** | Free à 0 €/mois. Lite à 26 €/mois + 0,11 € par étiquette (suivi personnalisé, 4 800 étiquettes/an max) |
| **Packlink PRO** | Inscription gratuite. Tarifs visibles après inscription (non fait) |

- **Choix** : livraison **Mondial Relay en point relais offerte** + Colissimo domicile en option payante, étiquettes via Shopify Shipping.
- Compare avec Boxtal en créant un compte avant le drop (tarif pro attendu entre 4 et 6 € en relais, (E)).

### Avis
- **Judge.me Free** : avis illimités, photos et vidéos, rich snippets. Awesome à 15 $/mois.
- Inutile pour le drop 01 (aucun client livré). Active les demandes d'avis après livraison pour le drop 02, et affiche si les avis sont vérifiés et comment (art. L111-7-2 C. conso).

### Pixels et CAPI (stack Shopify)
- **Facebook & Instagram (Meta)** : partage de données **« Maximum »** (pixel + Conversions API), puis finalisation dans Meta Events Manager, avec des événements « server » attendus.
- **TikTok for Shopify** : partage des données au maximum (Events API).
- **Google & YouTube** : GA4 et Google Ads.
- Consentement relayé par Consentmo Standard (Consent Mode v2, Meta, TikTok).
- **À installer avant d'envoyer du trafic vers la liste d'attente**, pour constituer les audiences dès le début.

### Bannière cookies conforme CNIL
| CMP | Prix |
|---|---|
| **Consentmo** (Shopify, 5,0/5, ≈ 2 000 avis) | Free ; Standard 10 $ (Consent Mode v2, pixels Meta et TikTok) ; Plus 37 $ (inclut une « EU Withdrawal page », directive 2023/2673) ; Max 99 $ (preuve de consentement) |
| Axeptio (app Shopify 3,3/5, 9 avis) | Par pages vues : gratuit jusqu'à 200 visiteurs ; 7,50 $ (2 500 PV, annuel) ; 29 $ (5 000 PV) ; 69 $ (100 000 PV). **Cher en cas de pic TikTok** |
| Bannière native Shopify | Gratuite, mais fonctions limitées |

- Règles CNIL : bouton « Refuser » aussi visible que « Accepter », aucun traceur avant consentement, preuve et durée du consentement.
- Pixels de suivi dans les e-mails : recommandation CNIL du 14/04/2026 (consentement pour certains usages). Demande à Klaviyo comment il s'y conforme.

### Pages légales (à faire relire par un juriste)
- **Mentions légales** : modèle Service-Public (gratuit).
- **CGV avec clauses de précommande** :
  - date de livraison ;
  - paiement intégral à la commande ;
  - en cas de retard, droit d'annuler et remboursement sous 14 jours (art. L216-1 et suivants) ;
  - rétractation de 14 jours à compter de la réception (L221-18) ;
  - frais de retour ;
  - médiateur.
  Générateurs : LegalPlace dès 34,90 € HT, Captain.Legal dès 4,90 € par document.
- **Formulaire de rétractation type** (annexe à l'article R221-1, gratuit).
- **Fonction « Renoncer au contrat ici »**, obligatoire depuis le 19/06/2026. Accessible sans compte, avec confirmation et accusé de réception sur support durable.
  - Sur Shopify : page dédiée + formulaire Klaviyo qui déclenche l'accusé de réception automatique, ou Consentmo Plus.
  - Références françaises citées par les sources : ordonnance n° 2026-2 du 05/01/2026 (NV, à vérifier sur Légifrance).
- **Médiateur de la consommation** obligatoire (L612-1). CM2C ou Médicys, environ 40-50 €/an selon Margeo (NV), à demander en devis.
- **Allégations** : la directive 2024/825 est applicable depuis le 27/09/2026. Pas de « écologique » ni de label maison. Et toujours pas d'« imperméable » sans test (cf. RESUME).

### Analytics
- **Shopify Analytics** : natif, vue en direct pendant le drop.
- **GA4** : via l'app Google & YouTube, avec Consent Mode v2.
- **Microsoft Clarity** : cartes de chaleur et enregistrements. Le consentement est exigé dans l'EEE depuis le 31/10/2025.
- **UTM** sur tous les liens de bio TikTok et Instagram.
- **Meta et TikTok Events Manager.**
- Option : un outil configuré pour l'exemption CNIL (Matomo, par exemple) pour compter aussi les visiteurs qui refusent les cookies.

---

## 7. Coût fixe mensuel (stack recommandée)
| Poste | Version minimale | Mois de drop (2 500 profils) | Entre deux drops |
|---|---|---|---|
| Shopify Basic | 27 € (annuel) | 36 € (mensuel) | Pause and Build : 9 $ |
| Klaviyo | Gratuit (≤ 250 profils) | 60 $ | Selon la taille de la liste |
| Consentmo | Gratuit | 10 $ | 10 $ |
| Précommande | 0 $ (natif) | 0-10 $ (STOQ Lite) | 0 $ |
| Judge.me, GA4, Clarity, Shopify Shipping | 0 € | 0 € | 0 € |
| **Total** | **≈ 27 €** | **≈ 36 € + 70-80 $ ≈ 100-110 € (E)** | **≈ 9 $ + Klaviyo** |

Hors mois :
- SMS à la consommation, ≈ 210 $ par drop dans l'hypothèse du §6 (E) ;
- médiateur ≈ 40-50 €/an (NV) ;
- domaine ≈ 10-20 €/an (E) ;
- CGV : coût unique.

Comparaison : stack C ≈ 45 $/mois (Vercel Pro + Supabase Pro) + outil e-mail. Stack B ≈ A + 20 $.

## 8. Coût variable par commande à 119 € TTC
| Moyen de paiement | Shopify Basic | Stripe |
|---|---|---|
| Carte EEE, Apple Pay, Shop Pay (Google Pay pour Stripe) | **2,04 €** | 2,04 € (3,58 € pour une carte premium) |
| Amex ou carte hors EEE | 3,46 € | 4,00 € |
| PayPal (4X inclus) | 3,80 € | 4,14 € |
| Klarna | 6,29 € | 6,34 € |
| Alma 3x | 6,90 € (HT + 2 %) | 5,66 € |

- **Panier type (E)** : 70 % carte/wallet, 20 % PayPal, 10 % Klarna, soit **2,81 €** de frais de paiement. Avec Mondial Relay offert (5,99 € public), on arrive à 8,80 €, et **≈ 9-10 €** avec l'emballage (≈ 1 €, (E)). Cela représente environ 8 % du prix TTC.
- App de précommande éventuelle : Timesact Fixed (23 $) réparti sur 150 commandes ≈ 0,15 $ par commande.
- Litiges : 15 € (Shopify) ou 20 € (Stripe) par rétrofacturation.
- Sur un drop de 150 commandes (E) : ≈ 420 € de frais de paiement + ≈ 900 € de port en relais au tarif public.

---

## 9. Mise en place, dans l'ordre
1. **Prérequis** : statut et SIRET (pour les mentions légales), compte bancaire pro, adhésion à un médiateur. Vérifie ton régime de TVA avec un comptable.
2. **Shopify Basic** (offre à 1 €/mois pendant 3 mois) + domaine.
   - Active **Shopify Payments** tôt : le KYC prend du temps.
   - Active PayPal et Klarna. Apple Pay et Shop Pay sont actifs automatiquement.
3. **Cookies et tracking avant tout trafic** :
   - Consentmo ;
   - apps Facebook & Instagram (Maximum), TikTok, Google & YouTube (GA4) ;
   - Clarity ;
   - convention UTM.
4. **Liste d'attente dès maintenant** :
   - page « coming soon » v0 (hero vidéo + formulaire) ;
   - formulaires Klaviyo avec cases e-mail et SMS séparées (double opt-in e-mail conseillé) ;
   - segments « liste d'attente » et « SMS » ;
   - flow de bienvenue.
   Les inscriptions commencent pendant les tests d'échantillons (priorité produit du RESUME).
5. **Légal** :
   - CGV de précommande, mentions légales, confidentialité, cookies ;
   - page « Renoncer au contrat ici » avec accusé de réception automatique ;
   - date de livraison visible sur la page, dans le panier, le checkout et l'e-mail.
6. **Thème one-page custom** (Skeleton theme), dans l'ordre des sections du RESUME :
   - hero, compteur, slider sèche/mouillée, fiche technique, tailles, date de livraison, FAQ, bouton collant ;
   - budget de performance mobile (vidéo compressée, JS minimal).
7. **Produit et stock** :
   - une variante par couleur avec stock de 150 et la taille en propriété de ligne, ou une allocation par taille ;
   - propriété « Livraison prévue » ;
   - e-mail de confirmation modifié ;
   - tag Flow ;
   - branding du checkout.
8. **Mécanique du drop** :
   - J-1 : early access de 24 h, boutique protégée par un mot de passe envoyé par e-mail et SMS ;
   - J0 : mot de passe retiré, 4 jours publics ;
   - à la fin : état « sold out » + formulaire drop 02 ;
   - commandes de test (mode test), test sur mobile 4G.
9. **Expédition** :
   - comparer Shopify Shipping et Boxtal sur Mondial Relay ;
   - tester une étiquette ;
   - choisir l'emballage et le peser (rester sous 1 kg).
10. **Après livraison** : demandes d'avis Judge.me, Pause and Build si plus d'un mois sans drop, puis publicités Meta et TikTok (le CAPI est déjà en place).

---

## 10. À vérifier / limites
- Prix Shopify en euros : sources tierces datées (HT ou TTC non précisé). À confirmer dans l'admin au moment de souscrire.
- Tarif SMS France de Klaviyo : non publié, visible seulement dans le compte.
- Tarifs pro Boxtal, Packlink et Shopify Shipping : visibles après création de compte (non fait, recherche en lecture seule).
- Délai long entre paiement et livraison : risque de rétrofacturations et de réserve chez le prestataire de paiement. Vérifie les conditions Shopify Payments et Stripe sur les précommandes.
- Références françaises du bouton de rétractation (ordonnance n° 2026-2) et du BNPL au 20/11/2026 : à confirmer avec un juriste.

## Sources (consultées le 08/11/2026 sauf mention)
- Shopify, tarifs (USD via proxy) : https://www.shopify.com/fr/tarifs
- Kanal, prix Shopify FR (relevé du 29/09/2026) : https://getkanal.com/fr/blog/prix-shopify
- Kanal, frais Shopify Payments FR (relevé du 07/10/2026) : https://getkanal.com/fr/blog/shopify-payments-frais
- Shopify Help, forfait Starter : https://help.shopify.com/fr/manual/intro-to-shopify/pricing-plans/plans-features/shopify-starter-plan
- Shopify Help, moyens de paiement France (Google Pay) : https://help.shopify.com/fr/manual/payments/shopify-payments/supported-countries/france/payment-methods
- Shopify Help, Pause and Build : https://help.shopify.com/en/manual/your-account/pause-store
- Shopify Help, partage de données Meta : https://help.shopify.com/en/manual/promoting-marketing/analyze-marketing/meta-data-sharing
- Shopify Help, Shopify Shipping avec Mondial Relay : https://help.shopify.com/manual/shipping/shopify-shipping/shipping-carriers/mondial-relay
- Shopify Help, tarifs Shopify Tax : https://help.shopify.com/en/manual/taxes/shopify-tax/pricing
- Shopify.dev, Skeleton theme (21/05/2025) : https://shopify.dev/changelog/skeleton-theme-is-now-available
- Shopify.dev, Storefront Web Components : https://shopify.dev/docs/api/storefront-web-components
- App Store : https://apps.shopify.com/preproduct · https://apps.shopify.com/timesact-discount-pre-order · https://apps.shopify.com/back-in-stock-restock-alerts · https://apps.shopify.com/judgeme · https://apps.shopify.com/gdpr-backpack · https://apps.shopify.com/axeptio-cookies
- Kanal, paiement en plusieurs fois sur Shopify (MAJ du 19/10/2026) : https://getkanal.com/fr/blog/paiement-plusieurs-fois-shopify
- Stripe, tarifs FR : https://stripe.com/fr/pricing · https://stripe.com/fr/pricing/local-payment-methods
- PayPal, grille FR du 15/07/2026 : https://www.paypalobjects.com/marketing/ua/pdf/FR/fr/fr-fr-merchant-fees-15-jul-2026.pdf · 4X inclus : https://www.paypal.com/fr/campaign/enable-pay-later
- Alma, tarifs : https://almapay.com/fr-FR/tarifs
- Klaviyo, tarifs (USD) : https://www.klaviyo.com/fr/pricing · SMS France (blog du 03/08/2026) : https://www.klaviyo.com/fr/blog/prix-campagne-sms · tarification par message (MAJ du 20/10/2026) : https://help.klaviyo.com/hc/en-us/articles/52952739755931
- Kanal, Klaviyo vs Brevo (relevés des 24 et 29/10/2026) : https://getkanal.com/fr/blog/klaviyo-vs-brevo
- Kanal, prix Omnisend (relevé du 24/10/2026) : https://getkanal.com/fr/blog/omnisend-prix · Omnisend Help : https://support.omnisend.com/fr/articles/3533018-plans-tarifaires-omnisend-2026
- Brevo Help, SMS : https://help.brevo.com/hc/fr/articles/208717449
- Kanal, Shopify Email et Messaging (relevé du 07/10/2026) : https://getkanal.com/fr/blog/shopify-email-avis
- La Poste, Colissimo 2026 : https://www.laposte.fr/tarif-colissimo
- ShippyPro, tarifs 2026 (28/08/2026) : https://www.shippypro.com/blog/fr/envoyer-un-colis-prix-et-tarifs-2026-des-transporteurs-en-france
- Sendcloud, tarifs : https://www.sendcloud.com/fr/tarifs/ · Boxtal : https://www.boxtal.com/fr/fr/tarifs-expedition
- Axeptio, tarifs (USD) : https://www.axept.io/pricing
- Vercel, tarifs : https://vercel.com/pricing · fair use (14/09/2026) : https://vercel.com/docs/limits/fair-use-guidelines
- Supabase, tarifs : https://supabase.com/pricing
- Leptidigital, obligations 2026 (rétractation, BNPL, pixels e-mail) : https://www.leptidigital.fr/e-commerce/paiement-fractionne-labels-verts-pixels-mail-obligations-changent-e-commercants-92144/
- Digismoothie, bouton de rétractation UE (MAJ du 01/10/2026) : https://www.digismoothie.com/fr/blog/eu-withdrawal-button
- DGCCRF, règles du e-commerce : https://www.economie.gouv.fr/dgccrf/les-fiches-pratiques/e-commerce-les-regles-entre-professionnels-et-consommateurs
- Microsoft Clarity, consentement : https://learn.microsoft.com/en-us/clarity/setup-and-installation/consent-management
- StatCounter, OS mobile France (juin 2026) : https://gs.statcounter.com/os-market-share/mobile-tablet/france
- Médiateur : https://donneespersonnelles.fr/mediation-consommation · https://margeoapp.com/blog/mediateur-consommation-revendeur-obligatoire
