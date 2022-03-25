---
keywords: Experience Platform; Erste Schritte; Content-Hilfe; Commerce-API; Content- und Commerce-API; Keyword-Extraktion; Keyword-Extraktion
solution: Intelligent Services
title: Keyword-Extraktion in der Inhalts- und Commerce-API
topic-legacy: Developer guide
description: Der Suchbegriffextraktionsdienst extrahiert bei der Bereitstellung eines Textdokuments automatisch Suchbegriffe oder Suchbegriffe, die den Betreff des Dokuments am besten beschreiben. Um Suchbegriffe zu extrahieren, wird eine Kombination aus benannten Algorithmen zur Identifikation von Entitäten (NER) und unbeaufsichtigten Keyword-Extraktion verwendet.
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 4%

---

# Keyword-Extraktion

>[!NOTE]
>
>[!DNL Content and Commerce AI] ist in der Beta-Phase. Die Dokumentation kann sich ändern.

Der Suchbegriffextraktionsdienst extrahiert bei der Bereitstellung eines Textdokuments automatisch Suchbegriffe oder Suchbegriffe, die den Betreff des Dokuments am besten beschreiben. Um Suchbegriffe zu extrahieren, wird eine Kombination aus benannten Algorithmen zur Identifikation von Entitäten (NER) und unbeaufsichtigten Keyword-Extraktion verwendet.

Die benannten Entitäten, die von [!DNL Content and Commerce AI] sind in der folgenden Tabelle aufgeführt:

| Entitätsname | Beschreibung |
| --- | --- |
| PERSON | Menschen, einschließlich fiktionaler. |
| NORP | Nationalitäten oder religiöse oder politische Gruppen. |
| GPE | Länder, Städte und Staaten. |
| LOC | Nicht-GPE-Orte, Gebirgszüge, Wasserkörper. |
| FAC | Gebäude, Flughäfen, Autobahnen, Brücken usw. |
| ORG | Unternehmen, Agenturen, Einrichtungen usw. |
| PRODUKT | Objekte, Fahrzeuge, Lebensmittel usw. (Keine Dienste.) |
| EREIGNIS | Benannte Hurrikane, Kämpfe, Kriege, Sportveranstaltungen usw. |
| WORK_OF_ART | Titel von Büchern, Liedern usw. |
| GESETZ | Spezifische Dokumente, die in Gesetze umgewandelt wurden. |
| SPRACHE | Jede benannte Sprache. |

>[!NOTE]
>
>Wenn Sie die Verarbeitung von PDF planen, überspringen Sie die Anweisungen für [PDF-Keyword-Extraktion](#pdf-extraction) in diesem Dokument. Außerdem wird die Unterstützung für zusätzliche Dateitypen wie docx, ppt und amd xml so eingestellt, dass sie zu einem späteren Zeitpunkt veröffentlicht werden.

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anfrage extrahiert Suchbegriffe aus einem Dokument basierend auf den in der Payload bereitgestellten Eingabeparametern.

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

Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

>[!CAUTION]
>
>`analyzer_id` bestimmt, [!DNL Sensei Content Framework] verwendet. Vergewissern Sie sich bitte, dass Sie über die richtige `analyzer_id` bevor Sie Ihre Anfrage stellen. Für den Suchbegriffextraktionsdienst muss die Variable `analyzer_id` Die ID lautet:
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
| `analyzer_id` | Die [!DNL Sensei] Dienst-ID, unter der Ihre Anfrage bereitgestellt wird. Diese ID bestimmt, welcher der [!DNL Sensei Content Frameworks] verwendet werden. Wenden Sie sich bei benutzerdefinierten Diensten an das KI-Team von Content and Commerce, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `data` | Ein Array, das ein JSON-Objekt mit jedem Objekt im Array enthält, das ein Dokument darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer Kraft, die außerhalb der `data` Array. Jede der anderen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, kann von innerhalb `data`. | Ja |
| `language` | Sprache des Eingabetexts. Der Standardwert lautet `en`. | Nein |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anfragetexts oder einer signierten URL für einen S3-Behälter ist. Der Standardwert für diese Eigenschaft lautet `inline`. | Ja |
| `encoding` | Das Kodierungsformat des Eingabetexts. Dies kann `utf-8` oder `utf-16`. Der Standardwert für diese Eigenschaft lautet `utf-8`. | Nein |
| `threshold` | Der Schwellenwert des Punktes (0 bis 1), über dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold`, ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Limits. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die weitergegeben werden sollen. Für diese Eigenschaft ist ein gültiges JSON-Objekt erforderlich, damit sie funktioniert. Siehe [Anhang](#appendix) für weitere Informationen zu den benutzerdefinierten Parametern. | Nein |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht übergeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der vom Suchbegriffextraktionsdienst verwendete Inhalt. Der Inhalt kann als Rohtext (&quot;inline&quot;-Inhaltstyp) verwendet werden. <br> Wenn der Inhalt eine Datei auf S3 ist (&#39;s3-bucket&#39; Inhaltstyp), übergeben Sie die signierte URL. Wenn Inhalt Teil des Anfragetexts ist, sollte die Liste der Datenelemente nur ein Objekt enthalten. Wenn mehr als ein Objekt übergeben wird, wird nur das erste Objekt verarbeitet. | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt ein JSON-Objekt zurück, das extrahierte Schlüsselwörter in der `response` Array.

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

## PDF-Keyword-Extraktion {#pdf-extraction}

Der Suchbegriffextraktionsdienst unterstützt PDF. Sie müssen jedoch eine neue Analyzer-ID für PDF-Dateien verwenden und den Dokumenttyp in PDF ändern. Weitere Informationen finden Sie im folgenden Beispiel.

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Anfrage extrahiert Suchbegriffe aus einem PDF-Dokument basierend auf den in der Payload bereitgestellten Eingabeparametern.

>[!CAUTION]
>
>`analyzer_id` bestimmt, [!DNL Sensei Content Framework] verwendet. Vergewissern Sie sich bitte, dass Sie über die richtige `analyzer_id` bevor Sie Ihre Anfrage stellen. Bei der PDF-Keyword-Extraktion wird die `analyzer_id` Die ID lautet:
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
| `analyzer_id` | Die [!DNL Sensei] Dienst-ID, unter der Ihre Anfrage bereitgestellt wird. Diese ID bestimmt, welcher der [!DNL Sensei Content Frameworks] verwendet werden. Wenden Sie sich bei benutzerdefinierten Diensten an das KI-Team von Content and Commerce, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `data` | Ein Array, das ein JSON-Objekt mit jedem Objekt im Array enthält, das ein Dokument darstellt. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer Kraft, die außerhalb der `data` Array. Jede der anderen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, kann von innerhalb `data`. | Ja |
| `language` | Sprache der Eingabe. Der Standardwert ist `en` (Englisch). | Nein |
| `content-type` | Wird verwendet, um den Typ des eingegebenen Inhalts anzugeben. Dies sollte auf `file`. | Ja |
| `encoding` | Das Kodierungsformat der Eingabe. Dies sollte auf `pdf`. Weitere Kodierungstypen werden zu einem späteren Zeitpunkt unterstützt. | Ja |
| `threshold` | Der Schwellenwert des Punktes (0 bis 1), über dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold`, ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Limits. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die weitergegeben werden sollen. Für diese Eigenschaft ist ein gültiges JSON-Objekt erforderlich, damit sie funktioniert. Siehe [Anhang](#appendix) für weitere Informationen zu den benutzerdefinierten Parametern. | Nein |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht übergeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Dies sollte auf `file`. | Ja |

**Antwort**

Eine erfolgreiche Antwort gibt ein JSON-Objekt zurück, das extrahierte Schlüsselwörter in der `response` Array.

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

Weitere Informationen und ein Beispiel für die Verwendung der PDF-Extraktion mit Anweisungen zum Einrichten, Bereitstellen und Integrieren des AEM Cloud Service. Besuchen Sie die [CCAI PDF Extraktions-Worker-GitHub-Repository](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## Anhang {#appendix}

Die folgende Tabelle enthält die verfügbaren Parameter, die in verwendet werden können `custom`.

| Name | Beschreibung | Obligatorisch |
| --- | --- | --- |
| `min-n` | Die Mindestanzahl von Wörtern, die für die Suchbegriffe erforderlich sind. | Nein |
| `entity-types` | Typen der zurückzugebenden Entitäten. Siehe die benannte Entitätserkennungstabelle am Anfang dieses Dokuments. | Nein |
