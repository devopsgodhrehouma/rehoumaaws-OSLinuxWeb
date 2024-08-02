
```plaintext
                                  Internet
                                     |
                                     |
                             +-------+-------+
                             | Application   |
                             | Load Balancer |
                             +-------+-------+
                                     |
                                     |
                              +------+-------+
                              |              |
                              |              |
                      +-------+-------+ +----+-------+
                      |   EC2 Instance  | |  EC2 Instance |
                      |    (Public)     | |   (Public)    |
                      +-------+-------+ +----+-------+
                              |              |
                              |              |
                 +------------+-------------+
                 |         Public Subnet         |
                 +-------------------------------+
                              |
                              |
              +---------------+---------------+
              |               VPC             |
              +---------------+---------------+
                              |
                              |
                 +------------+-------------+
                 |         Private Subnet        |
                 +-------------------------------+
                              |
                              |
                      +-------+-------+
                      |    RDS        |
                      | (Database)    |
                      +---------------+
```

### Explication du Schéma

1. **Internet**: Le point d'entrée pour les utilisateurs accédant à l'application web.
2. **Application Load Balancer (ALB)**: Distribue le trafic entrant vers les instances EC2 dans les sous-réseaux publics.
3. **Instances EC2**: Hébergent l'application web. Elles sont situées dans des sous-réseaux publics pour être accessibles via Internet.
4. **Public Subnet**: Sous-réseau où les instances EC2 sont déployées.
5. **VPC (Virtual Private Cloud)**: Conteneur réseau qui regroupe les ressources AWS.
6. **Private Subnet**: Sous-réseau où la base de données RDS est déployée. Il n'est pas accessible directement depuis Internet pour des raisons de sécurité.
7. **RDS (Relational Database Service)**: Base de données MySQL hébergée dans un sous-réseau privé pour stocker les données de l'application.

### Points Importants

- Le **Load Balancer** distribue le trafic de manière uniforme entre les instances EC2 pour assurer la haute disponibilité.
- Les instances **EC2** dans le sous-réseau public sont configurées pour être accessibles publiquement et communiquer avec la base de données RDS.
- La base de données **RDS** dans le sous-réseau privé est protégée contre les accès non autorisés depuis Internet.
- La **scalabilité** est assurée par le groupe Auto Scaling (ASG) qui ajuste automatiquement le nombre d'instances EC2 en fonction de la charge de travail.

Ce schéma simple en ASCII offre une vue d'ensemble de l'architecture d'une application web sur AWS avec une configuration de haute disponibilité et de scalabilité.
