# Comptes élèves du Labo Arduino

Le script `Code.gs` relie le Labo Arduino à un Google Sheet : connexion avec l'adresse de l'école (ou un code reçu par e-mail), suivi des défis de chaque élève, page « Mes élèves » pour les professeurs. C'est le même système que le Banc de câblage, avec ses propres données.

Sans compte, le Labo reste entièrement utilisable : rien n'est verrouillé, mais rien n'est envoyé au professeur.

## Mise en route (une seule fois, avec le compte de l'école)

1. Créer un Google Sheet vide nommé **Labo Arduino – données**.
2. **Extensions › Apps Script**. Renommer le projet **Labo Arduino – comptes**. Effacer le contenu de `Code.gs`, coller tout le fichier [`Code.gs`](Code.gs), enregistrer.
3. En haut, choisir la fonction **installer** puis **Exécuter**. Accepter les autorisations (Google affiche « application non validée » : c'est votre propre script, cliquer sur *Paramètres avancés › Accéder à…*). Le script crée les onglets Profs, Classes, Autorisés, Demandes, Résultats et Journal.
4. Choisir la fonction **autoriserPlateforme** puis **Exécuter** (une fois) : Google demande l'autorisation de contacter la Plateforme technique, pour la connexion automatique depuis la plateforme.
5. **Paramètres du projet** (roue dentée à gauche) › **Propriétés du script** › Ajouter : `CLE_PROF` = le mot de passe du mode prof du Labo. Les professeurs connectés ont alors les solutions sans taper le mot de passe.
6. Créer les deux déploiements : **Déployer › Nouveau déploiement › roue dentée › Application Web**.

   | Déploiement | Description | Exécuter en tant que | Qui a accès |
   |---|---|---|---|
   | A | Connexion | Moi | Tous les utilisateurs de elmarche.be |
   | B | Données | Moi | Tout le monde |

7. Copier l'**URL de l'application Web** de chacun (elle se termine par `/exec`) et les mettre dans l'app : `var CPT = {loginUrl: A, apiUrl: B}` dans `index.html`.

## Installation actuelle

- Google Sheet « Labo Arduino – données » et projet Apps Script « Labo Arduino – comptes » (compte olivier.lesenfants@elmarche.be), propriété CLE_PROF réglée.
- Les deux adresses (Connexion et Données) sont dans `index.html`.

## Onglets

- **Profs** : adresses des professeurs (solutions et page « Mes élèves »). La remarque « Propriétaire » donne le rôle administrateur.
- **Classes** : une ligne par classe, avec l'adresse du professeur.
- **Autorisés** : adresses autorisées, ou tout un domaine en écrivant `@domaine.be`. L'installation y met `@elmarche.be` : tous les élèves de l'école sont suivis dès leur première connexion. Retirer cette ligne pour valider chaque élève un par un.
- **Demandes** : premières connexions en attente d'accord (adresses hors domaine autorisé).
- **Résultats** : une ligne par élève et par défi (essais, réussi ou non, au combientième essai, dates).
- **Journal** : chaque vérification, avec sa date et le message du testeur.

## Mettre à jour le script

Recoller le code, exécuter **installer**, puis **Gérer les déploiements › crayon › Nouvelle version**, pour chacun des deux déploiements (les adresses ne changent pas).
