---
keywords: Zielkonto aktualisieren, Zielkonten, Aktualisieren von Konten, Ziel aktualisieren
title: Aktualisieren von Zielkonten
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Aktualisieren von Zielkonten in der Adobe Experience Platform-Benutzeroberfläche aufgelistet
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 10%

---

# Aktualisieren von Zielkonten

## Übersicht {#overview}

Die **[!UICONTROL Konten]** zeigt Details zu den Verbindungen an, die Sie mit verschiedenen Zielen hergestellt haben. Unter [Konten - Übersicht](../ui/destinations-workspace.md#accounts) finden Sie alle Informationen, die Sie zu den einzelnen Zielkonten erhalten können.

In diesem Tutorial werden die Schritte zum Aktualisieren der Details des Zielkontos mithilfe der Experience Platform-Benutzeroberfläche beschrieben.

Sie können die Details des Zielkontos aktualisieren, um die Anmeldeinformationen für Ihre aktuellen oder abgelaufenen Konten für Ziele, die Sie derzeit verwenden, zu aktualisieren und erneut zu authentifizieren. Normalerweise haben OAuth- und Bearer-Token je nach Zielplattform eine begrenzte Lebensdauer. Wenn diese Token ablaufen, können Sie sie im Workflow aktualisieren, der weiter unten beschrieben wird. Dieser Workflow leitet Sie durch den OAuth-Workflow oder zum erneuten Einfügen eines Tokens. Wenn sich ein Kennwort oder der Benutzerzugriff in der nachgelagerten Plattform geändert hat, können Sie die Anmeldeinformationen ebenfalls aktualisieren.

Bei Batch-Zielen können Sie den Zugriffs- oder Geheimschlüssel aktualisieren, wenn sich einer dieser Schlüssel geändert hat. Wenn Sie Ihre Dateien in Zukunft verschlüsseln möchten, können Sie außerdem einen öffentlichen RSA-Schlüssel einfügen, und Ihre exportierten Dateien werden in Zukunft verschlüsselt.

![Registerkarte „Konten“](../assets/ui/update-accounts/destination-accounts.png)

## Aktualisieren von Konten {#update}

Gehen Sie wie folgt vor, um Verbindungsdetails für vorhandene Ziele zu aktualisieren.

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Wählen Sie **[!UICONTROL Konten]** in der oberen Kopfzeile aus, um Ihre vorhandenen Konten anzuzeigen.

   ![Registerkarte „Konten“](../assets/ui/update-accounts/accounts-tab.png)

2. Wählen Sie das Symbol ![Filter](/help/images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Konten anzuzeigen, die mit den ausgewählten Zielen verknüpft sind.

   ![Filtern von Zielkonten](../assets/ui/update-accounts/filter-accounts.png)

3. Klicken Sie auf die Auslassungszeichen (`...`) neben dem Namen des Kontos, das Sie aktualisieren möchten. Es wird ein Popup-Bedienfeld angezeigt, das Optionen zum **[!UICONTROL Aktivieren von Zielgruppen]**, **[!UICONTROL Bearbeiten von]** und **[!UICONTROL Löschen]** des Kontos bietet. Klicken Sie auf die ![Details bearbeiten](/help/images/icons/edit.png)Schaltfläche **[!UICONTROL Details bearbeiten]**, um die Kontoinformationen zu bearbeiten.

   ![Konto bearbeiten](../assets/ui/update-accounts/accounts-edit.png)

4. Geben Sie Ihre aktualisierten Kontoanmeldeinformationen ein.

   * Wählen Sie bei Konten, die einen `OAuth1`- oder `OAuth2` Verbindungstyp verwenden, die Option **[!UICONTROL OAuth erneut verbinden]** aus, um Ihre Kontoanmeldeinformationen zu verlängern. Sie können auch den Namen und die Beschreibung Ihres Kontos aktualisieren.

   ![OAuth-Details bearbeiten](../assets/ui/update-accounts/edit-details-oauth.png)

   * Bei Konten, die einen `Access Key`- oder `ConnectionString` Verbindungstyp verwenden, können Sie Ihre Kontoauthentifizierungsinformationen bearbeiten, einschließlich Informationen wie Zugriffs-ID, geheime Schlüssel oder Verbindungszeichenfolgen. Sie können auch den Namen und die Beschreibung Ihres Kontos aktualisieren.

   ![Zugriffsschlüssel für Details bearbeiten](../assets/ui/update-accounts/edit-details-key.png)

   * Bei Konten, die einen `Bearer token` Verbindungstyp verwenden, können Sie bei Bedarf ein neues Bearer-Token eingeben. Sie können auch den Namen und die Beschreibung Ihres Kontos aktualisieren.

   ![Bearbeiten von Details Bearer-Token](../assets/ui/update-accounts/edit-details-bearer.png)

   * Bei Konten, die einen `Server to server` Verbindungstyp verwenden, können Sie den Namen und die Beschreibung Ihres Kontos aktualisieren.

   ![Details Server-zu-Server bearbeiten](../assets/ui/update-accounts/edit-details-s2s.png)

5. Klicken Sie **[!UICONTROL Speichern]**, um die Aktualisierung der Kontodetails abzuschließen.

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich **[!UICONTROL Ziele]** verwendet, um vorhandene Konten zu aktualisieren.

Weitere Informationen zu Zielen finden Sie unter [Ziele - Übersicht](../catalog/overview.md).