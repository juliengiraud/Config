# Utiliser plusieurs dépôts git en ssh

1. Pour que ça marche il faut bien sûr créer les clés SSH

    ```sh
    # Création de clé
    ssh-keygen -t rsa -b 4096 -C "mon_adresse@example.com"

    # Ajout de la clé au SSH agent
    ssh-add adresse_dossier_ssh/nom_de_la_clé
    ```

2. Il faut ensuite ajouter un fichier `config` dans le dossier `.ssh` pour configurer quelle clé publique utiliser selon le dépôt. Pour ça on associe les clés ssh à des identifiants distincts

    ```sh
    #### VERSION LINUX ####
    #### ~/.ssh/config ####

    # Compte par défaut
    Host github.com
    HostName github.com
    User git
    AddKeysToAgent yes
    # Clé à utiliser par défaut
    IdentityFile ~/.ssh/id_rsa

    # Compte spécial 1
    # Ajout d'un 1er identifiant, ici "juliengiraud"
    Host github.com-juliengiraud
    HostName github.com
    User git
    AddKeysToAgent yes
    # Clé à utiliser pour les dépôts qui possèdent cet identifiant
    IdentityFile ~/.ssh/id_rsa_pro
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

3. Puis il faut s'assurer qu'il n'y a pas de problème de droit avec les fichiers

    ```sh
    chmod 600 adresse_dossier_ssh/*
    ```

4. Il faut enfin ajouter les identifiants aux différent projets (sauf ceux de la clé par défaut). Pour ça il faut modifier l'adresse du dépôt en y ajoutant l'identifiant

    ```sh
    #### VERSION LINUX ####
    # Si on clone le projet
    git clone git@github.com-identifiant:username/depot.git

    # Si le projet est déjà en local
    git remote remove origin
    git remote add origin git@github.com-identifiant:username/depot.git
    ```
