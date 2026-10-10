# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Nature du dépôt

Dépôt privé de **documentation uniquement** (Markdown) : pas de code, de build, de lint ni de tests. Il regroupe des comptes rendus de travaux faits avec Claude Code. `README.md` sert d'index et renvoie vers chaque dossier de sujet ; tout nouveau document doit y être ajouté en lien.

Contenu actuel : `documents-reorganization/` (méthode de rangement de Documents et Drive, puis méthodes de chiffrement AES-256 zip et Cryptomator).

## Règles propres à ce dépôt

- **Contenu anonymisé et générique.** Ne jamais écrire de nom, d'e-mail, de mot de passe, de code, de clé de récupération, d'identifiant Drive, de nom de coffre ni de contenu de fichier personnel. Relancer une recherche de ces éléments avant chaque commit.
- **Ne pas décrire les failles de la configuration de l'utilisateur** (niveau de protection réel, données laissées en clair, force des codes). Les détails sensibles vont dans le dépôt séparé `documents-reorganization-log`, pas ici.
- Les documents sont en anglais, sauf ce fichier ; les noms de dossiers cités (`00_INBOX`, `01_ADMINISTRATIF`...) restent en français.
- Commits : identité « noreply » GitHub de l'utilisateur (jamais son e-mail réel) et ligne `Co-Authored-By: Claude Sonnet 5.5 <noreply@anthropic.com>` en fin de message.
- Le dépôt est **privé** : ne pas le passer en public sans demande explicite de l'utilisateur.
