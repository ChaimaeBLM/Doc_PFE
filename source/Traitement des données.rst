Traitement des Donnnées 
==========================
---------------------------------


1. Introduction
---------------
- 1.1 Objectif du traitement des données  
Malgré les avancées significatives dans le domaine du traitement automatique du langage naturel (NLP), l'acquisition et la curation de jeux de données textuelles de haute qualité restent un défi pour de nombreux praticiens des données. L'absence d'outils de prétraitement automatisés fiables nécessite souvent une intervention humaine sous forme d’étiquetage et de curation manuels — un processus long, fastidieux, et souvent peu plaisant. Cela est particulièrement vrai lorsqu’on travaille avec des données brutes non structurées. Ces dernières constituent une catégorie vaste qui englobe, entre autres, les quantités massives de textes et de publications sur les réseaux sociaux disponibles en ligne.

Un autre défi pour les praticiens des données est le processus de détection et de filtrage des informations sensibles, privées, ou non désirées dans les jeux de données. Selon Marinelli et al. (2020), ce processus est « presque entièrement confié à l'expérience des experts humains du domaine, qui sont submergés par le nombre énorme et en constante augmentation de documents à traiter ». Il en résulte que les data scientists et analystes passent la majeure partie de leur temps à nettoyer, organiser et préparer les données, plutôt qu’à les analyser ou les exploiter (Forbes, 2016 ; Weka, 2023).

Ces défis sont aujourd’hui partiellement relevés par les pipelines automatisés de traitement des données : des algorithmes, modèles statistiques et autres outils NLP permettent de gérer efficacement de grandes quantités de données. Entraîner des modèles de machine learning (ML) pour la correction d’erreurs, le nettoyage des données ou d’autres étapes de prétraitement est une option viable, mais cela requiert des jeux de données d’entraînement difficiles à obtenir, car ils doivent être annotés et étiquetés manuellement. Le problème de ces méthodes traditionnelles est qu’elles sont souvent limitées aux tâches spécifiques et aux types de contenus pour lesquels elles ont été conçues. Par conséquent, elles ne sont pas généralisables à de nouvelles tâches et échouent face à des variations inattendues dans le contenu ou le type de données.

Les modèles de deep learning (DL) plus sophistiqués peuvent mieux s’en sortir, mais nécessitent souvent une curation manuelle chronophage des jeux de données, ainsi qu’un fine-tuning coûteux en ressources computationnelles pour être efficaces.

Les grands modèles de langage (LLM), en revanche, ont montré une capacité remarquable à s’adapter à un large éventail de tâches de génération de texte grâce à leurs compétences générales en NLP. Cela les rend plus adaptés aux tâches complexes caractérisées par des variations imprévues, fréquentes dans la préparation de données. Les LLM comme GPT-3.5 affichent des performances à l’état de l’art pour des tâches simples sur des données tabulaires structurées, incluant la reconnaissance d’entités nommées (NER), la détection d’erreurs et l’imputation de données (Zhang et al., 2023 ; Wang et al., 2023). Cela soulève la question de savoir si ces capacités peuvent être étendues à des tâches de prétraitement plus complexes et globales impliquant des données brutes non structurées.

Si les LLM peuvent résoudre des tâches complexes de gestion des données et être utilisés comme préprocesseurs avancés, cela permettrait d’automatiser des pipelines de gestion des données complexes — ce qui constitue depuis longtemps le "graal" de la communauté de gestion des données. Deux principaux défis se dressent toutefois sur cette voie : le manque de connaissances sur la façon d’implémenter les LLM comme préprocesseurs avancés, et les problématiques classiques liées à toute mise en œuvre de LLM. Pollution des données, ressources computationnelles, passage à l’échelle, sécurité des données, protection de la vie privée, hallucinations, et problèmes de fiabilité sont autant de défis à surmonter pour rendre les LLM viables en tant que préprocesseurs de données avancés.

- 1.2 Contexte d’utilisation d’AugmentoToolkit  
- 1.3 Vue d’ensemble du pipeline de traitement  

2. Présentation d’AugmentoToolkit
----------------------------------
- 2.1 Description générale de l’outil  
- 2.2 Fonctionnalités clés utilisées  
- 2.3 Justification du choix d’AugmentoToolkit  

3. Préparation des données sources
----------------------------------
- 3.1 Types de fichiers acceptés (PDF, DOCX, TXT, HTML, CSV, EPUB, etc.)  
- 3.2 Structure des répertoires et organisation des fichiers  
- 3.3 Méthodes d’extraction des textes depuis différents formats  
  - 3.3.1 Extraction des textes depuis des fichiers PDF  
  - 3.3.2 Nettoyage des métadonnées et balises HTML  
  - 3.3.3 Gestion de l’encodage et des caractères spéciaux  

4. Segmentation et filtrage des textes
--------------------------------------
- 4.1 Stratégie de segmentation en paragraphes  
- 4.2 Critères de sélection des segments pertinents  
- 4.3 Élimination des doublons et des sections non pertinentes  
- 4.4 Langues traitées et détection automatique de la langue  

5. Génération automatique de questions-réponses
-----------------------------------------------
- 5.1 Configuration du modèle LLM utilisé (via API compatible OpenAI)  
- 5.2 Paramètres de génération (nombre de QA, température, top_p, etc.)  
- 5.3 Stratégies d’alignement des QA avec le contenu source  
- 5.4 Exemples concrets de QA générées  

6. Post-traitement et validation
--------------------------------
- 6.1 Vérification manuelle des QA générées (qualité, cohérence)  
- 6.2 Détection et suppression des QA non pertinentes  
- 6.3 Structuration finale des données (format JSONL)  
- 6.4 Ajout éventuel de métadonnées (catégories, sources, tags)  

7. Exportation et sauvegarde des données
----------------------------------------
- 7.1 Format de sortie standard (JSONL pour le fine-tuning)  
- 7.2 Exemple de structure d’un fichier JSONL  
- 7.3 Stockage dans une base de données ou un répertoire local  
- 7.4 Gestion des versions des jeux de données générés  

8. Problèmes rencontrés et solutions apportées
----------------------------------------------
- 8.1 Problèmes liés à l’extraction de texte (PDF scannés, tableaux, etc.)  
- 8.2 Problèmes de cohérence linguistique  
- 8.3 Limitations rencontrées avec l’API ou le modèle utilisé  
- 8.4 Optimisations effectuées pour améliorer les performances  

9. Perspectives d’amélioration
------------------------------
- 9.1 Automatisation complète du pipeline  
- 9.2 Intégration de la validation humaine via interface  
- 9.3 Utilisation de modèles multilingues ou spécialisés  
- 9.4 Adaptation à d’autres types de données (audio, vidéo, etc.)  

10. Annexes
-----------
- 10.1 Schémas du pipeline de traitement  
- 10.2 Scripts ou fichiers de configuration utilisés  
- 10.3 Références techniques (liens vers la doc AugmentoToolkit, API LLM, etc.)  
- 10.4 Liste des sources traitées (noms de fichiers ou types de documents)
