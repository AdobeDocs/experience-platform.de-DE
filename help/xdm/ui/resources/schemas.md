---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Schema; Schemas;
solution: Experience Platform
title: Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche
description: Lernen Sie die Grundlagen zum Erstellen und Bearbeiten von Schemas in der Benutzeroberfläche von Experience Platform kennen.
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 49a54b78d1e3745694352e779fb2226acd99d663
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche

Dieses Handbuch bietet einen Überblick darüber, wie Sie Experience-Datenmodell (XDM)-Schemas für Ihr Unternehmen in der Adobe Experience Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

>[!IMPORTANT]
>
>XDM-Schemata sind extrem anpassbar, sodass die Schritte zum Erstellen eines Schemas variieren können, je nachdem, welche Art von Daten das Schema erfassen soll. Daher behandelt dieses Dokument nur die grundlegenden Interaktionen, die Sie mit Schemas in der Benutzeroberfläche durchführen können, und schließt verwandte Schritte wie das Anpassen von Klassen, Schemafeldergruppen, Datentypen und Feldern aus.
>
>Eine vollständige Übersicht über den Schema-Erstellungsprozess erhalten Sie, wenn Sie mit dem [Tutorial zur Schemaerstellung](../../tutorials/create-schema-ui.md) , um ein vollständiges Beispielschema zu erstellen und sich mit den zahlreichen Funktionen der [!DNL Schema Editor].

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Siehe Abschnitt [XDM-Übersicht](../../home.md) für eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem und die [Grundlagen der Schemakomposition](../../schema/composition.md) für einen Überblick darüber, wie Schemas erstellt werden.

## Erstellen eines neuen Schemas {#create}

Im [!UICONTROL Schemas] Arbeitsbereich, wählen Sie **[!UICONTROL Schema erstellen]** in der oberen rechten Ecke. Im angezeigten Dropdown-Menü können Sie zwischen **[!UICONTROL XDM Individual Profile]** und **[!UICONTROL XDM ExperienceEvent]** als Basisklasse für das Schema. Alternativ können Sie **[!UICONTROL Durchsuchen]** aus der vollständigen Liste der verfügbaren Klassen auszuwählen oder [eine neue benutzerdefinierte Klasse erstellen](./classes.md#create) anstatt.

![](../../images/ui/resources/schemas/create-schema.png)

Sobald Sie eine Klasse auswählen, wird die [!DNL Schema Editor] angezeigt und die (von der Klasse bereitgestellte) Basisstruktur des Schemas wird auf der Arbeitsfläche angezeigt. Von hier aus können Sie die rechte Leiste verwenden, um eine **[!UICONTROL Anzeigename]** und **[!UICONTROL Beschreibung]** für das Schema.

![](../../images/ui/resources/schemas/schema-details.png)

Sie können jetzt mit der Erstellung der Schemastruktur beginnen, indem Sie [Schemafeldgruppen hinzufügen](#add-field-groups).

## Vorhandenes Schema bearbeiten {#edit}

>[!NOTE]
>
>Sobald ein Schema gespeichert und in der Datenerfassung verwendet wurde, können nur noch additive Änderungen daran vorgenommen werden. Siehe [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) für weitere Informationen.

Um ein vorhandenes Schema zu bearbeiten, wählen Sie die **[!UICONTROL Durchsuchen]** und wählen Sie dann den Namen des Schemas aus, das Sie bearbeiten möchten.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Sie können die Such- und Filterfunktionen des Arbeitsbereichs verwenden, um das Schema leichter zu finden. Siehe Handbuch unter [Erkunden von XDM-Ressourcen](../explore.md) für weitere Informationen.

Sobald Sie ein Schema auswählen, wird die [!DNL Schema Editor] angezeigt, wobei die Struktur des Schemas auf der Arbeitsfläche angezeigt wird. Sie können jetzt [Feldergruppen hinzufügen](#add-field-groups) zum Schema, [Anzeigenamen von Feldern bearbeiten](#display-names)oder [Bearbeiten vorhandener benutzerdefinierter Feldergruppen](./field-groups.md#edit) , wenn das Schema eine verwendet.

## Hinzufügen von Feldergruppen zu einem Schema {#add-field-groups}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie einem Schema vorhandene Feldergruppen hinzufügen. Wenn Sie eine neue benutzerdefinierte Feldergruppe erstellen möchten, lesen Sie das Handbuch unter [Erstellen und Bearbeiten von Feldergruppen](./field-groups.md#create) anstatt.

Nachdem Sie ein Schema im [!DNL Schema Editor]können Sie dem Schema mithilfe von Feldergruppen Felder hinzufügen. Wählen Sie zunächst **[!UICONTROL Hinzufügen]** neben **[!UICONTROL Feldergruppen]** in der linken Leiste.

![](../../images/ui/resources/schemas/add-field-group-button.png)

Es wird ein Dialogfeld mit einer Liste von Feldergruppen angezeigt, die Sie für das Schema auswählen können. Da Feldergruppen nur mit einer Klasse kompatibel sind, werden nur die Feldergruppen aufgelistet, die mit der ausgewählten Klasse des Schemas verknüpft sind. Standardmäßig werden die aufgelisteten Feldergruppen nach ihrer Nutzungspersönlichkeit in Ihrem Unternehmen sortiert.

![](../../images/ui/resources/schemas/field-group-popularity.png)

Wenn Sie die allgemeine Aktivität oder den Geschäftsbereich der Felder kennen, die Sie hinzufügen möchten, wählen Sie in der linken Leiste eine oder mehrere der vertikalen Industriekategorien aus, um die angezeigte Liste der Feldergruppen zu filtern.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Weitere Informationen zu Best Practices für branchenspezifische Datenmodellierung in XDM finden Sie in der Dokumentation zu [Branchendatenmodelle](../../schema/industries/overview.md).

Sie können auch die Suchleiste verwenden, um Ihre gewünschte Feldergruppe zu finden. Feldergruppen, deren Name mit der Abfrage übereinstimmt, werden oben in der Liste angezeigt. under **[!UICONTROL Standardfelder]**, werden Feldergruppen mit Feldern angezeigt, die die gewünschten Datenattribute beschreiben.

![](../../images/ui/resources/schemas/field-group-search.png)

Aktivieren Sie das Kontrollkästchen neben dem Namen der Feldergruppe, die Sie zum Schema hinzufügen möchten. Sie können mehrere Feldergruppen aus der Liste auswählen, wobei jede ausgewählte Feldergruppe in der rechten Leiste angezeigt wird.

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Für alle aufgelisteten Feldergruppen können Sie den Mauszeiger über das Informationssymbol (![](../../images/ui/resources/schemas/info-icon.png)), um eine kurze Beschreibung der Art der von der Feldergruppe erfassten Daten anzuzeigen. Sie können auch das Vorschausymbol (![](../../images/ui/resources/schemas/preview-icon.png)), um die Struktur der Felder anzuzeigen, die die Feldergruppe bereitstellt, bevor Sie sie zum Schema hinzufügen.

Nachdem Sie die Feldergruppen ausgewählt haben, wählen Sie **[!UICONTROL Feldergruppen hinzufügen]** , um sie dem Schema hinzuzufügen.

![](../../images/ui/resources/schemas/add-field-group-finish.png)

Die [!DNL Schema Editor] wird mit den von der Feldergruppe bereitgestellten Feldern auf der Arbeitsfläche erneut angezeigt.

![](../../images/ui/resources/schemas/field-groups-added.png)

## Aktivieren eines Schemas für das Echtzeit-Kundenprofil {#profile}

[Echtzeit-Kundenprofil](../../../profile/home.md) führt Daten aus unterschiedlichen Quellen zusammen, um eine vollständige Ansicht jedes einzelnen Kunden zu erhalten. Wenn die von einem Schema erfassten Daten an diesem Prozess teilnehmen sollen, müssen Sie das Schema zur Verwendung in [!DNL Profile].

>[!IMPORTANT]
>
>So aktivieren Sie ein Schema für [!DNL Profile]muss ein primäres Identitätsfeld definiert sein. Siehe Handbuch unter [Identitätsfelder definieren](../fields/identity.md) für weitere Informationen.

Um das Schema zu aktivieren, wählen Sie zunächst den Namen des Schemas in der linken Leiste aus und wählen Sie dann die **[!UICONTROL Profil]** in der rechten Leiste ein-/ausschalten.

![](../../images/ui/resources/schemas/profile-toggle.png)

Es wird ein Popup angezeigt, in dem Sie darauf hingewiesen werden, dass ein Schema nach seiner Aktivierung und Speicherung nicht mehr deaktiviert werden kann. Auswählen **[!UICONTROL Aktivieren]** , um fortzufahren.

![](../../images/ui/resources/schemas/profile-confirm.png)

Die Arbeitsfläche wird mit der [!UICONTROL Profil] Umschalten aktiviert.

>[!IMPORTANT]
>
>Da das Schema noch nicht gespeichert wurde, ist dies der Punkt, an dem es nicht zurückgegeben wird, wenn Sie Ihre Meinung ändern, das Schema im Echtzeit-Kundenprofil teilnehmen zu lassen: Wenn Sie ein aktiviertes Schema speichern, kann es nicht mehr deaktiviert werden. Wählen Sie die **[!UICONTROL Profil]** Schalten Sie erneut um, um das Schema zu deaktivieren.

Um den Prozess abzuschließen, wählen Sie **[!UICONTROL Speichern]** , um das Schema zu speichern.

![](../../images/ui/resources/schemas/profile-enabled.png)

Das Schema ist jetzt für die Verwendung im Echtzeit-Kundenprofil aktiviert. Wenn Platform Daten in Datensätze erfasst, die auf diesem Schema basieren, werden diese Daten in Ihre aggregierten Profildaten integriert.

## Anzeigenamen für Schemafelder bearbeiten {#display-names}

Nachdem Sie einem Schema eine Klasse zugewiesen und Feldergruppen hinzugefügt haben, können Sie die Anzeigenamen der Felder des Schemas bearbeiten, unabhängig davon, ob diese Felder von standardmäßigen oder benutzerdefinierten XDM-Ressourcen bereitgestellt wurden.

>[!NOTE]
>
>Beachten Sie, dass die Anzeigenamen von Feldern, die zu Standardklassen oder Feldgruppen gehören, nur im Kontext eines bestimmten Schemas bearbeitet werden können. Das heißt, dass eine Änderung des Anzeigenamens eines Standardfelds in einem Schema keine Auswirkungen auf andere Schemas hat, die dieselbe zugehörige Klasse oder Feldergruppe verwenden.
>
>Sobald Sie die Anzeigenamen für die Felder eines Schemas ändern, werden diese Änderungen sofort in allen vorhandenen Datensätzen übernommen, die auf diesem Schema basieren.

Um den Anzeigenamen eines Schemafelds zu bearbeiten, wählen Sie das Feld auf der Arbeitsfläche aus. Geben Sie in der rechten Leiste den neuen Namen unter ein. **[!UICONTROL Anzeigename]**.

![](../../images/ui/resources/schemas/display-name.png)

Auswählen **[!UICONTROL Anwenden]** in der rechten Leiste angezeigt wird, wird die Arbeitsfläche aktualisiert, um den neuen Anzeigenamen des Felds anzuzeigen. Auswählen **[!UICONTROL Speichern]** , um die Änderungen auf das Schema anzuwenden.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Klasse eines Schemas ändern {#change-class}

Sie können die Klasse eines Schemas jederzeit während des anfänglichen Kompositionsprozesses ändern, bevor das Schema gespeichert wurde.

>[!WARNING]
>
>Die Neuzuweisung der Klasse für ein Schema sollte mit äußerster Vorsicht erfolgen. Feldergruppen sind nur mit bestimmten Klassen kompatibel. Daher werden die Arbeitsfläche und alle von Ihnen hinzugefügten Felder durch Ändern der Klasse zurückgesetzt.

Um eine Klasse neu zuzuweisen, wählen Sie **[!UICONTROL Zuweisen]** auf der linken Seite der Arbeitsfläche.

![](../../images/ui/resources/schemas/assign-class-button.png)

Es wird ein Dialogfeld angezeigt, in dem eine Liste aller verfügbaren Klassen angezeigt wird, einschließlich aller von Ihrer Organisation definierten Klassen (der Inhaber ist der[!UICONTROL Kunde]&quot;) sowie durch die Adobe definierten Standardklassen.

Wählen Sie eine Klasse aus der Liste aus, um ihre Beschreibung auf der rechten Seite des Dialogfelds anzuzeigen. Sie können auch **[!UICONTROL Vorschau der Klassenstruktur]** , um die mit der Klasse verknüpften Felder und Metadaten anzuzeigen. Auswählen **[!UICONTROL Klasse zuweisen]** , um fortzufahren.

![](../../images/ui/resources/schemas/assign-class.png)

Es wird ein neues Dialogfeld geöffnet, in dem Sie aufgefordert werden zu bestätigen, dass Sie eine neue Klasse zuweisen möchten. Auswählen **[!UICONTROL Zuweisen]** zur Bestätigung.

![](../../images/ui/resources/schemas/assign-confirm.png)

Nach Bestätigung der Klassenänderung wird die Arbeitsfläche zurückgesetzt und der gesamte Kompositionsprozess geht verloren.

## Nächste Schritte

In diesem Dokument wurden die Grundlagen zum Erstellen und Bearbeiten von Schemas in der Platform-Benutzeroberfläche beschrieben. Es wird dringend empfohlen, die [Tutorial zur Schemaerstellung](../../tutorials/create-schema-ui.md) für einen umfassenden Workflow zum Erstellen eines vollständigen Schemas in der Benutzeroberfläche, einschließlich der Erstellung benutzerdefinierter Feldergruppen und Datentypen für eindeutige Anwendungsfälle.

Weitere Informationen zu den Funktionen der [!UICONTROL Schemas] Arbeitsbereich, siehe [[!UICONTROL Schemas] Arbeitsbereich - Übersicht](../overview.md).

Informationen zum Verwalten von Schemata finden Sie im Abschnitt [!DNL Schema Registry] API, siehe [Endpunktleitfaden für Schemata](../../api/schemas.md).
