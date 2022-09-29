---
title: Übersicht über Datenströme
description: Verbinden Sie Ihre Client-seitige Experience Platform SDK-Integration mit Adobe-Produkten und Zielen von Drittanbietern.
keywords: Konfiguration;Datenströme;datastreamId;edge;datastream id;Umgebungseinstellungen;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Ereignis-Datensatz;Target;Client-Code;Eigenschafts-Token;Target-Umgebungs-ID;Cookie-Ziele;URL-Ziele;Analytics Settings Blockreport suite id;Datenvorbereitung für Datenerfassung;Data Prep;Mapper;XDM Mapper;Mapper in Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 81b20d40d3511592125cba123fa070fc27aace5a
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 92%

---

# Übersicht über Datenströme

Ein Datenstrom stellt die Server-seitige Konfiguration bei der Implementierung der Adobe Experience Platform Web- und Mobile-SDKs dar. Während mit dem [configure-Befehl](../fundamentals/configuring-the-sdk.md) im SDK Elemente kontrolliert werden, die auf dem Client verarbeitet werden müssen (z. B. die `edgeDomain`), handhaben Datenströme alle anderen Konfigurationen für das SDK. Wenn eine Anfrage an das Adobe Experience Platform Edge Network gesendet wird, wird die `edgeConfigId` verwendet, um auf den Datenstrom zu verweisen. Auf diese Weise können Sie die Server-seitige Konfiguration aktualisieren, ohne Code-Änderungen auf Ihrer Website vornehmen zu müssen.

In diesem Dokument werden die Schritte zum Konfigurieren eines Datenspeichers in der Benutzeroberfläche beschrieben.

## Zugriff auf den Arbeitsbereich [!UICONTROL Datenströme ]

Sie können Datenspeicher in der Datenerfassungs-Benutzeroberfläche oder in der Experience Platform-Benutzeroberfläche erstellen und verwalten, indem Sie **[!UICONTROL Datenspeicher]** in der linken Navigation.

![Registerkarte &quot;Datenspeicher&quot;in der Benutzeroberfläche](../assets/datastreams/overview/datastreams-tab.png)

In der Registerkarte [!UICONTROL Datenströme] wird eine Liste mit vorhandenen Datenströmen angezeigt, darunter auch der Anzeigename, die Kennung und das Datum der letzten Änderung. Wählen Sie den Namen eines Datenstroms aus, um [seine Details anzuzeigen und Services zu konfigurieren](#view-details).

Wählen Sie das Symbol „Mehr“ (**...**) aus, wenn Sie für einen bestimmten Datenstrom weitere Optionen anzeigen möchten. Auswählen Sie **[!UICONTROL Bearbeiten]** aus, um die [Basiskonfiguration](#configure) für den Datenstrom zu aktualisieren, oder wählen Sie **[!UICONTROL Löschen]** aus, um den Datenstrom zu entfernen.

![Optionen zum Bearbeiten oder Löschen eines vorhandenen Datenstroms](../assets/datastreams/overview/edit-datastream.png)

## Erstellen eines neuen Datenstroms {#create}

Um einen Datenstrom zu erstellen, wählen Sie zunächst **[!UICONTROL Neuer Datenstrom]** aus.

![Neuen Datenspeicher auswählen](../assets/datastreams/overview/new-datastream-button.png)

Der Workflow zur Erstellung eines Datenstroms wird geöffnet, beginnend mit dem Konfigurationsschritt. Geben Sie hier einen Namen und eine optionale Beschreibung für den Datenstrom an.

Wenn Sie diesen Datenstrom zur Verwendung in Experience Platform konfigurieren und das Platform Web SDK verwenden, müssen Sie auch ein [ereignisbasiertes Experience-Datenmodell-Schema (XDM)](../../xdm/classes/experienceevent.md) für die Daten auswählen, die aufgenommen werden sollen.

![Basiskonfiguration für einen Datenstrom](../assets/datastreams/overview/configure.png)

Wählen Sie **[!UICONTROL Erweiterte Optionen]** aus, um zusätzliche Steuerelemente zum Konfigurieren des Datenstroms anzuzeigen.

![Erweiterte Konfigurationsoptionen](../assets/datastreams/overview/advanced-options.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Geografie – Standort] | Hiermit legen Sie fest, ob anhand der IP-Adresse des Benutzers GPS-Suchen stattfinden. Mit der Standardeinstellung **[!UICONTROL Keine]** werden alle GPS-Suchen deaktiviert, während die Einstellung **[!UICONTROL Ort]** GPS-Koordinaten auf zwei Dezimalstellen genau bereitstellt. |
| [!UICONTROL First-Party-ID-Cookie] | Wenn diese Einstellung aktiviert ist, weist sie das Edge-Netzwerk an, bei der Suche nach einer [First-Party-Geräte-ID](../identity/first-party-device-ids.md) ein bestimmtes Cookie zu verwenden, anstatt nach diesem Wert in der Identity Map zu suchen.<br><br>Wenn Sie diese Einstellung aktivieren, müssen Sie den Namen des Cookies angeben, in dem die ID gespeichert ist. |
| [!UICONTROL Synchronisierung der Third-Party-ID] | ID-Synchronisationen können in Container zusammengefasst werden, damit verschiedene ID-Synchronisationen zu unterschiedlichen Zeiten ausgeführt werden können. Wenn diese Einstellung aktiviert ist, können Sie festlegen, welcher Container mit ID-Synchronisationen für diesen Datenstrom ausgeführt werden soll. |
| [!UICONTROL Zugriffstyp] | Definiert den Authentifizierungstyp, den das [!DNL Edge Network] für den Datenstrom akzeptiert. <ul><li>**[!UICONTROL Gemischte Authentifizierung]**: Wenn diese Option aktiviert ist, akzeptiert das Edge Network sowohl authentifizierte als auch nicht authentifizierte Anfragen. Wählen Sie diese Option, wenn Sie das Web SDK oder das [Mobile SDK](https://aep-sdks.gitbook.io/docs/) zusammen mit der [Server-API](../../server-api/overview.md) verwenden möchten. </li><li>**[!UICONTROL Nur authentifiziert]**: Wenn diese Option aktiviert ist, akzeptiert das Edge Network nur authentifizierte Anfragen. Wählen Sie diese Option aus, wenn Sie nur die Server-API verwenden und verhindern möchten, dass nicht authentifizierte Anforderungen vom [!DNL Edge Network] verarbeitet werden. </li></ul> |

Wenn hier Ihren Datenstrom für Experience Platform konfigurieren, folgen Sie dem Tutorial zu [Datenvorbereitung für die Datenerfassung](./data-prep.md), um Ihre Daten einem Platform-Ereignisschema zuzuordnen, bevor Sie mit dieser Anleitung fortfahren. Wählen Sie andernfalls **[!UICONTROL Speichern]** und fahren Sie mit dem nächsten Abschnitt fort.

## Anzeigen von Datenstromdetails {#view-details}

Nachdem Sie einen neuen Datenstrom konfiguriert oder einen vorhandenen ausgewählt haben, um ihn anzuzeigen, wird die Detailseite für diesen Datenstrom angezeigt. Hier finden Sie weitere Informationen zum Datenstrom, einschließlich seiner Kennung.

![Detailseite für einen erstellten Datenstrom](../assets/datastreams/overview/view-details.png)

Im Bildschirm mit den Datenspeicherdetails können Sie [Services hinzufügen](#add-services), um Funktionen der Adobe Experience Cloud-Produkte zu aktivieren, auf die Sie Zugriff haben. Sie können auch die [Basiskonfiguration](#create) des Datenstroms bearbeiten, seine [Zuordnungsregeln](./data-prep.md) aktualisieren, [den Datenstrom kopieren](#copy) oder vollständig löschen.

## Hinzufügen von Services zu einem Datenstrom {#add-services}

Wählen Sie auf der Detailseite eines Datenstroms die Option **[!UICONTROL Service hinzufügen]** aus, um verfügbare Services für diesen Datenstrom hinzuzufügen.

![„Service hinzufügen“ auswählen, um fortzufahren](../assets/datastreams/overview/add-service.png)

Wählen Sie im nächsten Bildschirm im Dropdown-Menü einen Service aus, der für diesen Datenstrom konfiguriert werden soll. In dieser Liste werden nur die Services angezeigt, auf die Sie Zugriff haben.

![Wählen Sie einen Service aus der Liste aus](../assets/datastreams/overview/service-selection.png)

Wählen Sie den gewünschten Service aus, geben Sie die angezeigten Konfigurationsoptionen ein und wählen Sie dann **[!UICONTROL Speichern]** aus, um den Service zum Datenstrom hinzuzufügen. Alle hinzugefügten Services werden in der Detailansicht für den Datenstrom angezeigt.

![Zu einem Datenstrom hinzugefügte Services](../assets/datastreams/overview/services-added.png)

In den folgenden Unterabschnitten werden die Konfigurationsoptionen für die einzelnen Services beschrieben.

>[!NOTE]
>
>Jede Service-Konfiguration enthält den Umschalter **[!UICONTROL Aktiviert]**, der automatisch aktiviert wird, wenn der Service ausgewählt wird. Um den ausgewählten Service für diesen Datenstrom zu deaktivieren, wählen Sie nochmals den Umschalter **[!UICONTROL Aktiviert]** aus.

### Adobe Analytics-Einstellungen {#analytics}

Mit diesem Service wird festgelegt, ob und wie Daten an Adobe Analytics gesendet werden. Weitere Informationen finden Sie in der Anleitung zum [Senden von Daten an Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics-Einstellungen](../assets/datastreams/overview/analytics-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Report Suite-ID] | **(Erforderlich)** Die ID der Analytics Report Suite, an die Sie Daten senden möchten. Diese ID finden Sie in der Adobe Analytics-Benutzeroberfläche unter [!UICONTROL Administration] > [!UICONTROL ReportSuites]. Wenn mehrere Report Suites angegeben sind, werden die Daten in jede einzelne Report Suite kopiert. |

### Adobe Audience Manager-Einstellungen {#audience-manager}

Mit diesem Service wird festgelegt, ob und wie Daten an Adobe Audience Manager gesendet werden. Zum Senden von Daten an Audience Manager müssen Sie nur diesen Abschnitt aktivieren. Die anderen Einstellungen sind optional, werden jedoch empfohlen.

![Adobe Audience Manager-Einstellungen](../assets/datastreams/overview/audience-manager-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Cookie-Ziele aktiviert] | Ermöglicht dem SDK das Freigeben von Segmentinformationen über [Cookie-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html?lang=de) in [!DNL Audience Manager]. |
| [!UICONTROL URL-Ziele aktiviert] | Ermöglicht dem SDK das Freigeben von Segmentinformationen über [URL-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html?lang=de) in [!DNL Audience Manager]. |

### Adobe Experience Platform-Einstellungen {#aep}

>[!IMPORTANT]
>
>Beachten Sie beim Aktivieren eines Datastreams für Platform die aktuell verwendete Platform-Sandbox, wie im oberen Band der Benutzeroberfläche angezeigt.
>
>![Ausgewählte Sandbox](../assets/datastreams/overview/platform-sandbox.png)
>
>Sandboxes sind virtuelle Partitionen in Adobe Experience Platform, mit denen Sie Ihre Daten und Implementierungen von anderen in Ihrem Unternehmen isolieren können. Nachdem ein Datenstrom erstellt wurde, kann seine Sandbox nicht mehr geändert werden. Weitere Informationen zur Rolle von Sandboxes in Experience Platform finden Sie i der [Sandbox-Dokumentation](../../sandboxes/home.md).

Mit diesem Service wird festgelegt, ob und wie Daten an Adobe Experience Platform gesendet werden.

![Adobe Experience Platform-Einstellungen](../assets/datastreams/overview/platform-config.png)

| Einstellung | Beschreibung |
|---| --- |
| [!UICONTROL Ereignis-Datensatz] | **(Erforderlich)** Wählen Sie den Platform-Datensatz aus, an den Kundenereignisdaten gestreamt werden. Dieses Schema muss die [XDM ExperienceEvent-Klasse](../../xdm/classes/experienceevent.md) verwenden. |
| [!UICONTROL Profildatensatz] | Wählen Sie den Platform-Datensatz aus, an den Kundenattributdaten gesendet werden. Dieses Schema muss die [Klasse „XDM Individual Profile“](../../xdm/classes/individual-profile.md) verwenden. |
| [!UICONTROL Offer Decisioning] | Aktivieren Sie dieses Kontrollkästchen, um Offer Decisioning für eine Platform Web SDK-Implementierung zu aktivieren. Weitere Informationen dazu finden Sie in der Anleitung zum [Verwenden von Offer Decisioning mit dem Platform Web SDK](../personalization/offer-decisioning/offer-decisioning-overview.md). <br><br> Weitere Informationen zu Offer Decisioning-Funktionen finden Sie in der [Adobe Journey Optimizer-Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=de). |
| [!UICONTROL Edge-Segmentierung] | Aktivieren Sie dieses Kontrollkästchen, um [Edge-Segmentierung](../../segmentation/ui/edge-segmentation.md) für diesen Datenstrom zu aktivieren. Wenn das SDK Daten über einen Datenstrom sendet, für den die Edge-Segmentierung aktiviert ist, werden alle aktualisierten Segmentzugehörigkeiten für das betreffende Profil in der Antwort zurückgesendet.<br><br>Diese Option kann in Kombination mit [!UICONTROL Personalisierungsziele] für [Anwendungsfälle für die Personalisierung der nächsten Seite](../../destinations/ui/configure-personalization-destinations.md)oder in Kombination mit [!UICONTROL Adobe Journey Optimizer]. |
| [!UICONTROL Personalisierungsziele] | Wenn diese Option nach dem Aktivieren des Kontrollkästchens [!UICONTROL Edge-Segmentierung] aktiviert wird, kann der Datenstrom mit Personalisierungszielen, wie [benutzerdefinierte Personalisierung](../../destinations/catalog/personalization/custom-personalization.md), verbunden werden. <br><br>Die genauen Schritte zum [Konfigurieren von Personalisierungszielen](../../destinations/ui/configure-personalization-destinations.md) finden Sie in der Dokumentation zu Zielen. |
| [!UICONTROL Adobe Journey Optimizer] | Aktivieren Sie dieses Kontrollkästchen, um [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de) für diesen Datastream. <br><br> Durch Aktivierung dieser Option kann der Datastream personalisierte Inhalte aus Web- und App-basierten eingehenden Kampagnen in [!DNL Adobe Journey Optimizer]. Diese Option erfordert [!UICONTROL Edge-Segmentierung] aktiv sein. Wenn [!UICONTROL Edge-Segmentierung] deaktiviert ist, ist diese Option grau ausgeblendet. |

### Adobe Target-Einstellungen {#target}

Mit diesem Service wird festgelegt, ob und wie Daten an Adobe Target gesendet werden.

![Adobe Target-Einstellungen](../assets/datastreams/overview/target-config.png)

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Eigenschafts-Token] | [!DNL Target] ermöglicht Kunden, Berechtigungen durch die Verwendung von Eigenschaften zu steuern. Weitere Informationen zu Eigenschaften finden Sie in der Anleitung zum [Konfigurieren von Unternehmensberechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=de) in der [!DNL Target]-Dokumentation.<br><br>Das Eigenschafts-Token befindet sich in der Adobe Target-Benutzeroberfläche unter [!UICONTROL Einrichtung] > [!UICONTROL Eigenschaften]. |
| [!UICONTROL Target-Umgebungs-ID] | [Umgebungen in Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=de) helfen Ihnen in allen Entwicklungsphasen bei der Implementierung. Diese Einstellung gibt an, welche Umgebung Sie für diesen Datenstrom verwenden werden.<br><br>Empfohlen wird, der Einfachheit halber eine unterschiedliche Einstellung für jede Ihrer `dev`-, `stage`- und `prod`Datenstrom-Umgebungen auszuwählen. Wenn Sie jedoch bereits Adobe Target-Umgebungen definiert haben, können Sie diese verwenden. |
| [!UICONTROL Namespace der Target-Third-Party-ID] | Der Identity-Namespace für die `mbox3rdPartyId`, den Sie für diesen Datenstrom verwenden möchten. Weitere Informationen dazu erhalten Sie im Handbuch zur [Implementierung der `mbox3rdPartyId` mit dem Web SDK](../personalization/adobe-target/using-mbox-3rdpartyid.md). |

### Einstellungen zur [!UICONTROL Ereignisweiterleitung]

Mit diesem Service wird festgelegt, ob und wie Daten an die [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) gesendet werden.

![Abschnitt „Ereignisweiterleitung“ der Konfigurations-Benutzeroberfläche](../assets/datastreams/overview/event-forwarding-config.png)

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
>Datenströme können nur innerhalb derselben [Sandbox](../../sandboxes/home.md) kopiert werden. Mit anderen Worten: Sie können den Datenstrom von einer Sandbox nicht in eine andere kopieren.

Wählen Sie auf der Hauptseite im Arbeitsbereich [!UICONTROL Datenströme] die Auslassungszeichen für den entsprechenden Datenstrom aus (**...**) und danach **[!UICONTROL Kopieren]**.

![Bild, das die Option [!UICONTROL Kopieren] zeigt, die in der Datenstrom-Listenansicht ausgewählt wird](../assets/datastreams/overview/copy-datastream-list.png)

Alternativ können Sie in der Detailansicht eines Datenstroms **[!UICONTROL Datenstrom kopieren]** auswählen.

![Bild, das die Option [!UICONTROL Kopieren] zeigt, die in der Datenstrom-Detailansicht ausgewählt wird](../assets/datastreams/overview/copy-datastream-details.png)

Ein Bestätigungsdialogfeld erscheint, in dem Sie aufgefordert werden, einen eindeutigen Namen für den neuen, zu erstellenden Datenstrom sowie Details zu den Konfigurationsoptionen, die kopiert werden, anzugeben. Wenn Sie bereit sind, wählen Sie **[!UICONTROL Kopieren]** aus.

![Bild des Bestätigungsdialogfelds zum Kopieren eines Datenstroms](../assets/datastreams/overview/copy-datastream-confirm.png)

Die Hauptseite des Arbeitsbereichs [!UICONTROL Datenstrom] wird erneut angezeigt, diesmal mit dem neuen Datenstrom.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Datenspeicher in der Benutzeroberfläche verwalten. Weitere Informationen zum Installieren und Konfigurieren des Web SDK nach dem Einrichten eines Datenstroms finden Sie im [Handbuch E2E zur Datenerfassung](../../collection/e2e.md#install).
