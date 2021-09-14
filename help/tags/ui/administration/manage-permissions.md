---
title: Verwalten von Berechtigungen für Tags
description: Hier erfahren Sie, wie Sie in Adobe Experience Platform Berechtigungen für Tags erteilen.
source-git-commit: 72d2e9328bcfb6abf0a7f8f0c5113f021a112a35
workflow-type: ht
source-wordcount: '1054'
ht-degree: 100%

---

# Verwalten von Berechtigungen für Tags

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere Terminologieänderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Um Tags in Adobe Experience Platform verwenden zu können, muss Ihnen über Adobe Admin Console Zugriff auf mindestens ein Adobe Experience Cloud-Produkt gewährt werden. Darüber hinaus müssen Sie auch Berechtigungen für Tags auf der Ebene des Produktprofils besitzen, damit Sie bestimmte Aktionen ausführen können, wenn Sie über die Datenerfassungs-Benutzeroberfläche angemeldet sind.

In diesem Handbuch wird beschrieben, wie Sie diese Berechtigungen Benutzern gewähren, die Admin Console verwenden.

>[!NOTE]
>
>Ausführliche Informationen zu den verschiedenen in diesem Handbuch erwähnten Arten von verfügbaren Tag-Berechtigungen finden Sie in der [Übersicht über Benutzerberechtigungen](./user-permissions.md).

## Erhalten von Administratorrechten für ein Tags-Produktprofil

Um Benutzerberechtigungen für Tags zu verwalten, müssen Sie mindestens ein Produktprofiladministrator für Tags in Adobe Admin Console sein. Systemadministratoren und Produktadministratoren können auch Berechtigungen für ein Tags-Produktprofil verwalten.

Weitere Informationen zu den verschiedenen Administrationsebenen und zur Verwaltung dieser Rollen innerhalb Ihres Unternehmens finden Sie im Admin Console-Dokument zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/admin-guide.html/enterprise/using/admin-roles.ug.html).

## Auswählen eines Produktprofils, für das Berechtigungen verwaltet werden sollen

Sobald Sie über Administratorrechte verfügen, melden Sie sich bei Admin Console an und wählen Sie **[!UICONTROL Produkte]** aus der oberen Navigationsleiste aus. Wählen Sie aus der Liste der angezeigten Produkte **[!UICONTROL Adobe Experience Platform Launch]** aus.

![Produkt auswählen](../../images/ui/administration/manage-permissions/select-product.png)

Eine Liste mit Produktprofilen wird angezeigt. Ein Produktprofil ist ein Konstrukt, das eine Gruppe von Berechtigungen mit einer Benutzergruppe verknüpft. Von hier aus können Sie ein neues Profil erstellen, um es zu konfigurieren, oder Sie können ein vorhandenes Produktprofil aus der Liste zur Bearbeitung auswählen (vorausgesetzt, Sie verfügen über Administratorrechte für dieses Profil).

![Produktprofile](../../images/ui/administration/manage-permissions/product-profiles.png)

### Erstellen eines Produktprofils

>[!NOTE]
>
>Wenn Sie ein vorhandenes Profil zur Bearbeitung ausgewählt haben, fahren Sie mit dem [nächsten Abschnitt](#permissions) fort.

Wählen Sie **[!UICONTROL Neues Profil]** aus, um ein neues Produktprofil zu erstellen.

![Neues Profil](../../images/ui/administration/manage-permissions/new-profile-button.png)

Es wird ein Dialogfeld angezeigt, in dem Sie einen Namen und optional eine Beschreibung für das Profil angeben können. Sie können auch ein- oder ausschalten, ob Benutzer E-Mails erhalten sollen, wenn sie zu diesem Profil hinzugefügt oder daraus entfernt werden. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Profildetails](../../images/ui/administration/manage-permissions/profile-details.png)

## Konfigurieren von Berechtigungen für das Produktprofil {#permissions}

Die Detailseite für das Produktprofil wird angezeigt. Mithilfe der verfügbaren Registerkarten können Sie die dem Profil zugewiesenen Benutzer verwalten und die spezifischen Eigenschaften und Rechte konfigurieren, die das Profil diesen Benutzern gewährt.

Schritte zum Hinzufügen von Benutzern finden Sie [weiter unten in diesem Handbuch](#users). Wählen Sie zunächst **[!UICONTROL Berechtigungen]** aus.

![Profil-Landingpage](../../images/ui/administration/manage-permissions/profile-landing.png)

Der nächste Bildschirm zeigt einen Überblick über die Anzahl der Plattformen, Eigenschaften und Rechte, die dem Profil derzeit zugewiesen sind. Wählen Sie **[!UICONTROL Bearbeiten]** neben einer der Zeilen, um mit der Konfiguration der Profilberechtigungen zu beginnen.

![Berechtigungen](../../images/ui/administration/manage-permissions/edit-permissions.png)

Der Bildschirm [!UICONTROL Berechtigungen bearbeiten] wird angezeigt, über den Sie Berechtigungen zum Produktprofil hinzufügen und daraus entfernen können. Im Abschnitt **[!UICONTROL Plattformen]** können Sie sehen, dass standardmäßig alle Plattformen zum Profil hinzugefügt wurden.

![Plattformen](../../images/ui/administration/manage-permissions/platforms.png)

### Zuweisen von Eigenschaften

Um diesem Profil Eigenschaften zuzuweisen, wählen Sie im linken Navigationsbereich **[!UICONTROL Eigenschaften]** aus.

![Eigenschaften](../../images/ui/administration/manage-permissions/properties.png)

Standardmäßig erhält ein neues Produktprofil automatisch Zugriff auf alle Eigenschaften, die für Ihr Unternehmen verfügbar sind. Dazu gehören Eigenschaften, die aktuell verfügbar sind, sowie alle zukünftigen Eigenschaften.

Wenn Sie die verfügbaren Eigenschaften einschränken möchten, klicken Sie auf den Umschalter **[!UICONTROL Automatisch einschließen]**. Auf diese Weise können Sie je nach Bedarf Eigenschaften für die Eigenschaft manuell hinzufügen und entfernen.

![Automatisches Einschließen deaktiviert](../../images/ui/administration/manage-permissions/auto-include-off.png)

Wenn „Automatisch einfügen“ deaktiviert ist, werden alle zur Zeit verfügbaren Eigenschaften auf der linken Seite aufgeführt. Sie können Eigenschaften zum Profil hinzufügen, indem Sie in der linken Spalte das Pluszeichen (**+**) neben der betreffenden Eigenschaft auswählen. Um eine Eigenschaft zu entfernen, klicken Sie in der rechten Spalte auf das Symbol **X** neben der betreffenden Eigenschaft.

![Berechtigung hinzufügen und entfernen](../../images/ui/administration/manage-permissions/add-remove-permission.png)

>[!IMPORTANT]
>
>Wenn Sie die Funktion zum automatischen Einschließen deaktivieren, müssen alle in der Zukunft erstellten Eigenschaften manuell zum Produktprofil hinzugefügt werden, damit es Zugriff darauf erhält.

### Zuweisen von Rechten

Standardmäßig sind alle Rechte für ein Produktprofil deaktiviert und müssen manuell hinzugefügt werden, damit sie aktiviert werden können. Wenn Sie zu einem Produktprofil gehören, das Eigenschaften automatisch einschließt, aber keine Rechte hat, haben Sie nur Lesezugriff auf alle Eigenschaften.

>[!NOTE]
>
>Ein Benutzer kann in Admin Console mehreren Produktprofilen angehören, aber die Rechte aus diesen Profilen werden nicht in einem übergeordneten Berechtigungssatz zusammengefasst. Der Benutzer verfügt weiterhin nur über die explizit in den einzelnen Gruppen gewährten Rechte.
>
>Wenn Ihnen beispielsweise Gruppe 1 den Zugriff auf Eigenschaft A mit dem Recht „Entwickeln“ gewährt und Gruppe 2 Zugriff auf Eigenschaft B mit dem Recht „Veröffentlichen“, dann werden die Rechte „Entwickeln“ und „Veröffentlichen“ nicht für Eigenschaft A und B kombiniert. Sie können nur für Eigenschaft A entwickeln und für Eigenschaft B veröffentlichen.

Wählen Sie im linken Navigationsbereich **[!UICONTROL Eigenschaftsrechte]** aus. Wie bei Eigenschaften können Sie auf das Pluszeichen (**+**) neben einem Eigenschaftsrecht klicken, um es zum Profil hinzuzufügen. Wenn Sie dem Profil alle Eigenschaftsrechte hinzufügen möchten, können Sie auch **[!UICONTROL Alle hinzufügen]** auswählen.

![Eigenschaftsrechte](../../images/ui/administration/manage-permissions/property-rights.png)

Wählen Sie anschließend **[!UICONTROL Unternehmensrechte]** im linken Navigationsbereich aus. Fügen Sie die erforderlichen Rechte hinzu oder entfernen Sie sie. Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Speichern]**.

![Unternehmensrechte](../../images/ui/administration/manage-permissions/company-rights.png)

## Zuweisen von Benutzern zum Profil {#users}

Um dem Produktprofil Benutzer zuzuweisen, wählen Sie die Registerkarte [!UICONTROL Benutzer] und dann [!UICONTROL Benutzer hinzufügen] aus.

![Benutzer](../../images/ui/administration/manage-permissions/users.png)

Geben Sie im angezeigten Dialogfeld den Namen, die Benutzergruppe oder die E-Mail-Adressen der Benutzer ein, die Sie zum Profil hinzufügen möchten. Wenn ein Benutzer Teil Ihres Unternehmens ist, werden seine Informationen in einem Dropdown-Menü mit automatischer Vervollständigung angezeigt, welches Sie auswählen können, um die Details auszufüllen. Wenn er nicht Teil Ihrer Organisation ist, können Sie stattdessen seine Informationen manuell eingeben.

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Speichern]**, um die angegebenen Benutzer zum Produktprofil hinzuzufügen.

![Benutzer zuweisen](../../images/ui/administration/manage-permissions/assign-users.png)

Nachdem Benutzer zum Profil hinzugefügt wurden, erhalten sie eine E-Mail, in der sie darüber informiert werden, dass sie jetzt über Rechte für die Datenerfassungs-Benutzeroberfläche verfügen.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie mit Adobe Admin Console Eigenschaften und Rechte für die Datenerfassungs-Benutzeroberfläche verwalten. Weitere Informationen zu den verfügbaren Berechtigungen und den Funktionen, auf die sie Zugriff gewähren, finden Sie in der Übersicht zu [Benutzerberechtigungen](./user-permissions.md).
