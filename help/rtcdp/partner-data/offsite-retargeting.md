---
title: Offsite-Retargeting nicht authentifizierter Besucher
description: Erfahren Sie, wie Sie nicht authentifizierte Benutzer erneut ansprechen können, indem Sie mit Interessenten-IDs ein berechnetes Attribut erstellen, das zur Erstellung einer Audience nicht authentifizierter Benutzer verwendet werden kann.
feature: Use Cases, Customer Acquisition
exl-id: cffa3873-d713-445a-a3e1-1edf1aa8eebb
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 1%

---

# Offsite-Retargeting nicht authentifizierter Besucher

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate lizenziert haben. Weitere Informationen zu diesen Paketen finden Sie in den [Produktbeschreibungen](https://helpx.adobe.com/de/legal/product-descriptions.html) und erhalten Sie von Ihrem Adobe-Support-Team.

Erfahren Sie, wie Sie mithilfe von vom Partner bereitgestellten dauerhaften IDs eine Zielgruppe nicht authentifizierter Besucher erstellen und erneut ansprechen können.

![Eine Infografik, die den Fluss von Partnerdaten von der Aufnahme in Adobe Experience Platform zur Ausgabe über Zielgruppen an ein nachgelagertes Ziel zeigt.](../assets/offsite-retargeting/header.png)

## Gründe für diesen Anwendungsfall {#why-use-case}

Nach der Abschaffung von Drittanbieter-Cookies müssen Experten für Digital Marketing ihre Strategien für die erneute Interaktion mit anonymen Besuchern neu überdenken. Marken, die sich für die Integration mit Identitätsanbietern zur Echtzeit-Besuchererkennung entscheiden, können auch von Partnern bereitgestellte dauerhafte Kennungen für das externe Retargeting bezahlter Medien nutzen.

Trotz des hohen Traffics verzeichnen viele Marken in der Konversionsphase einen deutlichen Rückgang. Besucher interagieren mit Inhalten und Produktdemos, verlassen diese jedoch, ohne sich anzumelden oder einen Kauf zu tätigen.

Sie können nicht nur Zielgruppen erstellen, die auf der Interaktion vor Ort basieren, um Marketing-Nachrichten zu personalisieren, sondern auch die Adobe-Unterstützung für Partner-IDs nutzen, um über Paid-Media-Ziele hinweg erneut mit Besuchern zu interagieren.

## Voraussetzungen und Planung {#prerequisites-and-planning}

Beachten Sie bei der Planung von Retargeting für nicht authentifizierte Besucher während Ihres Planungsprozesses die folgenden Voraussetzungen:

- Habe ich die Partner-IDs mit den richtigen Identity-Namespaces eingerichtet?

Um den Anwendungsfall zu implementieren, verwenden Sie außerdem die folgenden Real-Time CDP-Funktionen und Benutzeroberflächenelemente. Stellen Sie sicher, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu gewähren.

- [Zielgruppen](/help/segmentation/home.md)
- [Berechnete Attribute](/help/profile/computed-attributes/overview.md)
- [Ziele](/help/destinations/home.md)
- [Datenerfassung](/help/collection/home.md)

## Holen von Partnerdaten in Real-Time CDP {#get-data-in}

Um eine Zielgruppe nicht authentifizierter Besucher zu erstellen, müssen Sie zunächst Ihre Partnerdaten in Real-Time CDP importieren.

Informationen zum optimalen Importieren von Daten in Real-Time CDP mithilfe von Web SDK finden Sie in den [Abschnitten Datenverwaltung und Ereignisdatenerfassung](./onsite-personalization.md#data-management) des Anwendungsfalls Personalisierung vor Ort.

## Von Partnern bereitgestellte IDs vorziehen {#bring-partner-ids-forward}

Nachdem Sie die vom Partner bereitgestellten IDs in einen Ereignis-Datensatz importiert haben, müssen Sie diese Daten in die Profildatensätze übertragen. Dazu können Sie berechnete Attribute verwenden.

Berechnete Attribute ermöglichen es Ihnen, Profilverhaltensdaten auf Profilebene schnell in aggregierte Werte zu konvertieren. Daher können Sie diese Ausdrücke, z. B. „Gesamtkauf über die gesamte Lebensdauer“, für das Profil verwenden, sodass Sie das berechnete Attribut einfach in Ihren Zielgruppen verwenden können. Weitere Informationen zu berechneten Attributen finden Sie unter [Berechnete Attribute - Übersicht](/help/profile/computed-attributes/overview.md).

Um auf berechnete Attribute zuzugreifen, wählen Sie **[!UICONTROL Profiles]** und dann **[!UICONTROL Computed attributes]** und **[!UICONTROL Create computed attribute]** aus.

![Die Schaltfläche &quot;[!UICONTROL Create computed attributes]&quot; ist zusätzlich zur Registerkarte &quot;[!UICONTROL Computed attributes]&quot; im Arbeitsbereich &quot;[!UICONTROL Profiles]&quot; hervorgehoben.](../assets/offsite-retargeting/create-ca.png)

Die Seite **[!UICONTROL Create computed attribute]** wird angezeigt. Auf dieser Seite können Sie die Komponenten zum Erstellen Ihres berechneten Attributs verwenden.

![Der Arbeitsbereich „Berechnete Attribute erstellen“ wird angezeigt.](../assets/offsite-retargeting/ca-page.png)

>[!NOTE]
>
>Ausführlichere Informationen zum Erstellen berechneter Attribute finden Sie im [Handbuch zur Benutzeroberfläche für berechnete Attribute](/help/profile/computed-attributes/ui.md).

Für diesen Anwendungsfall können Sie ein berechnetes Attribut erstellen, das, wenn die Partner-ID vorhanden ist, den neuesten Wert der Partner-ID innerhalb der letzten 24 Stunden abruft.

Über die Suchleiste können Sie das Ereignis „Partner-ID“ suchen und [, das Sie während des Anwendungsfalls „Personalisierung vor Ort“ erstellt haben](#get-data-in) zur Arbeitsfläche für berechnete Attribute hinzufügen.

![Die Registerkarte &quot;[!UICONTROL Events]&quot; und die Suchleiste sind hervorgehoben.](../assets/offsite-retargeting/ca-add-partner-id.png)

Nachdem Sie der Definition das Ereignis „Partner-ID“ hinzugefügt haben, legen Sie die Ereignisfilterbedingung auf **[!UICONTROL Exists]** fest, legen Sie die Ereignisfilterbedingung auf den **[!UICONTROL Most Recent]** Wert der hinzugefügten Partner-ID fest und verfügen über einen Lookback-Zeitraum von 24 Stunden.

![Die Definition des berechneten Attributs, das Sie erstellen möchten, ist hervorgehoben.](../assets/offsite-retargeting/ca-add-definition.png)

Geben Sie dem berechneten Attribut einen geeigneten Namen (z. B. „Partner-ID„) und eine Beschreibung und wählen Sie dann **[!UICONTROL Publish]** aus, um den Erstellungsprozess des berechneten Attributs abzuschließen.

![Die grundlegenden Informationen des berechneten Attributs, das Sie erstellen möchten, sind hervorgehoben.](../assets/offsite-retargeting/ca-publish.png)

## Erstellen einer Zielgruppe mit dem berechneten Attribut {#create-audience}

Nachdem Sie das berechnete Attribut erstellt haben, können Sie dieses berechnete Attribut verwenden, um eine Zielgruppe zu erstellen. In diesem Beispiel erstellen Sie eine Zielgruppe aus Besuchern, die Ihre Website in diesem Monat mehr als fünfmal besucht haben, sich aber noch nicht angemeldet haben.

Um eine Zielgruppe zu erstellen, wählen Sie **[!UICONTROL Audiences]** und dann **[!UICONTROL Create audience]** aus.

![Die Schaltfläche &quot;[!UICONTROL Create audience]&quot; ist hervorgehoben.](../assets/offsite-retargeting/create-audience.png)

Ein Dialogfeld wird angezeigt, in dem Sie zwischen [!UICONTROL Compose audience] und [!UICONTROL Build rule] wählen können. Wählen Sie **[!UICONTROL Build rule]** und dann **[!UICONTROL Create]** aus.

![Die Schaltfläche &quot;[!UICONTROL Build rule]&quot; ist hervorgehoben.](../assets/offsite-retargeting/select-build-rule.png)

Die Seite Segment Builder wird angezeigt. Auf dieser Seite können Sie die Komponenten zum Aufbau Ihrer Audience verwenden.

![Der Segment Builder wird angezeigt.](../assets/offsite-retargeting/segment-builder.png)

>[!NOTE]
>
>Ausführlichere Informationen zur Verwendung von Segment Builder finden Sie im [Handbuch zur Benutzeroberfläche von Segment Builder](/help/segmentation/ui/segment-builder.md).

Um diese Besucher zu finden, müssen Sie zunächst ein **[!UICONTROL Page View]** Ereignis zu Ihrer Audience hinzufügen. Wählen Sie die Registerkarte **[!UICONTROL Events]** unter **[!UICONTROL Fields]** aus, ziehen Sie das **[!UICONTROL Page View]** Ereignis per Drag-and-Drop und fügen Sie es zum Bereich Ereignisse hinzu.

![Die Registerkarte &quot;[!UICONTROL Events]&quot; im Abschnitt &quot;[!UICONTROL Fields]&quot; ist hervorgehoben, während das [!UICONTROL Page View]Ereignis“ angezeigt wird](../assets/offsite-retargeting/add-page-view.png)

Wählen Sie das neu hinzugefügte **[!UICONTROL Page View]** aus. Ändern Sie den Lookback-Zeitraum von **[!UICONTROL Any time]** auf **[!UICONTROL This month]** und ändern Sie die Ereignisregel so, dass sie (**5)**.

![Details zum hinzugefügten [!UICONTROL Page View] werden angezeigt.](../assets/offsite-retargeting/edit-event.png)

Nachdem Sie Ihr Ereignis hinzugefügt haben, müssen Sie ein -Attribut hinzufügen. Da Sie mit nicht authentifizierten Besuchern arbeiten, können Sie das soeben erstellte berechnete Attribut hinzufügen. Mit diesem neu erstellten berechneten Attribut können Partner-IDs mit einer Zielgruppe verknüpft werden.

Um das berechnete Attribut hinzuzufügen, wählen Sie unter **[!UICONTROL Attributes]** die Option **[!UICONTROL XDM Individual Profile]** und **[Mandanten-ID Ihres Unternehmens](/help/xdm/api/getting-started.md#know-your-tenant-id) aus.**, **[!UICONTROL SystemComputedAttributes]** und **[!UICONTROL PartnerID]**. Fügen Sie nun die **[!UICONTROL Value]** des berechneten Attributs zum Abschnitt „Attribute“ der Arbeitsfläche hinzu.

![Der Ordnerpfad für den Zugriff auf das berechnete Attribut wird angezeigt.](../assets/offsite-retargeting/access-computed-attribute.png)

Suchen Sie außerdem nach **[!UICONTROL Personal Email]** und fügen Sie das unten stehende **[!UICONTROL Address]** Attribut **[!UICONTROL PartnerID]** zum Abschnitt „Attribute“ der Arbeitsfläche hinzu.

![Das [!UICONTROL PartnerID] berechnete Attribut und das [!UICONTROL Personal Email Address] Attribut werden auf der Arbeitsfläche von Segment Builder hervorgehoben.](../assets/offsite-retargeting/added-attributes.png)

Nachdem Sie Ihre Attribute hinzugefügt haben, müssen Sie deren Auswertungskriterien festlegen. Legen Sie **[!UICONTROL PartnerID]** das Kriterium auf **[!UICONTROL exists]** und **[!UICONTROL Address]** das Kriterium auf **[!UICONTROL does not exist]** fest.

![Die Eigenwerte der Attribute sind hervorgehoben.](../assets/offsite-retargeting/set-attribute-values.png)

Sie haben jetzt erfolgreich eine Zielgruppe erstellt, die nach Besuchern mit hoher Intensität sucht, die über eine vom Partner bereitgestellte ID verfügen, sich aber noch nicht für Ihre Site angemeldet haben. Benennen Sie Ihre Audience mit „Retargeting nicht authentifizierter Benutzer“ und wählen Sie **[!UICONTROL Save]** aus, um die Erstellung Ihrer Audience abzuschließen.

![Die Zielgruppeneigenschaften sind hervorgehoben.](../assets/offsite-retargeting/save-audience-properties.png)

## Zielgruppe aktivieren {#activate-audience}

Nachdem Sie Ihre Zielgruppe erfolgreich erstellt haben, können Sie diese Zielgruppe jetzt für nachgelagerte Ziele aktivieren. Wählen Sie in der linken Navigationsleiste **[!UICONTROL Audiences]** aus, suchen Sie die neu erstellte Zielgruppe, klicken Sie auf das Symbol mit den Auslassungspunkten und wählen Sie **[!UICONTROL Activate to destination]** aus.

![Die Schaltfläche &quot;[!UICONTROL Activate to destination]&quot; ist hervorgehoben.](../assets/offsite-retargeting/activate-to-destination.png)

>[!NOTE]
>
>Alle Zieltypen, einschließlich dateibasierter Ziele, unterstützen die Zielgruppenaktivierung mit Partner-IDs.
>
>Weitere Informationen zum Aktivieren von Zielgruppen für ein Ziel finden Sie unter [Aktivierung - Übersicht](/help/destinations/ui/activation-overview.md).

Die Seite **[!UICONTROL Activate destination]** wird angezeigt. Auf dieser Seite können Sie auswählen, für welches Ziel Sie Ihr Ziel aktivieren möchten. Wählen Sie nach Auswahl des gewünschten Ziels **[!UICONTROL Next]** aus.

![Das Ziel, für das Sie die Zielgruppe aktivieren möchten, ist hervorgehoben.](../assets/offsite-retargeting/select-destination.png)

Die Seite **[!UICONTROL Scheduling]** wird angezeigt. Auf dieser Seite können Sie einen Zeitplan erstellen, der bestimmt, wie oft die Zielgruppe aktiviert werden soll. Wählen Sie **[!UICONTROL Create schedule]** aus, um einen Zeitplan für die Zielgruppenaktivierung zu erstellen.

![Die Schaltfläche &quot;[!UICONTROL Create schedule]&quot; ist hervorgehoben.](../assets/offsite-retargeting/select-create-schedule.png)

Das [!UICONTROL Scheduling]-Popover wird angezeigt. Auf dieser Seite können Sie den Zeitplan für die Aktivierung Ihrer Audience erstellen. Wählen Sie nach dem Konfigurieren des Zeitplans **[!UICONTROL Create]** aus, um fortzufahren.

![Das Pop-up „Zeitplan konfigurieren“ wird angezeigt.](../assets/offsite-retargeting/configure-schedule.png)

Nachdem Sie die Planungsdetails bestätigt haben, wählen Sie **[!UICONTROL Next]** aus.

![Die Details des Zeitplans werden angezeigt.](../assets/offsite-retargeting/created-schedule.png)

Die Seite **[!UICONTROL Select attributes]** wird angezeigt. Auf dieser Seite können Sie auswählen, welche Attribute Sie zusammen mit der aktivierten Zielgruppe exportieren möchten. Sie sollten zumindest die Partner-ID einschließen, damit Sie die Besucher identifizieren können, die Sie erneut ansprechen möchten. Wählen Sie **[!UICONTROL Add new mapping]** aus und suchen Sie nach dem berechneten Attribut. Wählen Sie nach dem Hinzufügen der erforderlichen Attribute **[!UICONTROL Next]** aus.

![Sowohl die Schaltfläche &quot;[!UICONTROL Add new mapping]&quot; als auch das berechnete Attribut sind hervorgehoben.](../assets/offsite-retargeting/add-new-mapping.png)

Die Seite **[!UICONTROL Review]** wird angezeigt. Auf dieser Seite können Sie die Details Ihrer Zielgruppenaktivierung überprüfen. Wenn Sie mit den angegebenen Details zufrieden sind, wählen Sie **[!UICONTROL Finish]** aus.

![Die Seite [!UICONTROL Review] wird mit Details zur Zielgruppenaktivierung angezeigt.](../assets/offsite-retargeting/review-destination-activation.png)

Sie haben jetzt eine Zielgruppe nicht authentifizierter Benutzer für ein nachgelagertes Ziel für das weitere Retargeting aktiviert.

## Andere Anwendungsfälle {#other-use-cases}

Sie können weitere Anwendungsfälle erkunden, die über die Partnerdatenunterstützung in Real-Time CDP aktiviert wurden:

- [Gewinnen und gewinnen Sie neue Kunden](./prospecting.md) mithilfe von Partnerdaten.
- [Personalisieren von Onsite](./offsite-retargeting.md)Erlebnissen mit Partnerunterstützung der Besuchererkennung.
- [Erstanbieterprofile ergänzen](./supplement-first-party-profiles.md) durch von Partnern bereitgestellte Attribute.
