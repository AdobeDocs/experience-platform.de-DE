---
keywords: Visuelle Ähnlichkeit;visuelle Ähnlichkeit;ccai-API
solution: Experience Platform
title: Visuelle Ähnlichkeit in der Content and Commerce AI-API
description: Der Service für visuelle Ähnlichkeit sucht automatisch nach visuell ähnlichen Bildern aus einem Katalog, wenn ihm ein Bild gegeben wird.
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 3%

---

# Visuelle Ähnlichkeit

>[!NOTE]
>
>[!DNL Content and Commerce AI] befindet sich in der Betaphase. Die Dokumentation kann sich ändern.

Der Service für visuelle Ähnlichkeit sucht automatisch nach visuell ähnlichen Bildern aus einem Katalog, wenn ihm ein Bild gegeben wird.

Die folgende Abbildung wurde in der in diesem Dokument gezeigten Beispielanfrage verwendet:

![Testbild](../images/Query_Image.jpeg)

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anfrage ruft basierend auf den in der Payload bereitgestellten Eingabeparametern visuell ähnliche Bilder aus einem Katalog ab. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

>[!CAUTION]
>
>`analyzer_id` bestimmt, welche [!DNL Sensei Content Framework] verwendet wird. Vergewissern Sie sich, dass Sie über die richtigen `analyzer_id` verfügen, bevor Sie Ihre Anfrage stellen. Wenden Sie sich an das Beta-Team von Content and Commerce AI , um Ihre `analyzer_id` für diesen Service zu erhalten.

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
         "parameters": {
          "application-id": "1234", 
          "content-type": "inline", 
          "encoding": "jpeg", 
          "threshold": "0", 
          "top-N": "0", 
          "custom": {}, 
          "data": [{
            "content-id": "0987", 
            "content": "inline-image", 
            "content-type": "inline", 
            "encoding": "jpeg", 
            "threshold": "0", 
            "top-N": "0", 
            "historic-metadata": [], 
            "custom": {}
            }]
          }
      }
    ]
}'
```

| Eigenschaft | Beschreibung | Obligatorisch |
| --- | --- | --- |
| `analyzer_id` | Die [!DNL Sensei]-Service-ID, unter der Ihre Anfrage bereitgestellt wird. Diese ID bestimmt, welche der [!DNL Sensei Content Frameworks] verwendet werden. Wenden Sie sich für benutzerdefinierte Services an das KI-Team für Inhalte und Commerce, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID des erstellten Programms. | Ja |
| `data` | Ein Array, das ein JSON-Objekt enthält, wobei jedes Objekt im Array ein Bild darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, überschreiben die globalen Parameter, die außerhalb des `data`-Arrays angegeben werden. Alle verbleibenden Eigenschaften, die unten in dieser Tabelle beschrieben werden, können in `data` überschrieben werden. | Ja |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dieser nicht übergeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der Inhalt, der vom visuellen Ähnlichkeitsdienst analysiert werden soll. Falls das Bild Teil des Anfragetexts ist, verwenden Sie `-F file=@<filename>` im curl-Befehl, um das Bild zu übergeben, wobei dieser Parameter als leere Zeichenfolge verbleibt. <br> Wenn es sich bei dem Bild um eine Datei auf S3 handelt, übergeben Sie die signierte URL. Wenn Inhalte Teil des Anfragetexts sind, sollte die Liste der Datenelemente nur ein -Objekt haben. Wenn mehr als ein Objekt übergeben wird, wird nur das erste Objekt verarbeitet. | Ja |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anfragetexts oder eine signierte URL für einen S3-Bucket ist. Der Standardwert für diese Eigenschaft ist `inline`. | Nein |
| `encoding` | Das Dateiformat des Eingabebildes. Derzeit können nur JPEG- und PNG-Bilder verarbeitet werden. Der Standardwert für diese Eigenschaft ist `jpeg`. | Nein |
| `threshold` | Der Schwellenwert des Scores (0 bis 1), bei dessen Überschreitung die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Der Standardwert für diese Eigenschaft ist `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold` ist die Anzahl der zurückgegebenen Ergebnisse der niedrigere der beiden festgelegten Grenzwerte. Der Standardwert für diese Eigenschaft ist `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die übergeben werden sollen. | Nein |
| `historic-metadata` | Ein Array, das Metadaten übergeben werden kann. | Nein |

**Antwort**

Eine erfolgreiche Antwort gibt ein `response`-Array zurück, das eine `feature_value` und einen `feature_name` für jedes der visuell ähnlichen Bilder enthält, die im Katalog gefunden werden.

Die folgenden visuell ähnlichen Bilder wurden in der unten gezeigten Beispielantwort zurückgegeben:

![Ähnliche Bilder](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```
