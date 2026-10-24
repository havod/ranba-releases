# Installer Ranba

Ranba suit les niveaux gamma d'OptionExp et ton compte IBKR, sur ton ordinateur. Cette
version **n'envoie aucun ordre** : elle observe et affiche, c'est tout. Rien de ce que fait
l'app ne quitte ton poste.

Il te faut trois choses, à installer une fois :

1. **Tailscale**, pour joindre OptionExp ;
2. **IB Gateway**, le petit programme d'IBKR auquel Ranba se branche ;
3. **Ranba**.

Compte environ 15 minutes.

## 1. Tailscale

1. Installe Tailscale : <https://tailscale.com/download> (Mac ou Windows).
2. Connecte-toi, et accepte l'invitation que tu as reçue par courriel.
3. Garde Tailscale connecté quand tu utilises Ranba (icône dans la barre des menus ou près de
   l'horloge).

## 2. IB Gateway

1. Télécharge **IB Gateway (Stable)** :
   <https://www.interactivebrokers.com/en/trading/ibgateway-stable.php>, puis installe-le.
2. Lance-le, choisis **IB API** et **Paper Trading**, puis connecte-toi avec ton compte
   **paper** IBKR (identifiant qui commence par DU). Valide la connexion sur IBKR Mobile si on
   te le demande.
3. Dans IB Gateway : **Configure › Settings › API › Settings**
   - coche **Enable ActiveX and Socket Clients** ;
   - **Socket port** : `4002` ;
   - coche **Read-Only API** (Ranba n'a pas besoin d'envoyer d'ordres) ;
   - dans **Trusted IPs**, ajoute `127.0.0.1` ;
   - **OK**.
4. Dans **Configure › Settings › Lock and Exit** : choisis un redémarrage automatique
   quotidien, hors des heures de marché (par exemple 23 h 45).

Pour avoir les prix en temps réel, le compte paper doit partager les abonnements de données de
ton compte réel (options US « OPRA » et actions US) : Portail client IBKR › Réglages ›
Réglages du compte paper › partager les données de marché.

## 3. Ranba

Télécharge la dernière version : <https://github.com/havod/ranba-releases/releases/latest>

### Sur Mac (Apple Silicon : M1 et plus récent)

1. Ouvre le fichier `.dmg` et glisse **Ranba** dans **Applications**.
2. Ouvre Ranba. Comme l'app n'est pas signée par Apple, macOS la bloque la première fois :
   - va dans **Réglages Système › Confidentialité et sécurité**, tout en bas : « Ranba a été
     bloqué… » › **Ouvrir quand même**, puis confirme ;
   - si macOS dit que l'app est **endommagée**, ouvre le Terminal et tape :
     `xattr -cr /Applications/Ranba.app`, puis rouvre Ranba.

### Sur Windows (10 ou 11, 64 bits)

1. Lance le fichier `Ranba-…-windows-x64-setup.exe`.
2. Windows SmartScreen prévient que l'éditeur est inconnu : **Informations complémentaires ›
   Exécuter quand même**.
3. L'installation ne demande pas de droits d'administrateur. Ranba est ensuite dans le menu
   Démarrer.

## Premier lancement

Ranba ouvre ses **Réglages** :

1. **Adresse d'OptionExp** : celle qu'on t'a donnée (elle se termine par `.ts.net`).
2. **Port d'IB Gateway** : `4002` (IB Gateway, paper).
3. **Tester** : les deux lignes doivent être vertes, avec ton numéro de compte paper.
4. **Enregistrer et redémarrer**.

Tu peux revenir à ces réglages à tout moment avec le bouton **Réglages**, en haut.

## Au quotidien

- Avant l'ouverture (9 h 30, heure de New York) : Tailscale connecté, IB Gateway ouvert et
  connecté, puis ouvre Ranba.
- Pendant la séance, Ranba empêche l'ordinateur de se mettre en veille. Fermer la fenêtre
  arrête Ranba.
- Une nouvelle version s'annonce par un bandeau en haut de la fenêtre : télécharge-la et
  installe-la par-dessus l'ancienne. Tes réglages et tes données sont gardés.

## En cas de problème

| Ce que tu vois | À faire |
| --- | --- |
| OptionExp « Injoignable » | Tailscale est-il connecté ? L'adresse est-elle la bonne ? |
| IBKR « Déconnecté » ou « injoignable » | IB Gateway est-il ouvert et connecté ? L'API est-elle activée sur le port 4002 ? |
| Niveaux « Périmés » hors séance | Normal : OptionExp ne recalcule qu'en séance. |
| Autre chose | Envoie le fichier `ranba.log` à la personne qui t'a donné Ranba. |

Le fichier `ranba.log` et les données de Ranba sont dans :

- Mac : `~/Library/Application Support/Ranba` (dans le Finder : **Aller › Aller au dossier…**) ;
- Windows : `%LOCALAPPDATA%\Ranba` (à taper dans la barre d'adresse de l'Explorateur).
