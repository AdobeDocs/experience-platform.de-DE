---
keywords: OCR;Textpräsenz;optische Zeichenerkennung
solution: Experience Platform, Intelligent Services
title: Textpräsenz und optische Zeichenerkennung
topic-legacy: Developer guide
description: In der API für Inhalts- und Commerce-API kann der Dienst für die Texterkennung/optische Zeichenerkennung (OCR) angeben, ob Text in einem bestimmten Bild vorhanden ist. Wenn Text vorhanden ist, kann OCR den Text zurückgeben.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 4%

---

# Textpräsenz und optische Zeichenerkennung

>[!NOTE]
>
>Die AI für Inhalte und Commerce befindet sich in der Betaphase. Die Dokumentation kann geändert werden.

Der Dienst &quot;Texterkennung/Optische Zeichenerkennung&quot;(OCR) kann bei Angabe eines Bildes angeben, ob Text im Bild vorhanden ist. Wenn Text vorhanden ist, kann OCR den Text zurückgeben.

Die folgende Abbildung wurde in der Beispielanforderung in diesem Dokument verwendet:

![Testbild](../images/shef.jpeg)

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anforderung prüft, ob Text auf der Grundlage des in der Nutzlast bereitgestellten Eingabebilds vorhanden ist. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispielpayload.

>[!CAUTION]
>
>`analyzer_id` bestimmt, welche verwendet  [!DNL Sensei Content Framework] wird. Bitte überprüfen Sie, ob Sie die richtige `analyzer_id` haben, bevor Sie Ihre Anfrage machen. Wenden Sie sich an das AI Beta-Team von Content and Commerce, um Ihre `analyzer_id` für diesen Dienst zu erhalten.

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
| `analyzer_id` | Die [!DNL Sensei]-Dienst-ID, unter der Ihre Anforderung bereitgestellt wird. Diese ID bestimmt, welche der [!DNL Sensei Content Frameworks] verwendet werden. Wenden Sie sich bei benutzerdefinierten Diensten an das Content and Commerce AI-Team, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `data` | Ein Array, das ein JSON-Objekt mit jedem Objekt im Array enthält, das ein weitergeleitetes Bild darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer dem Array `data` außer Kraft. Die übrigen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, können innerhalb von `data` überschrieben werden. | Ja |
| `language` | Sprache des Eingabetexts. Der Standardwert lautet `en`. | Nein |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anforderungstextes oder einer signierten URL für einen S3-Behälter ist. Die Standardeinstellung für diese Eigenschaft ist `inline`. | Nein |
| `encoding` | Das Dateiformat des Eingabebilds. Derzeit können nur JPEG- und PNG-Bilder verarbeitet werden. Die Standardeinstellung für diese Eigenschaft ist `jpeg`. | Nein |
| `threshold` | Der Schwellenwert des Ergebnisses (0 bis 1), ab dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert `0`, um alle Ergebnisse zurückzugeben. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert `0`, um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold` ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden angegebenen Grenzwerte. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die übergeben werden sollen. Für diese Eigenschaft ist ein gültiges JSON-Objekt erforderlich, um zu funktionieren. | Nein |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht weitergegeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der Inhalt kann ein Rohbild (&quot;inline&quot;-Inhaltstyp) sein. <br> Wenn es sich bei dem Inhalt um eine Datei unter S3 handelt (Content-Typ des s3-Buckets), übergeben Sie die signierte URL. | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt den Text zurück, der im Array `feature_value` erkannt wurde. Der Text wird gelesen und von links nach rechts oben zurückgegeben. Wenn also &quot;Ich liebe Adobe&quot;erkannt wurde, gibt Ihre Nutzlast &quot;Ich&quot;, &quot;Liebe&quot;und &quot;Adobe&quot;in separaten Objekten zurück. Im Objekt erhalten Sie ein `feature_name`, das das Wort und ein `feature_value` enthält, das eine Konfidenzmetrik für diesen Text enthält.

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
