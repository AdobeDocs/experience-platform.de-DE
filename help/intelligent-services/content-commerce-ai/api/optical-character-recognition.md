---
keywords: OCR;Textpräsenz;optische Zeichenerkennung
solution: Experience Platform
title: Textpräsenz- und optische Zeichenerkennung
description: In der Content-Tagging-API kann der Service für Textpräsenz-/optische Zeichenerkennung (OCR) anzeigen, ob Text in einem bestimmten Bild vorhanden ist. Wenn Text vorhanden ist, kann OCR den Text zurückgeben.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 82722ddf7ff543361177b555fffea730a7879886
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 4%

---

# Textpräsenz- und optische Zeichenerkennung

Der Service „Textpräsenz-/Optische Zeichenerkennung (OCR)“ kann bei einem gegebenen Bild anzeigen, ob Text im Bild vorhanden ist. Wenn Text vorhanden ist, kann OCR den Text zurückgeben.

Die folgende Abbildung wurde in der in diesem Dokument gezeigten Beispielanfrage verwendet:

![Beispielbild](../images/sample_image.png)

**API-Format**

```http
POST /services/v2/predict
```

**Anfrage**

Die folgende Anfrage prüft anhand des in der Payload bereitgestellten Eingabebilds, ob Text vorhanden ist. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

Ausführung mit Inline-Bild:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der Text zurückgegeben, der in der `tags` für jedes Bild erkannt wurde, das in der Anfrage übergeben wurde. Wenn ein bestimmtes Bild keinen Text enthält, ist `is_text_present` 0 und `tags` ist eine leere Liste.

[result0, result1, …]: Liste der Antworten für jedes Eingabedokument. Jedes Ergebnis ist ein dict mit Schlüsseln:

1. REQUEST_ELEMENT_ID: Entsprechender Index der Eingabedatei für diese Antwort, 0 für das erste Bild in der Dokumentliste der Anfrage, 1 für das nächste usw.
2. Tags: Liste der Wörterbücher Jedes Wörterbuch hat zwei Schlüssel: Text, der ein erkanntes Wort aus dem Bild ist, und Relevanz, die als der Bruchteil des Bereichs des Begrenzungsrahmens des extrahierten Textes im Vergleich zum vollständigen Bild berechnet wird. 0,01 würde in einen Text übersetzt werden, der mindestens 1 % des Bildes einnimmt.
3. is_text_present: 0 oder 1, je nachdem, ob Text im Bild vorhanden ist. Wenn Tags den Wert 0 haben, ist die Liste leer.

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.06
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**Anfrage**

Die folgende Anfrage prüft anhand des in der Payload bereitgestellten Eingabebilds, ob Text vorhanden ist. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

Ausführung mit URL:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| Eigenschaft | Beschreibung | Obligatorisch |
| --- | --- | --- |
| `documents` | Liste der JSON-Elemente, wobei jedes Element in der Liste ein Bild darstellt. Alle Parameter, die als Teil dieser Liste übergeben werden, überschreiben den globalen Parameter, der außerhalb der Liste für das entsprechende Listenelement angegeben ist. | Ja |
| `sensei:multipart_field_name` | field_name, aus dem der Eingabedateipfad gelesen werden soll. | Ja |
| `repo:path` | Vordefinierte URL zum Bild-Asset. | Ja |
| `sensei:repoType` | „HTTP“ (für vordefinierte URL). | Nein |
| `dc:format` | Kodiertes Format des Eingabebildes. Für die Bildcodierung sind nur Bildformate wie JPEG, JPG, PNG und TIFF zulässig. Das dc:format wird mit zulässigen Formaten abgeglichen. | Nein |
| `correct_with_dictionary` | Ob die Wörter mit einem englischen Wörterbuch korrigiert werden sollen? Wenn diese Option nicht aktiviert ist, könnten nicht-englische Wörter erkannt werden. Der Standardwert ist „true“ (aktiviert). Beachten Sie, dass Sie bei eingeschaltetem Wörterbuch nicht immer ein englisches Wort erhalten müssen. Wir versuchen, es zu korrigieren, aber wenn es in einer bestimmten Bearbeitungsdistanz nicht möglich ist, geben wir das Originalwort zurück. | Nein |
| `filter_with_dictionary` | Gibt an, ob die Wörter so gefiltert werden sollen, dass sie nur Wörter aus dem englischen Wörterbuch enthalten? Wenn diese Option aktiviert ist, gehören die zurückgegebenen Wörter immer zu dem großen englischen , das 470.000 Wörter umfasst. | Nein |
| `min_probability` | Wie hoch ist die Mindestwahrscheinlichkeit für die erkannten Wörter? Nur Wörter, die aus dem Bild extrahiert wurden und eine höhere Wahrscheinlichkeit als „min_probability“ aufweisen, werden vom Service zurückgegeben. Der Standardwert ist 0,2. | Nein |
| `min_relevance` | Welches ist die Mindestrelevanz für die erkannten Wörter? Der Service gibt nur Wörter zurück, die aus dem Bild extrahiert wurden und eine größere Relevanz als „min_relevant“ haben. Der Standardwert ist 0,01. Die Relevanz wird als Bruchteil des Bereichs des Begrenzungsrahmens des extrahierten Textes im Vergleich zum vollständigen Bild berechnet. 0,01 würde in einen Text übersetzt werden, der mindestens 1 % des Bildes einnimmt. | Nein |

| Name | Datentyp | Erforderlich | Standard | Werte | Beschreibung |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | – | – | – | Vordefinierte URL des Bildes, aus dem Text extrahiert werden muss. |
| `sensei:repoType` | Zeichenfolge | – | – | HTTPS | Typ des Repositorys, in dem das Bild gespeichert wird. |
| `sensei:multipart_field_name` | Zeichenfolge | – | – | – | Verwenden Sie dies, wenn Sie das Bild als mehrteiliges Argument übergeben, anstatt vordefinierte URLs zu verwenden. |
| `dc:format` | Zeichenfolge | Ja | – | „image/jpg“, <br>„image/jpeg“, <br>„image/png“, <br>„image/tiff“ | Die Bildkodierung wird vor der Verarbeitung mit den zulässigen Eingabekodierungstypen abgeglichen. |