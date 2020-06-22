---
title: Google Ad Manager-Ziel
seo-title: Google Ad Manager-Ziel
description: 'Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten. '
seo-description: 'Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten. '
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 34%

---


# Google Ad Manager-Ziel

## Übersicht

Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.

## Zielspezifikationen

Beachten Sie die folgenden Details, die sich speziell auf Google Ad Manager-Ziele beziehen:

* Sie können die folgenden [Identitäten](../../identity-service/namespaces.md) an Google Ad Manager-Ziele senden: **Google-Cookie-ID, IDFA, GAID, Roku-IDs, Microsoft-IDs, Amazon Fire TV-IDs**.
* Aktivierte Zielgruppen werden in der Google-Plattform programmgesteuert erstellt.
* Die Echtzeit-Kundendatenplattform von Adobe umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Lesen Sie die Audiencen in Google, um die Integration zu validieren und die Targeting-Größe der Audience zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit Google Ad Manager erstellen möchten und die [ID-Synchronisierungsfunktion](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) im Experience Cloud-ID-Dienst in der Vergangenheit nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder den Kundendienst, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor Google-Integrationen in Audience Manager eingerichtet haben, werden die ID-Synchronisierungen, die Sie eingerichtet haben, auf Adobe Echtzeit-CDP übertragen.

## Voraussetzungen

### Zulassungsliste

>[!NOTE]
>
>Die zulassungsliste ist obligatorisch, bevor Sie Ihr erstes Google Ad Manager-Ziel in der Adobe Echtzeit-CDP einrichten. Vergewissern Sie sich bitte, dass der unten beschriebene zulassungsliste-Vorgang von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das Google Ad Manager-Ziel in Adobe Echtzeit-CDP erstellen, müssen Sie sich an Google wenden, damit Adobe die Liste der zulässigen Datenanbieter erhält und Ihr Konto der zulassungsliste hinzugefügt wird. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkonto-Kennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* **Netzwerk-ID** : dies ist Ihr Konto bei Google Ad Manager
* **Audience Link-ID** : dies ist Ihr Konto bei Google Ad Manager
* Ihr Kontotyp. **DFP von Google** oder **AdX-Käufer**.

## Ziel erstellen

1. In **[!UICONTROL Connections > Destinations]**, select Google Ad Manager, and select **[!UICONTROL Create destination]**.
   ![Google Ad Manager-Ziel verbinden](/help/rtcdp/destinations/assets/google-1-destination.png)

2. Geben Sie im Schritt **Einrichten** des Arbeitsablaufs zum Erstellen des Ziels die [!UICONTROL Grundinformationen] für das Ziel ein. <br>

   ![Grundlegende Informationen Google Ad Manager](/help/rtcdp/destinations/assets/ad-manager-setup-step.png)
* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * DoubleClick `DFP by Google` für Herausgeber verwenden
   * Verwenden Sie `AdX buyer` für Google AdX.
* **[!UICONTROL Kontokennung]**: Geben Sie Ihre Google-Kontokennung ein. Dies kann Ihre Netzwerk-ID oder Ihre Audience Link-ID sein. Normalerweise ist dies eine achtstellige ID.
* **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen von Adobe definierten Anwendungsfällen für Marketing finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions).

> [!NOTE]
>
> Wenden Sie sich beim Einrichten eines Google Ad Manager-Ziels an Ihren Google-Kundenbetreuer oder Adobe-Kundenbetreuer, um zu verstehen, welchen Kontotyp Sie haben.

## Aktivieren von Segmenten in Google Ad Manager

For instructions on how to activate segments to Google Ad Manager, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).