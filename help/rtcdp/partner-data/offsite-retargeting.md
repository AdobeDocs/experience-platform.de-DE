---
title: Offsite-Retargeting nicht authentifizierter Besucher
description: Erfahren Sie, wie Sie nicht authentifizierte Benutzer erneut ansprechen können, indem Sie mit Interessenten-IDs ein berechnetes Attribut erstellen, das zur Erstellung einer Audience nicht authentifizierter Benutzer verwendet werden kann.
feature: Use Cases, Customer Acquisition
exl-id: cffa3873-d713-445a-a3e1-1edf1aa8eebb
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1462'
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

Sie können nicht nur Zielgruppen erstellen, die auf der Interaktion vor Ort basieren, um Marketing-Nachrichten zu personalisieren, sondern Sie können auch den Adobe-Support für Partner-IDs verwenden, um über Paid-Media-Ziele hinweg erneut mit Besuchern zu interagieren.

## Voraussetzungen und Planung {#prerequisites-and-planning}

Beachten Sie bei der Planung von Retargeting für nicht authentifizierte Besucher während Ihres Planungsprozesses die folgenden Voraussetzungen:

- Habe ich die Partner-IDs mit den richtigen Identity-Namespaces eingerichtet?

Um den Anwendungsfall zu implementieren, verwenden Sie außerdem die folgenden Real-Time CDP-Funktionen und Benutzeroberflächenelemente. Stellen Sie sicher, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu gewähren.

- [Zielgruppen](../../segmentation/home.md)
- [Berechnete Attribute](../../profile/computed-attributes/overview.md)
- [Ziele](../../destinations/home.md)
- [Web SDK](../../web-sdk/home.md)

## Holen von Partnerdaten in Real-Time CDP {#get-data-in}

Um eine Zielgruppe nicht authentifizierter Besucher zu erstellen, müssen Sie zunächst Ihre Partnerdaten in Real-Time CDP importieren.

Informationen zum optimalen Importieren von Daten in Real-Time CDP mithilfe von Web SDK finden Sie in den [Abschnitten Datenverwaltung und Ereignisdatenerfassung](./onsite-personalization.md#data-management) des Anwendungsfalls Personalisierung vor Ort.

## Von Partnern bereitgestellte IDs vorziehen {#bring-partner-ids-forward}

Nachdem Sie die vom Partner bereitgestellten IDs in einen Ereignis-Datensatz importiert haben, müssen Sie diese Daten in die Profildatensätze übertragen. Dazu können Sie berechnete Attribute verwenden.

Berechnete Attribute ermöglichen es Ihnen, Profilverhaltensdaten auf Profilebene schnell in aggregierte Werte zu konvertieren. Daher können Sie diese Ausdrücke, z. B. „Gesamtkauf über die gesamte Lebensdauer“, für das Profil verwenden, sodass Sie das berechnete Attribut einfach in Ihren Zielgruppen verwenden können. Weitere Informationen zu berechneten Attributen finden Sie unter [Berechnete Attribute - Übersicht](../../profile/computed-attributes/overview.md).

Um auf berechnete Attribute zuzugreifen, wählen Sie **[!UICONTROL Profile]** gefolgt von **[!UICONTROL Berechnete Attribute]** und **[!UICONTROL Berechnetes Attribut erstellen]**.

![Die Schaltfläche [!UICONTROL Berechnete Attribute erstellen] ist zusätzlich zur Registerkarte [!UICONTROL Berechnete Attribute] im [!UICONTROL Profile] Arbeitsbereich hervorgehoben.](../assets/offsite-retargeting/create-ca.png)

Die **[!UICONTROL Berechnetes Attribut erstellen]** wird angezeigt. Auf dieser Seite können Sie die Komponenten zum Erstellen Ihres berechneten Attributs verwenden.

![Der Arbeitsbereich „Berechnete Attribute erstellen“ wird angezeigt.](../assets/offsite-retargeting/ca-page.png)

>[!NOTE]
>
>Ausführlichere Informationen zum Erstellen berechneter Attribute finden Sie im [Handbuch zur Benutzeroberfläche für berechnete Attribute](../../profile/computed-attributes/ui.md).

Für diesen Anwendungsfall können Sie ein berechnetes Attribut erstellen, das, wenn die Partner-ID vorhanden ist, den neuesten Wert der Partner-ID innerhalb der letzten 24 Stunden abruft.

Über die Suchleiste können Sie das Ereignis „Partner-ID“ suchen und [, das Sie während des Anwendungsfalls „Personalisierung vor Ort“ erstellt haben](#get-data-in) zur Arbeitsfläche für berechnete Attribute hinzufügen.

![Die Registerkarte [!UICONTROL Ereignisse] und die Suchleiste sind hervorgehoben.](../assets/offsite-retargeting/ca-add-partner-id.png)

Nachdem Sie der Definition das Ereignis „Partner-ID“ hinzugefügt haben, legen Sie die Ereignisfilterbedingung auf &quot;**[!UICONTROL Vorhanden]** fest und legen Sie die Ereignisfilterbedingung auf den Wert **[!UICONTROL Zuletzt verwendet]** der hinzugefügten Partner-ID fest, wobei der Lookback-Zeitraum 24 Stunden beträgt.

![Die Definition des berechneten Attributs, das Sie erstellen möchten, ist hervorgehoben.](../assets/offsite-retargeting/ca-add-definition.png)

Geben Sie dem berechneten Attribut einen geeigneten Namen (z. B. „Partner-ID„) und eine Beschreibung, und wählen Sie dann **[!UICONTROL Publish]** aus, um den Prozess zur Erstellung des berechneten Attributs abzuschließen.

![Die grundlegenden Informationen des berechneten Attributs, das Sie erstellen möchten, sind hervorgehoben.](../assets/offsite-retargeting/ca-publish.png)

## Erstellen einer Zielgruppe mit dem berechneten Attribut {#create-audience}

Nachdem Sie das berechnete Attribut erstellt haben, können Sie dieses berechnete Attribut verwenden, um eine Zielgruppe zu erstellen. In diesem Beispiel erstellen Sie eine Zielgruppe aus Besuchern, die Ihre Website in diesem Monat mehr als fünfmal besucht haben, sich aber noch nicht angemeldet haben.

Um eine Zielgruppe zu erstellen, wählen Sie **[!UICONTROL Zielgruppen]** und dann **[!UICONTROL Zielgruppe erstellen]** aus.

![Die Schaltfläche [!UICONTROL Zielgruppe erstellen] ist hervorgehoben.](../assets/offsite-retargeting/create-audience.png)

Es wird ein Dialogfeld angezeigt, in dem Sie zwischen „Zielgruppe [!UICONTROL &quot; &#x200B;] „Regel [!UICONTROL &quot; &#x200B;] können. Wählen **[!UICONTROL Regel erstellen]** gefolgt von **[!UICONTROL Erstellen]** aus.

![Die Schaltfläche [!UICONTROL Regel erstellen] ist hervorgehoben.](../assets/offsite-retargeting/select-build-rule.png)

Die Seite Segment Builder wird angezeigt. Auf dieser Seite können Sie die Komponenten zum Aufbau Ihrer Audience verwenden.

![Der Segment Builder wird angezeigt.](../assets/offsite-retargeting/segment-builder.png)

>[!NOTE]
>
>Ausführlichere Informationen zur Verwendung von Segment Builder finden Sie im [Handbuch zur Benutzeroberfläche von Segment Builder](../../segmentation/ui/segment-builder.md).

Um diese Besucher zu finden, müssen Sie Ihrer Zielgruppe zunächst ein Ereignis **[!UICONTROL Seitenansicht]** hinzufügen. Wählen Sie die **[!UICONTROL Ereignisse]** unter **[!UICONTROL Felder]** aus, ziehen Sie das **[!UICONTROL Seitenansicht]**-Ereignis per Drag-and-Drop und fügen Sie es zum Bereich „Ereignisse“ hinzu.

![Die Registerkarte [!UICONTROL Ereignisse] im Abschnitt [!UICONTROL Felder] ist hervorgehoben, während [!UICONTROL Seitenansicht]Ereignis.](../assets/offsite-retargeting/add-page-view.png) angezeigt wird

Wählen Sie das neu hinzugefügte **[!UICONTROL Seitenansicht]**-Ereignis aus. Ändern Sie den Lookback-Zeitraum von **[!UICONTROL Beliebig]** auf **[!UICONTROL Diesen Monat]** und ändern Sie die Ereignisregel so, dass sie **Mindestens 5**.

![Details des hinzugefügten Ereignisses [!UICONTROL Seitenansicht] werden angezeigt.](../assets/offsite-retargeting/edit-event.png)

Nachdem Sie Ihr Ereignis hinzugefügt haben, müssen Sie ein -Attribut hinzufügen. Da Sie mit nicht authentifizierten Besuchern arbeiten, können Sie das soeben erstellte berechnete Attribut hinzufügen. Mit diesem neu erstellten berechneten Attribut können Partner-IDs mit einer Zielgruppe verknüpft werden.

Um das berechnete Attribut hinzuzufügen, wählen **[!UICONTROL Attribute]** die Option **[!UICONTROL XDM Individual Profile]** und anschließend **[Mandanten-ID Ihres Unternehmens](../../xdm/api/getting-started.md#know-your-tenant-id).**, **[!UICONTROL SystemComputedAttributes]** und **[!UICONTROL PartnerID]**. Fügen Sie nun den **[!UICONTROL Wert]** des berechneten Attributs zum Abschnitt „Attribute“ der Arbeitsfläche hinzu.

![Der Ordnerpfad für den Zugriff auf das berechnete Attribut wird angezeigt.](../assets/offsite-retargeting/access-computed-attribute.png)

Suchen Sie außerdem nach **[!UICONTROL Persönliche E-Mail]** und fügen Sie das Attribut **[!UICONTROL Adresse]** unter **[!UICONTROL PartnerID]** zum Abschnitt „Attribute“ der Arbeitsfläche hinzu.

![Das berechnete Attribut [!UICONTROL PartnerID] und das Attribut [!UICONTROL Persönliche E-Mail-]) werden auf der Arbeitsfläche von Segment Builder hervorgehoben.](../assets/offsite-retargeting/added-attributes.png)

Nachdem Sie Ihre Attribute hinzugefügt haben, müssen Sie deren Auswertungskriterien festlegen. Legen Sie **[!UICONTROL PartnerID]** das Kriterium auf **[!UICONTROL exists]** und für **[!UICONTROL Address]** das Kriterium auf **[!UICONTROL Does Not exists]** fest.

![Die Eigenwerte der Attribute sind hervorgehoben.](../assets/offsite-retargeting/set-attribute-values.png)

Sie haben jetzt erfolgreich eine Zielgruppe erstellt, die nach Besuchern mit hoher Intensität sucht, die über eine vom Partner bereitgestellte ID verfügen, sich aber noch nicht für Ihre Site angemeldet haben. Benennen Sie Ihre Audience mit „Retargeting nicht authentifizierter Benutzer“ und wählen Sie **[!UICONTROL Speichern]** aus, um die Erstellung Ihrer Audience abzuschließen.

![Die Zielgruppeneigenschaften sind hervorgehoben.](../assets/offsite-retargeting/save-audience-properties.png)

## Zielgruppe aktivieren {#activate-audience}

Nachdem Sie Ihre Zielgruppe erfolgreich erstellt haben, können Sie diese Zielgruppe jetzt für nachgelagerte Ziele aktivieren. Wählen Sie **[!UICONTROL Zielgruppen]** in der linken Navigationsleiste aus, suchen Sie die neu erstellte Zielgruppe, klicken Sie auf das Symbol mit den Auslassungspunkten und wählen Sie **[!UICONTROL Für Ziel aktivieren]**.

![Die Schaltfläche [!UICONTROL Für Ziel aktivieren] ist hervorgehoben.](../assets/offsite-retargeting/activate-to-destination.png)

>[!NOTE]
>
>Alle Zieltypen, einschließlich dateibasierter Ziele, unterstützen die Zielgruppenaktivierung mit Partner-IDs.
>
>Weitere Informationen zum Aktivieren von Zielgruppen für ein Ziel finden Sie unter [Aktivierung - Übersicht](../../destinations/ui/activation-overview.md).

Die **[!UICONTROL Ziel aktivieren]** wird angezeigt. Auf dieser Seite können Sie auswählen, für welches Ziel Sie Ihr Ziel aktivieren möchten. Klicken Sie nach Auswahl des gewünschten Ziels auf **[!UICONTROL Weiter]**.

![Das Ziel, für das Sie die Zielgruppe aktivieren möchten, ist hervorgehoben.](../assets/offsite-retargeting/select-destination.png)

Die **[!UICONTROL Planung]** wird angezeigt. Auf dieser Seite können Sie einen Zeitplan erstellen, der bestimmt, wie oft die Zielgruppe aktiviert werden soll. Wählen Sie **[!UICONTROL Zeitplan erstellen]**, um einen Zeitplan für die Zielgruppenaktivierung zu erstellen.

![Die Schaltfläche [!UICONTROL Zeitplan erstellen] ist hervorgehoben.](../assets/offsite-retargeting/select-create-schedule.png)

Das [!UICONTROL Planung]-Popup wird angezeigt. Auf dieser Seite können Sie den Zeitplan für die Aktivierung Ihrer Audience erstellen. Klicken Sie nach dem Konfigurieren des Zeitplans auf **[!UICONTROL Erstellen]**, um fortzufahren.

![Das Pop-up „Zeitplan konfigurieren“ wird angezeigt.](../assets/offsite-retargeting/configure-schedule.png)

Klicken Sie nach Bestätigung der Zeitplandetails auf **[!UICONTROL Weiter]**.

![Die Details des Zeitplans werden angezeigt.](../assets/offsite-retargeting/created-schedule.png)

Die **[!UICONTROL Attribute auswählen]** wird angezeigt. Auf dieser Seite können Sie auswählen, welche Attribute Sie zusammen mit der aktivierten Zielgruppe exportieren möchten. Sie sollten zumindest die Partner-ID einschließen, damit Sie die Besucher identifizieren können, die Sie erneut ansprechen möchten. Wählen **[!UICONTROL Neue Zuordnung hinzufügen]** und suchen Sie nach dem berechneten Attribut. Nachdem Sie die erforderlichen Attribute hinzugefügt haben, klicken Sie auf **[!UICONTROL Weiter]**.

![Sowohl die Schaltfläche [!UICONTROL Neue Zuordnung hinzufügen] als auch das berechnete Attribut sind hervorgehoben.](../assets/offsite-retargeting/add-new-mapping.png)

Die **[!UICONTROL &quot;]**&quot; wird angezeigt. Auf dieser Seite können Sie die Details Ihrer Zielgruppenaktivierung überprüfen. Wenn Sie mit den angegebenen Details zufrieden sind, klicken Sie auf **[!UICONTROL Beenden]**.

![Die Seite [!UICONTROL Überprüfen] wird mit Details zur Zielgruppenaktivierung angezeigt.](../assets/offsite-retargeting/review-destination-activation.png)

Sie haben jetzt eine Zielgruppe nicht authentifizierter Benutzer für ein nachgelagertes Ziel für das weitere Retargeting aktiviert.

## Andere Anwendungsfälle {#other-use-cases}

Sie können weitere Anwendungsfälle erkunden, die über die Partnerdatenunterstützung in Real-Time CDP aktiviert wurden:

- [Gewinnen und gewinnen Sie neue Kunden](./prospecting.md) mithilfe von Partnerdaten.
- [Personalisieren von Onsite](./offsite-retargeting.md)Erlebnissen mit Partnerunterstützung der Besuchererkennung.
- [Erstanbieterprofile ergänzen](./supplement-first-party-profiles.md) durch von Partnern bereitgestellte Attribute.
