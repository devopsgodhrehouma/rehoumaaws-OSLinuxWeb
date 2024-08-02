## Étudiant AWS Academy (Construire une Application Web Hautement Disponible et Extensible)

### Contexte du Projet

Ce projet nécessite une compréhension des services AWS essentiels, tels que les services de calcul, de stockage, de réseau et de base de données. Il exige également des connaissances sur les meilleures pratiques architecturales, telles que la haute disponibilité, la scalabilité et la sécurité. Les étudiants devraient avoir complété le cours AWS Academy Cloud Architecting pour acquérir ces connaissances nécessaires. Les étudiants ayant complété le cours AWS Academy Cloud Foundations et inscrits au cours AWS Academy Cloud Architecting peuvent également tenter de réaliser ce projet avec l'aide des supports de cours, des laboratoires des cours et des conseils des éducateurs. La connaissance de tout langage de programmation, tel que Python ou JavaScript, est un avantage mais n'est pas obligatoire.

### Scénario

Votre scénario consiste à planifier, concevoir, construire et déployer l'application web sur le cloud AWS de manière cohérente avec les meilleures pratiques du cadre AWS Well-Architected Framework. Pendant la période de pointe des admissions, l'application doit supporter des milliers d'utilisateurs et être hautement disponible, extensible, équilibrée en charge, sécurisée et performante.

### Objectifs

- Créer un schéma architectural pour représenter les divers services AWS et leurs interactions.
- Estimer le coût des services en utilisant l'AWS Pricing Calculator.
- Déployer une application web fonctionnelle fonctionnant sur une seule machine virtuelle et soutenue par une base de données relationnelle.
- Architecturer une application web pour séparer les couches de l'application, telles que le serveur web et la base de données.
- Créer un réseau virtuel configuré de manière appropriée pour héberger une application web accessible publiquement et sécurisée.
- Déployer une application web avec la charge répartie sur plusieurs serveurs web.
- Configurer les paramètres de sécurité réseau appropriés pour les serveurs web et la base de données.
- Mettre en œuvre la haute disponibilité et l'extensibilité dans la solution déployée.
- Configurer les permissions d'accès entre les services AWS.

### Exigences Fonctionnelles

- **Fonctionnalité**: La solution répond aux exigences fonctionnelles, telles que la capacité à visualiser, ajouter, supprimer ou modifier les dossiers des étudiants, sans délai perceptible.
- **Équilibrée en charge**: La solution peut correctement équilibrer le trafic utilisateur pour éviter les ressources surchargées ou sous-utilisées.
- **Extensible**: La solution est conçue pour s'adapter aux demandes placées sur l'application.
- **Hautement disponible**: La solution est conçue pour avoir un temps d'arrêt limité lorsqu'un serveur web devient indisponible.
- **Sécurisée**: La base de données est sécurisée et ne peut pas être accessible directement depuis les réseaux publics.
- **Optimisée en coût**: La solution est conçue pour maintenir les coûts bas.
- **Performante**: Les opérations courantes (visualisation, ajout, suppression ou modification de dossiers) sont effectuées sans délai perceptible sous des charges normales, variables et de pointe.

### Hypothèses

- L'application est déployée dans une seule région AWS (la solution n'a pas besoin d'être multi-régionale).
- Le site web n'a pas besoin d'être disponible sur HTTPS ou un domaine personnalisé (nous n'utiliserons pas Amazon CloudFront, Route 53).
- La solution est déployée sur des machines Ubuntu en utilisant le code JavaScript fourni.
- Utilisez le code JavaScript tel quel, sauf si les instructions vous demandent spécifiquement de modifier le code.
- La solution utilise des services et des fonctionnalités dans les restrictions de l'environnement de laboratoire.
- La base de données est hébergée dans une seule zone de disponibilité.
- Le site web est accessible publiquement sans authentification.
- L'estimation des coûts est approximative.

### Planification de la Conception et Estimation des Coûts

- **Planification de la conception**: Utilisez plusieurs outils pour créer la conception de l'architecture. L'un des outils recommandés est Lucidchart. Téléchargez les icônes d'architecture officielles AWS et consultez les schémas d'architecture de référence AWS.
- **Estimation des coûts**: Utilisez l'AWS Pricing Calculator pour estimer le coût des services AWS utilisés. Vérifiez également les coûts des ressources AWS spécifiques, par exemple les prix d'Amazon Route 53, pour vous assurer de l'exactitude des coûts.

### Création du VPC

1. **Créer un VPC**: Un Cloud Privé Virtuel (VPC) est un réseau virtuel sur le cloud qui vous permet de connecter et de gérer de manière sécurisée les ressources au sein de votre environnement cloud. Il offre une isolation et un contrôle sur votre infrastructure réseau.
   - **Nom**: Définissez un nom pour votre VPC.
   - **IPv4 CIDR**: Entrez 10.0.0.0/16.
   - **DNS**: Activez les noms d'hôtes DNS.
   - **Créer les sous-réseaux**: Créez des sous-réseaux publics et privés dans différentes zones de disponibilité.

2. **Créer une Passerelle Internet**:
   - **Nom**: Définissez un nom pour votre passerelle Internet.
   - **Attacher au VPC**: Attachez la passerelle Internet au VPC créé.

3. **Créer des Tables de Routage**:
   - **Nom**: Définissez un nom pour votre table de routage public.
   - **Route**: Ajoutez une route avec la destination 0.0.0.0/0 pointant vers la passerelle Internet.

4. **Associer des Sous-réseaux**:
   - **Public**: Associez les sous-réseaux publics à la table de routage public.
   - **Privé**: Créez une table de routage privée et associez-la aux sous-réseaux privés.

### Création d'une Instance EC2 pour l'Application Web

1. **Lancer une Instance**:
   - **AMI**: Choisissez Ubuntu.
   - **Type d'Instance**: Sélectionnez t2.micro.
   - **VPC et Sous-réseau**: Choisissez le VPC et le sous-réseau public créés.
   - **Auto-assigner IPv4 Publique**: Activez l'auto-assignation IPv4 publique.
   - **Groupe de Sécurité**: Créez un groupe de sécurité pour autoriser le trafic HTTP et SSH.

2. **Configurer les Détails de l'Instance**:
   - **Script de Données Utilisateur**: Utilisez un script pour installer Node.js, MySQL, et déployer l'application web.

3. **Vérifier l'Instance**:
   - Assurez-vous que l'instance est en cours d'exécution et que les vérifications d'état sont réussies.

### Création et Configuration d'Amazon RDS

1. **Créer une Base de Données RDS**:
   - **Type de Moteur**: Sélectionnez MySQL.
   - **Options de Création**: Choisissez l'option Free Tier.
   - **Nom de l'Instance**: Définissez un nom unique pour l'instance RDS.
   - **Authentification**: Utilisez la gestion des secrets AWS ou définissez un mot de passe maître.

2. **Configurer la Connectivité**:
   - Assurez-vous que la RDS et l'EC2 sont dans le même VPC et configurez les règles de sécurité pour autoriser le trafic entre eux.

### Migration de la Base de Données

1. **Créer un Secret Manager**:
   - Créez un secret dans AWS Secrets Manager pour stocker les informations d'identification de la base de données.

2. **Migrer les Données**:
   - Utilisez AWS Cloud9 pour exécuter des commandes `mysqldump` et migrer les données de l'EC2 vers la RDS.

### Mise en Œuvre d'un Équilibreur de Charge (ALB)

1. **Créer un Groupe Cible**:
   - Définissez un groupe cible pour les instances EC2.

2. **Créer un ALB**:
   - Configurez l'ALB pour diriger le trafic vers le groupe cible.

### Mise en Œuvre d'un Groupe Auto Scaling (ASG)

1. **Créer une AMI**:
   - Créez une image AMI de l'instance EC2.

2. **Configurer le Groupe Auto Scaling**:
   - Utilisez le modèle de lancement créé et configurez les politiques de mise à l'échelle automatique.

### Conclusion

Créer un groupe Auto Scaling dans AWS permet de gérer automatiquement le nombre d'instances en fonction de la demande. En suivant les étapes décrites dans ce guide, vous pouvez facilement créer un groupe Auto Scaling et garantir que votre application peut gérer efficacement les charges de travail variables.
