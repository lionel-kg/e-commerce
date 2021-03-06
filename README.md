# Projet S4

## Comment participer au projet ?

1. Git clone

        $ git clone https://iut-info.univ-reims.fr/gitlab/verd0012/e-commerce.git

2. Démarrer le serveur

        $ composer start

3. Installer les dépendances si besoin

        $ composer install

4. Créer la BD
    - Dupliquer le fichier .env et le renommer en .env.local
    - Modifier la ligne commençant par DATABASE_URL 
      ( pour l'iut "DATABASE_URL=mysql://infs4_prj08:Azerty01@mysql:3306/infs4_prj08")
    - Modifier la ligne commençant par MAILER_URL par MAILER_URL=gmail://monsuperprojetiut@gmail.com:azerty-51@localhost
    - Créer la BD avec la commande
        
            $ bin/console doctrine:schema:create
    
    - Générer les données avec la commande

            $ bin/console doctrine:fixtures:load

## Le projet

### L'inscription

Lorsqu'un utilisateur s'inscrit, un email contenant un lien de confirmation lui est envoyé afin de confirmer son email.

Le lien contient un token et l'email du client afin de permettre de passez son compte sur "actif".

Le token a une durée de validité de 24H.

### L'authentification

La connection se fait par le biais de l'email du client.

Le compte admin a pour adresse mail "admin@gmail.com", pour les autres vous devez vous réferencer à votre bd.

Le mot de passe par default pour tout les comptes est "azerty"

L'accès au compte du client connecté se fait par le biais de la route :

        http://127.0.0.1:8000/compte

Ses commandes sont accessible depuis :

        http://127.0.0.1:8000/compte/commandes

L'administration est accessible depuis :

        http://127.0.0.1:8000/admin

### Mot de passe oublié

Sur la page d'authentification, un lien permet a l'utilisateur de se faire envoyer un mail de changement de mot de passe à partir de son adresse email.

Le lien contient un token valide pendant 1H et lui permet d'acceder à un formulaire de modification de mot de passe.

### Les criteres de tri

Les articles peuvent être triés a l'aide de plusieurs filtres :

        http://127.0.0.1:8000/article?libelle=jupe&sections[]=homme&sections[]=femme&critere_tri=prix_u&tri_ordre=DESC&tailles[]=L&types[]=jupe&categories[]=vetement&categories[]=Accessoire&prix_entre=20_30&description=pull

### Pagination

La liste des articles est paginé.

Elle a comme valeur par default la page 1 et 20 articles par page.

La page et le nombre d'articles par page peuvent etre passé en parametre

        http://127.0.0.1:8000/article?page=1&nb_max_par_page=30

Les parametres actuels sont retournes au template en string depuis l'attribut "pagination.params" il sufit d'y donc d'y ajouter le parametre de la page demmandé.

La numero de la page et de la derniere page sont accessible depuis les attributs "pagination.page" et "pagination.nbPages".

### Le panier

Le panier est accessible depuis :

        http://127.0.0.1:8000/panier

Le panier est stocké dans les données de session.

Lorque l'utilisateur est en ligne, don panier est aussi stocké dans la bdd afin qu'il retrouve son panier a sa prochaine connection depuis nimporte quelle appareil.

Lorque l'utilisateur a ajouté des articles a son panier avant de se connecter et qu'il y a deja des articles stockes dans la bdd le panier se verra automatiquement ajouter les articles en bdd.

Il est accessible partout depuis le service App\Service\Panier\PanierService

Il est possible d'ajouter/supprimer un article :

        http://127.0.0.1:8000/panier/add/{id}?taille={idTaille}

        http://127.0.0.1:8000/panier/add/{id}?taille={idTaille}&quantite={quantite}

        http://127.0.0.1:8000/panier/remove/{id}?taille={idTaille}


### Emails

Un email est envoyé au client afin de le prévenir de la confirmation de sa commande.

Pour ne pas envoyer d'email sur des compte généré aléatoirement par les fixtures, l'email est redirigé sur le compte Gmail du projet.

L'acces à ce compte Gmail se fait via les identifiants suivant:
- login: monsuperprojetiut@gmail.com
- mdp: azerty-51

### Idées


### A faire

[Voir les Issues](https://iut-info.univ-reims.fr/gitlab/verd0012/e-commerce/issues)
