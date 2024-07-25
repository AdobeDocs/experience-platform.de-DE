---
keywords: Löschen von Zielkonten, Zielkonten, Löschen von Konten
title: Löschen von Zielkonten
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Löschen von Zielkonten in der Adobe Experience Platform-Benutzeroberfläche aufgeführt
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 18%

---

# Löschen von Zielkonten

## Übersicht {#overview}

Die Registerkarte **[!UICONTROL Konten]** enthält Details zu den Verbindungen, die Sie mit verschiedenen Zielen hergestellt haben. In der [Übersicht über Konten](../ui/destinations-workspace.md#accounts) finden Sie alle Informationen, die Sie für jedes Zielkonto erhalten können.

In diesem Tutorial werden die Schritte zum Löschen von Zielkonten beschrieben, die nicht mehr über die Experience Platform-Benutzeroberfläche benötigt werden.

![Registerkarte „Konten“](../assets/ui/update-accounts/destination-accounts.png)

## Löschen von Konten {#delete}

>[!TIP]
>
>Bevor Sie das Zielkonto löschen, müssen Sie zunächst alle vorhandenen Datenflüsse löschen, die mit dem Zielkonto verknüpft sind. Informationen zum Löschen vorhandener Ziel-Datenflüsse finden Sie im Tutorial zum [Löschen von Ziel-Datenflüssen in der Benutzeroberfläche](./delete-destinations.md).

Gehen Sie wie folgt vor, um vorhandene Zielkonten zu löschen.

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Wählen Sie in der oberen Kopfzeile **[!UICONTROL Konten]** aus, um Ihre vorhandenen Konten anzuzeigen.

   ![Registerkarte „Konten“](../assets/ui/delete-accounts/accounts-tab.png)

2. Wählen Sie das Symbol ![Filter](/help/images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Konten anzuzeigen, die mit den ausgewählten Zielen verknüpft sind.

   ![Ziele filtern](../assets/ui/delete-accounts/filter-accounts.png)

3. Wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Kontos aus, das Sie löschen möchten. Es wird ein Popup-Bedienfeld angezeigt, das Optionen für **[!UICONTROL Zielgruppen aktivieren]**, **[!UICONTROL Details bearbeiten]** und **[!UICONTROL Löschen]** des Kontos bereitstellt. Wählen Sie die Schaltfläche ![Löschen ](/help/images/icons/delete.png) **[!UICONTROL Löschen]** aus, um das gewünschte Konto zu löschen.

   ![Zielkonto löschen](../assets/ui/delete-accounts/delete-accounts.png)

4. Ein letztes Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Löschen]** aus, um den Vorgang abzuschließen.

![Kontolöschung bestätigen](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich &quot;Ziele&quot;zum Löschen vorhandener Konten verwendet.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service]-API finden Sie im Tutorial zum [Löschen von Verbindungen mithilfe der Flow Service-API](../api/delete-destination-account.md) .
