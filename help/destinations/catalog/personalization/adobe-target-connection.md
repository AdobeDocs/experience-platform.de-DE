---
keywords: Zielpersonalisierung;Ziel;Ziel von Experience Platform;Adobe Target-Ziel;
title: Adobe Target-Verbindung
description: Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: e5c34ffb9b27ddad0c6523a7279fdf712c84f3ff
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 29%

---

# Adobe Target-Verbindung {#adobe-target-connection}

## Ziel-Änderungsprotokoll {#changelog}

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| April 2024 | Funktions- und Dokumentationsaktualisierung | Beim Herstellen einer Verbindung zum Target-Ziel und Verwenden einer Datastraam-ID müssen Sie jetzt *nicht benötigen* , um den Datastream für die Kantensegmentierung zu aktivieren. Das bedeutet, dass das Target-Ziel mit Batch- und Streaming-Zielgruppen funktioniert, obwohl die Anwendungsfälle, die Sie ausführen können, unterschiedlich sind. Die Tabelle im [Verbindungsparameter](#parameters) für weitere Informationen. |
| Januar 2024 | Funktions- und Dokumentationsaktualisierung | Sie können jetzt Zielgruppen und Profilattribute für die Adobe Target-Verbindung für die standardmäßige Produktions-Sandbox und andere nicht standardmäßige Sandboxes freigeben. |
| Juni 2023 | Funktions- und Dokumentationsaktualisierung | Ab Juni 2023 können Sie beim Konfigurieren einer neuen Adobe Target-Zielverbindung den Adobe Target-Arbeitsbereich auswählen, für den Sie Zielgruppen freigeben möchten. Weitere Informationen finden Sie im Abschnitt [Verbindungsparameter](#parameters). Weitere Informationen über Arbeitsbereiche finden Sie im Tutorial zum [Konfigurieren von Arbeitsbereichen](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html) in Adobe Target. |
| Mai 2023 | Funktions- und Dokumentationsaktualisierung | Ab Mai 2023 wird die **[!UICONTROL Adobe Target]** Verbindungsunterstützung [attributbasierte Personalisierung](../../ui/activate-edge-personalization-destinations.md#map-attributes) und ist allgemein für alle Kunden verfügbar. |

{style="table-layout:auto"}

## Übersicht {#overview}

Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.

Adobe Target ist eine Personalisierungsverbindung im Adobe Experience Platform-Zielkatalog.

## Videoüberblick {#video-overview}

Eine kurze Übersicht über die Konfiguration der Adobe Target-Verbindung unter Experience Platform finden Sie im folgenden Video.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Voraussetzungen {#prerequisites}

### Datastream-ID {#datastream-id}

Beim Konfigurieren der Adobe Target-Verbindung zu [Verwenden einer Datensatz-ID](#parameters), müssen Sie über die [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) implementiert.

Zum Konfigurieren der Adobe Target-Verbindung ohne Verwendung einer Datastraam-ID müssen Sie das Web SDK nicht implementieren.

>[!IMPORTANT]
>
>Bevor Sie eine [!DNL Adobe Target]-Verbindung erstellen, lesen Sie das Handbuch zur [Konfiguration von Personalisierungszielen für die Personalisierung derselben Seite und der nächsten Seite](../../ui/activate-edge-personalization-destinations.md). In diesem Handbuch werden die erforderlichen Konfigurationsschritte für die Personalisierungsfälle der gleichen und der nächsten Experience Platform-Seite beschrieben. Um die Personalisierung von derselben Seite und nächsten Seiten zu erreichen, müssen Sie beim Konfigurieren der Adobe Target-Verbindung eine Datastraam-ID verwenden.

### Voraussetzungen in Adobe Target {#prerequisites-in-adobe-target}

Stellen Sie in Adobe Target sicher, dass Ihr Benutzer über Folgendes verfügt:

* Zugriff auf [Standardarbeitsbereich](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace);
* Die **Genehmiger** [Rolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

Weitere Informationen zum Gewähren von Berechtigungen für [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) und [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

>[!IMPORTANT]
>
>Beim Aktivieren *Edge-Zielgruppen für Anwendungsfälle der Personalisierung von derselben Seite und nächsten Seiten*, die Zielgruppen *must* verwenden Sie eine [aktive Zusammenführungsrichtlinie](../../../segmentation/ui/segment-builder.md#merge-policies). Die [!DNL active-on-edge] Zusammenführungsrichtlinie stellt sicher, dass Zielgruppen kontinuierlich ausgewertet werden [am Rand](../../../segmentation/ui/edge-segmentation.md) und sind für Anwendungsfälle zur Personalisierung von Echtzeit- und nächsten Seiten verfügbar.  Informationen [alle verfügbaren Anwendungsfälle](#parameter), basierend auf dem Implementierungstyp.
>Wenn Sie Edge-Zielgruppen, die eine andere Zusammenführungsrichtlinie verwenden, Adobe Target-Zielen zuordnen, werden diese Zielgruppen nicht für Anwendungsfälle in Echtzeit und auf der nächsten Seite ausgewertet.
>Befolgen Sie die Anweisungen zum [Erstellen einer Zusammenführungsrichtlinie](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy) und stellen Sie sicher, dass Sie die **[!UICONTROL Active-On-Edge-Zusammenführungsrichtlinie]** aktivieren.


| Audience Origin | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Sie fordern alle Zielgruppen an, die im Adobe Target-Ziel für ein einzelnes Profil zugeordnet sind. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informationen zu Datenstrom-IDs"
>abstract="Diese Option bestimmt, in welchen Datenerfassungsdatastream die Zielgruppen eingeschlossen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die die Target-Konfiguration aktiviert ist. Um die Kantensegmentierung zu verwenden, müssen Sie eine Datastream-ID auswählen. Wenn Sie Kein auswählen, werden alle Anwendungsfälle deaktiviert, die Kantensegmentierung verwenden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Erfahren Sie mehr über die Auswahl von Datastreams"

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

Adobe Experience Platform stellt automatisch eine Verbindung zur Adobe Target-Instanz Ihrer Firma her. Es ist keine Authentifizierung erforderlich.

### Verbindungsparameter {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Informationen zu Adobe Target-Arbeitsbereichen"
>abstract="Wählen Sie den Adobe Target-Arbeitsbereich aus, für den Zielgruppen freigegeben werden sollen. Sie können für jede Adobe Target-Verbindung einen einzigen Arbeitsbereich auswählen. Nach der Aktivierung werden die Zielgruppen zum ausgewählten Arbeitsbereich weitergeleitet, während die entsprechenden Experience Platform-Datennutzungsbezeichnungen befolgt werden."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html" text="Weitere Informationen zu Adobe Target-Arbeitsbereichen"

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **Name**: Geben Sie den gewünschten Namen für das Ziel ein.
* **Beschreibung**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **Datenspeicher-ID**: Dadurch wird bestimmt, in welchem Datenerfassungsdatenstrom die Zielgruppen einbezogen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die die Target- und Adobe Experience Platform-Dienste aktiviert sind. Siehe [Konfigurieren eines Datenspeichers](../../../datastreams/configure.md#aep) für detaillierte Informationen zum Konfigurieren eines Datastreams für Adobe Experience Platform und Adobe Target.

  >[!IMPORTANT]
  >
  >Die Datastream-ID ist für jede Adobe Target-Zielverbindung eindeutig. Wenn Sie die gleichen Zielgruppen mehreren Datastreams zuordnen müssen, müssen Sie [Erstellen einer neuen Zielverbindung](../../ui/connect-destination.md) für jede Datastream-ID und durchlaufen Sie die [Zielgruppenaktivierungsfluss](#activate).

   * **[!UICONTROL Keines]**: Wählen Sie diese Option aus, wenn Sie die Adobe Target-Personalisierung konfigurieren möchten, die Implementierung der [Experience Platform Web SDK](/help/web-sdk/home.md). Bei Verwendung dieser Option unterstützen Zielgruppen, die von Experience Platform nach Target exportiert werden, nur die Personalisierung der nächsten Sitzung und die Kantensegmentierung ist deaktiviert. In der unten stehenden Tabelle finden Sie einen Vergleich der verfügbaren Anwendungsfälle pro Implementierungstyp.

  | Adobe Target-Implementierung *without* Web SDK | Adobe Target-Implementierung *mit* Web SDK | Adobe Target-Implementierung *mit* Web SDK *und* Kantensegmentierung deaktiviert |
  |---|---|---|
  | <ul><li>Ein Datastream ist nicht erforderlich. Adobe Target kann über bereitgestellt werden [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [serverseitig](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation)oder [hybrid](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) Implementierungsmethoden.</li><li>[Edge-Segmentierung](../../../segmentation/ui/edge-segmentation.md) wird nicht unterstützt.</li><li>[Personalisierung auf derselben Seite und auf der nächsten Seite](../../ui/activate-edge-personalization-destinations.md) werden nicht unterstützt.</li><li>Sie können Zielgruppen und Profilattribute für die Adobe Target-Verbindung freigeben. *Standard-Produktions-Sandbox* und nicht standardmäßigen Sandboxes.</li><li>Verwenden Sie zum Konfigurieren der Personalisierung der nächsten Sitzung ohne Verwendung einer Datastraam-ID die [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>Ein Datastream mit Adobe Target und Experience Platform ist als Dienste konfiguriert.</li><li>Die Edge-Segmentierung funktioniert wie erwartet.</li><li>[Personalisierung auf derselben Seite und auf der nächsten Seite](../../ui/activate-edge-personalization-destinations.md#use-cases) werden unterstützt.</li><li>Die Freigabe von Zielgruppen und Profilattributen aus anderen Sandboxes wird unterstützt.</li></ul> | <ul><li>Ein Datastream mit Adobe Target und Experience Platform ist als Dienste konfiguriert.</li><li>Wann [Konfigurieren des Datenspeichers](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream), wählen Sie nicht die **Edge-Segmentierung** aktivieren.</li><li>[Personalisierung der nächsten Sitzung](../../ui/activate-edge-personalization-destinations.md#next-session) wird unterstützt.</li><li>Die Freigabe von Zielgruppen und Profilattributen aus anderen Sandboxes wird unterstützt.</li></ul> |

* **Arbeitsbereich**: Wählen Sie die Adobe Target aus. [Arbeitsbereich](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html) für die Zielgruppen freigegeben werden. Sie können für jede Adobe Target-Verbindung einen einzigen Arbeitsbereich auswählen. Bei Aktivierung werden die Zielgruppen zum ausgewählten Arbeitsbereich weitergeleitet, während die entsprechenden [Experience Platform-Datennutzungsbezeichnungen](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>Bei Verwendung eines benutzerdefinierten Target-Arbeitsbereichs für [Personalisierung von derselben Seite und nächster Seite mit Attributen](../../ui/activate-edge-personalization-destinations.md), wobei nur die [ausgewählte Zielgruppen](../../ui/activate-edge-personalization-destinations.md#select-audiences) werden an den ausgewählten Target-Arbeitsbereich gesendet. Die [Zugeordnete Attribute](../../ui/activate-edge-personalization-destinations.md#mapping) werden an den standardmäßigen Target-Arbeitsbereich gesendet.
><br>
>Dieses Verhalten wird sich in einer zukünftigen Aktualisierung ändern.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Zielgruppen für Edge-Personalisierungsziele](../../ui/activate-edge-personalization-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

## Entfernen von Zielgruppen aus einem Target-Ziel {#remove}

Es sind zusätzliche Schritte erforderlich, um eine Zielgruppe aus einer bestehenden Adobe Target-Verbindung zu entfernen, wenn diese Zielgruppe bereits in einer Adobe Target verwendet wird [activity](https://experienceleague.adobe.com/en/docs/target/using/activities/activities). Wenn Sie versuchen, eine Zielgruppe aus einer Adobe Target-Verbindung zu entfernen, wird ein Fehler ausgegeben, wenn die Zielgruppe von einer Adobe Target-Aktivität verwendet wird.

![Platform-UI-Bild, das einen Fehler anzeigt, der durch den Versuch verursacht wird, eine Zielgruppe zu entfernen, die von einer Target-Aktivität verwendet wird.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

Um eine Zielgruppe aus einem Target-Ziel zu entfernen, wenn die Zielgruppe in einer Aktivität verwendet wird, müssen Sie zunächst die Zielgruppe entweder aus der Target-Aktivität entfernen, die sie verwendet, oder die Aktivität ganz löschen. Anschließend können Sie die Zielgruppe aus Ihrer Target-Verbindung entfernen.

Wenn die Audience nicht in einer Aktivität verwendet wird, gehen Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** > **[!UICONTROL Zieldatenfluss auswählen]** > **[!UICONTROL Aktivierungsdaten]**, wählen Sie die Zielgruppen aus, die Sie entfernen möchten, und klicken Sie dann auf **[!UICONTROL Entfernen von Zielgruppen]**.

## Exportierte Daten {#exported-data}

Adobe Target *reads* Profildaten aus dem Adobe Experience Platform-Edge Network, sodass keine Daten exportiert werden.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).
