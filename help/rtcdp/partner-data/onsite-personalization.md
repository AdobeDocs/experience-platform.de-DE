---
title: Verwenden der partnergestützten Besuchererkennung zur Personalisierung von Onsite-Erlebnissen
description: Erfahren Sie, wie Sie mit der partnergestützten Besuchererkennung personalisierte Onsite-Erlebnisse für Ihre Besucherinnen und Besucher bereitstellen können.
source-git-commit: b4a18cdf434055be81dacbf19de4dd3e3f229d19
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 97%

---

# Verwenden der partnergestützten Besuchererkennung zur Personalisierung von Onsite-Erlebnissen

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die Real-Time CDP (App Service), Adobe Experience Platform Activation, Echtzeit-Kundendatenplattform, Real-Time CDP Prime und Real-Time CDP Ultimate lizenziert haben. Weitere Informationen zu diesen Paketen finden Sie in den [Produktbeschreibungen](https://helpx.adobe.com/de/legal/product-descriptions.html) und erhalten Sie von Ihrem Adobe-Support-Team.

Erfahren Sie, wie Sie die partnergestützte Erkennung nutzen können, um den Besucherinnen und Besuchern Ihrer Website personalisierte Erlebnisse zu bieten. Verwenden Sie dieses Tutorial, um die Implementierungssequenz verschiedener Elemente in Experience Platform und anderen Experience Cloud-Lösungen zu verstehen, um authentifizierten und nicht authentifizierten Besucherinnen und Besuchern ein personalisiertes Erlebnis anzuzeigen.

![Eine Infografik, die beschreibt, wie Sie mit von Partnern bereitgestellten Attributen personalisierte Erlebnisse für Ihre Besucherinnen und Besucher bereitstellen können.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## Branchenbeispiel {#industry-example}

Nehmen wir als Beispiel eine Baumarktmarke, die niedrige Authentifizierungsraten hat. Diese Marke möchte Menschen, die zum ersten Mal eine Website besuchen, ein personalisiertes Erlebnis bieten, ohne dass sie sich vorher anmelden oder authentifizieren müssen und ohne dass sie sich auf Cookies von Drittanbietern verlassen müssen.

Diese Marke hat sich für eine Technologie zur Partnererkennung entschieden, um Besucherinnen und Besucher mit einer gewissen Wahrscheinlichkeit zu erkennen und ihnen ein personalisiertes Erlebnis zu bieten. Dies trägt dazu bei, die Kauferwägung der Besucherinnen und Besucher auf ihrem Weg durch den Marketing-Trichter voranzutreiben. So könnte die Marke beispielsweise von Partnern bereitgestellte demografische Signale für Onsite-Inhalte nutzen, die Menschen ansprechen, die kürzlich umgezogen sind, und ihnen einen Rabatt auf beliebte Heimwerkerprodukte anbieten.

## Voraussetzungen und Planung {#prerequisites-and-planning}

Wenn Sie planen, von Partnern bereitgestellte Attribute zu verwenden, um Ihren authentifizierten und nicht authentifizierten Besucherinnen und Besuchern personalisierte Erlebnisse zu bieten, sollten Sie die folgenden Voraussetzungen in Ihrem Planungsprozess berücksichtigen:

* Welche Eingaben erwartet die Erkennungstechnologie Ihres Partners, damit zusätzliche Attribute hinzugefügt werden können?
* Inwiefern sind Sie damit einverstanden, Personalisierung in verschiedenen Kanälen und für verschiedene Anwendungsfälle auf der Grundlage von probabilistisch abgeleiteten Attributen zu liefern, im Gegensatz zu deterministisch bestätigten Attributen?
* Wie sollte sich das Erlebnis für vorauthentifizierte, aber erkannte Besucherinnen und Besucher bei der Authentifizierung ändern?

### Benutzeroberflächenfunktionen, Platform-Komponenten und Experience Cloud-Produkte, die Sie verwenden werden {#ui-functionality-and-elements}

Um dieses Anwendungsbeispiel erfolgreich zu implementieren, müssen Sie mehrere Bereiche von Real-time Customer Data Platform und anderen Experience Cloud-Lösungen verwenden. Vergewissern Sie sich, dass Sie die notwendigen [Attribut-basierten Zugriffsrechte](/help/access-control/abac/overview.md) für alle diese Bereiche haben, oder bitten Sie Ihre Systemadmins, Ihnen die notwendigen Rechte zu erteilen.

* Datenerfassung
   * [Adobe Experience Platform Web SDK](/help/edge/home.md)
   * [Tags](/help/tags/home.md)
   * [Datenströme](/help/datastreams/overview.md)
* Datenverwaltung in Real-Time CDP
   * [Identitäten](/help/identity-service/namespaces.md)
   * [Schemata](/help/xdm/home.md)
   * [Datennutzungskennzeichnungen](/help/data-governance/labels/overview.md)
   * [Datensätze](/help/catalog/datasets/overview.md)
* Personalisierung von Web-Eigenschaften
   * [Edge-Segmentierung](/help/segmentation/ui/edge-segmentation.md)
   * [Edge-Personalisierungsziele](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (oder eine von Ihnen ausgewählte Personalisierungsplattform. In diesem Anwendungsbeispiel wird Adobe Target als Personalisierungs-Engine hervorgehoben)

## Videoeinführung {#video-walkthrough}

Sehen Sie sich das Video-Tutorial unten an, um eine exemplarische Vorgehensweise zum Personalisieren von Onsite-Erlebnissen für unbekannte Besucher zu erhalten:

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

![Eine Infografik, die beschreibt, wie Sie mit von Partnern bereitgestellten Attributen personalisierte Erlebnisse für Ihre Besucherinnen und Besucher bereitstellen können.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Als **Kundin bzw. Kunde** lizenzieren Sie vom **Datenpartner** die Möglichkeit, in Echtzeit Einblicke über ansonsten anonyme Website-Besucherinnen und -Besucher zu erhalten.
2. Als **Kundin bzw. Kunde** setzen Sie Client-seitige Bibliotheken auf Ihren Eigenschaften ein, um **Partner**-APIs aufzurufen, und Sie konfigurieren Web SDK oder Mobile SDK, um vom Partner bereitgestellte Signale an Real-Time CDP zu senden.
3. Beim Durchsuchen Ihrer Website oder App werden **Besucherinnen und Besucher** vom **Partner** probabilistisch erkannt, der Attribute zusammen mit einer ID zurückgibt.
4. Real-Time CDP führt die Edge-Segmentierung aus, um eingehende Ereignistreffer zu bewerten und Ergebnisse anhand der [ECID-Kennung](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de) festzuhalten.
5. Adobe Target verwendet die Edge-Segmentierungausgabe, um das Erlebnis für die **Besucherinnen und Besucher** mit Personalisierung während der Sitzung zu rendern.
6. Das Ereignis wird für nachgelagerte Workflows wie Analyse und Retargeting vollständig beibehalten.

## Erreichen des Anwendungsfalls: Schrittweise Anweisungen {#step-by-step-instructions}

Lesen Sie die folgenden Abschnitte, die Links zu weiterführender Dokumentation enthalten, um die einzelnen Schritte in der oben stehenden allgemeinen Übersicht auszuführen.

### Datenverwaltung – Erstellen eines Identity-Namespace, -Schemas und -Datensatzes zur Verwaltung von Datenattributen {#data-management}

Um den Anwendungsfall zur Personalisierung des Erlebnisses nicht authentifizierter Besucherinnen und Besucher zu erreichen, müssen Sie zunächst die Daten-Management-Struktur in Real-Time CDP einrichten, um die eingehenden Echtzeit-Ereignis- und Zielgruppenqualifizierungsdaten zu erhalten.

#### Erstellen eines Identity-Namespace für die Partner-ID 

Zunächst müssen Sie einen Identity-Namespace für die Partner-ID erstellen. Navigieren Sie in der linken Leiste zu **[!UICONTROL Kunde]** > **[!UICONTROL Identitäten]** und wählen Sie dann in der oberen rechten Ecke des Bildschirms **[!UICONTROL Identity-Namespace erstellen]** aus.

![Das Dialogfeld „Identity-Namespace erstellen“ mit hervorgehobener Partner-ID.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Weitere Informationen zum [Erstellen eines Identity-Namespace für die Partner-ID](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Erstellen eines Schemas

Erstellen Sie als Nächstes ein [!UICONTROL Erlebnisereignis]-Schema, um die Zeitreihendaten zu speichern, die Sie später aus Ihren Web-Eigenschaften erfassen, und stellen Sie sicher, dass Sie [!UICONTROL XDM Experience Event] als Basisklasse für das Schema verwenden. Erfahren Sie mehr über das [Erstellen eines Schemas mithilfe der Experience Platform-Benutzeroberfläche](/help/xdm/ui/resources/schemas.md#create).

![Der Arbeitsbereich „Schemata“, wobei „Schema erstellen“ und XDM Experience Event hervorgehoben sind.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

Während Sie das Schema erstellen und [Feldergruppen zu Ihrem Schema hinzufügen](/help/xdm/ui/resources/schemas.md#add-field-groups), sollten Sie erwägen, die Feldergruppen [Web-Seite besuchen](/help/xdm/field-groups/event/web-details.md) und [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md) hinzuzufügen. Dies ist zusätzlich zu anderen Feldergruppen möglich, die für Ihre digitalen Eigenschaften und Datenerfassungspraktiken gelten.

Darüber hinaus können Sie eine vorhandene Feldergruppe erstellen oder wiederverwenden und zu Ihrem Schema hinzufügen, um von Partnern bereitgestellte Einblicke über die Besucherin bzw. den Besucher zu erfassen. Lesen Sie mehr über das [Erstellen einer Feldergruppe](/help/xdm/ui/resources/field-groups.md) und das [Hinzufügen von Feldern](/help/xdm/ui/resources/field-groups.md) zur Feldergruppe. Wenn Sie beispielsweise erwarten, dass Ihre Feldergruppe anhand von durch Partner bereitgestellten Einblicken wie Altersgruppe, Beschäftigungsstatus, monatliche Kaufkraft oder Kaufverhalten personalisiert wird, müssen Sie geeignete Felder in Ihre Feldergruppe aufnehmen.

Wenn der Datenpartner eine stabile Kennung für die Besucherin bzw. den Besucher bereitstellt und Sie diese in Real-Time CDP einbringen möchten, stellen Sie sicher, dass in Ihrer benutzerspezifischen Feldergruppe ein passend benanntes Feld für die Kennung vorhanden ist. Sie sollten das Feld auch im zuvor erstellten Identity-Namespace als Identität markieren. Denken Sie auch daran, [das Schema zu aktivieren, das in das Profil aufgenommen werden soll](/help/xdm/ui/resources/schemas.md#profile).

#### Erstellen eines Datensatzes

Als Nächstes müssen Sie einen Datensatz erstellen, der die Zeitreihendaten enthält, die Sie von Ihren Besucherinnen und Besuchern der Web-Eigenschaft erfassen und die Sie für die Personalisierung auf der Site verwenden werden.

Lesen Sie das Tutorial zum [Erstellen eines Datensatzes](/help/catalog/datasets/user-guide.md#create) und denken Sie daran, die Option zum Erstellen des Datensatzes aus einem Schema auszuwählen. Erstellen Sie den Datensatz basierend auf dem Schema, das Sie im vorherigen Schritt erstellt haben.

Ähnlich wie beim Erstellen eines Schemas müssen Sie den Datensatz aktivieren, der in das [!UICONTROL Echtzeit-Kundenprofil] aufgenommen werden soll. Weitere Informationen zum Aktivieren des Datensatzes für die Verwendung im [!UICONTROL Echtzeit-Kundenprofil] erhalten Sie im [Tutorial zum Erstellen von Schemata.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementieren der Ereignisdatenerfassung in Ihrer Web-Eigenschaft {#implement-data-collection}

Nach der Einrichtung der Daten-Management-Konfiguration müssen Sie jetzt die [Datenerfassung](/help/collection/home.md) für Echtzeit-Ereignisse in Ihrer Web-Eigenschaft implementieren. Sie müssen Ihre Eigenschaft mit der Datenerfassungsbibliothek von Adobe – [!UICONTROL Web SDK] – ausstatten, um Abrufe von Echtzeit-Ereignissen zu erfassen und sie zurück an Real-Time CDP zu senden. Dieses Element besteht aus einigen separaten Aufgaben für einige Datenerfassungskomponenten.

>[!IMPORTANT]
>
>Um von Partnern bereitgestellte Attribute abzurufen, müssen Sie außerdem *Ihre Web-Eigenschaft mit Partner-APIs oder anderen Methoden integrieren, um Attribute von Datenpartnern in Echtzeit aufzurufen und zu beziehen*. Bitte besprechen Sie diesen Aspekt mit dem Partner Ihrer Wahl, da er nicht Gegenstand dieses Tutorials ist.

Verwenden Sie zunächst den Anwendungsumschalter in der rechten oberen Ecke des Bildschirms, um zum Abschnitt **[!UICONTROL Datenerfassung]** zu navigieren.

>[!TIP]
>
>Wenden Sie sich an Ihre Systemadmins, um Zugriff anzufordern, wenn Sie [!UICONTROL Datenerfassung] nicht im Anwendungsumschalter sehen können.

![Anwendungsumschalter, um zum Abschnitt „Datenerfassung“ zu gelangen.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

Der Abschnitt **[!UICONTROL Datenerfassung]** der Benutzeroberfläche ähnelt dem unten stehenden Bild.

![Der Abschnitt „Datenerfassung“ in der Platform-Benutzeroberfläche.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Datenstrom erstellen

Im Abschnitt zur Datenerfassung [erstellen Sie einen neuen Datenstrom](/help/datastreams/configure.md) als ersten Schritt. Der Datenstrom bildet die Grundlage dafür, wie Daten erfasst und korrekt an die richtige Adobe-Anwendung weitergeleitet werden, in diesem Fall Experience Platform.

Wenn Sie den Datenstrom erstellen, wählen Sie im Feld **[!UICONTROL Ereignisschema]** das zuvor erstellte Schema aus.

![Die Ereignisschema-Auswahl beim Konfigurieren eines neuen Datenstroms ist hervorgehoben.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Wählen Sie den Ereignis-Datensatz aus](/help/datastreams/configure.md#aep), den Sie zuvor aus der Dropdown-Liste erstellt haben, aktivieren Sie die Kontrollkästchen neben **[!UICONTROL Edge-Segmentierung]** und **[!UICONTROL Personalisierungsziele]** und wählen Sie **[!UICONTROL Speichern]** aus.

Beachten Sie, dass Sie in diesem Szenario keinen Profildatensatz auswählen müssen, da Sie ereignisbasierte Zeitreihendaten einbringen.

#### Erstellen einer Tag-Eigenschaft

Stellen Sie sich eine Eigenschaft als einen Container vor, den Sie mit Erweiterungen, Regeln, Datenelementen und Bibliotheken füllen, wenn Sie Tags auf Ihrer Website bereitstellen.

Navigieren Sie zu **[!UICONTROL Tags]** und wählen Sie **[!UICONTROL Neue Eigenschaft]** aus.

![Erstellen Sie eine neue Tag-Eigenschaft.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Speichern]** aus.

![Ausfüllen der erforderlichen Felder für die neue Eigenschaft.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Erhalten Sie vollständige Informationen zum [Erstellen einer Tag-Eigenschaft](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=de).

Als Nächstes müssen Sie verschiedene Erweiterungen in der Eigenschaft installieren. Wählen Sie Ihre Tag-Eigenschaft aus und navigieren Sie zum Abschnitt [!UICONTROL Erweiterungen].

![Eine neue Tag-Eigenschaft auswählen.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

[!UICONTROL Core] ist bereits installiert. Wie in den nächsten Abschnitten beschrieben, müssen zwei weitere Erweiterungen installiert werden.

![Anzeigen der installierten Erweiterungen.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Installieren der Web SDK-Erweiterung

In diesem Tutorial wird gezeigt, wie eine Website mit Web SDK instrumentiert werden kann. Sie können [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) auch für Ihre App verwenden, um das Erlebnis für Ihre App-Besucherinnen und -Besucher zu personalisieren.

![Ansicht der Web SDK-Erweiterung im Erweiterungskatalog.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Navigieren Sie im Bildschirm zur Konfiguration des Web SDK nach unten zum Abschnitt **[!UICONTROL Datenströme]** und geben Sie Informationen zur Experience Platform-Sandbox an, die Sie verwenden. Wählen Sie die entsprechende Sandbox und den in den vorherigen Schritten erstellten Datenstrom aus der nächsten Dropdown-Liste aus. Sie können dieselben Sandbox- und Datenstromwerte für alle anderen Umgebungen auswählen. Belassen Sie die anderen Einstellungen und wählen Sie **[!UICONTROL Speichern]** aus.

Vollständige Informationen zum [Installieren des Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html?lang=de).

#### Installieren der ID-Service-Erweiterung

Verwenden Sie die [Erweiterung „ID-Dienst“ für Experience Cloud](/help/tags/extensions/client/id-service/overview.md) aus, um eine eindeutige gerätebasierte Erstanbieteridentität für Besucherinnen und Besucher aus allen Experience Cloud-Lösungen zu erstellen. Suchen Sie im Erweiterungskatalog nach **[!UICONTROL ID-Dienst]** und installieren Sie ihn. Bei der Installation der Erweiterung müssen alle Standardeinstellungen beibehalten werden.

![Ansicht der Erweiterung „ID-Dienst“ im Erweiterungskatalog.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Einrichten der Umgebungen

Gehen Sie als Nächstes über die linke Navigationsleiste zum Abschnitt **[!UICONTROL Umgebungen]**. In diesem Schritt muss die Website mit dem Adobe Edge Network verbunden werden, um Besucherinformationen in Echtzeit abzurufen und bereitzustellen.

Wählen Sie rechts neben der Entwicklungsumgebung das Kästchensymbol aus und kopieren Sie die Standardversion des JavaScript-Code-Snippets, das in einem modalen Fenster angezeigt wird.

![Wählen Sie das Kästchensymbol aus, das im Abschnitt „Umgebungen“ der Datenerfassungs-Benutzeroberfläche hervorgehoben ist.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Dieses Code-Fragment muss ganz oben auf der Website hinzugefügt werden. Dann ruft die Website das Adobe Edge-Network auf, um JavaScript-Logik abzurufen, die auf der Seite geladen und ausgeführt wird. Dies ermöglicht Funktionen wie die Generierung von Besucher-IDs, Datenerfassung und Personalisierung von Erlebnissen in Echtzeit.

#### Einrichten von Datenelementen

Datenelemente sind Bausteine für Ihr Datenwörterbuch (oder Ihre Datenkarte). Ein einzelnes Datenelement ist eine Variable, deren Wert Abfragezeichenfolgen, URLs, Cookie-Werten, JavaScript-Variablen usw. zugeordnet werden kann. Weitere Informationen über [Datenelemente](/help/tags/ui/managing-resources/data-elements.md).

Für diesen Anwendungsfall müssen zwei Datenelemente eingerichtet werden.

Richten Sie zunächst ein `partnerData`-Element ein. Navigieren Sie zum Abschnitt **[!UICONTROL Datenelemente]** und wählen Sie **[!UICONTROL Neues Datenelement erstellen]** aus.

![Neues Datenelement erstellen.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Benennen Sie das Datenelement `partnerData`, belassen Sie den Wert [!UICONTROL Erweiterung] bei [!UICONTROL Kern] und legen Sie den **[!UICONTROL Datenelementtyp]** als **[!UICONTROL JavaScript-Variable]** fest. Geben Sie `partnerData` im Feld mit dem Titel **[!UICONTROL JavaScript-Variablenname]** ein und wählen Sie **[!UICONTROL Speichern]** aus.

![Hervorgehobene Auswahlen zur korrekten Konfiguration des Datenelements partnerData.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Um das zweite Datenelement einzurichten, benennen Sie die neue Variable `pageVisit`, setzen Sie die **[!UICONTROL Erweiterung]** auf **[!UICONTROL Adobe Experience Platform]** und wählen Sie als den Datentyp **[!UICONTROL XDM-Objekt]** aus.

![Markierte Auswahlen zur korrekten Konfiguration des Datenelements pageVisit .](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

Wählen Sie im Schema die Attribute von Drittanbietern aus, die den Werten entsprechen, die Sie vom Datenpartner erwarten. Wählen Sie dann das Optionsfeld mit dem Titel **[!UICONTROL Gesamtes Objekt bereitstellen]** aus. Klicken Sie auf das Symbol, das wie eine Datenbank aussieht, und wählen Sie das `partnerData`-Datenelement aus, das Sie zuvor erstellt haben.

#### Einrichten von Regeln

Im Abschnitt **[!UICONTROL Regeln]** können Sie Ihre Website so konfigurieren, dass eine Personalisierungsanfrage an Adobe mit den Attributen gesendet wird, die in die soeben erstellten Datenelemente geladen werden. Weitere Informationen zum [Erstellen von Regeln](/help/tags/ui/managing-resources/rules.md).

Wählen Sie **[!UICONTROL Neue Regel erstellen]** aus. Benennen Sie diese Regel **[!UICONTROL Personalisieren]** und wählen Sie das Pluszeichen neben **[!UICONTROL Ereignissen]** aus. Wählen Sie **[!UICONTROL Seitenende]** als Ereignis aus und speichern Sie.

![Auswahl des Ereignistypteils einer Regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Wählen Sie das Pluszeichen neben **[!UICONTROL Aktionen]** aus. Aktualisieren Sie die Erweiterung auf **[!UICONTROL Adobe Experience Platform Web SDK]** und setzen Sie den **[!UICONTROL Aktionstyp]** auf **[!UICONTROL Ereignis senden]**.

![Auswahl für den Aktionstypteils einer Regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Wählen Sie aus der Dropdown-Auswahl **[!UICONTROL Typ]** auf der rechten Seite `web.webpagedetails.pageViews` als den Ereignistyp.

![Auswählen des Ereignistyps.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Klicken Sie auf das Datenbanksymbol neben „XDM-Daten“ und wählen Sie das Datenelement `pageVisit` aus.

Scrollen Sie in der Liste der Aktionskonfigurationen nach unten und aktivieren Sie das Kontrollkästchen **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]**. Dies ist wichtig, damit Erlebnisse, die über Adobe Target oder ähnliche Produkte bereitgestellt werden, visuell auf der Web-Seite dargestellt werden können. Wählen Sie **[!UICONTROL Änderungen beibehalten]** aus und **[!UICONTROL speichern]** Sie dann die Regel.

![Aktivieren Sie das Kontrollkästchen „Visuelle Personalisierungsentscheidungen rendern“.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Einrichten des Veröffentlichungs-Workflows

Um diese Konfiguration auf der Web-Seite bereitzustellen, müssen Sie im nächsten Schritt eine Bibliothek erstellen, die die soeben erstellten Ressourcen enthält. Lesen Sie mehr über das [Einrichten eines Veröffentlichungsflusses](/help/tags/ui/publishing/publishing-flow.md).

Wählen Sie **[!UICONTROL Veröffentlichungsfluss]** und dann **[!UICONTROL Bibliothek hinzufügen]** aus.

Wählen Sie **[!UICONTROL Alle geänderten Ressourcen hinzufügen]** aus, benennen Sie die Bibliothek, setzen Sie die Umgebung auf **[!UICONTROL Entwicklung]** und wählen Sie **[!UICONTROL Speichern und in Entwicklung erstellen]** aus.

![Erstellen von Bibliotheken und Bereitstellen in der Entwicklungsumgebung](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Website testen

An dieser Stelle sollte Ihre Website vollständig mit dem Web SDK instrumentiert sein. Um zu testen, ob die Datenerfassung erwartungsgemäß funktioniert, können Sie zu Ihrer Website navigieren und die Entwickler-Tools Ihres Browsers verwenden, um den Netzwerk-Traffic zu untersuchen.

Geben Sie `interact` in das Suchfeld ein, aktualisieren Sie die Seite, und Sie sollten sehen, dass die Netzwerkaufrufe von Ihrer Website an das Adobe Edge-Netzwerk aufgefüllt werden.

![Ansicht der Netzwerkereignisse, die in Entwickler-Tools aufgefüllt werden.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalisierung {#personalization}

Jetzt können Sie Zielgruppen für die Personalisierung erstellen und aktivieren.

#### Einrichten der Edge-Segmentierung

Richten Sie die [Edge-Segmentierung](/help/segmentation/ui/edge-segmentation.md) ein, sodass die Zielgruppenzugehörigkeit Ihrer Besucherinnen und Besucher beim Besuch Ihrer Web-Eigenschaft in Echtzeit ausgewertet wird.

Stellen Sie sicher, dass auch eine [„Active-On-Edge“-Zusammenführungsrichtlinie](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) für die Edge-Zielgruppen eingerichtet ist.

#### Integrieren mit Adobe Target oder einem anderen benutzerdefinierten Personalisierungsziel

Jetzt können Sie eine Engine für Personalisierung integrieren, um Ihren Website- oder App-Besucherinnen und -Besuchern personalisierte Inhalte anzuzeigen. Adobe empfiehlt für diesen Zweck die Verwendung des [Adobe Target-Ziels](/help/destinations/catalog/personalization/adobe-target-connection.md).

>[!IMPORTANT]
>
>Lesen Sie das Tutorial zum [Aktivieren von Zielgruppen für Edge-Personalisierungsziele](/help/destinations/ui/activate-edge-personalization-destinations.md), um einen vollständigen Überblick über die Schritte zu erhalten, die zur Aktivierung Ihrer Zielgruppen erforderlich sind.

## Einschränkungen und Fehlerbehebung {#limitations-and-troubleshooting}

Beachten Sie die folgenden Einschränkungen, wenn Sie sich den auf dieser Seite beschriebenen Anwendungsfall ansehen:

* Wenn Sie Partner-IDs verwenden, beachten Sie, dass diese IDs beim Erstellen Ihres [Identitätsdiagramms](/help/identity-service/ui/identity-graph-viewer.md) nicht verwendet werden.

## Andere durch Partnerdatenunterstützung ermöglichte Anwendungsfälle {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die durch die Unterstützung von Partnerdaten in Real-Time CDP ermöglicht werden:

* [Ergänzen Sie Erstanbieterprofile mit Attributen von vertrauenswürdigen Datenpartnern, um Ihre Datengrundlage zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und eine bessere Zielgruppenoptimierung zu erzielen.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Verwenden Sie die Unterstützung von Drittanbieterdaten in Real-Time CDP, damit Sie [Ihre Profilbasis mit potenziellen Profilen von Datenpartnern erweitern und mit ihnen interagieren können, um neue Kundinnen und Kunden zu gewinnen oder zu erreichen](/help/rtcdp/partner-data/prospecting.md).
* [Erweiterte Aktivierung von Interessenten- und Interessenten-Zielgruppen](/help/destinations/ui/activate-prospect-audiences.md) , um Ziele auszuwählen.