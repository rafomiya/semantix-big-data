# Exercises - Aggregation I

1. Create the database `school`.

```javascript
use school
// output:
// switched to db school
```
2. Create the collection `students` on the database `school`.

```javascript
db.createCollection('students')
// output:
// { "ok": 1 }
```

3. Import the file `dataset/alunos.csv` to the collection `students`, with the following attributes:

- `id_discente`: Number
- `nome`: String
- `ano_ingresso`: Number
- `nivel`: String
- `id_curso`: Number

```javascript
// Made through MongoDB Compass
```

4. Visualize the unique values of `nivel` of each `ano_ingresso`.

```javascript
db.students.aggregate({
    $group: {
        _id: '$ano_ingresso',
        level_by_year: {
            $addToSet: '$nivel'
        }
    }
})
// output:
// { "_id" : "2010", "result" : [ "G", "T", "M" ] }
// { "_id" : "2013", "result" : [ "G", "T", "M" ] }
// { "_id" : "2017", "result" : [ "G", "N", "M", "T", "L", "E" ] }
// { "_id" : "2016", "result" : [ "G", "L", "T", "M" ] }
// { "_id" : "2015", "result" : [ "G", "T", "M" ] }
// { "_id" : "2008", "result" : [ "M" ] }
// { "_id" : "2012", "result" : [ "G", "T", "M" ] }
// { "_id" : "2019", "result" : [ "G", "N", "T", "L", "M" ] }
// { "_id" : "2014", "result" : [ "G", "M", "T" ] }
// { "_id" : "2011", "result" : [ "G", "M", "T" ] }
// { "_id" : "2018", "result" : [ "N", "G", "T", "L", "E", "M" ] }
```

5. Calculate the amount of `students` registered for each `id_curso`.

```javascript
db.students.aggregate({
    $group: {
        _id: '$id_curso',
        amount_by_course: {
            $sum: 1
        }
    }
})
// output:
// { "_id" : "67444", "amount_by_course" : 110 }
// { "_id" : "78384", "amount_by_course" : 55 }
// { "_id" : "1222", "amount_by_course" : 28 }
// { "_id" : "2399330", "amount_by_course" : 49 }
// { "_id" : "3676346", "amount_by_course" : 24 }
// { "_id" : "2399358", "amount_by_course" : 55 }
// { "_id" : "76320", "amount_by_course" : 38 }
// { "_id" : "39", "amount_by_course" : 193 }
// { "_id" : "2080", "amount_by_course" : 27 }
// { "_id" : "7478", "amount_by_course" : 49 }
// { "_id" : "69341", "amount_by_course" : 63 }
// { "_id" : "485725", "amount_by_course" : 20 }
// { "_id" : "2399331", "amount_by_course" : 49 }
// { "_id" : "2362295", "amount_by_course" : 16 }
// { "_id" : "1435399", "amount_by_course" : 23 }
// { "_id" : "35662", "amount_by_course" : 73 }
// { "_id" : "2372100", "amount_by_course" : 31 }
// { "_id" : "298256", "amount_by_course" : 51 }
// { "_id" : "2627321", "amount_by_course" : 13 }
// { "_id" : "1444206", "amount_by_course" : 17 }
// Type "it" for more
```

6. Calcular a quantidade de `students` registered for each `ano_ingresso` on `id_curso: 1222`.

```javascript
db.students.aggregate([
    { $match: { id_curso: 1222 } },
    {
        $group: {
            _id: '$ano_ingresso',
            amount_students: {
                $sum: 1
            }
        }
    }
])
// output:
// { "_id" : "2017", "amount_students" : 22 }
// { "_id" : "2016", "amount_students" : 4 }
// { "_id" : "2014", "amount_students" : 2 }
```

7. Visualize all the documents where `nível` equals to `'M'`.

```javascript
db.students.find({ nivel: 'M' })
// output:
// { "_id" : ObjectId("621fa282549c549f9b094fdd"), "id_discente" : "553", "nome" : "ABIEL GODOY MARIANO", "ano_ingresso" : "2015", "nivel" : "M", "id_curso" : "3402" }
// { "_id" : ObjectId("621fa282549c549f9b094fdf"), "id_discente" : "16613", "nome" : "ABIGAIL FERNANDA MALHEIROS BRASIL", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "1222" }
// { "_id" : ObjectId("621fa282549c549f9b094fe0"), "id_discente" : "17398", "nome" : "ABIGAIL JOSIANE RIL ROCHA", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "5041" }
// { "_id" : ObjectId("621fa282549c549f9b094ff5"), "id_discente" : "12236", "nome" : "ADEMIR MOREIRA CARVALHO", "ano_ingresso" : "2016", "nivel" : "M", "id_curso" : "5738" }
// { "_id" : ObjectId("621fa282549c549f9b094fff"), "id_discente" : "16277", "nome" : "ADLEY JOSÉ BATISTA FERNANDES", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "475930" }
// { "_id" : ObjectId("621fa282549c549f9b095000"), "id_discente" : "12141", "nome" : "ADREAN BRUM RODRIGUES", "ano_ingresso" : "2016", "nivel" : "M", "id_curso" : "3402" }
// { "_id" : ObjectId("621fa282549c549f9b09500e"), "id_discente" : "19315", "nome" : "ADRIANA FERREIRA BIQUE", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "6218" }
// { "_id" : ObjectId("621fa282549c549f9b09500f"), "id_discente" : "16096", "nome" : "ADRIANA FOSS", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "1108" }
// { "_id" : ObjectId("621fa282549c549f9b095017"), "id_discente" : "13453", "nome" : "ADRIANA OLIVEIRA DA ROSA", "ano_ingresso" : "2016", "nivel" : "M", "id_curso" : "12341" }
// { "_id" : ObjectId("621fa282549c549f9b095025"), "id_discente" : "15863", "nome" : "ADRIAN DANIEL KRALIK DA SILVA", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "5143" }
// { "_id" : ObjectId("621fa282549c549f9b095032"), "id_discente" : "19943", "nome" : "ADRIANE SPITZMACHER CORDEIRO", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "3763" }
// { "_id" : ObjectId("621fa282549c549f9b09503a"), "id_discente" : "9406", "nome" : "ADRIANO BREMM FENRDERIK", "ano_ingresso" : "2013", "nivel" : "M", "id_curso" : "5041" }
// { "_id" : ObjectId("621fa282549c549f9b095042"), "id_discente" : "16163", "nome" : "ADRIANO EUZÉBIO", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "3908" }
// { "_id" : ObjectId("621fa282549c549f9b095048"), "id_discente" : "15600", "nome" : "ADRIANO WLOSIUK LAGAGGIO", "ano_ingresso" : "2016", "nivel" : "M", "id_curso" : "5041" }
// { "_id" : ObjectId("621fa282549c549f9b095049"), "id_discente" : "15939", "nome" : "ADRIEL BATISTA DE OLIVEIRA", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "3669" }
// { "_id" : ObjectId("621fa282549c549f9b09504a"), "id_discente" : "16254", "nome" : "ADRIELE ELENICE MENEZES PETINI", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "3208" }
// { "_id" : ObjectId("621fa282549c549f9b09504c"), "id_discente" : "16314", "nome" : "ADRIELE POCHE GIACOMELLI", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "3208" }
// { "_id" : ObjectId("621fa282549c549f9b095052"), "id_discente" : "1969", "nome" : "AFFONSO HENRIQUE SOARES PAZDZIORA", "ano_ingresso" : "2014", "nivel" : "M", "id_curso" : "1108" }
// { "_id" : ObjectId("621fa282549c549f9b095053"), "id_discente" : "16860", "nome" : "AFONSO SEVERO TOALDO", "ano_ingresso" : "2017", "nivel" : "M", "id_curso" : "3402" }
// { "_id" : ObjectId("621fa282549c549f9b095067"), "id_discente" : "1717", "nome" : "ALANA AQUINO DA SILVA", "ano_ingresso" : "2013", "nivel" : "M", "id_curso" : "11442" }
// Type "it" for more
```

8. Visualize the last year of each `id_curso` of level `'M'`

```javascript
db.students.aggregate([
    { $match: { nivel: 'M' } },
    {
        $group: {
            _id: '$id_curso',
            last_year: {
                $max: '$ano_ingresso'
            }
        }
    }
])
// output:
// { "_id" : 2080, "last_year" : 2017 }
// { "_id" : 5321, "last_year" : 2017 }
// { "_id" : 4508, "last_year" : 2017 }
// { "_id" : 1845, "last_year" : 2017 }
// { "_id" : 3763, "last_year" : 2017 }
// { "_id" : 6218, "last_year" : 2017 }
// { "_id" : 1846, "last_year" : 2017 }
// { "_id" : 11443, "last_year" : 2017 }
// { "_id" : 93490, "last_year" : 2013 }
// { "_id" : 5738, "last_year" : 2017 }
// { "_id" : 35662, "last_year" : 2017 }
// { "_id" : 12341, "last_year" : 2017 }
// { "_id" : 7479, "last_year" : 2015 }
// { "_id" : 7480, "last_year" : 2017 }
// { "_id" : 11442, "last_year" : 2017 }
// { "_id" : 1222, "last_year" : 2017 }
// { "_id" : 3208, "last_year" : 2017 }
// { "_id" : 3908, "last_year" : 2018 }
// { "_id" : 5244, "last_year" : 2016 }
// { "_id" : 5041, "last_year" : 2018 }
// Type "it" for more
```

9. Visualize the last year of each `id_curso` of level `'M'`, sorted by the most recent years of each course.

```javascript
db.students.aggregate([
    { $match: { nivel: 'M' } },
    {
        $group: {
            _id: '$id_curso',
            last_year: {
                $max: '$ano_ingresso'
            }
        }
    },
    { $sort: { last_year: -1 } }
])
// output:
// { "_id" : 3402, "last_year" : 2019 }
// { "_id" : 3908, "last_year" : 2018 }
// { "_id" : 5041, "last_year" : 2018 }
// { "_id" : 7476, "last_year" : 2018 }
// { "_id" : 2080, "last_year" : 2017 }
// { "_id" : 5321, "last_year" : 2017 }
// { "_id" : 4508, "last_year" : 2017 }
// { "_id" : 1845, "last_year" : 2017 }
// { "_id" : 3763, "last_year" : 2017 }
// { "_id" : 6218, "last_year" : 2017 }
// { "_id" : 1846, "last_year" : 2017 }
// { "_id" : 11443, "last_year" : 2017 }
// { "_id" : 5738, "last_year" : 2017 }
// { "_id" : 35662, "last_year" : 2017 }
// { "_id" : 12341, "last_year" : 2017 }
// { "_id" : 7480, "last_year" : 2017 }
// { "_id" : 11442, "last_year" : 2017 }
// { "_id" : 1222, "last_year" : 2017 }
// { "_id" : 3208, "last_year" : 2017 }
// { "_id" : 3669, "last_year" : 2017 }
// Type "it" for more
```

10. Visualize the last year that had the last 5 courses (`id_curso`) of level `'M'`, sorted by more recent years.

```javascript
db.students.aggregate([
    { $match: { nivel: 'M' } },
    {
        $group: {
            _id: '$id_curso',
            last_year: {
                $max: '$ano_ingresso'
            }
        }
    },
    { $sort: { last_year: 1 } },
    { $limit: 5 }
])
// output:
// { "_id" : 93490, "last_year" : 2013 }
// { "_id" : 4282, "last_year" : 2015 }
// { "_id" : 7479, "last_year" : 2015 }
// { "_id" : 5244, "last_year" : 2016 }
// { "_id" : 1845, "last_year" : 2017 }
```
