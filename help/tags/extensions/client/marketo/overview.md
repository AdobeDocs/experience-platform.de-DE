---
title: Marketo Munchkin-Erweiterung  Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Marketo Munchkin“ in Adobe Experience Platform vertraut.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 100%

---

# Marketo Munchkin-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Verwenden Sie diese Erweiterung, um den JavaScript-Trackingcode für [!DNL Marketo Munchkin] in Ihre Eigenschaft zu integrieren. Mit [!DNL Marketo Munchkin]-JavaScript können Sie Seitenbesuche und -klicks von Endbenutzern auf Ihren Marketo-Landingpages und externen Web-Seiten verfolgen.

## Marketo Munchkin-Erweiterung installieren

Wenn die [!DNL Marketo Munchkin]-Erweiterung noch nicht installiert ist, öffnen Sie die Eigenschaft, wählen Sie **[!UICONTROL Erweiterungen > Katalog]** aus, bewegen Sie den Mauszeiger über die [!DNL Marketo Munchkin]-Erweiterung und klicken Sie auf **[!UICONTROL Installieren]**.

Diese Erweiterung hat keine erforderliche Konfiguration.

## Aktionstypen für die Marketo Munchkin-Erweiterung

In diesem Abschnitt werden die in der [!DNL Marketo Munchkin]-Erweiterung verfügbaren Aktionstypen beschrieben.

### Initialisieren

![](../../../images/munchkin-Init.png)

**Munchkin ID: (erforderlich)** Munchkin-Konto-ID gefunden unter Admin > Integration > Munchkin-Menü.

**Configurations:** Alle konfigurierbaren Parameter sind [hier](https://developers.marketo.com/javascript-api/lead-tracking/configuration/) dokumentiert.

### Seitenbesuch

![](../../../images/munchkin-visit-page.png)

**url: (erforderlich)** Der URL-Dateipfad, der zum Aufzeichnen eines Seitenbesuchs verwendet wird.

**params:** Eine Abfragezeichenfolge der gewünschten Parameter, die aufgezeichnet werden sollen.

**name:** Der benutzerdefinierte Name des Webseitenassets.

### Link-Aufruf

![](../../../images/munchkin-click-link.png)

**href: (erforderlich)** Der URL-Dateipfad, der zum Aufzeichnen eines Link-Aufrufs verwendet wird.
