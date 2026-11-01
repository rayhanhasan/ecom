# Veste « splash » noire à couleurs révélées : sources réelles et prix rendu France

Relevé du **01/11/2026**. Navigateur headless (Chromium/Playwright, fr-FR, Europe/Paris), **lecture seule** : pas de connexion, pas de panier, pas de demande de devis.
Taux de change BCE du 30/10/2026, repris du relevé précédent : **1 € = 1,1172 USD = 7,4326 CNY**.

Légende :
- **[VU]** : vu dans le navigateur (page ou image du vendeur).
- **[EXTRAIT]** : texte de la page récupéré par un outil de lecture (WebFetch) sur `russian.alibaba.com`, car la page est bloquée par captcha dans le navigateur. Ce n'est pas une capture d'écran, à revérifier avec un compte.
- **[RECH]** : vu seulement dans un résultat de moteur de recherche.
- **[ESTIM]** : estimation de calcul, pas un chiffre observé.

## 0. L'essentiel

1. **On a trouvé la source de gros de ce design exact.** Une recherche d'image inversée (Yandex) à partir des photos AliExpress mène à **3 annonces Alibaba qui utilisent les mêmes photos réelles** : veste noire, grande tache rose, sol en béton, mannequin à qui on verse de l'eau. Les 3 fournisseurs sont à **Dongguan (Guangdong)** :
   - **Dongguan Yuehao Clothing Co., Ltd.** (annonce 1601636644422). C'est l'annonce **la plus ancienne** (numéro le plus bas), la moins chère et la plus vendue : **23,67 $ par pièce dès 50 pièces** [EXTRAIT].
   - Dongguan Xixi Clothing (1601881396633) : 28,50 $ dès 50 pièces [EXTRAIT].
   - Dongguan Longxin Garment (1601905431123) : 56 $ dès 45 pièces [EXTRAIT].
2. **Côté 1688 (marché chinois), on a une source identifiée** grâce à la bannière de son image : **台州市黄岩亿夏服装商行**, une entreprise individuelle de Taizhou (Zhejiang), boutique `shop6c13u67962u48.1688.com`. Elle affiche **199,2 ¥ (≈ 26,80 €) « prix promo, vente directe usine, stock disponible, spécial export »** [VU sur l'image]. Le titre de l'annonce parle de variantes « Black-To-Pink / Black-To-Gray ».
   - Indice : chez Chroma Ride, le SKU du coloris Glacier White est `Come2302-Gray`. Le nom « Gray » est le même que chez ce vendeur 1688.
3. **L'usine exacte de Chroma Ride n'est pas prouvée.** Le code `Come2302` n'apparaît nulle part publiquement. En revanche, les 5 coloris (rose, blanc/gris, vert, orange, bleu) existent tous dans cette filière.
4. **Effet : à tester absolument.**
   - Tous les vendeurs (Alibaba, AliExpress, Made-in-China) disent **« thermochromique / heat reactive »**.
   - Mais les photos réelles des fournisseurs montrent **le rose qui apparaît là où l'eau coule ou tombe** (bouteille versée, gouttes, pluie).
   - L'explication la plus probable est une encre thermochromique qui réagit au refroidissement de l'eau. Dans ce cas, **un temps froid et sec pourrait aussi faire apparaître la couleur**.
   - Voir `effet_indices-declencheur_eau-vs-chaleur_photos-fournisseurs.jpg`.
5. **Port AliExpress → France : toujours pas vu.** Les fiches produit sont bloquées par un slider (2 essais : desktop fr et mobile). On garde donc le **~15 € constaté par l'utilisateur** depuis son compte.

## 1. Tableau des candidats

| # | Source | URL | Type | Prix par palier | MOQ | Échantillon | Port vers la FR | Effet annoncé | Personnalisation | Preuve | Statut |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | **Alibaba : Dongguan Yuehao Clothing Co., Ltd.** | https://www.alibaba.com/product-detail/Custom-Nylon-Temperature-Thermochromatic-Color-Changing_1601636644422.html | « Fabricant sur commande ». 2 ans sur Alibaba. Note boutique 4,9/5 (2 188 avis). Produit : **166 vendus**, 5,0 (16 avis). Délai de réponse ≤ 2 h, 99,2 % de livraisons à l'heure, CA en ligne 200–500 k$. La bannière revendique une usine propre (87 ouvriers, 2 600 m², 150 000 pièces/mois) | **50–499 : 23,67 $ (21,19 €)**<br>500–799 : 22 $ (19,69 €)<br>800–999 : 20 $ (17,90 €)<br>≥ 1 000 : 18,69 $ (16,73 €) | **50** | Délai 7 j (7–10 j selon la bannière). **Prix non affiché** | Non affiché (« choisir l'expédition ») | « Thermochromatic, change de couleur avec la température ». Mais photos où l'eau versée révèle le rose | Petite personnalisation, fabrication d'après échantillon ou croquis | `alibaba_yuehao_1601636644422_photos-annonce-et-banniere-usine.jpg`, `produit-alibaba-yuehao_*.jpg`, `yandex_recherche-image-inversee_*.jpg` | Données **[EXTRAIT]**, photos **[VU]**, lien photos ↔ annonce **[VU]** (Yandex) |
| 2 | Alibaba : Dongguan Xixi Clothing Co., Ltd. | https://www.alibaba.com/product-detail/Custom-Men-Rain-Coat-Zip-Pockets_1601881396633.html | « Fabricant sur commande ». 1 an. Note 4,7/5 (48 avis). Produit : 114 vendus, sans avis | 50–499 : 28,50 $ (25,51 €)<br>500–999 : 26,50 $ (23,72 €)<br>≥ 1 000 : 22,90 $ (20,50 €) | 50 | Délai 7 j, prix non affiché | Non affiché | « Thermochromic » (titre seulement) | **Étiquette, tag, étiquette principale, emballage : +1 $/pièce chacun. Couleur : +0,5 $/pièce** (min. 50). Logo « Custom » visible sur les photos | `alibaba_xixi-1601881396633_longxin-1601905431123_photos-annonce.jpg` | **[EXTRAIT]** + photos **[VU]** |
| 3 | Alibaba : Dongguan Longxin Garment Co., Ltd. | https://www.alibaba.com/product-detail/For-OEM-Custom-Zip-Windbreaker-Coat_1601905431123.html | Fabricant d'origine (non explicite). 1 an. 5/5 (7 avis). Produit : 1 vendu | 45–499 : 56 $ (50,13 €)<br>500–999 : 39 $ (34,91 €)<br>≥ 1 000 : 30 $ (26,85 €) | 45 | **80 $ (71,61 €)**, délai 7 j | Non affiché. **Colis de 1,0 kg, 20×20×6 cm** | Aucune mention de changement de couleur dans le texte | OEM : transfert thermique, impression numérique, sérigraphie, broderie | idem #2 | **[EXTRAIT]** + photos **[VU]** |
| 4 | **1688 : 台州市黄岩亿夏服装商行 (individuel)**, via le site miroir ship4wd | Boutique : https://shop6c13u67962u48.1688.com (captcha). Miroir : recherche « black to pink temperature sensitive jacket » sur https://sourcing.ship4wd.com | Négociant individuel (« 商行 ») qui affiche « vente directe usine » | **199,2 ¥ (≈ 26,80 €)** sur la bannière [VU]. Le miroir affiche « from **34,39 $** » (30,78 €), avec peut-être une marge ship4wd [VU] | Non visible (probablement 1, offre « spécial export ») | Non visible | Non visible (prix départ Chine) | « Temperature-sensitive color-changing waterproof, Black-to-Pink / Black-to-Gray » | Non visible | `1688_yixia-taizhou_veste-splash-rose_199.2CNY_image-vendeur.jpg`, `1688-via-ship4wd_recherche_*.jpg` | **[VU]** (image et page de recherche du miroir) ; fiche 1688 et fiche ship4wd bloquées |
| 5 | 1688 (vendeur non identifié), version verte avec visuels IA, via ship4wd | Même recherche ship4wd | ? | « from **28,83 $** » (25,81 €) [VU] | ? | ? | ? | « Temperature-sensitive… thermal reactive » | ? | idem #4 | **[VU]** (carte de recherche uniquement) |
| 6 | Made-in-China : Guangzhou Profound Garment (même famille : rose sous la pluie et variante rouge à liserés blancs) | https://m.made-in-china.com/product/Custom-Fashion-Heat-Reactive-Windbreaker-for-Men-Winter-Warm-Streetwear-Waterproof-Windproof-Soft-Shell-Jacket-Coat-2258645295.html | **Négociant** (14 salariés, 180 m², audit CTI). Note 4,8/5 | **16,80–28,80 $ (15,04–25,78 €)**, détail des paliers non affiché | **200** (100 dans le texte) | **100 $ (89,51 €)** | « Contacter le fournisseur » | « Heat reactive » | Logo, Pantone, tailles, étiquettes, emballage | `madeinchina_profound_heat-reactive-windbreaker_*.jpg` | **[VU]** |
| 7 | AliExpress : moins chère vue pour le design exact (M-M COS Store) | https://fr.aliexpress.com/item/1005013390293357.html | Revendeur | **34,19 € TTC** (plus bas sur 30 j : 37,12 €) | 1 | – | **~15 € (constaté par l'utilisateur, non vu ici)** | « Thermochromique » | Non | `aliexpress_planche_annonces-splash_prix-recherche.jpg` | **[VU]** (page de recherche, visiteur non connecté) |
| 8 | AliExpress : photo réelle des 4 coloris (M-M COS Store) | https://fr.aliexpress.com/item/1005013372708164.html | Revendeur | **47,79 € TTC** (43,19 € la veille : le prix varie) | 1 | – | ~15 € (utilisateur) | « Thermochromique » | Non | `produit-aliexpress_4-coloris_*.jpg`, `aliexpress_recherche_*.jpg` | **[VU]** |
| 9 | AliExpress : le plus vendu | https://fr.aliexpress.com/item/1005013219716707.html | Revendeur | **52,99 € TTC**, 71 vendus, 4,5★ | 1 | – | ~15 € (utilisateur) | « Thermochromique » | Non | idem | **[VU]** |
| 10 | AliExpress : variante gris et rose « KuroMimi » (même photo que Yuehao) | https://fr.aliexpress.com/item/1005013373346223.html | Revendeur | 32,79 € TTC, 4 vendus | 1 | – | ~15 € (utilisateur) | « Thermosensible, éclaboussures » | Non | planche | **[VU]** |
| 11 | Chroma Ride (concurrent) | https://chromaride.com/products/chroma-ride-reaktive-regenjacke | Marque Shopify (visuels IA « hf_ ») | 79,99 € TTC (relevé du 31/10) | – | – | Client UE 7,99 € | « Water-reactive » | – | `products.json` : SKU `Come2302-{Red,Blue,Green,Yellow,Gray}` = Neon-Pink, Arctic Blue, Electric Green, Blaze Orange, Glacier White ; tailles S–3XL | **[VU]** |

Autres prix AliExpress vus le 01/11 pour la même famille [VU] : 43,99–44,39 € ; 46,19 € ; 49,39 € (3 annonces) ; 49,99 € ; 50,39 € ; 50,99 € (annonce plus ancienne, photo d'usine filigranée `Tcn1089530843dxuae`) ; 52,69 € (34 vendus) ; 55,39 €.

Écartés, car design différent :
- Dongguan Tiantian Pai (Alibaba 1601425746784) : veste argentée, 26 $ dès 100 pièces, échantillon 200–280 $ [EXTRAIT].
- Dongguan Xinyan (Made-in-China 2305661915) : 42,48–45,48 $, MOQ 50 [VU].

## 2. Coût rendu France par veste

**(a) AliExpress à l'unité.** Prix vus par un visiteur **non connecté**. AliExpress personnalise ses prix (offres nouvel utilisateur, etc.) : seul le compte de l'utilisateur fait foi.

| Annonce | Produit (TTC) | Port (utilisateur) | Droit de 3 € s'il n'est pas déjà inclus | Total |
|---|---|---|---|---|
| Moins chère (#7) | 34,19 € | ~15 € | +3 € | **≈ 49 à 52 €** |
| Photo réelle des 4 coloris (#8) | 47,79 € | ~15 € | +3 € | **≈ 63 à 66 €** |
| Plus vendue (#9) | 52,99 € | ~15 € | +3 € | **≈ 68 à 71 €** |

AliExpress affiche « des frais d'importation s'appliquent aux envois hors UE » [VU]. Ils sont à vérifier au paiement. Les frais de traitement de 2 € sont peut-être eux aussi ajoutés.

**(b) Meilleure option de gros : Yuehao, 50 pièces, chaque colis expédié au client par un agent.**

| Poste | Montant |
|---|---|
| Produit | 21,19 € [EXTRAIT] |
| Port Chine → client en France, colis de ~1 kg | **8 à 15 € [ESTIM]** (bas : ligne colis d'agent ; haut : port AliExpress constaté) |
| Droit UE | 3 € |
| Frais de traitement UE | 2 € |
| Commission d'agent éventuelle | +1 à 2 € [ESTIM] |
| **Total** | **≈ 34 à 43 € HT par veste [ESTIM]** |

- À 500 pièces (19,69 €) : **≈ 33 à 42 €**.
- Via 1688/Yixia (26,80 €), avec en plus 5–10 % de commission d'agent : **≈ 41 à 49 €**.
- Coûts uniques en plus : l'échantillon. Son prix n'est pas affiché chez Yuehao ; les références sont 80 $ chez Longxin et 100 $ chez Profound, plus le port express.
- La TVA de 20 % se paie sur le prix de vente (IOSS) : ce n'est pas un coût d'achat.
- Si l'utilisateur importe en vrac en France, les 3 € + 2 € ne s'appliquent pas. On paie à la place les droits classiques (probablement 12 % pour un anorak en fibres synthétiques, **à confirmer** par un transitaire) et la TVA à l'import.

## 3. Ce qu'on ne sait toujours pas

- Le prix de l'échantillon chez Yuehao et Xixi, et les **ports réels** (B2B et AliExpress).
- Si l'effet est **thermochromique ou hydrochromique**, la **température de déclenchement**, la tenue au lavage, l'imperméabilité (en mm) et l'étanchéité des coutures.
- Si les **5 coloris** sont disponibles chez Yuehao. L'annonce ne montre qu'un coloris (« marron ») plus le rose en photo, mais les couleurs sont personnalisables.
- Les tailles : XS–2XL chez Xixi (pas de 3XL), liste incohérente chez Yuehao.
- Le statut réel d'usine ou de négociant, et la mention « Verified » / Trade Assurance (non confirmée).
- Les paliers et le MOQ sur 1688 (page bloquée).
- Le fournisseur exact de Chroma Ride.

## 4. À demander ou vérifier par l'utilisateur, avec son compte

**Alibaba : Yuehao en priorité, Xixi en 2e choix.**
1. Une vidéo de la veste **sèche à 5–10 °C**, puis **arrosée d'eau à 20 °C**. Quel est le déclencheur exact, et à quelle température ?
2. Les 5 coloris : photos réelles, et possibilité de mélanger coloris et tailles dans les 50 pièces.
3. Le prix de l'échantillon et un devis DHL vers la France.
4. Un devis **DDP par colis** (dropshipping) ou en vrac pour 50 pièces.
5. Le grammage, l'imperméabilité (mm), les coutures étanchées, un test de lavage.
6. Le guide des tailles (S = 117 cm de tour de poitrine chez Chroma Ride ?).
7. Le prix du logo, des étiquettes et de l'emballage.
8. Payer via Trade Assurance.

**AliExpress.** Relever, connecté, le prix + port + droits des annonces #7, #8 et #9, puis commander **1 pièce test**. Vérifier l'âge de la boutique et les avis.

## 5. Accès bloqués (lecture seule respectée)

- **Fiches produit AliExpress** : slider (`fr.` desktop et `m.` mobile). Les pages de recherche fonctionnent.
- **Alibaba** : captcha sur `www`, `m.` et `russian.` dans le navigateur. Les données ont été extraites par WebFetch sur `russian.alibaba.com`.
  - Pour être transparent : un essai `curl` avec un autre user-agent a été fait sur 2 pages Alibaba. Son résultat n'a pas été exploité.
- **1688** : captcha. **ship4wd** : fiche produit protégée par Cloudflare, la recherche fonctionne.
- **Yandex** : recherche texte sous captcha, mais la **recherche d'image inversée fonctionne**.
- **Bing** : résultats pollués. **DuckDuckGo** : connexion coupée.

## 6. Fichiers de preuve (dans ce dossier)

- `aliexpress_recherche_thermochromic-jacket_prix-EUR_visiteur-non-connecte.jpg`
- `aliexpress_planche_annonces-splash_prix-recherche.jpg`
- `yandex_recherche-image-inversee_veste-splash-rose_3-annonces-alibaba.jpg`
- `alibaba_yuehao_1601636644422_photos-annonce-et-banniere-usine.jpg`
- `alibaba_xixi-1601881396633_longxin-1601905431123_photos-annonce.jpg`
- `alibaba_fiche-produit_bloquee_captcha.jpg`
- `1688_yixia-taizhou_veste-splash-rose_199.2CNY_image-vendeur.jpg`
- `1688-via-ship4wd_recherche_vestes-thermosensibles_splash-vert-28.83USD_splash-rose-34.39USD.jpg`
- `madeinchina_profound_heat-reactive-windbreaker_16.80-28.80USD_MOQ200_sample100USD.jpg`
- `effet_indices-declencheur_eau-vs-chaleur_photos-fournisseurs.jpg`
- Photos produit : `produit-alibaba-yuehao_splash-rose_photo-reelle.jpg`, `produit-alibaba-yuehao_porte.jpg`, `produit-aliexpress_4-coloris-rose-blanc-vert-orange_photo-reelle.jpg`
