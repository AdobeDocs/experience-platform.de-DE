---
keywords: OCR; Textpräsenz; optische Zeichenerkennung
solution: Experience Platform
title: Textpräsenz und optische Zeichenerkennung
description: In der Content Tagging API kann der Dienst für die Texterkennung (OCR) angeben, ob in einem Bild Text vorhanden ist. Wenn Text vorhanden ist, kann OCR den Text zurückgeben.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 82722ddf7ff543361177b555fffea730a7879886
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 4%

---

# Textpräsenz und optische Zeichenerkennung

Der Dienst für die Texterkennung/optische Zeichenerkennung (OCR) kann bei einem Bild angeben, ob im Bild Text vorhanden ist. Wenn Text vorhanden ist, kann OCR den Text zurückgeben.

Die folgende Abbildung wurde in der Beispielanfrage in diesem Dokument verwendet:

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

Eine erfolgreiche Antwort gibt den Text zurück, der in der `tags` Liste für jedes Bild, das in der Anfrage übergeben wurde. Wenn in einem bestimmten Bild kein Text vorhanden ist, `is_text_present` ist 0 und `tags` ist eine leere Liste.

[result0, result1, ...]: Liste der Antworten für jedes Eingabedokument. Jedes Ergebnis enthält ein Dict mit Schlüsseln:

1. request_element_id: entspricht dem Index der Eingabedatei für diese Antwort, 0 für das erste Bild in der Dokumentenliste der Anforderung, 1 für das nächste usw.
2. Tags: Liste von Wörterbüchern enthält jedes Wörterbuch zwei Schlüssel: Text, das ein erkanntes Wort aus dem Bild ist, und Relevanz, die als Bruchteil des Bereichs des Begrenzungsrahmens des extrahierten Textes im Vergleich zum vollständigen Bild berechnet wird. 0,01 würde in einen Text übersetzen, der mindestens 1 % des Bildes umfasst.
3. is_text_present: 0 oder 1, je nachdem, ob im Bild Text vorhanden ist. Wenn die Tags 0 sind, ist die Liste leer.

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
| `documents` | Liste der JSON-Elemente mit jedem Element in der Liste, das ein Bild darstellt. Alle Parameter, die als Teil dieser Liste übergeben werden, überschreiben den außerhalb der Liste angegebenen globalen Parameter für das entsprechende Listenelement. | Ja |
| `sensei:multipart_field_name` | field_name , um den Pfad der Eingabedatei zu lesen. | Ja |
| `repo:path` | Vordefinierte URL für Bild-Asset. | Ja |
| `sensei:repoType` | &quot;HTTP&quot;(für vorsignierte URL). | Nein |
| `dc:format` | Kodiertes Format des Eingabebilds. Für die Bildkodierung sind nur Bildformate wie jpeg, jpg, png und tiff zulässig. Das dc:format wird mit den zulässigen Formaten abgeglichen. | Nein |
| `correct_with_dictionary` | Ob die Wörter mit einem englischen Wörterbuch korrigiert werden sollen? Wenn diese Option nicht aktiviert ist, werden möglicherweise nicht englische Wörter erkannt. Der Standardwert ist True: aktiviert.) Beachten Sie, dass es bei Aktivierung des Wörterbuchs nicht notwendig ist, immer ein englisches Wort zu erhalten. Wir versuchen, es zu korrigieren, aber wenn es innerhalb einer bestimmten Bearbeitungsentfernung nicht möglich ist, geben wir das ursprüngliche Wort zurück. | Nein |
| `filter_with_dictionary` | Ob die Wörter so gefiltert werden sollen, dass sie nur die Wörter aus dem englischen Wörterbuch enthalten? Wenn diese Option aktiviert ist, gehören die zurückgegebenen Wörter immer zum großen Englisch , das 470.000 Wörter umfasst. | Nein |
| `min_probability` | Wie hoch ist die Mindestwahrscheinlichkeit für die erkannten Wörter? Nur die Wörter, die aus dem Bild extrahiert werden und eine höhere Wahrscheinlichkeit als min_wahrscheinlicher haben, werden vom Dienst zurückgegeben. Der Standardwert ist auf 0,2 festgelegt. | Nein |
| `min_relevance` | Was ist die minimale Relevanz für die erkannten Wörter? Nur die Wörter, die aus dem Bild extrahiert werden und eine größere Relevanz als min_relevant haben, werden vom Dienst zurückgegeben. Der Standardwert wird auf 0,01 gesetzt. Die Relevanz wird als der Anteil des Bereichs des Begrenzungsrahmens des extrahierten Textes im Vergleich zum vollständigen Bild berechnet. 0,01 würde in einen Text übersetzen, der mindestens 1 % des Bildes umfasst. | Nein |

| Name | Datentyp | Erforderlich | Standard | Werte | Beschreibung |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | – | – | – | Vordefinierte URL des Bildes, aus dem Text extrahiert werden soll. |
| `sensei:repoType` | Zeichenfolge | – | – | HTTPS | Typ des Repositorys, in dem das Bild gespeichert wird. |
| `sensei:multipart_field_name` | Zeichenfolge | – | – | – | Verwenden Sie dies, wenn Sie das Bild als mehrteiliges Argument übergeben, anstatt vorsignierte URLs zu verwenden. |
| `dc:format` | Zeichenfolge | Ja | – | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | Die Bildkodierung wird vor der Verarbeitung mit den zulässigen Eingabekodierungstypen abgeglichen. |