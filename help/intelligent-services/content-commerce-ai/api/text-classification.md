---
keywords: text classification;Text classification
solution: Experience Platform
title: Endpunkt der Textklassifizierungs-API
topic: Developer guide
description: Der Text-Classification-Dienst kann ein Textfragment in eine oder mehrere Beschriftungen klassifizieren. Die Klassifizierung kann aus einer einzelnen Bezeichnung, mehreren Beschriftungen oder einer hierarchischen Struktur bestehen.
translation-type: tm+mt
source-git-commit: 31e4f1441676daa79f064c567ddc47e9198d0a0b
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 5%

---


# Textklassifizierung

>[!NOTE]
>
>Die AI für Inhalte und Commerce befindet sich in der Betaphase. Die Dokumentation kann geändert werden.

Der Text-Classification-Dienst kann ein Textfragment in eine oder mehrere Beschriftungen klassifizieren. Die Klassifizierung kann aus einer einzelnen Bezeichnung, mehreren Beschriftungen oder einer hierarchischen Struktur bestehen.

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anforderung klassifiziert Text aus einem Fragment anhand der in der Nutzlast bereitgestellten Eingabeparameter. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispielpayload.

>[!CAUTION]
>
>`analyzer_id` bestimmt, welche verwendet [!DNL Sensei Content Framework] wird. Vergewissern Sie sich bitte, dass Sie über die erforderlichen Informationen verfügen, `analyzer_id` bevor Sie Ihre Anfrage bearbeiten. Wenden Sie sich an das AI Beta-Team von Content and Commerce, um Ihren `analyzer_id` Service zu erhalten.

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
| `analyzer_id` | Die [!DNL Sensei] Dienst-ID, unter der Ihre Anforderung bereitgestellt wird. Mit dieser ID wird festgelegt, welche der Variablen verwendet [!DNL Sensei Content Frameworks] werden. Wenden Sie sich bei benutzerdefinierten Diensten an das Content and Commerce AI-Team, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `data` | Ein Array, das ein JSON-Objekt mit jedem Objekt im Array enthält, das ein Dokument darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer dem `data` Array außer Kraft. Die übrigen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, können von innen aus überschrieben werden `data`. | Ja |
| `language` | Sprache des Eingabetexts. Der Standardwert lautet `en`. | Nein |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anforderungstextes oder einer signierten URL für einen S3-Behälter ist. Die Standardeinstellung für diese Eigenschaft ist `inline`. | Nein |
| `encoding` | Das Kodierungsformat des Eingabetexts. Das kann sein `utf-8` oder `utf-16`. Die Standardeinstellung für diese Eigenschaft ist `utf-8`. | Nein |
| `threshold` | Der Schwellenwert des Ergebnisses (0 bis 1), ab dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert, `0` um alle Ergebnisse zurückzugeben. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert, `0` um alle Ergebnisse zurückzugeben. Bei gleichzeitiger Verwendung `threshold`ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Grenzwerte. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die übergeben werden sollen. Für diese Eigenschaft ist ein gültiges JSON-Objekt erforderlich, um zu funktionieren. | Nein |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht übergeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der vom Text-Classification-Dienst verwendete Inhalt. Der Inhalt kann als Rohtext (&quot;inline&quot;-Inhaltstyp) verwendet werden. <br> Wenn es sich bei dem Inhalt um eine Datei unter S3 handelt (&#39;s3-bucket&#39; Content-Typ), übergeben Sie die signierte URL. | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt den klassifizierten Text in einem Antwortarray zurück.

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
