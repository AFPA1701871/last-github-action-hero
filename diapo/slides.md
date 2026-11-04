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
<p class="tagline">du suspens, des émotions fortes, des bugs... et des GITHUB ACTIONS ! </p>

---

# Pourquoi GitHub Actions ?

<div class="cols">
  <div class="card bad">
  <h3>Ce qu'on ne veut plus entendre</h3>
  - "Ça marche sur ma machine !"<br/>
  - "Des tests unitaires ? Pour quoi faire ?"<br/>
  - "Vendredi 15h, parfait pour un déploiement manuel !"<br/>
  - "Montre voir comment tu déploies, toi ?"<br/>
  </div>
<div class="card good">
  <h3>Ce qu'on souhaite entendre</h3>
    - "Ils sont passés les tests du dernier push ?"<br/>
    - "T'as vérifié le résultat du build sur Github ?"<br/>
    - "Il est bien la 2ème étape de ton workflow"<br/>
    - "T'a modifié l'environnement de test commun ?"<br/>
  </div>
</div>


<img src="/lets-party.gif" class="logo" alt="Let's party" />

---

# Anatomie d'un workflow

<div class="wf">
  <div class="wf-title">WORKFLOW <small>le scénario · un fichier YAML dans .github/workflows</small></div>
  <div class="trigger">TRIGGER <small>"Action !"" : push, pull request, bouton manuel, planning</small></div>
  <div class="jobs">
  <div class="job">
    <div class="job-title">JOB "ci" <small>une scène · sur un runner</small>
    </div>
  <div class="steps"><div class="step">STEP<small>récupérer le code</small></div><div class="step">STEP<small>lancer les tests</small></div><div class="step">STEP<small>construire l'application</small></div></div>
</div>
<div class="needs">needs<br/>▶</div>
  <div class="job">
    <div class="job-title">JOB "cd" <small>une autre scène, un autre runner</small>
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

# Le runner

<div class="cols3">
    <div class="card">
        <h3>Quel type ?</h3>
        <p><b>Hébergé par GitHub</b> : Linux, Windows ou macOS, nouveau conteneur à chaque job.</p>
        <p class="ex">runs-on: ubuntu-latest<br />runs-on: windows-latest<br />runs-on: macos-latest</p>
    </div>
    <div class="card">
        <h3>Quelle version ?</h3>
        <p>
            <code>ubuntu-latest</code>
        </p>
        <p><code>ubuntu-26.04</code> fixe la version</p>
        <p class="ex">runs-on: ubuntu-26.04</p>
    </div>
    <!-- <div class="card"> -->
    <!-- </div> -->
</div>

<img style="width: 400px;" src="/running-man.gif" class="logo" alt="Running man" />
---

# Un workflow

```yaml {1|2|3-5|6-8}
name: Mon premier workflow       # le titre du workflow
on: push                         # Action ! : le déclencheur
jobs:
  test_the_code:                 # une scène (un job)
    runs-on: ubuntu-latest       # le runner : une machine fournie par GitHub
    steps:
      - uses: actions/checkout@v4   # une action toute faite
      - run: npm test               # une commande
```

<img style="width: 300px; height: auto;" src="/the-plan.gif" class="logo" alt="The plan" />
---

# Deux types d'étapes : run et uses

<div class="cols2">
  <div class="card">
    <h3><code>run:</code></h3>
    <p>Une commande shell.</p>
    <p class="ex">npm test</p>
  </div>
  <div class="card">
    <h3><code>uses:</code></h3>
    <p>Une action réutilisable du Marketplace.</p>
    <p class="ex">actions/checkout@7</p>
  </div>
</div>

---

# Actions du marketplace

<div class="cols3">
    <div class="card">
        <h3><code>checkout</code></h3>
        <p>récupère le code du dépôt sur le runner.</p>
        <p class="ex">actions/checkout@v7</p>
    </div>
    <div class="card">
        <h3><code>setup-node</code></h3>
        <p>installe Node et active le cache npm.</p>
        <p class="ex">actions/setup-node@v7</p>
    </div>
    <div class="card">
        <h3><code>Pages</code></h3>
        <p>publie le site sur GitHub Pages.</p>
        <p class="ex">actions/upload-pages-artifact@v5<br />actions/deploy-pages@v5</p>
    </div>
    <div class="card">
        <h3><code>github-script</code></h3>
        <p>du JavaScript en lien avec l'API GitHub (commentaire de PR, label, issue).</p>
        <p class="ex">actions/github-script@v9</p>
    </div>
    <div class="card">
        <h3><code>send-mail</code></h3>
        <p>Le courrier de fin : envoie un email via SMTP, succès ou échec.</p>
        <p class="ex">dawidd6/action-send-mail@v6</p>
    </div>
</div>
<p class="foot">
    Aussi très utilisées : <code>actions/cache</code>, <code>actions/upload-artifact</code>.
</p>


---

# CI / CD : bon cop / bad cop

<div class="flow">
  <div class="stage"><b>Push</b><small>Action !</small></div>
  <span>▶</span>
  <div class="stage"><b>Checkout</b><small>Récupération de code</small></div>
  <span>▶</span>
  <div class="stage"><b>Die Hard</b><small>Linter</small></div>
  <span>▶</span>
  <div class="stage"><b>Terminator</b><small>Tests unitaires</small></div>
  <span>▶</span>
  <div class="stage"><b>Commando</b><small>Build de production</small></div>
  <span>▶</span>
  <div class="stage"><b>Rambo</b><small>Déploiement</small></div>
</div>

<div class="cols brace">
<div><b>CI</b> : intégration continue<br/>on vérifie le code à chaque modification</div>
<div><b>CD</b> : livraison continue<br/>on publie automatiquement si tout est OK</div>
</div>

<img style="width: 300px; height: auto;" src="/badboys.gif" class="logo" alt="The plan" />

---
layout: center
class: text-center
---

# À vous de jouer !

<div class="steps-list">
  <div><b>1</b>Fork du repo</div>
  <div><b>2</b>Compléter la partie CI</div>
  <div><b>3</b>Compléter la partie CD</div>
  <div><b>4</b>Devenir le véritable Last Github Action hero</div>
</div>

<img style="width: 400px;" src="/prepare.gif" class="logo" alt="Preparation" />
