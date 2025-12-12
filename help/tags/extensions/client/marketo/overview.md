---
title: Marketo Munchkin-Erweiterung - Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Marketo Munchkin“ in Adobe Experience Platform vertraut.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 97%

---

# Marketo Munchkin-Erweiterung – Übersicht

Verwenden Sie diese Erweiterung, um den JavaScript-Trackingcode für [!DNL Marketo Munchkin] in Ihre Eigenschaft zu integrieren. Mit [!DNL Marketo Munchkin]-JavaScript können Sie Seitenbesuche und -klicks von Endbenutzern auf Ihren Marketo-Landingpages und externen Web-Seiten verfolgen.

## Marketo Munchkin-Erweiterung installieren

Wenn die [!DNL Marketo Munchkin]-Erweiterung noch nicht installiert ist, öffnen Sie die Eigenschaft, wählen Sie **[!UICONTROL Extensions > Catalog]** aus, bewegen Sie den Mauszeiger über die [!DNL Marketo Munchkin]-Erweiterung und klicken Sie auf **[!UICONTROL Install]**.

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
