# UML :
Ci-dessous le diagramme de classes UML pour l'ensemble de ce programme  :
```mermaid
---
title: F08-Garage
---
classDiagram
class Application {
    +main(String[] args)$ void
}
class Voiture {
    -String marque
    -String modele
    -int km
    -double prix
    +Voiture(String marque, String modele, int km, double prix)
    +toString() String
    +getMarque() String
    +setMarque(String marque) void
    +getModele() String
    +setModele(String modele) void
    +getKm() int
    +setKm(int km) void
    +getPrix() int
    +setPrix(double prix) void
}
class Garage {
    +int MAX_VOITURES$
    -String nom
    -String ville
    -String proprietaire
    -Voiture[] parking
    +Garage(String nom, String ville, String proprietaire)
    +Garage(String nom, String ville)
    +ajouteVoiture(Voiture v) boolean
    +supprimeVoiture(Voiture v) boolean
    +listeDesVoitures() Voiture[]
    +toString() String
    +getNom() String
    +setNom(String nom) void
    +getVille() String
    +setVille(String ville) void
    +getProprietaire() String
    +setProprietaire(String proprietaire) void
}
note for Garage "MAX_VOITURES = 10"
Garage "1" o--> "0..n" Voiture : -parking
Application ..> Garage : utilise
```
