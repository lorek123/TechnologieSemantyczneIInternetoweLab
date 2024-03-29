# Sprawozdanie - Laboratorium 1 Technologii Semantycznych i Internetowych 
## Artur Lorenz

1. Zawartość pliku:

```
@prefix : <http://www.semanticweb.org/myOntology#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@base <http://www.semanticweb.org/myOntology> .

:Mike a foaf:Person ;
		:livesIn :Poznan ; 
		:likes "X-Men_Movie"^^xsd:string .
		
:Michał :mieszkaW :Poznan .

:Michał :lubi :Kasia .

:Poznan :znajdujeSieW :Wielkopolska .
```

W Języku naturalnym zdania wyglądałyby w następujący sposób:
- Mike lives in Poznan and likes "X-Men_Movie".
- Michał mieszka w Poznaniu.
- Poznań znajduje się w Wielkopolsce.

Ponadto Mike nie został zdefiniowany jako Person. Ponadto Mike Lubi X-Men_Movie, a Michał lubi Kasię. Z wykorzystaniem Protege Stworzyłem ontologię:
```
@prefix : <http://www.semanticweb.org/myOntology#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix xml: <http://www.w3.org/XML/1998/namespace> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@base <http://www.w3.org/2002/07/owl#> .

[ rdf:type owl:Ontology
 ] .

#################################################################
#    Annotation properties
#################################################################

###  http://www.semanticweb.org/myOntology#likes
:likes rdf:type owl:AnnotationProperty .


###  http://www.semanticweb.org/myOntology#livesIn
:livesIn rdf:type owl:AnnotationProperty .


###  http://www.semanticweb.org/myOntology#lubi
:lubi rdf:type owl:AnnotationProperty .


###  http://www.semanticweb.org/myOntology#mieszkaW
:mieszkaW rdf:type owl:AnnotationProperty .


###  http://www.semanticweb.org/myOntology#znajdujeSieW
:znajdujeSieW rdf:type owl:AnnotationProperty .


#################################################################
#    Classes
#################################################################

###  http://xmlns.com/foaf/0.1/Person
foaf:Person rdf:type owl:Class .


#################################################################
#    Individuals
#################################################################

###  http://www.co-ode.org/ontologies/ont.owl#Kasia
<http://www.co-ode.org/ontologies/ont.owl#Kasia> rdf:type owl:NamedIndividual ,
                                                          foaf:Person .


###  http://www.co-ode.org/ontologies/ont.owl#Michał
<http://www.co-ode.org/ontologies/ont.owl#Michał> rdf:type owl:NamedIndividual ,
                                                           foaf:Person ;
                                                  owl:sameAs :Mike ;
                                                  :lubi <http://www.co-ode.org/ontologies/ont.owl#Kasia> ;
                                                  :mieszkaW <http://www.co-ode.org/ontologies/ont.owl#Poznan> .


###  http://www.co-ode.org/ontologies/ont.owl#Poznan
<http://www.co-ode.org/ontologies/ont.owl#Poznan> rdf:type owl:NamedIndividual ;
                                                  :znajdujeSieW <http://www.co-ode.org/ontologies/ont.owl#Wielkopolska> .


###  http://www.co-ode.org/ontologies/ont.owl#Wielkopolska
<http://www.co-ode.org/ontologies/ont.owl#Wielkopolska> rdf:type owl:NamedIndividual .


###  http://www.semanticweb.org/myOntology#Mike
:Mike rdf:type owl:NamedIndividual ,
               foaf:Person ;
      :likes "X-Men_Movie"^^xsd:string ;
      :livesIn :Poznan .


#################################################################
#    Annotations
#################################################################

:Michał :lubi :Kasia ;
        :mieszkaW :Poznan .

:Poznan :znajdujeSieW :Wielkopolska .


###  Generated by the OWL API (version 4.2.8.20170104-2310) https://github.com/owlcs/owlapi

``` 
Która opisuje odpowiednie zależności. Faktycznie brakującą mogło być `owl:sameAs :Mike ;`


2. Dodano informacje:

```
:ZamekCesarski :znajdujeSieW :Poznan ;
			:maLat :107 .
:uniwersystetXYZ :znajdujeSieW :Poznan .
:JanNowak a foaf:Person ;  
			:jestRektorem :uniwersystetXYZ .
:JanKowalski a foaf:Person ; 
			:jest :Profesor ;
			:wykładaNa :uniwersystetXYZ .

```

3.
- Zamek Cesarski ma swoją stronę internetową http://ckzamek.pl/. # nie znalazłem w przestrzeni FOAF ani DC sposobu na opisanie lokalizacji lub budynku

4. Nie udało mi się napisać wymienionych punktów ręcznie, na szczęście protege świetnie sobie dało radę. 

5. 
- Functional - Dla każdej wartości y jest tylko jedna wartość x. źródło: https://www.infowebml.ws/rdf-owl/FunctionalProperty.htm

- Symmetric - Dla każdej pary wartości (x,y) intancji obiektu istnieje (y,x)

- Dodałem wpisy o filmach, jednak nie udało mi się przenalizować wyników z zakładki DL Query, ponieważ nie udało mi się wykonać zapytania

6. Graf przedstawia bardzo skomplikowane zależności, mam wrażenie że ontologia nie została przeze mnie zbyt dobrze zaprojektowana. Strona pozwala na wygenerowania informacji o trójkach oraz grafu.

7. XML wykorzystuje tagi, przez co jest mniej czytelny dla człowieka. Turtle wykorzystuje składnię podobną do języka Prolog, jest nieco podobny do składni YAML.