# StarUML-5.x.x

# Obtenir la version complète de StarUML


1. Vérifiez que Node.js est déjà installé sur votre ordinateur. Si ce n'est pas le cas, veuillez le [télécharger](https://nodejs.org/fr/download/) depuis la page officielle.

2. Ensuite, accédez au répertoire d'installation de StarUML. Habituellement, il se trouve dans `C:\Program Files`.

3. Allez dans le dossier `StarUML\resources`, puis copiez le chemin d'accès de ce répertoire à partir de la barre d'adresse.

4. Ouvrez l'invite de commandes en tant qu'administrateur.

5. Ensuite, accédez à ce répertoire en tapant la commande suivante dans l'invite de commandes :

```
cd C:\Program Files\StarUML\resources
```

Veuillez noter que vous devez remplacer les guillemets simples (`'`) par des guillemets doubles (`"`) dans le chemin d'accès si vous l'avez copié depuis la barre d'adresse.

![image](https://github.com/Algorithme123/StarUML-5.x.x/assets/101357738/c59c22fb-48d5-4e43-9ec3-7253d225d2e1)


## Ensuite, installez Asar en utilisant la commande suivante :


```
npm install -g asar 
```

Veuillez patienter jusqu'à ce que l'opération soit terminée.

6. Une fois terminée, extrayez le fichier asar en utilisant la commande suivante :

```
asar extract app.asar app
```

7. Accédez au répertoire ``` app\src\engine ```.

Ouvrez le fichier license-manager.js et recherchez le texte ``` checkLicenseValidity ``` .

Copiez le code ci-dessous et collez-le dans les lignes 131 à 142 du fichier :

```
checkLicenseValidity () {
    if (packageJSON.config.setappBuild) {
      setStatus(this, true)
    } else {
      this.validate().then(() => {
        setStatus(this, true)
      }, () => {
        setStatus(this, true)
        // UnregisteredDialog.showDialog()
      })
    }
  }
```

Assurez-vous de bien sauvegarder les modifications apportées au fichier.


8. Une fois que vous avez contourné la licence, nous allons désactiver la mise à jour automatique de la version.

Ouvrez le fichier `update-manager.js` et recherchez le texte ```handleMessages() {```.

Copiez le code ci-dessous et collez-le dans les lignes 34 à 58 du fichier :

```

handleMessages () {
    ipcRenderer.on('autoUpdater:update-available', (event, info) => {
      //this.state = 'available'
      //this.updateInfo = info
      //this.emit('update-available', info)
    })
    ipcRenderer.on('autoUpdater:update-not-available', (event, info) => {
      this.state = 'no-update'
      this.updateInfo = info
      this.emit('update-not-available', info)
    })
    ipcRenderer.on('autoUpdater:download-progress', (event, progress) => {
      //this.state = 'downloading'
      //this.progress = progress
      //this.emit('download-progress', progress)
    })
    ipcRenderer.on('autoUpdater:update-downloaded', (event, info) => {
      //this.state = 'ready'
      //this.updateInfo = info
      //this.emit('update-downloaded', info)
    })
    ipcRenderer.on('autoUpdater:error', (event, err) => {
      this.emit('update-error', err)
    })
  }

```

Assurez-vous de bien sauvegarder les modifications apportées au fichier.




9. Une fois que les deux fichiers ont été modifiés, nous allons les repackager à l'aide d'asar.

Exécutez la commande ci-dessous pour packager à nouveau avec asar :

```
asar pack app app.asar
```

Ensuite, ouvrez à nouveau l'application StarUML.

Et voilà ! Vous ne verrez plus l'inscription "UNREGISTERED" et il n'y aura plus de fenêtre contextuelle vous demandant d'acheter la licence.

J'espère que cela vous sera utile
