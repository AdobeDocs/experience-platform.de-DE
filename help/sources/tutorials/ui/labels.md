---
title: Anwenden von Zugriffskennzeichnungen zur Verwaltung des Benutzerzugriffs auf Datenflüsse von Quellen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mit der Experience Platform-Benutzeroberfläche Zugriffsbeschriftungen anwenden und den Benutzerzugriff auf Ihre Quelldatenflüsse verwalten können.
exl-id: 7aab9706-2f43-43c7-9878-1959d5a8a6b0
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 3%

---

# Anwenden von Zugriffskennzeichnungen zur Verwaltung des Benutzerzugriffs auf Datenflüsse von Quellen in der Benutzeroberfläche

Real-Time CDP Sie können die von der [attributbasierten Zugriffssteuerung) in &#x200B;](../../../access-control/abac/overview.md) bereitgestellten Funktionen verwenden, um Beschriftungen auf Ihre Quelldatenflüsse anzuwenden. Mit dieser Funktion können Sie sicherstellen, dass nur eine Untergruppe von Benutzern in Ihrer Organisation Zugriff auf bestimmte Quellen und Datenflüsse erhält.

Wenn Sie einem bestimmten Datenfluss eine Zugriffsbeschriftung hinzufügen, können nur Benutzer, die Zugriff auf eine Rolle haben, der diese Beschriftung zugewiesen ist, diesen Datenfluss anzeigen und bearbeiten. Wenn ein Quelldatenfluss nicht mit Beschriftungen gekennzeichnet ist, ist er für alle Benutzer sichtbar, die zu Ihrer Organisation gehören. Wenn Sie beispielsweise die Kennzeichnung C12 auf einen Datenfluss anwenden, können Benutzende, denen eine Rolle zugewiesen wurde, die nicht über die Kennzeichnung C12 verfügt, den Datenfluss nicht mit der Kennzeichnung C12 anzeigen und bearbeiten.

Lesen Sie dieses Handbuch, um Informationen zum Anwenden von Zugriffsbeschriftungen auf Ihre Quelldatenflüsse mithilfe der Benutzeroberfläche von Adobe Experience Platform zu erhalten.

## Erste Schritte

Bevor Sie mit Zugriffssteuerungsbeschriftungen arbeiten, stellen Sie sicher, dass Sie sich zunächst mit den Funktionen der attributbasierten Zugriffssteuerung vertraut machen. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [Attributbasierte Zugriffssteuerung – Übersicht](../../../access-control/abac/overview.md)
* [End-to-End-Handbuch zur attributbasierten Zugriffssteuerung](../../../access-control/abac/end-to-end-guide.md)
* [Verwalten von Kennzeichnungen mithilfe der Benutzeroberfläche „Berechtigungen“](../../../access-control/abac/ui/labels.md)
* [Glossar der Datennutzungskennzeichnungen](../../../data-governance/labels/reference.md)

## Anwenden von Zugriffskennzeichnungen auf Quellen-Datenflüsse

>[!NOTE]
>
>* Sie können keine Kennzeichnungen auf eine Flussausführung anwenden. Flussausführungen übernehmen jedoch alle Beschriftungen, die Sie auf den übergeordneten Datenfluss anwenden.
>
>* Wenn Sie keinen Ansichtszugriff auf einen Datenfluss haben, können Sie auch die entsprechenden Flussausführungen nicht anzeigen.

Um Zugriffsbeschriftungen auf die Quelldatenflüsse anzuwenden, navigieren Sie zu **[!UICONTROL Quellen]** > **[!UICONTROL Datenflüsse]** und suchen Sie nach dem Datenfluss, den Sie aktualisieren möchten, und beschränken Sie den Benutzerzugriff darauf.

Klicken Sie als Nächstes auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und wählen Sie dann **[!UICONTROL Zugriffskennzeichnungen anwenden]** aus, um Kennzeichnungen für den ausgewählten Datenfluss hinzuzufügen und zu verwalten.

![Die Seite „Datenflüsse“ in Quellen, auf der die Option „Zugriffskennzeichnungen anwenden“ ausgewählt ist.](../../images/tutorials/labels/apply_access_labels.png)

Das Fenster [!UICONTROL Anwenden von Zugriffs- und Data Governance]Kennzeichnungen“ wird angezeigt. Verwenden Sie dieses Fenster, um die Kennzeichnungen auszuwählen, die Sie auf Ihren Datenfluss anwenden möchten. Sie können Kennzeichnungen auch nach ihrem Typ filtern. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Das Fenster mit den Data Governance-Beschriftungen, wobei die C2-Beschriftung ausgewählt ist.](../../images/tutorials/labels/labels_window.png)

Nachdem Sie Zugriffsbeschriftungen für Ihren Datenfluss erfolgreich konfiguriert haben, können Benutzer, die keinen Zugriff auf diese Beschriftung haben, den Datenfluss nicht mehr abrufen. Sie können auch die Spalte [!UICONTROL Zugriffsbeschriftungen] verwenden, um die Beschriftungen anzuzeigen, die auf einen bestimmten Datenfluss angewendet werden.

## Nächste Schritte

Sie wissen jetzt, wie Sie Zugriffsbeschriftungen auf Ihre Quelldatenflüsse anwenden. Sie können jetzt sicherstellen, dass nur eine bestimmte Benutzergruppe in Ihrer Organisation auf bestimmte Datenflüsse für Quellen zugreifen kann. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [Anwenden von Zugriffskennzeichnungen auf Datenflüsse von Quellen in der API](../api/labels.md)
* [Zugriffskontrolle – Übersicht](../../../access-control/home.md)
