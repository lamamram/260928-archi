## Template pour l'Atelier sur les Attributs de Qualité 

### Étape 1 : Identifier les Attributs de Qualité Prioritaires

**Méthode** : Quality Attribute Workshop (QAW): Atelier avec les parties prenantes

**Questions clés** :
- Quel est le temps de réponse pour consulter un article acceptable ? < 200ms pour 95% des requêtes sur un scenario de charge normale
- Quel taux de disponibilité exigé ? 99.9% avec bascule < 5s

### Étape 2 : Définir les Scénarios de Qualité

**Format** :
> **Source** → **Stimulus** → **Artefact** → **Environnement** → **Réponse** → **Mesure**
  
- **Source** : utilisateur
- **Stimulus** : requête HTTP
- **Artefact** : afficher la liste produit
- **Environnement** : opération/charge normale
- **Réponse** : réponse sans ou avec bascule
- **Mesure** : dispo à 99.9 à bascule < 5s>

### Étape 3 : Sélectionner les Tactiques


* Scénario 1:
  - cache: Redis facilement réplicable
  - ContentDeliveryNetwork: cloudflare
  - pooling: Doctrine PHP
  - pagination
  - healthcheck
  - ip failover



### Étape 4 : Évaluer les Trade-offs (compromis) et les Risques

**Méthode ATAM** (Architecture Tradeoff Analysis Method) :

* Identifier les trade-offs et Documenter les risques
1. décision: cache
   - trade-off: performance UP / cohérence DOWN
   - risque: données obsolètes pendant le TTL
   - atténuation: TTL court (30s), invalidation proactive sur update


### Étape 5 : Validation des Scénarios de Qualité

* test de performance: Jmeter
```bash
## mesurer le temps de répone moyenne pour 95% de 100 requêtes
jmeter -n -t test_plan.jmx -l results.jtl
```

* test de disponibilité:

```bash
# vérifier que le master de k8s recréé un pod de reverse proxy en cas de défaillance
kubectl delete pod -l app=reverse-proxy
```

### Étape 6 : Documenter les Décisions (ADR)