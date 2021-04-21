---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: Handbuch zur Fehlerbehebung beim Profil in Echtzeit
topic-legacy: guide
type: Documentation
description: In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zum Echtzeit-Profil von Kunden sowie eine Anleitung zur Fehlerbehebung bei häufigen Fehlern beim Arbeiten mit Profil-Daten mit Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Handbuch zur Fehlerbehebung beim Profil in Echtzeit

In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zum Echtzeit-Profil von Kunden sowie eine Anleitung zur Fehlerbehebung für häufige Fehler. Weitere Informationen zu Fragen und zur Fehlerbehebung in Zusammenhang mit anderen Diensten in Adobe Experience Platform finden Sie im Handbuch [Experience Platform Fehlerbehebung](../landing/troubleshooting.md).

Mit [!DNL Real-time Customer Profile] können Sie eine ganzheitliche Ansicht jedes einzelnen Kunden anzeigen, indem Sie Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombinieren. Dadurch können Marketingexperten koordinierte, konsistente und relevante Erlebnisse für mehrere Kanal bereitstellen.

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zum Echtzeit-Profil von Kunden.

### Welche Daten werden für Echtzeit-Kundendaten akzeptiert?

Profil akzeptiert sowohl **record**- als auch **Zeitreihen**-Daten, solange die betreffenden Daten mindestens einen Identitätswert enthalten, der die Daten mit einer individuellen Person verknüpft.

Wie alle Plattformdienste erfordert Profil, dass seine Daten semantisch unter einem Experience Data Model (XDM)-Schema strukturiert sind. Dieses Schema muss wiederum eine **primäre Identität** definiert und für die Verwendung in Profil aktiviert sein.

Wenn Sie mit XDM nicht vertraut sind, sollten Sie sich mit dem [XDM overview](../xdm/home.md) vertraut machen, um weitere Informationen zu erhalten. Als Nächstes finden Sie im XDM-Benutzerhandbuch Anweisungen zum Festlegen von Identitätsfeldern [und [Aktivieren eines Schemas für Profil](../xdm/tutorials/create-schema-ui.md#profile).](../xdm/tutorials/create-schema-ui.md#identity-field)

### Wo werden Profil-Daten gespeichert?

Echtzeit-Kundendaten-Profil unterhält einen eigenen Datenspeicher (der als &quot;Profil-Store&quot;bezeichnet wird), der vom Data Lake mit anderen erfassten Plattformdaten getrennt ist.

### Wenn ich bereits Daten in Platform integriert habe, kann ich sie dann im Profil Store zur Verfügung stellen?

Wenn Daten in einen Dataset aufgenommen wurden, der kein Profil ist, müssen Sie diese Daten erneut in einen Datensatz mit aktiviertem Profil erfassen, damit sie im Profil-Store verfügbar sind. Es ist möglich, einen vorhandenen Datensatz zum Profil zu aktivieren. Daten, die vor dieser Konfiguration erfasst wurden, werden jedoch weiterhin nicht im Profil Store angezeigt.

Wenn Sie dem Datenspeicher zuvor erfasste Daten hinzufügen möchten, führen Sie das folgende [Tutorial zur Datenkonfiguration](./tutorials/dataset-configuration.md) durch, um einen neuen Datensatz zu erstellen oder einen vorhandenen Datensatz zu konvertieren, der zum Profil aktiviert werden soll, und erfassen Sie dann die gewünschten Daten erneut in diesen Datensatz.

### Wie kann ich meine erfassten Profil-Daten Ansicht haben?

Es gibt mehrere Methoden zum Anzeigen von Profil-Daten, je nachdem, ob Sie die API oder die Benutzeroberfläche verwenden.

#### Verwenden der API

Wenn Sie die IDs der Profil-Entitäten kennen, auf die Sie zugreifen möchten, können Sie den `/entities` (Profil-Zugriff)-Endpunkt in der Profil-API verwenden, um diese Entitäten nachzuschlagen. Weitere Informationen finden Sie im Abschnitt zu [Entitäten](./api/entities.md) im Entwicklerhandbuch.

Sie können auch die Adobe Experience Platform Segmentation Service API verwenden, um auf die einzelnen Profil von Kunden zuzugreifen, die sich für eine Segmentmitgliedschaft qualifiziert haben. Weitere Informationen finden Sie unter [Übersicht über den Segmentierungsdienst](../segmentation/home.md).

#### Verwenden der UI

In der Benutzeroberfläche &quot;Experience Platform&quot;können Sie auf der Registerkarte **[!UICONTROL Durchsuchen]** im Arbeitsbereich **[!UICONTROL Profil]** die Gesamtzahl der Profil und die Suche nach einzelnen Profilen anhand ihres Identitätswerts Ansicht haben. Weitere Informationen finden Sie im [Profil-Benutzerhandbuch](./ui/user-guide.md).

Sie können auch eine Liste Ihrer Segmente auf der Registerkarte **[!UICONTROL Durchsuchen]** im Arbeitsbereich **[!UICONTROL Segmente]** Ansicht haben. Nach Auswahl eines Segments wird ein Beispiel von Profilen angezeigt, die für dieses Segment qualifiziert sind. Sie können dann eines der aufgelisteten Profil auswählen, um deren Details Ansicht. Weitere Informationen finden Sie unter [Übersicht über die Segmentierungsbenutzeroberfläche](../segmentation/ui/overview.md).

## Fehlercodes

Im Folgenden finden Sie eine Liste von Fehlermeldungen, die Sie möglicherweise bei der Arbeit mit der Echtzeit-Client-Profil-API erhalten. Wenn der Fehler, auf den Sie stoßen, hier nicht aufgeführt ist, finden Sie ihn möglicherweise im allgemeinen [Handbuch zur Fehlerbehebung für Plattformen](../landing/troubleshooting.md).

### Schema des berechneten Attributs für den angegebenen Pfad konnte nicht nachgeschlagen werden

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Beim Erstellen eines neuen berechneten Attributs tritt dieser Fehler auf, wenn das System das in der Anforderungsnutzlast bereitgestellte Schema nicht finden konnte. Vergewissern Sie sich, dass Sie die richtige Mieter-ID in der Eigenschaft `path` der Payload angegeben haben und dass die Werte von `schema.name` ein gültiger Schema-Name sind.

Wenn Sie Ihre Pächter-ID nicht kennen, können Sie sie abrufen, indem Sie die Schritte im [Schema Registry-Entwicklerhandbuch](../xdm/api/getting-started.md) befolgen.

### Funktion mit demselben Namen ist bereits für das angegebene Schema oder definedOn vorhanden

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Beim Erstellen eines neuen berechneten Attributs tritt dieser Fehler auf, wenn die angegebene `name`-Eigenschaft bereits für das unter `schema.name` angegebene Schema verwendet wird. Ersetzen Sie den Wert durch einen eindeutigen Namen, bevor Sie ihn erneut versuchen.

### Das Rückgabeattribut des Ausdrucks ist nicht dasselbe wie das Schema des berechneten Schemas im XDM-Schema

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Beim Erstellen eines neuen berechneten Attributs tritt dieser Fehler auf, wenn die angegebene `name`-Eigenschaft bereits für das unter `schema.name` angegebene Schema verwendet wird. Ersetzen Sie den Wert durch einen eindeutigen Namen, bevor Sie ihn erneut versuchen.

### Ungültige Löschanforderung (Profil-Systemauftrag)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Dieser Fehler tritt auf, wenn eine ungültige Nutzlast für einen Löschsystemauftrag angegeben wird. Stellen Sie sicher, dass Sie unter der Eigenschaft `dataSetID` bzw. `batchID` eine gültige Dataset- oder Batch-ID angeben. Weitere Informationen finden Sie im Profil Developer Guide unter [Erstellen einer Löschanforderung](./api/profile-system-jobs.md#create-a-delete-request).

### Stapel nicht gefunden für Profil-Datensatz

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

Dieser Fehler tritt auf, wenn beim Versuch, eine Löschanforderung für Profil-Daten zu erstellen, kein gültiger Stapel gefunden werden konnte. Vergewissern Sie sich, dass Sie die richtige ID für einen Profil-aktivierten Datensatz eingegeben haben, bevor Sie es erneut versuchen.

### Das Projektionsziel wurde noch nicht erstellt

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Dieser Fehler tritt auf, wenn die in einer `POST /config/projections`-Anforderung angegebene `destinationId`-Anforderung ungültig ist. Überprüfen Sie vor dem erneuten Versuch, ob Sie eine gültige Ziel-ID angegeben haben. Gehen Sie zum Erstellen eines neuen Ziels wie im [Profil Developer Guide](./api/edge-projections.md#create-a-destination) beschrieben vor.

### Nicht unterstützter Medientyp

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Dieser Fehler tritt auf, wenn eine POST oder eine PUT-Anforderung mit einem ungültigen Content-Type-Header gesendet wird. Überprüfen Sie bei der Dublette, ob Sie einen gültigen Content-Type-Wert für den von Ihnen verwendeten Endpunkt angeben.

Die meisten Profil-Endpunkte akzeptieren &quot;application/json&quot;für ihren Content-Type-Header, mit folgenden Ausnahmen:

| Endpunkt | Inhaltstyp |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectsConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectsDestination+json; version=1 |
