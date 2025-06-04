---
title: Namespace-Priorität
description: Erfahren Sie mehr über die Namespace-Priorität in Identity Service.
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 7df0d0c7eb97760190ac8b20d1b74472b87e8b6a
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 2%

---

# Namespace-Priorität {#namespace-priority}

>[!CONTEXTUALHELP]
>id="platform_identities_namespacepriority"
>title="Namespace-Priorität"
>abstract="Die Namespace-Priorität bestimmt, wie Links aus dem Identitätsdiagramm entfernt werden."

Jede Kundenimplementierung ist einzigartig und auf die Ziele einer bestimmten Organisation zugeschnitten. Daher variiert die Bedeutung eines bestimmten Namespace von Kunde zu Kunde. Beispiele aus der Praxis sind:

* Ihr Unternehmen könnte jede E-Mail-Adresse als Einzelperson-Entität betrachten und daher [Identitätseinstellungen](./identity-settings-ui.md) verwenden, um den E-Mail-Namespace als eindeutig zu konfigurieren. Ein anderes Unternehmen möchte jedoch möglicherweise Einzelpersonen-Entitäten mit mehreren E-Mail-Adressen darstellen und daher den E-Mail-Namespace als nicht eindeutig konfigurieren. Diese Unternehmen müssen einen anderen Identity-Namespace als eindeutig verwenden, z. B. einen CRMID-Namespace, sodass es eine Einzelpersonen-Kennung geben kann, die mit den mehreren E-Mail-Adressen verknüpft ist.
* Sie können das Online-Verhalten mithilfe eines „Anmelde-ID“-Namespace erfassen. Diese Anmelde-ID könnte eine 1:1-Beziehung mit der CRMID haben, die dann Attribute aus einem CRM-System speichert und als der wichtigste Namespace betrachtet werden kann. In diesem Fall stellen Sie dann fest, dass der CRM-Namespace eine genauere Darstellung einer Person ist, während der Namespace der Anmelde-ID der zweitwichtigste ist.

Sie müssen in Identity Service Konfigurationen vornehmen, die die Bedeutung Ihrer Namespaces widerspiegeln, da dies beeinflusst, wie Profile und ihre zugehörigen Identitätsdiagramme gebildet und aufgeteilt werden.

## Festlegen von Prioritäten

Die Bestimmung der Namespace-Priorität basiert auf den folgenden Faktoren:

### Struktur des Identitätsdiagramms

Wenn die Diagrammstruktur Ihres Unternehmens mehrschichtig ist, sollte die Namespace-Priorität dies widerspiegeln, damit die richtigen Links im Fall eines Diagrammausfalls entfernt werden.

>[!TIP]
>
>* „Diagrammausblendung“ bezieht sich auf Szenarien, in denen mehrere unterschiedliche Profile versehentlich zu einem einzigen Identitätsdiagramm zusammengeführt werden.
>
>* Ein geschichtetes Diagramm bezieht sich auf Identitätsdiagramme, die mehrere Ebenen von Links aufweisen. Im folgenden Bild sehen Sie ein Beispiel für ein Diagramm mit drei Ebenen.

![Diagramm von Diagrammschichten](../images/namespace-priority/graph-layers.png "Diagramm von Diagrammschichten"){zoomable="yes"}

### Semantische Bedeutung des Namespace

Eine Identität stellt ein reales Objekt dar. Das Identitätsdiagramm stellt drei Objekte dar. Nach ihrer Bedeutung sind sie:

* Personen (geräteübergreifend, E-Mail, Telefonnummer)
* Hardwareeinheit
* Webbrowser (Cookie)

Personen-Namespaces sind im Vergleich zu Hardware-Geräten (wie IDFA, GAID), die im Vergleich zu Webbrowsern relativ unveränderlich sind, relativ unveränderlich. Grundsätzlich sind Sie (eine Person) immer eine einzige Entität, die über mehrere Hardwaregeräte (Smartphone, Laptop, Tablet usw.) verfügen und mehrere Browser (Google Chrome, Safari, FireFox usw.) verwenden kann

Eine weitere Möglichkeit, dieses Thema anzugehen, ist die Kardinalität. Wie viele Identitäten werden für eine bestimmte Personenentität erstellt? In den meisten Fällen verfügt eine Person über eine CRMID, eine Handvoll Hardware-Geräte-IDs (IDFA-/GAID-Zurücksetzungen sollten nicht oft vorkommen) und noch mehr Cookies (eine Person könnte vorstellbar auf mehreren Geräten browsen, den Inkognito-Modus verwenden oder Cookies jederzeit zurücksetzen). Im Allgemeinen **eine niedrigere Kardinalität einen Namespace mit einer höheren Priorität**.

## Überprüfen der Einstellungen für die Namespace-Priorität

Sobald Sie eine Vorstellung davon haben, wie Sie Ihre Namespaces priorisieren werden, können Sie das Diagrammsimulations-Tool in der Benutzeroberfläche verwenden, um verschiedene Szenarien zum Reduzieren von Diagrammen zu testen und sicherzustellen, dass Ihre Prioritätskonfigurationen die erwarteten Diagrammergebnisse zurückgeben. Weitere Informationen finden Sie im Handbuch zum Verwenden des [Diagrammsimulations-Tools](./graph-simulation.md).

## Namespace-Priorität konfigurieren

Die Namespace-Priorität kann mithilfe der [Benutzeroberfläche für Identitätseinstellungen“ konfiguriert ](./identity-settings-ui.md). In der Benutzeroberfläche für Identitätseinstellungen können Sie einen Namespace per Drag-and-Drop verschieben, um dessen relative Bedeutung zu bestimmen.

>[!IMPORTANT]
>
>Sie können keine Geräte-/Cookie-Namespaces gegenüber Personen-Namespaces priorisieren. Durch diese Einschränkung wird sichergestellt, dass keine Fehlkonfigurationen auftreten.

## Verwendung der Namespace-Priorität

Derzeit beeinflusst die Namespace-Priorität das Systemverhalten des Echtzeit-Kundenprofils. Das folgende Diagramm veranschaulicht dieses Konzept. Weitere Informationen finden Sie im Handbuch zu [Architekturdiagrammen für Adobe Experience Platform und Programme](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![Ein Diagramm zum Anwendungsbereich mit Namespace-Priorität.](../images/namespace-priority/application-scope.png "Ein Diagramm zum Anwendungsbereich mit Namespace-Priorität."){zoomable="yes"}

## Identity Service: Algorithmus zur Identitätsoptimierung

Bei relativ komplexen Diagrammstrukturen spielt die Namespace-Priorität eine wichtige Rolle dabei, sicherzustellen, dass die richtigen Links entfernt werden, wenn Szenarien zum Reduzieren von Diagrammen auftreten. Weitere Informationen finden Sie unter [Übersicht über den Identitätsoptimierungsalgorithmus](../identity-graph-linking-rules/identity-optimization-algorithm.md).

## Echtzeit-Kundenprofil: Primäre Identitätsbestimmung für Erlebnisereignisse

* Nachdem Sie die Identitätseinstellungen für eine bestimmte Sandbox konfiguriert haben, wird die primäre Identität für Erlebnisereignisse durch die höchste Namespace-Priorität in der Konfiguration bestimmt.
   * Dies liegt daran, dass Erlebnisereignisse dynamisch sind. Eine Identitätszuordnung kann drei oder mehr Identitäten enthalten, und die Namespace-Priorität stellt sicher, dass dem Erlebnisereignis der wichtigste Namespace zugeordnet ist.
* Daher werden die folgenden Konfigurationen **vom Echtzeit-Kundenprofil nicht mehr verwendet**:
   * Die primäre Identitätskonfiguration (`primary=true`) beim Senden von Identitäten in der `identityMap` mithilfe der Web SDK, Mobile SDK oder Edge Network API (Identity-Namespace und Identitätswert werden weiterhin in Profile verwendet). **Hinweis**: Services außerhalb des Echtzeit-Kundenprofils wie Data Lake Storage oder Adobe Target verwenden weiterhin die primäre Identitätskonfiguration (`primary=true`).
   * Alle Felder, die in einem XDM-Erlebnisereignis-Klassenschema als primäre Identität gekennzeichnet sind.
   * Standardeinstellungen für die primäre Identität im Adobe Analytics-Quell-Connector (ECID oder AAID).
* Dagegen bestimmt **Namespace-Priorität nicht die primäre Identität für Profildatensätze**.
   * Für Profildatensätze sollten Sie weiterhin Ihre Identitätsfelder im Schema definieren, einschließlich der primären Identität. Weitere Informationen finden Sie im Handbuch unter [Definieren von Identitätsfeldern in ](../../xdm/ui/fields/identity.md) Benutzeroberfläche“.

>[!TIP]
>
>* Die Namespace-Priorität ist **eine Eigenschaft eines Namespace**. Dies ist ein numerischer Wert, der einem Namespace zugewiesen wird, um seine relative Bedeutung anzugeben.
>
>* Die Primäre Identität ist die Identität, für die ein Profilfragment gespeichert wird. Ein Profilfragment ist ein Datensatz mit Daten, die Informationen zu einem bestimmten Benutzer speichern: Attribute (z. B. CRM-Datensätze) oder Ereignisse (z. B. Website-Browsen).

### Beispielszenario

Dieser Abschnitt enthält ein Beispiel dafür, wie sich die Prioritätskonfiguration auf Ihre Daten auswirken kann.

Angenommen, die folgenden Konfigurationen werden für eine bestimmte Sandbox festgelegt:

| Namespace | Reale Anwendung des Namespace | Priorität |
| --- | --- | --- |
| CRMID | Benutzer | 1 |
| IDFA | Apple-Hardwaregerät (iPhone, IPad usw.) | 2 |
| GAID | Google-Hardwaregerät (Google Pixel, Pixelbook usw.) | 3 |
| ECID | Webbrowser (Firefox, Safari, Google Chrome usw.) | 4 |
| AAID | Webbrowser | 5 |

{style="table-layout:auto"}

Angesichts der oben beschriebenen Konfigurationen werden Benutzeraktionen und die Bestimmung der primären Identität als solche aufgelöst:

| Benutzeraktion (Erlebnisereignis) | Authentifizierungsstatus | Datenquelle | Namespaces im Ereignis | Namespace der primären Identität |
| --- | --- | --- | --- | --- |
| Kreditkartenangebot-Seite anzeigen | Nicht authentifiziert (anonym) | Web SDK | `{ECID}` | ECID |
| Hilfeseite anzeigen | Nicht authentifiziert | Mobile SDK | `{ECID, IDFA}` | IDFA |
| Kontostand anzeigen | Authentifiziert | Web SDK | `{CRMID, ECID}` | CRMID |
| Melden Sie sich für ein Eigenheimdarlehen an | Authentifiziert | Analytics-Quell-Connector | `{CRMID, ECID, AAID}` | CRMID |
| Transfer von $1.000 vom Check-in zum Sparen | Authentifiziert | Mobile SDK | `{CRMID, GAID, ECID}` | CRMID |

{style="table-layout:auto"}

## Segmentierungs-Service: Speichern von Metadaten für die Segmentzugehörigkeit

![Ein Diagramm zur Speicherung der Segmentzugehörigkeit.](../images/namespace-priority/segment-membership-storage.png "Ein Diagramm zum Speicher der Segmentzugehörigkeit."){zoomable="yes"}

Für ein bestimmtes zusammengeführtes Profil werden Segmentzugehörigkeiten für die Identität mit der höchsten Namespace-Priorität gespeichert.

Angenommen, es gibt zwei Profile:

* Profil 1 stellt John dar.
   * Johns Profil qualifiziert sich für S1 (Segmentzugehörigkeit 1). Beispielsweise könnte S1 auf ein Segment von Kundinnen und Kunden verweisen, die sich als männlich identifizieren.
   * Johns Profil ist auch für S2 (Segmentzugehörigkeit 2) qualifiziert. Dies könnte sich auf ein Segment von Kundinnen und Kunden beziehen, deren Treuestatus „Gold“ ist.
* Profil 2 stellt Jane dar.
   * Janes Profil qualifiziert sich für S3 (Segmentzugehörigkeit 3). Dies könnte sich auf ein Segment von Kundinnen beziehen, die sich als weiblich identifizieren.
   * Janes Profil qualifiziert sich auch für S4 (Segmentzugehörigkeit 4). Dies könnte sich auf ein Segment von Kundinnen und Kunden beziehen, deren Treuestatus Platin ist.

Wenn John und Jane ein Gerät teilen, wird die ECID (Webbrowser) von einer Person auf eine andere übertragen. Dies hat jedoch keinen Einfluss auf die Segmentzugehörigkeitsinformationen, die für John und Jane gespeichert sind.

Wenn die Segmentqualifikationskriterien ausschließlich auf anonymen Ereignissen basieren, die für die ECID gespeichert wurden, ist Jane für dieses Segment qualifiziert.

## Auswirkungen auf andere Experience Platform-Services {#implications}

In diesem Abschnitt wird beschrieben, wie sich die Namespace-Priorität auf andere Experience Platform-Services auswirken kann.

### Erweitertes Daten-Lifecycle-Management

Anfragen zum Löschen von Datenhygiene-Datensätzen funktionieren für eine bestimmte Identität wie folgt:

* Echtzeit-Kundenprofil: Löscht jedes Profilfragment mit der angegebenen Identität als primäre Identität. **Die primäre Identität im Profil wird jetzt anhand der Namespace-Priorität bestimmt.**
* Data Lake: Löscht alle Datensätze mit der angegebenen Identität als primäre Identität. Im Gegensatz zum Echtzeit-Kundenprofil basiert die primäre Identität im Data Lake auf der primären Identität, die im WebSDK (`primary=true`) angegeben ist, oder auf einem Feld, das als primäre Identität gekennzeichnet ist

Weitere Informationen finden Sie im Abschnitt [Übersicht über das erweiterte Lebenszyklus-Management](../../hygiene/home.md).

### Berechnete Attribute

Wenn die Identitätseinstellungen aktiviert sind, verwenden berechnete Attribute die Namespace-Priorität, um den berechneten Attributwert zu speichern. Für ein bestimmtes Ereignis wird der Wert des berechneten Attributs für die Identität mit der höchsten Namespace-Priorität geschrieben. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche für berechnete Attribute](../../profile/computed-attributes/ui.md).

### Data Lake

Die Datenaufnahme im Data Lake berücksichtigt weiterhin die primären Identitätseinstellungen, die in [Web SDK](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) und Schemata konfiguriert sind.

Data Lake bestimmt keine primäre Identität basierend auf der Namespace-Priorität. Adobe Customer Journey Analytics verwendet beispielsweise auch dann Werte in der Identitätszuordnung, wenn die Namespace-Priorität aktiviert ist (z. B. beim Hinzufügen eines Datensatzes zu einer neuen Verbindung), da Customer Journey Analytics deren Daten aus dem Data Lake verwendet.

### Experience-Datenmodell (XDM)-Schemata

Jedes Schema, das kein XDM-Erlebnisereignis ist, z. B. einzelne XDM-Profile, berücksichtigt weiterhin alle [Felder, die Sie als Identität markieren](../../xdm/ui/fields/identity.md).

Weitere Informationen zu XDM-Schemata finden Sie unter [Schemata - Übersicht](../../xdm/home.md).

### Intelligent Services

Bei der Auswahl Ihrer Daten müssen Sie einen Namespace angeben, mit dem die Ereignisse bestimmt werden, die die Bewertungen berechnen, sowie die Ereignisse, die die berechneten Bewertungen speichern. Es wird empfohlen, den Namespace auszuwählen, der eine Person darstellt.

* Wenn Sie Web-Verhaltensdaten mit WebSDK erfassen, wird empfohlen, den CRMID-Namespace innerhalb der Identitätszuordnung auszuwählen.
* Wenn Sie Web-Verhaltensdaten mit dem Analytics-Quell-Connector erfassen, sollten Sie den Identitätsdeskriptor (CRMID) auswählen.

Diese Konfiguration führt dazu, dass Scores nur anhand authentifizierter Ereignisse berechnet werden.

Weitere Informationen finden Sie in den Dokumenten zu [Attributions-KI](../../intelligent-services/attribution-ai/overview.md) und [Kunden-KI](../../intelligent-services/customer-ai/overview.md).

### Partnerdefinierte Ziele

Aktualisierte Ergebnisse zur Zielgruppen-Disqualifizierung für Profile, die mit einem freigegebenen Gerät verknüpft sind, können nicht an nachgelagerte Ziele gesendet werden. Dies kann in bestimmten seltenen Fällen vorkommen, in denen:

* Die Zielgruppen-Qualifizierung basiert nur auf anonymer Aktivität.
* Anmeldungen über mehrere Profile hinweg erfolgen in einem kurzen Zeitraum.

Weitere Informationen zu von Partnern erstellten Zielen finden Sie unter [Ziele - Übersicht](../../destinations/home.md#adobe-built-and-partner-built-destinations).

### Privacy Service

[Privacy Service-Löschanfragen](../privacy.md) funktionieren für eine bestimmte Identität wie folgt:

* Echtzeit-Kundenprofil: Löscht jedes Profilfragment mit dem angegebenen Identitätswert als primäre Identität. **Die primäre Identität im Profil wird jetzt anhand der Namespace-Priorität bestimmt.**
* Data Lake: Löscht alle Datensätze mit der angegebenen Identität als primäre oder sekundäre Identität.

Weitere Informationen finden Sie unter [Übersicht über Privacy Service](../../privacy-service/home.md).

### Edge-Segmentierung und Edge Network-Programme

Im Zusammenhang mit [!DNL Identity Graph Linking Rules] gibt es zwei wichtige Verhaltensänderungen, die bezüglich der Edge-Segmentierung und Edge Network-Anwendungen zu beachten sind:

1. Die `identityMap` muss einen Personen-Namespace enthalten, der als eindeutig gekennzeichnet wurde. Als Identität markierte Felder (Identitätsdeskriptoren) werden nicht unterstützt.
2. Der Personen-Namespace muss über die `primary = true`-Konfiguration verfügen, wenn ein Endbenutzer während der Authentifizierung browst.

#### Edge-Segmentierung

Stellen Sie bei einem bestimmten Ereignis sicher, dass alle Ihre Namespaces, die eine Personenentität darstellen, in der `identityMap` enthalten sind, da [Identitäten, die als XDM-Felder gesendet ](../../xdm/ui/fields/identity.md), ignoriert werden und nicht für die Speicherung von Metadaten für die Segmentzugehörigkeit verwendet werden.

* **Ereignisanwendbarkeit**: Dieses Verhalten gilt nur für Ereignisse, die direkt an die Edge Network gesendet werden (z. B. WebSDK und Mobile SDK). Ereignisse, die vom [Experience Platform-Hub](../../landing/edge-and-hub-comparison.md) aufgenommen werden, z. B. Ereignisse, die mit der HTTP-API-Quelle, anderen Streaming-Quellen und Batch-Quellen aufgenommen werden, unterliegen nicht dieser Einschränkung.
* **Spezifität der Edge**-Segmentierung: Dieses Verhalten ist spezifisch für die Edge-Segmentierung. Batch- und Streaming-Segmentierung sind separate Services, die am Hub ausgewertet werden und nicht demselben Prozess folgen. Weitere Informationen finden [ im ](../../segmentation/methods/edge-segmentation.md) zur Edge-Segmentierung .
* Weitere Informationen finden Sie in den [Architekturdiagrammen für Adobe Experience Platform ](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications#detailed-architecture-diagram) Anwendungen und auf den [Vergleichsseiten ](../../landing/edge-and-hub-comparison.md) Edge Network und Hub .

#### Edge Network-Programme

Um sicherzustellen, dass Programme auf der Edge Network ohne Verzögerung Zugriff auf das Edge-Profil haben, stellen Sie sicher, dass Ihre Ereignisse `primary=true` auf der CRMID enthalten. Dadurch wird eine sofortige Verfügbarkeit sichergestellt, ohne auf Aktualisierungen des Identitätsdiagramms vom Hub zu warten.

* Programme auf Edge Network wie Adobe Target, Offer Decisioning und benutzerdefinierte Personalization-Ziele hängen auch weiterhin von der Primäridentität in den Ereignissen ab, um auf Profile über das Edge-Profil zuzugreifen.
* Lesen Sie das Architekturdiagramm für [Experience Platform Web SDK und Edge Network](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/deployment/websdk#experience-platform-webmobile-sdk-or-edge-network-server-api-deployment), um weitere Informationen zum Verhalten von Edge Network zu erhalten.
* SDK Weitere Informationen zum Konfigurieren [ Primäridentität in Web finden Sie in der Dokumentation ](../../tags/extensions/client/web-sdk/data-element-types.md)Datenelementtypen und [Identitätsdaten in Web ](../../web-sdk/identity/overview.md)SDK).
* Stellen Sie sicher, dass die ECID im Erlebnisereignis enthalten ist. Wenn die ECID fehlt, wird sie der Ereignis-Payload mit `primary=true` hinzugefügt, was zu unerwarteten Ergebnissen führen kann.