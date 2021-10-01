---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Klasse; Klassen;
solution: Experience Platform
title: Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Klassen in der Benutzeroberfläche von Experience Platform erstellen und bearbeiten.
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 5%

---

# Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) definieren Klassen die verhaltensbezogenen Aspekte der Daten, die ein Schema enthalten wird (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemas, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Adobe bietet mehrere Standard-XDM-Klassen (&quot;Core&quot;), darunter [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent]. Zusätzlich zu diesen Core-Klassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihr Unternehmen zu beschreiben.

Dieses Dokument bietet einen Überblick darüber, wie Sie benutzerdefinierte Klassen in der Adobe Experience Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis des XDM-Systems voraus. Eine Einführung in die Rolle von XDM im Experience Platform-Ökosystem finden Sie in der [XDM-Übersicht](../../home.md) und den [Grundlagen der Schemakomposition](../../schema/composition.md) , um zu erfahren, wie Klassen zu XDM-Schemas beitragen.

Für dieses Handbuch ist zwar nicht erforderlich, Sie sollten jedoch auch das Tutorial zum Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.[

## Neue Klasse erstellen {#create}

Wählen Sie im Arbeitsbereich **[!UICONTROL Schemas]** die Option **[!UICONTROL Schema erstellen]** und dann **[!UICONTROL Durchsuchen]** aus der Dropdown-Liste.

![](../../images/ui/resources/classes/browse-classes.png)

Es wird ein Dialogfeld angezeigt, in dem Sie aus einer Liste verfügbarer Klassen auswählen können. Wählen Sie oben im Dialogfeld **[!UICONTROL Neue Klasse erstellen]** aus. Anschließend können Sie Ihrer neuen Klasse einen Anzeigenamen (einen kurzen, beschreibenden, eindeutigen und benutzerfreundlichen Namen für die Klasse), eine Beschreibung und ein Verhalten für die Daten geben, die das Schema definieren wird (&quot;[!UICONTROL Record]&quot; oder &quot;[!UICONTROL Zeitreihen]&quot;).

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Klasse zuweisen]** aus.

![](../../images/ui/resources/classes/class-details.png)

Das [!DNL Schema Editor] wird angezeigt und zeigt ein neues Schema auf der Arbeitsfläche an, das auf der soeben erstellten benutzerdefinierten Klasse basiert. Da der Klasse noch keine Felder hinzugefügt wurden, enthält das Schema nur ein `_id` -Feld, das die systemgenerierte eindeutige Kennung darstellt, die automatisch auf alle Ressourcen in [!DNL Schema Registry] angewendet wird.

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Denken Sie beim Erstellen eines Schemas, das eine von Ihrem Unternehmen definierte Klasse implementiert, daran, dass Schemafeldgruppen nur für kompatible Klassen verfügbar sind. Da die von Ihnen definierte Klasse neu ist, sind keine kompatiblen Feldergruppen im Dialogfeld **[!UICONTROL Feldergruppe hinzufügen]** aufgeführt. Stattdessen müssen Sie [neue Feldergruppen](./field-groups.md#create) für die Verwendung mit dieser Klasse erstellen. Wenn Sie das nächste Mal ein Schema erstellen, das die neue Klasse implementiert, werden die von Ihnen definierten Feldergruppen aufgelistet und zur Verwendung verfügbar.

Sie können [jetzt mit dem Hinzufügen von Feldern zur Klasse](#add-fields) beginnen, die von allen Schemas gemeinsam genutzt wird, die die Klasse verwenden.

## Vorhandene Klasse bearbeiten {#edit}

>[!NOTE]
>
>Nur benutzerdefinierte Klassen, die von Ihrem Unternehmen definiert wurden, können vollständig bearbeitet und angepasst werden. Für von Adobe definierte Hauptklassen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schemas bearbeitet werden. Weitere Informationen finden Sie im Abschnitt [Bearbeiten von Anzeigenamen für Schemafelder](./schemas.md#display-names) .
>
>Sobald eine benutzerdefinierte Klasse gespeichert und bei der Datenerfassung verwendet wurde, können danach nur noch additive Änderungen daran vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schemaentwicklung](../../schema/composition.md#evolution) .

Um eine vorhandene Klasse zu bearbeiten, wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** und dann den Namen eines Schemas aus, das die Klasse verwendet, die Sie bearbeiten möchten.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Sie können die Such- und Filterfunktionen des Arbeitsbereichs verwenden, um das Schema leichter zu finden. Weitere Informationen finden Sie im Handbuch [Erkunden von XDM-Ressourcen](../explore.md) .

Der [!DNL Schema Editor] wird angezeigt, wobei die Struktur des Schemas auf der Arbeitsfläche angezeigt wird. Jetzt können Sie [Felder zur Klasse](#add-fields) hinzufügen.

![](../../images/ui/resources/classes/edit.png)

## Felder zu einer Klasse hinzufügen {#add-fields}

Sobald Sie über ein Schema verfügen, das eine benutzerdefinierte Klasse verwendet, die im [!UICONTROL Schema-Editor] geöffnet ist, können Sie damit beginnen, der Klasse Felder hinzuzufügen. Um ein neues Feld hinzuzufügen, wählen Sie das Symbol **plus (+)** neben dem Namen des Schemas aus.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Beachten Sie, dass alle Felder, die Sie zu einer Klasse hinzufügen, in allen Schemas verwendet werden, die diese Klasse verwenden. Daher sollten Sie sorgfältig überlegen, welche Felder in allen Anwendungsfällen des Schemas nützlich sein werden. Wenn Sie erwägen, ein Feld hinzuzufügen, das möglicherweise nur in einigen Schemas unter dieser Klasse verwendet wird, sollten Sie es diesen Schemas hinzufügen, indem Sie stattdessen [eine Feldergruppe](./field-groups.md#create) erstellen.

Ein **[!UICONTROL Neues Feld]** wird auf der Arbeitsfläche angezeigt und die rechte Leiste aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Spezifische Schritte zum Konfigurieren und Hinzufügen des Felds zur Klasse finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define) .

Fügen Sie der Klasse weiterhin beliebig viele Felder hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Save]** aus, um sowohl das Schema als auch die Klasse zu speichern.

![](../../images/ui/resources/classes/save.png)

Wenn Sie zuvor Schemas erstellt haben, die diese Klasse verwenden, werden die neu hinzugefügten Felder automatisch in diesen Schemata angezeigt.

## Klasse eines Schemas ändern {#schema}

Sie können die Klasse des Schemas jederzeit während des anfänglichen Erstellungsprozesses ändern, bevor es gespeichert wurde. Weitere Informationen finden Sie im Handbuch zum Erstellen und Bearbeiten von Schemas](./schemas.md#change-class).[

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Klassen mithilfe der Platform-Benutzeroberfläche erstellt und bearbeitet werden. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schemas] finden Sie unter [[!UICONTROL Schemas] Workspace - Übersicht](../overview.md).

Informationen zum Verwalten von Klassen mithilfe der [!DNL Schema Registry]-API finden Sie im [Klassen-Endpunkthandbuch](../../api/classes.md).
