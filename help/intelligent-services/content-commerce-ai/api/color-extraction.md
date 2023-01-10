---
keywords: Experience Platform; Erste Schritte; Inhaltsai; Commerce-API; Inhalts- und Commerce-API; Farbextraktion; Farbextraktion
solution: Experience Platform
title: Farbextraktion in der Inhalts- und Commerce-API
description: Der Farbextraktionsdienst kann, wenn er ein Bild erhält, das Histogramm der Pixelfarben berechnen und durch dominante Farben in Behälter sortieren.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 3%

---

# Farbextraktion

>[!NOTE]
>
>[!DNL Content and Commerce AI] ist in der Beta-Phase. Die Dokumentation kann sich ändern.

Der Farbextraktionsdienst kann, wenn er ein Bild erhält, ein Histogramm von Pixelfarben berechnen und diese anhand dominanter Farben in Behältern sortieren. Die Farben der Bildpixel werden in 40 vorherrschende Farben zusammengefasst, die für das Farbspektrum repräsentativ sind. Ein Histogramm mit Farbwerten wird dann unter diesen 40 Farben berechnet. Der Dienst weist zwei Varianten auf:

**Farbextraktion (Vollbild)**

Diese Methode extrahiert ein Farbhistogramm über das gesamte Bild.

**Farbextraktion (mit Maske)**

Diese Methode verwendet einen auf tiefem Lernen basierenden Vordergrundextraktor, um Objekte im Vordergrund zu identifizieren. Das Modell wird anhand eines Katalogs von E-Commerce-Bildern trainiert. Nachdem das Vordergrundobjekt extrahiert wurde, wird ein Histogramm über die dominanten Farben berechnet, wie zuvor beschrieben.

Das folgende Bild wurde in dem in diesem Dokument gezeigten Beispiel verwendet:

![Testbild](../images/QQAsset1.jpg)

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Beispielanfrage verwendet die Vollbildmethode für die Farbextraktion.

Die folgende Anfrage extrahiert Farben aus einem Bild basierend auf den in der Payload bereitgestellten Eingabeparametern. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispiel-Payload .

>[!CAUTION]
>
>`analyzer_id` bestimmt, [!DNL Sensei Content Framework] verwendet. Vergewissern Sie sich bitte, dass Sie über die richtige `analyzer_id` bevor Sie Ihre Anfrage stellen. Für den Farbextraktionsdienst muss die Variable `analyzer_id` Die ID lautet:
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
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
            "custom": {"exclude_mask": 1}
            }]
          }
      }
    ]
}'
```

| Eigenschaft | Beschreibung | Obligatorisch |
| --- | --- | --- |
| `analyzer_id` | Die [!DNL Sensei] Dienst-ID, unter der Ihre Anfrage bereitgestellt wird. Diese ID bestimmt, welcher der [!DNL Sensei Content Frameworks] verwendet werden. Wenden Sie sich bei benutzerdefinierten Diensten an das KI-Team von Content and Commerce, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `data` | Ein Array, das JSON-Objekte enthält. Jedes Objekt im Array stellt ein Bild dar. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer Kraft, die außerhalb der `data` Array. Jede der anderen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, kann von innerhalb `data`. | Ja |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht übergeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der vom Farbextraktionsdienst zu analysierende Inhalt. Falls das Bild Teil des Anfrageinhalts ist, verwenden Sie `-F file=@<filename>` im curl -Befehl, um das Bild zu übergeben, wobei dieser Parameter als leere Zeichenfolge beibehalten wird. <br> Wenn das Bild eine Datei auf S3 ist, übergeben Sie die signierte URL. Wenn der Inhalt Teil des Anfragetexts ist, sollte die Liste der Datenelemente nur ein Objekt enthalten. Wenn mehr als ein Objekt übergeben wird, wird nur das erste Objekt verarbeitet. | Ja |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anfragetexts oder einer signierten URL für einen S3-Behälter ist. Der Standardwert für diese Eigenschaft lautet `inline`. | Nein |
| `encoding` | Das Dateiformat des Eingabebilds. Derzeit können nur JPEG- und PNG-Bilder verarbeitet werden. Der Standardwert für diese Eigenschaft lautet `jpeg`. | Nein |
| `threshold` | Der Schwellenwert des Punktes (0 bis 1), über dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert `0` , um alle Ergebnisse zurückzugeben. Bei Verwendung in Verbindung mit `threshold`, ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Limits. Der Standardwert für diese Eigenschaft lautet `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die weitergegeben werden sollen. | Nein |
| `historic-metadata` | Ein Array, das Metadaten übergeben werden kann. | Nein |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der extrahierten Farben zurück. Jede Farbe wird durch eine `feature_value` -Schlüssel, der die folgenden Informationen enthält:

- Ein Farbname
- Der Prozentsatz, in dem diese Farbe im Verhältnis zum Bild angezeigt wird
- Der RGB-Wert der Farbe

Im ersten Beispielobjekt unten wird die `feature_value` von `White,0.59,251,251,243` bedeutet, dass die gefundenen Farben weiß sind, weiß in 59 % des Bildes gefunden wird und einen RGB-Wert von 251.251.243 hat.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `content_id` | Der Name des Bildes, das in Ihre Bildanforderung hochgeladen wurde. |
| `feature_value` | Ein Array, dessen Objekte Schlüssel mit demselben Eigenschaftsnamen enthalten. Diese Schlüssel enthalten eine Zeichenfolge, die den Farbnamen darstellt. Ein Prozentsatz dieser Farbe wird in Bezug auf das in der Variablen `content_id`und den RGB-Wert der Farbe. |
