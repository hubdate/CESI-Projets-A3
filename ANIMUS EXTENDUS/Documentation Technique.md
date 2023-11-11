## Serveur de Conteneurisation
L'infrastructure du Système d'Information d'ABSTERGO, intègre un serveur spécifiquement dédié à la conteneurisation. Cette décision stratégique, découle de la volonté d'offrir une solution efficace pour encapsuler, distribuer et exécuter des applications de manière indépendante, permettant par la même occasion une maintenance ainsi qu'un déploiement accéléré.


Le choix de la conteneurisation plutôt que de la vritualisation repose sur plusieurs considérations clés, visant à optimiser l'efficacité ainsi que la gestion de l'infrastructure. Contrairement à la virtualisation, qui encapsule un système d'exploitation entier avec ses ressources, la conteneurisation isole uniquement l'application et ses dépendances, partageant le même noyau d'exploitation avec le système hôte.

De plus, la conteneurisation offre une grande flexibilité, permettant non seulement une utilisation plus efficiente des ressources système, des temps de démarrage plus rapides, mais également la possibilité de créer rapidement de nouveaux conteneurs pour répartir la charge en cas de besoin. Cette capacité dynamique à ajuster la capacité selon les exigences spécifiques de chaque service garantit une réponse agile aux variations de charge et une utilisation optimale des ressources disponibles

## Tunneling VPN
Afin d'assurer une communication sécurisée et fiable entre le siège social et le site de Lyon, a été décidé la mise en place d'une solution de tunneling VPN (Vitrual Private Network). Permettant ainsi une connexion cryptée entre les deux sites, garantissant la confidentialité et l'intégrité des données échangées.

Le choix de cette solution a été motivé par plusieurs facteurs clefs. Tout d'abord, IPsec est reconnu comme un protocole de sécurité robuste, proposant des mécanismes de chiffrement solides et des méthodes d'authentification sécurisées. Permettant ainsi de garantir la confidentialité et l'intégrité des données transitant par le tunnel. De plus, sa large adoption en tant que standard ouvert favorise une interopérabilité étendue entre différents équipements réseau, offrant une flexibilité cruciale lors de l'intégration de nouveaux équipements ou de la mise à niveau de l'infrastructure. La flexibilité des options d'authentification, la gestion avancée des tunnels, et les performances optimisées pour un débit réseau élevé sont autant de caractéristiques qui ont influencé ce choix, assurant une connectivité constante, fiable et performante entre les deux sites.

### Scénarios d'utilisations
La mise en place du tunnel VPN entre le siège social et le site de Lyon vise à répondre à des besoins spécifiques, offrant une connectivité sécurisée et facilitant des scénarios d'utilisation essentiels. Les cas d'usage concrets du tunnel VPN comprennent :

- **Accès aux Services Centralisés:** Les utilisateurs du site de Lyon bénéficient d'un accès sécurisé aux services centralisés, hébergés exclusivement au siège social. Cette approche garantit une utilisation fluide de l'ERP et d'autres applications stratégiques.

- **Supervision à Distance:** Le tunnel VPN permet une supervision à distance du site de Lyon à partir du serveur de supervision localisé au siège social. Cette fonctionnalité assure une gestion proactive de la santé du réseau et des systèmes à Lyon.


### Configuration
- **Protocole VPN :** IPsec
- **Phases de Négociation :** Phase 1 et Phase 2

#### Phase 1 (Négotiation Principale)
- **Algorithme de Chiffrement :** AES-256
- **Méthode de Hachage :** SHA-256
- **Groupe DH (Diffie-Hellman) :** Groupe 14 (2048 bits)
- **Durée de vie :** 28800 secondes
- **DPD (Détection de Chute de Tunnels) :**
    - **Activation :** Oui
    - **Intervalle :** 10 secondes
    - **Essais avant l'échec :** 5 essais


#### Phase 2 (Négotiation Principale)
- **Protocole :** ESP 
- **Algorithme de Chiffrement :** AES-256
- **Méthode de Hachage :** SHA-256
- **Groupe de Clés PSF (Perfect Forward Secrecy) :** Groupe 14 (2048 bits)
- **Durée de Vie :** 3600 secondes
- **Keep Alive :** Activé


#### Authentification
- **Méthode :** Clé partagée
- **Clé partagée :** 0ddda55d3a4af6f8a739a6f3483f9f2a4f8e69cf32aadaf4a3b41049

### Évolutivité et Modifications du Tunnel VPN
Cette section vise à mettre en lumière la capacité du tunnel VPN à évoluer en fonction des besoins changeants de l'entreprise et à intégrer des modifications sans compromettre la stabilité du système.

- **Redondance du Tunnel VPN:** Pour garantir une disponibilité continue des services, le tunnel VPN a été conçu avec une architecture redondante. En cas de défaillance d'un lien ou d'un équipement, un tunnel de secours (backup) entre le siège social et le site de Lyon s'active automatiquement. Cette redondance assure une connectivité ininterrompue, minimisant les temps d'indisponibilité potentiels.

- **Adaptabilité aux Évolutions:** L'architecture du tunnel VPN a été pensée pour s'adapter aux évolutions futures du système d'information. Les paramètres de configuration, tels que les algorithmes de chiffrement, les méthodes d'authentification, et les capacités de détection de chute de tunnel, peuvent être ajustés en fonction des meilleures pratiques de sécurité et des besoins opérationnels à venir.
