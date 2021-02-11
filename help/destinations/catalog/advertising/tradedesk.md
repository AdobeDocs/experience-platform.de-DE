---
keywords: Werbung; die Fachstelle;
title: Verbindung zum Trade Desk
description: 'Der Trade Desk ist eine Selbstbedienungsplattform für Anzeigenkäufer, um zielgerichtete digitale Kampagnen über Display-, Video- und mobile Inventurquellen hinweg auszuführen. '
translation-type: tm+mt
source-git-commit: ad025630cbae5c220f5bbd7f55cad70620b6f335
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 5%

---


# [!DNL The Trade Desk] connection

[!DNL The Trade Desk] Mit &quot;target&quot;können Sie Profil-Daten an  [!DNL The Trade Desk].

[!DNL The Trade Desk] ist eine Selbstbedienungsplattform für Anzeigenkäufer, um Retargeting und Audience zielgerichteter digitaler Kampagnen für Display-, Video- und Mobilgeräte-Inventurquellen durchzuführen.

Um Profil-Daten an [!DNL The Trade Desk] zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Zielspezifikationen {#destination-specs}

Beachten Sie die folgenden Details, die für das [!DNL The Trade Desk]-Ziel spezifisch sind:

* Sie können die folgenden [Identitäten](../../../identity-service/namespaces.md) an [!DNL The Trade Desk]-Ziele senden: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## Anwendungsbeispiele {#use-cases}

Als Marketingspezialist möchte ich Segmente verwenden können, die aus [!DNL Trade Desk IDs] oder Geräte-IDs erstellt wurden, um Retargeting oder Audience zielgerichteter digitaler Kampagnen zu erstellen.

## Exporttyp {#export-type}

**[!DNL Segment export]** - Sie exportieren alle Segmentmitglieder (Audiencen) in das Ziel.

## Mit Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** [!DNL The Trade Desk] aus und wählen Sie **[!UICONTROL Konfigurieren]**.

![Das Ziel des Trade Desk konfigurieren](../../assets/catalog/advertising/tradedesk/configure.png)

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt [Katalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.
>
>![Handelsdatenträger-Ziel aktivieren](../../assets/catalog/advertising/tradedesk/activate.png)

Geben Sie im Schritt [!UICONTROL Authentication] die Verbindungsdetails [!DNL The Trade Desk] ein:

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, mit der Sie dieses Ziel in Zukunft identifizieren können.
* **[!UICONTROL Konto-ID]**: Ihre  [!DNL Trade Desk] [!UICONTROL Konto-ID].
* **[!UICONTROL Serverort]**: Fragen Sie Ihren  [!DNL The Trade Desk] Kundenbetreuer, welchen regionalen Server Sie verwenden sollten. Die folgenden regionalen Server stehen zur Auswahl:

   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapur]**
   * **[!UICONTROL Tokio]**
   * **[!UICONTROL Nordamerika Osten]**
   * **[!UICONTROL Nordamerika - Westen]**
   * **[!UICONTROL Lateinamerika]**

* **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Adobe Experience Platform](../../../data-governance/policies/overview.md). Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

![Schritt zur Authentifizierung des Trade Desk](../../assets/catalog/advertising/tradedesk/authenticate.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**. Ihr Ziel wird jetzt erstellt. Sie können auf [!UICONTROL Speichern und beenden] klicken, wenn Sie Segmente später aktivieren möchten, oder Sie können [!UICONTROL Weiter] auswählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen finden Sie den Rest des Workflows im nächsten Abschnitt [Segmente aktivieren](#activate-segments).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md#select-attributes).

Im Schritt [Segmentplan](../../ui/activate-destinations.md#segment-schedule) müssen Sie Ihre Segmente manuell der entsprechenden ID oder dem Anzeigenamen im Ziel zuordnen.

Bei der Segmentzuordnung empfehlen wir, den Segmentnamen [!DNL Platform] oder eine kürzere Form zu verwenden, um die Verwendung zu vereinfachen. Die Segment-ID oder der Name in Ihrem Ziel muss jedoch nicht mit der in Ihrem [!DNL Platform]-Konto übereinstimmen. Jeder Wert, den Sie in das Zuordnungsfeld einfügen, wird vom Ziel übernommen.

Wenn Sie mehrere Gerätezuordnungen (Cookie-IDs, [!DNL IDFA], [!DNL GAID]) verwenden, stellen Sie sicher, dass Sie denselben Zuordnungswert für alle drei Zuordnungen verwenden. [!DNL The Trade Desk] werden alle Elemente in einem Segment mit einer Aufschlüsselung auf Geräteebene Aggregat.

![Segmentzuordnungs-ID](../../assets/common/segment-mapping-id.png)

## Exportierte Daten {#exported-data}

Um zu überprüfen, ob Daten erfolgreich an das [!DNL The Trade Desk]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL The Trade Desk]-Konto. Wenn die Aktivierung erfolgreich war, werden Audiencen in Ihrem Konto ausgefüllt.
