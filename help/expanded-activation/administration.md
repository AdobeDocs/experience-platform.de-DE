---
title: Erweiterte Verwaltung von Aktivierungskonten
description: Erfahren Sie, wie Sie Verwaltungsaufgaben für Ihr erweitertes Aktivierungskonto ausführen, z. B. die Lizenznutzung überwachen und die richtigen Berechtigungen zuweisen.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Kontoverwaltung

Um Zielgruppen aus Audience Manager zu erfassen und sie für Social- und Werbeziele zu aktivieren, müssen Sie zunächst ein Benutzerkonto für erweiterte Aktivierung erstellen und das Konto der richtigen Berechtigungsrolle zuweisen.

Auf dieser Seite wird beschrieben, wie Sie ein Benutzerkonto in der Admin Console erstellen und die richtigen Berechtigungen für die erweiterte Aktivierung zuweisen.

## Benutzerkonten erstellen {#create-users}

Bevor Sie [!DNL Audience Manager Expanded Activation], müssen Sie ein Benutzerkonto erstellen.

So erstellen Sie ein Benutzerkonto für [!DNL Expanded Activation]Befolgen Sie die Anweisungen zum Verwalten von Benutzern über die [Adobe Admin Console](https://helpx.adobe.com/de/enterprise/using/manage-users-individually.html) Dokumentation.

## Benutzer zur Berechtigungsrolle hinzufügen {#permissions}

Nachdem Sie ein Benutzerkonto erstellt haben, müssen Sie es zum [!DNL Expanded Activation] Berechtigungsrolle in der [!DNL Expanded Activation] -Benutzeroberfläche.

Navigieren Sie zu **[!UICONTROL Administration]** -> **[!UICONTROL Berechtigungen]** -> **[!UICONTROL Rollen]** und wählen Sie die **[!UICONTROL Erweiterte Aktivierungsstandardrolle]**.

![Erweitertes Bild der Benutzeroberfläche &quot;Aktivierung&quot;mit der Seite &quot;Rollen&quot;.](assets/expanded-activation-role.png)

Navigieren Sie zu **[!UICONTROL Benutzer]** Registerkarte und wählen Sie **[!UICONTROL Benutzer hinzufügen]**.

![Erweitertes Bild der Aktivierungsbenutzeroberfläche, das die Seite Benutzer anzeigt.](assets/add-users.png)

Wählen Sie den neu erstellten Benutzer aus der verfügbaren Liste aus und wählen Sie **[!UICONTROL Speichern]**.

![Erweitertes Bild der Aktivierungsbenutzeroberfläche mit der Seite Benutzer hinzufügen .](assets/add-user.png)

Das Benutzerkonto wird jetzt erstellt und der richtigen Rolle zugewiesen. Sie kann jetzt auf die **[!UICONTROL Erweiterte Aktivierung]** -Benutzeroberfläche.

## Lizenznutzung überwachen {#license-usage}

Ihre [!DNL Audience Manager Expanded Activation] Der Vertrag gibt die maximale Anzahl von Hash-E-Mails an, die Sie in Ihr Konto aufnehmen können.

Diese Informationen finden Sie unter **[!UICONTROL Administration]** -> **[!UICONTROL Lizenzverwendung]** Seite.

![Erweitertes Bild der Aktivierungsbenutzeroberfläche, das den Bildschirm zur Lizenznutzung anzeigt.](assets/license-usage.png)

Auf dieser Seite finden Sie die folgenden Informationen:

* **[!UICONTROL Produkt]**: Das Adobe-Produkt, für das Sie lizenziert sind. Dies wird immer **[!UICONTROL Erweiterte Aktivierung des Audience Managers]**.
* **[!UICONTROL Primäre Metrik]**: Der Name der Metrik, die zur Verwendung verfolgt wird. Dies wird immer **[!UICONTROL Ansprechbare Zielgruppe]**.
* **[!UICONTROL Lizenzbetrag]**: Die maximale Anzahl von Hash-E-Mails, die lizenziert sind zu erfassen.

  >[!TIP]
  >
  >Sie erfassen Hash-E-Mails über die [Quell-Connector für Audience Manager](../sources/connectors/adobe-applications/audience-manager.md). Siehe die Dokumentation unter [So aktivieren Sie Zielgruppen](activate-audiences.md) für weitere Details.

* **[!UICONTROL Nutzung]**: die Anzahl der erfassten gehashten E-Mails.
* **[!UICONTROL Nutzung %]**: der Prozentsatz Ihres Lizenzbetrags, den Sie verwendet haben.

Weitere Informationen zur Lizenzverwendung im Experience Platform finden Sie unter [Dokumentation zur Lizenzverwendung](../dashboards/guides/license-usage.md).

## Nächste Schritte {#next-steps}

Nachdem Sie mindestens ein Benutzerkonto mit dem richtigen Zugriff auf &quot;Erweiterte Aktivierung&quot;konfiguriert haben, können Sie mit der Verwendung des Kontos beginnen, um [Zielgruppen aktivieren](activate-audiences.md).
