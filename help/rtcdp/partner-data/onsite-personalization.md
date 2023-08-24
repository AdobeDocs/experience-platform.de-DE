---
title: Verwenden der Partner-unterstützten Besuchererkennung zur Personalisierung von Onsite-Erlebnissen
description: Erfahren Sie, wie Sie mit der von Partnern unterstützten Besuchererkennung personalisierte On-site-Erlebnisse für Ihre Besucher bereitstellen können.
source-git-commit: 9d7e8ef99a42e804896f5c9befcf98bb1c010606
workflow-type: tm+mt
source-wordcount: '2530'
ht-degree: 7%

---

# Verwenden der von Partnern unterstützten Besuchererkennung zur Personalisierung von Onsite-Erlebnissen

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die Real-Time CDP (App Service), Adobe Experience Platform Activation, Echtzeit-Kundendatenplattform, Real-Time CDP Prime und Real-Time CDP Ultimate lizenziert haben. Weitere Informationen zu diesen Paketen finden Sie in den [Produktbeschreibungen](https://helpx.adobe.com/de/legal/product-descriptions.html) und erhalten Sie von Ihrem Adobe-Support-Team.

Erfahren Sie, wie Sie mit der von Partnern unterstützten Erkennung personalisierte Erlebnisse für Ihre Webeigenschaftsbesucher bereitstellen können. Verwenden Sie dieses Tutorial, um die Implementierungssequenz verschiedener Elemente in Experience Platform- und anderen Experience Cloud-Lösungen zu verstehen und authentifizierten und nicht authentifizierten Besuchern ein personalisiertes Erlebnis anzuzeigen.

![Eine Infografik, die beschreibt, wie Sie mit von Partnern bereitgestellten Attributen personalisierte Erlebnisse für Ihre Besucher bereitstellen können.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## Branchenbeispiel {#industry-example}

Betrachten Sie beispielsweise eine Marke zur Verbesserung von Wohnraum mit niedrigen Authentifizierungsraten. Diese Marke möchte erstmaligen Besuchern personalisierte Erlebnisse bereitstellen, ohne dass zuvor ein Verlauf oder eine Authentifizierung erfolgt ist und keine verblassende Abhängigkeit von Drittanbieter-Cookies besteht.

Diese Marke nutzt die Technologie zur Partnererkennung, um Besucher probabilistisch zu erkennen und ein personalisierteres Erlebnis zu bieten. Dies hilft bei der vorherigen Betrachtung, da der Besucher den Marketing-Trichter nach unten bewegt. So könnte die Marke beispielsweise demografische Signale von Partnern für On-site-Inhalte verwenden, die für Personen attraktiv sind, die kürzlich umgezogen sind, und einen Rabatt auf beliebte DIY-Produkte anbieten.

## Voraussetzungen und Planung {#prerequisites-and-planning}

Beachten Sie bei der Planung der Verwendung von durch Partner bereitgestellten Attributen zur Bereitstellung personalisierter Erlebnisse für authentifizierte und nicht authentifizierte Besucher die folgenden Voraussetzungen in Ihrem Planungsprozess:

* Welche Eingaben werden von der Erkennungstechnologie Ihres Partners erwartet, damit sie zusätzliche Attribute nutzen können?
* Inwieweit können Sie Personalisierungen in verschiedenen Kanälen und für verschiedene Anwendungsfälle basierend auf probabilistisch abgeleiteten Attributen bereitstellen, im Vergleich zu deterministisch bestätigten Attributen?
* Wie sollte sich das Erlebnis für einen vorauthentifizierten, aber erkannten Besucher bei der Authentifizierung ändern?

### Benutzeroberflächenfunktionen, Plattformkomponenten und Experience Cloud-Produkte, die Sie verwenden werden {#ui-functionality-and-elements}

Um dieses Anwendungsbeispiel erfolgreich zu implementieren, müssen Sie mehrere Bereiche von Real-time Customer Data Platform und anderen Experience Cloud-Lösungen verwenden. Vergewissern Sie sich, dass Sie über die erforderlichen [Attributbasierte Zugriffssteuerungsberechtigungen](/help/access-control/abac/overview.md) für alle diese Bereiche oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu erteilen.

* Datenerfassung
   * [Adobe Experience Platform Web SDK](/help/edge/home.md)
   * [Tags](/help/tags/home.md)
   * [Datenströme](/help/datastreams/overview.md)
* Datenmanagement in Real-Time CDP
   * [Identitäten](/help/identity-service/namespaces.md)
   * [Schemata](/help/xdm/home.md)
   * [Datennutzungskennzeichnungen](/help/data-governance/labels/overview.md)
   * [Datensätze](/help/catalog/datasets/overview.md)
* Personalisierung von Webeigenschaften
   * [Edge-Segmentierung](/help/segmentation/ui/edge-segmentation.md)
   * [Edge-Personalisierungsziele](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (oder einer von Ihnen ausgewählten Personalisierungsplattform). In diesem Anwendungsbeispiel wird Adobe Target als Personalisierungsmaschine hervorgehoben.

## Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

![Eine Infografik, die beschreibt, wie Sie mit von Partnern bereitgestellten Attributen personalisierte Erlebnisse für Ihre Besucher bereitstellen können.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Als **customer**, lizenzieren Sie über die **Datenpartner** die Möglichkeit, Einblicke in Echtzeit von anonymen Website-Besuchern abzurufen.
2. Als **customer**, stellen Sie clientseitige Bibliotheken in Ihren Eigenschaften bereit, um **Partner** APIs erstellen und Sie konfigurieren Web SDK oder Mobile SDK, um von Partnern bereitgestellte Signale an Real-Time CDP zu senden.
3. Wenn Sie Ihre Website oder App durchsuchen, wird die Variable **Besucher** wird wahrscheinlich von der **Partner**, der Attribute zusammen mit einer ID zurückgibt.
4. Real-Time CDP führt die Kantensegmentierung aus, um eingehende Ereignistreffer zu bewerten und Ergebnisse anhand der [ECID-Kennung](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de).
5. Adobe Target verwendet die Kantensegmentierungsausgabe, um das Erlebnis zurück an die **Besucher** zur Personalisierung während der Sitzung.
6. Das Ereignis wird für nachgelagerte Workflows wie Analyse und Retargeting vollständig beibehalten.

## Erreichen des Anwendungsfalls: Schrittweise Anweisungen {#step-by-step-instructions}

Lesen Sie die folgenden Abschnitte, die Links zu weiterführender Dokumentation enthalten, um die einzelnen Schritte in der oben stehenden allgemeinen Übersicht auszuführen.

### Datenverwaltung - Erstellen eines Identitäts-Namespace, -Schemas und -Datensatzes zur Verwaltung von Datenattributen {#data-management}

Um das Nutzungsszenario zur Personalisierung nicht authentifizierter Besuchererlebnisse zu erreichen, müssen Sie zunächst die Datenverwaltungsstruktur in Real-Time CDP einrichten, um die eingehenden Echtzeit-Ereignis- und Zielgruppenqualifizierungsdaten zu erhalten.

#### Identitäts-Namespace der Partner-ID erstellen

Zunächst müssen Sie einen Identitäts-Namespace für die Partner-ID erstellen. Navigieren Sie zu **[!UICONTROL Kunde]** > **[!UICONTROL Identitäten]** in der linken Leiste und wählen Sie dann **[!UICONTROL Identitäts-Namespace erstellen]** in der oberen rechten Ecke des Bildschirms.

![Das Dialogfeld Identitäts-Namespace erstellen mit hervorgehobener Partner-ID.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Weitere Informationen zum [Erstellen eines Partner-ID-Identitäts-Namespace](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Erstellen eines Schemas

Erstellen Sie als Nächstes eine [!UICONTROL Erlebnisereignis] Schema, um die Zeitreihendaten zu speichern, die Sie später aus Ihren Web-Eigenschaften erfassen, und stellen Sie sicher, dass Sie [!UICONTROL XDM ExperienceEvent] als Basisklasse für das Schema. Erfahren Sie mehr über [Erstellen eines Schemas mithilfe der Experience Platform-Benutzeroberfläche](/help/xdm/ui/resources/schemas.md#create).

![Der Arbeitsbereich &quot;Schemas&quot;mit Schema erstellen und XDM-Erlebnis-Ereignis wurde hervorgehoben.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

Während der Erstellung des Schemas und [Hinzufügen von Feldergruppen zu Ihrem Schema](/help/xdm/ui/resources/schemas.md#add-field-groups), sollten Sie erwägen, [Webseite besuchen](/help/xdm/field-groups/event/web-details.md) und [Identity Map](/help/xdm/field-groups/profile/identitymap.md) Feldergruppen. Dies ist zusätzlich zu anderen Feldergruppen möglich, die für Ihre digitalen Eigenschaften und Datenerfassungspraktiken gelten.

Darüber hinaus können Sie eine vorhandene Feldergruppe erstellen oder wiederverwenden und zu Ihrem Schema hinzufügen, um von Partnern bereitgestellte Einblicke über den Besucher zu erfassen. Lesen der Anleitung [Feldergruppe erstellen](/help/xdm/ui/resources/field-groups.md) und wie [Felder hinzufügen](/help/xdm/ui/resources/field-groups.md) zur Feldergruppe hinzu. Wenn Sie beispielsweise erwarten, dass Ihre Feldergruppe anhand von von Partnern bereitgestellten Einblicken wie Altersgruppe, Beschäftigungsstatus, monatliche Kaufkraft oder Kaufverhalten personalisiert wird, müssen Sie geeignete Felder in Ihre Feldergruppe aufnehmen.

Wenn der Datenpartner eine stabile Kennung für den Besucher bereitstellt und Sie diese in Real-Time CDP einbringen möchten, stellen Sie sicher, dass in Ihrer benutzerspezifischen Feldergruppe ein passend benanntes Feld für die Kennung vorhanden ist. Sie sollten das Feld auch im zuvor erstellten Identitäts-Namespace als Identität markieren. Denken Sie auch an [Aktivieren Sie das Schema, das in das Profil aufgenommen werden soll.](/help/xdm/ui/resources/schemas.md#profile).

#### Erstellen eines Datensatzes

Als Nächstes müssen Sie einen Datensatz erstellen, der die Zeitreihendaten enthält, die Sie von Ihren Webeigenschaftsbesuchern erfassen und die Sie für die Personalisierung auf der Site verwenden werden.

Tutorial lesen unter [Erstellen eines Datensatzes](/help/catalog/datasets/user-guide.md#create) und denken Sie daran, die Option zum Erstellen des Datensatzes aus einem Schema auszuwählen. Erstellen Sie den Datensatz basierend auf dem Schema, das Sie im vorherigen Schritt erstellt haben.

Ähnlich wie beim Erstellen eines Schemas müssen Sie die Aufnahme des Datensatzes in die [!UICONTROL Echtzeit-Kundenprofil]. Weitere Informationen zum Aktivieren des Datensatzes für die Verwendung in [!UICONTROL Echtzeit-Kundenprofil], lesen Sie die [Tutorial zum Erstellen von Schemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementieren der Ereignisdatenerfassung in Ihre Webeigenschaft {#implement-data-collection}

Nach der Einrichtung Ihrer Datenverwaltungskonfiguration müssen Sie jetzt Echtzeit-Ereignisse implementieren [Datenerfassung](/help/collection/home.md) in Ihrer Webeigenschaft. Sie müssen Ihre Eigenschaft mit der Adobe-Datenerfassungsbibliothek instrumentieren - [!UICONTROL Web SDK] - zum Erfassen von Echtzeit-Ereignisaufrufen und zum Zurücksenden an Real-Time CDP. Dieses Element besteht aus einigen separaten Aufgaben für einige Datenerfassungskomponenten.

>[!IMPORTANT]
>
>Um von Partnern bereitgestellte Attribute abzurufen, müssen Sie auch *Integrieren Ihrer Webeigenschaft mit Partner-APIs oder anderen Methoden zum Aufrufen und Abrufen von Attributen von Datenpartnern in Echtzeit*. Bitte besprechen Sie diesen Aspekt mit Ihrem Partner Ihrer Wahl, da er nicht Gegenstand dieses Tutorials ist.

Verwenden Sie zunächst den Anwendungsschalter in der oberen rechten Ecke des Bildschirms, um zur **[!UICONTROL Datenerfassung]** Abschnitt.

>[!TIP]
>
>Wenden Sie sich an Ihren Systemadministrator, um Zugriff anzufordern, wenn Sie nicht sehen können, [!UICONTROL Datenerfassung] im Anwendungsschalter.

![App-Umschalter , um zum Abschnitt Datenerfassung zu gelangen.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

Die **[!UICONTROL Datenerfassung]** -Abschnitt der Benutzeroberfläche ähnelt dem unten stehenden Bild.

![Datenerfassung in der Platform-Benutzeroberfläche.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Erstellen von Datenspeichern

Als ersten Schritt im Abschnitt zur Datenerfassung gilt Folgendes: [Erstellen eines neuen Datastreams](/help/datastreams/configure.md). Der Datastream bildet die Grundlage dafür, wie Daten erfasst und korrekt an die richtige Adobe-App, in diesem Fall Experience Platform, weitergeleitet werden.

Wenn Sie den Datastream erstellen, finden Sie im **[!UICONTROL Ereignisschema]** auswählen, wählen Sie das zuvor erstellte Schema aus.

![Die Ereignisschemaauswahl wurde beim Konfigurieren eines neuen Datastreams hervorgehoben.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Ereignis-Datensatz auswählen](/help/datastreams/configure.md#aep) die Sie zuvor aus der Dropdown-Liste erstellt haben, aktivieren Sie die Kontrollkästchen neben **[!UICONTROL Edge-Segmentierung]** und **[!UICONTROL Personalisierungsziele]** und wählen Sie **[!UICONTROL Speichern]**.

Beachten Sie, dass Sie in diesem Szenario keinen Profildatensatz auswählen müssen, da Sie ereignisbasierte Zeitreihendaten einbringen.

#### Tag-Eigenschaft erstellen

Stellen Sie sich eine Eigenschaft als Container vor, den Sie beim Bereitstellen von Tags auf Ihrer Site mit Erweiterungen, Regeln, Datenelementen und Bibliotheken füllen.

Navigieren Sie zu **[!UICONTROL Tags]** und wählen **[!UICONTROL Neue Eigenschaft]**.

![Erstellen Sie eine neue Tag-Eigenschaft.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Speichern]**.

![Füllen Sie die erforderlichen Felder für die neue Eigenschaft aus.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Abrufen vollständiger Informationen zum [Tag-Eigenschaft erstellen](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

Als Nächstes müssen Sie verschiedene Erweiterungen in der Eigenschaft installieren. Wählen Sie Ihre Tag-Eigenschaft aus und navigieren Sie zum [!UICONTROL Erweiterungen] Abschnitt.

![Wählen Sie Ihre neue Tag-Eigenschaft aus.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Beachten Sie, dass [!UICONTROL Core] ist bereits installiert. Sie müssen zwei weitere Erweiterungen installieren, wie in den nächsten Abschnitten beschrieben.

![Anzeigen installierter Erweiterungen.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Installieren der Web SDK-Erweiterung

Beachten Sie, dass dieses Tutorial anzeigt, wie Sie Ihre Website mit Web SDK instrumentieren können. Sie können auch [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) in Ihrer App verwenden, um das Erlebnis für Ihre App-Besucher zu personalisieren.

![Ansicht der Web SDK-Erweiterung im Erweiterungskatalog.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Navigieren Sie im Bildschirm zur Konfiguration des Web SDK nach unten zum **[!UICONTROL Datenspeicher]** und geben Sie Informationen zur verwendeten Experience Platform-Sandbox an. Wählen Sie die entsprechende Sandbox und den in den vorherigen Schritten aus der nächsten Dropdown-Liste erstellten Datastream aus. Sie können dieselben Sandbox- und Datastream-Werte für alle anderen Umgebungen auswählen. Belassen Sie die anderen Einstellungen und wählen Sie **[!UICONTROL Speichern]**.

Vollständige Informationen zu erhalten [Installieren des Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### Installieren der ID-Diensterweiterung

Verwenden Sie die [Experience Cloud ID-Diensterweiterung](/help/tags/extensions/client/id-service/overview.md) , um eine eindeutige gerätebasierte Erstanbieteridentität für Besucher aus allen Experience Cloud-Lösungen zu erstellen. Suchen Sie nach **[!UICONTROL ID-Dienst]** in den Erweiterungskatalog ein und installieren Sie ihn. Behalten Sie bei der Installation der Erweiterung alle Standardeinstellungen bei.

![Ansicht der ID-Diensterweiterung im Erweiterungskatalog.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Einrichten von Umgebungen

Als Nächstes fahren Sie zum **[!UICONTROL Umgebungen]** aus der linken Navigationsleiste. In diesem Schritt müssen Sie Ihre Website mit dem Adobe Edge-Netzwerk verbinden, um Besucherinformationen in Echtzeit abzurufen und bereitzustellen.

Wählen Sie rechts neben der Entwicklungsumgebung das Kästchensymbol aus und kopieren Sie die Standardversion des JavaScript-Code-Snippets, das in einem modalen Fenster angezeigt wird.

![Wählen Sie das Feldsymbol aus, das im Abschnitt Umgebungen der Datenerfassungs-Benutzeroberfläche hervorgehoben ist.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Sie müssen dieses Codefragment ganz oben auf Ihrer Website hinzufügen. Daher ruft Ihre Website das Adobe Edge-Netzwerk auf, um JavaScript-Logik abzurufen, die auf der Seite geladen und ausgeführt wird. Dies ermöglicht Funktionen wie die Besucher-ID-Generierung, Datenerfassung und Echtzeit-Personalisierung von Erlebnissen.

#### Einrichten von Datenelementen

Datenelemente sind Bausteine für Ihr Datenwörterbuch (oder Ihre Datenkarte). Ein einzelnes Datenelement ist eine Variable, deren Wert Abfragezeichenfolgen, URLs, Cookie-Werten, JavaScript-Variablen usw. zugeordnet werden kann. Mehr dazu [Datenelemente](/help/tags/ui/managing-resources/data-elements.md).

Für diesen Anwendungsfall müssen Sie zwei Datenelemente einrichten.

Richten Sie zunächst einen `partnerData` -Element. Navigieren Sie zum **[!UICONTROL Datenelemente]** und wählen Sie **[!UICONTROL Neues Datenelement erstellen]**.

![Erstellen Sie ein neues Datenelement.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Benennen des Datenelements `partnerData`, lassen Sie die [!UICONTROL Erweiterung] Wert als [!UICONTROL Core]und legen **[!UICONTROL Datenelementtyp]** as **[!UICONTROL JavaScript-Variable]**. Eingabe `partnerData` im Feld mit dem Titel **[!UICONTROL JavaScript-Variablenname]** und wählen **[!UICONTROL Speichern]**.

![Markierte Auswahlen zur korrekten Konfiguration des Datenelements &quot;partnerData&quot;.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Benennen Sie die neue Variable, um das zweite Datenelement einzurichten. `pageVisit`, legen Sie die **[!UICONTROL Erweiterung]** nach **[!UICONTROL Adobe Experience Platform]** und wählen **[!UICONTROL XDM-Objekt]** als Datentyp.

![Markierte Auswahlen zur korrekten Konfiguration des Datenelements pageVisit .](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

Wählen Sie im Schema die Attribute von Drittanbietern aus, die den vom Datenpartner erwarteten Werten entsprechen. Wählen Sie dann das Optionsfeld mit dem Titel **[!UICONTROL Gesamtes Objekt bereitstellen]**. Wählen Sie das Datenbanksymbol aus und wählen Sie die `partnerData` -Datenelement, das Sie zuvor erstellt haben.

#### Einrichten von Regeln

Im **[!UICONTROL Regeln]** -Bereich können Sie Ihre Website so konfigurieren, dass eine Personalisierungsanfrage an die Adobe gesendet wird, wobei die Attribute in die soeben erstellten Datenelemente geladen werden. Mehr dazu [Erstellen von Regeln](/help/tags/ui/managing-resources/rules.md).

Auswählen **[!UICONTROL Neue Regel erstellen]**. Diese Regel benennen **[!UICONTROL Personalisieren]** und wählen Sie das Pluszeichen neben **[!UICONTROL Veranstaltungen]**. Auswählen **[!UICONTROL Seitenende]** als Ereignis und speichern Sie.

![Auswahl des Ereignistypteils einer Regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Wählen Sie das Pluszeichen neben **[!UICONTROL Aktionen]**. Aktualisieren Sie die Erweiterung auf **[!UICONTROL Adobe Experience Platform Web SDK]** und **[!UICONTROL Aktionstyp]** nach **[!UICONTROL Ereignis senden]**.

![Auswahl des Aktionstypteils einer Regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Aus dem **[!UICONTROL Typ]** Dropdown-Auswahl auf der rechten Seite auswählen `web.webpagedetails.pageViews` als Ereignistyp.

![Wählen Sie den Ereignistyp aus.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Wählen Sie das Datenbanksymbol neben den XDM-Daten aus und wählen Sie die `pageVisit` Datenelement.

Scrollen Sie in der Liste der Aktionskonfigurationen nach unten und aktivieren Sie das Kontrollkästchen **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]**. Dies ist wichtig, damit Erlebnisse, die über Adobe Target oder ähnliche Produkte bereitgestellt werden, visuell auf der Webseite dargestellt werden können. Auswählen **[!UICONTROL Änderungen beibehalten]**, und dann **[!UICONTROL Speichern]** die Regel.

![Aktivieren Sie das Kontrollkästchen Ausgewählte Personalisierungsentscheidungen rendern .](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Veröffentlichungs-Workflow einrichten

Um diese Konfiguration auf der Webseite bereitzustellen, müssen Sie im nächsten Schritt eine Bibliothek erstellen, die die soeben erstellten Ressourcen enthält. Mehr dazu [Einrichten eines Veröffentlichungsflusses](/help/tags/ui/publishing/publishing-flow.md).

Auswählen **[!UICONTROL Veröffentlichungsfluss]** und dann **[!UICONTROL Bibliothek hinzufügen]**.

Auswählen **[!UICONTROL Alle geänderten Ressourcen hinzufügen]**, benennen Sie die Bibliothek, setzen Sie die Umgebung auf **[!UICONTROL Entwicklung]** und wählen **[!UICONTROL Speichern und in Entwicklung erstellen]**.

![Erstellen von Bibliotheken und Bereitstellen in der Entwicklungsumgebung](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Website testen

An dieser Stelle sollte Ihre Website vollständig mit dem Web SDK instrumentiert sein. Um zu testen, ob die Datenerfassung erwartungsgemäß funktioniert, können Sie zu Ihrer Website navigieren und die Entwicklertools Ihres Browsers verwenden, um den Netzwerk-Traffic zu untersuchen.

Eingabe `interact` Aktualisieren Sie die Seite im Suchfeld. Außerdem sollten Netzwerkaufrufe von Ihrer Website zum Adobe Edge-Netzwerk angezeigt werden.

![Ansicht der Netzwerkereignisse, die in Entwicklertools aufgefüllt werden.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalisierung {#personalization}

Jetzt können Sie Zielgruppen für die Personalisierung erstellen und aktivieren.

#### Einrichten der Kantensegmentierung

Einrichten [Kantensegmentierung](/help/segmentation/ui/edge-segmentation.md) sodass die Zielgruppenzugehörigkeit Ihrer Besucher in Echtzeit beim Besuch Ihrer Webeigenschaft ausgewertet wird.

Stellen Sie sicher, dass auch ein [aktive Zusammenführungsrichtlinie](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) für die Edge-Zielgruppen.

#### Integrieren mit Adobe Target oder einem anderen benutzerdefinierten Personalisierungsziel

Jetzt können Sie in eine Personalisierungsmaschine integrieren, um Ihren Website- oder App-Besuchern personalisierte Inhalte anzuzeigen. Adobe empfiehlt die Verwendung der [Adobe Target-Ziel](/help/destinations/catalog/personalization/adobe-target-connection.md) zu diesem Zweck.

>[!IMPORTANT]
>
>Tutorial lesen unter [Aktivieren von Zielgruppen für Edge-Personalisierungsziele](/help/destinations/ui/activate-edge-personalization-destinations.md) für einen vollständigen Überblick über die Schritte, die zur Aktivierung Ihrer Zielgruppen erforderlich sind.

## Einschränkungen und Fehlerbehebung {#limitations-and-troubleshooting}

Beachten Sie die folgenden Einschränkungen, wenn Sie sich den auf dieser Seite beschriebenen Anwendungsfall ansehen:

* Wenn Sie Partner-IDs verwenden, beachten Sie, dass diese IDs beim Erstellen Ihrer [Identitätsdiagramm](/help/identity-service/ui/identity-graph-viewer.md).

## Andere durch Partnerdatenunterstützung ermöglichte Anwendungsfälle {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die durch die Unterstützung von Partnerdaten in Real-Time CDP ermöglicht werden:

* [Ergänzen Sie Erstanbieterprofile mit Attributen von vertrauenswürdigen Datenpartnern, um Ihre Datengrundlage zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und eine bessere Zielgruppenoptimierung zu erzielen.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Verwenden Sie die Datenunterstützung von Drittanbietern in Real-Time CDP, um [Erweitern Sie Ihre Profilbasis mit potenziellen Profilen von Datenpartnern und interagieren Sie mit ihnen, um neue Kunden zu gewinnen oder zu erreichen.](/help/rtcdp/partner-data/prospecting.md).
* [Erweiterte Aktivierung von Interessenten- und Interessenten-Zielgruppen](/help/destinations/ui/activate-prospect-audiences.md) , um Ziele auszuwählen.