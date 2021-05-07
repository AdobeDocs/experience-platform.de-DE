---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: Konfigurieren eines Felds für berechnete Attribute
topic-legacy: guide
type: Documentation
description: Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene Aggregat werden. Um ein berechnetes Attribut zu konfigurieren, müssen Sie zunächst das Feld ermitteln, das den berechneten Attributwert enthält. Dieses Feld kann mithilfe einer Feldgruppe erstellt werden, um das Schema einem vorhandenen Schema hinzuzufügen, oder durch Auswahl eines Felds, das Sie bereits in einem Schema definiert haben.
translation-type: tm+mt
source-git-commit: 6e0f7578d0818f88e13b963f64cb2de6729f0574
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 41%

---


# (Alpha) Konfigurieren Sie ein Feld für ein berechnetes Attribut in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Um ein berechnetes Attribut zu konfigurieren, müssen Sie zunächst das Feld ermitteln, das den berechneten Attributwert enthält. Dieses Feld kann mithilfe einer Feldgruppe erstellt werden, um das Schema einem vorhandenen Schema hinzuzufügen, oder durch Auswahl eines Felds, das Sie bereits in einem Schema definiert haben.

>[!NOTE]
>
>Berechnete Attribute können nicht zu Feldern innerhalb von Adoben-definierten Feldgruppen hinzugefügt werden. Das Feld muss sich im `tenant`-Namespace befinden, d. h. es muss ein Feld sein, das Sie definieren und einem Schema hinzufügen.

Um ein berechnetes Attributfeld erfolgreich zu definieren, muss das Schema für [!DNL Profile] aktiviert sein und als Teil des Vereinigung-Schemas für die Klasse angezeigt werden, auf der das Schema basiert. Weitere Informationen zu [!DNL Profile]-aktivierten Schemas und Vereinigungen finden Sie im Abschnitt [!DNL Schema Registry] Entwicklerhandbuch unter [Aktivieren eines Schemas zum Profil und Anzeigen von Vereinigung-Schemas](../../xdm/api/getting-started.md). Außerdem empfehlen wir Ihnen, den [Abschnitt über Vereinigungen](../../xdm/schema/composition.md) in der Grundlagendokumentation zur Schemakomposition zu lesen.

Der Arbeitsablauf in diesem Lernprogramm verwendet ein [!DNL Profile]-aktiviertes Schema und führt die Schritte zum Definieren einer neuen Feldgruppe mit dem berechneten Attributfeld und zum Sicherstellen des richtigen Namensraums durch. Wenn Sie bereits über ein Feld verfügen, das sich in einem Profil-aktivierten Schema im richtigen Namespace befindet, können Sie direkt mit dem [Erstellen eines berechneten Attributs](#create-a-computed-attribute) fortfahren.

## Schema anzeigen

Die folgenden Schritte werden in der Adobe Experience Platform-Benutzeroberfläche ausgeführt, um ein Schema zu suchen, eine Feldgruppe hinzuzufügen und ein Feld zu definieren. Wenn Sie die API lieber verwenden möchten, lesen Sie das [Schema Registry-Entwicklerhandbuch](../../xdm/api/getting-started.md), um zu erfahren, wie Sie eine Feldgruppe erstellen, eine Feldgruppe zu einem Schema hinzufügen und ein Schema für [!DNL Real-time Customer Profile] aktivieren.[!DNL Schema Registry]

Klicken Sie in der Benutzeroberfläche in der linken Leiste auf **[!UICONTROL Schemas]** und nutzen Sie die Suchleiste auf dem Tab **[!UICONTROL Durchsuchen]**, um das Schema, das Sie aktualisieren möchten, zu suchen.

![](../images/computed-attributes/Schemas-Browse.png)

Nachdem Sie das Schema gefunden haben, klicken Sie auf seinen Namen, um das [!DNL Schema Editor] zu öffnen, in dem Sie Änderungen am Schema vornehmen können.

![](../images/computed-attributes/Schema-Editor.png)

## Erstellen einer Feldgruppe

Um eine neue Feldgruppe zu erstellen, klicken Sie auf **[!UICONTROL Hinzufügen]** neben **[!UICONTROL Feldgruppen]** im Abschnitt **[!UICONTROL Komposition]** links im Editor. Dadurch wird das Dialogfeld **[!UICONTROL Hinzufügen Feldgruppe]** geöffnet, in dem Sie die vorhandenen Feldgruppen sehen können. Klicken Sie auf das Optionsfeld für **[!UICONTROL Neue Feldgruppe]** erstellen, um Ihre neue Feldgruppe zu definieren.

Geben Sie der Feldgruppe einen Namen und eine Beschreibung ein und klicken Sie nach Abschluss auf **[!UICONTROL Hinzufügen Feldgruppe]**.

![](../images/computed-attributes/Add-field-group.png)

## Berechnetes Attributfeld für das Schema hinzufügen

Ihre neue Feldgruppe sollte nun im Abschnitt &quot;[!UICONTROL Feldgruppen]&quot;unter &quot;[!UICONTROL Zusammensetzung]&quot;angezeigt werden. Klicken Sie auf den Namen der Feldgruppe, und im Abschnitt **[!UICONTROL Struktur]** werden mehrere Schaltflächen **[!UICONTROL Hinzufügen Feld]** angezeigt.

Wählen Sie neben dem Namen des Schemas **[!UICONTROL Feld hinzufügen]**, um ein Feld der obersten Ebene hinzuzufügen. Alternativ können Sie das Feld an einer beliebigen Stelle im gewünschten Schema einfügen.

Nachdem Sie auf **[!UICONTROL Feld hinzufügen]** geklickt haben, wird ein neues Objekt mit dem Namen Ihrer Mandantenkennung geöffnet. Dies zeigt, dass sich das Feld im richtigen Namespace befindet. Innerhalb des Objekts wird ein **[!UICONTROL neues Feld]** angezeigt. Dies ist das Feld, in dem Sie das berechnete Attribut definieren werden.

![](../images/computed-attributes/New-field.png)

## Feld konfigurieren

Geben Sie im Abschnitt **[!UICONTROL Feldeigenschaften]** auf der rechten Seite des Editors die erforderlichen Daten für das neue Feld ein, einschließlich Name, Anzeigename und Typ.

>[!NOTE]
>
>Der Typ für das Feld muss mit dem Typ des berechneten Attributwerts übereinstimmen. Wenn der berechnete Attributwert beispielsweise eine Zeichenfolge ist, muss auch das im Schema definierte Feld eine Zeichenfolge sein.

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Übernehmen]**. Daraufhin werden der Name des Felds sowie der Typ im Abschnitt **[!UICONTROL Struktur]** des Editors angezeigt.

![](../images/computed-attributes/Apply.png)

## Schema für [!DNL Profile] aktivieren

Bevor Sie fortfahren, stellen Sie sicher, dass das Schema für [!DNL Profile] aktiviert wurde. Klicken Sie im Bereich **[!UICONTROL Struktur]** des Editors auf den Namen des Schemas, um den Tab **[!UICONTROL Schemaeigenschaften]** anzuzeigen. Wenn der Schieberegler **[!UICONTROL Profil]** blau ist, wurde das Schema für [!DNL Profile] aktiviert.

>[!NOTE]
>
>Die Aktivierung eines Schemas für [!DNL Profile] kann nicht rückgängig gemacht werden. Wenn Sie also auf den Schieberegler klicken, müssen Sie nicht riskieren, es zu deaktivieren.

![](../images/computed-attributes/Profile.png)

Jetzt können Sie auf **[!UICONTROL Speichern]** klicken, um das aktualisierte Schema zu speichern und mit dem Rest des Tutorials unter Nutzung der API fortzufahren.

## Nächste Schritte

Nachdem Sie ein Feld erstellt haben, in dem der berechnete Attributwert gespeichert wird, können Sie das berechnete Attribut mit dem API-Endpunkt `/computedattributes` erstellen. Ausführliche Anweisungen zum Erstellen eines berechneten Attributs in der API finden Sie in der Anleitung [API-Endpunkt für berechnete Attribute](ca-api.md).