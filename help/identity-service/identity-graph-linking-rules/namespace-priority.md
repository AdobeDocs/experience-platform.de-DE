---
title: Namespace-Priorität
description: Erfahren Sie mehr über die Namespace-Priorität in Identity Service.
badge: Beta
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 5674309e4e8f17ad4c951ec4a5cb0cbc0a15ab03
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 2%

---

# Namespace-Priorität

>[!AVAILABILITY]
>
>Diese Funktion ist noch nicht verfügbar. Das Betaprogramm für Regeln zur Identitätsdiagrammverlinkung wird voraussichtlich im Juli für Entwicklungs-Sandboxes beginnen. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zu den Teilnahmekriterien zu erhalten.

Jede Kundenimplementierung ist einzigartig und auf die Ziele eines bestimmten Unternehmens zugeschnitten. Daher variiert die Bedeutung eines bestimmten Namespace von Kunde zu Kunde. Beispiele aus der realen Welt:

* Auf der einen Seite könnten Sie den E-Mail-Namespace als eine Entität einer Person betrachten und somit pro Person eindeutig sein. Andererseits könnte ein anderer Kunde den E-Mail-Namespace als unzuverlässige Kennung betrachten und daher zulassen, dass eine einzelne CRM-ID mit mehreren Identitäten mit dem E-Mail-Namespace verknüpft wird.
* Sie können das Online-Verhalten mithilfe des Namespace &quot;Anmelde-ID&quot;erfassen. Diese Anmelde-ID kann eine 1:1-Beziehung zur CRM-ID aufweisen, die dann Attribute aus einem CRM-System speichert und als der wichtigste Namespace betrachtet werden kann. In diesem Fall bestimmen Sie dann, dass der CRM-ID-Namespace eine genauere Darstellung einer Person darstellt, während der Anmelde-ID-Namespace der zweitwichtigste ist.

Sie müssen im Identity Service Konfigurationen vornehmen, die die Wichtigkeit Ihrer Namespaces widerspiegeln, da dies Einfluss darauf hat, wie Profile gebildet und segmentiert werden.

## Legen Sie Ihre Prioritäten fest

Die Bestimmung der Namespace-Priorität basiert auf den folgenden Faktoren:

### Identitätsdiagrammstruktur

Wenn das strukturierte Diagramm Ihres Unternehmens eine Ebene hat, sollte die Namespace-Priorität dies widerspiegeln, damit die richtigen Links im Falle eines Diagrammausfalls entfernt werden.

>[!TIP]
>
>* &quot;Diagrammausfall&quot;bezieht sich auf Szenarien, in denen versehentlich mehrere unterschiedliche Profile zu einem Identitätsdiagramm zusammengeführt werden.
>
>* Ein Diagramm mit Ebenen bezieht sich auf Identitätsdiagramme mit mehreren Ebenen von Links. Sehen Sie sich das folgende Bild an, um ein Beispiel für ein Diagramm mit drei Ebenen anzuzeigen.

![Diagramm der Diagrammebenen](../images/namespace-priority/graph-layers.png)

### Semantische Bedeutung des Namespace

Eine Identität stellt ein Objekt der realen Welt dar. Im Identitätsdiagramm werden drei Objekte dargestellt. In der Reihenfolge ihrer Bedeutung sind sie:

* Personen (geräteübergreifend, E-Mail, Telefonnummer)
* Hardwaregerät
* Webbrowser (Cookie)

Personen-Namespaces sind im Vergleich zu Hardwaregeräten (wie IDFA, GAID), die im Vergleich zu Webbrowsern relativ unveränderlich sind, relativ unveränderlich. Grundsätzlich sind Sie (die Person) immer eine Einheit, die über mehrere Hardwaregeräte (Smartphone, Laptop, Tablet usw.) und mehrere Browser (Google Chrome, Safari, FireFox usw.) verfügen kann.

Eine andere Möglichkeit, dieses Thema anzugehen, ist die Kardinalität. Wie viele Identitäten werden für eine bestimmte Entität erstellt? In den meisten Fällen verfügt eine Person über eine CRM-ID, eine Handvoll Hardware-Geräte-IDs (IDFA/GAID-Resets sollten nicht oft auftreten) und sogar über mehr Cookies (eine Person könnte möglicherweise mehrere Geräte durchsuchen, den Inkognito-Modus verwenden oder Cookies jederzeit zurücksetzen). Im Allgemeinen **Eine niedrigere Kardinalität zeigt einen Namespace mit einem höheren Wert an**.

## Validieren der Namespace-Prioritätseinstellungen

Sobald Sie eine Vorstellung davon haben, wie Sie Ihre Namespaces priorisieren, können Sie das Tool zur Diagrammsimulation verwenden, um verschiedene Szenarien für die Diagrammreduzierung zu testen und sicherzustellen, dass Ihre Prioritätskonfigurationen die erwarteten Diagrammergebnisse zurückgeben. Weitere Informationen finden Sie im Handbuch zur Verwendung der [Tool zur Diagrammsimulation](./graph-simulation.md).

## Namespace-Priorität konfigurieren

Die Namespace-Priorität kann mithilfe von [!UICONTROL Identitätseinstellungen]. Im [!UICONTROL Identitätseinstellungen] -Schnittstelle verwenden, können Sie einen Namespace per Drag-and-Drop verschieben, um dessen relative Bedeutung zu bestimmen.

>[!IMPORTANT]
>
>Sie können Geräte-/Cookie-Namespaces nicht den Personen-Namespaces vorziehen. Diese Einschränkung stellt sicher, dass keine Fehlkonfigurationen auftreten.

## Verwendung der Namespace-Priorität

Derzeit beeinflusst die Namespace-Priorität das Systemverhalten des Echtzeit-Kundenprofils. Das folgende Diagramm zeigt dieses Konzept. Weitere Informationen finden Sie im Handbuch unter [Architekturdiagramme für Adobe Experience Platform und Anwendungen](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![Abbildung des Anwendungsbereichs der Namespace-Priorität](../images/namespace-priority/application-scope.png)

### Identity Service: Identitätsoptimierungsalgorithmus

Bei relativ komplexen Diagrammstrukturen spielt die Namespace-Priorität eine wichtige Rolle, um sicherzustellen, dass beim Reduzieren von Diagrammen die richtigen Links entfernt werden. Weitere Informationen finden Sie unter [[!DNL Identity Optimization Algorithm] Übersicht](../identity-graph-linking-rules/identity-optimization-algorithm.md).

### Echtzeit-Kundenprofil: primäre Identitätsfeststellung für Erlebnisereignisse

* Bei Erlebnisereignissen wird die primäre Identität nach der Konfiguration der Identitätseinstellungen für eine bestimmte Sandbox durch die höchste Namespace-Priorität bestimmt.
   * Dies liegt daran, dass Erlebnisereignisse von Natur aus dynamisch sind. Eine Identitätszuordnung kann drei oder mehr Identitäten enthalten. Mit der Namespace-Priorität wird sichergestellt, dass der wichtigste Namespace mit dem Erlebnisereignis verknüpft ist.
* Die folgenden Konfigurationen **wird nicht mehr vom Echtzeit-Kundenprofil verwendet**:
   * Kontrollkästchen &quot;Primär&quot;zum Datenelementtyp im WebSDK.
   * Alle Felder, die in einem XDM Experience Event Class-Schema als primäre Identität markiert sind.
   * Standardmäßige primäre Identitätseinstellungen im Adobe Analytics-Quell-Connector (ECID oder AAID).
* Auf der anderen Seite **Namespace-Priorität bestimmt keine primäre Identität für Profildatensätze**.
   * Für Profildatensätze können Sie den Arbeitsbereich &quot;Schemas&quot;in der Experience Platform-Benutzeroberfläche verwenden, um Ihre Identitätsfelder einschließlich der primären Identität zu definieren. Lesen Sie das Handbuch unter [Identitätsfelder in der Benutzeroberfläche definieren](../../xdm/ui/fields/identity.md) für weitere Informationen.

>[!NOTE]
>
>* Namespace-Priorität ist **eine Eigenschaft eines Namespace**. Es handelt sich um einen numerischen Wert, der einem Namespace zugewiesen wird, um dessen relative Bedeutung anzugeben.
>
>* Primäre Identität ist die Identität, mit der ein Profilfragment gespeichert wird. Ein Profilfragment ist ein Datensatz mit Daten, in dem Informationen über einen bestimmten Benutzer gespeichert werden: Attribute (in der Regel über CRM-Datensätze erfasst) oder Ereignisse (in der Regel aus Erlebnisereignissen oder Online-Daten erfasst).

### Beispiel für ein Diagrammszenario

In diesem Abschnitt finden Sie ein Beispiel dafür, wie sich die Prioritätskonfiguration auf Ihre Daten auswirken kann.

Angenommen, die folgenden Konfigurationen werden für eine bestimmte Sandbox festgelegt:

| Namespace | Echtzeit-Anwendung des Namespace | Priorität |
| --- | --- | --- |
| CRMID | Benutzer | 1 |
| IDFA | Apple-Hardwaregerät (iPhone, IPad usw.) | 2 |
| GAID | Google-Hardwaregerät (Google Pixel, Pixelbook usw.) | 3 |
| ECID | Webbrowser (Firefox, Safari, Google Chrome usw.) | 4 |
| AAID | Webbrowser | 5 |

{style="table-layout:auto"}

In Anbetracht der oben beschriebenen Konfigurationen werden Benutzeraktionen und die Bestimmung der primären Identität als solche aufgelöst:

| Benutzeraktion (Erlebnisereignis) | Authentifizierungsstatus | Datenquelle | Identitätszuordnung | Primäre Identität (Primärschlüssel des Profilfragments) |
| --- | --- | --- | --- | --- |
| Angebotsseite für Kreditkarten anzeigen | Nicht authentifiziert (anonym) | Web SDK | {ECID} | ECID |
| Hilfeseite anzeigen | Nicht authentifiziert | Mobile SDK | {ECID, IDFA} | IDFA |
| Kontoübersicht anzeigen | Authentifiziert | Web SDK | {CRM ID, ECID} | CRM-ID |
| Für Eigenheimdarlehen anmelden | Authentifiziert | Analytics-Quell-Connector | {CRM ID, ECID, AAID} | CRM-ID |
| 1.000 USD aus der Überprüfung auf Einsparungen übertragen | Authentifiziert | Mobile SDK | {CRM ID, GAID, ECID} | CRM-ID |

{style="table-layout:auto"}

### Segmentierungsdienst: Metadatenspeicherung von Segmentmitgliedschaften

![Ein Diagramm zum Speicher der Segmentzugehörigkeit](../images/namespace-priority/segment-membership-storage.png)

Für ein bestimmtes zusammengeführtes Profil werden Segmentmitgliedschaften mit der Identität mit dem Namespace mit der höchsten Priorität gespeichert.

Angenommen, es gibt zwei Profile:

* Das erste Profil steht für John.
* Das zweite Profil steht für Jane.

Wenn John und Jane ein Gerät gemeinsam nutzen, wird die ECID (Webbrowser) von einer Person an eine andere übertragen. Dies hat jedoch keinen Einfluss auf die Informationen zur Segmentmitgliedschaft, die für John und Jane gespeichert wurden.

Wenn die Segmentqualifikationskriterien ausschließlich auf anonymen Ereignissen basieren, die mit der ECID gespeichert wurden, würde Jane sich für dieses Segment qualifizieren

## Auswirkungen auf andere Experience Platform-Dienste {#implications}

In diesem Abschnitt wird beschrieben, wie sich die Namespace-Priorität auf andere Experience Platform-Dienste auswirken kann.

### Erweiterte Lebenszyklusverwaltung

Löschanfragen von Datensammlungen funktionieren für eine bestimmte Identität wie folgt:

* Echtzeit-Kundenprofil: Löscht alle Profilfragmente mit der angegebenen Identität als primäre Identität. **Die primäre Identität für das Profil wird jetzt anhand der Namespace-Priorität bestimmt.**
* Data Lake: Löscht jeden Datensatz mit der angegebenen Identität als primäre Identität.

Weitere Informationen finden Sie im Abschnitt [Überblick über das erweiterte Lebenszyklusmanagement](../../hygiene/home.md).

### Data Lake

Die Datenerfassung in Data Lake berücksichtigt weiterhin die in konfigurierten primären Identitätseinstellungen. [Web SDK](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) und Schemas.

Data Lake bestimmt die primäre Identität nicht basierend auf der Namespace-Priorität. Adobe Customer Journey Analytics verwendet beispielsweise weiterhin Werte in der Identitätszuordnung, auch wenn die Namespace-Priorität aktiviert ist (z. B. Hinzufügen eines Datensatzes zu einer neuen Verbindung), da Customer Journey Analytics ihre Daten aus dem Data Lake verbraucht.

### Experience-Datenmodell (XDM)-Schemas

Jedes Schema, das kein XDM-Erlebnisereignis ist, z. B. individuelle XDM-Profile, berücksichtigt weiterhin alle [Felder, die Sie als Identität markieren](../../xdm/ui/fields/identity.md).

Weitere Informationen zu XDM-Schemas finden Sie im Abschnitt [Übersicht über Schemas](../../xdm/home.md).

### Intelligente Dienste

Bei der Auswahl Ihrer Daten müssen Sie einen Namespace angeben, der verwendet wird, um die Ereignisse zu bestimmen, die Bewertungen berechnen, sowie die Ereignisse, die die berechneten Bewertungen speichern. Es wird empfohlen, den Namespace auszuwählen, der eine Person darstellt.

* Wenn Sie Web-Verhaltensdaten mit WebSDk erfassen, sollten Sie den CRM-ID-Namespace in der Identitätszuordnung auswählen.
* Wenn Sie Webverhaltensdaten mithilfe des Analytics-Quell-Connectors erfassen, sollten Sie den Identitätsdeskriptor (CRM-ID) auswählen.

Diese Konfiguration führt dazu, dass Bewertungen nur mit authentifizierten Ereignissen berechnet werden.

Weitere Informationen finden Sie in den Dokumenten unter [Attribution AI](../../intelligent-services/attribution-ai/overview.md) und [Customer AI](../../intelligent-services/customer-ai/overview.md).

### Privacy Service

[Löschanfragen von Privacy Services](../privacy.md) -Funktion auf folgende Weise für eine bestimmte Identität verwenden:

* Echtzeit-Kundenprofil: Löscht alle Profilfragmente mit dem angegebenen Identitätswert als primäre Identität. **Die primäre Identität für das Profil wird jetzt anhand der Namespace-Priorität bestimmt.**
* Data Lake: Löscht jeden Datensatz mit der angegebenen Identität als primäre oder sekundäre Identität.

Weitere Informationen finden Sie im Abschnitt [Übersicht über den Datenschutzdienst](../../privacy-service/home.md).
