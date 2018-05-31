# spring-boot-crud-restful

## Exemple CRUD Restful WebService avec Spring Boot

### 1-	Objectif 

Dans cet article, on va montrer comment créer une application  Restful Web Service à l'aide de Spring Boot, et ayant 4 fonctionnements  Create, Read, Update, Delete (CRUD). 

Les données que l'utilisateur recevra seront au format XML ou JSON alors on a besoin d'une bibliothèque de convertir XML en objet  Java et vice versa et une autre pour convertir  JSON en  Java et vice versa que l’on verra par la suite.

### Read (méthode GET)

 Construire un URI qui est assigné pour renvoyer à l'utilisateur une liste d'employés et définit un autre URI qui renvoie à l'utilisateur les informations d'un employé particulier.

•	GET http://localhost:8080/employees

•	GET http://localhost:8080/employee/E01

### Update (méthode PUT).

Construire un URI pour traiter la demande de modification des informations d'un employé. Cet URI n'accepte que les requêtes avec la méthode PUT. Les données jointes à la requête sont les nouvelles informations de l'employé, au format XML ou JSON.

•	PUT http://localhost:8080/employee

### Create (méthode POST)

Construire un  URI pour traiter les demandes (request) dans but de créer un employé (employee). Cet  URI n'accepte que les demandes avec la méthode  POST. Les données attachées de cette demande est l'information de l'employé crée. Elle est sous format de  XML ou  JSON.

•	POST http://localhost:8080/employee

### Delete (méthode DELETE)

Construire un  URI pour traiter une demande (request) de suppression d'un employé (employee). Cet  URI n'accepte que les demandes utilisant la méthode  DELETE

•	DELETE  http://localhost:8080/employee/{empNo}

### 2-	Créer le projet Spring Boot
 
 Ouvrir "IntelliJ IDEA" et cliquez sur "Créer un nouveau projet"
 
![open](https://user-images.githubusercontent.com/28655112/40772501-046363c4-64b8-11e8-95a7-e30deedb3807.png)

Sélectionner  "Projet Maven"

![capture3](https://user-images.githubusercontent.com/28655112/40772533-1e667e6e-64b8-11e8-9c18-d1fc764a12f6.PNG)
 
Remplir les informations requises. "GroupId" est le nom d'organisation unique (dans la plupart des cas, les gens utilisent le nom de domaine de leur société tel que "com.axeane"), "ArtifactId" est le nom unique du projet, et "Version" est le numéro de version du projet
 
 ![capture1](https://user-images.githubusercontent.com/28655112/40772573-3ef0e7a0-64b8-11e8-8907-5fcda7866913.PNG)

On obtient 
 
 ![2](https://user-images.githubusercontent.com/28655112/40772614-5c91fe34-64b8-11e8-9af3-7785d28eb99e.png)

### 3-	Configurer le fichier pom.xml

Dans cet exemple, nous avons besoin d'une bibliothèque de convertir (convert) XML en objet  Java et vice versa. Et une autre bibliothèque de convertir  JSON en  Java et vice versa.

#### JSON <==> Java

spring-boot-starter-web a construit dans  jackson-databind, cette bibliothèque convertit  JSON en objet  Java et vice versa. 
  ```bash
  <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
```

![3](https://user-images.githubusercontent.com/28655112/40772685-9ebc471a-64b8-11e8-9692-ca0c9bf61081.png)
 
#### XML <==> Java

Spring Boot utilise  JAXB (Disponible dans  JDK) comme une bibliothèque par défaut pour convertir  XML et  Java. Pourtant, des classes de Java ont besoin d'être annotées par  @XmlRootElement,... On doit aussi utiliser jackson-dataformat-xml comme une biblothèque de convertir  XML et  Java et la déclarer dans le fichier  pom.xml:
```bash
<dependency>
        <groupId>com.fasterxml.jackson.dataformat</groupId>
        <artifactId>jackson-dataformat-xml</artifactId>
  </dependency>
 ```
### 4-	Code de l'application 

•	La "classe principale" nommée " SpringBootCrudRestfulApplication.java" permet l’exécution de l’application annotée par  @SpringBootApplication

•	La classe  Employee représente un employé.

•	La classe  EmployeeDAO est annotée par  @Repository afin de notifier le  Spring qu'elle est un  Spring BEAN. Cette classe comprend les méthodes qui aident à enquêter la liste des employés (employee), à créer des employés, mettre à jour de l'information des employés et à supprimer des employés.

#### Remarque :
```bash
produces={MediaType.APPLICATION_JSON_VALUE,MediaType.APPLICATION_XML_VALUE}
produces = { "application/json" , "application/xml" }
```
L'attribut  produces sert à spécifier un  URL qui créera seulement (renverra à l’utilisateur) les données sous quel format. Par exemple:  "application/json", "application/xml"

### 5-	Exécuter l'application

Après avoir exécuté l'application, on peut tester ses fonctionnements.

Dans le but d'extraire la liste des employés (employee), l'utilisateur doit envoyer une demande (requête) avec la méthode  GET. Vous pouvez tester facilement ce fonctionnement en utilisant un navigateur

•	http://localhost:8080/employees
 
 ![5](https://user-images.githubusercontent.com/28655112/40772821-f035742c-64b8-11e8-8c12-7a5b828ec13e.PNG)

•	http://localhost:8080/employee/E01
 
 ![6](https://user-images.githubusercontent.com/28655112/40772853-0a111ec8-64b9-11e8-84ab-f23084689bf3.png)

#### Test POST

Afin de créer un employé (employee), on a besoin d’une requête avec la méthode  POST, et de l'attacher les informations de l'employé qui a été créée. Les données attachées seront sous le format de  JSON ou celui de  XML :
 
 Créer un employé en Json
 
 ![7](https://user-images.githubusercontent.com/28655112/40772964-5c705346-64b9-11e8-9fa0-76c1027dd8d0.PNG)

 Créer un employé en XML
 
 ![8](https://user-images.githubusercontent.com/28655112/40772992-79376578-64b9-11e8-9a85-6999c2d4f7a6.PNG)


