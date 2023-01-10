---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API
title: Handbuch zur Fehlerbehebung bei Echtzeit-Kundenprofilen
type: Documentation
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Echtzeit-Kundenprofil sowie eine Anleitung zur Fehlerbehebung bei häufigen Fehlern beim Arbeiten mit Profildaten mit Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 3%

---

# Handbuch zur Fehlerbehebung bei Echtzeit-Kundenprofilen

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Echtzeit-Kundenprofil sowie eine Anleitung zur Fehlerbehebung bei häufigen Fehlern. Fragen und Antworten zur Fehlerbehebung bei anderen Diensten in Adobe Experience Platform finden Sie im Abschnitt [Handbuch zur Fehlerbehebung bei Experience Platformen](../landing/troubleshooting.md).

Das [!DNL Real-Time Customer Profile] ermöglicht Ihnen eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. Dadurch können Marketing-Experten koordinierte, konsistente und relevante Erlebnisse für Kunden über mehrere Kanäle hinweg bereitstellen.

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zum Echtzeit-Kundenprofil.

### Welche Daten werden für das Echtzeit-Kundenprofil akzeptiert?

Das Profil akzeptiert beide **record** und **Zeitreihen** Daten, sofern die betreffenden Daten mindestens einen Identitätswert enthalten, der die Daten mit einer eindeutigen Person verknüpft.

Wie alle Platform-Dienste erfordert Profil, dass seine Daten semantisch unter einem Experience-Datenmodell (XDM)-Schema strukturiert sind. Dieses Schema muss wiederum eine **primäre Identität** definiert und für die Verwendung in Profil aktiviert sein.

Wenn Sie XDM nicht kennen, beginnen Sie mit dem [XDM-Übersicht](../xdm/home.md) , um mehr zu erfahren. Als Nächstes finden Sie im XDM-Benutzerhandbuch Anweisungen zum [Identitätsfelder festlegen](../xdm/tutorials/create-schema-ui.md#identity-field) und [Schema für Profil aktivieren](../xdm/tutorials/create-schema-ui.md#profile).

### Wo werden Profildaten gespeichert?

Das Echtzeit-Kundenprofil unterhält einen eigenen Datenspeicher (der als &quot;Profilspeicher&quot;bezeichnet wird), der vom Data Lake getrennt ist, der andere aufgenommene Platform-Daten enthält.

### Wenn ich bereits Daten in Platform erfasst habe, kann ich sie dann im Profilspeicher verfügbar machen?

Wenn Daten in einen Nicht-Profil-Datensatz aufgenommen wurden, müssen Sie diese Daten erneut in einen Profil-aktivierten Datensatz erfassen, um ihn im Profilspeicher verfügbar zu machen. Es ist möglich, einen vorhandenen Datensatz für Profil zu aktivieren. Daten, die vor dieser Konfiguration erfasst wurden, werden jedoch weiterhin nicht im Profilspeicher angezeigt.

Wenn Sie zuvor erfasste Daten zum Profilspeicher hinzufügen möchten, befolgen Sie die Anweisungen unter [Tutorial zur Datensatzkonfiguration](./tutorials/dataset-configuration.md) , um einen neuen Datensatz zu erstellen oder einen vorhandenen Datensatz zu konvertieren, damit er für Profil aktiviert werden kann, und dann die gewünschten Daten erneut in diesen Datensatz zu erfassen.

### Wie kann ich meine erfassten Profildaten anzeigen?

Je nachdem, ob Sie die API oder die Benutzeroberfläche verwenden, gibt es mehrere Methoden zum Anzeigen von Profildaten.

#### Verwenden der API

Wenn Sie die IDs der Profilentitäten kennen, auf die Sie zugreifen möchten, können Sie die `/entities` (Profilzugriff) in der Profil-API zum Nachschlagen dieser Entitäten. Siehe Abschnitt zu [entity](./api/entities.md) im Entwicklerhandbuch für weitere Informationen.

Sie können auch die Adobe Experience Platform Segmentation Service-API verwenden, um auf die individuellen Profile von Kunden zuzugreifen, die sich für eine Segmentzugehörigkeit qualifiziert haben. Siehe [Übersicht über den Segmentierungsdienst](../segmentation/home.md) für weitere Informationen.

#### Verwenden der Benutzeroberfläche

In der Experience Platform-Benutzeroberfläche wird die **[!UICONTROL Durchsuchen]** im **[!UICONTROL Profile]** In Workspace können Sie die Gesamtzahl der Profile anzeigen und nach einzelnen Profilen anhand ihres Identitätswerts suchen. Siehe [Profil-Benutzerhandbuch](./ui/user-guide.md) für weitere Informationen.

Sie können auch eine Liste Ihrer Segmente unter dem **[!UICONTROL Durchsuchen]** im **[!UICONTROL Segmente]** Arbeitsbereich. Nach Auswahl eines Segments wird ein Beispiel mit Profilen angezeigt, die für dieses Segment qualifiziert sind. Sie können dann eines dieser aufgelisteten Profile auswählen, um dessen Details anzuzeigen. Siehe [Übersicht über die Segmentierungsbenutzeroberfläche](../segmentation/ui/overview.md) für weitere Informationen.

## Fehlercodes

Im Folgenden finden Sie eine Liste von Fehlermeldungen, die bei der Arbeit mit der Echtzeit-Kundenprofil-API auftreten können. Wenn der aufgetretene Fehler hier nicht aufgeführt ist, finden Sie ihn möglicherweise im allgemeinen [Handbuch zur Fehlerbehebung bei Platform](../landing/troubleshooting.md) anstatt.

### Schema des berechneten Attributs für den angegebenen Pfad konnte nicht nachgeschlagen werden

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Beim Erstellen eines neuen berechneten Attributs tritt dieser Fehler auf, wenn das System das in der Anfrage-Payload bereitgestellte Schema nicht finden konnte. Stellen Sie sicher, dass Sie die richtige Mandantenkennung in der Payload angegeben haben. `path` -Eigenschaft und dass die Werte von `schema.name` ist ein gültiger Schemaname.

Wenn Sie Ihre Mandantenkennung nicht kennen, können Sie sie abrufen, indem Sie die Schritte im Abschnitt [Entwicklerhandbuch zur Schema Registry](../xdm/api/getting-started.md).

### Funktion mit demselben Namen ist bereits für das angegebene Schema oder definedOn vorhanden

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Beim Erstellen eines neuen berechneten Attributs tritt dieser Fehler auf, wenn die `name` -Eigenschaft bereits für das Schema verwendet wird, das unter `schema.name`. Ersetzen Sie den Wert durch einen eindeutigen Namen, bevor Sie es erneut versuchen.

### Das Rückgabeschema des Ausdrucks ist nicht dasselbe wie das Schema des berechneten Attributs im XDM-Schema

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Beim Erstellen eines neuen berechneten Attributs tritt dieser Fehler auf, wenn die `name` -Eigenschaft bereits für das Schema verwendet wird, das unter `schema.name`. Ersetzen Sie den Wert durch einen eindeutigen Namen, bevor Sie es erneut versuchen.

### Ungültige Löschanfrage (Profilsystemauftrag)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Dieser Fehler tritt auf, wenn eine ungültige Payload für einen Löschsystemauftrag bereitgestellt wird. Stellen Sie sicher, dass Sie eine gültige Datensatz- oder Batch-ID unter der Payload angeben. `dataSetID` oder `batchID` -Eigenschaft. Siehe Abschnitt zu [Löschanfrage erstellen](./api/profile-system-jobs.md#create-a-delete-request) Weitere Informationen finden Sie im Entwicklerhandbuch für Profile .

### Batch für Profildatensatz nicht gefunden

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

Dieser Fehler tritt auf, wenn beim Versuch, eine Löschanfrage für Profildaten zu erstellen, kein gültiger Batch gefunden werden konnte. Vergewissern Sie sich, dass Sie die richtige ID für einen Profil-aktivierten Datensatz eingegeben haben, bevor Sie es erneut versuchen.

### Das Projektionsziel wurde noch nicht erstellt

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Dieser Fehler tritt auf, wenn die `destinationId` in `POST /config/projections` -Anfrage ist ungültig. Vergewissern Sie sich, dass Sie eine gültige Ziel-ID angegeben haben, bevor Sie es erneut versuchen. Um ein neues Ziel zu erstellen, führen Sie die Schritte aus, die im Abschnitt [Entwicklerhandbuch für Profile](./api/edge-projections.md#create-a-destination).

### Nicht unterstützter Medientyp

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Dieser Fehler tritt auf, wenn eine POST- oder PUT-Anfrage mit einer ungültigen Content-Type-Kopfzeile gesendet wird. Überprüfen Sie, ob Sie einen gültigen Content-Type-Wert für den verwendeten Endpunkt angeben.

Die meisten Endpunkte des Profils akzeptieren &quot;application/json&quot;für ihre Kopfzeile vom Typ &quot;Content&quot;, mit folgenden Ausnahmen:

| Endpunkt | Inhaltstyp |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projektionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projektionDestination+json; version=1 |
