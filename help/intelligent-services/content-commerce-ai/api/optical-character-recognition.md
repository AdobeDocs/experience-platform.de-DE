---
keywords: OCR; Textpräsenz; optische Zeichenerkennung
solution: Experience Platform
title: Textpräsenz und optische Zeichenerkennung
description: In der Inhalts- und Commerce-API kann der Dienst für die Texterkennung/Optische Zeichenerkennung (OCR) angeben, ob in einem bestimmten Bild Text vorhanden ist. Wenn Text vorhanden ist, kann OCR den Text zurückgeben.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 4%

---

# Textpräsenz und optische Zeichenerkennung

>[!NOTE]
>
>Die KI für Inhalte und Commerce befindet sich in der Beta-Phase. Die Dokumentation kann sich ändern.

Der Dienst für die Texterkennung/optische Zeichenerkennung (OCR) kann bei einem Bild angeben, ob im Bild Text vorhanden ist. Wenn Text vorhanden ist, kann OCR den Text zurückgeben.

Die folgende Abbildung wurde in der Beispielanfrage in diesem Dokument verwendet:

![Testbild](../images/shef.jpeg)

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anfrage prüft anhand des in der Payload bereitgestellten Eingabebilds, ob Text vorhanden ist. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

>[!CAUTION]
>
>`analyzer_id` bestimmt, [!DNL Sensei Content Framework] verwendet. Vergewissern Sie sich bitte, dass Sie über die richtige `analyzer_id` bevor Sie Ihre Anfrage stellen. Kontaktieren Sie das Beta-Team von Content and Commerce AI , um Ihre `analyzer_id` für diesen Dienst.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
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
    }]
  }'
```

| Eigenschaft | Beschreibung | Obligatorisch |
| --- | --- | --- |
| `analyzer_id` | Die [!DNL Sensei] Dienst-ID, unter der Ihre Anfrage bereitgestellt wird. Diese ID bestimmt, welcher der [!DNL Sensei Content Frameworks] verwendet werden. Wenden Sie sich bei benutzerdefinierten Diensten an das KI-Team von Content and Commerce, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die Kennung der erstellten Anwendung. | Ja |
| `data` | Ein Array, das ein JSON-Objekt enthält, wobei jedes Objekt im Array ein weitergegebenes Bild darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer Kraft, die außerhalb der `data` Array. Jede der anderen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, kann von innerhalb `data`. | Ja |
| `language` | Sprache des Eingabetexts. Der Standardwert lautet `en`. | Nein |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anfragetexts oder einer signierten URL für einen S3-Behälter ist. Der Standardwert für diese Eigenschaft lautet `inline`. | Nein |
| `encoding` | Das Dateiformat des Eingabebilds. Derzeit können nur JPEG- und PNG-Bilder verarbeitet werden. Der Standardwert für diese Eigenschaft lautet `jpeg`. | Nein |
| `threshold` | Der Schwellenwert des Punktes (0 bis 1), über dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold`, ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Limits. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die weitergegeben werden sollen. Für diese Eigenschaft ist ein gültiges JSON-Objekt erforderlich, damit sie funktioniert. | Nein |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht übergeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der Inhalt kann ein Rohbild sein (&quot;Inline&quot;-Inhaltstyp). <br> Wenn der Inhalt eine Datei auf S3 ist (&#39;s3-bucket&#39; Inhaltstyp), übergeben Sie die signierte URL. | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt den Text zurück, der in der `feature_value` Array. Der Text wird gelesen und von links nach rechts von oben zurückgegeben. Wenn also &quot;Ich liebe Adobe&quot;erkannt wurde, gibt Ihre Payload &quot;I&quot;, &quot;Love&quot;und &quot;Adobe&quot;in separaten Objekten zurück. Im Objekt erhalten Sie eine `feature_name` , das das Wort und ein `feature_value` , die eine Konfidenzmetrik für diesen Text enthält.

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
