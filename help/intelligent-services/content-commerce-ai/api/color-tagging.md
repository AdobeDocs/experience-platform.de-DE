---
keywords: Experience Platform;Erste Schritte;Inhalt;Inhalts-Tagging;Farb-Tagging;Farbextraktion;
solution: Experience Platform
title: Farb-Tagging in der Content-Tagging-API
description: Der Farb-Tagging-Service kann bei der Bereitstellung eines Bildes das Histogramm der Pixelfarben berechnen und diese nach dominanten Farben in Buckets sortieren.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 6%

---

# Farb-Tagging

Der Farb-Tagging-Service kann bei der Bereitstellung eines Bildes ein Histogramm der Pixelfarben berechnen und diese nach dominanten Farben in Buckets sortieren. Die Farben in den Bildpixeln werden in 40 vorherrschende Farben zusammengefasst, die für das Farbspektrum repräsentativ sind. Aus diesen 40 Farben wird dann ein Histogramm der Farbwerte berechnet. Der Service kann in zwei Varianten angeboten werden:

**Farb-Tagging (Vollbild)**

Diese Methode extrahiert ein Farbhistogramm über das gesamte Bild.

**Farb-Tagging (mit Maske)**

Diese Methode verwendet einen auf Deep Learning basierenden Vordergrundextraktor, um Objekte im Vordergrund zu identifizieren. Nach dem Extrahieren der Vordergrundobjekte wird ein Histogramm über den dominanten Farben für den Vordergrund und den Hintergrund zusammen mit dem gesamten Bild berechnet.

**Tonabnahme**

Zusätzlich zu den oben genannten Varianten können Sie den Service so konfigurieren, dass ein Histogramm von Tönen für Folgendes abgerufen wird:

- Das Gesamtbild (bei Verwendung der vollständigen Bildvariante)
- Das Gesamtbild sowie die Vorder- und Hintergrundbereiche (bei Verwendung der Variante mit Maskierung)

Die folgende Abbildung wurde in dem in diesem Dokument gezeigten Beispiel verwendet:

![Testbild](../images/QQAsset1.jpg)

**API-Format**

```http
POST /services/v2/predict
```

**Anfrage - vollständige Bildvariante**

Die folgende Beispielanfrage verwendet die Full-Image-Methode für das Farb-Tagging und extrahiert Farben aus einem Bild basierend auf den in der Payload bereitgestellten Eingabeparametern. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

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

Eine erfolgreiche Antwort gibt die Details der extrahierten Farben zurück. Jede Farbe wird durch einen `feature_value` dargestellt, der die folgenden Informationen enthält:

- Ein Farbname
- Der Prozentsatz, um den diese Farbe in Bezug auf das Bild angezeigt wird
- Der RGB-Wert der Farbe

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`bedeutet, dass die gefundene Farbe Weiß ist, was in 58,34 % des Bildes zu finden ist, und einen mittleren RGB-Wert von 254, 254, 243 hat.

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

Beachten Sie, dass für das Ergebnis hier Farbe aus dem gesamten Bildbereich extrahiert wurde.

**Anfrage - maskierte Bildvariante**

Die folgende Beispielanfrage verwendet die Maskierungsmethode für Farb-Tagging. Dies wird aktiviert, indem in der Anfrage der `enable_mask` auf `true` gesetzt wird.

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

>[!NOTE]
>
>Darüber hinaus wird der `retrieve_tone` Parameter in der obigen Anfrage ebenfalls auf `true` gesetzt. Auf diese Weise können wir ein Tonverteilungs-Histogramm über warme, neutrale und kalte Töne in den gesamten, Vordergrund- und Hintergrundbereichen des Bildes abrufen.

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

Zusätzlich zu den Farben aus dem Gesamtbild können Sie jetzt auch Farben aus den Vordergrund- und Hintergrundbereichen sehen. Da der Tonabruf für jede der oben genannten Regionen aktiviert ist, können Sie auch das Histogramm eines Tons abrufen.

**Eingabeparameter**

| Name | Datentyp | Erforderlich | Standard | Werte | Beschreibung |
| --- | --- | --- | --- | --- | --- |
| `documents` | Array (Document-Object) | Ja | – | Siehe unten | Liste der JSON-Elemente, wobei jedes Element in der Liste ein Dokument darstellt. |
| `top_n` | number | Nein | 0 | Ganzzahl ohne negative Auswirkung | Anzahl der zurückzugebenden Ergebnisse. 0, um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit einem Schwellenwert ist die Anzahl der zurückgegebenen Ergebnisse kleiner als beide Grenzen. |
| `min_coverage` | number | Nein | 0,05 | Reelle Zahl | Schwellenwert für die Abdeckung, ab dem die Ergebnisse zurückgegeben werden müssen. Parameter ausschließen, um alle Ergebnisse zurückzugeben. |
| `resize_image` | number | Nein | True | true/false | Gibt an, ob die Größe des Eingabebilds geändert werden soll. Standardmäßig werden die Bilder auf 320*320 Pixel skaliert, bevor die Farbextraktion durchgeführt wird. Zu Debuggingzwecken können wir zulassen, dass der Code auch auf dem vollständigen Bild ausgeführt wird, indem wir dies auf `False` setzen. |
| `enable_mask` | number | Nein | False | true/false | Aktiviert/Deaktiviert die Farbextraktion |
| `retrieve_tone` | number | Nein | False | true/false | Aktiviert/Deaktiviert die Tonextraktion |

**Dokumentobjekt**

| Name | Datentyp | Erforderlich | Standard | Werte | Beschreibung |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | – | – | – | Vordefinierte URL des Dokuments. |
| `sensei:repoType` | Zeichenfolge | – | – | HTTPS | Typ des Repositorys, in dem das Bild gespeichert wird. |
| `sensei:multipart_field_name` | Zeichenfolge | – | – | – | Verwenden Sie dies, wenn Sie die Bilddatei als mehrteiliges Argument übergeben, anstatt vordefinierte URLs zu verwenden. |
| `dc:format` | Zeichenfolge | Ja | – | „image/jpg“,<br>„image/jpeg“,<br>„image/png“,<br>„image/tiff“ | Die Bildkodierung wird vor der Verarbeitung mit den zulässigen Eingabekodierungstypen abgeglichen. |