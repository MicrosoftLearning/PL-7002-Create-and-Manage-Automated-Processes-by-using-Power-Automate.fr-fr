---
lab: title: « Labo 6 : « Flux planifié : « Module 5 : Intégration approfondie de Power Automate parmi plusieurs sources de données
---

# Labo pratique 6 : Flux planifié

Dans ce labo, vous allez créer un flux planifié.

## Contenu du didacticiel

- Comment créer un flux planifié Power Automate et traiter une liste d’éléments SharePoint.

## Étapes de labo de haut niveau

- Créer un flux planifié
- Interroger une liste SharePoint
- Utiliser les opérations sur les données
- Tester le flux
  
## Prérequis

- Vous devez avoir terminé **Labo 3 : SharePoint**

## Procédure détaillée

## Exercice 1 : Créer un flux planifié

### Tâche 1.1 : Créer le déclencheur

1. Accédez au portail Power Automate <https://make.powerautomate.com>.

1. Vérifiez que vous êtes dans l’environnement **Dev One**.

1. Sélectionnez l’onglet **+ Créer** dans le menu de gauche.

1. Sélectionnez **Flux de cloud planifié**.

1. Entrez `Daily New Tasks` pour **Nom du flux**.

1. Sélectionner **Jour**.

    ![Capture d’écran de la génération d’un flux planifié.](../media/build-scheduled-flow.png)

1. Sélectionnez **Créer**.

### Tâche 1.2 : Configurer le déclencheur

1. Sélectionnez l’étape **Périodicité**.

1. Sélectionnez le nom d’étape **Périodicité** et entrez `Daily`.

### Tâche 1.3 : Interroger de nouvelles tâches

1. Sélectionnez l’icône **+** sous l’étape du déclencheur, puis sélectionnez **Ajouter une action**.

1. Entrez `list items` dans Rechercher.

1. Sélectionnez **Obtenir les éléments** sous **SharePoint**.

1. Sélectionnez le nom d’étape **Obtenir les éléments** et entrez `New tasks`.

1. Sélectionner le **site SharePoint Power Automate**.

1. Sélectionnez la liste **Tâches**.

1. Sélectionnez **Afficher tout**.

1. Sélectionnez le champ **Filtrer la requête** et entrez `ApprovalStatus eq 'New'`

    ![Capture d’écran de la requête d’éléments de liste.](../media/list-items.png)

### Tâche 1.4 : Sélectionner des colonnes

1. Sélectionnez l’icône **+** sous l’étape Nouvelles tâches, puis sélectionnez **Ajouter une action**.

1. Entrez `Select` dans Rechercher.

1. Pour **Runtime**, sélectionnez **Intégré**.

1. Sous **Opérations de données**, sélectionnez **Sélectionner**.

1. Sélectionnez le champ **De**, puis l’icône de contenu dynamique.

1. Dans **Nouvelles tâches**, sélectionnez **corps/valeur**.

1. Sélectionnez le champ **Entrer la clé** et entrez `Task`.

1. Sélectionnez le champ **Entrer la valeur**, puis l’icône de contenu dynamique.

1. Dans **Nouvelles tâches**, sélectionnez **Titre**.

1. Sélectionnez le champ **Entrer la clé** et entrez `Description`.

1. Sélectionnez le champ **Entrer la valeur**, puis l’icône de contenu dynamique.

1. Dans **Nouvelles tâches**, sélectionnez**Description**.

1. Sélectionnez le champ **Entrer la clé** et entrez `Due`.

1. Sélectionnez le champ **Entrer une valeur** et l’icône Contenu dynamique, puis **Voir plus**.

1. Dans **Nouvelles tâches**, sélectionnez **Échéance**.

    ![Capture d’écran de Sélectionner l’action.](../media/select-action.png)

1. Si le concepteur de flux a automatiquement ajouté une ou plusieurs boucles For Each, faites glisser l’étape Sélectionner en dehors des boucles et supprimez la ou les boucles.

    ![Capture d’écran des étapes de flux sans boucles.](../media/flow-without-loops.png)

### Tâche 1.5 : Créer un tableau

1. Sélectionnez l’icône **+** sous l’étape Sélectionner, puis sélectionnez **Ajouter une action**.

1. Entrez `create html` dans Rechercher.

1. Sous **Opérations de données**, sélectionnez **Créer un tableau HTML**.

1. Sélectionnez le nom d’étape **Créer un tableau HTML** et entrez `Format as HTML table`.

1. Sélectionnez le champ **De**, puis l’icône de contenu dynamique.

1. Dans **Sélectionner**, sélectionnez **Sortie**.

    ![Capture d’écran de l’action Mettre sous forme de tableau HTML.](../media/format-html-action.png)

### Tâche 1.6 : Envoyer un e-mail

1. Sous l’étape Créer un tableau HTML, sélectionnez l’icône **+**, puis **Ajouter une action**.

1. Entrez `email` dans Rechercher.

1. Sous **Office 365 Outlook**, sélectionnez **Envoyer un e-mail (V2)**.

1. Sélectionnez le nom d’étape **Envoyer un e-mail (V2)** et entrez `Notify by email`.

1. Sélectionnez le champ **À**, puis **Entrer une valeur personnalisée**.

1. Pour **À**, entrez l’ID d’utilisateur de votre locataire.

1. Sélectionnez le champ **Objet** et entrez `Daily Tasks`.

1. Sélectionnez le champ **Corps**, puis l’icône de contenu dynamique.

1. Dans **Mettre sous forme de tableau HTML**, sélectionnez **Sortie**.

1. Sélectionnez **Enregistrer**.

## Exercice 2 : Tester le flux planifié

### Tâche 2.1 : Exécuter manuellement le flux planifié

1. Sélectionnez **Tester**.

1. Sélectionnez **Manuellement**.

1. Sélectionnez **Test**.

1. Cliquez sur **Exécuter le flux**.

1. Cliquez sur **Terminé**.

1. Dans le portail Power Automate, sélectionnez le **lanceur d’applications** en haut à gauche de la fenêtre du navigateur, puis **Outlook**.

    ![Capture d’écran de l’action Mettre sous forme de tableau HTML.](../media/daily-tasks-email.png)
