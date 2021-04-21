---
keywords: Visuelle Ähnlichkeit;Visuelle Ähnlichkeit;ccai API
solution: Experience Platform, Intelligent Services
title: Visuelle Ähnlichkeit in der API für Inhalts- und Commerce-API
topic-legacy: Developer guide
description: Der Dienst für visuelle Ähnlichkeit findet bei einem gegebenen Bild automatisch visuell ähnliche Bilder aus einem Katalog.
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# Visuelle Ähnlichkeit

>[!NOTE]
>
>[!DNL Content and Commerce AI] in der Betaphase enthalten. Die Dokumentation kann geändert werden.

Der Dienst für visuelle Ähnlichkeit findet bei einem gegebenen Bild automatisch visuell ähnliche Bilder aus einem Katalog.

Die folgende Abbildung wurde in der Beispielanforderung in diesem Dokument verwendet:

![Testbild](../images/Query_Image.jpeg)

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anforderung ruft visuell ähnliche Bilder aus einem Katalog ab, basierend auf den in der Nutzlast bereitgestellten Eingabeparametern. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispielpayload.

>[!CAUTION]
>
>`analyzer_id` bestimmt, welche verwendet  [!DNL Sensei Content Framework] wird. Bitte überprüfen Sie, ob Sie die richtige `analyzer_id` haben, bevor Sie Ihre Anfrage machen. Wenden Sie sich an das AI Beta-Team von Content and Commerce, um Ihre `analyzer_id` für diesen Dienst zu erhalten.

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
| `analyzer_id` | Die [!DNL Sensei]-Dienst-ID, unter der Ihre Anforderung bereitgestellt wird. Diese ID bestimmt, welche der [!DNL Sensei Content Frameworks] verwendet werden. Wenden Sie sich bei benutzerdefinierten Diensten an das Content and Commerce AI-Team, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `data` | Ein Array, das ein JSON-Objekt mit jedem Objekt im Array enthält, das ein Bild darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer dem Array `data` außer Kraft. Die übrigen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, können innerhalb von `data` überschrieben werden. | Ja |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht weitergegeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der Inhalt, der vom Dienst für visuelle Ähnlichkeit analysiert werden soll. Verwenden Sie im Ereignis, dass das Image zum Anforderungstext gehört, `-F file=@<filename>` im curl-Befehl, um das Image zu übergeben, wobei dieser Parameter eine leere Zeichenfolge bleibt. <br> Wenn das Bild eine Datei auf S3 ist, übergeben Sie die signierte URL. Wenn der Inhalt zum Anforderungstext gehört, sollte die Liste der Datenelemente nur ein Objekt enthalten. Wenn mehr als ein Objekt übergeben wird, wird nur das erste Objekt verarbeitet. | Ja |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anforderungstextes oder einer signierten URL für einen S3-Behälter ist. Die Standardeinstellung für diese Eigenschaft ist `inline`. | Nein |
| `encoding` | Das Dateiformat des Eingabebilds. Derzeit können nur JPEG- und PNG-Bilder verarbeitet werden. Die Standardeinstellung für diese Eigenschaft ist `jpeg`. | Nein |
| `threshold` | Der Schwellenwert des Ergebnisses (0 bis 1), ab dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert `0`, um alle Ergebnisse zurückzugeben. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert `0`, um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold` ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden angegebenen Grenzwerte. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die übergeben werden sollen. | Nein |
| `historic-metadata` | Ein Array, an das Metadaten übergeben werden können. | Nein |

**Antwort**

Bei einer erfolgreichen Antwort wird ein `response`-Array zurückgegeben, das ein `feature_value` und `feature_name` für jedes der visuell ähnlichen Bilder im Katalog enthält.

Die folgenden visuell ähnlichen Bilder wurden in der folgenden Beispielantwort zurückgegeben:

![ähnliche Bilder](../images/results.jpg)

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
