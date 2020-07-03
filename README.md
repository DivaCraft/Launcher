<p align="center"><img src="./app/assets/images/SealCircle.png" width="150px" height="150px" alt="aventium softworks"></p>

<h1 align="center">DivaCraft Launcher</h1>

<em><h5 align="center">(basé sur l'Helios Launcher, anciennement Electron Launcher)</h5></em>

[<p align="center"><img src="https://img.shields.io/travis/DivaCraft/Launcher.svg?style=for-the-badge" alt="travis">](https://travis-ci.org/github/DivaCraft/Launcher) [<img src="https://img.shields.io/github/downloads/DivaCraft/Launcher/total.svg?style=for-the-badge" alt="downloads">](https://github.com/DivaCraft/Launcher/releases) <img src="https://forthebadge.com/images/badges/winter-is-coming.svg"  height="28px" alt="stark"></p>

<p align="center">Jouer au modpack/serveur DivaCraft sans se soucier d'installer Java, Forge ou des mods. Nous nous occupons de ça.</p>

![Screenshot 1](https://i.imgur.com/6o7SmH6.png)
![Screenshot 2](https://i.imgur.com/x3B34n1.png)

## Fonctionnalités

* 🔒 Gestion de compte complète.
  * Ajouter plusieurs comptes et changer de compte rapidement.
  * Les identifiants de connexion ne sont jamais stockés et transmis directement à Mojang.
* 📂 Gestion des fichiers éfficace.
  * Recevez les mises à jour client au moment ou nous les publions.
  * Les fichiers sont validés avant chaque démarrage. Les fichiers corrompus ou manquants seront retéléchargés.
* ☕ **Validation automatique de Java.**
  * Si vous avez une version incompatible de Java installée, nous installerons la bonne *pour vous*.
  * Vous n'avez pas besoin d'avoir Java d'installé pour utiliser le launcher.
* 📰 Fil de nouveautés intégré dans le launcher.
* ⚙️ Paramètres intuitifs, inclus les paramètres Java.
* Supporte le serveur DivaCraft
  * Permet de changer de serveur (Beta, ...) simplement.
  * Voir le nombre de joueurs connectés sur le serveur correspondant.
* Mises à jour automatiques. Oui oui, le launcher se met à jour de lui même.
* Permet de voir le status des serveurs de Mojang.

Cette liste est non exhaustive. Téléchargez le launcher pour juger de ses fonctionnalités !

#### Besoin d'aide ? [Visitez le Wiki (en Anglais).][wiki]

#### Vous aimez le projet ? Laissez une ⭐ étoile sur le repository !

## Téléchargements

Vous pouvez télécharger le launcher depuis les [Releases GitHub](https://github.com/DivaCraft/Launcher/releases)

#### Dernière Version

[![](https://img.shields.io/github/release/DivaCraft/Launcher.svg?style=flat-square)](https://github.com/DivaCraft/Launcher/releases/latest)

#### Dernière Pre-Release
[![](https://img.shields.io/github/release/DivaCraft/Launcher/all.svg?style=flat-square)](https://github.com/DivaCraft/Launcher/releases)

**Plateformes Supportées**

Si vous téléchargez depuis l'onglet [Releases](https://github.com/DivaCraft/Launcher/releases), sélectionnez l'installeur en fonction de votre système d'exploitation.

| Plateforme | Fichier |
| -------- | ---- |
| Windows x64 | `divacraftlauncher-setup-VERSION.exe` |
| macOS | `divacraftlauncher-VERSION.dmg` |
| Linux x64 | `divacraftlauncher-VERSION-x86_64.AppImage` |

## Console

Pour ouvrir la console, utilisez le raccourci clavier suivant.

```console
ctrl + shift + i
```

Si vous ne voyez toujours pas la console, vérifiez que l'onglet "Console" est sélectionné. Ne copiez-collez jamais quoi que ce soit dans cette console SAUF si vous savez à 100% ce que vous faites. Copier-coller des commandes pourrait exposer des informations sensitives.

#### Exporter les logs vers un fichier

Si vous voulez exporter les logs de la console, faites simplement un clique droit n'importe ou dans la console et cliquez sur **Save as..**

![console example](https://i.imgur.com/T5e73jP.png)


## Développement

### Bien démarrer

**Prérequis**

* [Node.js][nodejs] v12

---

**Clonage et installation des dépendances**

```console
> git clone https://github.com/DivaCraft/Launcher.git
> cd Launcher
> npm install
```

---

**Démarrer l'Application**

```console
> npm start
```

---

**Compiler les installeurs**

Pour compiler l'installeur de votre plateforme.

```console
> npm run dist
```

Pour compiler pour une autre plateforme.

| Platforme    | Commande              |
| ----------- | -------------------- |
| Windows x64 | `npm run dist:win`   |
| macOS       | `npm run dist:mac`   |
| Linux x64   | `npm run dist:linux` |

La compilation pour macOS ne fonctionnera pas sur Windows/Linux et vice-versa.

---

### Visual Studio Code

Le développement du launcher doit se faire via [Visual Studio Code][vscode].

Copier-coller dans `.vscode/launch.json`

```JSON
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug Main Process",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceRoot}",
      "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/electron.cmd"
      },
      "args": ["."],
      "console": "integratedTerminal",
      "protocol": "inspector"
    },
    {
      "name": "Debug Renderer Process",
      "type": "chrome",
      "request": "launch",
      "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/electron.cmd"
      },
      "runtimeArgs": [
        "${workspaceRoot}/.",
        "--remote-debugging-port=9222"
      ],
      "webRoot": "${workspaceRoot}"
    }
  ]
}
```

Cela ajoute deux configurations de debug.

#### Debug Main Process

Permet de debug le [main process][mainprocess] d'Electron. Vous pouvez débugger les scripts du [renderer process][rendererprocess] en ouvrant la console.

#### Debug Renderer Process

Permet de debug le [renderer process][rendererprocess] d'Electron. Nécessite l'extension [Debugger for Chrome][chromedebugger].

Note : Vous ne **pouvez pas** ouvrir la console de développement en utilisant cette configuration de Debug. Chromium autorise un seul debugger, en ouvrir un second fera crash le programme.

---

### Note sur l'utilisation par des tiers

Vous pouvez utiliser ce logiciel dans votre propre projet pour autant que les conditions suivantes soient remplies.

* Le crédit est expressément accordé aux auteurs originaux (Daniel Scalzi).
  * Inclure un lien vers la source originale sur la page "À propos" du launcher.
  * Mentionner les auteurs et fournir un lien vers la source originale dans toute publication ou page de téléchargement.
* Le code source reste **public** en tant que fork du dépot original.

L'auteur original se réserve le droit d'actualiser ces conditions à tout moment.

---

## Ressources

* [Wiki de l'Helios Launcher][wiki]

Vous pouvez contacter les développeurs originaux du Launcher sur leur Discord (en Anglais) :

[![discord](https://discordapp.com/api/guilds/211524927831015424/embed.png?style=banner3)][discord]

---

### À bientôt en jeu !


[nodejs]: https://nodejs.org/en/ 'Node.js'
[vscode]: https://code.visualstudio.com/ 'Visual Studio Code'
[mainprocess]: https://electronjs.org/docs/tutorial/application-architecture#main-and-renderer-processes 'Main Process'
[rendererprocess]: https://electronjs.org/docs/tutorial/application-architecture#main-and-renderer-processes 'Renderer Process'
[chromedebugger]: https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome 'Debugger for Chrome'
[discord]: https://discord.gg/zNWUXdt 'Discord'
[wiki]: https://github.com/dscalzi/HeliosLauncher/wiki 'wiki'
[nebula]: https://github.com/dscalzi/Nebula 'dscalzi/Nebula'
[v2branch]: https://github.com/dscalzi/HeliosLauncher/tree/ts-refactor 'v2 branch'
