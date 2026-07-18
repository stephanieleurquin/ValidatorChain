# 🔗 ValidatorChain

**Validez vos données en chaîne avec des messages pédagogiques !**

[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-orange.svg)](https://pypi.org/project/validator-chain/)

---

## 📖 À quoi ça sert ?

**ValidatorChain** est une bibliothèque Python qui vous permet de **valider des données** (mots de passe, emails, numéros de téléphone, âges, etc.) en **enchaînant des règles** de manière fluide et intuitive.

**Sa particularité ?** Elle ne se contente pas de dire "valide" ou "invalide". Elle vous **explique POURQUOI** une donnée est invalide, avec des **messages clairs et pédagogiques**.

---

## 🚀 Installation

bash
pip install validator-chain

git clone https://github.com/votre-nom/validator-chain.git
cd validator-chain
pip install -e .

from validator_chain import ValidatorChain

####Exemple concret #####

# Créer une chaîne de validation pour un mot de passe
validator = ValidatorChain() \
    .nom_champ("Mot de passe") \
    .not_empty() \
    .min_length(8) \
    .has_majuscule() \
    .has_minuscule() \
    .has_chiffre() \
    .has_special()

# Tester un mot de passe
resultat = validator.valider("MonPassword123!")

if resultat.valide:
    print("✅ Mot de passe valide !")
else:
    print("❌ Mot de passe invalide :")
    for erreur in resultat.erreurs:
        print(f"   - {erreur}")

   Sortie :
        ✅ Mot de passe valide !

        🛠️ Fonctionnalités
✅ Validateurs inclus
Validateur	Description
.not_empty()	La valeur ne doit pas être vide
.min_length(n)	Longueur minimale
.max_length(n)	Longueur maximale
.is_email()	Format email valide
.is_phone()	Numéro de téléphone français
.has_majuscule()	Contient au moins une majuscule
.has_minuscule()	Contient au moins une minuscule
.has_chiffre()	Contient au moins un chiffre
.has_special()	Contient au moins un caractère spécial
.is_int()	Est un nombre entier
.is_float()	Est un nombre décimal
.gt(n)	Strictement supérieur à n
.gte(n)	Supérieur ou égal à n
.lt(n)	Strictement inférieur à n
.lte(n)	Inférieur ou égal à n
.custom(fonction, message)	Validation personnalisée
✅ Options avancées
python
# Personnaliser le nom du champ (pour les messages d'erreur)
validator.nom_champ("Email")

# Arrêter à la première erreur (mode "fail fast")
validator.fail_fast(True)
✅ Validation avec exception
python
try:
    validator.valider_raise("test")
except ValueError as e:
    print(e)  # Validation échouée: Mot de passe doit faire au moins 8 caractères, ...
📝 Exemples d'utilisation
🔐 Validation d'un mot de passe
python
validator = ValidatorChain() \
    .nom_champ("Mot de passe") \
    .not_empty("Veuillez saisir un mot de passe") \
    .min_length(8, "8 caractères minimum requis") \
    .has_majuscule("Au moins une majuscule requise") \
    .has_chiffre("Au moins un chiffre requis")

resultat = validator.valider("monmdp")

print(resultat.valide)  # False
for erreur in resultat.erreurs:
    print(erreur)
# 8 caractères minimum requis
# Au moins une majuscule requise
# Au moins un chiffre requis
📧 Validation d'un email
python
validator = ValidatorChain() \
    .nom_champ("Email") \
    .not_empty() \
    .is_email()

print(validator.valider("toto@gmail.com").valide)  # True
print(validator.valider("pasunemail").valide)      # False
📱 Validation d'un numéro de téléphone
python
validator = ValidatorChain() \
    .nom_champ("Téléphone") \
    .not_empty() \
    .is_phone()

print(validator.valider("0612345678").valide)  # True
print(validator.valider("0123").valide)        # False
🎂 Validation d'un âge
python
validator = ValidatorChain() \
    .nom_champ("Âge") \
    .is_int() \
    .gt(0, "L'âge doit être positif") \
    .lt(150, "L'âge doit être inférieur à 150")

print(validator.valider(25).valide)   # True
print(validator.valider(-5).valide)   # False
print(validator.valider(200).valide)  # False
✏️ Validation personnalisée
python
validator = ValidatorChain() \
    .nom_champ("Code") \
    .custom(lambda x: x.startswith("ABC"), "Le code doit commencer par ABC")

print(validator.valider("ABC123").valide)  # True
print(validator.valider("XYZ123").valide)  # False
🗂️ Structure du projet
text
validator_chain/
├── validator_chain/
│   ├── __init__.py          # Point d'entrée de la bibliothèque
│   └── chain.py             # Le code principal (ValidatorChain)
├── tests/
│   └── test_chain.py        # Tests unitaires (à créer)
├── README.md                # Ce fichier
├── setup.py                 # Installation avec pip
└── LICENSE                  # Licence MIT
🔧 Développement
Installer en mode développement
bash
git clone https://github.com/votre-nom/validator-chain.git
cd validator-chain
pip install -e .
Exécuter les tests
bash
pip install pytest
pytest tests/
📦 Publication sur PyPI
bash
# Installer les outils
pip install build twine

# Construire la bibliothèque
python -m build

# Publier sur PyPI
python -m twine upload dist/*
🤝 Contribuer
Les contributions sont les bienvenues !

Forkez le projet

Créez votre branche (git checkout -b feature/amazing)

Committez vos changements (git commit -m 'Add amazing feature')

Pushez vers la branche (git push origin feature/amazing)

Ouvrez une Pull Request

📄 Licence
Ce projet est sous licence MIT. Voir le fichier LICENSE pour plus de détails.

👤 Auteur
Vanschoor S.



🙏 Remerciements
Inspiré par les besoins de validation pédagogique dans les applications Python. Un grand merci à la communauté open-source.

⭐ Soutenez le projet
Si ce projet vous est utile, n'hésitez pas à :

⭐ Le starrer sur GitHub

🐛 Reporter des bugs

💡 Suggérer des améliorations

🔧 Contribuer au code

Fait avec ❤️ pour la communauté Python


`
