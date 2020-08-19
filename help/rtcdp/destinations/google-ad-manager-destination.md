---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager
title: Google Ad Manager-Ziel
seo-title: Google Ad Manager-Ziel
description: 'Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten. '
seo-description: 'Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten. '
translation-type: tm+mt
source-git-commit: 2dfa46906374151628d46c309df724a59f8dc50e
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 46%

---


# [!DNL Google Ad Manager Destination]

## Übersicht

[!DNL Google Ad Manager], früher als für Herausgeber oder bekannt, ist eine AdX-Plattform von , die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.[!DNL DoubleClick][!DNL DoubleClick AdX][!DNL Google]

## Zielspezifikationen

Note the following details that are specific to [!DNL Google Ad Manager] destinations:

* Sie können die folgenden [Identitäten](../../identity-service/namespaces.md)[!DNL Google Ad Manager] an -Ziele senden: **Google-Cookie-ID, IDFA, GAID, Roku-IDs, Microsoft-IDs, Amazon Fire TV-IDs**.
* Activated audiences are created programmatically in the [!DNL Google] platform.
* Die Echtzeit-Kundendatenplattform von Adobe umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Zielgruppengröße zu verstehen.

>[!IMPORTANT]
>
>If you are looking to create your first destination with [!DNL Google Ad Manager] and have not enabled the [ID sync functionality](https://docs.adobe.com/content/help/de-DE/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in the past (with Audience Manager or other applications), please reach out to Adobe Consulting or Customer Care to enable ID syncs. If you had previously set up [!DNL Google] integrations in Audience Manager, the ID syncs you had set up carry over to Adobe Real-time CDP.

## Voraussetzungen 

### Zulassungsliste

>[!NOTE]
>
>Die Zulassungsliste ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ad Manager] Ziel in der Adobe Echtzeit-CDP einrichten. Please ensure the allow list process described below has been completed by [!DNL Google] before creating a destination.

Bevor Sie das [!DNL Google Ad Manager] Ziel in Adobe Echtzeit-CDP erstellen, müssen Sie sich an [!DNL Google] die Adobe wenden, um die Liste der zulässigen Datenanbieter aufzunehmen und Ihr Konto der Zulassungsliste hinzuzufügen. Contact [!DNL Google] and provide the following information:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei [!DNL Google]. Wenden Sie sich an die Kundenunterstützung von Adobe oder Ihren Adobe-Support-Mitarbeiter, um diese Kennung zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkontokennung bei [!DNL Google]. Wenden Sie sich an die Kundenunterstützung von Adobe oder Ihren Adobe-Support-Mitarbeiter, um diese Kennung zu erhalten.
* **Netzwerkkennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* **Zielgruppenverknüpfungskennung**: Dies ist Ihr Konto bei [!DNL Google Ad Manager]
* Ihr Kontotyp. **DFP von Google** oder **AdX Buyer**.

## Ziel konfigurieren

1. Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** die Option [!DNL Google Ad Manager]und wählen Sie **[!UICONTROL Konfigurieren]**.
   ![Mit Google Ad Manager-Ziel verbinden](/help/rtcdp/destinations/assets/google-1-destination.png)

   >[!NOTE]
   >
   >Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche &quot; **[!UICONTROL Aktivieren]** &quot;angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt &quot; [Katalog](/help/rtcdp/destinations/destinations-workspace.md#catalog) &quot;der Dokumentation zum Zielarbeitsbereich.

2. In the **Setup** step of the create destination workflow, fill in the [!UICONTROL Basic Information] for the destination. <br>

   ![Grundlegende Informationen – Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `DFP by Google` für for Publishers.[!DNL DoubleClick]
   * Use `AdX buyer` for [!DNL Google AdX]
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID ein [!DNL Google]. Dies kann Ihre Netzwerkkennung oder Ihre Zielgruppenverknüpfungskennung sein. Normalerweise ist dies eine achtstellige Kennung.
* **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions).

>[!NOTE]
>
> When setting up a [!DNL Google Ad Manager] destination please work with your [!DNL Google Account Manager] or Adobe representative to understand which account type you have.

## Activate segments to [!DNL Google Ad Manager]

For instructions on how to activate segments to [!DNL Google Ad Manager], see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

## Exportierte Daten

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL Google Ad Manager] Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Ad Manager] Konto. Wenn die Aktivierung erfolgreich war, werden Audiencen in Ihrem Konto ausgefüllt.