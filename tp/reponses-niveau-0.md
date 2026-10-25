## 1 - Schema relationel
categorie: (<u>id</u>, libelle)

plat: (<u>id</u>, nom, prix, #id_categorie)

commande: (<u>id</u>, date_commande, numero_table)

commande_ligne: (<u>id</u>, #id_commande, #id_plat, quantite, prix_unitaire) 

## 2 - COmmande_ligne :
elle contient une colonne prix_unitaire  pour sauvegarder le prix unitaire d'une ligne de commande par exemple une personne A commande un cafe de 1000 ar aujourdhui ,ce 1000 ar est stocke dans prix_unitaire  de cette commande ensuite le lendemain gargote decide de changer le prix du cafe passant a 500 ar donc le prix unitaire de la commande de A  ne change pas or si l'on avait pas cette colonne auparavant des qu'on changera le prix du plat dans la table plat tous les commandes d'avant changeront aussi  

## 3-

les lignes d'une comande sont supprimer aussi si on supprime  la colonne 
DELETE CASCADE en ai responsable 

 ## 4- Donnee absurde 
    Prix negatif : -4

    Meme nom plat meme categorie 


## 0.3 
 a-  code http : 200 

    [
        {
            "id": 7,
            "nom": "Mi sao",
            "prix": 6500,
            "id_categorie": 2,
            "categorie": "Soupe"
        },
        {
            "id": 6,
            "nom": "Soupe chinoise",
            "prix": 6000,
            "id_categorie": 2,
            "categorie": "Soupe"
        },
        {
            "id": 13,
            "nom": "Test",
            "prix": 800,
            "id_categorie": 2,
            "categorie": "Soupe"
        }
    ] 

 b- code http : 201 (Created) 

    {
        "id": 18,
        "nom": "Mofo gasy",
        "prix": 300,
        "id_categorie": 1
    } 
 c- code http: 422 Unprocessable Content

    {
    "message": "Données invalides.",
    "errors": {
        "nom": "Le nom du plat est obligatoire.",
        "prix": "Le prix doit être un nombre entier (en Ariary).",
        "id_categorie": "Choisissez une catégorie."
    }
} 
 d- code http: 409 conflict 

    {
    "message": "Ce plat figure déjà dans des commandes, il ne peut pas être supprimé.",
    "errors": {}
}

 e- code http:404 not found


    {
        "message": "Commande 999 introuvable.",
        "errors": {}
    }   


## 5 

    j'obtiens un code 201 car il s'agit d'un POST  c'est a dire d'une creation d'un plat donc il renvoi un 201 pour confirmer la creation et non un 200
     car 200 cest pour dire le succes dun renvoi de donnee venant du serveur 

## 6 
    Postgresql qui bloque a cause du fait quil y a une contrainte sur la cles etrangere id_plat de la table commande_ligne

        id_plat        INTEGER NOT NULL REFERENCES plat(id),

## 7 Creer une commande 

curl -i -X POST \
  http://localhost:8080/api/commandes \
  -H "Content-Type: application/json" \
  -d '{
    "numero_table": 6,
    "lignes": [
      {"id_plat": 4, "quantite": 2},
      {"id_plat": 10, "quantite": 1}
    ]
  }'
 