---
keywords: Ziel verbinden;Zielverbindung;Ziel verbinden;Ziel verbinden
title: Erstellen einer neuen Zielverbindung
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Herstellen einer Verbindung zu einem Ziel in Adobe Experience Platform aufgeführt
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: b275621d9c6552327e0e55c00c8fcf0397088168
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 6%

---

# Erstellen einer neuen Zielverbindung

## Übersicht {#overview}

Bevor Sie Zielgruppendaten an ein Ziel senden können, müssen Sie eine Verbindung zu Ihrer Zielplattform herstellen. In diesem Artikel erfahren Sie, wie Sie mit der Adobe Experience Platform-Benutzeroberfläche ein neues Ziel einrichten.

## Erstellen einer neuen Zielverbindung {#setup}

1. Navigieren Sie zu **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** und wählen Sie die **[!UICONTROL Katalog]** Registerkarte.

   ![Katalogseite](../assets/ui/connect-destinations/catalog.png)

1. Je nachdem, ob Sie über eine bestehende Verbindung zu Ihrem Ziel verfügen, können Sie entweder eine **[!UICONTROL Einrichten]** oder **[!UICONTROL Segmente aktivieren]** auf der Zielkarte. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Segmente aktivieren]** und **[!UICONTROL Einrichten]**, siehe [Katalog](../ui/destinations-workspace.md#catalog) Abschnitt der Dokumentation zum Zielarbeitsbereich.

   Wählen Sie entweder **[!UICONTROL Einrichten]** oder **[!UICONTROL Segmente aktivieren]**, je nachdem, welche Schaltfläche für Sie verfügbar ist.

   ![Katalogseite](../assets/ui/connect-destinations/set-up.png)

   ![Aktivieren von Segmenten](../assets/ui/connect-destinations/activate-segments.png)

1. Wenn Sie **[!UICONTROL Einrichten]**, fahren Sie mit dem nächsten Schritt fort.

   Wenn Sie **[!UICONTROL Segmente aktivieren]** können Sie jetzt eine Liste der vorhandenen Zielverbindungen anzeigen.

   Auswählen **[!UICONTROL Neues Ziel konfigurieren]**.

   ![Neues Ziel konfigurieren](../assets/ui/connect-destinations/configure-new-destination.png)

1. Geben Sie die Verbindungsdetails der Zielplattform ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

   >[!NOTE]
   >
   >Das folgende Bild dient nur zu Veranschaulichungszwecken. Die Details der Zielverbindung variieren je nach Ziel. Detaillierte Informationen zu den Verbindungsdetails für Ihr Ziel finden Sie unter **Verbindungsparameter** in jedem [Zielkatalog](../catalog/overview.md) Seite (z. B. [Google-Kundenabgleich](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Mit Ziel verbinden](../assets/ui/connect-destinations/connect-destination.png)

1. (Optional) Wählen Sie die Ziel-Datenfluss-Warnhinweise aus, die Sie abonnieren möchten. Sie können Warnhinweise abonnieren, wenn Sie einen Datenfluss erstellen, um Warnhinweise zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten. Siehe [In-Context-Zielwarnungen abonnieren](alerts.md) für detaillierte Informationen zu Ziel-Datenfluss-Warnhinweisen.

   ![Benutzeroberflächenbild mit den kontextbezogenen Ziel-Warnhinweisoptionen für Abonnements](../assets/ui/connect-destinations/subscribe-to-alerts.png)

1. Wählen Sie **[!UICONTROL Weiter]** aus.

   ![Mit Ziel verbinden](../assets/ui/connect-destinations/next.png)

1. Wählen Sie die Marketing-Aktionen aus, die für die Daten gelten, die Sie an das Ziel exportieren möchten. Marketing-Aktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketing-Aktionen auswählen oder eine eigene Marketing-Aktion erstellen. Weitere Informationen zu Marketing-Aktionen finden Sie unter [Datennutzungsrichtlinien - Übersicht](../../data-governance/policies/overview.md) Seite.

   ![Marketingaktionen auswählen](../assets/ui/connect-destinations/governance.png)

1. Auswählen **[!UICONTROL Speichern und beenden]** , um die Zielkonfiguration zu speichern, oder wählen Sie **[!UICONTROL Nächste]** um mit den Zielgruppendaten fortzufahren [Aktivierungsfluss](activation-overview.md).