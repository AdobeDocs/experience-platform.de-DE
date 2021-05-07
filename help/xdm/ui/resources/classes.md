---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;XDM-System;Erlebnisdatenmodell;Datenmodell;ui;Workspace;class;Klassen;
solution: Experience Platform
title: Klassen in der Benutzeroberfläche erstellen und bearbeiten
description: Erfahren Sie, wie Sie Klassen in der Benutzeroberfläche "Experience Platform"erstellen und bearbeiten.
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 5%

---

# Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche

Im Erlebnis-Datenmodell (XDM) definieren Klassen die Verhaltensaspekte der Daten, die ein Schema enthalten soll (Datensatz oder Zeitreihen). Darüber hinaus beschreiben Klassen die kleinste Anzahl gemeinsamer Eigenschaften, die alle Schemas, die auf dieser Klasse basieren, beinhalten müssen, und bieten eine Möglichkeit zum Zusammenführen mehrerer kompatibler Datensätze.

Adobe bietet mehrere Standard- (&quot;Core&quot;) XDM-Klassen, einschließlich [!DNL XDM Individual Profile] und [!DNL XDM ExperienceEvent]. Zusätzlich zu diesen Hauptklassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihr Unternehmen zu beschreiben.

In diesem Dokument wird beschrieben, wie Sie benutzerdefinierte Klassen in der Adobe Experience Platform-Benutzeroberfläche erstellen, bearbeiten und verwalten.

## Voraussetzungen 

Dieses Handbuch erfordert ein funktionierendes Verständnis des XDM-Systems. In der [XDM-Übersicht](../../home.md) finden Sie eine Einführung zur Rolle von XDM im Experience Platform-Ökosystem und in den [Grundlagen der Schema-Komposition](../../schema/composition.md), um zu erfahren, wie Klassen zu XDM-Schemas beitragen.

Es wird empfohlen, das Tutorial zum [Erstellen eines Schemas in der Benutzeroberfläche](../../tutorials/create-schema-ui.md) zu befolgen, um sich mit den verschiedenen Funktionen von [!DNL Schema Editor] vertraut zu machen.

## Neue Klasse erstellen {#create}

Wählen Sie im Arbeitsbereich **[!UICONTROL Schemas]** **[!UICONTROL Schema erstellen]** und wählen Sie dann **[!UICONTROL Durchsuchen]** aus der Dropdownliste.

![](../../images/ui/resources/classes/browse-classes.png)

Es wird ein Dialogfeld angezeigt, in dem Sie aus einer Liste verfügbarer Klassen auswählen können. Wählen Sie oben im Dialogfeld **[!UICONTROL Neue Klasse erstellen]**. Anschließend können Sie der neuen Klasse einen Anzeigenamen (einen kurzen, beschreibenden, eindeutigen und benutzerfreundlichen Klassennamen), eine Beschreibung und ein Verhalten für die Daten geben, die vom Schema definiert werden (&quot;[!UICONTROL Record]&quot;oder &quot;[!UICONTROL Zeitreihen]&quot;).

Wählen Sie **[!UICONTROL Klasse zuweisen]** aus, wenn Sie fertig sind.

![](../../images/ui/resources/classes/class-details.png)

Das Symbol [!DNL Schema Editor] wird angezeigt und zeigt ein neues Schema auf der Arbeitsfläche, das auf der soeben erstellten benutzerspezifischen Klasse basiert. Da der Klasse noch keine Felder hinzugefügt wurden, enthält das Schema nur das Feld `_id`, das den systemgenerierten eindeutigen Bezeichner darstellt, der automatisch auf alle Ressourcen in [!DNL Schema Registry] angewendet wird.

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Denken Sie beim Erstellen eines Schemas, das eine von Ihrem Unternehmen definierte Klasse implementiert, daran, dass Schema-Feldgruppen nur mit kompatiblen Klassen verwendet werden können. Da die von Ihnen definierte Klasse neu ist, sind keine kompatiblen Feldgruppen im Dialogfeld **[!UICONTROL Hinzufügen Feldgruppe]** aufgeführt. Stattdessen müssen Sie [neue Feldgruppen](./field-groups.md#create) erstellen, um sie mit dieser Klasse zu verwenden. Wenn Sie das nächste Mal ein Schema erstellen, das die neue Klasse implementiert, werden die von Ihnen definierten Feldgruppen aufgelistet und zur Verwendung verfügbar.

Sie können nun Beginn [hinzufügen, die der Klasse](#add-fields) hinzugefügt werden. Diese Felder werden von allen Schemas freigegeben, die die Klasse verwenden.

## Bearbeiten einer vorhandenen Klasse {#edit}

>[!NOTE]
>
>Nur benutzerdefinierte Klassen, die von Ihrem Unternehmen definiert wurden, können vollständig bearbeitet und angepasst werden. Bei von der Adobe definierten Hauptklassen können nur die Anzeigenamen für ihre Felder im Kontext einzelner Schema bearbeitet werden. Weitere Informationen finden Sie im Abschnitt [Bearbeiten von Anzeigenamen für Schema-Felder](./schemas.md#display-names).
>
>Nachdem eine benutzerspezifische Klasse gespeichert und bei der Datenerfassung verwendet wurde, können danach nur noch zusätzliche Änderungen daran vorgenommen werden. Weitere Informationen finden Sie unter [Regeln der Schema-Evolution](../../schema/composition.md#evolution).

Um eine vorhandene Klasse zu bearbeiten, wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** und wählen Sie dann den Namen des Schemas aus, das die zu bearbeitende Klasse verwendet.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Sie können die Such- und Filterfunktionen des Arbeitsbereichs verwenden, um das Schema leichter zu finden. Weitere Informationen finden Sie im Handbuch [XDM-Ressourcen](../explore.md) zu erkunden.

Das [!DNL Schema Editor] wird angezeigt, wobei die Struktur des Schemas auf der Arbeitsfläche angezeigt wird. Sie können nun Beginn [Hinzufügen von Feldern zur Klasse](#add-fields) hinzufügen.

![](../../images/ui/resources/classes/edit.png)

## hinzufügen von Feldern zu einer Klasse {#add-fields}

Wenn Sie ein Schema haben, das eine benutzerdefinierte Klasse verwendet, und im [!UICONTROL Schema-Editor] geöffnet sind, können Sie Beginn zum Hinzufügen von Feldern zur Klasse hinzufügen. Um ein neues Feld hinzuzufügen, wählen Sie das Symbol **plus (+)** neben dem Namen des Schemas aus.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Denken Sie daran, dass alle Felder, die Sie einer Klasse hinzufügen, in allen Schemas verwendet werden, die diese Klasse verwenden. Daher sollten Sie sorgfältig überlegen, welche Schemas in allen Anwendungsfällen nützlich sein werden. Wenn Sie überlegen, ein Feld hinzuzufügen, das möglicherweise nur in einigen Schemas unter dieser Klasse verwendet wird, sollten Sie es diesen Schemas hinzufügen, indem Sie stattdessen [eine Feldgruppe](./field-groups.md#create) erstellen.

Ein **[!UICONTROL Neues Feld]** wird auf der Arbeitsfläche angezeigt und die rechte Leiste wird aktualisiert, um Steuerelemente zum Konfigurieren der Feldeigenschaften anzuzeigen. Genaue Schritte zum Konfigurieren und Hinzufügen des Felds zur Klasse finden Sie im Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../fields/overview.md#define).

Fügen Sie der Klasse weiterhin so viele Felder wie erforderlich hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]**, um sowohl das Schema als auch die Klasse zu speichern.

![](../../images/ui/resources/classes/save.png)

Wenn Sie zuvor Schema erstellt haben, die diese Klasse verwenden, werden die neu hinzugefügten Felder automatisch in diesen Schemas angezeigt.

## Klasse eines Schemas ändern {#schema}

Sie können die Klasse des Schemas jederzeit während des ersten Erstellungsprozesses ändern, bevor es gespeichert wurde. Weitere Informationen finden Sie im Handbuch [Erstellen und Bearbeiten von Schemas](./schemas.md#change-class).

## Nächste Schritte

In diesem Dokument wurde das Erstellen und Bearbeiten von Klassen mithilfe der Plattform-Benutzeroberfläche behandelt. Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schema] finden Sie unter [[!UICONTROL Schema] Arbeitsbereichsübersicht](../overview.md).

Informationen zum Verwalten von Klassen mithilfe der API finden Sie im [Klassen-Endpunktleitfaden](../../api/classes.md).[!DNL Schema Registry]
