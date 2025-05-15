![alt text](img/image-66.png)
# Atelier 2 : Compromission de credentials
---

## Exercice 1 - Compromettre un compte d’administrateur local
### Tâche 1 - Pulvériser le mot de passe du compte administrateur de SRV01

> ![alt text](img/image-24.png)

.\hydra.exe -V -F -L .\users.lst -P .\passwords.lst SRV01 rdp
> ![alt text](img/image-25.png)


Testons-le maintenant et ouvrons une fenêtre Explorateur de fichiers. Dans la barre d’adresse, tapez \\SRV01\C$ et appuyez sur Entrée. Une fenêtre contextuelle d’authentification devrait s’afficher. Utilisez les informations d’identification fraîchement devinées :

> ![alt text](img/image-27.png)


### Tâche 2 - Vérification des traces laissées sur SRV0

> Filtre 4625 (echec) :
> ![alt text](img/image-28.png)
> Ici type 3, donc une connexion réseau.


> Filtre 4624 (succes) :
> ![alt text](img/image-29.png)

auditpol /get /subcategory:Logon
#### 📝 Quelle est la commande pour répertorier toutes les catégories d’audit ?
> auditpol /get /category:*

---

## Exercice 2 - Sécurisation du compte d’administrateur local
### Tâche 1 - Stratégie de mot de passe pour les serveurs membres

![alt text](img/image-30.png)

Dans la fenêtre Local Computer Policy Editor, accédez à Local Computer Policy > Computer Configuration > Windows Settings > Security Settings > Account Policies > Password Policies.

#### Pouvez-vous modifier l’un des paramètres ?
![alt text](img/image-31.png)
> On ne peux pas modifier la majorité des paramètres, sauf "Relax Minimum password lenght limits" et "Relax minimum password length limits".


![alt text](img/image-32.png)

![alt text](img/image-33.png)

### Tâche 2 - Restreindre l’utilisation du compte d’administrateur local

![alt text](img/image-34.png)


### Tâche 3 - Vérifier la restriction de connexion de l’administrateur local
> Le mot de passe n'est plus valide
> ![alt text](img/image-35.png)

> ![alt text](img/image-36.png)


### Tâche 4 - Vérifier le journal de sécurité sur SRV01
> ![alt text](img/image-37.png)

#### 📝 Quel est le code d’état dans la section des informations de défaillance de l’événement ?
> Status: 0xC000015B


---
## Exercice 3 - Attaquer les mots de passe des comptes de domaine

### Tâche 1 - Pulvériser des comptes de domaine par mot de passe via SRV01

#### 📝 Combien y a-t-il de mots de passe dans cette liste ?
> Il y a 11 mots de passe dans la liste.



#### Exécutez Hydra en exécutant .\hydra.exe -V -F -L .\domainusers.lst -P .\passwords.lst SRV01 rdp CONTOSO. Notez les résultats.
> ![alt text](img/image-38.png)

