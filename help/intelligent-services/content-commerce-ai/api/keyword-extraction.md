---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: Suchbegriff-Extraktion
topic: Developer guide
description: Der Suchbegriff-Extraktion-Dienst extrahiert automatisch Suchbegriffe oder Schlüsselbegriffe, die das Dokument am besten beschreiben, wenn er ein Textfeld erhält. Um Suchbegriffe zu extrahieren, wird eine Kombination aus benannten Algorithmen zur Unternehmenserkennung (NER) und unbeaufsichtigten Suchbegriffserkennung (Keyword Extraktion) verwendet.
translation-type: tm+mt
source-git-commit: e397711baf31092402de83b826887ebef16321eb
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 4%

---


# Suchbegriff-Extraktion

>[!NOTE]
>
>[!DNL Content and Commerce AI] ist in der Betaphase enthalten. Die Dokumentation kann geändert werden.

Der Suchbegriff-Extraktion-Dienst extrahiert automatisch Suchbegriffe oder Schlüsselbegriffe, die das Dokument am besten beschreiben, wenn er ein Textfeld erhält. Um Suchbegriffe zu extrahieren, wird eine Kombination aus benannten Algorithmen zur Unternehmenserkennung (NER) und unbeaufsichtigten Suchbegriffserkennung (Keyword Extraktion) verwendet.

Die benannten Entitäten, die von erkannt werden, [!DNL Content and Commerce AI] sind in der folgenden Tabelle aufgeführt:

| Entitätsname | Beschreibung |
| --- | --- |
| PERSON | Leute, einschließlich fiktiv. |
| NORP | Nationalitäten oder religiöse oder politische Gruppen. |
| GPE | Länder, Städte und Staaten. |
| LOC | Nicht-GPE-Standorte, Bergketten, Wasserkörper. |
| FAC | Gebäude, Flughäfen, Autobahnen, Brücken usw. |
| ORG | Firmen, Agenturen, Einrichtungen usw. |
| PRODUKT | Objekte, Fahrzeuge, Lebensmittel usw. (Keine Dienstleistungen.) |
| EREIGNIS | Benannte Hurrikane, Kämpfe, Kriege, Ereignisse usw. |
| WORK_OF_ART | Titel von Büchern, Liedern usw. |
| GESETZ | Benannte Dokumente, die in Gesetze umgewandelt wurden. |
| SPRACHE | Jede benannte Sprache. |

>[!NOTE]
>
>Wenn Sie die Verarbeitung von PDF-Dateien planen, gehen Sie in diesem Dokument zu den Anweisungen für die Extraktion [von](#pdf-extraction) PDF-Schlüsselwörtern. Darüber hinaus wird die Unterstützung für weitere Dateitypen wie &quot;docx&quot;, &quot;ppt&quot;und &quot;amd xml&quot;so eingestellt, dass sie zu einem späteren Zeitpunkt veröffentlicht wird.

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anforderung extrahiert Suchbegriffe aus einem Dokument basierend auf den in der Nutzlast bereitgestellten Eingabeparametern.

Vereinfachtes JSON der Eingabedatei:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispielpayload.

>[!CAUTION]
>
>`analyzer_id` bestimmt, welche verwendet [!DNL Sensei Content Framework] wird. Vergewissern Sie sich bitte, dass Sie über die erforderlichen Informationen verfügen, `analyzer_id` bevor Sie Ihre Anfrage bearbeiten. Für den Suchbegriff-Extraktion-Dienst lautet die `analyzer_id` ID:
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

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
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
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
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anforderungstextes oder einer signierten URL für einen S3-Behälter ist. Die Standardeinstellung für diese Eigenschaft ist `inline`. | Ja |
| `encoding` | Das Kodierungsformat des Eingabetexts. Das kann sein `utf-8` oder `utf-16`. Die Standardeinstellung für diese Eigenschaft ist `utf-8`. | Nein |
| `threshold` | Der Schwellenwert des Ergebnisses (0 bis 1), ab dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert, `0` um alle Ergebnisse zurückzugeben. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert, `0` um alle Ergebnisse zurückzugeben. Bei gleichzeitiger Verwendung `threshold`ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Grenzwerte. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die übergeben werden sollen. Für diese Eigenschaft ist ein gültiges JSON-Objekt erforderlich, um zu funktionieren. Weitere Informationen zu den benutzerdefinierten Parametern finden Sie im [Anhang](#appendix) . | Nein |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht weitergegeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der vom Suchbegriff-Extraktion-Dienst verwendete Inhalt. Der Inhalt kann als Rohtext (&quot;inline&quot;-Inhaltstyp) verwendet werden. <br> Wenn es sich bei dem Inhalt um eine Datei unter S3 handelt (&#39;s3-bucket&#39; Content-Typ), übergeben Sie die signierte URL. Wenn der Inhalt Teil des Anforderungskörpers ist, sollte die Liste der Datenelemente nur ein Objekt enthalten. Wenn mehr als ein Objekt übergeben wird, wird nur das erste Objekt verarbeitet. | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt ein JSON-Objekt zurück, das extrahierte Suchbegriffe im `response` Array enthält.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## PDF-Suchbegriff-Extraktion {#pdf-extraction}

Der Keyword-Extraktion-Dienst unterstützt PDFs. Sie müssen jedoch eine neue AnalyzerID für PDF- verwenden und den Dokument in PDF ändern. Weitere Informationen finden Sie im Beispiel unten.

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anforderung extrahiert Suchbegriffe aus einem PDF-Dokument basierend auf den in der Payload bereitgestellten Eingabeparametern.

>[!CAUTION]
>
>`analyzer_id` bestimmt, welche verwendet [!DNL Sensei Content Framework] wird. Vergewissern Sie sich bitte, dass Sie über die erforderlichen Informationen verfügen, `analyzer_id` bevor Sie Ihre Anfrage bearbeiten. Bei der Extraktion des PDF-Suchbegriffs lautet die `analyzer_id` ID:
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| Eigenschaft | Beschreibung | Obligatorisch |
| --- | --- | --- |
| `analyzer_id` | Die [!DNL Sensei] Dienst-ID, unter der Ihre Anforderung bereitgestellt wird. Mit dieser ID wird festgelegt, welche der Variablen verwendet [!DNL Sensei Content Frameworks] werden. Wenden Sie sich bei benutzerdefinierten Diensten an das Content and Commerce AI-Team, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `data` | Ein Array, das ein JSON-Objekt mit jedem Objekt im Array enthält, das ein Dokument darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer dem `data` Array außer Kraft. Die übrigen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, können von innen aus überschrieben werden `data`. | Ja |
| `language` | Sprache der Eingabe. The default value is `en` (english). | Nein |
| `content-type` | Dient zur Angabe des Eingabeinhaltstyps. Dies sollte auf `file`festgelegt werden. | Ja |
| `encoding` | Das Kodierungsformat der Eingabe. Dies sollte auf `pdf`festgelegt werden. Weitere Kodierungstypen werden zu einem späteren Zeitpunkt unterstützt. | Ja |
| `threshold` | Der Schwellenwert des Ergebnisses (0 bis 1), ab dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert, `0` um alle Ergebnisse zurückzugeben. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert, `0` um alle Ergebnisse zurückzugeben. Bei gleichzeitiger Verwendung `threshold`ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Grenzwerte. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die übergeben werden sollen. Für diese Eigenschaft ist ein gültiges JSON-Objekt erforderlich, um zu funktionieren. Weitere Informationen zu den benutzerdefinierten Parametern finden Sie im [Anhang](#appendix) . | Nein |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht weitergegeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Dies sollte auf `file`festgelegt werden. | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt ein JSON-Objekt zurück, das extrahierte Suchbegriffe im `response` Array enthält.

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

Weitere Informationen und ein Beispiel zur Verwendung der PDF-Extraktion mit Anweisungen zum Einrichten, Bereitstellen und Integrieren des AEM Cloud-Dienstes. Besuchen Sie das [CCAI PDF Extraktion Worker-github-Repository](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## Anhang {#appendix}

Die folgende Tabelle enthält die verfügbaren Parameter, die von innen verwendet werden können `custom`.

| Name | Beschreibung | Obligatorisch |
| --- | --- | --- |
| `min-n` | Die Mindestanzahl von Wörtern, die in den Suchbegriffen erforderlich sind. | Nein |
| `entity-types` | Typen der zurückzugebenden Entitäten. Siehe die benannte Entitätserkennungstabelle zu Beginn dieses Dokuments. | Nein |