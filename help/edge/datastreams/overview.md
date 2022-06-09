---
title: Übersicht über Datenspeicher
description: Verbinden Sie Ihre Client-seitige Experience Platform SDK-Integration mit Adobe-Produkten und Zielen von Drittanbietern.
keywords: Konfiguration;Datastreams;datastreamId;edge;datastream id;Umgebungseinstellungen;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Ereignis-Datensatz;Target;Client-Code;Eigenschaft-Token;Target-Umgebungs-ID;Cookie-Ziele;URL-Ziele;Analytics Settings Blockreport suite id;Data Prep für Datenerfassung;Mappings;Mappings er;XDM Mapper;Mapper in Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: e0c39c20ce536b057367da2854901e33a3f67dd6
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 3%

---

# Übersicht über Datenspeicher

Ein Datastream stellt die serverseitige Konfiguration bei der Implementierung der Adobe Experience Platform Web- und Mobile-SDKs dar. Während [configure-Befehl](../fundamentals/configuring-the-sdk.md) im SDK steuert Elemente, die auf dem Client verarbeitet werden müssen (z. B. die `edgeDomain`), verarbeiten Datastreams alle anderen Konfigurationen für das SDK. Wenn eine Anforderung an das Adobe Experience Platform Edge Network gesendet wird, muss die `edgeConfigId` wird verwendet, um auf den Datastream zu verweisen. Auf diese Weise können Sie die serverseitige Konfiguration aktualisieren, ohne Codeänderungen auf Ihrer Website vornehmen zu müssen.

In diesem Dokument werden die Schritte zum Konfigurieren eines Datastreams in der Datenerfassungs-Benutzeroberfläche beschrieben.

>[!NOTE]
>
>Ihre Organisation muss für diese Funktion freigeschaltet sein, damit sie über die Benutzeroberfläche darauf zugreifen kann. Bitte füllen Sie Folgendes aus [Formular](https://adobe.ly/websdkaccess) , um den erforderlichen Zugriff anzufordern. Um Datenspeicher zu verwalten, muss Ihr Benutzerkonto einem Produktprofil für Tags in hinzugefügt werden. [!DNL Adobe Experience Platform].

## Zugriff auf [!UICONTROL Datenspeicher] Arbeitsbereich

Sie können Datenspeicher in der Datenerfassungs-Benutzeroberfläche erstellen und verwalten, indem Sie **[!UICONTROL Datenspeicher]** in der linken Navigation.

![Registerkarte &quot;Datenspeicher&quot;in der Benutzeroberfläche &quot;Datenerfassung&quot;](../images/datastreams/overview/datastreams-tab.png)

Die [!UICONTROL Datenspeicher] zeigt eine Liste der vorhandenen Datensätze an, einschließlich Anzeigename, Kennung und Datum der letzten Änderung. Wählen Sie den Namen eines Datastreams aus, um [Anzeigen der Details und Konfigurieren von Diensten](#view-details).

Wählen Sie das Symbol &quot;Mehr&quot;(**...**) für einen bestimmten Datastream, um weitere Optionen anzuzeigen. Auswählen **[!UICONTROL Bearbeiten]** , um die [Basiskonfiguration](#configure) für den Datastream oder wählen Sie **[!UICONTROL Löschen]** , um den Datastream zu entfernen.

![Optionen zum Bearbeiten oder Löschen und Löschen vorhandener Datenspeicher](../images/datastreams/overview/edit-datastream.png)

## Neuen Datastream erstellen {#create}

Um einen Datastream zu erstellen, wählen Sie zunächst **[!UICONTROL Neuer Datenspeicher]**.

![Neuen Datenspeicher auswählen](../images/datastreams/overview/new-datastream-button.png)

Der Workflow zur Erstellung von Datensätzen wird angezeigt, beginnend mit dem Konfigurationsschritt. Von hier müssen Sie einen Namen und eine optionale Beschreibung für den Datastream angeben.

Wenn Sie diesen Datastream zur Verwendung in Experience Platform konfigurieren und das Platform Web SDK verwenden, müssen Sie auch eine [ereignisbasiertes Experience-Datenmodell (XDM)-Schema](../../xdm/classes/experienceevent.md) um die Daten darzustellen, die Sie für die Aufnahme planen.

![Grundlegende Konfiguration für einen Datastream](../images/datastreams/overview/configure.png)

Auswählen **[!UICONTROL Erweiterte Optionen]** , um zusätzliche Steuerelemente zum Konfigurieren des Datenspeichers anzuzeigen.

![Erweiterte Konfigurationsoptionen](../images/datastreams/overview/advanced-options.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Geo-Position] | Bestimmt anhand der IP-Adresse des Benutzers, ob GPS-Suchen stattfinden. Die Standardeinstellung **[!UICONTROL Keines]** deaktiviert alle GPS-Suchen, während die **[!UICONTROL Ort]** -Einstellung stellt GPS-Koordinaten auf zwei Dezimalstellen bereit. |
| [!UICONTROL Erstanbieter-ID-Cookie] | Wenn diese Einstellung aktiviert ist, weist sie das Edge-Netzwerk an, bei der Suche nach einem [Erstanbieter-Geräte-ID](../identity/first-party-device-ids.md), anstatt nach diesem Wert in der Identity Map zu suchen.<br><br>Wenn Sie diese Einstellung aktivieren, müssen Sie den Namen des Cookies angeben, in dem die ID gespeichert werden soll. |
| [!UICONTROL Synchronisierung der Drittanbieter-ID] | ID-Synchronisationen können in Container gruppiert werden, damit verschiedene ID-Synchronisierungen zu unterschiedlichen Zeiten ausgeführt werden können. Wenn diese Einstellung aktiviert ist, können Sie festlegen, welcher Container mit ID-Synchronisierungen für diesen Datastream ausgeführt wird. |
| [!UICONTROL Zugriffstyp] | Definiert den Authentifizierungstyp, den die [!DNL Edge Network] akzeptiert für den Datastream. <ul><li>**[!UICONTROL Gemischte Authentifizierung]**: Wenn diese Option aktiviert ist, akzeptiert das Edge Network sowohl authentifizierte als auch nicht authentifizierte Anforderungen. Wählen Sie diese Option, wenn Sie das Web SDK verwenden möchten, oder [Mobile SDK](https://aep-sdks.gitbook.io/docs/)zusammen mit [Server-API](../../server-api/overview.md). </li><li>**[!UICONTROL Nur authentifiziert]**: Wenn diese Option aktiviert ist, akzeptiert das Edge-Netzwerk nur authentifizierte Anforderungen. Wählen Sie diese Option aus, wenn Sie nur die Server-API verwenden möchten und verhindern möchten, dass nicht authentifizierte Anforderungen von der [!DNL Edge Network]. </li></ul> |

Wenn Sie von hier aus Ihren Datastream für die Experience Platform konfigurieren, folgen Sie dem Tutorial zu [Datenvorbereitung für die Datenerfassung](./data-prep.md) , um Ihre Daten einem Platform-Ereignisschema zuzuordnen, bevor Sie zu diesem Handbuch zurückkehren. Andernfalls wählen Sie **[!UICONTROL Speichern]** und fahren Sie mit dem nächsten Abschnitt fort.

## Anzeigen von Datenspeicherdetails {#view-details}

Nachdem Sie einen neuen Datastream konfiguriert oder einen vorhandenen ausgewählt haben, um ihn anzuzeigen, wird die Detailseite für diesen Datastream angezeigt. Hier finden Sie weitere Informationen zum Datastream, einschließlich seiner Kennung.

![Detailseite für einen erstellten Datastream](../images/datastreams/overview/view-details.png)

Im Bildschirm mit den Datenspeicherdetails können Sie [Dienste hinzufügen](#add-services) , um Funktionen aus den Adobe Experience Cloud-Produkten zu aktivieren, auf die Sie Zugriff haben. Sie können auch die [Basiskonfiguration](#create), die [Zuordnungsregeln](./data-prep.md), [Kopieren Sie den Datastream](#copy)oder löschen Sie sie vollständig.

## Hinzufügen von Diensten zu einem Datastream {#add-services}

Wählen Sie auf der Detailseite eines Datastreams die Option **[!UICONTROL Dienst hinzufügen]** , um mit dem Hinzufügen der verfügbaren Dienste für diesen Datastream zu beginnen.

![Wählen Sie Dienst hinzufügen aus, um fortzufahren](../images/datastreams/overview/add-service.png)

Wählen Sie im nächsten Bildschirm im Dropdown-Menü einen Dienst aus, der für diesen Datastream konfiguriert werden soll. In dieser Liste werden nur die Dienste angezeigt, auf die Sie Zugriff haben.

![Wählen Sie einen Dienst aus der Liste aus](../images/datastreams/overview/service-selection.png)

Wählen Sie den gewünschten Dienst aus, geben Sie die angezeigten Konfigurationsoptionen ein und wählen Sie dann **[!UICONTROL Speichern]** , um den Dienst zum Datastream hinzuzufügen. Alle hinzugefügten Dienste werden in der Detailansicht für den Datastream angezeigt.

![Zu einem Datastream hinzugefügte Dienste](../images/datastreams/overview/services-added.png)

In den folgenden Unterabschnitten werden die Konfigurationsoptionen für die einzelnen Dienste beschrieben.

>[!NOTE]
>
>Jede Dienstkonfiguration enthält eine **[!UICONTROL Aktiviert]** ein-/ausschalten, der automatisch aktiviert wird, wenn der Dienst ausgewählt ist. Um den ausgewählten Dienst für diesen Datastream zu deaktivieren, wählen Sie die **[!UICONTROL Aktiviert]** wieder umschalten.

### Adobe Analytics-Einstellungen {#analytics}

Dieser Dienst steuert, ob und wie Daten an Adobe Analytics gesendet werden. Weitere Informationen finden Sie im Handbuch zu [Senden von Daten an Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics-Einstellungsblock](../images/datastreams/overview/analytics-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Report Suite-ID] | **(Erforderlich)** Die ID der Analytics Report Suite, an die Sie Daten senden möchten. Diese ID finden Sie in der Adobe Analytics-Benutzeroberfläche unter [!UICONTROL Admin] > [!UICONTROL ReportSuites]. Wenn mehrere Report Suites angegeben sind, werden die Daten in die einzelnen Report Suites kopiert. |

### Adobe Audience Manager-Einstellungen {#audience-manager}

Dieser Dienst steuert, ob und wie Daten an Adobe Audience Manager gesendet werden. Zum Senden von Daten an Audience Manager ist nur diese Option erforderlich. Die anderen Einstellungen sind optional, werden jedoch empfohlen.

![Adobe Audience Manager-Einstellungsblock](../images/datastreams/overview/audience-manager-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Cookie-Ziele aktiviert] | Ermöglicht dem SDK das Freigeben von Segmentinformationen über [Cookie-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) von [!DNL Audience Manager]. |
| [!UICONTROL URL-Ziele aktiviert] | Ermöglicht dem SDK das Freigeben von Segmentinformationen über [URL-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) von [!DNL Audience Manager]. |

### Adobe Experience Platform-Einstellungen {#aep}

>[!IMPORTANT]
>
>Beachten Sie beim Aktivieren eines Datastreams für Platform die aktuell verwendete Platform-Sandbox, wie im oberen Band der Datenerfassungs-Benutzeroberfläche angezeigt.
>
>![Ausgewählte Sandbox](../images/datastreams/overview/platform-sandbox.png)
>
>Sandboxes sind virtuelle Partitionen in Adobe Experience Platform, mit denen Sie Ihre Daten und Implementierungen von anderen in Ihrem Unternehmen isolieren können. Nachdem ein Datastream erstellt wurde, kann seine Sandbox nicht mehr geändert werden. Weitere Informationen zur Rolle von Sandboxes in Experience Platform finden Sie unter [Sandbox-Dokumentation](../../sandboxes/home.md).

Dieser Dienst steuert, ob und wie Daten an Adobe Experience Platform gesendet werden.

![Adobe Experience Platform-Einstellungsblock](../images/datastreams/overview/platform-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Ereignis-Datensatz] | **(Erforderlich)** Wählen Sie den Platform-Datensatz aus, an den Kundenereignisdaten gestreamt werden. Dieses Schema muss [XDM ExperienceEvent-Klasse](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Profildatensatz] | Wählen Sie den Platform-Datensatz aus, an den Kundenattributdaten gesendet werden. Dieses Schema muss [Klasse &quot;XDM Individual Profile&quot;](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Aktivieren Sie dieses Kontrollkästchen, um die Offer decisioning für eine Platform Web SDK-Implementierung zu aktivieren. Siehe Handbuch unter [Verwenden von Offer decisioning mit dem Platform Web SDK](../personalization/offer-decisioning/offer-decisioning-overview.md) für weitere Implementierungsdetails. Weitere Informationen zu Offer decisioning-Funktionen finden Sie im Abschnitt [Adobe Journey Optimizer-Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=de). |
| [!UICONTROL Edge-Segmentierung] | Aktivieren Sie dieses Kontrollkästchen, um [Kantensegmentierung](../../segmentation/ui/edge-segmentation.md) für diesen Datastream. Wenn das SDK Daten über einen Datastream sendet, der für die Kantensegmentierung aktiviert ist, werden alle aktualisierten Segmentmitgliedschaften für das betreffende Profil in der Antwort zurückgesendet.<br><br>Diese Option kann in Kombination mit [!UICONTROL Personalisierungsziele] für [Anwendungsfälle für die Personalisierung der nächsten Seite](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Personalisierungsziele] | Bei Verwendung in Kombination mit dem [!UICONTROL Edge-Segmentierung] aktivieren, ermöglicht es diese Option dem Datastream, eine Verbindung zu Personalisierungsmaschinen wie Adobe Target herzustellen. Spezifische Schritte finden Sie in der Dokumentation zu Zielen unter [Konfigurieren von Personalisierungszielen](../../destinations/ui/configure-personalization-destinations.md). |

### Adobe Target-Einstellungen {#target}

Dieser Dienst steuert, ob und wie Daten an Adobe Target gesendet werden.

![Adobe Target-Einstellungsblock](../images/datastreams/overview/target-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Eigenschafts-Token] | [!DNL Target] ermöglicht es Kunden, Berechtigungen durch die Verwendung von Eigenschaften zu steuern. Weitere Informationen zu Eigenschaften finden Sie im Handbuch unter [Konfigurieren von Unternehmensberechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=de) im [!DNL Target] Dokumentation.<br><br>Das Eigenschafts-Token befindet sich in der Adobe Target-Benutzeroberfläche unter [!UICONTROL Einrichtung] > [!UICONTROL Eigenschaften]. |
| [!UICONTROL Target-Umgebungs-ID] | [Umgebungen in Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) helfen Ihnen bei der Verwaltung Ihrer Implementierung in allen Phasen der Entwicklung. Diese Einstellung gibt an, welche Umgebung Sie für diesen Datastream verwenden werden.<br><br>Best Practice ist, dies für jeden Ihrer `dev`, `stage`und `prod` Datastream-Umgebungen, um die Dinge einfach zu halten. Wenn Sie jedoch bereits Adobe Target-Umgebungen definiert haben, können Sie diese verwenden. |
| [!UICONTROL Namespace der Target-Drittanbieter-ID] | Der Identitäts-Namespace für `mbox3rdPartyId` Sie möchten für diesen Datastream verwenden. Siehe Handbuch unter [Umsetzung `mbox3rdPartyId` mit dem Web SDK](../personalization/adobe-target/using-mbox-3rdpartyid.md) für weitere Informationen. |

### [!UICONTROL Ereignisweiterleitung] settings

Dieser Dienst steuert, ob und wie Daten an gesendet werden [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md).

![Abschnitt &quot;Ereignisweiterleitung&quot;der Konfigurationsoberfläche](../images/datastreams/overview/event-forwarding-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Launch-Eigenschaft] | **(Erforderlich)** Die Ereignisweiterleitungs-Eigenschaft, an die Sie Daten senden möchten. |
| [!UICONTROL Launch-Umgebung] | **(Erforderlich)** Die Umgebung innerhalb der ausgewählten Eigenschaft, an die Sie Daten senden möchten. |

>[!NOTE]
>
>Sie können **[!UICONTROL IDs manuell eingeben]** um die Eigenschaften- und Umgebungsnamen einzugeben, anstatt die Dropdown-Menüs zu verwenden.

## Datensatz kopieren {#copy}

Sie können eine Kopie eines vorhandenen Datenspeichers erstellen und seine Details nach Bedarf ändern.

>[!NOTE]
>
>Datenspeicher können nur innerhalb desselben kopiert werden [Sandbox](../../sandboxes/home.md). Mit anderen Worten: Sie können einen Datenspeicher nicht von einer Sandbox in eine andere kopieren.

Auf der Hauptseite im [!UICONTROL Datenspeicher] Arbeitsbereich, wählen Sie die Auslassungszeichen (**....**) für den betreffenden Datastream und wählen Sie dann **[!UICONTROL Kopieren]**.

![Bild, das die [!UICONTROL Kopieren] Option, die in der Listenansicht des Datenspeichers ausgewählt wird](../images/datastreams/overview/copy-datastream-list.png)

Alternativ können Sie **[!UICONTROL Datenspeicher kopieren]** aus der Detailansicht eines bestimmten Datastreams.

![Bild, das die [!UICONTROL Kopieren] Option, die in der Detailansicht des Datenspeichers ausgewählt wird](../images/datastreams/overview/copy-datastream-details.png)

Es wird ein Bestätigungsdialogfeld angezeigt, in dem Sie aufgefordert werden, einen eindeutigen Namen für den neuen zu erstellenden Datastream sowie Details zu den Konfigurationsoptionen, die kopiert werden, anzugeben. Wenn Sie bereit sind, wählen Sie **[!UICONTROL Kopieren]**.

![Bild des Bestätigungsdialogfelds zum Kopieren eines Datenspeichers](../images/datastreams/overview/copy-datastream-confirm.png)

Die Hauptseite der [!UICONTROL Datenspeicher] Workspace wird mit dem neuen Datastream erneut angezeigt.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Datenspeicher in der Datenerfassungs-Benutzeroberfläche verwalten. Weitere Informationen zum Installieren und Konfigurieren des Web SDK nach dem Einrichten eines Datastreams finden Sie im Abschnitt [Handbuch zur Datenerfassung E2E](../../collection/e2e.md#install).
