---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;color extraction;Color extraction
solution: Experience Platform, Intelligent Services
title: Extraktion
topic: Developer guide
description: Der Dienst für Extraktion von Farben kann, wenn ein Bild gegeben wird, das Histogramm der Pixelfarben berechnen und durch vorherrschende Farben in Behältern sortieren.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---


# Extraktion

>[!NOTE]
>
>[!DNL Content and Commerce AI] in der Betaphase enthalten. Die Dokumentation kann geändert werden.

Der Dienst für Extraktion von Farben kann ein Histogramm von Pixelfarben berechnen und durch vorherrschende Farben in Behältern sortieren. Die Farben in den Bildpixeln werden zu 40 vorherrschenden Farben zusammengefasst, die für das Farbspektrum repräsentativ sind. Ein Histogramm mit Farbwerten wird dann unter diesen 40 Farben berechnet. Der Dienst hat zwei Varianten:

**Extraktion (Vollbild)**

Diese Methode extrahiert ein Farbhistogramm über das gesamte Bild.

**Extraktion (mit Maske)**

Diese Methode verwendet einen tief lernenden Vordergrundextraktor, um Objekte im Vordergrund zu identifizieren. Das Modell wird auf einem Katalog von E-Commerce-Bildern trainiert. Sobald das Vordergrundobjekt extrahiert wurde, wird ein Histogramm über die dominanten Farben berechnet, wie zuvor beschrieben.

In dem in diesem Dokument gezeigten Beispiel wurde folgende Abbildung verwendet:

![Testbild](../images/QQAsset1.jpg)

**API-Format**

```http
POST /services/v1/predict
```

**Anfrage**

Die folgende Beispielanforderung verwendet die Vollbildmethode für die Extraktion von Farben.

Die folgende Anforderung extrahiert Farben aus einem Bild basierend auf den in der Payload bereitgestellten Eingabeparametern. Weitere Informationen zu den angezeigten Eingabeparametern finden Sie in der Tabelle unter der Beispielpayload.

>[!CAUTION]
>
>`analyzer_id` bestimmt, welche verwendet [!DNL Sensei Content Framework] wird. Vergewissern Sie sich bitte, dass Sie über die erforderlichen Informationen verfügen, `analyzer_id` bevor Sie Ihre Anfrage bearbeiten. Für den Extraktion-Dienst lautet die `analyzer_id` ID:
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
| `analyzer_id` | Die [!DNL Sensei] Dienst-ID, unter der Ihre Anforderung bereitgestellt wird. Mit dieser ID wird festgelegt, welche der Variablen verwendet [!DNL Sensei Content Frameworks] werden. Wenden Sie sich bei benutzerdefinierten Diensten an das Content and Commerce AI-Team, um eine benutzerdefinierte ID einzurichten. | Ja |
| `application-id` | Die ID der erstellten Anwendung. | Ja |
| `data` | Ein Array, das JSON-Objekte enthält. Jedes Objekt im Array stellt ein Bild dar. Alle Parameter, die als Teil dieses Arrays übergeben werden, setzen die globalen Parameter außer dem `data` Array außer Kraft. Die übrigen Eigenschaften, die unten in dieser Tabelle aufgeführt sind, können von innen aus überschrieben werden `data`. | Ja |
| `content-id` | Die eindeutige ID für das Datenelement, das in der Antwort zurückgegeben wird. Wenn dies nicht weitergegeben wird, wird eine automatisch generierte ID zugewiesen. | Nein |
| `content` | Der vom Extraktion-Dienst zu analysierende Inhalt. In dem Ereignis, dass das Bild zum Anforderungstext gehört, verwenden Sie `-F file=@<filename>` den Befehl curl, um das Bild zu übergeben, wobei dieser Parameter als leere Zeichenfolge hinterlegt wird. <br> Wenn das Bild eine Datei auf S3 ist, übergeben Sie die signierte URL. Wenn der Inhalt zum Anforderungstext gehört, sollte die Liste der Datenelemente nur ein Objekt enthalten. Wenn mehr als ein Objekt übergeben wird, wird nur das erste Objekt verarbeitet. | Ja |
| `content-type` | Wird verwendet, um anzugeben, ob die Eingabe Teil des Anforderungstextes oder einer signierten URL für einen S3-Behälter ist. Die Standardeinstellung für diese Eigenschaft ist `inline`. | Nein |
| `encoding` | Das Dateiformat des Eingabebilds. Derzeit können nur JPEG- und PNG-Bilder verarbeitet werden. Die Standardeinstellung für diese Eigenschaft ist `jpeg`. | Nein |
| `threshold` | Der Schwellenwert des Ergebnisses (0 bis 1), ab dem die Ergebnisse zurückgegeben werden müssen. Verwenden Sie den Wert, `0` um alle Ergebnisse zurückzugeben. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `top-N` | Die Anzahl der zurückzugebenden Ergebnisse (darf keine negative Ganzzahl sein). Verwenden Sie den Wert, `0` um alle Ergebnisse zurückzugeben. Bei gleichzeitiger Verwendung `threshold`ist die Anzahl der zurückgegebenen Ergebnisse die niedrigere der beiden festgelegten Grenzwerte. Die Standardeinstellung für diese Eigenschaft ist `0`. | Nein |
| `custom` | Alle benutzerdefinierten Parameter, die übergeben werden sollen. | Nein |
| `historic-metadata` | Ein Array, an das Metadaten übergeben werden können. | Nein |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der extrahierten Farben zurück. Jede Farbe wird durch einen `feature_value` Schlüssel dargestellt, der die folgenden Informationen enthält:

- Ein Farbname
- Der Prozentsatz, in dem diese Farbe im Verhältnis zum Bild angezeigt wird
- Der RGB-Wert der Farbe

Im ersten Beispielobjekt unten ist der Wert `feature_value` von `White,0.59,251,251,243` bedeutet, dass die gefundene Farbe weiß ist, Weiß in 59 % des Bildes und hat einen RGB-Wert von 251.251.243.

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
| `content_id` | Der Name des Bilds, das in Ihrer POST hochgeladen wurde. |
| `feature_value` | Ein Array, dessen Objekte Schlüssel mit demselben Eigenschaftennamen enthalten. Diese Schlüssel enthalten eine Zeichenfolge, die den Farbnamen darstellt, einen Prozentsatz, den diese Farbe im Verhältnis zum gesendeten Bild `content_id`und den RGB-Wert der Farbe angibt. |
