# Dev GO
le language fonctionne mieux sur le parallélisme et est moins lourd en consommation d'infra.
Le projet devait initialement être des forks de C++, mais refusés par la communauté et là est né un projet indépendant.

Pour rendre une fonction public, on la commence par une lettre majuscule.

Initialisation des modules:
```
go mod init
```

Execution d'un script :
```
go run main.go
```

Build d'un module :
```
go build main.go
```

## Keywords in GO

**package**

**import**

```
import "fmt"
import "image/png"
import "image/jpeg"
```
```
import (
    "fmt"
    "image/png"
    "image/jpeg"
)
```
```
import (
    "fmt"
    _ "image/png" //permet d'indiquer en cas de compilation si ce package n'est pas utilisé, et empêche ainsi la compilation de ressources inutiles.
    . "image/jpeg" //récupère tout ce qui est présent dans la librairie
)
```

**const**

Créer une variable dont la valeur ne sera plus modifiée.
définition de plusieurs constantes:
```
type Periodic int
const (
    Ag Periodic = iota
    La
```

**var**

Variables scopés:
```
{
    var a string = "A"
    {
        var a = "B"//a vaut B
    }
    //a vaut A
}
```

**func**
fonctions sont typés, et le return est typé également.

```
func Hello (n string) string {
    return "Salut " + n
}
```

Si deux cas de retournement de fonction, on les précises:
```
func Hello (n string) (string,error) {
    if len(n) == 0{
        return "Salut " + n
    }
    return errors.New('no name')
}
```

**defer**

exécution du code après l'exécution d'une fonction.

**map**
dictionnaires

```
m := make(map[string]int)

m := map[string]int{
    "keyA":0,
    "keyB":1,
    "keyC":2,
}
```

# projet
Team de 3-4 personnes.
API à développer autour d'un système de vote.
Sécurisation avec JWT

On se revoit le 30.

Deux notes : 
- bonnes pratiques de code
- performances

L'analyser pour les perfs s'appel GoReporter (Github)
 Voir le Readme du projet pour le cahier des charges

il faudra ilmplémenter l'interface JSON -> https://golang.org/pkg/encoding/json/
A faire avant le dimanche 29 Septembre !
ORM : https://gorm.io/docs/
