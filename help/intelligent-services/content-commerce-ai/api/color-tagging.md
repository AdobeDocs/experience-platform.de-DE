---
keywords: Experience Platform; Erste Schritte; Inhalt; Tagging von Inhalten; Farbmarkierung; Farbextraktion;
solution: Experience Platform
title: Farb-Tagging in der Inhalts-Tagging-API
description: Der Color Tagging-Dienst kann, wenn ihm ein Bild gegeben wird, das Histogramm der Pixelfarben berechnen und sie anhand dominanter Farben in Behältern sortieren.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: e6ea347252b898f73c2bc495b0324361ee6cae9b
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 6%

---

# Farb-Tagging

Der Farb-Tagging-Dienst kann, wenn ein Bild vorhanden ist, ein Histogramm von Pixelfarben berechnen und diese anhand dominanter Farben in Behälter sortieren. Die Farben der Bildpixel werden in 40 vorherrschende Farben zusammengefasst, die für das Farbspektrum repräsentativ sind. Ein Histogramm mit Farbwerten wird dann unter diesen 40 Farben berechnet. Der Dienst weist zwei Varianten auf:

**Farb-Tagging (Vollbild)**

Diese Methode extrahiert ein Farbhistogramm über das gesamte Bild.

**Farb-Tagging (mit Maske)**

Diese Methode verwendet einen auf tiefem Lernen basierenden Vordergrundextraktor, um Objekte im Vordergrund zu identifizieren. Sobald die Vordergrundobjekte extrahiert wurden, wird ein Histogramm über die dominanten Farben für die Vordergrund- und Hintergrundbereiche sowie das gesamte Bild berechnet.

**Tonextraktion**

Zusätzlich zu den oben genannten Varianten kann der Dienst so konfiguriert werden, dass ein Histogramm mit Tönen abgerufen wird für:

- Das Gesamtbild (bei Verwendung der vollständigen Bildvariante)
- Das Gesamtbild sowie die Vordergrund- und Hintergrundbereiche (bei Verwendung der Variante mit Maskierung)

Das folgende Bild wurde in dem in diesem Dokument gezeigten Beispiel verwendet:

![Testbild](../images/QQAsset1.jpg)

**API-Format**

```http
POST /services/v2/predict
```

**Anfrage - vollständige Bildvariante**

Die folgende Beispielanfrage verwendet die Vollbildmethode für das Farb-Tagging und extrahiert Farben aus einem Bild basierend auf den in der Payload bereitgestellten Eingabeparametern. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**Antwort - vollständige Bildvariante**

Eine erfolgreiche Antwort gibt die Details der extrahierten Farben zurück. Jede Farbe wird durch eine `feature_value` -Schlüssel, der die folgenden Informationen enthält:

- Ein Farbname
- Der Prozentsatz, in dem diese Farbe im Verhältnis zum Bild angezeigt wird
- Der RGB-Wert der Farbe

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`bedeutet, dass die gefundenen Farben weiß sind, was in 58,34 % des Bildes zu finden ist und einen durchschnittlichen RGB-Wert von 254, 254, 243 aufweist.

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

Beachten Sie, dass das Ergebnis hier eine Farbe für den Bildbereich &quot;insgesamt&quot;extrahiert hat.

**Anfrage - maskierte Bildvariante**

Die folgende Beispielanfrage verwendet die Maskierungsmethode für das Farb-Tagging. Wir aktivieren dies, indem Sie die `enable_mask` Parameter auf `true` in der Anfrage.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>Hinweis: Darüber hinaus legen wir `retrieve_tone` Parameter auf `true` in der obigen Anfrage. Dadurch können wir ein Tonverteilungs-Histogramm über warme, neutrale und kühle Töne in den gesamten, Vordergrund- und Hintergrundbereichen des Bildes abrufen.

**Antwort - maskierte Bildvariante**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

Zusätzlich zu den Farben des Gesamtbilds können Sie jetzt auch Farben aus den Vordergrund- und Hintergrundbereichen sehen. Da wir für jede der oben genannten Regionen die Tonabfrage aktivieren, können wir auch ein Tonhistogramm abrufen.

**Eingabeparameter**

| Name | Datentyp | Erforderlich | Standard | Werte | Beschreibung |
| --- | --- | --- | --- | --- | --- |
| `documents` | array (Document-Object) | Ja | – | Siehe unten | Liste der JSON-Elemente mit jedem Element in der Liste, das ein Dokument darstellt. |
| `top_n` | number | Nein | 0 | Nicht negative Ganzzahl | Anzahl der zurückzugebenden Ergebnisse. 0, um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit einem Schwellenwert ist die Anzahl der zurückgegebenen Ergebnisse kleiner als die beiden Begrenzungen. |
| `min_coverage` | number | Nein | 0.05 | Real number | Deckungsschwellenwert, über den die Ergebnisse zurückgegeben werden müssen. Parameter ausschließen , um alle Ergebnisse zurückzugeben. |
| `resize_image` | number | Nein | True | True/False | Gibt an, ob die Größe des Eingabebilds geändert werden soll oder nicht. Standardmäßig wird die Größe der Bilder auf 320 x 320 Pixel geändert, bevor die Farbextrahierung durchgeführt wird. Zu Debugging-Zwecken können wir auch zulassen, dass der Code auf Vollbild ausgeführt wird, indem dieser auf &quot;False&quot;gesetzt wird. |
| `enable_mask` | number | Nein | False | True/False | Aktiviert/Deaktiviert die Farbextraktion |
| `retrieve_tone` | number | Nein | False | True/False | Aktiviert/Deaktiviert die Tonextraktion |

**Dokumentobjekt**

| Name | Datentyp | Erforderlich | Standard | Werte | Beschreibung |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | – | – | – | Vordefinierte URL des Dokuments, aus dem Schlüsselbegriffe extrahiert werden sollen. |
| `sensei:repoType` | Zeichenfolge | – | – | HTTPS | Typ des Repositorys, in dem das Dokument gespeichert wird. |
| `sensei:multipart_field_name` | Zeichenfolge | – | – | – | Verwenden Sie dies, wenn Sie das Dokument als mehrteiliges Argument übergeben, anstatt vorsignierte URLs zu verwenden. |
| `dc:format` | Zeichenfolge | Ja | – | &quot;text/plain&quot;,<br>&quot;application/pdf&quot;,<br>&quot;text/pdf&quot;,<br>&quot;text/html&quot;,<br>&quot;text/rtf&quot;,<br>&quot;application/rtf&quot;,<br>&quot;application/msword&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.wordprocessingml.document&quot;,<br>&quot;application/mspowerpoint&quot;,<br>&quot;application/vnd.ms-powerpoint&quot;,<br>&quot;application/vnd.openxmlformats-officedocument.presentationml.presentation&quot; | Die Dokumentkodierung wird vor der Verarbeitung mit den zulässigen Eingabekodierungstypen abgeglichen. |