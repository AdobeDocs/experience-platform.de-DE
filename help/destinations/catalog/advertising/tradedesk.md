---
keywords: Werbung; die Fachstelle;
title: Verbindung zum Trade Desk
description: 'Der Trade Desk ist eine Selbstbedienungsplattform für Anzeigenkäufer, mit der sie zielgerichtete digitale Kampagnen über Display-, Video- und mobile Inventurquellen hinweg ausführen können. '
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 5%

---


# [!DNL The Trade Desk] connection

## Übersicht {#overview}

[!DNL The Trade Desk] Mit &quot;target&quot;können Sie Profil-Daten an  [!DNL The Trade Desk].

[!DNL The Trade Desk] ist eine Selbstbedienungsplattform für Anzeigenkäufer, um Retargeting und Audience zielgerichteter digitaler Kampagnen für Display-, Video- und Mobilgeräte-Inventurquellen durchzuführen.

Um Profil-Daten an [!DNL Trade Desk] zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Zielspezifikationen {#destination-specs}

Beachten Sie die folgenden Details, die für das [!DNL Trade Desk]-Ziel spezifisch sind:

* Sie können die folgenden [Identitäten](../../../identity-service/namespaces.md) an [!DNL The Trade Desk]-Ziele senden: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL The Trade Desk] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in der Vergangenheit im Experience Cloud-ID-Dienst (mit Adobe Audience Manager oder anderen Anwendungen) nicht aktiviert haben, wenden Sie sich bitte an Adobe Consulting oder den Kundendienst, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor [!DNL The Trade Desk]-Integrationen in Audience Manager eingerichtet haben, werden die ID-Synchronisierungen, die Sie eingerichtet haben, auf Plattform übertragen.

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
* **[!UICONTROL Serverort]**: Fragen Sie Ihren  [!DNL Trade Desk] Kundenbetreuer, welchen regionalen Server Sie verwenden sollten. Die folgenden regionalen Server stehen zur Auswahl:

   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapur]**
   * **[!UICONTROL Tokio]**
   * **[!UICONTROL Nordamerika Osten]**
   * **[!UICONTROL Nordamerika - Westen]**
   * **[!UICONTROL Lateinamerika]**

* **[!UICONTROL Marketingaktion]**: Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie auf der Seite [Datenverwaltung in Adobe Experience Platform](../../../data-governance/policies/overview.md). Informationen zu den einzelnen, von der Adobe definierten Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

![Schritt zur Authentifizierung des Trade Desk](../../assets/catalog/advertising/tradedesk/authenticate.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**. Ihr Ziel wird jetzt erstellt. Sie können auf [!UICONTROL Speichern und beenden] klicken, wenn Sie Segmente später aktivieren möchten, oder Sie können [!UICONTROL Weiter] auswählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen finden Sie den Rest des Workflows im nächsten Abschnitt [Segmente aktivieren](#activate-segments).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md#select-attributes).

Im Schritt [Segmentplan](../../ui/activate-destinations.md#segment-schedule) müssen Sie Ihre Segmente manuell der entsprechenden ID oder dem Anzeigenamen im Ziel zuordnen.

Bei der Segmentzuordnung empfehlen wir, den Segmentnamen [!DNL Platform] oder eine kürzere Form zu verwenden, um die Verwendung zu vereinfachen. Die Segment-ID oder der Name in Ihrem Ziel muss jedoch nicht mit der in Ihrem [!DNL Platform]-Konto übereinstimmen. Jeder Wert, den Sie in das Zuordnungsfeld einfügen, wird vom Ziel übernommen.

Wenn Sie mehrere Gerätezuordnungen (Cookie-IDs, [!DNL IDFA], [!DNL GAID]) verwenden, stellen Sie sicher, dass Sie denselben Zuordnungswert für alle drei Zuordnungen verwenden. [!DNL The Trade Desk] werden alle Elemente in einem Segment mit einer Aufschlüsselung auf Geräteebene Aggregat.

![Segmentzuordnungs-ID](../../assets/common/segment-mapping-id.png)

## Exportierte Daten {#exported-data}

Um zu überprüfen, ob Daten erfolgreich an das [!DNL The Trade Desk]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Trade Desk]-Konto. Wenn die Aktivierung erfolgreich war, werden Audiencen in Ihrem Konto ausgefüllt.
