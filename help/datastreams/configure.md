---
title: Erstellen und Konfigurieren von Datenspeichern
description: Erfahren Sie, wie Sie Ihre Client-seitige Web SDK-Integration mit anderen Adobe-Produkten und Drittanbieterzielen verbinden.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: b87cb25ac791bebbf865f8513f2b4b482a1531bc
workflow-type: tm+mt
source-wordcount: '2817'
ht-degree: 52%

---


# Erstellen und Konfigurieren von Datenspeichern

Dieses Dokument beschreibt die Schritte zum Konfigurieren eines [Datenstroms](./overview.md) in der Benutzeroberfläche.

## Zugriff auf den Arbeitsbereich [!UICONTROL Datenströme]

Sie können Datenströme in der Datenerfassungs-Benutzeroberfläche oder der Experience Platform-Benutzeroberfläche durch Auswählen von **[!UICONTROL Datenströme]** in der linken Navigationsleiste erstellen und verwalten.

![Registerkarte „Datenströme“ in der Datenerfassungs-Benutzeroberfläche](assets/configure/datastreams-tab.png)

In der Registerkarte **[!UICONTROL Datenströme]** wird eine Liste mit vorhandenen Datenströmen angezeigt, darunter auch der Anzeigename, die Kennung und das Datum der letzten Änderung. Um [seine Details anzuzeigen und Dienste zu konfigurieren](#view-details), wählen Sie den Namen eines Datastreams aus.

Um weitere Optionen für einen bestimmten Datastream anzuzeigen, wählen Sie das Symbol &quot;Mehr&quot;(**...**). Um die [grundlegende Konfiguration](#configure) für den Datastream zu aktualisieren, wählen Sie **[!UICONTROL Bearbeiten]** aus. Um den Datastream zu entfernen, wählen Sie **[!UICONTROL Löschen]** aus.

![Optionen zum Bearbeiten oder Löschen eines vorhandenen Datenstroms](assets/configure/edit-datastream.png)

## Erstellen eines Datenspeichers {#create}

Um einen Datenstrom zu erstellen, wählen Sie zunächst **[!UICONTROL Neuer Datenstrom]** aus.

![Neuen Datenspeicher auswählen](assets/configure/new-datastream-button.png)

Der Workflow zur Erstellung eines Datenstroms wird geöffnet, beginnend mit dem Konfigurationsschritt. Geben Sie hier einen Namen und eine optionale Beschreibung für den Datenstrom an.

Wenn Sie einen Datastream zur Verwendung in Experience Platform konfigurieren und auch das Web SDK verwenden, müssen Sie auch ein [ereignisbasiertes Experience-Datenmodell (XDM)-Schema](../xdm/classes/experienceevent.md) auswählen, das die Daten darstellt, die Sie für die Aufnahme planen.

![Basiskonfiguration für einen Datenstrom](assets/configure/configure.png)

### Geolocation und Netzwerksuche konfigurieren {#geolocation-network-lookup}

Mit den Einstellungen für Geolocation und Netzwerksuche können Sie die Granularität der geografischen Daten und Daten auf Netzwerkebene definieren, die Sie erfassen möchten.

Erweitern Sie den Abschnitt **[!UICONTROL Geolocation and network lookup]** , um die unten beschriebenen Einstellungen zu konfigurieren.

![Konfigurationsbildschirm für Datastream mit hervorgehobenen Geolocation- und Netzwerk-Lookup-Einstellungen.](assets/configure/geolookup.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Geo-Suche] | Aktiviert die Geolocation-Suche für die ausgewählten Optionen basierend auf der IP-Adresse des Besuchers. Zu den verfügbaren Optionen gehören: <ul><li>**Land**: Füllt `xdm.placeContext.geo.countryCode`</li><li>**Postleitzahl**: Füllt `xdm.placeContext.geo.postalCode`</li><li>**Bundesland/-staat**: Füllt `xdm.placeContext.geo.stateProvince`</li><li>**DMA**: Füllt `xdm.placeContext.geo.dmaID`</li><li>**Stadt**: Füllt `xdm.placeContext.geo.city`</li><li>**Latitude**: Füllt `xdm.placeContext.geo._schema.latitude`</li><li>**Längengrad**: Füllt `xdm.placeContext.geo._schema.longitude`</li></ul>Die Auswahl von **[!UICONTROL Stadt]**, **[!UICONTROL Breitengrad]** oder **[!UICONTROL Längengrad]** liefert Koordinaten mit bis zu zwei Dezimalstellen, unabhängig davon, welche anderen Optionen ausgewählt wurden. Dies gilt als Granularität auf Stadtebene.<br> <br> Wenn keine Option ausgewählt wird, werden die Geolocation-Suchen deaktiviert. Die Geolokation erfolgt vor der [!UICONTROL IP-Verschleierung], was bedeutet, dass sie von der Einstellung [!UICONTROL IP-Verschleierung] nicht betroffen ist. |
| [!UICONTROL Netzwerksuche] | Aktiviert die Netzwerksuche für die ausgewählten Optionen basierend auf der IP-Adresse des Besuchers. Zu den verfügbaren Optionen gehören: <ul><li>**Mobilnetzbetreiber**: Füllt `xdm.environment.carrier`</li><li>**Domäne**: Füllt `xdm.environment.domain`</li><li>**ISP**: Füllt `xdm.environment.ISP`</li><li>**Verbindungstyp**: Füllt `xdm.environment.connectionType`</li></ul> |

Wenn Sie eines der oben genannten Felder für die Datenerfassung aktivieren, stellen Sie sicher, dass Sie die [`context`](/help/web-sdk/commands/configure/context.md) -Array-Eigenschaft beim Konfigurieren des Web SDK korrekt festlegen.

Geolocation-Suchfelder verwenden die `context` Array-Zeichenfolge `"placeContext"`, während Netzwerksuchfelder die `context` Array-Zeichenfolge `"environment"` verwenden.

Stellen Sie außerdem sicher, dass jedes gewünschte XDM-Feld in Ihrem Schema vorhanden ist. Ist dies nicht der Fall, können Sie die von der Adobe bereitgestellte `Environment Details` Feldergruppe zu Ihrem Schema hinzufügen.

### Konfigurieren der Gerätesuche {#geolocation-device-lookup}

Mit den Einstellungen für die **[!UICONTROL Gerätesuche]** können Sie gerätespezifische Informationen auswählen, die Sie erfassen möchten.

Erweitern Sie den Abschnitt **[!UICONTROL Gerätesuche]** , um die unten beschriebenen Einstellungen zu konfigurieren.

![Konfigurationsbildschirm für den Datastraam mit hervorgehobenen Sucheinstellungen für das Gerät.](assets/configure/device-lookup.png)

>[!IMPORTANT]
>
>Die in der folgenden Tabelle angezeigten Einstellungen schließen sich gegenseitig aus. Es ist nicht möglich, beide Benutzeragenten-Daten *und* gleichzeitig für die Gerätesuche auszuwählen.

| Einstellung | Beschreibung |
| --- | --- |
| **[!UICONTROL Behalten Sie die Kopfzeilen von Benutzeragent und Client-Hinweisen bei]** | Wählen Sie diese Option, um nur die in der Benutzeragenten-Zeichenfolge gespeicherten Informationen zu erfassen. Diese Einstellung ist standardmäßig ausgewählt. Füllt `xdm.environment.browserDetails.userAgent` |
| **[!UICONTROL Verwenden Sie die Gerätesuche, um die folgenden Informationen zu sammeln]** | Wählen Sie diese Option aus, wenn Sie eine oder mehrere der folgenden gerätespezifischen Informationen erfassen möchten: <ul><li>**[!UICONTROL Device]** -Informationen:<ul><li>**Gerätehersteller**: Füllt `xdm.device.manufacturer`</li><li>**Gerätemodell**: Füllt `xdm.device.modelNumber`</li><li>**Marketing-Name**: Füllt `xdm.device.model`</li></ul></li><li>**[!UICONTROL Hardware]**-Informationen: <ul><li>**Hardwaretyp**: Füllt `xdm.device.type`</li><li>**Anzeigehöhe**: Füllt `xdm.device.screenHeight`</li><li>**Anzeigebreite**: Füllt `xdm.device.screenWidth`</li><li>**Farbtiefe anzeigen**: Füllt `xdm.device.colorDepth`</li></ul></li><li>**[!UICONTROL Browser]** -Informationen: <ul><li>**Browser-Anbieter**: Füllt `xdm.environment.browserDetails.vendor`</li><li>**Browsername**: Füllt `xdm.environment.browserDetails.name`</li><li>**Browserversion**: Füllt `xdm.environment.browserDetails.version`</li></ul></li><li>**[!UICONTROL Betriebssysteminformationen]**: <ul><li>**Betriebssystemanbieter**: Füllt `xdm.environment.operatingSystemVendor`</li><li>**OS name**: Füllt `xdm.environment.operatingSystem`</li><li>**Betriebssystemversion**: Füllt `xdm.environment.operatingSystemVersion`</li></ul></li></ul>Informationen zur Gerätesuche können nicht zusammen mit Benutzeragent und Client-Hinweisen erfasst werden. Wenn Sie auswählen, Geräteinformationen zu erfassen, wird die Erfassung von Benutzeragent- und Client-Hinweisen deaktiviert und umgekehrt. |
| **[!UICONTROL Erfassen Sie keine Geräteinformationen]** | Wählen Sie diese Option aus, wenn Sie keine Gerätesucherinformationen erfassen möchten. Es werden keine Daten zu Gerät, Hardware, Browser, Betriebssystem, Benutzeragent oder Client-Hinweis erfasst. |

Wenn Sie eines der oben genannten Felder für die Datenerfassung aktivieren, stellen Sie sicher, dass Sie die [`context`](/help/web-sdk/commands/configure/context.md) -Array-Eigenschaft beim Konfigurieren des Web SDK korrekt festlegen.

Geräte- und Hardwareinformationen verwenden die `context` Array-Zeichenfolge `"device"`, während Browser- und Betriebssysteminformationen die `context` Array-Zeichenfolge `"environment"` verwenden.

Stellen Sie außerdem sicher, dass jedes gewünschte XDM-Feld in Ihrem Schema vorhanden ist. Ist dies nicht der Fall, können Sie die von der Adobe bereitgestellte `Environment Details` Feldergruppe zu Ihrem Schema hinzufügen.

### Erweiterte Optionen konfigurieren {#@advanced-options}

Um erweiterte Konfigurationsoptionen anzuzeigen, wählen Sie **[!UICONTROL Erweiterte Optionen]** aus. Hier können Sie zusätzliche Datenspeichereinstellungen konfigurieren, wie IP-Verschleierung, Erstanbieter-ID-Cookies und mehr.

![Erweiterte Konfigurationsoptionen](assets/configure/advanced-settings.png)

>[!IMPORTANT]
>
> Sie sind dafür verantwortlich sicherzustellen, dass Sie alle erforderlichen Berechtigungen, Einverständnisse, Genehmigungen und Autorisierungen erhalten haben, die nach den geltenden Gesetzen und Vorschriften erforderlich sind, um personenbezogene Daten zu erfassen, zu verarbeiten und zu übermitteln, einschließlich genauer Geolocation-Informationen.
> 
> Ihre Auswahl der Verschleierung von IP-Adressen wirkt sich nicht auf die Ebene der Geolocation-Informationen aus, die von der IP-Adresse abgeleitet und an Ihre konfigurierten Adobe-Lösungen gesendet werden. Die Suche nach Geolokalisierungen muss begrenzt oder separat deaktiviert werden.

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL IP-Verschleierung] | Gibt den Typ der IP-Verschleierung an, die auf dem Datenstrom angewendet werden soll. Die IP-Verschleierungseinstellung wirkt sich auf jede Verarbeitung basierend auf der Kunden-IP aus. Dies umfasst alle Experience Cloud-Dienste, die Daten aus Ihrem Datenstrom empfangen. <p>Verfügbare Optionen:</p> <ul><li>**[!UICONTROL Keine]**: Deaktiviert die IP-Verschleierung. Die vollständige Benutzer-IP-Adresse wird über den Datastream gesendet.</li><li>**[!UICONTROL Teilweise]**: Bei IPv4-Adressen wird das letzte Oktett der Benutzer-IP-Adresse verschleiert. Bei IPv6-Adressen werden die letzten 80 Bits der Adresse verschleiert. <p>Beispiele:</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL Vollständig]**: Verschleiert die gesamte IP-Adresse. <p>Beispiele:</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> Auswirkungen der IP-Verschleierung auf andere Adobe-Produkte: <ul><li>**Adobe Target**: Die IP-Verschleierung auf Datastraamebene [!UICONTROL 3} wird vor der in Adobe Target durchgeführten [!UICONTROL IP-Verschleierung] auf alle in der Anfrage vorhandenen IP-Adressen angewendet. ] Wenn beispielsweise die Option [!UICONTROL IP-Verschleierung] auf der Datastreamebene auf **[!UICONTROL Full]** und die Option für die IP-Verschleierung der Adobe Target auf **[!UICONTROL Letzte Oktettverschleierung]** eingestellt ist, erhält Adobe Target eine vollständig verschleierte IP. Wenn die Option [!UICONTROL IP-Verschleierung] auf der Datenasterebene auf **[!UICONTROL Teil]** gesetzt ist und die IP-Verschleierungsoption der Adobe Target auf **[!UICONTROL Full]** eingestellt ist, erhält Adobe Target eine teilweise verschleierte IP-Adresse und wendet dann die vollständige Verschleierung an. Die IP-Verschleierung von Adobe Target wird unabhängig vom Datastraam verwaltet. Weitere Informationen finden Sie in der Adobe Target-Dokumentation zu [IP-Verschleierung](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/privacy.html) und [Geolokalisierung](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html).</li><li>**Audience Manager**: Die Einstellung [!UICONTROL IP-Verschleierung] auf Datastraamebene wird angewendet, bevor die im Audience Manager ausgeführte [!UICONTROL IP-Verschleierung] auf alle in der Anfrage vorhandenen IP-Adressen angewendet wird. Jede von Audience Manager durchgeführte Geolokalisierungssuche ist von der Option [!UICONTROL IP-Verschleierung] auf Datenstromebene betroffen. Eine Geolocation-Suche in Audience Manager basierend auf einer vollständig verschleierten IP führt zu einer unbekannten Region, und alle Segmente, die auf den resultierenden Geolocation-Daten basieren, werden nicht realisiert. Weitere Informationen finden Sie in der Audience Manager-Dokumentation unter [IP-Verschleierung](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html).</li><li>**Adobe Analytics**: Wenn die IP-Verschleierungseinstellung auf Datastream-Ebene auf **[!UICONTROL Full]** festgelegt ist, behandelt Adobe Analytics die IP-Adresse als leer. Dies wirkt sich auf alle Analytics-Prozesse aus, die von der IP-Adresse abhängig sind, wie z. B. die Geolocation-Suche und IP-Filterung. Damit Analytics die nicht verschleierten oder teilweise verschleierten IP-Adressen erhält, setzen Sie die Einstellung für die IP-Verschleierung auf **[!UICONTROL Teil]** oder **[!UICONTROL Keine]**. Teilweise verschleierte und nicht verschleierte IP-Adressen können in Analytics weiter verschleiert werden. Weitere Informationen zum Aktivieren der IP-Verschleierung in Analytics finden Sie in der Adobe Analytics- [Dokumentation](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html?lang=de) . Wenn die IP-Adresse vollständig verschleiert ist und der Seitentreffer weder ein [!DNL ECID] noch ein [!DNL VisitorID] aufweist, verliert Analytics den Treffer, anstatt eine [Fallback-ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-ids.html?lang=en) zu generieren, die teilweise auf der IP-Adresse basiert.</li></ul> |
| [!UICONTROL First-Party-ID-Cookie] | Wenn diese Einstellung aktiviert ist, weist sie das Edge-Netzwerk an, bei der Suche nach einer [First-Party-Geräte-ID](../web-sdk/identity/first-party-device-ids.md) ein bestimmtes Cookie zu verwenden, anstatt nach diesem Wert in der Identity Map zu suchen.<br><br>Wenn Sie diese Einstellung aktivieren, müssen Sie den Namen des Cookies angeben, in dem die ID gespeichert werden soll. |
| [!UICONTROL Synchronisierung der Third-Party-ID] | ID-Synchronisationen können in Container zusammengefasst werden, damit verschiedene ID-Synchronisationen zu unterschiedlichen Zeiten ausgeführt werden können. Wenn diese Einstellung aktiviert ist, können Sie festlegen, welcher Container mit ID-Synchronisationen für diesen Datenstrom ausgeführt werden soll. |
| [!UICONTROL Container-ID der Drittanbieter-ID-Synchronisierung] | Die numerische ID des Containers, der für die ID-Synchronisierung von Drittanbietern verwendet werden soll. |
| [!UICONTROL Überschreibungen der Container-ID] | In diesem Abschnitt können Sie zusätzliche IDs für ID-Synchronisierungs-Container von Drittanbietern definieren, die Sie verwenden können, um die standardmäßige zu überschreiben. |
| [!UICONTROL Zugriffstyp] | Legt den Authentifizierungstyp fest, den das Edge Network für den Datenstrom akzeptiert. <ul><li>**[!UICONTROL Gemischte Authentifizierung]**: Wenn diese Option aktiviert ist, akzeptiert das Edge Network sowohl authentifizierte als auch nicht authentifizierte Anfragen. Wählen Sie diese Option, wenn Sie das Web SDK oder das [Mobile SDK](https://developer.adobe.com/client-sdks/home/) zusammen mit der [Server-API](../server-api/overview.md) verwenden möchten. </li><li>**[!UICONTROL Nur authentifiziert]**: Wenn diese Option aktiviert ist, akzeptiert das Edge Network nur authentifizierte Anfragen. Wählen Sie diese Option aus, wenn Sie beabsichtigen, nur die Server-API zu verwenden und verhindern möchten, dass nicht authentifizierte Anfragen vom Edge Network verarbeitet werden.</li></ul> |
| [!UICONTROL Media Analytics] | Ermöglicht die Verarbeitung von Streaming-Tracking-Daten für die Edge Network-Integration über Experience Platform-SDKs oder die [Media Edge-API](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/getting-started/). Informationen zu Media Analytics finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=de). |

Wenn hier Ihren Datenstrom für Experience Platform konfigurieren, folgen Sie dem Tutorial zu [Datenvorbereitung für die Datenerfassung](./data-prep.md), um Ihre Daten einem Platform-Ereignisschema zuzuordnen, bevor Sie mit dieser Anleitung fortfahren. Wählen Sie andernfalls **[!UICONTROL Speichern]** und fahren Sie mit dem nächsten Abschnitt fort.

## Anzeigen von Datenstromdetails {#view-details}

Nachdem Sie einen neuen Datenstrom konfiguriert oder einen vorhandenen ausgewählt haben, um ihn anzuzeigen, wird die Detailseite für diesen Datenstrom angezeigt. Hier finden Sie weitere Informationen zum Datenstrom, einschließlich seiner Kennung.

![Detailseite für Datastraam.](assets/configure/view-details.png)

Im Bildschirm mit den Datenspeicherdetails können Sie [Services hinzufügen](#add-services), um Funktionen der Adobe Experience Cloud-Produkte zu aktivieren, auf die Sie Zugriff haben. Sie können auch die [Basiskonfiguration](#create) des Datenstroms bearbeiten, seine [Zuordnungsregeln](./data-prep.md) aktualisieren, [den Datenstrom kopieren](#copy) oder vollständig löschen.

## Hinzufügen von Services zu einem Datenstrom {#add-services}

Wählen Sie auf der Detailseite eines Datenstroms die Option **[!UICONTROL Service hinzufügen]** aus, um verfügbare Services für diesen Datenstrom hinzuzufügen.

![Wählen Sie Dienst hinzufügen aus, um fortzufahren.](assets/configure/add-service.png)

Wählen Sie im nächsten Bildschirm im Dropdown-Menü einen Service aus, der für diesen Datenstrom konfiguriert werden soll. In dieser Liste werden nur die Dienste angezeigt, auf die Sie Zugriff haben.

![Wählen Sie einen Dienst aus der Liste.](assets/configure/service-selection.png)

Wählen Sie den gewünschten Service aus, geben Sie die angezeigten Konfigurationsoptionen ein und wählen Sie dann **[!UICONTROL Speichern]** aus, um den Service zum Datenstrom hinzuzufügen. Alle hinzugefügten Services werden in der Detailansicht für den Datenstrom angezeigt.

![Zu einem Datenstrom hinzugefügte Services](assets/configure/services-added.png)

In den folgenden Unterabschnitten werden die Konfigurationsoptionen für die einzelnen Services beschrieben.

>[!NOTE]
>
>Jede Service-Konfiguration enthält den Umschalter **[!UICONTROL Aktiviert]**, der automatisch aktiviert wird, wenn der Service ausgewählt wird. Um den ausgewählten Service für diesen Datenstrom zu deaktivieren, wählen Sie nochmals den Umschalter **[!UICONTROL Aktiviert]** aus.

### Adobe Analytics-Einstellungen {#analytics}

Mit diesem Service wird festgelegt, ob und wie Daten an Adobe Analytics gesendet werden. Siehe [Senden von Daten an Adobe Analytics](/help/web-sdk/use-cases/adobe-analytics.md).

![Adobe Analytics-Datastream-Einstellungen.](assets/configure/analytics-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Report Suite-ID] | **(Erforderlich)** Die ID der Analytics Report Suite, an die Sie Daten senden möchten. Diese ID finden Sie in der Adobe Analytics-Benutzeroberfläche unter [!UICONTROL Administration] > [!UICONTROL ReportSuites]. Wenn mehrere Report Suites angegeben sind, werden die Daten in jede einzelne Report Suite kopiert. |
| [!UICONTROL Besucher-ID-Namespace] | (Optional) Der Namespace, den Sie für die Adobe Analytics [visitorID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=de) verwenden möchten. Wenn Sie ein Ereignis mit einem für diesen Namespace angegebenen Wert senden, wird es in Analytics automatisch als `visitorID` verwendet. |
| [!UICONTROL Report Suite-Überschreibungen] | In diesem Abschnitt können Sie zusätzliche Report Suite-IDs hinzufügen, die Sie verwenden können, um die Standard-ID zu überschreiben. |

### Adobe Audience Manager-Einstellungen {#audience-manager}

Mit diesem Service wird festgelegt, ob und wie Daten an Adobe Audience Manager gesendet werden. Zum Senden von Daten an Audience Manager müssen Sie nur diesen Abschnitt aktivieren. Die anderen Einstellungen sind optional, werden jedoch empfohlen.

![Adobe Audience Verwalten Sie die Einstellungen des Datenspeichers.](assets/configure/audience-manager-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Cookie-Ziele aktiviert] | Ermöglicht dem SDK das Freigeben von Segmentinformationen über [Cookie-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html?lang=de) in [!DNL Audience Manager]. |
| [!UICONTROL URL-Ziele aktiviert] | Ermöglicht dem SDK das Freigeben von Segmentinformationen über [URL-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html?lang=de) in [!DNL Audience Manager]. |

### Adobe Experience Platform-Einstellungen {#aep}

>[!IMPORTANT]
>
>Beachten Sie beim Aktivieren eines Datenstroms für Platform die aktuell verwendete Platform-Sandbox, die in der oberen Leiste der Benutzeroberfläche angezeigt wird.
>
>![Ausgewählte Sandbox](assets/configure/platform-sandbox.png)
>
>Sandboxes sind virtuelle Partitionen in Adobe Experience Platform, mit denen Sie Ihre Daten und Implementierungen von anderen in Ihrem Unternehmen isolieren können. Nachdem ein Datenstrom erstellt wurde, kann seine Sandbox nicht mehr geändert werden. Weitere Informationen zur Rolle von Sandboxes in Experience Platform finden Sie i der [Sandbox-Dokumentation](../sandboxes/home.md).

Mit diesem Service wird festgelegt, ob und wie Daten an Adobe Experience Platform gesendet werden.

![Adobe Experience Platform-Datastream-Einstellungen.](assets/configure/platform-config.png)

| Einstellung | Beschreibung |
|---| --- |
| [!UICONTROL Ereignis-Datensatz] | **(Erforderlich)** Wählen Sie den Platform-Datensatz aus, an den Kundenereignisdaten gestreamt werden. Dieses Schema muss die [XDM ExperienceEvent-Klasse](../xdm/classes/experienceevent.md) verwenden. Um weitere Datensätze hinzuzufügen, wählen Sie **[!UICONTROL Ereignis-Datensatz hinzufügen]** aus. |
| [!UICONTROL Profildatensatz] | Wählen Sie den Platform-Datensatz aus, an den Kundenattributdaten gesendet werden. Dieses Schema muss die [Klasse „XDM Individual Profile“](../xdm/classes/individual-profile.md) verwenden. |
| [!UICONTROL Offer Decisioning] | Aktiviert Offer decisioning für Web SDK-Implementierungen. Weitere Informationen zur Implementierung finden Sie im Handbuch zum Verwenden von Offer decisioning mit Web SDK](../web-sdk/personalization/offer-decisioning/offer-decisioning-overview.md) .[<br><br>Weitere Informationen zu Offer Decisioning-Funktionen finden Sie in der [Adobe Journey Optimizer-Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/starting-offer-decisioning.html?lang=de). |
| [!UICONTROL Edge-Segmentierung] | Aktiviert die [Kantensegmentierung](../segmentation/ui/edge-segmentation.md) für diesen Datastream. Wenn das [Web SDK](../web-sdk/home.md) oder die [Edge Network Server API](../server-api/overview.md) Daten über einen Datastream sendet, bei dem die Kantensegmentierung aktiviert ist, werden alle aktualisierten Zielgruppenmitgliedschaften für das betreffende Profil in der Antwort zurückgesendet.<br><br>Sie können diese Option in Kombination mit **[!UICONTROL Personalization-Zielen]** für Anwendungsfälle der Personalisierung von derselben Seite und nächsten Seiten über [Edge-Ziele](../destinations/ui/activate-edge-personalization-destinations.md) oder [!DNL Offer Decisioning] verwenden. |
| [!UICONTROL Personalisierungsziele] | Wenn diese Option nach dem Aktivieren des Kontrollkästchens [!UICONTROL Edge-Segmentierung] aktiviert wird, kann der Datenstrom mit Personalisierungszielen, wie etwa [benutzerdefinierte Personalisierung](../destinations/catalog/personalization/custom-personalization.md), verbunden werden.<br><br>Die genauen Schritte zum [Konfigurieren von Personalisierungszielen](../destinations/ui/activate-edge-personalization-destinations.md) finden Sie in der Dokumentation zu Zielen. |
| [!UICONTROL Adobe Journey Optimizer] | Aktiviert [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de) für diesen Datenspeicher. <br><br> Wenn diese Option aktiviert ist, kann der Datenstrom personalisierte Inhalte aus Web- und App-basierten Inbound-Kampagnen in [!DNL Adobe Journey Optimizer] zurückgeben. [!UICONTROL Edge-Segmentierung] muss aktiv sein. Wenn die Option [!UICONTROL Edge-Segmentierung] deaktiviert ist, ist diese Option grau ausgeblendet. |

### Adobe Target-Einstellungen {#target}

Mit diesem Service wird festgelegt, ob und wie Daten an Adobe Target gesendet werden.

![Adobe Target-Datastream-Einstellungen.](assets/configure/target-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Eigenschafts-Token] | Mit [!DNL Target] können Kunden Berechtigungen mithilfe von Eigenschaften steuern. Weitere Informationen zu Eigenschaften finden Sie in der Anleitung zum [Konfigurieren von Unternehmensberechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=de) in der [!DNL Target]-Dokumentation.<br><br>Das Eigenschafts-Token befindet sich in der Adobe Target-Benutzeroberfläche unter [!UICONTROL Einrichtung] > [!UICONTROL Eigenschaften]. |
| [!UICONTROL Target-Umgebungs-ID] | [Umgebungen in Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=de) helfen Ihnen in allen Entwicklungsphasen bei der Implementierung. Diese Einstellung gibt an, welche Umgebung Sie für diesen Datenstrom verwenden werden.<br><br>Empfohlen wird, der Einfachheit halber eine unterschiedliche Einstellung für jede Ihrer `dev`-, `stage`- und `prod`Datenstrom-Umgebungen auszuwählen. Wenn Sie jedoch bereits Adobe Target-Umgebungen definiert haben, können Sie diese verwenden. |
| [!UICONTROL Namespace der Target-Third-Party-ID] | Der Identity-Namespace für die `mbox3rdPartyId`, den Sie für diesen Datenstrom verwenden möchten. Wenn Sie eine [!DNL Customer Attributes] -Integration in Adobe Target verwenden oder `thirdPartyId` verwenden, um Profile über die [Adobe Target Profiles API](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profiles-api) zu aktualisieren oder zu erstellen, müssen Sie einen Namespace-Wert Ihrer Wahl angeben. Sie müssen diesen Namespace im Abschnitt `IdentityMap` Ihres XDM-Schemas verwenden, um die `customerID` oder `thirdPartyId` zu senden, die beim Hochladen der Kundenattribut-Datei oder in Ihren API-Aufrufen zur Profilaktualisierung verwendet werden.  Weitere Informationen dazu erhalten Sie im Handbuch zur [Implementierung der `mbox3rdPartyId` mit dem Web SDK](../web-sdk/personalization/adobe-target/using-mbox-3rdpartyid.md). |
| [!UICONTROL Eigenschafts-Token-Überschreibungen] | In diesem Abschnitt können Sie zusätzliche Eigenschafts-Token definieren, mit denen Sie den Standard überschreiben können. |

### Einstellungen zur [!UICONTROL Ereignisweiterleitung]

Mit diesem Service wird festgelegt, ob und wie Daten an die [Ereignisweiterleitung](../tags/ui/event-forwarding/overview.md) gesendet werden.

![Abschnitt &quot;Ereignisweiterleitung&quot;des Konfigurationsbildschirms des Datenspeichers.](assets/configure/event-forwarding-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Start-Eigenschaft] | **(Erforderlich)** Die Ereignisweiterleitungs-Eigenschaft, an die Sie Daten senden möchten. |
| [!UICONTROL Start-Umgebung] | **(Erforderlich)** Die Umgebung innerhalb der ausgewählten Eigenschaft, an die Sie Daten senden möchten. |

>[!NOTE]
>
>Sie können die Option **[!UICONTROL IDs manuell eingeben]** auswählen, um die Eigenschafts- und Umgebungsnamen manuell einzugeben, anstatt die Dropdown-Menüs zu verwenden.

## Kopieren eines Datenstroms {#copy}

Sie können eine Kopie eines vorhandenen Datenstroms erstellen und seine Details nach Bedarf ändern.

>[!NOTE]
>
>Datenströme können nur innerhalb derselben [Sandbox](../sandboxes/home.md) kopiert werden. Mit anderen Worten: Sie können den Datenstrom von einer Sandbox nicht in eine andere kopieren.

Wählen Sie auf der Hauptseite im Arbeitsbereich [!UICONTROL Datenströme] die Auslassungszeichen für den entsprechenden Datenstrom aus (**...**) und danach **[!UICONTROL Kopieren]**.

![Bild, das die in der Listenansicht des Datenspeichers ausgewählte Option Kopieren anzeigt.](assets/configure/copy-datastream-list.png)

Alternativ können Sie in der Detailansicht eines Datenstroms **[!UICONTROL Datenstrom kopieren]** auswählen.

![Kopieren Sie die Option, die in der Detailansicht des Datenspeichers ausgewählt wird.](assets/configure/copy-datastream-details.png)

Ein Bestätigungsdialogfeld erscheint, in dem Sie aufgefordert werden, einen eindeutigen Namen für den neuen, zu erstellenden Datenstrom sowie Details zu den Konfigurationsoptionen, die kopiert werden, anzugeben. Wenn Sie bereit sind, wählen Sie **[!UICONTROL Kopieren]** aus.

![Bestätigungsdialogfeld zum Kopieren eines Datenspeichers.](assets/configure/copy-datastream-confirm.png)

Die Hauptseite des Arbeitsbereichs [!UICONTROL Datenstrom] wird erneut angezeigt, diesmal mit dem neuen Datenstrom.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Datenströme in der Datenerfassungs-Benutzeroberfläche verwaltet werden. Weitere Informationen zum Installieren und Konfigurieren des Web SDK nach dem Einrichten eines Datenstroms finden Sie im [Handbuch E2E zur Datenerfassung](../collection/e2e.md#install).
