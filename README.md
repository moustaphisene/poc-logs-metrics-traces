# poc-logs-metrics-traces
L'observabilité d'une application se réfère à la capacité de surveiller et de comprendre l'état interne d'un système en analysant les sorties externes telles que les journaux, les métriques et les traces. C'est un concept crucial pour la gestion des systèmes modernes, en particulier ceux qui sont distribués, complexes et évolutifs.

Composants de l'observabilité :
Logs (journaux) : Ils fournissent des enregistrements séquentiels des événements survenus dans l'application. Ils sont essentiels pour diagnostiquer les problèmes après coup.

Métriques : Ce sont des mesures quantitatives du comportement d'une application, comme l'utilisation du CPU, la mémoire, le nombre de requêtes par seconde, etc.

Traces : Elles montrent le parcours d'une requête à travers divers services d'une application distribuée, ce qui est essentiel pour comprendre le contexte global d'une transaction.

Importance de l'observabilité pour la sécurité des systèmes d'information (SI) :
Détection proactive des menaces : Une observabilité avancée permet d'identifier rapidement les comportements anormaux, comme une augmentation inattendue du trafic, des erreurs récurrentes ou des tentatives d'accès non autorisées. Cela permet de réagir rapidement avant qu'une menace ne devienne un incident majeur.

Réponse rapide aux incidents : Lorsqu'un incident de sécurité survient, l'observabilité permet d'accélérer l'analyse de la cause racine. Avec des journaux détaillés et des traces, les équipes de sécurité peuvent retracer l'incident et identifier les points faibles à corriger.

Conformité et audits : De nombreuses réglementations exigent une surveillance rigoureuse des systèmes pour assurer leur sécurité. L'observabilité permet de maintenir les journaux d'audit nécessaires pour démontrer la conformité aux normes de sécurité.

Prévention des interruptions de service : En identifiant rapidement les problèmes potentiels (comme une surcharge système ou des erreurs applicatives), l'observabilité aide à éviter les pannes qui pourraient être exploitées par des attaquants.

Amélioration continue : En analysant les données collectées, les équipes peuvent améliorer en continu la résilience et la sécurité de l'application. Les failles de sécurité découvertes peuvent être corrigées avant qu'elles ne soient exploitées.

NB: L'observabilité est un pilier essentiel pour assurer la sécurité des systèmes d'information. Elle permet non seulement de détecter et de répondre rapidement aux menaces, mais aussi d'améliorer continuellement la posture de sécurité d'une organisation. Sans une observabilité adéquate, il est presque impossible de garantir la sécurité et la résilience d'une application moderne.

Voici comment cette architecture fonctionne :

Front End :

C'est l'interface utilisateur ou le client qui interagit avec l'application.
Il envoie des requêtes HTTP à l'application via un API Gateway.
API Gateway :

Il agit comme un point d'entrée unique pour toutes les requêtes externes.
Les requêtes sont ensuite transmises au service approprié, ici représenté par le Product-service.
Product-service (Actuator) :

C'est le service principal de l'application qui gère les requêtes des utilisateurs.
Il communique avec d'autres services distants (Remote Service) via des requêtes HTTP.
Ce service utilise Actuator, un outil de Spring Boot, pour exposer des points de terminaison qui permettent de surveiller l'état de l'application, comme la santé, les métriques, et les informations de traçage.
Prometheus :

Prometheus est utilisé pour collecter les métriques du Product-service.
Il interroge périodiquement le service pour récupérer ces métriques et les stocker pour une analyse ultérieure.
Loki (Logs) :

Les logs générés par le Product-service sont envoyés à Loki via Loki4jAppender.
Loki est un système de gestion des logs, il permet de centraliser et de rechercher les logs de manière efficace.
Zipkin :

Zipkin est un système de traçabilité distribuée qui collecte et gère les traces des requêtes traversant les différents services.
Le Product-service pousse ses traces vers Zipkin pour permettre une visualisation et une analyse de bout en bout des requêtes.
Tempo :

Tempo est un autre outil de traçabilité, il interroge les traces stockées pour fournir une vue globale des performances et du chemin des requêtes dans l'application.
Grafana :

Grafana est une plateforme de visualisation qui s'intègre avec Prometheus, Loki, Zipkin, et Tempo.
Elle permet de créer des tableaux de bord (dashboards) pour visualiser les métriques, les logs, et les traces de l'application de manière cohérente et unifiée.

En définitice, Les requêtes des utilisateurs sont gérées par le Product-service via l'API Gateway.
Prometheus collecte les métriques du Product-service.
Loki reçoit et gère les logs du service.
Zipkin et Tempo gèrent les traces pour permettre une analyse de bout en bout des requêtes.
Enfin, Grafana centralise toutes ces informations (métriques, logs, traces) pour les visualiser sur un tableau de bord unique, permettant une meilleure observabilité et gestion de l'application.
Cette architecture est essentielle pour garantir que les équipes peuvent surveiller la performance, diagnostiquer les problèmes, et assurer la sécurité du système en réagissant rapidement aux incidents potentiels.
