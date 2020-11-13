---
keywords: advertising; the trade desk;
title: Ziel des Trade Desk
seo-title: Ziel des Trade Desk
description: 'Der Trade Desk ist eine Selbstbedienungsplattform für Anzeigenkäufer, um zielgerichtete digitale Kampagnen über Display-, Video- und mobile Inventurquellen hinweg auszuführen. '
seo-description: Der Trade Desk ist eine Selbstbedienungsplattform für Anzeigenkäufer, um zielgerichtete digitale Kampagnen über Display-, Video- und mobile Inventurquellen hinweg auszuführen.
translation-type: tm+mt
source-git-commit: c9fb63b390d4c7dddcdb35a85710ff664614ad63
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 5%

---


# [!DNL The Trade Desk] Ziel

## Übersicht {#overview}

[!DNL The Trade Desk] Mit &quot;target&quot;können Sie Profil-Daten an [!DNL The Trade Desk].

[!DNL The Trade Desk] ist eine Selbstbedienungsplattform für Anzeigenkäufer, um Retargeting und Audience zielgerichteter digitaler Kampagnen für Display-, Video- und Mobilgeräte-Inventurquellen durchzuführen.

Um Profil-Daten an [!DNL The Trade Desk]zu senden, müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Zielspezifikationen {#destination-specs}

Note the following details that are specific to the [!DNL The Trade Desk] destination:

* Sie können die folgenden [Identitäten](../../identity-service/namespaces.md) an [!DNL The Trade Desk] Ziele senden: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## Anwendungsbeispiele {#use-cases}

Als Marketingspezialist möchte ich Segmente verwenden können, die aus [!DNL Trade Desk IDs] oder Geräte-IDs aufgebaut sind, um Retargeting oder Audience zielgerichteter digitaler Kampagnen zu erstellen.

## Exporttyp {#export-type}

**[!DNL Segment export]** - Sie exportieren alle Segmentmitglieder (Audiencen) in das Ziel.

## Mit Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** die Option [!DNL The Trade Desk]und wählen Sie **[!UICONTROL Konfigurieren]**.

   ![Das Ziel des Trade Desk konfigurieren](assets/tradedesk-destination-configure.png)

   >[!NOTE]
   >
   >Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche &quot; **[!UICONTROL Aktivieren]** &quot;angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt &quot; [Katalog](../destinations/destinations-workspace.md#catalog) &quot;der Dokumentation zum Zielarbeitsbereich.
   >
   >![Handelsdatenträger-Ziel aktivieren](assets/tradedesk-destination-activate.png)

1. Im Schritt [!UICONTROL Authentifizierung] müssen Sie die [!DNL The Trade Desk] Verbindungsdetails eingeben:

   * **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in Zukunft erkennen werden.
   * **[!UICONTROL Beschreibung]**: Eine Beschreibung, mit der Sie dieses Ziel in Zukunft identifizieren können.
   * **[!UICONTROL Konto-ID]**: Ihre [!DNL Trade Desk] Konto-ID .
   * **[!UICONTROL geheim]**: Der in den `clientSecret` Clientberechtigungen verwendete [!DNL OAuth2] Parameter.
   * **[!UICONTROL Serverort]**: Fragen Sie Ihren [!DNL The Trade Desk] Kundenbetreuer, welchen regionalen Server Sie verwenden sollten. Die folgenden regionalen Server stehen zur Auswahl:

      * **[!UICONTROL Europa]**
      * **[!UICONTROL Singapur]**
      * **[!UICONTROL Tokio]**
      * **[!UICONTROL Nordamerika Osten]**
      * **[!UICONTROL Nordamerika - Westen]**
      * **[!UICONTROL Lateinamerika]**
   * **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](../../data-governance/policies/overview.md#core-actions).

   ![Schritt zur Authentifizierung des Trade Desk](assets/tradedesk-destination-authentication.png)

1. Klicken Sie auf Ziel **[!UICONTROL erstellen]**. Ihr Ziel wird jetzt erstellt. You can click [!UICONTROL Save &amp; Exit] if you want to activate segments later, or you can select [!UICONTROL Next] to continue the workflow and select segments to activate. In either case, see the next section, [Activate Segments](#activate-segments), for the rest of the workflow.

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](activate-destinations.md#select-attributes).

Während des Zeitplanschritts für [Segmente](activate-destinations.md#segment-schedule) müssen Sie Ihre Segmente manuell der entsprechenden ID oder dem Anzeigenamen im Ziel zuordnen.

Beim Zuordnen von Segmenten sollten Sie den [!DNL Platform] Segmentnamen oder eine kürzere Form verwenden, um die Verwendung zu vereinfachen. Die Segment-ID oder der Name in Ihrem Ziel muss jedoch nicht mit der in Ihrem [!DNL Platform] Konto übereinstimmen. Jeder Wert, den Sie in das Zuordnungsfeld einfügen, wird vom Ziel übernommen.

Wenn Sie mehrere Gerätezuordnungen verwenden (Cookie-IDs, [!DNL IDFA][!DNL GAID]), stellen Sie sicher, dass Sie denselben Zuordnungswert für alle drei Zuordnungen verwenden. [!DNL The Trade Desk] werden alle Elemente in einem Segment mit einer Aufschlüsselung auf Geräteebene Aggregat.

![Segmentzuordnungs-ID](assets/segment-mapping-id.png)


## Exportierte Daten {#exported-data}

Überprüfen Sie Ihr [!DNL The Trade Desk] Konto, um zu überprüfen, ob die Daten erfolgreich an [!DNL The Trade Desk] das Ziel exportiert wurden. Wenn die Aktivierung erfolgreich war, werden Audiencen in Ihrem Konto ausgefüllt.
