# **RAPPORT DE PROJET : Cube en Rotation avec Bouton Start/Stop dans Unity (Vuforia ou Unity classique)**
Auteur : Jamila Dabachine : Cube en Rotation avec Bouton Start/Stop dans Unity (Vuforia ou Unity classique)**
## **1. Introduction**

Ce rapport présente la réalisation d’un mini‑projet en Unity permettant d’afficher un cube 3D en rotation continue, ainsi qu’un bouton d’interface utilisateur (UI Button) permettant de démarrer ou d’arrêter cette rotation. Le projet a été réalisé dans un contexte d’apprentissage de la création d’interfaces interactives dans Unity, ainsi que la manipulation d’objets 3D et de scripts C#.

Le but est de comprendre :

* la création d’un objet 3D (Cube) ;
* l’animation d’un mouvement par script ;
* la création d’une interface utilisateur (Canvas, Button) ;
* le lien entre un bouton et un script (OnClick Event) ;
* la gestion d’un état logique (rotation active ou arrêtée).

---

## **2. Étapes de réalisation du projet**

### **2.1. Création d’un nouveau projet Unity**

1. Ouvrir *Unity Hub*.
2. Cliquer sur **New Project**.
3. Choisir le template **3D Core**.
4. Nommer le projet : *CubeRotationProject*.
5. Cliquer sur **Create Project**.

Cette étape initialise l’environnement de travail dans lequel seront placés tous les éléments 3D et UI du projet.

---

### **2.2. Création du Cube 3D**

*(Dans notre projet basé sur Vuforia, le cube sera affiché au-dessus d’un Image Target.)*

### **Étape Vuforia : Création et ajout d’un Image Target**

Avant de créer le cube, il est nécessaire d’ajouter une cible AR (Image Target) car le cube doit apparaître uniquement lorsque la caméra détecte une image.

#### **1) Création d’une base de données Vuforia (sur le site officiel)**

1. Aller sur : [https://developer.vuforia.com](https://developer.vuforia.com)
2. Se connecter à son compte.
3. Dans le menu, ouvrir **Target Manager**.
4. Cliquer sur **Add Database** → choisir le type : **Device Database**.
5. Donner un nom à la base (ex : *CubeRotationDB*).
6. Cliquer sur la base créée puis faire **Add Target**.
7. Choisir le type : **Image Target**.
8. Importer l’image à utiliser comme marqueur AR.
9. Indiquer la taille (par exemple 10 cm → 0.1 unity unit).
10. Cliquer sur **Add**.
11. Ensuite cliquer sur **Download Database (Unity Package)**.
12. Importer le fichier dans Unity (Double-click → Unity → Import All).

#### **2) Ajout d’un Image Target dans Unity**

1. Dans *Hierarchy* : `Right Click → Vuforia Engine → Image Target`.
2. Dans *Inspector* :

   * Type : **From Database**.
   * Database : madatabase.
   * Image : sélectionner l’image importée.
3. L’Image Target apparaît dans la scène et servira de support pour le cube.
voila mon image :
![Lilo and stitch SVG PNG Vector](https://github.com/user-attachments/assets/81377c93-41a7-4c02-b41b-fad5158e1f97)

---

### **Création du Cube 3D**

1. Dans la fenêtre **Hierarchy**, faire :
   `Right Click → 3D Object → Cube`.
2. Renommer l’objet en : **RotatingCube**.
3. Ajuster la position si nécessaire (par défaut : 0,0,0).

Ce cube constitue l’objet principal du projet, celui sur lequel sera appliquée la rotation.

---

### **2.3. Création du Script de Rotation**

Un script C# est nécessaire pour animer la rotation du cube.

1. Aller dans le dossier **Assets**.
2. Clic droit → `Create → C# Script`.
3. Nommer le script : **CubeRotate**.
4. Ouvrir le script et saisir le code suivant :

```csharp
using UnityEngine;

public class CubeRotate : MonoBehaviour
{
    public float speed = 50f;
    private bool isRotating = true;

    void Update()
    {
        if (isRotating)
        {
            transform.Rotate(Vector3.up * speed * Time.deltaTime);
        }
    }

    public void ToggleRotation()
    {
        isRotating = !isRotating;
    }
}
```

### **Explication de cette étape :**

* `speed` : vitesse de rotation.
* `isRotating` : variable qui indique si la rotation est active.
* Dans `Update()`, le cube tourne uniquement si `isRotating == true`.
* La méthode `ToggleRotation()` inverse l'état de rotation : si ça tourne → ça s'arrête, si c'est arrêté → ça tourne.

5. Glisser le script **CubeRotate** sur l’objet **RotatingCube**.

---

## **2.4. Création d’une Interface Utilisateur (Canvas + Button)**

Pour contrôler la rotation, un bouton Start/Stop est ajouté.

### **Étapes de création du bouton :**

1. Dans **Hierarchy** : `Right Click → UI → Button (TextMeshPro)`.
2. Unity demande d’importer TextMeshPro → cliquer sur **Import TMP Essentials**.
3. Renommer le bouton : **ToggleRotationButton**.
4. Ouvrir l’objet pour modifier le texte :

   * Sélectionner *Text (TMP)*.
   * Changer le texte en :
     **"Start / Stop Rotation"**.

### **Explication :**

Le Canvas permet l’affichage d’éléments UI dans la scène.
Le bouton sera utilisé pour appeler la fonction `ToggleRotation()` du script.

---

## **2.5. Configuration du bouton (OnClick Event)**

Cette étape relie le bouton au script du cube.

1. Sélectionner **ToggleRotationButton**.
2. Dans l’inspecteur, trouver la section **Button → OnClick()**.
3. Cliquer sur **+** pour ajouter un événement.
4. Faire **Drag & Drop** de l’objet **RotatingCube** dans la zone de l’événement.
5. Dans le menu déroulant, choisir :

```
CubeRotate → ToggleRotation()
```

### **Explication :**

À chaque clic, Unity appelle la fonction `ToggleRotation()` du script CubeRotate, ce qui démarre ou arrête la rotation.

---

## **3. Résultat obtenu**

À la fin du projet, les fonctionnalités suivantes sont opérationnelles :

* Un cube 3D visible dans la scène.
* Le cube tourne automatiquement autour de l’axe Y.
* Un bouton UI "Start / Stop Rotation" est affiché.
* Lorsque l’utilisateur clique sur ce bouton, la rotation du cube s’arrête.
* Un deuxième clic relance immédiatement la rotation.

Le projet permet donc de comprendre la logique d’interaction entre interface graphique (UI), scripts C#, et objets 3D.

---
<img width="855" height="486" alt="projet unity" src="https://github.com/user-attachments/assets/72f260fe-913b-4d42-9a04-425f88a346ae" />


## **4. Conclusion**

Ce projet simple mais pédagogique permet de se familiariser avec :

* la création d’objets 3D ;
* la programmation orientée objet en C# ;
* les interactions utilisateur via UI Buttons ;
* le système d’événements dans Unity ;
* la gestion des états (rotation active/non active).

Il constitue une bonne base pour réaliser des projets plus avancés comme :

* des objets interactifs en AR (Vuforia) ;
* des animations déclenchées par boutons ;
* des mini‑jeux 3D.

Si nécessaire, une version plus avancée ou une mise en page type "rapport universitaire" peut être fournie.

---

## **5. Suggestions d’amélioration**

* Ajouter un effet sonore au clic du bouton.
* Changer la couleur du cube à chaque clic.
* Ajouter un slider pour régler la vitesse de rotation.
* Intégrer le cube comme objet AR via Vuforia.
https://drive.google.com/drive/folders/1emR8mFhz5j4mhNFf7mXxtg5fxVcZfsQe?usp=drive_link
---

## **6. Annexes**

### Code source complet

(cf. section 2.3.)
