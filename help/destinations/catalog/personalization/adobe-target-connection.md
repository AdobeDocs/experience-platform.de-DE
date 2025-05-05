---
keywords: Zielpersonalisierung;Ziel;Ziel von Experience Platform;Adobe Target-Ziel;
title: Adobe Target-Verbindung
description: Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 31%

---

# Adobe Target-Verbindung {#adobe-target-connection}

## Ziel-Änderungsprotokoll {#changelog}

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| April 2024 | Funktions- und Dokumentationsaktualisierung | Beim Herstellen einer Verbindung zum Target-Ziel und Verwenden einer Datenstrom-ID *Sie jetzt (*) unbedingt den Datenstrom für die Edge-Segmentierung aktivieren. Das bedeutet, dass das Target-Ziel mit Batch- und Streaming-Zielgruppen funktioniert, wobei die möglichen Anwendungsfälle unterschiedlich sind. Weitere Informationen finden Sie in der Tabelle [ Abschnitt ](#parameters)Verbindungsparameter“. |
| Januar 2024 | Funktions- und Dokumentationsaktualisierung | Sie können jetzt Zielgruppen und Profilattribute für die Adobe Target-Verbindung für die standardmäßige Produktions-Sandbox und andere nicht standardmäßige Sandboxes freigeben. |
| Juni 2023 | Funktions- und Dokumentationsaktualisierung | Ab Juni 2023 können Sie beim Konfigurieren einer neuen Adobe Target-Zielverbindung den Adobe Target-Arbeitsbereich auswählen, für den Sie Zielgruppen freigeben möchten. Weitere Informationen finden Sie im Abschnitt [Verbindungsparameter](#parameters). Weitere Informationen über Arbeitsbereiche finden Sie im Tutorial zum [Konfigurieren von Arbeitsbereichen](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=de) in Adobe Target. |
| Mai 2023 | Funktions- und Dokumentationsaktualisierung | Seit Mai 2023 unterstützt die **[!UICONTROL Adobe Target]**-Verbindung [attributbasierte Personalisierung](../../ui/activate-edge-personalization-destinations.md#map-attributes) und steht allen Kundinnen und Kunden allgemein zur Verfügung. |

{style="table-layout:auto"}

## Übersicht {#overview}

Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.

Adobe Target ist eine Personalisierungsverbindung im Adobe Experience Platform-Zielkatalog.

## Videoüberblick {#video-overview}

Einen kurzen Überblick über die Konfiguration der Adobe Target-Verbindung in Experience Platform erhalten Sie im folgenden Video.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Unterstützte Anwendungsfälle basierend auf dem Implementierungstyp {#supported-use-cases}

In der folgenden Tabelle werden die unterstützten Anwendungsfälle für das Adobe Target-Ziel basierend auf Ihrem Implementierungstyp angezeigt, mit oder ohne [Web SDK](/help/web-sdk/home.md) und mit oder ohne [Edge-Segmentierung](/help/segmentation/home.md#edge).

| Adobe Target-Implementierung *ohne* Web SDK | Adobe Target-Implementierung *mit* Web SDK | Adobe Target-Implementierung *mit* Web SDK *und* Edge-Segmentierung deaktiviert |
|---|---|---|
| <ul><li>Ein Datenstrom ist nicht erforderlich. Adobe Target kann über Implementierungsmethoden [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=de), [serverseitig](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=de#server-side-implementation) oder [Hybrid](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=de#hybrid-implementation) bereitgestellt werden.</li><li>[Edge-](../../../segmentation/methods/edge-segmentation.md) wird nicht unterstützt.</li><li>[Personalisierung der gleichen Seite und der nächsten Seite](../../ui/activate-edge-personalization-destinations.md) wird nicht unterstützt.</li><li>Sie können Zielgruppen und Profilattribute für die Adobe Target-Verbindung für die *standardmäßige Produktions-Sandbox* und nicht standardmäßige Sandboxes freigeben.</li><li>Um die Personalisierung der nächsten Sitzung ohne Datenstrom-ID zu konfigurieren, verwenden Sie [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=de).</li></ul> | <ul><li>Ein Datenstrom mit Adobe Target und Experience Platform, die als Services konfiguriert sind, ist erforderlich.</li><li>Die Segmentierung in Edge funktioniert erwartungsgemäß.</li><li>[Personalisierung der gleichen Seite und der nächsten Seite](../../ui/activate-edge-personalization-destinations.md#use-cases) wird unterstützt.</li><li>Die Freigabe von Zielgruppen und Profilattributen aus anderen Sandboxes wird unterstützt.</li></ul> | <ul><li>Ein Datenstrom mit Adobe Target und Experience Platform, die als Services konfiguriert sind, ist erforderlich.</li><li>Aktivieren [ beim Konfigurieren ](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream) Datenstroms nicht das Kontrollkästchen **Edge-**.</li><li>[Personalisierung der nächsten Sitzung](../../ui/activate-edge-personalization-destinations.md#next-session) wird unterstützt.</li><li>Die Freigabe von Zielgruppen und Profilattributen aus anderen Sandboxes wird unterstützt.</li></ul> |


## Voraussetzungen {#prerequisites}

### Datastream-ID {#datastream-id}

Beim Konfigurieren der Adobe Target-Verbindung für [Verwenden einer Datenstrom](#parameters)ID) muss die [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) implementiert sein.

Wenn Sie die Adobe Target-Verbindung ohne Datenstrom-ID konfigurieren, müssen Sie die Web-SDK nicht implementieren.

>[!IMPORTANT]
>
>Bevor Sie eine [!DNL Adobe Target]-Verbindung erstellen, lesen Sie das Handbuch zur [Konfiguration von Personalisierungszielen für die Personalisierung derselben Seite und der nächsten Seite](../../ui/activate-edge-personalization-destinations.md). Dieses Handbuch führt Sie durch die erforderlichen Konfigurationsschritte für die Anwendungsfälle der Personalisierung der gleichen Seite und der nächsten Seite für mehrere Experience Platform-Komponenten. Um Anwendungsfälle für die Personalisierung der gleichen Seite und der nächsten Seite zu erreichen, müssen Sie beim Konfigurieren der Adobe Target-Verbindung eine Datenstrom-ID verwenden.

### Voraussetzungen in Adobe Target {#prerequisites-in-adobe-target}

Vergewissern Sie sich in Adobe Target, dass Ihre Benutzerin bzw. Ihr Benutzer über Folgendes verfügt:

* Zugriff auf den [Standardarbeitsbereich](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=de#default-workspace);
* Die **genehmigende**&#x200B;[rolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=de#roles-and-permissions).

Weitere Informationen zum Gewähren von Berechtigungen für [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=de#section_8C425E43E5DD4111BBFC734A2B7ABC80) und für [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=de#roles-permissions).

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

>[!IMPORTANT]
>
>Beim Aktivieren *Edge-Zielgruppen für Anwendungsfälle mit Personalisierung der gleichen Seite und der nächsten Seite* müssen die Zielgruppen ** eine [Active-On-Edge-Zusammenführungsrichtlinie) ](../../../segmentation/ui/segment-builder.md#merge-policies). Die [!DNL active-on-edge] Zusammenführungsrichtlinie stellt sicher, dass Zielgruppen ständig [on the Edge](../../../segmentation/methods/edge-segmentation.md) ausgewertet werden und für Anwendungsfälle der Personalisierung in Echtzeit und auf der nächsten Seite verfügbar sind.  Lesen Sie mehr über [alle verfügbaren Anwendungsfälle](#parameter) basierend auf dem Implementierungstyp.
>Wenn Sie Edge-Zielgruppen, die eine andere Zusammenführungsrichtlinie verwenden, Adobe Target-Zielen zuordnen, werden diese Zielgruppen nicht für Anwendungsfälle in Echtzeit und auf der nächsten Seite ausgewertet.
>Befolgen Sie die Anweisungen zum [Erstellen einer Zusammenführungsrichtlinie](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy) und stellen Sie sicher, dass Sie die **[!UICONTROL Active-On-Edge-Zusammenführungsrichtlinie]** aktivieren.


| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

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
>abstract="Mit dieser Option wird festgelegt, in welchen Datenerfassungs-Datenstrom die Zielgruppen einbezogen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Um die Edge-Segmentierung zu verwenden, müssen Sie eine Datenstrom-ID auswählen. Wenn Sie „Keine“ auswählen, werden alle Anwendungsfälle deaktiviert, die die Edge-Segmentierung verwenden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=de#parameters" text="Weitere Informationen zur Auswahl von Datenströmen"

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

Adobe Experience Platform stellt automatisch eine Verbindung zur Adobe Target-Instanz Ihrer Firma her. Es ist keine Authentifizierung erforderlich.

### Verbindungsparameter {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Informationen zu Adobe Target-Arbeitsbereichen"
>abstract="Wählen Sie den Adobe Target-Arbeitsbereich aus, für den Zielgruppen freigegeben werden sollen. Für jede Adobe Target-Verbindung kann ein Arbeitsbereich ausgewählt werden. Nach der Aktivierung werden die Zielgruppen zum ausgewählten Arbeitsbereich weitergeleitet, während die entsprechenden Kennzeichnungen für die Datennutzung aus Experience Platform befolgt werden."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=de" text="Weitere Informationen zu Adobe Target-Arbeitsbereichen"

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **Name**: Geben Sie den gewünschten Namen für das Ziel ein.
* **Beschreibung**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **Datenstrom-ID**: Dadurch wird bestimmt, in welchen Datenerfassungsdatenstrom die Zielgruppen aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Target- und Adobe Experience Platform-Services aktiviert sind. Siehe [Konfigurieren eines Datenstroms](../../../datastreams/configure.md#aep) für detaillierte Informationen zum Konfigurieren eines Datenstroms für Adobe Experience Platform und Adobe Target.

  >[!IMPORTANT]
  >
  >Die Datenstrom-ID ist für jede Adobe Target-Zielverbindung eindeutig. Sie können dieselbe Datenstrom-ID nicht für mehrere Adobe Target-Zielverbindungen verwenden.
  >Wenn Sie dieselben Zielgruppen mehreren Datenströmen zuordnen müssen, müssen Sie [für jede Datenstrom-ID eine neue Zielverbindung erstellen](../../ui/connect-destination.md) und den [Zielgruppenaktivierungsfluss“ ](#activate).

   * **[!UICONTROL Keine]**: Wählen Sie diese Option aus, wenn Sie die Adobe Target-Personalisierung konfigurieren müssen, die [Experience Platform Web SDK](/help/web-sdk/home.md) jedoch nicht implementieren können. Bei Verwendung dieser Option unterstützen Zielgruppen, die von Experience Platform nach Target exportiert werden, nur die Personalisierung der nächsten Sitzung, und die Edge-Segmentierung ist deaktiviert. Referenzieren Sie die Tabelle im Abschnitt [Unterstützte Anwendungsfälle](#supported-use-cases) für einen Vergleich der verfügbaren Anwendungsfälle pro Implementierungstyp.

  | Adobe Target-Implementierung *ohne* Web SDK | Adobe Target-Implementierung *mit* Web SDK | Adobe Target-Implementierung *mit* Web SDK *und* Edge-Segmentierung deaktiviert |
  |---|---|---|
  | <ul><li>Ein Datenstrom ist nicht erforderlich. Adobe Target kann über Implementierungsmethoden [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=de), [serverseitig](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=de#server-side-implementation) oder [Hybrid](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=de#hybrid-implementation) bereitgestellt werden.</li><li>[Edge-](../../../segmentation/methods/edge-segmentation.md) wird nicht unterstützt.</li><li>[Personalisierung der gleichen Seite und der nächsten Seite](../../ui/activate-edge-personalization-destinations.md) wird nicht unterstützt.</li><li>Sie können Zielgruppen und Profilattribute für die Adobe Target-Verbindung für die *standardmäßige Produktions-Sandbox* und nicht standardmäßige Sandboxes freigeben.</li><li>Um die Personalisierung der nächsten Sitzung ohne Datenstrom-ID zu konfigurieren, verwenden Sie [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=de).</li></ul> | <ul><li>Ein Datenstrom mit Adobe Target und Experience Platform, die als Services konfiguriert sind, ist erforderlich.</li><li>Die Segmentierung in Edge funktioniert erwartungsgemäß.</li><li>[Personalisierung der gleichen Seite und der nächsten Seite](../../ui/activate-edge-personalization-destinations.md#use-cases) wird unterstützt.</li><li>Die Freigabe von Zielgruppen und Profilattributen aus anderen Sandboxes wird unterstützt.</li></ul> | <ul><li>Ein Datenstrom mit Adobe Target und Experience Platform, die als Services konfiguriert sind, ist erforderlich.</li><li>Aktivieren [ beim Konfigurieren ](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream) Datenstroms nicht das Kontrollkästchen **Edge-**.</li><li>[Personalisierung der nächsten Sitzung](../../ui/activate-edge-personalization-destinations.md#next-session) wird unterstützt.</li><li>Die Freigabe von Zielgruppen und Profilattributen aus anderen Sandboxes wird unterstützt.</li></ul> |

* **Workspace**: Wählen Sie den Adobe Target-[Arbeitsbereich](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=de), für den Zielgruppen freigegeben werden sollen. Für jede Adobe Target-Verbindung kann ein Arbeitsbereich ausgewählt werden. Nach der Aktivierung werden die Zielgruppen zum ausgewählten Arbeitsbereich weitergeleitet, während die entsprechenden [Experience Platform-Datennutzungskennzeichnungen befolgt ](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>Bei Verwendung eines benutzerdefinierten Target-Arbeitsbereichs für [Personalisierung der gleichen Seite und der nächsten Seite mit ](../../ui/activate-edge-personalization-destinations.md)) werden nur [ausgewählten Zielgruppen](../../ui/activate-edge-personalization-destinations.md#select-audiences) an den ausgewählten Target-Arbeitsbereich gesendet. Die [zugeordneten Attribute](../../ui/activate-edge-personalization-destinations.md#mapping) werden an den standardmäßigen Target-Arbeitsbereich gesendet.
><br>
>Dieses Verhalten wird sich in einer zukünftigen Aktualisierung ändern.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen [ Aktivieren von Zielgruppen für dieses Ziel finden ](../../ui/activate-edge-personalization-destinations.md) unter Aktivieren von Zielgruppen für Edge-Personalisierungsziele .

## Entfernen von Zielgruppen aus einem Target-Ziel {#remove}

Es sind zusätzliche Schritte erforderlich, um eine Zielgruppe aus einer bestehenden Adobe Target-Verbindung zu entfernen, wenn diese Zielgruppe bereits in einer Adobe Target-[ (Aktivität) verwendet ](https://experienceleague.adobe.com/de/docs/target/using/activities/activities). Der Versuch, eine Zielgruppe aus einer Adobe Target-Verbindung zu entfernen, führt zu einem Fehler, wenn die Zielgruppe von einer Adobe Target-Aktivität verwendet wird.

![Bild der Experience Platform-Benutzeroberfläche, das einen Fehler anzeigt, der durch den Versuch verursacht wurde, eine Zielgruppe zu entfernen, die von einer Target-Aktivität verwendet wird.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

Um eine Zielgruppe aus einem Target-Ziel zu entfernen, wenn die Zielgruppe in einer Aktivität verwendet wird, müssen Sie zunächst entweder die Zielgruppe aus der Target-Aktivität entfernen, die sie verwendet, oder die Aktivität vollständig löschen. Anschließend können Sie die Zielgruppe aus Ihrer Target-Verbindung entfernen.

Wenn die Zielgruppe nicht in einer Aktivität verwendet wird, gehen Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** > **[!UICONTROL Zieldatenfluss auswählen]** > **[!UICONTROL Aktivierungsdaten]**, wählen Sie die Zielgruppen aus, die Sie entfernen möchten, und klicken Sie dann auf **[!UICONTROL Zielgruppen entfernen]**.

## Exportierte Daten {#exported-data}

Adobe Target *liest* Profildaten aus Adobe Experience Platform Edge Network, sodass keine Daten exportiert werden.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).
