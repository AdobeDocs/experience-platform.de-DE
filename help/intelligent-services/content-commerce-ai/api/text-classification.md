---
keywords: Textklassifizierung;Textklassifizierung
solution: Experience Platform
title: Textklassifizierung in der Content and Commerce AI-API
description: Wenn der Textklassifizierungs-Service ein Textfragment erhält, kann er es in eine oder mehrere Kennzeichnungen klassifizieren. Die Klassifizierung kann einteilig, mehrteilig oder hierarchisch sein.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 5%

---

# Textklassifizierung

>[!NOTE]
>
>Content and Commerce AI befindet sich in der Beta-Phase. Die Dokumentation kann sich ändern.

Wenn der Textklassifizierungs-Service ein Textfragment erhält, kann er es in eine oder mehrere Kennzeichnungen klassifizieren. Die Klassifizierung kann einteilig, mehrteilig oder hierarchisch sein.

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anfrage klassifiziert Text aus einem Fragment basierend auf den in der Payload bereitgestellten Eingabeparametern. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

>[!CAUTION]
>
>`analyzer_id` bestimmt, welche [!DNL Sensei Content Framework] verwendet wird. Vergewissern Sie sich, dass Sie über die richtigen `analyzer_id` verfügen, bevor Sie Ihre Anfrage stellen. Wenden Sie sich an das Beta-Team von Content and Commerce AI , um Ihre `analyzer_id` für diesen Service zu erhalten.

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
| `analyzer_id` | Die [!DNL Sensei]-Service-ID, unter der Ihre Anfrage bereitgestellt wird. Diese ID bestimmt, welche der [!DNL Sensei Content Frameworks] verwendet werden. Wenden Sie sich für benutzerdefinierte Services an das KI-Team für Inhalte und Commerce, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `data` | Ein Array, das ein JSON-Objekt enthält, wobei jedes Objekt im Array ein Dokument darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, überschreiben die globalen Parameter, die außerhalb des `data`-Arrays angegeben werden. Alle verbleibenden Eigenschaften, die unten in dieser Tabelle beschrieben werden, können in `data` überschrieben werden. | Ja |
| `language` | Sprache des Eingabetextes. Der Standardwert lautet `en`. | Nein |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anfragetexts oder eine signierte URL für einen S3-Bucket ist. Der Standardwert für diese Eigenschaft ist `inline`. | Nein |
| `encoding` | Das Kodierungsformat des Eingabetextes. Dies kann `utf-8` oder `utf-16` sein. Der Standardwert für diese Eigenschaft ist `utf-8`. | Nein |
| `threshold` | Der Schwellenwert des Scores (0 bis 1), bei dessen Überschreitung die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Der Standardwert für diese Eigenschaft ist `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold` ist die Anzahl der zurückgegebenen Ergebnisse der niedrigere der beiden festgelegten Grenzwerte. Der Standardwert für diese Eigenschaft ist `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die übergeben werden sollen. Diese Eigenschaft erfordert ein gültiges JSON-Objekt, um zu funktionieren. | Nein |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wurde. Wenn diese nicht weitergegeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der vom Textklassifizierungs-Service verwendete Inhalt. Bei dem Inhalt kann es sich um Rohtext handeln (Content-Typ „inline„). <br> Wenn es sich bei dem Inhalt um eine Datei auf S3 (&#39;s3-Bucket&#39; Inhaltstyp) handelt, übergeben Sie die signierte URL. | Ja |

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
