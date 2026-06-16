# 🌳 European Option Pricing — Binomial Tree

> Implémentation Python du modèle de l'arbre binomial (Cox-Ross-Rubinstein) pour le pricing d'options européennes.

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)](https://jupyter.org/)
[![Google Colab](https://img.shields.io/badge/Open%20in-Colab-yellow?logo=google-colab)](https://colab.research.google.com/github/NourSALHI28/European-Option-Pricing-Binomial-Tree/blob/main/Welcome_to_Colab.ipynb)

---

## 📌 Description

Ce projet implémente la méthode de l'**arbre binomial (modèle CRR — Cox, Ross & Rubinstein, 1979)** pour évaluer le prix d'**options européennes** (call et put). Cette approche discrétise l'évolution du prix d'un actif sous-jacent sur plusieurs périodes, permettant de remonter l'arbre pour calculer la valeur actuelle de l'option par actualisation risque-neutre.

Le notebook est conçu pour être exécuté directement dans **Google Colab** sans installation locale.

---

## 📐 Fondements théoriques

### Modèle de l'arbre binomial (CRR)

À chaque nœud de l'arbre, le prix de l'actif peut monter ou descendre selon les facteurs :

```
u = e^(σ√Δt)        # facteur de hausse
d = 1/u = e^(-σ√Δt) # facteur de baisse
```

La probabilité risque-neutre de hausse est :

```
p = (e^(rΔt) - d) / (u - d)
```

### Paramètres du modèle

| Symbole | Description |
|---------|-------------|
| `S`     | Prix spot de l'actif sous-jacent |
| `K`     | Prix d'exercice (strike) |
| `T`     | Maturité (en années) |
| `r`     | Taux sans risque (annualisé) |
| `σ`     | Volatilité implicite (annualisée) |
| `N`     | Nombre de pas de temps (périodes) |

### Payoffs à maturité

- **Call européen** : `max(S_T - K, 0)`
- **Put européen**  : `max(K - S_T, 0)`

La valeur de l'option est obtenue en actualisant récursivement depuis les feuilles jusqu'à la racine de l'arbre.

---

## 📁 Structure du dépôt

```
European-Option-Pricing-Binomial-Tree/
│
├── Welcome_to_Colab.ipynb   # Notebook Jupyter / Google Colab (principal)
├── welcome_to_colab.py      # Version script Python du notebook
└── README.md                # Documentation du projet
```

---

## 🚀 Utilisation

### ▶️ Option 1 — Google Colab (recommandé)

Cliquez sur le badge ci-dessous pour ouvrir directement le notebook dans Colab :

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/NourSALHI28/European-Option-Pricing-Binomial-Tree/blob/main/Welcome_to_Colab.ipynb)

### 💻 Option 2 — Exécution locale

1. **Cloner le dépôt**
```bash
git clone https://github.com/NourSALHI28/European-Option-Pricing-Binomial-Tree.git
cd European-Option-Pricing-Binomial-Tree
```

2. **Installer les dépendances**
```bash
pip install numpy matplotlib
```

3. **Lancer le notebook**
```bash
jupyter notebook Welcome_to_Colab.ipynb
```

Ou exécuter le script Python directement :
```bash
python welcome_to_colab.py
```

---

## 🔢 Exemple d'utilisation

```python
# Paramètres de l'option
S = 100    # Prix spot
K = 100    # Strike
T = 1      # Maturité (1 an)
r = 0.05   # Taux sans risque (5%)
sigma = 0.2  # Volatilité (20%)
N = 100    # Nombre de pas

# Calcul du prix
call_price = binomial_tree(S, K, T, r, sigma, N, option_type='call')
put_price  = binomial_tree(S, K, T, r, sigma, N, option_type='put')

print(f"Call européen : {call_price:.4f}")
print(f"Put européen  : {put_price:.4f}")
```

---

## 📊 Résultats attendus

Avec les paramètres ci-dessus (S=K=100, T=1, r=5%, σ=20%, N=100) :

| Option | Prix (Binomial) | Prix (Black-Scholes) |
|--------|----------------|----------------------|
| Call   | ~10.45          | ~10.45               |
| Put    | ~5.57           | ~5.57                |

> À mesure que `N` augmente, le prix binomial converge vers le prix Black-Scholes analytique.

---

## 📚 Références

- Cox, J.C., Ross, S.A., & Rubinstein, M. (1979). *Option pricing: A simplified approach*. Journal of Financial Economics, 7(3), 229–263.
- Hull, J.C. (2018). *Options, Futures, and Other Derivatives* (10th ed.). Pearson.
- Black, F., & Scholes, M. (1973). *The Pricing of Options and Corporate Liabilities*. Journal of Political Economy, 81(3), 637–654.

---

## 👤 Auteur

**Nour SALHI**  
[GitHub](https://github.com/NourSALHI28)

---

## 📝 Licence

Ce projet est distribué à des fins éducatives. Libre d'utilisation pour l'apprentissage et la recherche.
