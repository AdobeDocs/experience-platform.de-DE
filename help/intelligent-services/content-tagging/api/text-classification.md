---
keywords: Text-Classification; Text-Classification
solution: Experience Platform
title: Textklassifizierung in der Inhalts- und Commerce-API
description: Der Text-Classification-Dienst kann ein Textfragment in eine oder mehrere Beschriftungen klassifizieren. Die Classification kann aus einer einzigen Bezeichnung, mehreren Beschriftungen oder hierarchischen Strukturen bestehen.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: 081e31727b4e78126e60896b3b850c5589526152
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 5%

---

# Textklassifizierung

>[!NOTE]
>
>Die KI für Inhalte und Commerce befindet sich in der Beta-Phase. Die Dokumentation kann sich ändern.

Der Text-Classification-Dienst kann ein Textfragment in eine oder mehrere Beschriftungen klassifizieren. Die Classification kann aus einer einzigen Bezeichnung, mehreren Beschriftungen oder hierarchischen Strukturen bestehen.

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anfrage klassifiziert Text aus einem Fragment basierend auf den in der Payload bereitgestellten Eingabeparametern. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

>[!CAUTION]
>
>`analyzer_id` bestimmt, [!DNL Sensei Content Framework] verwendet. Vergewissern Sie sich bitte, dass Sie über die richtige `analyzer_id` bevor Sie Ihre Anfrage stellen. Kontaktieren Sie das Beta-Team von Content and Commerce AI , um Ihre `analyzer_id` für diesen Dienst.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\", 
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
         "parameters": {}
    }]
}'
```

| Eigenschaft | Beschreibung | Obligatorisch |
| --- | --- | --- |
| `analyzer_id` | Die [!DNL Sensei] Dienst-ID, unter der Ihre Anfrage bereitgestellt wird. Diese ID bestimmt, welcher der [!DNL Sensei Content Frameworks] verwendet werden. Wenden Sie sich bei benutzerdefinierten Diensten an das KI-Team von Content and Commerce, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die Kennung der erstellten Anwendung. | Ja |
| `data` | Ein Array, das ein JSON-Objekt mit jedem Objekt im Array enthält, das ein Dokument darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer Kraft, die außerhalb der `data` Array. Jede der anderen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, kann von innerhalb `data`. | Ja |
| `language` | Sprache des Eingabetexts. Der Standardwert lautet `en`. | Nein |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anfragetexts oder einer signierten URL für einen S3-Behälter ist. Der Standardwert für diese Eigenschaft lautet `inline`. | Nein |
| `encoding` | Das Kodierungsformat des Eingabetexts. Dies kann `utf-8` oder `utf-16`. Der Standardwert für diese Eigenschaft lautet `utf-8`. | Nein |
| `threshold` | Der Schwellenwert des Punktes (0 bis 1), über dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold`, ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Limits. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die weitergegeben werden sollen. Für diese Eigenschaft ist ein gültiges JSON-Objekt erforderlich, damit sie funktioniert. | Nein |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht übergeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der vom Text-Classification-Dienst verwendete Inhalt. Der Inhalt kann als roher Text (Inhaltstyp &quot;inline&quot;) verwendet werden. <br> Wenn der Inhalt eine Datei auf S3 ist (&#39;s3-bucket&#39; Inhaltstyp), übergeben Sie die signierte URL. | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt den klassifizierten Text in einem Antwort-Array zurück.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
