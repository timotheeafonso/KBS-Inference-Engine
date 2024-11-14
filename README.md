# Système à Base de Connaissance (SBC)

Création d'un système d'inférence prenant en charge à la fois la logique binaire et probabiliste. La base de connaissances et l'ensemble de règles peuvent être définis manuellement. Des algorithmes de chaînage avant et arrière sont disponibles.

## Exemple de Chaînage Avant :

### Base de faits :
```
A, C
```

### Base de règles : 
```
A -> B
B & C -> D
```

### Résultats :
```
A, B, C, D
```

## Exemple de Chaînage Arrière :

### Base de faits:
```
A, C
```

### Base de règles :
```
A -> B
B & C -> D
```

### But :
```
D
```

### Résultat :
```
D peut être déduit car A et C sont vrais et les règles permettent d'inférer D.
```

# Lancement du Projet

Possibilité de mettre à jour la base de faits et la base de règles. Dans le cas du chaînage arrière, il est également possible de modifier le but recherché. Les opérateurs acceptés pour la base de règles sont :
```
==, <, >, <=, >=, ~ (négation)
```

Une règle est de la forme :
```
<premisse> = <consequence>
```

`<premisse>` et `<consequence>` sont des ensembles de faits (booléens ou numériques) séparés par le symbole `&` pour exprimer des conditions multiples. Voir les fichiers d'exemples pour plus de détails (faits.txt, faitsInit.txt, regles.txt). Le tri des règles par paquets est possible afin d'accélérer le calcul. Pour cela, les règles doivent être identifiées par un numéro :
```
[numéro de paquet] <premisse> = <consequence>
```
Pour tester de nouveaux exemples, il faut créer un nouveau fichier de test (en s'inspirant des fichiers "Test---.java").

Chaînage avant:

```
public class TestChainageAvant {
    public static void main(String[] args) throws Exception {
		BaseFait bf = new BaseFait();
		try {
			bf.genererFaitsInitiaux("faits.txt");
		} catch (Exception e) {
			e.printStackTrace();
		}
		BaseRegle br = new BaseRegle();
		try {
			br.generer("regles.txt");
		} catch (Exception e) {
			e.printStackTrace();
		}
    MoteurInference.execChainageAvant(bf, br, false); // mettre true si utilisation de paquet
	}
}
```

Chaînage arrière:

```
public class Test... {
    public static void main(String[] args) throws Exception {
  		BaseRegle br = new BaseRegle();
  		try {
  			br.generer("regles.txt");
  		} catch (Exception e) {
  			e.printStackTrace();
  		}
      Fait but = new Fait("fait_objectif", true);  // fait de type boolean
      // Fait but = new Fait("fait_objectif", 5, ">");  // fait de type entier
		  MoteurInference.execChainageArriere(new BaseFait(),br,but,false); // mettre true si utilisation de paquet
	}
}
```
