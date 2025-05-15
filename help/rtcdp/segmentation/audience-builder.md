---
title: Audience Builder in Real-Time Customer Data Platform
description: Erfahren Sie, wie Sie mit dem Audience Builder in Real-Time Customer Data Platform Zielgruppen erstellen.
feature: Get Started, Audiences
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: da87baad-b82a-4a45-89c3-cf20d66fe657
source-git-commit: 3829f506d0b4d78b543b949e8e11806d8fe10b9c
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 10%

---

# Audience Builder in Real-Time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] basiert auf Adobe Experience Platform und kann alle Funktionen von Audience Builder nutzen, die Teil von [!DNL Experience Platform] sind. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die Dateneigenschaften entsprechen.

![Audience Builder im Abschnitt Konten.](../assets/segmentation/audience-builder/audience-builder.png){zoomable="yes"}

## Felder {#fields}

>[!CONTEXTUALHELP]
>id="platform_b2b_audiencebuilder_showfullxdmschema"
>title="Gesamtes XDM-Schema anzeigen"
>abstract="Standardmäßig werden nur Felder angezeigt, die Daten enthalten. Aktivieren Sie diese Option, um alle Felder im XDM-Schema anzuzeigen."

>[!CONTEXTUALHELP]
>id="platform_b2b_audiencebuilder_showrelationselectors"
>title="Beziehungsselektoren anzeigen"
>abstract="Standardmäßig werden die Standardbeziehungen für Ihre Organisation verwendet. Aktivieren Sie diese Option, um die verwendeten Beziehungsselektoren anzuzeigen."

>[!CONTEXTUALHELP]
>id="platform_b2b_audiencebuilder_showconstrainedfields"
>title="Eingeschränkte Felder anzeigen"
>abstract="Standardmäßig werden nur Felder ohne Einschränkungen angezeigt. Aktivieren Sie diese Option, um Felder mit Einschränkungen anzuzeigen."

Bei Verwendung von Audience Builder für -Konten können Sie Kontoattribute oder vorhandene Zielgruppen als Felder Ihrer Zielgruppe verwenden.

Sie können das Symbol ![Einstellungen](../../images/icons/settings.png) auswählen, um die Einstellungen für die angezeigten Felder anzupassen.

![Die Einstellungssymbole sind in Audience Builder hervorgehoben.](../assets/segmentation/audience-builder/select-settings.png){zoomable="yes"}

>[!NOTE]
>
>Der Abschnitt **[!UICONTROL Feldoptionen]** befindet sich derzeit in der Beta-Phase und steht nur ausgewählten Kundinnen und Kunden zur Verfügung. Wenden Sie sich an die Adobe-Kundenunterstützung, um weitere Informationen zu erhalten.

Der [!UICONTROL Einstellungen] wird angezeigt. In diesem Abschnitt können Sie festlegen, welche Felder angezeigt werden und wie die Beziehung der Felder aussieht.

Für die **[!UICONTROL Feldoptionen]** können Sie entweder nur die Felder anzeigen, die Daten enthalten, oder das vollständige XDM-Schema.

Für die **[!UICONTROL Beziehung von Feldern]** können Sie entweder die Standardbeziehungen für Ihre Organisation verwenden oder die Beziehungsselektoren anzeigen.

![Das Einstellungsmodul wird angezeigt.](../assets/segmentation/audience-builder/settings.png){width="300"}

### Attribute {#attributes}

Auf [!UICONTROL &#x200B; Registerkarte &#x200B;]Attribute“ können Sie Account-Attribute, die zur Klasse XDM Business Account gehören, sowie Opportunities und personenbasierte Attribute durchsuchen. Jeder Ordner kann erweitert werden, um zusätzliche Attribute anzuzeigen. Jedes Attribut ist eine Kachel, die in der Mitte des Arbeitsbereichs auf [ Arbeitsfläche ](#rule-builder-canvas)Regel-Builders“ gezogen werden kann.

![Die Registerkarte Attribute wird im Audience Builder angezeigt](../assets/segmentation/audience-builder/attributes.png)

Bei der Auswahl eines Attributs können Sie Zusammenfassungsdaten anzeigen, indem Sie auf das [Informationssymbol](../../images/icons/info.png) klicken. Die Zusammenfassungsdaten enthalten Informationen wie Spitzenwerte, eine Erläuterung des Felds sowie den Prozentsatz der Konten, die Werte für dieses Attribut enthalten.

![Ein Pop-up, das eine vollständig ausgefüllte Version der Zusammenfassungsdaten für ein Attribut anzeigt.](../assets/segmentation/audience-builder/full-summary-data.png){width="300"}

Wenn ein Attribut in weniger als 25 % der Konten eingetragen ist, wird stattdessen ![Datenhinweissymbol](../../images/icons/data-notice.png) angezeigt. Unabhängig davon werden für das Attribut dieselben Zusammenfassungsdaten angezeigt.

![Ein Pop-up, das eine Version der Zusammenfassungsdaten für ein Attribut anzeigt, wenn es mit weniger als 25 % der Konten gefüllt ist.](../assets/segmentation/audience-builder/empty-summary-data.png){width="300"}

>[!NOTE]
>
>Zusammenfassungsdaten sind nur verfügbar, wenn das Attribut zum Schema Konto, Person oder Opportunity gehört. Darüber hinaus werden die oberen Werte nur angezeigt, wenn das Feld **nicht** zu viele verschiedene Werte enthält und wenn die Werte dieser Felder häufig wiederholt werden.
>
>Diese Zusammenfassungsdaten werden **täglich**.

Eine detailliertere Anleitung zum Audience Builder finden Sie im [Audience Builder-Benutzerhandbuch](../../segmentation/ui/segment-builder.md){target="_blank"}.

### Zielgruppen {#audiences}

Auf **[!UICONTROL Registerkarte]** Zielgruppen“ werden alle personenbasierten und kontobasierten Zielgruppen aufgelistet, die in Experience Platform verfügbar sind.

Sie können den Mauszeiger über das ![Informationssymbol](../../images/icons/info.png) neben einer Zielgruppe bewegen, um Informationen über die Zielgruppe anzuzeigen, einschließlich ihrer ID, Beschreibung und der Ordnerhierarchie zum Auffinden der Zielgruppe.

![Es werden Informationen über die Zielgruppe angezeigt.](../assets/segmentation/audience-builder/audience-information.png){zoomable="yes"}

## Arbeitsfläche des Regel-Builders {#rule-builder-canvas}

Eine in Audience Builder erstellte Zielgruppe ist eine Sammlung von Regeln, mit denen wichtige Merkmale oder Verhaltensweisen einer Zielgruppe beschrieben werden. Diese Regeln werden mithilfe der Arbeitsfläche des Regel-Builders in der Mitte von Audience Builder erstellt.

Um Ihrer Segmentdefinition eine neue Regel hinzuzufügen, ziehen Sie eine Kachel aus der Registerkarte **[!UICONTROL Felder]** und legen Sie sie auf der Arbeitsfläche des Regel-Builders ab.

![Die Arbeitsfläche des Regel-Builders mit einem hinzugefügten Feld.](../assets/segmentation/audience-builder/added-field.png){zoomable="yes"}

Weitere Informationen zur Verwendung der Arbeitsfläche des Regel-Builders finden Sie in der [Segment Builder-Dokumentation](../../segmentation/ui/segment-builder.md#rule-builder-canvas){target="_blank"}.

### Container {#containers}

Zielgruppenregeln werden in der Reihenfolge ausgewertet, in der sie aufgelistet sind. Sie können Container verwenden, um die Ausführungsreihenfolge durch die Verwendung verschachtelter Abfragen besser steuern zu können.

Weitere Informationen zu Containern finden Sie in der [Segment Builder-Dokumentation](../../segmentation/ui/segment-builder.md#containers){target="_blank"}.

## Zielgruppen-Eigenschaften {#properties}

Im Abschnitt **[!UICONTROL Zielgruppeneigenschaften]** werden Informationen zur Zielgruppe angezeigt, einschließlich einer geschätzten Größe der Zielgruppe. Sie können auch Details zu Ihrer Audience angeben, einschließlich Name, Beschreibung und Tags.

![Der Abschnitt mit den Zielgruppeneigenschaften wird für die Zielgruppe in Audience Builder angezeigt.](../assets/segmentation/audience-builder/audience-properties.png){width="300"}

Die **[!UICONTROL Qualifizierte Konten]** gibt die tatsächliche Anzahl von Konten an, die den Regeln der Zielgruppe entsprechen. Diese Zahl wird nach Ausführung des Segmentierungsauftrags alle 24 Stunden aktualisiert.

Die **[!UICONTROL Geschätzte Konten]** gibt die ungefähre Anzahl von Konten basierend auf dem Beispielvorgang an. Sie können diesen Wert aktualisieren, nachdem Sie neue Regeln oder Bedingungen hinzugefügt und **[!UICONTROL Schätzung aktualisieren]** ausgewählt haben.

![Der Abschnitt „Schätzungen“ im Abschnitt „Zielgruppeneigenschaften“ wird angezeigt.](../assets/segmentation/audience-builder/account-estimates.png){width="300"}

Sie können auf **[!UICONTROL Konten anzeigen]** klicken, um ein Stichprobenverfahren für die Konten anzuzeigen, die mit den aktuellen Regeln für die Zielgruppe qualifiziert wären.

![Die Schaltfläche „Konten anzeigen“ ist hervorgehoben.](../assets/segmentation/audience-builder/view-accounts.png){width="300"}

Die **[!UICONTROL Code]** Ansicht) bietet eine textbasierte Code-Beschreibung der Regeln der Zielgruppe.

![Die Code-Ansichtsversion der Konto-Zielgruppe.](../assets/segmentation/audience-builder/code-view.png)

Sie können **[!UICONTROL Zugriffskennzeichnungen anwenden]** auswählen, um die entsprechenden Zugriffskennzeichnungen für die Zielgruppe anzuwenden. Weitere Informationen zu Zugriffsbeschriftungen finden Sie im [Handbuch zum Verwalten von Beschriftungen](../../access-control/abac/ui/labels.md){target="_blank"}.

![Das Pop-up „Zugriff anwenden“ und „Data Governance-Beschriftungen“ wird angezeigt.](../assets/segmentation/audience-builder/apply-access-labels.png)

Der Rest des Abschnitts „Zielgruppeneigenschaften“ ermöglicht die Bearbeitung von Details, die sich auf die Konto-Zielgruppe beziehen, einschließlich Name, Beschreibung und Tags.

![Die Details der Zielgruppeneigenschaften werden angezeigt.](../assets/segmentation/audience-builder/audience-details.png){width="300"}

Sie **die Auswertungsmethode** Konto-Zielgruppen nicht ändern, da alle Konto-Zielgruppen mithilfe der Batch-Segmentierung ausgewertet werden.

## Nächste Schritte {#next-steps}

Audience Builder bietet einen umfangreichen Workflow, mit dem Sie Zielgruppen aus Ihren XDM Business-Kontodaten erstellen können.

Weitere Informationen zum Segmentierungs-Service für Kundenprofildaten finden Sie unter [Segmentierungs-Service - Übersicht](../../segmentation/home.md){target="_blank"}.
