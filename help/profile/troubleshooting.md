---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: Handbuch zur Fehlerbehebung beim Echtzeit-Kundenprofil
type: Documentation
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Echtzeit-Kundenprofil sowie eine Anleitung zur Behebung gängiger Fehler beim Arbeiten mit Profildaten mit Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '1007'
ht-degree: 100%

---

# Handbuch zur Fehlerbehebung beim Echtzeit-Kundenprofil

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zum Echtzeit-Kundenprofil sowie eine Anleitung zur Behebung gängiger Fehler. Fragen und Fehlerbehebungen für andere Services in Adobe Experience Platform finden Sie im [Handbuch zur Fehlerbehebung in Experience Platform](../landing/troubleshooting.md).

Das [!DNL Real-Time Customer Profile] ermöglicht Ihnen eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen sowie anderen Kanälen miteinander kombiniert. So können Marketing-Fachleute über verschiedenste Kanäle hinweg koordinierte, konsistente und relevante Erlebnisse für Kundinnen und Kunden umsetzen.

## FAQs

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zum Echtzeit-Kundenprofil.

### Welche Arten von Daten werden beim Echtzeit-Kundenprofil akzeptiert?

Das Profil akzeptiert **Datensatz**- und **Zeitreihendaten**, sofern die betreffenden Daten mindestens einen Identitätswert enthalten, der die Daten mit einer eindeutigen Person verknüpft.

Wie alle Platform-Services ist es für das Profil erforderlich, dass seine Daten semantisch unter einem Experience-Datenmodell(XDM)-Schema strukturiert sind. Dieses Schema muss wiederum eine **primäre Identität** aufweisen, die für die Profilverwendung definiert und aktiviert ist.

Wenn Sie mit XDM nicht vertraut sind, sollten Sie sich zunächst die [XDM-Übersicht](../xdm/home.md) durchlesen, um mehr zu erfahren. Anschließend finden Sie im XDM-Benutzerhandbuch Anweisungen zum [Festlegen von Identitätsfeldern](../xdm/tutorials/create-schema-ui.md#identity-field) und [Aktivieren eines Schemas für Profil](../xdm/tutorials/create-schema-ui.md#profile).

### Wo werden Profildaten gespeichert?

Das Echtzeit-Kundenprofil unterhält einen eigenen Datenspeicher (der als „Profilspeicher“ bezeichnet wird), welcher vom Data Lake, der andere aufgenommene Platform-Daten enthält, getrennt ist.

### Wenn ich bereits Daten in Platform aufgenommen habe, kann ich sie dann im Profilspeicher verfügbar machen?

Wenn Daten in einen Nicht-Profil-Datensatz aufgenommen wurden, müssen Sie diese Daten erneut in einen profilaktivierten Datensatz aufnehmen, um sie im Profilspeicher verfügbar zu machen. Es ist möglich, einen vorhandenen Datensatz für das Profil zu aktivieren. Daten, die vor dieser Konfiguration aufgenommen wurden, werden jedoch nach wie vor nicht im Profilspeicher angezeigt.

Wenn Sie zuvor aufgenommene Daten zum Profilspeicher hinzufügen möchten, befolgen Sie die Anweisungen im [Tutorial zur Datensatzkonfiguration](./tutorials/dataset-configuration.md), um einen neuen Datensatz zu erstellen oder einen vorhandenen Datensatz zur Profilaktivierung zu konvertieren. Nehmen Sie dann die gewünschten Daten erneut in diesen Datensatz auf.

### Wie kann ich meine aufgenommenen Profildaten anzeigen?

Je nachdem, ob Sie die API oder die Benutzeroberfläche verwenden, gibt es mehrere Methoden zum Anzeigen von Profildaten.

#### Verwenden der API

Wenn Sie die IDs der Profilentitäten kennen, auf die Sie zugreifen möchten, können Sie den `/entities`-Endpunkt (Profilzugriff) in der Profil-API zum Suchen dieser Entitäten verwenden. Weiterführende Informationen finden Sie im Abschnitt zu [Entitäten](./api/entities.md) im Entwicklerhandbuch.

Sie können auch die Adobe Experience Platform Segmentation Service-API verwenden, um auf die individuellen Profile von Kundinnen und Kunden zuzugreifen, die sich für eine Segmentzugehörigkeit qualifiziert haben. Weiterführende Informationen finden Sie in der [Übersicht zum Segmentierungs-Service](../segmentation/home.md).

#### Verwenden der Benutzeroberfläche

In der Experience Platform-Benutzeroberfläche können Sie auf der Registerkarte **[!UICONTROL Durchsuchen]** im Arbeitsbereich **[!UICONTROL Profile]** die Gesamtzahl der Profile anzeigen und nach einzelnen Profilen anhand ihres Identitätswerts suchen. Weiterführende Informationen finden Sie im [Benutzerhandbuch für Profile](./ui/user-guide.md).

Sie können auch eine Liste Ihrer Segmente auf der Registerkarte **[!UICONTROL Durchsuchen]** im Arbeitsbereich **[!UICONTROL Segmente]** anzeigen. Nach Auswahl eines Segments wird ein Beispiel mit Profilen angezeigt, die für dieses Segment qualifiziert sind. Sie können dann eines dieser aufgelisteten Profile auswählen, um dessen Details anzuzeigen. Weiterführende Informationen finden Sie in der [Übersicht zur Segmentierungsbenutzeroberfläche](../segmentation/ui/overview.md).

## Fehler-Codes

Im Folgenden finden Sie eine Liste von Fehlermeldungen, die bei der Arbeit mit der Echtzeit-Kundenprofil-API auftreten können. Wenn der aufgetretene Fehler hier nicht aufgeführt ist, finden Sie ihn stattdessen möglicherweise im allgemeinen [Handbuch zur Fehlerbehebung bei Platform](../landing/troubleshooting.md).

### Schema des berechneten Attributs für angegebenen Pfad wurde nicht gefunden

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Beim Erstellen eines neuen berechneten Attributs tritt dieser Fehler auf, wenn das System das in der Anfrage-Payload angegebene Schema nicht finden konnte. Stellen Sie sicher, dass Sie die richtige Mandanten-ID in der `path`-Eigenschaft der Payload angegeben haben und dass es sich bei den Werten von `schema.name` um einen gültigen Schemanamen handelt.

Wenn Sie Ihre Mandanten-ID nicht kennen, können Sie sie abrufen, indem Sie die Schritte im [Entwicklerhandbuch zur Schemaregistrierung](../xdm/api/getting-started.md) befolgen.

### Funktion mit demselben Namen ist bereits für das angegebene Schema oder definedOn vorhanden

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Beim Erstellen eines neuen berechneten Attributs tritt dieser Fehler auf, wenn die `name`-Eigenschaft bereits für das unter `schema.name` angegebene Schema verwendet wird. Ersetzen Sie den Wert durch einen eindeutigen Namen, bevor Sie es erneut versuchen.

### Rückgabeschema des Ausdrucks ist nicht dasselbe wie das Schema des berechneten Attributs im XDM-Schema

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Beim Erstellen eines neuen berechneten Attributs tritt dieser Fehler auf, wenn die `name`-Eigenschaft bereits für das unter `schema.name` angegebene Schema verwendet wird. Ersetzen Sie den Wert durch einen eindeutigen Namen, bevor Sie es erneut versuchen.

### Ungültige Löschanfrage (Profilsystemauftrag)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Dieser Fehler tritt auf, wenn eine ungültige Payload für einen Löschsystemauftrag angegeben wird. Stellen Sie sicher, dass Sie eine gültige Datensatz- oder Batch-ID unter der `dataSetID`- bzw. `batchID`-Eigenschaft der Payload angeben. Weiterführende Informationen finden Sie im Entwicklerhandbuch für Profile im Abschnitt zum [Erstellen von Löschanfragen](./api/profile-system-jobs.md#create-a-delete-request).

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

Dieser Fehler tritt auf, wenn beim Versuch, eine Löschanfrage für Profildaten zu erstellen, kein gültiger Batch gefunden werden konnte. Vergewissern Sie sich, dass Sie die richtige ID für einen profilaktivierten Datensatz eingegeben haben, bevor Sie es erneut versuchen.

### Das Projektionsziel wurde noch nicht erstellt

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Dieser Fehler tritt auf, wenn der `destinationId`-Wert in einer `POST /config/projections`-Anfrage ungültig ist. Vergewissern Sie sich, dass Sie eine gültige Ziel-ID angegeben haben, bevor Sie es erneut versuchen. Um ein neues Ziel zu erstellen, befolgen Sie die im [Entwicklerhandbuch für Profile](./api/edge-projections.md#create-a-destination) beschriebenen Schritte.

### Nicht unterstützter Medientyp

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Dieser Fehler tritt auf, wenn eine POST- oder PUT-Anfrage mit einer Kopfzeile mit ungültigem Inhaltstyp gesendet wird. Vergewissern Sie sich, dass Sie einen gültigen Inhaltstypwert für den verwendeten Endpunkt angeben.

Die meisten Profil-Endpunkte akzeptieren „application/json“ für ihre Inhaltstyp-Kopfzeile, mit folgenden Ausnahmen:

| Endpunkt | Inhaltstyp |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
