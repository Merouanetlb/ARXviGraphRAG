# Brief projet — Graph RAG sur la littérature en inférence efficace des LLM

## Objectif
Projet portfolio GitHub pour trouver un emploi (ML engineer / NLP) et appuyer une candidature CIFRE en optimisation de l'IA. Le projet doit être fini, évalué avec des chiffres, démontrable (démo en ligne) et bien documenté.

## Sujet
Graph RAG sur la littérature scientifique en **inférence efficace des LLM** : quantization, distillation, pruning, speculative decoding, KV cache, sparsité, etc.

Exemples de questions visées (multi-hop, là où un RAG vectoriel classique échoue) :
- Quelles méthodes de quantization ont été comparées à GPTQ sur Llama, et avec quels résultats ?
- Quelles méthodes ont succédé à X, et sur quels benchmarks ont-elles été évaluées ?
- Quels auteurs ou labos travaillent à la fois sur la distillation et le speculative decoding ?

## Périmètre
- Papiers arXiv (principalement cs.CL, cs.LG) de 2020 à 2026 sur le sous-domaine.
- Taille cible : quelques milliers à ~20 000 papiers, gérable sur une machine perso.
- Élargissement possible plus tard, pas dans le MVP.

## Sources de données
- **arXiv** : métadonnées (titre, abstract, auteurs, catégories, dates) via le dataset Kaggle ou l'API officielle ; PDF si besoin du texte intégral (attention aux licences en cas de redistribution).
- **Semantic Scholar** : graphe de citations, auteurs désambiguïsés, intentions de citation. API gratuite, clé à demander.
- **OpenAlex** : clé API gratuite obligatoire depuis 2026 (1 $/jour de budget gratuit, suffisant) ; snapshot complet CC0 téléchargeable gratuitement sur S3.

## Défi principal
Aucune source ne fournit proprement les entités **méthodes, datasets, métriques, tâches, résultats** (Papers with Code a fermé). Il faut les extraire depuis les abstracts / le texte par NER ou LLM. C'est la valeur ajoutée du projet.
Ressources utiles pour entraîner / évaluer l'extraction : SciERC, SciREX.

## Stack envisagée (à confirmer)
- Graphe : Neo4j
- Embeddings : bge-m3 ; reranker : bge-reranker-v2-m3
- LLM local : Qwen ou Mistral via vLLM
- API : FastAPI ; démo : Gradio / Hugging Face Spaces
- Orchestration éventuelle : LangGraph

## Évaluation (prévue)
- Jeu de questions (factuelles, multi-hop, comparatives).
- Métriques retrieval (recall@k) et qualité des réponses (fidélité aux sources, exactitude).
- Comparaison : vecteur seul / graphe seul / hybride / hybride + reranker, éventuellement Microsoft GraphRAG ou LightRAG.
- Tableau de résultats dans le README.

## Contraintes
- Données publiques uniquement, implémentation entièrement personnelle, aucun lien avec des travaux de stage.
- Réponses toujours sourcées (papiers cités).

## Organisation
- Projet Claude : une conversation par chantier (schéma du graphe, ingestion, extraction d'entités, retrieval, évaluation, README).
- Ce brief est mis à jour à chaque décision importante.
- Implémentation avec Claude Code dans le repo (même brief dans `CLAUDE.md`).

## Décisions prises
- Sujet et périmètre ci-dessus validés.

## Prochaine étape
Définir le schéma du graphe (types de nœuds, relations, propriétés).