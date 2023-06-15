# Diagramme ER - Notation "patte d'oie" :
```mermaid
---
title: F08-Garage
---
erDiagram
    GARAGE ||--o{ VOITURE : contient
    GARAGE {
        string nom
        string ville
        string proprietaire
    }
    VOITURE {
        string marque
        string modele
        int km
        double prix
    }
```
# Diagramme UML - Séquence du main() de l'application :
```mermaid
---
title: F08-Garage
---
sequenceDiagram
    main()->>Garage monGarage : <<creation>>
    main()->>Voiture v1 : <<creation>>
    main()->>Voiture v2 : <<creation>>
    main()->>Voiture v3 : <<creation>>
    main()->>+Garage monGarage : ajouteVoiture(v1)
    Garage monGarage-->>-main(): ajoutOK
    alt ajoutOK == true
        main()->>System.out : println("Ajout de v1 a réussi !")
        main()->>+Garage monGarage : ajouteVoiture(v2)
        Garage monGarage-->>-main(): ajoutOK
        alt ajoutOK == true
            main()->>System.out : println("Ajout de v2 a réussi !")
            main()->>+Garage monGarage : ajouteVoiture(v3)
            Garage monGarage-->>-main(): ajoutOK
            alt ajoutOK == true
                main()->>System.out : println("Ajout de v3 a réussi !")

                main()->>+Garage monGarage : toString()
                Garage monGarage-->>-main(): txtGarage

                main()->>System.out : println("Voici le contenu du Garage : " + txtGarage)

                main()->>+Garage monGarage : listeDesVoitures()
                Garage monGarage-->>-main(): voitures

                loop FOR EVERY voiture IN voitures NOT NULL
                    main()->>System.out : println(voiture)
                end

            else
                main()->>System.err : println("La voiture v3 n'a pas été ajoutée car le parking est plein !")
            end
        else
            main()->>System.err : println("La voiture v2 n'a pas été ajoutée car le parking est plein !")
        end
    else
        main()->>System.err : println("La voiture v1 n'a pas été ajoutée car le parking est plein !")
    end
```

# Diagramme UML - Classes de l'application :
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
