---
title: Erweiterte Aktivierungskonto-Verwaltung
description: Erfahren Sie, wie Sie administrative Aufgaben für Ihr erweitertes Aktivierungskonto ausführen, z. B. die Lizenznutzung überwachen und die richtigen Berechtigungen zuweisen.
exl-id: ee0ec4b9-a083-447b-b7a7-e1307e90c646
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Kontoverwaltung

Um Zielgruppen aus Audience Manager aufzunehmen und sie für Social Media- und Werbeziele zu aktivieren, müssen Sie zunächst ein erweitertes Benutzerkonto für die Aktivierung erstellen und das Konto der richtigen Berechtigungsrolle zuweisen.

Auf dieser Seite wird beschrieben, wie Sie ein Benutzerkonto in der Admin Console erstellen und die richtigen Berechtigungen für die erweiterte Aktivierung zuweisen.

## Erstellen von Benutzerkonten {#create-users}

Bevor Sie [!DNL Audience Manager Expanded Activation] verwenden können, müssen Sie ein Benutzerkonto erstellen.

Um ein Benutzerkonto für [!DNL Expanded Activation] zu erstellen, befolgen Sie die Anweisungen zur Benutzerverwaltung in der Dokumentation zu [Adobe Admin Console](https://helpx.adobe.com/de/enterprise/using/manage-users-individually.html).

## Benutzer zu Berechtigungsrolle hinzufügen {#permissions}

Nachdem Sie ein Benutzerkonto erstellt haben, müssen Sie es in der [!DNL Expanded Activation]-Benutzeroberfläche der Rolle [!DNL Expanded Activation] hinzufügen.

Wechseln Sie zu **[!UICONTROL Administration]** -> **[!UICONTROL Berechtigungen]** -> **[!UICONTROL Rollen]** und wählen Sie die **[!UICONTROL Erweiterte Standardrolle für die Aktivierung]**.

![Benutzeroberflächenbild für die erweiterte Aktivierung, das die Seite „Rollen“ anzeigt.](assets/expanded-activation-role.png)

Gehen Sie zur Registerkarte **[!UICONTROL Benutzer]** und wählen Sie **[!UICONTROL Benutzer hinzufügen]** aus.

![Erweitertes Bild der Benutzeroberfläche für die Aktivierung, das die Seite „Benutzer“ anzeigt.](assets/add-users.png)

Wählen Sie den neu erstellten Benutzer aus der verfügbaren Liste aus und klicken Sie auf **[!UICONTROL Speichern]**.

![Benutzeroberflächenbild zur erweiterten Aktivierung , das die Seite „Benutzer hinzufügen“ anzeigt.](assets/add-user.png)

Das Benutzerkonto wird jetzt erstellt und der richtigen Rolle zugewiesen. Sie kann jetzt auf die Benutzeroberfläche **[!UICONTROL Erweiterte Aktivierung]** zugreifen.

## Überwachen der Lizenznutzung {#license-usage}

Ihr [!DNL Audience Manager Expanded Activation] legt die maximale Anzahl an gehashten E-Mails fest, die Sie in Ihr Konto aufnehmen können.

Diese Informationen finden Sie auf der Seite **[!UICONTROL Administration]** -> **[!UICONTROL Lizenznutzung]**.

![Erweitertes Bild der Benutzeroberfläche für die Aktivierung, das den Bildschirm zur Lizenznutzung anzeigt.](assets/license-usage.png)

Auf dieser Seite finden Sie die folgenden Informationen:

* **[!UICONTROL Product]**: Das Adobe-Produkt, für das Sie lizenziert sind. Dies ist immer die erweiterte Aktivierung des **[!UICONTROL Audience Managers]**.
* **[!UICONTROL Primäre Metrik]**: Der Name der Metrik, deren Verwendung verfolgt wird. Dies ist immer **[!UICONTROL adressierbare Zielgruppe]**.
* **[!UICONTROL Lizenzbetrag]**: Die maximale Anzahl von gehashten E-Mails, die Sie aufnehmen dürfen.

  >[!TIP]
  >
  >Sie nehmen gehashte E-Mails über den [Audience Manager-Quell-Connector](../sources/connectors/adobe-applications/audience-manager.md) auf. Weitere Informationen finden Sie in der [&#x200B; zum Aktivieren von &#x200B;](activate-audiences.md) .

* **[!UICONTROL Nutzung]**: die Anzahl der gehashten E-Mails, die Sie aufgenommen haben.
* **[!UICONTROL Nutzung %]**: Der Prozentsatz des von Ihnen verwendeten Lizenzbetrags.

Weitere Informationen zur Lizenznutzung in Experience Platform finden Sie unter [Lizenznutzungsdokumentation](../dashboards/guides/license-usage.md).

## Nächste Schritte {#next-steps}

Nachdem Sie nun mindestens ein Benutzerkonto mit dem richtigen Zugriff auf „Erweiterte Aktivierung“ konfiguriert haben, können Sie mit der Verwendung des Kontos beginnen [Zielgruppen aktivieren](activate-audiences.md).
