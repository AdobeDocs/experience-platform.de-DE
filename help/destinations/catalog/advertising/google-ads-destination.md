---
keywords: Google ads;google ads;google adwords;Google AdWords;Google Adwords
title: Google Ads-Ziel
seo-title: Google Ads-Ziel
description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
seo-description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
translation-type: tm+mt
source-git-commit: 7129a375b1bf4623f78989ed75fcd2bb5dad4a02
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 32%

---


# [!DNL Google Ads] Ziel

## Übersicht

[!DNL Google Ads], früher bekannt als [!DNL Google AdWords], ist ein Online-Werbedienst, der es Unternehmen ermöglicht, per Klick Werbung über textbasierte Suchvorgänge, grafische Displays, [!DNL YouTube] Videos und mobile In-App-Displays hinweg zu bezahlen.

## Zielspezifikationen

Note the following details that are specific to [!DNL Google Ads] destinations:

* You can send the following [identities](../../../identity-service/namespaces.md) to [!DNL Google Ads] destinations: Google cookie ID, IDFA, GAID, Roku IDs, Microsoft IDs, and Amazon Fire TV IDs.
* Activated audiences are created programmatically in the [!DNL Google] platform.
* Die Echtzeit-Kundendatenplattform von umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Zielgruppengröße zu verstehen.

>[!IMPORTANT]
>
>If you are looking to create your first destination with [!DNL Google Ads] and have not enabled the [ID sync functionality](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in the past (with Audience Manager or other applications), please reach out to Adobe Consulting or Customer Care to enable ID syncs. Wenn Sie zuvor Google-Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf die Echtzeit-Kundendatenplattform von übertragen.

### Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) in das Google-Ziel.

## Voraussetzungen

### Vorhandenes [!DNL Google Ads] Konto

>[!IMPORTANT]
>
> [!DNL Google] hat neue [!DNL Google Ads] Cookie-Integrationen mit Drittanbietern überholt. Um die Zulassungslisten im nächsten Abschnitt ausführen zu können, müssen Sie über eine vorhandene Integration mit verfügen [!DNL Google Ads]. Daher [!DNL Google Ads] wird empfohlen, eine Integration zu [!DNL Google Customer Match] erstellen. Weitere Informationen zum Erstellen einer [!DNL Google Customer Match] Integration finden Sie im Tutorial zum Erstellen einer [[!DNL Google Customer Match]](./google-customer-match.md) Verbindung.

### Zulassungsliste

>[!NOTE]
>
>Die Zulassungsliste ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ads] Ziel in Echtzeit-CDP einrichten. Please ensure the allow list process described below has been completed by [!DNL Google] before creating a destination.

Bevor Sie das [!DNL Google Ads] Ziel in Echtzeit-CDP erstellen, müssen Sie sich an [!DNL Google] die Liste der zulässigen Datenanbieter wenden, um die Adobe zu erhalten und Ihr Konto der Zulassungsliste hinzuzufügen. Contact [!DNL Google] and provide the following information:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei [!DNL Google]. Wenden Sie sich an die Kundenunterstützung von Adobe oder Ihren Adobe-Support-Mitarbeiter, um diese Kennung zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkontokennung bei [!DNL Google]. Wenden Sie sich an die Kundenunterstützung von Adobe oder Ihren Adobe-Support-Mitarbeiter, um diese Kennung zu erhalten.
* Ihr Kontotyp: **AdWords**
* **Google AdWords-ID** : Dies ist Ihre ID mit [!DNL Google]. Das Format der Kennung lautet in der Regel 123-456-7890.

## Ziel konfigurieren

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** die Option [!DNL Google Ads]und wählen Sie **[!UICONTROL Konfigurieren]**.

![Google Ads-Ziel verbinden](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche &quot; **[!UICONTROL Aktivieren]** &quot;angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt &quot; [Katalog](../../ui/destinations-workspace.md#catalog) &quot;der Dokumentation zum Zielarbeitsbereich.

In the **Setup** step of the create destination workflow, fill in the [!UICONTROL Basic Information] for the destination.

![Google Ads-Basisinformationen ](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: AdWords ist die einzige verfügbare Option.
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID ein [!DNL Google Ads]. Das Format der Kennung lautet in der Regel 123-456-7890.
* **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md#core-actions).

## Activate segments to [!DNL Google Ads]

For instructions on how to activate segments to [!DNL Google Ads], see [Activate Data to Destinations](../../ui/activate-destinations.md).

## Exportierte Daten

Um zu überprüfen, ob die Daten erfolgreich an das [!DNL Google Ads] Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Ads] Konto. Wenn die Aktivierung erfolgreich war, werden Audiencen in Ihrem Konto ausgefüllt.