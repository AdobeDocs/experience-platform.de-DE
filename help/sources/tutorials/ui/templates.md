---
keywords: Experience Platform;Startseite;beliebte Themen;
description: Adobe Experience Platform stellt vorkonfigurierte Vorlagen bereit, mit denen Sie den Datenerfassungsprozess beschleunigen können. Zu Vorlagen gehören automatisch generierte Assets wie Schemas, Datensätze, Zuordnungsregeln, Identitäts-Namespaces und Datenflüsse, die Sie beim Einbringen von Daten aus einer Quelle in eine Experience Platform verwenden können.
title: (Alpha) Erstellen Sie einen Datenfluss für Quellen mithilfe von Vorlagen in der Benutzeroberfläche
hide: true
hidefromtoc: true
source-git-commit: a0ca9cff43b6f8276268467fecf944c664992950
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 14%

---

# (Alpha) Erstellen Sie einen Datenfluss für Quellen mithilfe von Vorlagen in der Benutzeroberfläche

>[!IMPORTANT]
>
>Vorlagen befinden sich in Alpha und werden derzeit nur von der [[!DNL Marketo Engage] source](../../connectors/adobe-applications/marketo/marketo.md). Die Dokumentation und Funktionen können sich ändern.

Adobe Experience Platform stellt vorkonfigurierte Vorlagen bereit, mit denen Sie den Datenerfassungsprozess beschleunigen können. Zu Vorlagen gehören automatisch generierte Assets wie Schemas, Datensätze, Zuordnungsregeln, Identitäts-Namespaces und Datenflüsse, die Sie beim Einbringen von Daten aus einer Quelle in eine Experience Platform verwenden können.

Mit Vorlagen können Sie:

* Verringern Sie die Zeit bis zum Wert der Erfassung durch Beschleunigung der ML-basierten Asset-Erstellung.
* Minimieren Sie Fehler, die während der manuellen Datenerfassung auftreten können.
* Aktualisieren Sie automatisch generierte Assets zu jedem Zeitpunkt entsprechend Ihren Anwendungsfällen.

Das folgende Tutorial enthält Schritte zur Verwendung von Vorlagen in der Platform-Benutzeroberfläche mithilfe der [[!DNL Marketo Engage] source](../../connectors/adobe-applications/marketo/marketo.md).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Verwenden von Vorlagen in der Platform-Benutzeroberfläche {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Geschäftstyp auswählen"
>abstract="Wählen Sie den entsprechenden Geschäftstyp für Ihren Anwendungsfall aus. Ihr Zugriff variiert je nach Ihrem Real-time Customer Data Platform-Abonnementkonto."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=de" text="Übersicht über Real-Time CDP"

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, die zum Erstellen eines Kontos verwendet werden können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Unter dem [!UICONTROL Adobe Apps] category, select **[!UICONTROL Marketo Engage]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Ein Katalog des Quellarbeitsbereichs mit hervorgehobener Marketo Engage-Quelle.](../../images/tutorials/templates/catalog.png)

Es wird ein Popup-Fenster angezeigt, in dem Sie die Möglichkeit haben, Vorlagen zu durchsuchen oder vorhandene Schemata und Datensätze zu verwenden. Um automatisch generierte Assets zu verwenden, wählen Sie **[!UICONTROL Vorlagen durchsuchen]** und wählen Sie **[!UICONTROL Auswählen]**.

![Ein Popup-Fenster mit Optionen zum Durchsuchen von Vorlagen oder Verwenden vorhandener Assets.](../../images/tutorials/templates/browse-templates.png)

### Authentifizierung

Der Authentifizierungsschritt wird angezeigt und Sie werden aufgefordert, entweder ein neues Konto zu erstellen oder ein vorhandenes Konto zu verwenden.

#### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie [!UICONTROL Vorhandenes Konto] und wählen Sie dann das Konto, das Sie verwenden möchten, aus der angezeigten Liste aus.

![Die Auswahlseite für ein vorhandenes Konto mit einer Liste vorhandener Konten, auf die Sie zugreifen können.](../../images/tutorials/templates/existing-account.png)

#### Neues Konto

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann Ihre Details zur Quellverbindung und Anmeldedaten für die Kontoauthentifizierung an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]** und einige Zeit für die Einrichtung der neuen Verbindung.

![Die Authentifizierungsseite für ein neues Konto mit Details zur Quellverbindung und Anmeldeinformationen zur Kontoauthentifizierung.](../../images/tutorials/templates/new-account.png)

### Vorlagen auswählen

Nachdem Sie sich authentifiziert und Ihr Konto ausgewählt haben, wird eine Liste mit Vorlagen angezeigt. Wählen Sie das Vorschausymbol neben einem Vorlagennamen aus, um eine Vorschau der Beispieldaten aus der Vorlage anzuzeigen.

![Eine Liste von Vorlagen mit hervorgehobenem Vorschausymbol.](../../images/tutorials/templates/templates.png)

Das Vorschaufenster wird angezeigt, in dem Sie Beispieldaten aus Ihrer Vorlage analysieren und überprüfen können. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Got it]**.

![Das Fenster mit Beispieldaten für die Vorschau.](../../images/tutorials/templates/preview-sample-data.png)

Wählen Sie anschließend aus der Liste die Vorlage aus, die Sie verwenden möchten. Sie können mehrere Vorlagen auswählen und mehrere Datenflüsse gleichzeitig erstellen. Eine Vorlage kann jedoch nur einmal pro Konto verwendet werden. Nachdem Sie Ihre Vorlagen ausgewählt haben, wählen Sie **[!UICONTROL Beenden]** und lassen Sie einige Momente zu, in denen die Assets generiert werden.

![Die Liste der Vorlagen mit der ausgewählten Vorlage Kontaktrolle für Chancen .](../../images/tutorials/templates/select-template.png)

### Überprüfen von Assets {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Überprüfen der automatisch generierten Assets"
>abstract="Die Generierung aller Assets kann bis zu fünf Minuten dauern. Wenn Sie die Seite verlassen möchten, erhalten Sie eine Benachrichtigung, die zurückgegeben wird, sobald die Assets abgeschlossen sind. Sie können die Assets überprüfen, sobald sie generiert wurden, und jederzeit zusätzliche Konfigurationen an Ihrem Datenfluss vornehmen."

Die [!UICONTROL Vorlagen-Assets überprüfen] -Seite zeigt die Assets an, die automatisch als Teil Ihrer Vorlage generiert wurden. Auf dieser Seite können Sie die automatisch generierten Schemas, Datensätze, Identitäts-Namespaces und Datenflüsse anzeigen, die mit Ihrer Quellverbindung verknüpft sind.

Automatisch generierte Datenflüsse sind standardmäßig aktiviert. Wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Datenflusses und wählen Sie dann **[!UICONTROL Zuordnungen in der Vorschau anzeigen]** um die für Ihren Datenfluss erstellten Zuordnungssätze anzuzeigen.

![Ein Dropdown-Fenster mit ausgewählter Vorschauzuordnungsoption.](../../images/tutorials/templates/preview.png)

Eine Vorschauseite wird angezeigt, auf der Sie die Zuordnungsbeziehung zwischen Ihren Quelldatenfeldern und den Zielschemafeldern überprüfen können. Nachdem Sie die Zuordnungen Ihres Datenflusses angezeigt haben. Auswählen **[!UICONTROL Verstand es.]**

![Das Zuordnungsvorschaufenster.](../../images/tutorials/templates/preview-mappings.png)

Sie können Ihre Datenflüsse jederzeit nach der Ausführung aktualisieren. Wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Datenflusses und wählen Sie dann **[!UICONTROL Aktualisieren des Datenflusses]**. Sie gelangen auf die Seite mit dem Quellen-Workflow , auf der Sie Ihre Datenflussdetails aktualisieren können, einschließlich der Einstellungen für die partielle Erfassung, Fehlerdiagnose und Warnbenachrichtigungen sowie der Zuordnung Ihres Datenflusses.

![Ein Dropdown-Fenster mit aktivierter Option Datenfluss aktualisieren .](../../images/tutorials/templates/update.png)

## Nächste Schritte

In diesem Tutorial haben Sie jetzt Datenflüsse sowie Assets wie Schemas, Datensätze und Identitäts-Namespaces mit Vorlagen erstellt. Allgemeine Informationen zu Quellen finden Sie unter [Quellen - Übersicht](../../home.md).