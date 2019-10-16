# Utiliser plusieurs dépôts git en ssh

1. Il faut ajouter un fichier `config` dans le dossier `~/.ssh/` pour configurer quelle clé publique utiliser selon le  dépôt. Pour ça on associe les clés ssh à des identifiants distincts

    ```sh
    #### VERSION LINUX ####
    #### ~/.ssh/config ####

    # Compte par défaut
    Host github.com
    HostName github.com
    User git
    AddKeysToAgent yes
    IdentityFile ~/.ssh/id_rsa # Clé à utiliser par défaut

    # Compte spécial 1
    Host github.com-juliengiraud # Ajout d'un 1er identifiant, ici "juliengiraud"
    HostName github.com
    User git
    AddKeysToAgent yes
    IdentityFile ~/.ssh/id_rsa_pro # Clé à utiliser pour les dépôts qui possèdent cet identifiant
    ```

    ```sh
    #### VERSION WINDOWS ####
    #### /c/Users/USERNAME/.ssh/config ####
    # Compte par défaut
    Host github.com
    HostName github.com
    User git
    AddKeysToAgent yes
    # Clé à utiliser par défaut
    IdentityFile /c/Users/USERNAME/.ssh/id_rsa

    # Compte spécial 1
    # Ajout d'un 1er identifiant, ici "juliengiraud"
    Host github.com-juliengiraud
    HostName github.com
    User git
    AddKeysToAgent yes
    # Clé à utiliser pour les dépôts qui possèdent cet identifiant
    IdentityFile /c/Users/USERNAME/.ssh/id_rsa_pro
    ```

2. Il faut ajouter les identifiants aux différent projets (sauf ceux de la clé par défaut). Pour ça il faut modifier l'adresse du dépôt en y ajoutant l'identifiant

    ```sh
    #### VERSION LINUX ####
    # Si on clone le projet
    git clone git@github.com-identifiant:username/depot.git

    # Si le projet est déjà en local
    git remote remove origin
    git remote add origin git@github.com-identifiant:username/depot.git
    ```
