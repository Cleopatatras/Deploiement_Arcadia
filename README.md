# Projet Docker Symfony

Ce projet est une application Symfony intégrée dans un conteneur Docker. Il inclut tout ce qui est nécessaire pour lancer et exécuter l'application, sauf la base de données, qui doit être configurée séparément.

Prérequis

Docker et Docker Compose doivent être installés sur votre système.

Une base de données compatible avec Doctrine (comme MySQL ou PostgreSQL).

## Installation

- Clonez ce dépôt :

git clone <https://github.com/Cleopatatras/deploiement_arcadia.git>


- Copiez le fichier .env de base et personnalisez-le :

`cp .env.dist .env`

- Modifiez les paramètres de connexion à la base de données dans le fichier .env :

```DATABASE_URL="mysql://user:password@host:port/db_name"```

- Construisez et démarrez les conteneurs Docker :

`docker-compose up --build -d`

si besoin, installez les dépendances de l'application :

docker-compose exec app composer install

- Effectuez les migrations de la base de données :

`docker-compose exec app php bin/console doctrine:migrations:migrate`

## Mise à jour des tables

Le script pour le remplissage des tables est en annexe.

### Configuration de l'administrateur

Accédez à l'application et créez un utilisateur via l'URL :

http://<votre-domaine>/register

Une fois l'utilisateur créé, modifiez son rôle directement dans la base de données pour qu'il devienne administrateur. Par exemple, pour une base de données MySQL :

`UPDATE user SET roles='["ROLE_ADMIN"]' WHERE email='adresse_email_de_l_utilisateur';`

## Commandes utiles

Arrêter les conteneurs Docker :

docker-compose down

Voir les logs de l'application :

docker-compose logs -f

Accéder au conteneur de l'application :

docker-compose exec app bash

## Notes importantes

Assurez-vous que la base de données est configurée avant de lancer l'application.

La connexion à la base de données doit être opérationnelle pour que l'application fonctionne correctement.

Contribuer

Les contributions sont les bienvenues ! Créez une pull request pour proposer vos modifications.
## Annexe : création des données:
```INSERT INTO
    `habitats` (
        `id`,
        `nom`,
        `description`,
        `image`
    )
VALUES (
        3,
        'Savane',
        'La savane est un écosystème de prairies tropicales ou subtropicales caractérisé par une végétation herbeuse clairsemée et des arbres ou arbustes isolés. Elle se situe généralement dans des régions aux saisons sèches marquées, ce qui influence la croissance des plantes.\r\nVégétation: L\'herbe est dominante, avec des arbres comme les acacias et les baobabs qui se sont adaptés à ces conditions sèches (racines profondes, épines pour limiter la transpiration).\r\nFaune: La savane abrite une grande diversité d\'animaux, notamment des herbivores comme les zèbres, les gnous et les antilopes, ainsi que leurs prédateurs comme les lions, les léopards et les hyènes.\r\nClimat: Le climat est tropical, avec une saison des pluies et une saison sèche.',
        'f9b3f4eb4e017966a4bb95d118b66897.webp'
    ),
    (
        4,
        'Jungle',
        'La jungle est un écosystème forestier dense et humide, caractérisé par une végétation luxuriante et une biodiversité exceptionnelle. On la trouve généralement dans les régions tropicales.\r\nVégétation: La végétation est très dense, avec une canopée formée par les arbres les plus hauts, et un sous-bois dense où poussent des lianes, des fougères et d\'autres plantes.\r\nFaune: La jungle abrite une multitude d\'espèces animales, des insectes aux grands mammifères comme les singes, les éléphants et les félins.\r\nClimat: Le climat est tropical, chaud et humide toute l\'année.',
        '29344c806398062b8c11b274f9b299a5.webp'
    ),
    (
        5,
        'Marais',
        'Les marais sont des zones humides caractérisées par une végétation adaptée aux sols gorgés d\'eau. On les trouve dans différentes régions du monde.\r\nVégétation: La végétation est principalement composée de plantes aquatiques comme les roseaux, les joncs et les nénuphars.\r\nFaune: Les marais abritent une faune spécifique, comme les oiseaux d\'eau (hérons, canards), les amphibiens (grenouilles, tritons) et les poissons.\r\nClimat: Le climat peut varier selon la région, mais les marais sont généralement situés dans des zones humides.',
        '85d4bdce6ec9a9fbf950d879b1c7fdbd.webp'
    );```

    INSERT INTO
    `animaux` (
        `id`,
        `habitat_id`,
        `nom`,
        `race`,
        `image`,
        `views`
    )
VALUES (
        1,
        4,
        'Zorro',
        'Anaconda',
        '3820e33ebe7554aaf04f358d8c4fbaf8.webp',
        1
    ),
    (
        2,
        4,
        'Coco',
        'Ara',
        'd17313ccb386e804ae99f0213aa1069e.webp',
        0
    ),
    (
        3,
        4,
        'Mongo',
        'Gorille',
        'd4e7be7dabbab467a63648ecfc05e1cb.webp',
        2
    ),
    (
        4,
        4,
        'Indri',
        'Lémurien',
        'b299303aa0fcf2cba08bd2af9a40bbc1.webp',
        2
    ),
    (
        5,
        5,
        'Junior',
        'Castor',
        '45372ccf815a1255b75f2caee8a69fb6.webp',
        2
    ),
    (
        6,
        5,
        'Gator',
        'Crocodile',
        '04327a5f10b91b296dcf67482b65105c.webp',
        2
    ),
    (
        7,
        5,
        'Patapon',
        'Héron',
        '5fc231119e5e635c7d1904ec55dda2a2.webp',
        2
    ),
    (
        8,
        5,
        'Thot',
        'Ibis',
        '3d0fcf08af574d46a73b1c6ed5573c51.webp',
        1
    ),
    (
        9,
        3,
        'Marguerite',
        'girafe',
        '7fdbb5beaf8079290cfa3c88f1f0ea5b.webp',
        2
    ),
    (
        10,
        3,
        'Léo',
        'Lion',
        'a46921c569ab9aa1f459a742a225cf5b.webp',
        3
    ),
    (
        11,
        3,
        'Clown',
        'Zèbre',
        '8ca78bcaada54c1adcf318fa1b4984b9.webp',
        1
    ),
    (
        12,
        3,
        'Nonos',
        'Rhinocéros',
        '5b6d0749944d9e14d2871032d2b8b293.webp',
        1
    );

    INSERT INTO
    `nourriture` (
        `id`,
        `nom`,
        `description`,
        `image`
    )
VALUES (
        1,
        'Patée',
        'Nourriture pour les mamouths',
        'd05aaabc895278178958e7a1736f0d9e.webp'
    ),
    (
        2,
        'Céréales',
        'nourriture pour herbivores',
        'fe66280cbf6edb3f52e5425f87eae0c8.webp'
    ),
    (
        3,
        'Viande',
        'Nourriture pour les fauves',
        '6aa8edad36ce6031b62846992140136d.webp'
    ),
    (
        4,
        'Feuillage',
        'Feuilles fraiches du maraicher',
        '30d93e9eb09b767b88367d6205b86b3f.webp'
    );

INSERT INTO
    `services` (
        `id`,
        `nom`,
        `description`,
        `image`
    )
VALUES (
        2,
        'Visite en petit train',
        'Dès votre arrivée, profitez de la visite complète et écologique avec notre petit train !\r\nCelui-ci fonctionne grâce à l\'électricité produite par nos panneaux solaires !!\r\nNous vous attendons nombreux !!',
        '4ca527fc1aa6f5d08f6d15545b7255c0.webp'
    ),
    (
        4,
        'Restauration',
        'Notre restaurant snacking vous accueille toute la journée !\r\nRepas chauds ou froids\r\nBoissons et glaces !',
        'a22eb17ee25d1fdb96e8271a1960f3ac.webp'
    ),
    (
        5,
        'Visites guidées',
        'Pendant les vacances scolaires, un guide est à votre disposition !\r\nIl vous expliquera nos animaux, leurs soins et leurs environnement.\r\nHors période scolaire, nous contacter',
        'afd95ce182c0fe02da7df088dc83f2bb.webp'
    );

    INSERT INTO
    `compte_rendu` (
        `id`,
        `animal_id`,
        `user_id`,
        `nourriture_id`,
        `date`,
        `etat_animal`,
        `grammage`,
        `detail`
    )
VALUES (
        1,
        2,
        2,
        2,
        '2024-10-25',
        'correct',
        100,
        'RAS'
    ),
    (
        2,
        2,
        2,
        2,
        '2024-11-04',
        'mort',
        100,
        'ras'
    ),
    (
        3,
        12,
        2,
        3,
        '2024-11-08',
        'il est en pleine santé',
        1000,
        'il faut lui rajouter de l\'herbe dans son alimentation'
    ),
    (
        4,
        9,
        3,
        2,
        '2024-11-20',
        'Elle a l\'air plutôt bien.\nS\'accomode à son nouvel environnement',
        500,
        'Il lui faudrait plus de branchages'
    ),
    (
        5,
        12,
        3,
        2,
        '2024-11-24',
        'Il est en pleine forme',
        1000,
        'Mange correctement'
    );