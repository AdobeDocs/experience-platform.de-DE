---
keywords: Experience Platform;Startseite;beliebte Themen;etl;ETL;etl-Transformationen;ETL-Transformationen
solution: Experience Platform
title: Beispiel-ETL-Transformationen
description: Dieser Artikel zeigt die folgenden Beispiel-Transformationen, auf die ein Extrakt-, Transform-, Load-(ETL-)Entwickler stoßen kann.
exl-id: 8084f5fd-b621-4515-a329-5a06c137d11c
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 88%

---

# Beispiel-ETL-Transformationen

Dieser Artikel zeigt die folgenden Beispiel-Transformationen, auf die ein Extrakt-, Transform-, Load-(ETL-)Entwickler stoßen kann.

## Einfache CSV in Hierarchie

### Beispieldateien

CSV- und JSON-Beispieldateien sind im öffentlichen ETL-Referenz- [!DNL GitHub] -Repository verfügbar, das von Adobe verwaltet wird:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)

### Beispiel-CSV

Die folgenden CRM-Daten wurden als `CRM_profiles.csv` exportiert:

```shell
TITLE   F_NAME  L_NAME  GENDER  DOB EMAIL   CRMID   ECID    LOYALTYID   ECID2   PHONE   STREET  CITY    STATE   COUNTRY ZIP LAT LONG
Mr  Ewart   Bennedsen   M   2004-09-25  ebennedsenex@jiathis.com    71a16013-d805-7ece-9ac4-8f2cd66e8eaa    87098882279810196101440938110216748923  2e33192000007456-0365c00000000000   55019962992006103186215643814973128178  256-284-7231    72 Buhler Crossing  Anniston    Alabama US  36205   33.708276   -85.7922905
Dr  Novelia Ansteys F   1987-10-31  nansteysdk@spotify.com  2eeb6532-82e1-0d58-8955-bf97de66a6f5    50829196174854544323574004005273946998  2e3319208000765b-3811c00000000001   65233136134594262632703695260919939885  704-181-6371    79 Northfield Hill  Charlotte   North Carolina  US  28299   35.2188655  -80.8108885
Mr  Ulises  Mochan  M   1996-03-20  umochanco@gnu.org   6f393075-addb-bdd6-73f8-31c393b700f5    70086119428645095847094710218289660855  2e33192080003023-26b2000000000002   82011353387947708954389153068944017636  720-837-4159    00671 Mifflin Trail Lacolle Qu√&copy;bec CA  E5A 45.08338    -73.36585
Mrs Friederike  Durrell F   1979-01-3   fdurrellbj@utexas.edu   33d018ec-5fed-f1a3-56aa-079370a9511b    50164729868919217963697788808932473456  2e33192080006dfc-0cdf400000000003   64452712468609735658703639722261004071  798-528-3458    47 Fremont Hill Independencia   Veracruz Llave  MX  91891   19.3803931  -99.1476905
Rev Evita   Bingall F   1974-02-28  ebingallod@mac.com  8c93db88-f328-8efb-dc73-d5654d371cbe    74973364195185450328832136951985519627  2e331920800038db-0559e00000000004   58945501950285346322834356669253860483  397-178-5897    56 Crescent Oaks Court  Buenavista  Oaxaca  MX  71730   19.4458447  -99.1497665
Mr  Eugenie Bechley F   1969-05-19  ebechley9r@telegraph.co.uk  b0c76a3f-6526-0ad0-e050-48143b687d18    67119779213799783658184754966135750376  2e331920800001a4-24b2800000000005   59715249079109455676103900762283358508  718-374-7456    5760 Southridge Junction    Staten Island   New York    US  10310   40.6307451  -74.1181235
Dr  Cammi   Haslen  F   1973-12-17  chaslenqv@ehow.com  56059cd5-5006-ce5f-2f5f-15b4d856a204    61747117963243728095047674165570746095  2e33192080007c25-2ec0600000000006   86268258269066295956223980330791223320  865-538-8291    83 Veith Street Knoxville   Tennessee   US  37995   35.95   -84.05
```

### Zuordnung

Die Zuordnungsanforderungen für die CRM-Daten sind in der folgenden Tabelle aufgeführt und umfassen die folgenden Transformationen:
- Identitätsspalten in `identityMap`-Eigenschaften
- Geburtsdatum in Jahr und Monat
- Zeichenfolgen in Dubletten oder kurzen Ganzzahlen.

| CSV-Spalte | XDM-Pfad | Datenformatierung |
| ---------- | -------- | --------------- |
| TITEL | person.name.courtesyTitle | Als Zeichenfolge kopieren |
| F_NAME | person.name.firstName | Als Zeichenfolge kopieren |
| L_NAME | person.name.lastName | Als Zeichenfolge kopieren |
| GESCHLECHT | person.gender | Geschlecht als entsprechenden „person.gender-enum“-Wert transformieren |
| GEBURTSDATUM | person.birthDayAndMonth: &quot;MM-DD&quot;<br/>person.birthDate: &quot;YYYY-MM-DD&quot;<br/>person.birthYear: YYYY | birthDayAndMonth als Zeichenfolge transformieren<br/>birthDate als Zeichenfolge transformieren<br/>birthyear als “short intr”-Wert transformieren |
| E-MAIL | personalEmail.address | Als Zeichenfolge kopieren |
| CRMID | identityMap.CRMID[{&quot;id&quot;:x, primary:false}] | Kopieren Sie dies als Zeichenfolge in das CRMID-Array in „identityMap“ und setzen Sie „Primary as false“ |
| ECID | identityMap.ECID[{&quot;id&quot;:x, primary: false}] | Kopieren Sie dies als Zeichenfolge in den ersten Eintrag im ECID-Array in „identityMap“ und setzen Sie „Primary as false“ |
| LOYALTYID | identityMap.LOYALTYID[{&quot;id&quot;:x, primary:true}] | Kopieren Sie dies als Zeichenfolge in das LOYALTYID-Array in „identityMap“ und setzen Sie „Primary as true“ |
| ECID2 | identityMap.ECID[{&quot;id&quot;:x, primary:false}] | Kopieren Sie dies als Zeichenfolge in den zweiten Eintrag im ECID-Array in „identityMap“ und setzen Sie „Primary as false“ |
| TELEFON | homePhone.number | Als Zeichenfolge kopieren |
| STRASSE | homeAddress.street1 | Als Zeichenfolge kopieren |
| STADT | homeAddress.city | Als Zeichenfolge kopieren |
| BUNDESLAND | homeAddress.stateProvince | Als Zeichenfolge kopieren |
| LAND | homeAddress.country | Als Zeichenfolge kopieren |
| ZIP CODE | homeAddress.postalCode | Als Zeichenfolge kopieren |
| BREITENGRAD | homeAddress.latitude | In double-Wert konvertieren |
| LÄNGENGRAD | homeAddress.longitude | In double-Wert konvertieren |


### Ausgabe in XDM

Das folgende Beispiel zeigt die ersten beiden Zeilen des CSV, das in XDM umgewandelt wurde, wie in `CRM_profiles.json` dargestellt:

```json
{
   "person": {
      "name": {
         "courtesyTitle": "Mr",
         "firstName": "Ewart",
         "lastName": "Bennedsen"
      },
      "gender": "male",
      "birthDayAndMonth": "09-25",
      "birthDate": "2004-09-25",
      "birthYear": 2004
   },
   "identityMap": {
      "CRMID": [{
         "id": "71a16013-d805-7ece-9ac4-8f2cd66e8eaa",
         "primary": false
      }],
      "ECID": [{
         "id": "87098882279810196101440938110216748923",
         "primary": false
      },
      {
         "id": "55019962992006103186215643814973128178",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e33192000007456-0365c00000000000",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "256-284-7231"
   },
   "personalEmail": {
      "address": "ebennedsenex@jiathis.com"
   },
   "homeAddress": {
      "street1": "72 Buhler Crossing",
      "city": "Anniston",
      "stateProvince": "Alabama",
      "country": "US",
      "postalCode": "36205",
      "_schema": {
         "latitude": 33.708276,
         "longitude": -85.7922905
      }
   }
},{
   "person": {
      "name": {
         "courtesyTitle": "Dr",
         "firstName": "Novelia",
         "lastName": "Ansteys"
      },
      "gender": "female",
      "birthDayAndMonth": "10-31",
      "birthDate": "1987-10-31",
      "birthYear": 1987
   },
   "identityMap": {
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
         "primary": false
      }],
      "ECID": [{
         "id": "50829196174854544323574004005273946998",
         "primary": false
      },
      {
         "id": "65233136134594262632703695260919939885",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "704-181-6371"
   },
   "personalEmail": {
      "address": "nansteysdk@spotify.com"
   },
   "homeAddress": {
      "street1": "79 Northfield Hill",
      "city": "Charlotte",
      "stateProvince": "North Carolina",
      "country": "US",
      "postalCode": "28299",
      "_schema": {
         "latitude": 35.2188655,
         "longitude": -80.8108888
      }
   }
}
```

## Dataframe in XDM-Schema

Die Hierarchie eines Dataframes (z. B. einer Parquet-Datei) muss mit der des XDM-Schemas übereinstimmen, in das hochgeladen wird.

### Beispiel-Dataframe

Die Struktur des folgenden Beispiel-Datenrahmens wurde einem Schema zugeordnet, das die [!DNL XDM Individual Profile]-Klasse implementiert und die häufigsten Felder enthält, die mit Schemata dieses Typs verknüpft sind.

```python
[
    StructField("person", StructType(
        [
            StructField("name", StructType(
                [
                    StructField("courtesyTitle", StringType()),
                    StructField("firstName", StringType()),
                    StructField("lastName", StringType())
                ]
            )),
            StructField("gender", StringType()),
            StructField("birthDayAndMonth", StringType()),
            StructField("birthDate", StringType()),
            StructField("birthYear", LongType())
        ]
    )),
    StructField("identityMap", MapType(
        StructField("CRMID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("ECID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("LOYALTYID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        ))
    )),
    StructField("homePhone", StructType(
        [
            StructField("number", StringType())
        ]
    )),
    StructField("personalEmail", StructType(
        [
            StructField("address", StringType())
        ]
    )),
    StructField("homeAddress", StructType(
        [
            StructField("street1", StringType()),
            StructField("city", StringType()),
            StructField("stateProvince", StringType()),
            StructField("country", StringType()),
            StructField("postalCode", StringType()),
            StructField("_schema", StructType(
                [
                    StructField("latitude", DoubleType()),
                    StructField("latitude", DoubleType()),
                ]
            ))
        ]
    ))    
]
```

Beim Erstellen eines Dataframes zur Verwendung in Adobe Experience Platform muss sichergestellt werden, dass seine hierarchische Struktur exakt mit der eines vorhandenen XDM-Schemas übereinstimmt, damit die Felder korrekt zugeordnet werden können.

## Identitäten zur Identitätszuordnung

### Array von Identitäten

```json
[
  {
    "xdm:id": "someone1@example.com",
    "xdm:namespace": {
      "xdm:code": "Email"
    }
  },
  {
    "xdm:id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
    "xdm:namespace": {
      "xdm:code": "CRMID"
    }
  },
  {
    "xdm:id": "2e3319208000765b-3811c00000000001",
    "xdm:namespace": {
      "xdm:code": "LOYALTYID"
    }
  }
]
```

### Zuordnung

Die Zuordnungsanforderungen für das Array von Identitäten sind in der folgenden Tabelle aufgeführt:

| Identitätsfeld | identityMap-Feld | Datentyp |
| -------------- | ----------------- | --------- |
| identities[0].id | identityMap[Email][{"id"}] | Als Zeichenfolge kopieren |
| identities[1].id | identityMap[CRMID][{"id"}] | Als Zeichenfolge kopieren |
| identities[2].id | identityMap[LOYALTYID][{"id"}] | Als Zeichenfolge kopieren |

### Ausgabe in XDM

Im Folgenden finden Sie das Array der Identitäten, die in XDM umgewandelt werden:

```JSON
"identityMap": {
      "Email": [{
         "id": "someone1@example.com"
      }],
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5"
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001"
      }]
   }
```
