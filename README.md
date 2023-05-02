# tsv4tsv2kafka
Placement et gestion de fichier tsv directement exploitables par le service tsv2kafka (anciennement bacon2kafka)

## Documentation d'utilisation du dépôt

Ce document explique étape par étape comment modifier des fichiers tsv pour une prise en charge par le service tsv2kafka (anciennement bacon2kafka)

## Sommaire
- [Utilisation de GitHub](#1)
- [Déclenchement de la mise à jour](#2)
- [Langage TSV et particularités propres au service tsv2kafka, structure d'un fichier TSV](#3)
- [Description des champs pour chaque ligne kbart](#4)

## Utilisation de GitHub-  <a id="1"></a>
Github est un outil en ligne permettant de versionner des fichiers. Il dispose d'un éditeur en ligne permettant de modifier des fichiers puis de les sauvegarder tout en conservant un historique des modifications réalisées.

### Notion de branche
Une branche est une version du code disponible dans un projet. Elle dispose de son propre historique, et toutes les modifications effectuées sur cette branche auront leur propre cycle de vie. Pour sélectionner une branche, cliquez sur la liste déroulante : ![branches](https://user-images.githubusercontent.com/57490853/190959280-452d5f2b-a04e-4061-ac49-3bea09ddf00b.PNG) 
et sélectionnez la branche de travail. Le contenu de la branche est affiché.
> Pour modifier les règles et qu'elles soient prises en compte sur l'environnement de test, il est nécessaire de se 
> positionner sur la branche ``main``

### Editer un fichier
Pour modifier le contenu d'un fichier, cliquez sur le nom du fichier à modifier, puis sur la page suivante, cliquez sur le bouton ![edit](https://user-images.githubusercontent.com/57490853/190960013-f2216993-faee-468d-aee5-daf8dd0b41e3.PNG). Un éditeur en ligne s'affichera permettant de modifier le contenu du fichier.

### Sauvegarder un fichier
La sauvegarde d'un fichier est réalisée via l'action commit dans github. Lorsqu'on fichier est en édition, en bas de la page, renseignez un titre dans le premier champ texte, puis une description des modifications effectuées dans le second, cochez la case ``Commit directly to the <nom_de_la_branche> branch`` puis cliquez sur le bouton Commit changes :  
![commit](https://user-images.githubusercontent.com/57490853/190960543-e91a3708-9308-4f43-ad39-111ecb62a1ce.PNG) 
> Un commit est une sauvegarde à laquelle est ajoutée un commentaire.
> Chaque commit donne lieu à une nouvelle entrée dans l'historique des modifications du fichier et de la branche active.

## Déclenchement de la mise à jour <a id="2"></a>
A intervalles de temps régulier, la plateforme Ansible de l'Abes va scanner le dépot Github et détecter les changements sur la branche. Lorsqu'une modification est détectée, Ansible récupère les fichiers disponibles sur la branche, et appelle un programme qui va stocker le contenu des règles décrites dans les différents fichiers dans la base de données. Une fois terminé une notification est envoyée par mail, ainsi que sur le canal Slack #notif-qualimarc.

## Langage TSV et particularités propres au service tsv2kafka<a id="3"></a>

Les tsv dans le cadre du service tsv2kafka
- Les bouquets sont définis dans des fichiers TSV. Un fichier tsv contient des données séparées par des tabulations. Deux tabulations signifient un champ vide.
- Un provider est représenté par un fichier TSV.
- Le nom du provider se place en suffixe du nom de fichier. Exemple: BRILL_cde53_mono_print_only_via_onlineID.tsv ici le provider sera BRILL, exploité alors par le service tsv2kafka.
- La première ligne du fichier contient l'entête avec le nom pour chaque colonne (quoi)
- Les lignes suivantes jusqu'a la fin du fichier représentent un kbart (une ligne kbart)

Concernant la structure d'un fichier tsv
- L'ordre des champs est important
- Chaque tabulation représente le passage au champ suivant
- Deux tabulation qui se suivent représente un champ vide (au milieu des deux tabulations)

Par exemple :  

![image](https://user-images.githubusercontent.com/19894885/235693869-1b0fb07b-6ef7-4ca9-8e21-717fec9474cc.png)
Représentera en donnée
![image](https://user-images.githubusercontent.com/19894885/235694008-785b37a4-ba46-4277-9d34-0b0e6c4131bb.png)

## Description des champs pour chaque ligne kbart<a id="4"></a>
- publication_title	
- print_identifier	
- online_identifier	
- date_first_issue_online	
- num_first_vol_online	
- num_first_issue_online	
- date_last_issue_online	
- num_last_vol_online	num_last_issue_online	
- title_url	
- first_author	
- title_id	
- embargo_info	
- coverage_depth	
- notes	
- publisher_name	
- publication_type	
- date_monograph_published_print	
- date_monograph_published_online	
- monograph_volume	
- monograph_edition	
- first_editor	
- parent_publication_title_id	
- preceding_publication_title_id	
- access_type
