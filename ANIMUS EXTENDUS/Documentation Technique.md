## Serveur de Conteneurisation
L'infrastructure du Système d'Information d'ABSTERGO, intègre un serveur spécifiquement dédié à la conteneurisation. Cette décision stratégique, découle de la volonté d'offrir une solution efficace pour encapsuler, distribuer et exécuter des applications de manière indépendante, permettant par la même occasion une maintenance ainsi qu'un déploiement accéléré.


Le choix de la conteneurisation plutôt que de la vritualisation repose sur plusieurs considérations clés, visant à optimiser l'efficacité ainsi que la gestion de l'infrastructure. Contrairement à la virtualisation, qui encapsule un système d'exploitation entier avec ses ressources, la conteneurisation isole uniquement l'application et ses dépendances, partageant le même noyau d'exploitation avec le système hôte.

De plus, la conteneurisation offre une grande flexibilité, permettant non seulement une utilisation plus efficiente des ressources système, des temps de démarrage plus rapides, mais également la possibilité de créer rapidement de nouveaux conteneurs pour répartir la charge en cas de besoin. Cette capacité dynamique à ajuster la capacité selon les exigences spécifiques de chaque service garantit une réponse agile aux variations de charge et une utilisation optimale des ressources disponibles


### Plateforme de Conteneurisation
Au sein de l'infrastructure du Système d'Information d'ABSTERGO, la technologie de conteneurisation Docker a été sélectionner en tant que plateforme principale. Il est agréable de noté que, Docker est reconnu pour sa facilité d'utilisation, sa portabilité ainsi que son écosystème riche de conteneurs prêts à l'emploi. Son architecture légère et efficace en faisait un choix idéal, offrant une gestion simplifiée des conteneurs tout en assurant une isolation robuste.

### Services Conteneurisés
Dans le cadre de la migration vers l'infrastructure actuelle, nous avons reconduit plusieurs services présent au sein de l'ancienne architecture. Parmis ces services nous recensons les suivants : 

- **Le système ERP (Enterprise Ressource Plannning), Dolibarr.**

    La conteneurisation de Dolibarr a été privilégiée pour moderniser la gestion des opérations métier. Une approche modulaire a été adoptée à l'aide de Docker Compose. **Toutefois, il est important de noter que la base de données MariaDB n'est pas stockée dans le conteneur Docker, mais dans un emplacement externe. Cette configuration a été délibérément choisie pour simplifier la gestion du conteneur, tout en préservant l'intégrité des données en cas de suppression ou de modification du conteneur.** Cette stratégie garantit une séparation claire entre l'application Dolibarr et ses données sous-jacentes, facilitant ainsi la sauvegarde, la restauration et la gestion globale du Progiciel de Gestion Intégré (PGI / ERP).

    De plus l'adoption de cette nouvelle architecture conteneurisée garantit un environnement isolé et adaptable. Les avantages englobent un déploiement rapide des services, une maintenance simplifiée et une gestion efficace des dépendances entre les composants. Cette orientation renforce la stabilité et la disponibilité de l'ERP tout en simplifiant les ajustements ou évolutions futures de l'infrastructure.

- **L'Autocommutateur téléphonique privé (PBX), Asterisk.**

    La conteneurisation d'Asterisk a été choisie afin de regrouper de manière centralisée plusieurs services connexes. Parallèlement, cette décision a permis l'intégration des services PrivateDial, WebSMS et AutoBan au sein du même conteneur. Comme précedement, cette approche modulaire, orchestrée par Docker Compose, offre le flexibilité nécessaire pour faire coexister et interagir intelligement l'ensemble de ces services au sein du même environement.

    **En revanche il convient de souligner que les données d'Asterisk, comprenant la configuration et les enregistrements, sont délibérément stockées à l'extérieur du conteneur Docker, dans un emplacement dédié. Cette approche, identique à celle choisie pour la conteneurisation de Dolibarr, a pour objectif de simplifier la gestion du conteneur tout en préservant l'intégrité des données en cas de modifications ou de suppression du conteneur.** La séparation distincte entre l'application Asterisk et ses données sous-jacentes facilite ainsi les opérations de sauvegarde, de restauration et de gestion globale du système de communication.

    Cette approche permet, ainsi le déploiement d'un solution modulaire, s'occupant des différents services associés aux systèmes de PBX IP et aux passerelles VoIP. Par ailleurs cette encapsulation permet l'ajout ou le retrait de service similaire, assurant une adaptabilité continue aux besoins évolutifs d'ABSTERGO.
    
### Utilisation de Portainer
Pour simplifier la gestion et favoriser l'intégration harmonieuse des conteneurs actuels et futurs, nous avons opté pour Portainer. Portainer est une interface utilisateur centralisée, largement populaire, qui offre une visualisation claires des conteneurs, images, volumes et réseaux. En complément de Docker, Portainer permet une prise en main facilitée des ressources Docker sur le serveur, évitant ainsi la nécessité d'utiliser des commandes complexes.

Cette combinaison simplifie l'administration des applications et services conteneurisés, facilitant la surveillance, la gestion et l'ajustement des ressources en fonction des besoins spécifiques.

**Le conteneur Portainer est accessible à l'adresse suivante**
```
https://srv-dbn-02.abstergo.internal:9443       <--(Attention à ne pas omettre le port)
```
## Tunneling VPN
Afin d'assurer une communication sécurisée et fiable entre le siège social et le site de Lyon, a été décidé la mise en place d'une solution de tunneling VPN (Vitrual Private Network). Permettant ainsi une connexion cryptée entre les deux sites, garantissant la confidentialité et l'intégrité des données échangées.

Le choix de cette solution a été motivé par plusieurs facteurs clefs. Tout d'abord, IPsec est reconnu comme un protocole de sécurité robuste, proposant des mécanismes de chiffrement solides et des méthodes d'authentification sécurisées. Permettant ainsi de garantir la confidentialité et l'intégrité des données transitant par le tunnel. De plus, sa large adoption en tant que standard ouvert favorise une interopérabilité étendue entre différents équipements réseau, offrant une flexibilité cruciale lors de l'intégration de nouveaux équipements ou de la mise à niveau de l'infrastructure. La flexibilité des options d'authentification, la gestion avancée des tunnels, et les performances optimisées pour un débit réseau élevé sont autant de caractéristiques qui ont influencé ce choix, assurant une connectivité constante, fiable et performante entre les deux sites.

### Scénarios d'utilisations
La mise en place du tunnel VPN entre le siège social et le site de Lyon vise à répondre à des besoins spécifiques, offrant une connectivité sécurisée et facilitant des scénarios d'utilisation essentiels. Les cas d'usage concrets du tunnel VPN comprennent :

- **Accès aux Services Centralisés:** Les utilisateurs du site de Lyon bénéficient d'un accès sécurisé aux services centralisés, hébergés exclusivement au siège social. Cette approche garantit une utilisation fluide de l'ERP et d'autres applications stratégiques.

- **Supervision à Distance:** Le tunnel VPN permet une supervision à distance du site de Lyon à partir du serveur de supervision localisé au siège social. Cette fonctionnalité assure une gestion proactive de la santé du réseau et des systèmes à Lyon.


### Configuration
```
Protocole VPN : IPsec
Phases de Négociation : Phase 1 et Phase 2

Phase 1 (Négotiation Principale)
    - Algorithme de Chiffrement : AES-256
    - Méthode de Hachage : SHA-256
    - Groupe DH (Diffie-Hellman) : Groupe 14 (2048 bits)
    - Durée de vie : 28800 secondes
    - DPD (Détection de Chute de Tunnels) :
        - Activation : Oui
        - Intervalle : 10 secondes
        - Essais avant l'échec : 5 essais


Phase 2 (Négotiation Principale)
    - Protocole : ESP 
    - Algorithme de Chiffrement : AES-256
    - Méthode de Hachage : SHA-256
    - Groupe de Clés PSF (Perfect Forward Secrecy) : Groupe 14 (2048 bits)
    - Durée de Vie : 3600 secondes
    - Keep Alive : Activé


Authentification
    - Méthode : Clé partagée
    - Clé partagée : 0ddda55d3a4af6f8a739a6f3483f9f2a4f8e69cf32aadaf4a3b41049
```

### Évolutivité et Modifications du Tunnel VPN
Cette section vise à mettre en lumière la capacité du tunnel VPN à évoluer en fonction des besoins changeants de l'entreprise et à intégrer des modifications sans compromettre la stabilité du système.

- **Redondance du Tunnel VPN:** Pour garantir une disponibilité continue des services, le tunnel VPN a été conçu avec une architecture redondante. En cas de défaillance d'un lien ou d'un équipement, un tunnel de secours (backup) entre le siège social et le site de Lyon s'active automatiquement. Cette redondance assure une connectivité ininterrompue, minimisant les temps d'indisponibilité potentiels.

- **Adaptabilité aux Évolutions:** L'architecture du tunnel VPN a été pensée pour s'adapter aux évolutions futures du système d'information. Les paramètres de configuration, tels que les algorithmes de chiffrement, les méthodes d'authentification, et les capacités de détection de chute de tunnel, peuvent être ajustés en fonction des meilleures pratiques de sécurité et des besoins opérationnels à venir.
