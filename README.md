# Team : Rihab Ben Amor Souissi(3IDL2), Eya Ben El kadhi(3IDL2), Rouaa Mahmoudi (3IDL1), Sarah Hosni (3IDL1)
# Amal 
#Architecture Microservices DeepSeek

1. Accès : Web, Mobile, APIs externes → via API Gateway (sécurisée + Auth centralisée).
2. Services Métier : Utilisateurs, Recherche, ML, Notifications, Facturation… → découplés, autonomes.
3. Support : Logs, Config, Audit → observabilité & sécurité.
4. Infrastructure : BDD, Broker (async), Kubernetes, Monitoring → scalabilité & résilience.

Avantages : Évolutive, sécurisée, observable, haute dispo — idéale pour l’IA et la recherche à grande échelle.
# Critique 
DeepSeek utilise des modèles de deep learning, plus précisément une architecture Mixture-of-Experts (MoE) avancée, et non un système expert traditionnel.
#raisons
Systèmes Experts traditionnels : Utilisent des règles logiques programmées explicitement et une base de connaissances structurée.
Par contre 
DeepSeek : Utilise l'apprentissage profond où les modèles de comportement de raisonnement complexes peuvent se développer naturellement par apprentissage par renforcement sans programmation explicite
=>L'architecture MoE divise un modèle IA en sous-réseaux séparés (ou "experts"), chacun se spécialisant dans un sous-ensemble des données d'entrée, ce qui est dramatiquement moins intensif en ressources pour l'entraînement
# Proposition d'amélioration de l'architecture 
  * Décomposition du Service ML en sous-services spécialisés :
 Service Modèles : gestion des modèles entraînés, versions, déploiement (MLOps)
 Service Inférence : exécution des prédictions
 Service Apprentissage : entraînement automatique, orchestration (via Airflow/Kubeflow)
Raison :
Un seul service ML est trop monolithique. Cette décomposition permet : 

  Une meilleure scalabilité 
  Des pipelines d’apprentissage autonomes
  Une mise à jour sans impact sur l’inférence
  Une intégration plus facile avec des outils MLOps
