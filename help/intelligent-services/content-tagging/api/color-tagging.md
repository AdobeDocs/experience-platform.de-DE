---
keywords: Experience Platform; Erste Schritte; Inhaltsai; Commerce-Hilfe; Inhalts-Tagging; Farb-Tagging; Farbextraktion;
solution: Experience Platform
title: Farb-Tagging in der Inhalts-Tagging-API
description: Der Farb-Tagging-Dienst kann, wenn ein Bild vorhanden ist, das Histogramm der Pixelfarben berechnen und durch dominante Farben in Behälter sortieren.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: feebf4c20d20afcdcfe4523e0b61bff5b999084c
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 5%

---

# Farb-Tagging

Der Farb-Tagging-Dienst kann, wenn ein Bild vorhanden ist, ein Histogramm von Pixelfarben berechnen und diese anhand dominanter Farben in Behälter sortieren. Die Farben der Bildpixel werden in 40 vorherrschende Farben zusammengefasst, die für das Farbspektrum repräsentativ sind. Ein Histogramm mit Farbwerten wird dann unter diesen 40 Farben berechnet. Der Dienst weist zwei Varianten auf:

**Farb-Tagging (Vollbild)**

Diese Methode extrahiert ein Farbhistogramm über das gesamte Bild.

**Farb-Tagging (mit Maske)**

Diese Methode verwendet einen auf tiefem Lernen basierenden Vordergrundextraktor, um Objekte im Vordergrund zu identifizieren. Das Modell wird anhand eines Katalogs von E-Commerce-Bildern trainiert. Nachdem das Vordergrundobjekt extrahiert wurde, wird ein Histogramm über die dominanten Farben berechnet, wie zuvor beschrieben.

Das folgende Bild wurde in dem in diesem Dokument gezeigten Beispiel verwendet:

![Testbild](../images/QQAsset1.jpg)

**API-Format**

```http
POST /services/v2/predict
```

**Anfrage**

Die folgende Beispielanfrage verwendet die Vollbildmethode für das Farb-Tagging.

Die folgende Anfrage extrahiert Farben aus einem Bild basierend auf den in der Payload bereitgestellten Eingabeparametern. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| Eigenschaft | Beschreibung | Obligatorisch |
| --- | --- | --- |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `documents` | Eine Liste von JSON-Elementen mit jedem Element in der Liste, das ein Dokument darstellt. | Ja |
| `top_n` | Die Anzahl der zurückzugebenden Ergebnisse (hierbei kann es sich nicht um eine negative Ganzzahl handeln). Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold`, ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Limits. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `min_coverage` | Deckungsschwellenwert, über den die Ergebnisse zurückgegeben werden müssen. Schließen Sie den Parameter aus, um alle Ergebnisse zurückzugeben. | Nein |
| `resize_image` | Gibt an, ob die Größe des Eingabebilds geändert werden soll. Standardmäßig wird die Größe der Bilder auf 320 x 320 Pixel geändert, bevor das Farb-Tagging durchgeführt wird. Zu Debugging-Zwecken können wir auch zulassen, dass der Code auf Vollbild ausgeführt wird, indem dieser auf &quot;False&quot;gesetzt wird. | Nein |
| `enable_mask` | Aktiviert/Deaktiviert das Farb-Tagging innerhalb der Maske. | Nein |

| Name | Datentyp | Erforderlich | Standard | Werte | Beschreibung |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | – | – | – | Vordefinierte URL des Dokuments, aus dem Schlüsselbegriffe extrahiert werden sollen. |
| `sensei:repoType` | Zeichenfolge | – | – | HTTPS | Typ des Repositorys, in dem das Bild gespeichert wird. |
| `sensei:multipart_field_name` | Zeichenfolge | – | – | – | Verwenden Sie dies, wenn Sie eine Bilddatei als mehrteiliges Argument übergeben, anstatt vorsignierte URLs zu verwenden. |
| `dc:format` | Zeichenfolge | Ja | – | &quot;image/jpg&quot;, <br> &quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | Die Bildkodierung wird vor der Verarbeitung mit den zulässigen Eingabekodierungstypen abgeglichen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der extrahierten Farben zurück. Jede Farbe wird durch eine `feature_value` -Schlüssel, der die folgenden Informationen enthält:

- Ein Farbname
- Der Prozentsatz, in dem diese Farbe im Verhältnis zum Bild angezeigt wird
- Der RGB-Wert der Farbe

Im ersten Beispielobjekt unten wird die `feature_value` von `Mud_Green,0.069,102,72,95` bedeutet, dass die Farbe grün ist, Schlamm grün ist in 6,9% des Bildes gefunden, und einen RGB-Wert von 102,72,95 hat.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
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
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
