# 🐳 Exploration Docker

## 1. Recherche d’images Docker


| Nom de l’image | Lien Docker Hub | Description | Pourquoi ce choix |
|----------------|-----------------|--------------|-------------------|
| **redis** | [https://hub.docker.com/_/redis](https://hub.docker.com/_/redis) | Base de données en mémoire clé-valeur, très rapide, souvent utilisée pour le cache ou les files d’attente. | Parfait pour apprendre à gérer le cache d’une application et améliorer les performances. |
| **grafana** | [https://hub.docker.com/r/grafana/grafana](https://hub.docker.com/r/grafana/grafana) | Plateforme open source pour la visualisation de métriques et la supervision. | Très utile pour monitorer des conteneurs ou une infrastructure complète. |
| **node** | [https://hub.docker.com/_/node](https://hub.docker.com/_/node) | Environnement JavaScript côté serveur basé sur V8. | Idéal pour tester des APIs ou des applications web en Node.js sans rien installer localement. |
| **mysql** | [https://hub.docker.com/_/mysql](https://hub.docker.com/_/mysql) | Système de gestion de base de données relationnelle très répandu. | Permet de comparer avec PostgreSQL ou de pratiquer les requêtes SQL. |
| **portainer** | [https://hub.docker.com/r/portainer/portainer-ce](https://hub.docker.com/r/portainer/portainer-ce) | Interface web pour gérer facilement ses conteneurs, volumes, réseaux et images Docker. | Excellent outil pour visualiser et administrer Docker sans ligne de commande. |

---

## 2. Propositions d’usages personnels

1. **Créer un serveur de développement local**  
   - Utiliser `nginx` pour tester un site statique ou une API en local.  
   - Associer avec `postgres` ou `mongo` pour une base de données de test.

2. **Héberger un outil d’analyse interne**  
   - Déployer `metabase` connecté à `postgres` pour visualiser des données de projets ou d’expériences.

3. **Monter un mini cloud personnel**  
   - Utiliser `nextcloud` ou `wordpress` pour héberger ses propres fichiers et pages web sur un serveur local.

4. **Simuler une architecture microservices**  
   - Lancer plusieurs conteneurs (`nginx` + `api-python` + `db`) reliés via un réseau Docker pour comprendre les interactions entre services.

5. **Tester une base NoSQL**  
   - Jouer avec `mongo` pour insérer, requêter et comparer la performance par rapport à PostgreSQL.
