# TP Flutter : Découverte du Widget Stateless, MaterialApp, Color, Text, Scaffold, Drawer

## Objectifs du TP

Ce TP a pour objectif de découvrir les concepts fondamentaux de Flutter, notamment :
- L'utilisation des StatelessWidget
- La configuration de MaterialApp et ThemeData
- La personnalisation des couleurs et du texte
- L'implémentation d'un Scaffold avec AppBar et Drawer
- La centralisation des styles dans le thème

## Concepts Flutter expliqués

### StatelessWidget
Un StatelessWidget est un widget immuable, ce qui signifie que ses propriétés ne peuvent pas changer au fil du temps. Il est utilisé pour les parties de l'interface utilisateur qui n'ont pas besoin de maintenir un état et qui ne changent pas en fonction de l'interaction de l'utilisateur.

### MaterialApp
MaterialApp est le widget racine qui fournit de nombreuses fonctionnalités du Material Design. Il configure le thème, les routes, le titre de l'application et d'autres paramètres globaux.

### ThemeData
ThemeData définit les propriétés visuelles pour l'ensemble de l'application. Il permet de centraliser les styles (couleurs, typographie, etc.) pour maintenir une cohérence visuelle dans toute l'application.

### Scaffold
Scaffold fournit la structure de base pour un écran dans une application Material Design. Il inclut des fonctionnalités comme l'AppBar, le Drawer, le BottomNavigationBar, etc.

### AppBar
AppBar est la barre supérieure de l'application qui affiche généralement le titre de l'écran et peut contenir des actions.

### Drawer
Drawer est un panneau qui glisse depuis le côté de l'écran et sert généralement de menu de navigation.

## Architecture de l'application

L'application est structurée comme suit :
1. **MyApp (StatelessWidget)** : Widget racine qui configure MaterialApp et ThemeData
2. **MyHomePage (StatelessWidget)** : Écran principal qui implémente Scaffold avec AppBar, body et Drawer
3. **Drawer** : Menu latéral avec en-tête et éléments de menu stylisés

## Explication du code

### main.dart

```dart
import 'package:flutter/material.dart';

// Point d'entrée de l'application
void main() {
  runApp(const MyApp());
}

/// MyApp : Widget StatelessWidget racine de l'application
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    // MaterialApp est le widget racine qui fournit de nombreuses fonctionnalités Material Design
    return MaterialApp(
      title: 'TP Flutter Découverte',
      // ThemeData définit les propriétés visuelles pour toute l'application
      theme: ThemeData(
        // Définir la couleur primaire sur deepOrange comme requis
        primaryColor: Colors.deepOrange,
        primarySwatch: Colors.deepOrange,

        // Utiliser Material 3 design
        useMaterial3: true,

        // Configurer le schéma de couleurs
        colorScheme: ColorScheme.fromSeed(
          seedColor: Colors.deepOrange,
          secondary: Colors.teal,
          tertiary: Colors.tealAccent,
          brightness: Brightness.light,
        ),

        // Configurer le thème AppBar avec la couleur de titre teal comme requis
        appBarTheme: const AppBarTheme(
          elevation: 0,
          centerTitle: true,
          titleTextStyle: TextStyle(
            color: Colors.teal, // Changé en teal selon les exigences
            fontSize: 22,
            fontWeight: FontWeight.bold,
            letterSpacing: 1.2,
          ),
        ),

        // Configurer le thème de texte avec une typographie moderne
        textTheme: const TextTheme(
          // Centraliser la couleur et la taille du texte dans bodyLarge comme requis
          bodyLarge: TextStyle(
            fontSize: 20, // Taille de police augmentée pour une meilleure lisibilité
            color: Colors.black87, // Couleur de texte centralisée
            fontWeight: FontWeight.normal,
            letterSpacing: 0.5,
          ),
        ),
      ),
      // La propriété home définit la route par défaut de l'application
      home: const MyHomePage(title: 'Découverte Flutter'),
      debugShowCheckedModeBanner: false, // Supprime la bannière de débogage
    );
  }
}

/// MyHomePage : Écran principal de l'application
class MyHomePage extends StatelessWidget {
  final String title;

  const MyHomePage({super.key, required this.title});

  @override
  Widget build(BuildContext context) {
    // Scaffold fournit la structure de base pour un écran dans une application Material Design
    return Scaffold(
      // AppBar est la barre supérieure de l'application
      appBar: AppBar(
        backgroundColor: Theme.of(context).primaryColor, // Utilisation de la couleur deepOrange du thème
        title: Text(title), // Utilisation du titre passé depuis MyApp
      ),
      
      // Définir la couleur de fond sur deepOrange en utilisant Theme.of(context).primaryColor comme requis
      backgroundColor: Theme.of(context).primaryColor,

      // Le body contient le contenu principal de l'écran
      body: Center(
        child: Container(
          padding: const EdgeInsets.all(16.0),
          margin: const EdgeInsets.all(16.0),
          decoration: BoxDecoration(
            color: Colors.white,
            borderRadius: BorderRadius.circular(12.0),
            boxShadow: [
              BoxShadow(
                color: Colors.black.withOpacity(0.1),
                spreadRadius: 1,
                blurRadius: 5,
                offset: const Offset(0, 3),
              ),
            ],
          ),
          child: Text(
            'Bienvenue dans notre application de découverte Flutter!',
            // Utilisation du style de texte défini dans le thème
            style: Theme.of(context).textTheme.bodyLarge,
            textAlign: TextAlign.center,
          ),
        ),
      ),

      // Drawer est un panneau qui glisse depuis le côté de l'écran
      drawer: Drawer(
        child: ListView(
          padding: EdgeInsets.zero,
          children: <Widget>[
            // DrawerHeader est la section supérieure du drawer
            DrawerHeader(
              decoration: BoxDecoration(
                color: Theme.of(context).primaryColor,
                boxShadow: [
                  BoxShadow(
                    color: Colors.black.withOpacity(0.2),
                    spreadRadius: 1,
                    blurRadius: 5,
                    offset: const Offset(0, 3),
                  ),
                ],
              ),
              child: const Center(
                child: Text(
                  'Menu de Navigation',
                  style: TextStyle(
                    color: Colors.white,
                    fontSize: 24,
                    fontWeight: FontWeight.bold,
                    letterSpacing: 1.2,
                  ),
                  textAlign: TextAlign.center,
                ),
              ),
            ),

            // Éléments de menu utilisant Container avec un style personnalisé
            Container(
              margin: const EdgeInsets.all(8.0),
              decoration: BoxDecoration(
                border: Border.all(color: Colors.grey),
                borderRadius: BorderRadius.circular(8.0),
              ),
              child: const ListTile(
                leading: Icon(Icons.home),
                title: Text('Accueil'),
              ),
            ),

            Container(
              margin: const EdgeInsets.all(8.0),
              decoration: BoxDecoration(
                border: Border.all(color: Colors.grey),
                borderRadius: BorderRadius.circular(8.0),
              ),
              child: const ListTile(
                leading: Icon(Icons.settings),
                title: Text('Paramètres'),
              ),
            ),

            Container(
              margin: const EdgeInsets.all(8.0),
              decoration: BoxDecoration(
                border: Border.all(color: Colors.grey),
                borderRadius: BorderRadius.circular(8.0),
              ),
              child: const ListTile(
                leading: Icon(Icons.info),
                title: Text('À propos'),
              ),
            ),

            Container(
              margin: const EdgeInsets.all(8.0),
              decoration: BoxDecoration(
                border: Border.all(color: Colors.grey),
                borderRadius: BorderRadius.circular(8.0),
              ),
              child: const ListTile(
                leading: Icon(Icons.help),
                title: Text('Aide'),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```
## Résumé

Ce TP nous a permis de découvrir les concepts fondamentaux de Flutter :

- **StatelessWidget** : Widgets immuables pour les parties statiques de l'UI
- **MaterialApp** : Configuration globale de l'application
- **ThemeData** : Centralisation des styles pour toute l'application
- **Scaffold** : Structure de base d'un écran Material Design
- **AppBar** : Barre supérieure de l'application
- **Drawer** : Menu latéral pour la navigation
- **Theme.of(context)** : Accès aux propriétés du thème depuis n'importe quel widget

L'application implémentée répond à toutes les exigences du TP en utilisant les meilleures pratiques de Flutter.
