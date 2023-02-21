# Exercises - Aggregation II

1. Create the collection `courses` on the database `school`.

```javascript
use school
// output:
// switched to db school
db.createCollection('courses')
// output:
// { "ok": 1 }
```

2. Import the file `cursos.csv` to the collection `courses`, with the following attributes:
- id_curso: Number
- id_unidade: Number
- nome: String
- nivel: String

```javascript
// Made through MongoDB Compass
```

3. Perform the left outer join of the collection `students` and `courses`, when the `id_curso` from both collections is the same.

```javascript
db.students.aggregate({
    $lookup: {
        from: 'courses',
        localField: 'id_curso',
        foreignField: 'id_curso',
        as: 'student_courses'
    }
})
// output:
// { "_id" : ObjectId("621fa6fb549c549f9b0976ee"), "id_discente" : 18957, "nome" : "ABELARDO DA SILVA COELHO", "ano_ingresso" : 2017, "nivel" : "G", "id_curso" : 76995, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e93"), "id_curso" : 76995, "id_unidade" : 194, "nome" : "LICENCIATURA EM CIÊNCIAS BIOLÓGIAS", "nivel" : "G" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976ef"), "id_discente" : 553, "nome" : "ABIEL GODOY MARIANO", "ano_ingresso" : 2015, "nivel" : "M", "id_curso" : 3402, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e7d"), "id_curso" : 3402, "id_unidade" : 150, "nome" : "TÉCNICO EM AGROPECUÁRIA INTEGRADO", "nivel" : "M" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f0"), "id_discente" : 17977, "nome" : "ABIGAIL ANTUNES SALERNO FAN", "ano_ingresso" : 2017, "nivel" : "T", "id_curso" : 759711, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e12"), "id_curso" : 759711, "id_unidade" : 696, "nome" : "TÉCNICO EM ADMINISTRAÇÃO", "nivel" : "T" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f1"), "id_discente" : 16613, "nome" : "ABIGAIL FERNANDA MALHEIROS BRASIL", "ano_ingresso" : 2017, "nivel" : "M", "id_curso" : 1222, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099ea5"), "id_curso" : 1222, "id_unidade" : 349, "nome" : "TÉCNICO EM QUÍMICA INTEGRADO AO ENSINO MÉDIO-PB", "nivel" : "M" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f2"), "id_discente" : 17398, "nome" : "ABIGAIL JOSIANE RIL ROCHA", "ano_ingresso" : 2017, "nivel" : "M", "id_curso" : 5041, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e1c"), "id_curso" : 5041, "id_unidade" : 189, "nome" : "TÉCNICO EM AGROPECUÁRIA INTEGRADO - AL", "nivel" : "M" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f3"), "id_discente" : 26880, "nome" : "ABIMAEL CHRISTOPFER WESCHENFELDER", "ano_ingresso" : 2019, "nivel" : "T", "id_curso" : 1913420, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e35"), "id_curso" : 1913420, "id_unidade" : 269, "nome" : "TÉCNICO EM ADMINISTRAÇÃO EAD - SR", "nivel" : "T" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f4"), "id_discente" : 28508, "nome" : "ABNER NUNES PERES", "ano_ingresso" : 2019, "nivel" : "G", "id_curso" : 181097, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e79"), "id_curso" : 181097, "id_unidade" : 434, "nome" : "BACHARELADO EM ADMINISTRAÇÃO", "nivel" : "G" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f5"), "id_discente" : 18693, "nome" : "ACSA PEREIRA RODRIGUES", "ano_ingresso" : 2017, "nivel" : "G", "id_curso" : 77498, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099ea6"), "id_curso" : 77498, "id_unidade" : 155, "nome" : "LICENCIATURA EM CIÊNCIAS BIOLÓGICAS", "nivel" : "G" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f6"), "id_discente" : 28071, "nome" : "ACSA ROBALO DOS SANTOS", "ano_ingresso" : 2019, "nivel" : "T", "id_curso" : 3996007, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e0f"), "id_curso" : 3996007, "id_unidade" : 229, "nome" : "TÉCNICO EM LOGÍSTICA - SB", "nivel" : "T" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f7"), "id_discente" : 21968, "nome" : "AÇUCENA CARVALHO NUNES", "ano_ingresso" : 2018, "nivel" : "N", "id_curso" : 2399357, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099ee7"), "id_curso" : 2399357, "id_unidade" : 428, "nome" : "TÉCNICO EM COMÉRCIO - PROEJA", "nivel" : "N" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f8"), "id_discente" : 22374, "nome" : "ADALBERTO LUFT LUNARDI", "ano_ingresso" : 2018, "nivel" : "N", "id_curso" : 2399354, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099eb5"), "id_curso" : 2399354, "id_unidade" : 229, "nome" : "TÉCNICO EM INFORMÁTICA - SB", "nivel" : "N" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976f9"), "id_discente" : 26367, "nome" : "ADALBERTO SEIDEL CONY", "ano_ingresso" : 2019, "nivel" : "G", "id_curso" : 79131, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099ed4"), "id_curso" : 79131, "id_unidade" : 156, "nome" : "TECNOLOGIA EM GESTÃO PÚBLICA", "nivel" : "G" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976fa"), "id_discente" : 4392, "nome" : "ADALGIZA OLIVEIRA RATTES", "ano_ingresso" : 2013, "nivel" : "T", "id_curso" : 34, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e03"), "id_curso" : 34, "id_unidade" : 229, "nome" : "TÉCNICO EM NUTRIÇAO - SB", "nivel" : "T" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976fb"), "id_discente" : 4573, "nome" : "ADANA BIANCA DOS SANTOS", "ano_ingresso" : 2012, "nivel" : "T", "id_curso" : 39, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e26"), "id_curso" : 39, "id_unidade" : 229, "nome" : "TÉCNICO EM INFORMÁTICA PARA INTERNET - SB", "nivel" : "T" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976fc"), "id_discente" : 16219, "nome" : "ADÃO ANTÔNIO PILLAR DAMASCENO", "ano_ingresso" : 2016, "nivel" : "L", "id_curso" : 1444206, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099ede"), "id_curso" : 1444206, "id_unidade" : 402, "nome" : "ESPECIALIZAÇÃO EM EDUCAÇÃO DO CAMPO E AGROECOLOGIA (TURMA 2016)", "nivel" : "L" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976fd"), "id_discente" : 25120, "nome" : "ADÃO VAGNER DOS SANTOS MOTA", "ano_ingresso" : 2018, "nivel" : "G", "id_curso" : 283646, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e9c"), "id_curso" : 283646, "id_unidade" : 195, "nome" : "TECNOLOGIA EM PRODUÇÃO DE GRÃOS", "nivel" : "G" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976fe"), "id_discente" : 19638, "nome" : "ADELAR DE MELLO", "ano_ingresso" : 2017, "nivel" : "G", "id_curso" : 65489, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099eb8"), "id_curso" : 65489, "id_unidade" : 474, "nome" : "SUPERIOR DE TECNOLOGIA EM SISTEMAS PARA INTERNET", "nivel" : "G" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b0976ff"), "id_discente" : 13232, "nome" : "ADELAR SANTOS DAS DORES", "ano_ingresso" : 2016, "nivel" : "T", "id_curso" : 2057, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e70"), "id_curso" : 2057, "id_unidade" : 468, "nome" : "TÉCNICO EM INFORMÁTICA PARA INTERNET - SAN", "nivel" : "T" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b097700"), "id_discente" : 10071, "nome" : "ADELI CRISTIANO WEIZEMANN KLOCKNER", "ano_ingresso" : 2012, "nivel" : "G", "id_curso" : 182354, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099ec4"), "id_curso" : 182354, "id_unidade" : 234, "nome" : "LICENCIATURA EM FÍSICA-SB", "nivel" : "G" } ] }
// { "_id" : ObjectId("621fa6fb549c549f9b097701"), "id_discente" : 24787, "nome" : "ADELITA ALVES SILVEIRA", "ano_ingresso" : 2018, "nivel" : "T", "id_curso" : 31, "student_courses" : [ { "_id" : ObjectId("621fac2d549c549f9b099e2c"), "id_curso" : 31, "id_unidade" : 229, "nome" : "TÉCNICO EM COZINHA - SB", "nivel" : "T" } ] }
// Type "it" for more
```

4. Perform the left outer join of the collection `students` and `courses`, when the `id_curso` from both collections is the same. Visualize only the following fields:
- `students`: `id_discente`, `nivel`
- `courses`: `id_curso`, `id_unidade`, `nome`

```javascript
db.students.aggregate([
    {
        $lookup: {
            from: 'courses',
            localField: 'id_curso',
            foreignField: 'id_curso',
            as: 'student_courses'
        }
    },
    {
        $project: {
            _id: 0,
            id_discente: 1,
            nivel: 1,
            'student_courses.id_curso': 1,
            'student_courses.id_unidade': 1,
            'student_courses.nome': 1
        }
    }
])
// output:
// { "id_discente" : 18957, "nivel" : "G", "student_courses" : [ { "id_curso" : 76995, "id_unidade" : 194, "nome" : "LICENCIATURA EM CIÊNCIAS BIOLÓGIAS" } ] }
// { "id_discente" : 553, "nivel" : "M", "student_courses" : [ { "id_curso" : 3402, "id_unidade" : 150, "nome" : "TÉCNICO EM AGROPECUÁRIA INTEGRADO" } ] }
// { "id_discente" : 17977, "nivel" : "T", "student_courses" : [ { "id_curso" : 759711, "id_unidade" : 696, "nome" : "TÉCNICO EM ADMINISTRAÇÃO" } ] }
// { "id_discente" : 16613, "nivel" : "M", "student_courses" : [ { "id_curso" : 1222, "id_unidade" : 349, "nome" : "TÉCNICO EM QUÍMICA INTEGRADO AO ENSINO MÉDIO-PB" } ] }
// { "id_discente" : 17398, "nivel" : "M", "student_courses" : [ { "id_curso" : 5041, "id_unidade" : 189, "nome" : "TÉCNICO EM AGROPECUÁRIA INTEGRADO - AL" } ] }
// { "id_discente" : 26880, "nivel" : "T", "student_courses" : [ { "id_curso" : 1913420, "id_unidade" : 269, "nome" : "TÉCNICO EM ADMINISTRAÇÃO EAD - SR" } ] }
// { "id_discente" : 28508, "nivel" : "G", "student_courses" : [ { "id_curso" : 181097, "id_unidade" : 434, "nome" : "BACHARELADO EM ADMINISTRAÇÃO" } ] }
// { "id_discente" : 18693, "nivel" : "G", "student_courses" : [ { "id_curso" : 77498, "id_unidade" : 155, "nome" : "LICENCIATURA EM CIÊNCIAS BIOLÓGICAS" } ] }
// { "id_discente" : 28071, "nivel" : "T", "student_courses" : [ { "id_curso" : 3996007, "id_unidade" : 229, "nome" : "TÉCNICO EM LOGÍSTICA - SB" } ] }
// { "id_discente" : 21968, "nivel" : "N", "student_courses" : [ { "id_curso" : 2399357, "id_unidade" : 428, "nome" : "TÉCNICO EM COMÉRCIO - PROEJA" } ] }
// { "id_discente" : 22374, "nivel" : "N", "student_courses" : [ { "id_curso" : 2399354, "id_unidade" : 229, "nome" : "TÉCNICO EM INFORMÁTICA - SB" } ] }
// { "id_discente" : 26367, "nivel" : "G", "student_courses" : [ { "id_curso" : 79131, "id_unidade" : 156, "nome" : "TECNOLOGIA EM GESTÃO PÚBLICA" } ] }
// { "id_discente" : 4392, "nivel" : "T", "student_courses" : [ { "id_curso" : 34, "id_unidade" : 229, "nome" : "TÉCNICO EM NUTRIÇAO - SB" } ] }
// { "id_discente" : 4573, "nivel" : "T", "student_courses" : [ { "id_curso" : 39, "id_unidade" : 229, "nome" : "TÉCNICO EM INFORMÁTICA PARA INTERNET - SB" } ] }
// { "id_discente" : 16219, "nivel" : "L", "student_courses" : [ { "id_curso" : 1444206, "id_unidade" : 402, "nome" : "ESPECIALIZAÇÃO EM EDUCAÇÃO DO CAMPO E AGROECOLOGIA (TURMA 2016)" } ] }
// { "id_discente" : 25120, "nivel" : "G", "student_courses" : [ { "id_curso" : 283646, "id_unidade" : 195, "nome" : "TECNOLOGIA EM PRODUÇÃO DE GRÃOS" } ] }
// { "id_discente" : 19638, "nivel" : "G", "student_courses" : [ { "id_curso" : 65489, "id_unidade" : 474, "nome" : "SUPERIOR DE TECNOLOGIA EM SISTEMAS PARA INTERNET" } ] }
// { "id_discente" : 13232, "nivel" : "T", "student_courses" : [ { "id_curso" : 2057, "id_unidade" : 468, "nome" : "TÉCNICO EM INFORMÁTICA PARA INTERNET - SAN" } ] }
// { "id_discente" : 10071, "nivel" : "G", "student_courses" : [ { "id_curso" : 182354, "id_unidade" : 234, "nome" : "LICENCIATURA EM FÍSICA-SB" } ] }
// { "id_discente" : 24787, "nivel" : "T", "student_courses" : [ { "id_curso" : 31, "id_unidade" : 229, "nome" : "TÉCNICO EM COZINHA - SB" } ] }
// Type "it" for more
```
