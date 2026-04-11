# Addendum SEO + AEO : Rendre les articles trouvables par Google et les IA

Ce document complète le SYSTEM-PROMPT.md principal avec les règles d'optimisation pour la recherche Google et la recherche par IA (Perplexity, ChatGPT, Google AI Overviews, Gemini).

-----

## 1. Balises `<head>` obligatoires

Chaque article HTML doit inclure ces balises dans `<head>` :

```html
<!-- SEO Core -->
<title>{Titre H1} | Place des Armes · Le Blog</title>
<meta name="description" content="{Résumé de 150-160 caractères, incluant le mot-clé principal et un bénéfice lecteur}">
<meta name="robots" content="index, follow">
<link rel="canonical" href="https://place-des-armes.fr/blog/{slug}">

<!-- Date de publication (critique pour fraîcheur IA) -->
<meta property="article:published_time" content="{YYYY-MM-DD}T08:00:00+02:00">
<meta property="article:modified_time" content="{YYYY-MM-DD}T08:00:00+02:00">

<!-- Open Graph (Facebook, LinkedIn, Perplexity) -->
<meta property="og:type" content="article">
<meta property="og:title" content="{Titre H1}">
<meta property="og:description" content="{Même meta description}">
<meta property="og:image" content="https://place-des-armes.fr/blog/images/{slug}_cover.png">
<meta property="og:url" content="https://place-des-armes.fr/blog/{slug}">
<meta property="og:site_name" content="Place des Armes · Le Blog">
<meta property="og:locale" content="fr_FR">

<!-- Twitter / X Cards -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="{Titre H1}">
<meta name="twitter:description" content="{Même meta description}">
<meta name="twitter:image" content="https://place-des-armes.fr/blog/images/{slug}_cover.png">

<!-- Langue -->
<html lang="fr">
<meta http-equiv="content-language" content="fr-FR">
```

-----

## 2. Schema.org / JSON-LD (structured data)

Chaque article inclut un bloc `<script type="application/ld+json">` dans `<head>` avec au minimum :

### 2.1 Schema Article

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "{Titre H1}",
  "description": "{Meta description}",
  "image": "https://place-des-armes.fr/blog/images/{slug}_cover.png",
  "datePublished": "{YYYY-MM-DD}",
  "dateModified": "{YYYY-MM-DD}",
  "publisher": {
    "@type": "Organization",
    "name": "Place des Armes",
    "url": "https://place-des-armes.fr",
    "logo": {
      "@type": "ImageObject",
      "url": "https://place-des-armes.fr/logo.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://place-des-armes.fr/blog/{slug}"
  },
  "inLanguage": "fr-FR",
  "about": {
    "@type": "Thing",
    "name": "Tir sportif en France"
  },
  "keywords": ["{mot-clé 1}", "{mot-clé 2}", "{mot-clé 3}"]
}
```

### 2.2 Schema FAQPage (pour les articles avec questions/réponses)

Ajouter un bloc FAQ JSON-LD pour chaque paire question/réponse présente dans l'article :

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Combien coûte une licence FFTir en 2026 ?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "La part fédérale est de 69 € pour un adulte (49 € pour un jeune). La cotisation club varie de 150 à 400 €. Budget total première année : 250 à 550 €."
      }
    }
  ]
}
```

### 2.3 Schema HowTo (pour les articles avec étapes)

```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "Comment s'inscrire dans un club de tir en France",
  "step": [
    {
      "@type": "HowToStep",
      "position": 1,
      "name": "Trouver un club",
      "text": "Utilisez l'annuaire FFTir sur fftir.org pour trouver un club affilié près de chez vous."
    }
  ]
}
```

-----

## 3. Structure de contenu optimisée pour les featured snippets et les IA

### 3.1 Titres H2 en format question

Les IA et Google Featured Snippets favorisent les titres formulés comme des questions que les gens posent réellement :

| Titre actuel (créatif) | Titre optimisé (question-based) |
|---|---|
| Combien ça coûte | Combien coûte l'inscription en club de tir en France ? |
| Les 5 états d'une arme | Quels sont les 5 états d'une arme selon la FFTir ? |
| Le parcours vers la catégorie B | Comment obtenir une arme de catégorie B en France ? |
| Au stand : zones et protocole | Comment se déroule une séance au stand de tir ? |

**Règle :** au moins 2 des H2 de chaque article doivent être formulés comme des questions que les gens tapent dans Google ou posent à une IA.

### 3.2 Pattern "direct answer" (première phrase après le H2)

La première phrase après chaque H2 doit répondre directement et de façon autonome à la question du titre. Cette phrase est celle que les IA extrairont pour la citer.

```
❌ MAUVAIS :
## Combien coûte l'inscription en club de tir ?
Le budget dépend de plusieurs facteurs qu'il convient d'examiner attentivement.

✅ BON :
## Combien coûte l'inscription en club de tir ?
Le budget total première année se situe entre 250 et 550 €, comprenant 69 € de part fédérale FFTir et 150 à 400 € de cotisation club.
```

### 3.3 Section FAQ explicite en fin d'article

Ajouter une section `## Questions fréquentes` avec 3 à 5 paires Q/R courtes. Chaque réponse doit tenir en 2 à 3 phrases maximum. Cette section alimente à la fois :
- Les featured snippets Google ("People Also Ask")
- Les réponses directes des IA
- Le JSON-LD FAQPage

```html
<section class="faq">
  <h2>Questions fréquentes</h2>
  <details>
    <summary>Peut-on s'inscrire en club de tir sans expérience ?</summary>
    <p>Oui. Les clubs FFTir accueillent les débutants complets. L'école de tir obligatoire (~8 semaines) vous forme aux règles de sécurité et aux techniques de base. Le matériel est prêté la première année.</p>
  </details>
  <details>
    <summary>Faut-il un certificat médical pour le tir sportif ?</summary>
    <p>Oui. Un certificat de non contre-indication à la pratique du tir sportif, délivré par votre médecin traitant, est obligatoire pour l'inscription. Il est valable 12 mois.</p>
  </details>
</section>
```

### 3.4 Phrases "citables" (pour les IA)

Les IA (Perplexity, ChatGPT) citent des phrases qui :
- Sont factuelles et autonomes (compréhensibles sans contexte)
- Contiennent un chiffre précis ou une règle claire
- Font moins de 40 mots

**Exemples de phrases citables à intégrer dans le corps de l'article :**

```
"En France, la part fédérale de la licence FFTir est de 69 € pour un adulte et 49 € pour un jeune en 2025/2026."

"Le QCM FFTir comporte 15 questions de sécurité avec un seuil de réussite de 12/15, dont 8 questions éliminatoires."

"Une arme de catégorie B nécessite au minimum 6 mois de licence, 3 tirs contrôlés espacés de 2 mois, et une autorisation préfectorale via le SIA."
```

-----

## 4. Maillage interne entre les 10 articles

Chaque article doit contenir 2 à 3 liens vers d'autres articles de la série, intégrés naturellement dans le texte :

```html
<p>Pour comprendre les étapes d'acquisition après votre inscription, consultez notre guide 
<a href="/blog/categories-armes-bcd">Comprendre les catégories d'armes B, C et D</a>.</p>
```

**Matrice de maillage recommandée :**

| Article | Liens vers |
|---|---|
| 1. Règles de sécurité | → 6 (QCM), 7 (Séance) |
| 2. Inscription club | → 3 (Calibre), 5 (Catégories) |
| 3. Premier calibre | → 4 (Pistolet/Carabine), 2 (Inscription) |
| 4. Pistolet/Carabine | → 3 (Calibre), 10 (Discipline) |
| 5. Catégories B/C/D | → 2 (Inscription), 9 (Stockage) |
| 6. QCM FFTir | → 1 (Sécurité), 5 (Catégories) |
| 7. Séance de tir | → 1 (Sécurité), 8 (Erreurs) |
| 8. Erreurs techniques | → 7 (Séance), 3 (Calibre) |
| 9. Stockage | → 5 (Catégories), 2 (Inscription) |
| 10. Disciplines | → 4 (Pistolet/Carabine), 3 (Calibre) |

-----

## 5. Fichiers techniques pour le crawling

### 5.1 sitemap.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://place-des-armes.fr/blog/regles-securite-tir-sportif</loc>
    <lastmod>2026-04-11</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
  </url>
  <!-- Répéter pour chaque article -->
</urlset>
```

### 5.2 robots.txt

```
User-agent: *
Allow: /blog/
Sitemap: https://place-des-armes.fr/sitemap.xml

User-agent: GPTBot
Allow: /blog/

User-agent: PerplexityBot
Allow: /blog/

User-agent: ClaudeBot
Allow: /blog/

User-agent: Google-Extended
Allow: /blog/
```

**Note :** Autoriser explicitement les crawlers IA (GPTBot, PerplexityBot, ClaudeBot, Google-Extended) est essentiel pour que le contenu apparaisse dans les réponses des IA.

### 5.3 llms.txt (nouveau standard)

Fichier à la racine du site pour faciliter l'ingestion par les LLM :

```
# Place des Armes - Blog Tir Sportif

> 10 guides visuels pour débuter le tir sportif en France en toute sécurité.

## Articles

- [Règles de sécurité](https://place-des-armes.fr/blog/regles-securite-tir-sportif): Les 4 lois universelles qui protègent chaque tireur
- [Inscription en club](https://place-des-armes.fr/blog/inscription-club-tir): Étapes, coûts (250-550€) et documents pour obtenir sa licence FFTir
- [Premier calibre](https://place-des-armes.fr/blog/quelle-arme-pour-commencer): Air comprimé, .22 LR ou 9mm, le parcours de progression
<!-- etc. -->
```

-----

## 6. Optimisation des images pour la recherche

Chaque diagramme PNG exporté doit avoir :

### 6.1 Nommage descriptif

```
✅ regles-securite-4-couches-defense-tir-sportif.png
❌ regles-securite-tir-sportif_diag01.png
```

### 6.2 Attributs alt détaillés

```html
<img src="images/regles-securite-4-couches-defense.png" 
     alt="Diagramme montrant les 4 règles de sécurité du tir sportif organisées en couches concentriques de protection, de la règle 1 (toujours considérer l'arme comme chargée) à la règle 4 (identifier sa cible et ce qu'il y a derrière)"
     width="700" height="400"
     loading="lazy">
```

### 6.3 Données structurées ImageObject

```json
{
  "@type": "ImageObject",
  "contentUrl": "https://place-des-armes.fr/blog/images/regles-securite-4-couches-defense.png",
  "description": "Les 4 règles de sécurité du tir sportif en couches concentriques",
  "name": "Diagramme : les 4 lois de sécurité du tir sportif"
}
```

-----

## 7. Signaux de fraîcheur

Les IA et Google favorisent le contenu récent et mis à jour :

- Inclure l'année dans le titre quand pertinent : "Licence FFTir 2026 : prix et démarches"
- Mentionner la saison en cours : "saison 2025/2026"
- Ajouter une date visible dans l'article : `<time datetime="2026-04-11">11 avril 2026</time>`
- Mettre à jour la `dateModified` du JSON-LD à chaque modification

-----

## 8. Checklist SEO/AEO (vérifier en plus de la checklist qualité)

- [ ] `<title>` contient le mot-clé principal + "Place des Armes"
- [ ] `<meta description>` de 150-160 caractères avec mot-clé et bénéfice
- [ ] JSON-LD Article avec datePublished et dateModified
- [ ] JSON-LD FAQPage avec 3-5 questions/réponses
- [ ] Au moins 2 H2 formulés comme des questions
- [ ] Première phrase après chaque H2 = réponse directe et autonome
- [ ] Section "Questions fréquentes" avec `<details>/<summary>`
- [ ] 2-3 liens internes vers d'autres articles de la série
- [ ] Attributs alt descriptifs sur toutes les images
- [ ] `<time datetime>` avec date de publication visible
- [ ] robots.txt autorisant GPTBot, PerplexityBot, ClaudeBot
- [ ] sitemap.xml avec tous les articles
- [ ] llms.txt à la racine du site
