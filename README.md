# CAUE-WATCHER

## Description

**CAUE-WATCHER** est une application Java développée pour automatiser le tri et l’archivage des projets traités par le CAUE17. Elle fonctionne en complément de `CauePilote`, un logiciel interne générant les fichiers PDF de présentation des projets.

L’application surveille un dossier défini, détecte les nouveaux fichiers PDF, vérifie leur nom, et les classe automatiquement dans une arborescence organisée par année, type de projet et nom du projet.

Elle permet également de rejeter les fichiers non conformes dans un dossier séparé, et crée automatiquement des sous-dossiers types (Photos, Plans, etc.) pour chaque projet.

## Pré-requis

Assurez-vous que l'ordinateur sur lequel vous voulez installer l'application dispose de :
1.  **Git**
2.  **Java** (JDK version 21 ou supérieure)

> **Vérifier votre version de Java**
> Pour vérifier que Java est bien installé et connaître sa version, ouvrez une invite de commandes et tapez :
> ```bash
> java -version
> ```

## Installation

#### 1. Cloner le dépôt public

```bash
cd <répertoire_d'installation_de_l'application>
git clone https://forge.iut-larochelle.fr/wmaillar/CAUE-WATCHER-RELEASES.git
```
> Ce dépôt est public : aucun compte GitLab n’est requis pour y accéder.

#### 2. Modifier le fichier de configuration

Le fichier `Watcher.properties` contient les chemins des dossiers utilisés par l'application, ainsi que l'intervalle entre chaque sondage.

> **Important ! :**
> - Vous devez fournir des **chemins absolus** (complets), pas des chemins relatifs.
> - L'intervalle est en seconde.
> - Le fichier est lu **uniquement au démarrage**. Si vous le modifiez, redémarrez l’application pour appliquer les changements.

**Exemple de configuration sur Windows :**
```properties
# Chemins pour l'application CAUE-WATCHER
watcher.dossierReception=C:/Users/Utilisateur/Documents/CAUE/DOSSIER CIBLE
watcher.dossierRejet=C:/Users/Utilisateur/Documents/CAUE/FICHIERS NON TRAITABLES
watcher.dossierConseils=C:/Users/Utilisateur/Documents/CAUE/CONSEILS
```

#### 3. Lancer l’application

```bash
<chemin_vers_java>/jdk-<version>/bin/java.exe -jar <chemin_vers_l_application>/caue-watcher-<version>.jar
```

**Exemple de lancement :**
```bash
C:\Program Files\Java\jdk-21\bin\java.exe -jar C:\Documents\CAUE-WATCHER-RELEASES\caue-watcher-0.1.jar
```

>**Notes :** Pour Windows, n'hésitez pas à créé une tâche dans le planificateur de tâche afin d'automatiser le lancement de l'application sur votre système.

## Mise à jour

Pour bénéficier des dernières améliorations, il est recommandé de mettre à jour l'application lorsque de nouvelles versions sont disponibles.

#### 1. Arrêter l'application
Avant toute chose, fermez l'application en cours d'exécution, fermez la fenêtre du terminal ou mettez fin à la tâche dans le planificateur de tâche.

#### 2. Sauvegarder votre configuration
Par précaution, faites une copie de votre fichier `Watcher.properties` et placez-la en dehors du dossier de l'application (sur le Bureau, par exemple), si vous ne voulez pas perdre votre configuration.

#### 3. Télécharger la nouvelle version
Ouvrez git cmd et déplacez-vous dans le répertoire de l'application puis récupérez la nouvelle version :
```bash
cd C:\<chemin_vers_le_répertoire>\CAUE-WATCHER-RELEASES
git fetch
git reset --hard origin/main
```
Cette commande récupère tous les nouveaux fichiers, y compris la dernière version du fichier `.jar`.

#### 4. Restaurer votre configuration
Après la mise à jour, votre fichier `Watcher.properties` à une configuration par défaut. **Remplacez son contenu** par celui que vous aviez sauvegardé à l'étape 2, en veillant à ne pas supprimer les nouveaux paramètres s'il y en a.

#### 5. Relancer l'application
Lancez l'application en utilisant la même commande que pour l'installation, en adaptant le numéro de version si nécessaire, ou en relançant manuellement la tâche.

**Exemple, si la nouvelle version est la `0.2` :**
```bash
C:\Program Files\Java\jdk-21\bin\java.exe -jar C:\Documents\CAUE-WATCHER-RELEASES\caue-watcher-0.2.jar
```

## Fonctionnalités

- **Surveillance continue** du dossier de réception.
- **Filtrage des fichiers PDF valides** (via leur extension et type MIME).
- **Classement** dans une structure `année / type / projet`.
- **Création automatique de sous-dossiers** dans chaque projet (Photos, Plans, etc.).
- **Rejet des fichiers non valides** avec logs explicatifs.
- **Journalisation des événements** (fichier `.log` mensuel dans le dossier `JOURNAL ACTIVITÉ APPLI`).

## Dépannage

- Si l’application ne démarre pas, vérifiez :
  - La **version de Java** utilisée (`java -version`).
  - Les **droits d'accès** en lecture/écriture aux dossiers définis dans la configuration.
  - Que le fichier `.properties` est correctement formaté et placé **à côté du fichier `.jar`**.

- Les logs sont consultables dans le fichier généré dans le dossier `JOURNAL ACTIVITÉ APPLI`.
  > **Exemple de nom de fichier :** `journal-activité-projets-CAUE-2025-06.log`

## Auteur

- **Développé par :** Wilson Maillard (humble stagiaire) pour le CAUE17.
- **Encadré par :** M. Daniel François (CAUE17) et Mme Céline Marteau (IUT La Rochelle).