---
title: Erweiterte Verwaltung von Aktivierungskonten
description: Erfahren Sie, wie Sie Verwaltungsaufgaben für Ihr erweitertes Aktivierungskonto ausführen, z. B. die Lizenznutzung überwachen und die richtigen Berechtigungen zuweisen.
exl-id: ee0ec4b9-a083-447b-b7a7-e1307e90c646
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Kontoverwaltung

Um Zielgruppen aus Audience Manager zu erfassen und sie für Social- und Werbeziele zu aktivieren, müssen Sie zunächst ein Benutzerkonto für erweiterte Aktivierung erstellen und das Konto der richtigen Berechtigungsrolle zuweisen.

Auf dieser Seite wird beschrieben, wie Sie ein Benutzerkonto in der Admin Console erstellen und die richtigen Berechtigungen für die erweiterte Aktivierung zuweisen.

## Benutzerkonten erstellen {#create-users}

Bevor Sie [!DNL Audience Manager Expanded Activation] verwenden können, müssen Sie ein Benutzerkonto erstellen.

Um ein Benutzerkonto für [!DNL Expanded Activation] zu erstellen, befolgen Sie die Anweisungen zum Verwalten von Benutzern in der Dokumentation zu [Adobe Admin Console](https://helpx.adobe.com/de/enterprise/using/manage-users-individually.html) .

## Benutzer zur Berechtigungsrolle hinzufügen {#permissions}

Nachdem Sie ein Benutzerkonto erstellt haben, müssen Sie es der Berechtigungsrolle [!DNL Expanded Activation] in der Benutzeroberfläche von [!DNL Expanded Activation] hinzufügen.

Wechseln Sie zu **[!UICONTROL Administration]** -> **[!UICONTROL Berechtigungen]** -> **[!UICONTROL Rollen]** und wählen Sie die erweiterte Aktivierungsstandardrolle **[!UICONTROL 7 aus.]**

![ Erweitertes Bild der Aktivierungsbenutzeroberfläche, das die Seite &quot;Benutzerrollen&quot;anzeigt.](assets/expanded-activation-role.png)

Gehen Sie zur Registerkarte **[!UICONTROL Benutzer]** und wählen Sie **[!UICONTROL Benutzer hinzufügen]** aus.

![ Erweitertes Bild der Aktivierungsbenutzeroberfläche, das die Seite &quot;Benutzer&quot;anzeigt.](assets/add-users.png)

Wählen Sie den neu erstellten Benutzer aus der verfügbaren Liste und danach **[!UICONTROL Speichern]** aus.

![ Erweitertes Bild der Aktivierungsbenutzeroberfläche, das die Seite &quot;Benutzer hinzufügen&quot;anzeigt.](assets/add-user.png)

Das Benutzerkonto wird jetzt erstellt und der richtigen Rolle zugewiesen. Jetzt kann sie auf die Benutzeroberfläche **[!UICONTROL Erweiterte Aktivierung]** zugreifen.

## Lizenznutzung überwachen {#license-usage}

Ihr [!DNL Audience Manager Expanded Activation] -Vertrag gibt die maximale Anzahl von Hash-E-Mails an, die Sie in Ihr Konto aufnehmen können.

Sie finden diese Informationen auf der Seite **[!UICONTROL Administration]** -> **[!UICONTROL Lizenzverwendung]** .

![ Erweitertes Bild der Aktivierungsbenutzeroberfläche, das den Bildschirm zur Lizenznutzung anzeigt.](assets/license-usage.png)

Auf dieser Seite finden Sie die folgenden Informationen:

* **[!UICONTROL Produkt]**: Das Adobe-Produkt, für das Sie lizenziert sind. Dies ist immer **[!UICONTROL erweiterte Aktivierung des Audience Managers]**.
* **[!UICONTROL Primäre Metrik]**: Der Name der Metrik, die zur Verwendung verfolgt wird. Dabei handelt es sich immer um **[!UICONTROL adressierbare Zielgruppe]**.
* **[!UICONTROL Lizenzbetrag]**: Die maximale Anzahl von Hash-E-Mails, für die Sie eine Lizenz besitzen.

  >[!TIP]
  >
  >Sie erfassen gehashte E-Mails über den Quell-Connector [Audience Manager ](../sources/connectors/adobe-applications/audience-manager.md). Weitere Informationen finden Sie in der Dokumentation zu [Aktivierung von Zielgruppen](activate-audiences.md) .

* **[!UICONTROL Nutzung]**: die Anzahl der gehashten E-Mails, die Sie erfasst haben.
* **[!UICONTROL Nutzung %]**: der Prozentsatz Ihres Lizenzbetrags, den Sie verwendet haben.

Weitere Informationen zur Lizenzverwendung im Experience Platform finden Sie in der [Dokumentation zur Lizenzverwendung](../dashboards/guides/license-usage.md).

## Nächste Schritte {#next-steps}

Nachdem Sie jetzt mindestens ein Benutzerkonto mit dem richtigen Zugriff auf &quot;Erweiterte Aktivierung&quot;konfiguriert haben, können Sie mit der Verwendung des Kontos beginnen, um [Zielgruppen aktivieren](activate-audiences.md).
