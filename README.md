# Glade-install-Linux

# Compilation de Glade 3.40.0 — Guide

Ce document décrit les prérequis et la procédure d'installation des dépendances
nécessaires pour compiler Glade 3.40.0 depuis les sources avec Meson + Ninja.

---

## Partie 1 — Prérequis

### Système d'exploitation
- ** Ubuntu 22.04 (Jammy)** ou distribution dérivée basée sur Debian.
- Les commandes `apt` ci-dessous sont valables pour ces distributions.

### Outils de build
| Outil | Rôle |
|---|---|
| `meson` | Système de configuration et de build |
| `ninja-build` | Moteur de build utilisé par Meson |
| `gcc` | Compilateur C |
| `git` | Récupération des sources (si besoin) |

### Bibliothèques de développement
| Paquet | Rôle |
|---|---|
| `libgtk-3-dev` | Bibliothèque GTK+ 3 (interface graphique) |
| `libxml2-dev` | Analyse XML (fichiers `.glade`, catalogues) |
| `libglib2.0-dev` | Bibliothèque GLib/GObject/GIO |
| `libgirepository1.0-dev` | GObject Introspection (obligatoire pour Gladeui) |

### Outils de génération de documentation / traduction
| Paquet | Rôle |
|---|---|
| `itstool` | Traitement des fichiers de traduction ITS (aide) |
| `gettext` | Fournit `msgmerge`, `msgfmt` (traductions) |
| `xsltproc` | Processeur XSLT (génération des pages `man`) |
| `docbook-xsl` | Feuilles de style DocBook XSL (pour `xsltproc`) |
| `docbook-xml` | DTD DocBook XML |

### Outils optionnels (non bloquants)
| Paquet | Rôle |
|---|---|
| `libgjs-dev` | Support JavaScript dans Glade (GJS Widgets) |
| `python3-gi` | Support Python dans Glade |
| `libxml2-utils` | Fournit `xmllint` (supprime un warning de build) |

---

## Partie 2 — Installation des dépendances

### Étape 1 — Mise à jour de l'index des paquets

```bash
sudo apt update
```

### Étape 2 — Installation des outils de build

```bash
sudo apt install meson ninja-build gcc git
```

### Étape 3 — Installation des bibliothèques de développement

```bash
sudo apt install libgtk-3-dev libxml2-dev libglib2.0-dev libgirepository1.0-dev
```

### Étape 4 — Installation des outils de documentation / traduction

```bash
sudo apt install itstool gettext xsltproc docbook-xsl docbook-xml
```

### Étape 5 (optionnelle) — Support JavaScript, Python et `xmllint`

```bash
sudo apt install libgjs-dev python3-gi libxml2-utils
```

### Étape 6 — Vérification rapide

Vérifie que les outils essentiels sont bien disponibles :

```bash
meson --version
ninja --version
gcc --version
pkg-config --modversion gtk+-3.0
pkg-config --modversion gobject-introspection-1.0
```

---

## Partie 3 — Compilation (résumé)

Depuis le dossier `glade-3.40.0` :

```bash
rm -rf builddir
meson setup builddir
ninja -C builddir
```

### Lancer Glade sans installation

```bash
./builddir/src/glade
```

### Installer sur le système

```bash
sudo ninja -C builddir install
```

---

## Notes

- Les `warning` du type `g_memdup is deprecated` sont **normaux** : Glade 3.40.0
  est plus ancien que la GLib installée. Ils n'empêchent pas la compilation.
- Le message `XMLLINT n'est pas défini` peut être ignoré, ou supprimé en
  installant `libxml2-utils`.
- Le support **Python** (`pygobject-3.0`) est optionnel et peut rester désactivé.

---

## Commande "tout-en-un"

Pour installer toutes les dépendances d'un coup (copier-coller) :

```bash
sudo apt update && sudo apt install -y \
    meson ninja-build gcc git \
    libgtk-3-dev libxml2-dev libglib2.0-dev libgirepository1.0-dev \
    itstool gettext xsltproc docbook-xsl docbook-xml \
    libgjs-dev python3-gi libxml2-utils
```

# Licence MIT




