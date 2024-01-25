---
title: Erstellen einer Marketo Engage-Quellverbindung und eines Datenflusses für benutzerdefinierte Aktivitätsdaten in der Benutzeroberfläche
description: In diesem Tutorial erfahren Sie, wie Sie in der Benutzeroberfläche eine Marketo Engage-Quellverbindung und einen Datenfluss erstellen, um benutzerdefinierte Aktivitätsdaten in Adobe Experience Platform zu importieren.
exl-id: 05a7b500-11d2-4d58-be43-a2c4c0ceeb87
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 22%

---

# Erstellen Sie eine [!DNL Marketo Engage] Quellverbindung und Datenfluss für benutzerdefinierte Aktivitätsdaten in der Benutzeroberfläche

>[!NOTE]
>
>In diesem Tutorial werden spezifische Schritte zum Einrichten und Einführen von **benutzerdefinierte Aktivität** Daten aus [!DNL Marketo] auf Experience Platform. Schritte zum **Standardaktivität** -Daten, lesen Sie die [[!DNL Marketo] UI-Handbuch](./marketo.md).

Zusätzlich zu [Standardaktivitäten](../../../../connectors/adobe-applications/mapping/marketo.md#activities), können Sie auch die [!DNL Marketo] -Quelle, um benutzerdefinierte Aktivitätsdaten an Adobe Experience Platform zu übertragen. In diesem Dokument wird beschrieben, wie Sie eine Quellverbindung und einen Datenfluss für benutzerdefinierte Aktivitätsdaten mit der [!DNL Marketo] -Quelle in der Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [B2B-Namespaces und Dienstprogramm zur automatischen Schemaerstellung](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Mithilfe der B2B-Namespaces und des Dienstprogramm zur automatischen Schemaerstellung können Sie [!DNL Postman] , um automatisch Werte für Ihre B2B-Namespaces und -Schemas zu generieren. Sie müssen zuerst Ihre B2B-Namespaces und -Schemas abschließen, bevor Sie eine [!DNL Marketo] Quellverbindung und Datenfluss.
* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Experience-Datenmodell (XDM)](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](../../../../../xdm/ui/resources/schemas.md): Erfahren Sie, wie Sie in der Benutzeroberfläche Schemata erstellen und bearbeiten.
* [Identitäts-Namespaces](../../../../../identity-service/features/namespaces.md): Identitäts-Namespaces sind eine Komponente von [!DNL Identity Service], die als Indikatoren für den Kontext dienen, auf den sich eine Identität bezieht. Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Abrufen Ihrer benutzerdefinierten Aktivitätsdetails

Der erste Schritt zum Abrufen benutzerdefinierter Aktivitätsdaten aus [!DNL Marketo] zum Experience Platform bezeichnet, um den API-Namen und den Anzeigenamen Ihrer benutzerdefinierten Aktivität abzurufen.

Melden Sie sich mit dem [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) -Schnittstelle. In der linken Navigation, unter [!DNL Database Management]auswählen **Benutzerdefinierte Marketo-Aktivitäten**.

Die Benutzeroberfläche aktualisiert eine Anzeige Ihrer benutzerdefinierten Aktivitäten, einschließlich Informationen zu ihren jeweiligen Anzeigenamen und API-Namen. Sie können auch die rechte Leiste verwenden, um andere benutzerdefinierte Aktivitäten aus Ihrem Konto auszuwählen und anzuzeigen.

![Die Benutzeroberfläche &quot;Benutzerdefinierte Aktivitäten&quot;in der Adobe Marketo Engage-Benutzeroberfläche.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

Auswählen **Felder** aus der oberen Kopfzeile, um die mit Ihrer benutzerdefinierten Aktivität verknüpften Felder anzuzeigen. Auf dieser Seite können Sie die Namen, API-Namen, Beschreibungen und Datentypen der Felder in Ihrer benutzerdefinierten Aktivität anzeigen. Details zu einzelnen Feldern werden in einem späteren Schritt bei der Erstellung eines Schemas verwendet.

![Die Seite &quot;Marketo Custom Activity Fields Details&quot;in der Marketo Engage-Benutzeroberfläche.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## Einrichten von Feldergruppen für benutzerdefinierte Aktivitäten im Schema B2B-Aktivitäten

Im *[!UICONTROL Schemas]* Dashboard der Experience Platform-Benutzeroberfläche auswählen **[!UICONTROL Durchsuchen]** und wählen Sie **[!UICONTROL B2B-Aktivität]** aus der Liste der Schemas.

>[!TIP]
>
>Verwenden Sie die Suchleiste, um die Navigation durch die Liste der Schemas zu beschleunigen.

![Der Arbeitsbereich &quot;Schemas&quot;in der Experience Platform-Benutzeroberfläche mit dem ausgewählten Schema &quot;B2B-Aktivität&quot;.](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### Neue Feldergruppe für benutzerdefinierte Aktivität erstellen

Fügen Sie als Nächstes eine neue Feldergruppe zum [!DNL B2B Activity] Schema. Diese Feldergruppe sollte mit der benutzerdefinierten Aktivität übereinstimmen, die Sie erfassen möchten, und den Anzeigenamen der benutzerdefinierten Aktivität verwenden, den Sie zuvor abgerufen haben.

Um eine neue Feldergruppe hinzuzufügen, wählen Sie **[!UICONTROL + Hinzufügen]** neben dem *[!UICONTROL Feldergruppen]* Bereich unter *[!UICONTROL Komposition]*.

![Die Schemastruktur.](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

Die *[!UICONTROL Feldergruppen hinzufügen]* angezeigt. Auswählen **[!UICONTROL Neue Feldergruppe erstellen]** Geben Sie dann denselben Anzeigenamen für die benutzerdefinierte Aktivität an, den Sie in einem früheren Schritt abgerufen haben, und geben Sie eine optionale Beschreibung für die neue Feldergruppe an. Wählen Sie zum Abschluss **[!UICONTROL Feldergruppen hinzufügen]**.

![Das Fenster zur Beschriftung und Erstellung einer neuen Feldergruppe.](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

Nach der Erstellung erscheint Ihre neue Feldergruppe für die benutzerdefinierte Aktivität im [!UICONTROL Feldergruppen] Katalog.

![Die Schemastruktur mit einer neuen Feldergruppe, die unter dem Feldergruppenbereich hinzugefügt wird.](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### Hinzufügen eines neuen Felds zur Schemastruktur

Fügen Sie Ihrem Schema als Nächstes ein neues Feld hinzu. Dieses neue Feld muss auf `type: object` und enthält die einzelnen Felder der benutzerdefinierten Aktivität.

Um ein neues Feld hinzuzufügen, wählen Sie das Pluszeichen (`+`) neben dem Schemanamen. Ein Eintrag für *[!UICONTROL Unbenanntes Feld | Typ]* angezeigt. Konfigurieren Sie anschließend die Eigenschaften Ihres Felds mithilfe des *[!UICONTROL Feldeigenschaften]* Bedienfeld. Legen Sie den Feldnamen als API-Namen Ihrer benutzerdefinierten Aktivität fest und legen Sie den Anzeigenamen als Anzeigenamen für Ihre benutzerdefinierte Aktivität fest. Legen Sie anschließend den Typ auf `object` und weisen Sie die Feldergruppe der benutzerdefinierten Feldergruppe zu, die Sie im vorherigen Schritt erstellt haben. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus.

![Die Schemastruktur mit dem Pluszeichen (`+`) ausgewählt, damit ein neues Feld hinzugefügt werden kann.](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

Das neue Feld wird in Ihrem Schema angezeigt.

![Ein neues Feld wurde zum Schema hinzugefügt.](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### Hinzufügen von Unterfeldern zum Objektfeld {#add-sub-fields-to-the-object-field}

Der letzte Schritt bei der Vorbereitung Ihres Schemas besteht darin, einzelne Felder in das Feld einzufügen, das Sie im vorherigen Schritt erstellt haben.

![Eine Gruppe von Unterfeldern, die einem Feld innerhalb des Schemas hinzugefügt werden.](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## Erstellen eines Datenflusses

Nach Abschluss der Schemaeinrichtung können Sie nun einen Datenfluss für Ihre benutzerdefinierten Aktivitätsdaten erstellen.

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Adobe-Programme] die Option **[!UICONTROL Marketo Engage]**. Wählen Sie dann **[!UICONTROL Daten hinzufügen]**, um einen neuen [!DNL Marketo]-Datenfluss zu erstellen.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten Marketo Engage-Quelle.](../../../../images/tutorials/create/marketo/catalog.png)

### Daten auswählen

Auswählen **[!UICONTROL Tätigkeiten]** aus der Liste der [!DNL Marketo] Datensätze und wählen Sie dann **[!UICONTROL Nächste]**.

![Der Schritt Daten auswählen im Ursprungs-Workflow mit dem ausgewählten Aktivitätendatensatz.](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### Datenflussdetails

Als Nächstes [Informationen für Ihren Datenfluss bereitstellen](./marketo.md#provide-dataflow-details), einschließlich der Namen und Beschreibungen für Ihren Datensatz und Ihren Datenfluss, des von Ihnen verwendeten Schemas und der Konfigurationen für [!DNL Profile] Erfassung, Fehlerdiagnose und partielle Erfassung.

![Der Schritt zum Datenfluss-Detail .](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### Zuordnung

Zuordnungen für Standard-Aktivitätsfelder werden automatisch ausgefüllt, benutzerdefinierte Aktivitätsfelder müssen jedoch manuell den entsprechenden Zielfeldern zugeordnet werden.

Um mit der Zuordnung Ihrer benutzerdefinierten Aktivitätsfelder zu beginnen, wählen Sie **[!UICONTROL Neuer Feldtyp]** und wählen Sie **[!UICONTROL Neues Feld hinzufügen]**.

![Der Zuordnungsschritt mit dem Dropdown-Menü, um ein neues Feld hinzuzufügen.](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

Navigieren Sie durch die Quelldatenstruktur und suchen Sie das benutzerdefinierte Aktivitätsfeld, das Sie erfassen möchten. Wählen Sie zum Abschluss **[!UICONTROL Auswählen]**.

>[!TIP]
>
>Um Verwirrung zu vermeiden und doppelte Feldnamen zu verarbeiten, wird benutzerdefinierten Aktivitätsfeldern der API-Name vorangestellt.

![Die Quelldatenstruktur.](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

Um ein Zielfeld hinzuzufügen, wählen Sie das Schemensymbol aus ![Schemasymbol](../../../../images/tutorials/create/marketo-custom-activities/schema-icon.png) und wählen Sie dann die benutzerdefinierten Aktivitätsfelder aus dem Zielschema aus.

![Die Struktur des Zielschemas.](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

Wiederholen Sie die Schritte, um den Rest der benutzerdefinierten Felder für die Aktivitätszuordnung hinzuzufügen. Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Alle Zuordnungen für Quell- und Zieldaten.](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### Überprüfung

Der Schritt *[!UICONTROL Überprüfung]* wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quellentität und die Anzahl der Spalten innerhalb dieser Quellentität an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, wählen Sie **[!UICONTROL Speichern und Aufnehmen]** und gewähren Sie etwas Zeit für die Herstellung des Datenflusses.

![Der letzte Schritt zur Überprüfung, der Informationen zu den Feldern für Verbindung, Datensatz und Zuordnung zusammenfasst.](../../../../images/tutorials/create/marketo-custom-activities/review.png)

### Hinzufügen benutzerdefinierter Aktivitäten zu einem vorhandenen Aktivitäten-Datenfluss {#add-to-existing-dataflows}

Um einem vorhandenen Datenfluss benutzerdefinierte Aktivitätsdaten hinzuzufügen, ändern Sie die Zuordnungen eines vorhandenen Aktivitäts-Datenflusses mit den benutzerdefinierten Aktivitätsdaten, die Sie erfassen möchten. Auf diese Weise können Sie benutzerdefinierte Aktivitäten in denselben vorhandenen Aktivitäts-Datensatz aufnehmen. Weitere Informationen zum Aktualisieren der Zuordnungen eines vorhandenen Datenflusses finden Sie im Handbuch unter [Aktualisieren von Datenflüssen in der Benutzeroberfläche](../../update-dataflows.md).

### Verwendung [!DNL Query Service] Filtern von Aktivitäten für benutzerdefinierte Aktivitäten {#query-service-filter}

Sobald Ihr Datenfluss abgeschlossen ist, können Sie [Query Service](../../../../../query-service/home.md) , um Aktivitäten nach Ihren benutzerdefinierten Aktivitätsdaten zu filtern.

Wenn benutzerdefinierte Aktivitäten in Platform erfasst werden, wird der API-Name der benutzerdefinierten Aktivität automatisch zu `eventType`. Verwendung `eventType={API_NAME}` , um nach benutzerdefinierten Aktivitätsdaten zu filtern.

```sql
SELECT * FROM with_custom_activities_ds_today WHERE eventType='aepCustomActivityDemo1' 
```

Verwenden Sie die `IN` -Klausel zum Filtern mehrerer benutzerdefinierter Aktivitäten:

```sql
SELECT * FROM $datasetName WHERE eventType='{API_NAME}'
SELECT * FROM $datasetName WHERE eventType IN ('aepCustomActivityDemo1', 'aepCustomActivityDemo2')
```

Die folgende Abbildung zeigt eine Beispiel-SQL-Anweisung im [Abfrage-Editor](../../../../../query-service/ui/user-guide.md) , das nach benutzerdefinierten Aktivitätsdaten filtert.

![Platform-Benutzeroberfläche mit einem Abfragebeispiel für benutzerdefinierte Aktivitäten.](../../../../images/tutorials/create/marketo-custom-activities/queries.png)

## Nächste Schritte

In diesem Tutorial haben Sie ein Platform-Schema für [!DNL Marketo] benutzerdefinierte Aktivitätsdaten und einen Datenfluss erstellt, um diese Daten an Platform zu übertragen. Allgemeine Informationen über [!DNL Marketo] -Quelle, lesen Sie die [[!DNL Marketo] Quellübersicht](../../../../connectors/adobe-applications/marketo/marketo.md).
