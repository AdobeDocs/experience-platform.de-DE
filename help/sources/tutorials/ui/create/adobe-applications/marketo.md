---
keywords: Experience Platform;Startseite;beliebte Themen;Marketo-Quell-Connector;Marketo-Connector;Marketo-Quelle;Marketo
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Marketo Engage über die Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für Marketo Engage über die Benutzeroberfläche beschrieben, um B2B-Daten in Adobe Experience Platform zu importieren.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 72fb25a262d2ab76085f12e3ad0c6a8decba50ac
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 92%

---

# Erstellen eines Quell-Connectors für [!DNL Marketo Engage] über die Benutzeroberfläche

>[!IMPORTANT]
>
>Vor der Erstellung [!DNL Marketo Engage] Quellverbindung und einen Datenfluss müssen Sie zunächst sicherstellen, dass Sie [Ihrer Adobe IMS-Organisations-ID zugeordnet](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html?lang=en) in [!DNL Marketo]. Außerdem müssen Sie sicherstellen, dass Sie [automatisch Ihre [!DNL Marketo] B2B-Namespaces und -Schemata](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) vor der Erstellung einer Quellverbindung und eines Datenflusses.

In diesem Tutorial erfahren Sie, wie Sie einen [!DNL Marketo Engage]-Quell-Connector (im Folgenden als „[!DNL Marketo]“ abgekürzt) in der Benutzeroberfläche erstellen, um B2B-Daten in Adobe Experience Platform einzubringen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [B2B-Namespaces und Dienstprogramm zur automatischen Schemaerstellung](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Mithilfe der B2B-Namespaces und des Dienstprogramm zur automatischen Schemaerstellung können Sie [!DNL Postman] , um automatisch Werte für Ihre B2B-Namespaces und -Schemas zu generieren. Sie müssen zuerst Ihre B2B-Namespaces und -Schemas abschließen, bevor Sie eine [!DNL Marketo] Quellverbindung und Datenfluss.
* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Experience-Datenmodell (XDM)](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](../../../../../xdm/ui/resources/schemas.md): Erfahren Sie, wie Sie in der Benutzeroberfläche Schemata erstellen und bearbeiten.
* [Identitäts-Namespaces](../../../../../identity-service/namespaces.md): Identitäts-Namespaces sind eine Komponente von [!DNL Identity Service], die als Indikatoren für den Kontext dienen, auf den sich eine Identität bezieht. Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace.
* [[!DNL Real-time Customer Profile]](/help/profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihr [!DNL Marketo]-Konto in Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `munchkinId` | Die Munchkin-ID ist die eindeutige Kennung für eine bestimmte [!DNL Marketo]-Instanz. |
| `clientId` | Die eindeutige Client-ID Ihrer [!DNL Marketo]-Instanz. |
| `clientSecret` | Das eindeutige Client-Geheimnis Ihrer [!DNL Marketo]-Instanz. |

Weitere Informationen darüber, wie Sie diese Werte erhalten, finden Sie im [[!DNL Marketo] Authentifizierungshandbuch](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die Schritte im nächsten Abschnitt ausführen.

## Verbinden Ihres [!DNL Marketo]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Adobe-Programme] die Option **[!UICONTROL Marketo Engage]**. Wählen Sie dann **[!UICONTROL Daten hinzufügen]**, um einen neuen [!DNL Marketo]-Datenfluss zu erstellen.

![Katalog](../../../../images/tutorials/create/marketo/catalog.png)

Die Seite **[!UICONTROL Marketo Engage-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder ein neues Konto verwenden oder auf ein vorhandenes Konto zugreifen.

### Vorhandenes Konto

Um einen Datenfluss mit einem bestehenden Konto zu erstellen, klicken Sie auf **[!UICONTROL Bestehendes Konto]** und wählen Sie dann das [!DNL Marketo]-Konto aus, das Sie verwenden möchten. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/marketo/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im angezeigten Eingabeformular einen Kontonamen, eine optionale Beschreibung und Ihre [!DNL Marketo]-Authentifizierungsdaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/marketo/new.png)

## Auswählen eines Datensatzes

Nachdem Sie Ihr [!DNL Marketo]-Konto erstellt haben, können Sie im nächsten Schritt [!DNL Marketo]-Datensätze untersuchen.

Die linke Hälfte der Schnittstelle ist ein Verzeichnis-Browser, der die zehn [!DNL Marketo]-Datensätze anzeigt. Eine voll funktionsfähige [!DNL Marketo]-Quellverbindung erfordert das Aufnehmen der neun verschiedenen Datensätze. Wenn Sie außerdem die Funktion Account-Based Marketing (ABM) von [!DNL Marketo] verwenden, müssen Sie auch einen zehnten Datenfluss erstellen, um den Datensatz [!UICONTROL Benannte Konten] aufzunehmen.

>[!NOTE]
>
>Der Kürze halber wird im folgenden Tutorial [!UICONTROL Opportunities] als Beispiel verwendet, aber die unten beschriebenen Schritte gelten für jeden der zehn [!DNL Marketo]-Datensätze.

Wählen Sie den Datensatz aus, den Sie als Erstes aufnehmen möchten, und wählen Sie dann **[!UICONTROL Weiter]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Angeben von Datenflussdetails

Auf der Seite [!UICONTROL Datenflussdetails] können Sie auswählen, ob Sie einen vorhandenen Datensatz oder einen neuen Datensatz verwenden möchten. Während dieses Vorgangs können Sie auch Einstellungen für [!UICONTROL Profildatensatz], [!UICONTROL Fehlerdiagnose], [!UICONTROL Partielle Aufnahme] und [!UICONTROL Warnhinweise] vornehmen.

![dataflow-details](../../../../images/tutorials/create/marketo/dataflow-details.png)

### Verwenden eines vorhandenen Datensatzes

Um Daten in einen vorhandenen Datensatz aufzunehmen, wählen Sie **[!UICONTROL Vorhandener Datensatz]**. Sie können einen vorhandenen Datensatz entweder über die Option [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Datensätze im Dropdown-Menü abrufen. Nachdem Sie einen Datensatz ausgewählt haben, geben Sie einen Namen und eine Beschreibung für Ihren Datenfluss ein.

![existing-dataset](../../../../images/tutorials/create/marketo/existing-dataset.png)

### Verwenden eines neuen Datensatzes

Für ein Aufnehmen in einen neuen Datensatz wählen Sie **[!UICONTROL Neuer Datensatz]** aus und geben Sie einen Namen für den Ausgabedatensatz und eine optionale Beschreibung an. Wählen Sie als Nächstes mithilfe der Option [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Schemata im Dropdown-Menü ein Schema zum Zuordnen aus. Nachdem Sie ein Schema ausgewählt haben, geben Sie einen Namen und eine Beschreibung für Ihren Datenfluss ein.

![new-dataset](../../../../images/tutorials/create/marketo/new-dataset.png)

### Aktivieren von [!DNL Profile] und Fehlerdiagnose

Wählen Sie als Nächstes den **[!UICONTROL Profildatensatz]**-Umschalter aus, um Ihren Datensatz für [!DNL Profile] zu aktivieren. Auf diese Weise können Sie eine ganzheitliche Ansicht der Attribute und Verhaltensweisen einer Entität erstellen. Daten aus allen [!DNL Profile]-aktivierten Datensätzen werden in [!DNL Profile] eingeschlossen und Änderungen werden wirksam, wenn Sie Ihren Datenfluss speichern.

[!UICONTROL Fehlerdiagnose] ermöglicht eine detaillierte Erstellung von Fehlermeldungen für alle fehlerhaften Datensätze, die in Ihrem Datenfluss auftreten, während [!UICONTROL Partielle Aufnahme] die Aufnahme von fehlerhaften Daten bis zu einem gewissen Schwellenwert, den Sie manuell definieren, ermöglicht. Weitere Informationen finden Sie in der [Übersicht zur partiellen Batch-Aufnahme](../../../../../ingestion/batch-ingestion/partial.md).

>[!IMPORTANT]
>
>Der [!DNL Marketo]-Connector verwendet die Batch-Aufnahme, um alle historischen Datensätze aufzunehmen, und verwendet die Streaming-Aufnahme für Echtzeit-Aktualisierungen. Dadurch kann der Connector bei einer Aufnahme fehlerhafter Datensätze das Streaming fortsetzen. Aktivieren Sie den Umschalter **[!UICONTROL Teilweise Aufnahme]** und setzen Sie dann [!UICONTROL Fehler-Schwellenwert %] auf Maximum, um ein Fehlschlagen des Datenflusses zu verhindern.

![profile-and-errors](../../../../images/tutorials/create/marketo/profile-and-errors.png)

### Aktivieren von Warnhinweisen

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status Ihres Datenflusses zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Quellen über die Benutzeroberfläche](../../alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihren Datenfluss fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

![alerts](../../../../images/tutorials/create/marketo/alerts.png)

## Zuordnen Ihrer [!DNL Marketo]-Datensatz-Quellfelder zu XDM-Zielfeldern

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Für jeden Datensatz des Typs [!DNL Marketo] gibt es eigene spezifische Zuordnungsregeln, die befolgt werden müssen. Weitere Informationen dazu, wie Sie [!DNL Marketo]-Datensätze XDM zuordnen, finden Sie nachstehend:

* [Aktivitäten](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programme](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Programmmitgliedschaften](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Firmen](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Statische Listen](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Mitgliedschaften in statischen Listen](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Benannte Konten](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Opportunities](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Rollen von Kontakten bei Opportunities](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personen](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

![mapping](../../../../images/tutorials/create/marketo/mapping.png)

Wenn Ihre Mapping-Sets fertig sind, klicken Sie auf **[!UICONTROL Weiter]** und warten Sie einige Augenblicke, während der neue Datenfluss hergestellt wird.

## Überprüfen des Datenflusses

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quellentität und die Anzahl der Spalten innerhalb dieser Quellentität an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, wählen Sie **[!UICONTROL Speichern und Aufnehmen]** und gewähren Sie etwas Zeit für die Herstellung des Datenflusses.

![review](../../../../images/tutorials/create/marketo/review.png)

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss hergestellt worden ist, können Sie Daten, die dadurch aufgenommen werden, überwachen, um Informationen zu Aufnahmegeschwindigkeiten, Erfolg und Fehlern zu erhalten. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial zum [Überwachen von Datenflüssen in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

## Löschen Ihrer Attribute

Benutzerdefinierte Attribute in Datensätzen können nicht rückwirkend ausgeblendet oder entfernt werden. Wenn Sie ein benutzerdefiniertes Attribut aus einem vorhandenen Datensatz ausblenden oder entfernen möchten, müssen Sie einen neuen Datensatz ohne dieses benutzerdefinierte Attribut sowie ein neues XDM-Schema erstellen und für den neuen Datensatz, den Sie erstellen, einen neuen Datenfluss konfigurieren. Außerdem müssen Sie den ursprünglichen Datenfluss deaktivieren oder löschen, der aus dem Datensatz mit dem benutzerdefinierten Attribut besteht, das Sie ausblenden oder entfernen möchten.

## Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich [!UICONTROL Datenflüsse] verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).

## Nächste Schritte

Nach dem Vorbild dieses Tutorials haben Sie erfolgreich einen Datenfluss erstellt, um [!DNL Marketo]-Daten einzubringen. Eingehende Daten können jetzt von nachgelagerten Platform-Services wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] – Übersicht](/help/profile/home.md)
* [[!DNL Data Science Workspace] – Übersicht](/help/data-science-workspace/home.md)
