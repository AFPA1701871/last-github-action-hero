---
theme: default
title: Last GitHub Action Hero
colorSchema: dark
fonts:
  provider: none
transition: slide-left
drawings:
  enabled: false
layout: center
class: text-center
---

<p class="presents">Universal CI/CD Prod. presents</p>
<img src="/last-github-action-hero.svg" class="logo" alt="Last GitHub Action Hero" />
<p class="tagline">du suspens, des émotions fortes, des rebondissements... et des GITHUB ACTIONS ! </p>

---

# Pourquoi GitHub Actions ?

<div class="cols">
  <div class="card bad">
  <h3>Sans automatisation</h3>

  - "Ça marche sur ma machine !"
  - "Des tests unitaires ? Pour quoi faire ?"
  - Vendredi 18h, parfait pour un **déploiement manuel**
  - "Montre voir comment tu déploies, toi ?"
  </div>
<div class="card good">
  <h3>Avec GitHub Actions</h3>

  - Tout se lance à chaque **push**
  - Mêmes étapes pour toute l'équipe
  - Le résultat est visible dans GitHub
  - Tout se passe sur un conteneur fourni par Github
  </div>
</div>

---

# CI / CD : bon cop / bad cop

<div class="flow">
  <div class="stage"><b>Push</b><small>« Action ! »</small></div>
  <span>▶</span>
  <div class="stage"><b>Die Hard</b><small>Lint</small></div>
  <span>▶</span>
  <div class="stage"><b>Terminator</b><small>Tests</small></div>
  <span>▶</span>
  <div class="stage"><b>Commando</b><small>Build</small></div>
  <span>▶</span>
  <div class="stage"><b>Rambo</b><small>Déploiement</small></div>
</div>

<div class="cols brace">
<div><b>CI</b> : intégration continue<br/>on vérifie le code à chaque modification</div>
<div><b>CD</b> : livraison continue<br/>on publie automatiquement si tout est OK</div>
</div>

---

# Anatomie d'un workflow

<div class="wf">
  <div class="wf-title">WORKFLOW <small>le scénario · un fichier YAML dans .github/workflows</small></div>
  <div class="trigger">TRIGGER <small>"Action !"" : push, pull request, bouton manuel, planning</small></div>
  <div class="jobs">
  <div class="job">
    <div class="job-title">JOB "ci" <small>une scène · sur un **runner**</small>
    </div>
  <div class="steps"><div class="step">STEP<small>récupérer le code</small></div><div class="step">STEP<small>lancer les tests</small></div><div class="step">STEP<small>construire le site</small></div></div>
</div>
<div class="needs">needs<br/>▶</div>
  <div class="job">
    <div class="job-title">JOB "cd" <small>une autre scène, un autre plateau</small>
  </div>
  <div class="steps">
    <div class="step">STEP<small>déployer</small>
    </div>
  </div>
  </div>
  </div>
</div>

<p class="foot">Les steps d'un job partagent le même conteneur ! Chaque job en démarre un nouveau.</p>

---

# Un workflow, en vrai

```yaml {1|2|3-5|6-8}
name: Mon premier workflow       # le titre du workflow
on: push                         # Action ! : le déclencheur
jobs:
  test_the_code:                 # une scène (un job)
    runs-on: ubuntu-latest       # le plateau : une machine fournie par GitHub
    steps:
      - uses: actions/checkout@v4   # une action toute faite
      - run: npm test               # une commande
```

---

# Deux types d'étapes : run et uses

<div class="cols3">
  <div class="card">
    <h3><code>run:</code></h3>
    <p>Une commande shell.</p>
    <p class="ex">npm test</p>
  </div>
  <div class="card">
    <h3><code>uses:</code></h3>
    <p>Une action réutilisable du Marketplace.</p>
    <p class="ex">actions/checkout@v4</p>
  </div>
  <div class="card">
    <h3>Écrire la sienne</h3>
    <p><b>JavaScript</b> : rapide, la plus courante<br/><b>Docker</b> : environnement sur mesure, plus lourde<br/><b>Composite</b> : plusieurs steps regroupés en un</p>
  </div>
</div>

<p class="foot">Une action tierce s'exécute avec vos secrets : fixez sa version (@v4) et choisissez des sources de confiance.</p>

---
layout: center
class: text-center
---

# À vous de jouer !

<div class="steps-list">
  <div><b>1</b> Fork du repo</div>
  <div><b>2</b> Activer Actions</div>
  <div><b>3</b> Pages : source GitHub Actions</div>
  <div><b>4</b> Ajouter les secrets email</div>
  <div><b>5</b> Lancer le workflow</div>
</div>
