---
keywords: Experience Platform; Startseite; beliebte Themen; Marketo-Quell-Connector; Marketo-Connector; Marketo-Quelle; Marketo
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Marketo Engage über die Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für Marketo Engage in der Benutzeroberfläche beschrieben, um B2B-Daten in Adobe Experience Platform zu importieren.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 0661d124ffe520697a1fc8e2cae7b0b61ef4edfc
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 6%

---

# (Beta) Erstellen eines Quell-Connectors [!DNL Marketo Engage] in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die Quelle [!DNL Marketo Engage] in Adobe Experience Platform befindet sich derzeit in der Betaphase. Dokumentation und Funktionalität können sich ändern.

In diesem Tutorial werden Schritte zum Erstellen eines Quell-Connectors für [!DNL Marketo Engage] (nachfolgend als &quot;[!DNL Marketo]&quot;bezeichnet) in der Benutzeroberfläche beschrieben, um B2B-Daten in Adobe Experience Platform zu importieren.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Experience-Datenmodell (XDM)](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Erstellen und bearbeiten Sie Schemata in der Benutzeroberfläche](../../../../../xdm/ui/resources/schemas.md): Erfahren Sie, wie Sie in der Benutzeroberfläche Schemas erstellen und bearbeiten.
* [Identitäts-Namespaces](../../../../../identity-service/namespaces.md): Identitäts-Namespaces sind eine Komponente von ,  [!DNL Identity Service] die als Indikatoren für den Kontext dient, auf den sich eine Identität bezieht. Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace.
* [[!DNL Real-time Customer Profile]](/help/profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Marketo]-Konto in Platform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `munchkinId` | Die Munchkin-ID ist die eindeutige Kennung für eine bestimmte [!DNL Marketo]-Instanz. |
| `clientId` | Die eindeutige Client-ID Ihrer [!DNL Marketo]-Instanz. |
| `clientSecret` | Das eindeutige Client-Geheimnis Ihrer [!DNL Marketo]-Instanz. |

Weiterführende Informationen zum Erwerb dieser Werte finden Sie im [[!DNL Marketo] Authentifizierungshandbuch](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die Schritte im nächsten Abschnitt ausführen.

## Ihr [!DNL Marketo]-Konto verbinden

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Adobe Applications] die Option **[!UICONTROL Marketo Engage]** aus. Wählen Sie dann **[!UICONTROL Daten hinzufügen]** aus, um einen neuen [!DNL Marketo]-Datenfluss zu erstellen.

![Katalog](../../../../images/tutorials/create/marketo/catalog.png)

Die Seite **[!UICONTROL Mit Marketo Engage verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder ein neues Konto verwenden oder auf ein vorhandenes Konto zugreifen.

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Kontonamen, eine optionale Beschreibung und Ihre [!DNL Marketo]-Authentifizierungsdaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** aus und lassen Sie dann etwas Zeit für die Einrichtung der neuen Verbindung zu.

![new-account](../../../../images/tutorials/create/marketo/new.png)

### Vorhandenes Konto

Um einen Datenfluss mit einem vorhandenen Konto zu erstellen, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das [!DNL Marketo]-Konto aus, das Sie verwenden möchten. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![vorhandene](../../../../images/tutorials/create/marketo/existing.png)

## Datensatz auswählen

Nachdem Sie Ihr [!DNL Marketo]-Konto erstellt haben, bietet der nächste Schritt eine Oberfläche zum Erkunden von [!DNL Marketo] -Datensätzen.

Die linke Hälfte der Oberfläche ist ein Verzeichnisbrowser, in dem die 10 [!DNL Marketo] Datensätze angezeigt werden. Eine voll funktionsfähige [!DNL Marketo] Quellverbindung erfordert die Aufnahme der neun verschiedenen Datensätze. Wenn Sie auch die Funktion [!DNL Marketo] Konto-basiertes Marketing (ABM) verwenden, müssen Sie auch einen 10. Datenfluss erstellen, um den Datensatz [!UICONTROL Spezifische Konten] zu erfassen.

>[!NOTE]
>
>Aus Gründen der Kürze wird im folgenden Tutorial [!UICONTROL Spezifische Konten] als Beispiel verwendet. Die unten beschriebenen Schritte gelten jedoch für alle 10 [!DNL Marketo]-Datensätze.

Wählen Sie zuerst den Datensatz aus, den Sie erfassen möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## [!DNL Marketo]-Schemata Platform zuordnen

Der Schritt [!UICONTROL Mapping] wird angezeigt und stellt eine Schnittstelle bereit, um [!DNL Marketo]-Schemas Platform zuzuordnen.

Wählen Sie einen Datensatz für eingehende Daten aus, die in aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen.

### Vorhandenen Datensatz verwenden

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandenen Datensatz]** und dann das Datensatzsymbol aus.

![existing-dataset](../../../../images/tutorials/create/marketo/existing-dataset.png)

Das Dialogfeld **[!UICONTROL Datensatz auswählen]** wird angezeigt. Suchen Sie den Datensatz mit dem entsprechenden Schema, das Sie verwenden möchten, wählen Sie ihn aus und wählen Sie dann **[!UICONTROL Bestätigen]** aus.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### Verwenden eines neuen Datensatzes

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuer Datensatz]** aus und geben Sie einen Namen und eine Beschreibung für den Datensatz in die bereitgestellten Felder ein.

Sie können nach einem Schema suchen, indem Sie dessen Namen in die Suchleiste **[!UICONTROL Schema auswählen]** eingeben. Sie können auch das Dropdown-Symbol auswählen, um eine Liste der vorhandenen Schemas anzuzeigen. Alternativ können Sie **[!UICONTROL Erweiterte Suche]** auswählen, um auf die Seite vorhandener Schemas mit ihren jeweiligen Details zuzugreifen.

Schalten Sie die Schaltfläche **[!UICONTROL Profildatensatz]** um, um Ihren Zieldatensatz für [!DNL Profile] zu aktivieren, sodass Sie eine ganzheitliche Ansicht der Attribute und Verhaltensweisen einer Entität erstellen können. Daten aus allen [!DNL Profile]-aktivierten Datensätzen werden in [!DNL Profile] einbezogen und Änderungen werden angewendet, wenn Sie Ihren Datenfluss speichern.

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

Nachdem Sie ein Schema ausgewählt haben, scrollen Sie nach unten, um das Zuordnungsdialogfeld anzuzeigen, um mit der Zuordnung Ihrer [!DNL Marketo]-Datensatzfelder zu den entsprechenden Ziel-XDM-Feldern zu beginnen.

### Ordnen Sie Ihre [!DNL Marketo] -Datensatzquellenfelder den XDM-Zielfeldern zu.

Jeder [!DNL Marketo]-Datensatz verfügt über eigene spezifische Zuordnungsregeln, die befolgt werden müssen. Weitere Informationen zum Zuordnen von [!DNL Marketo]-Datensätzen zu XDM finden Sie im Folgenden:

* [Aktivitäten](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programme](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Programmmitgliedschaften](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Firmen](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Statische Listen](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Mitgliedschaft in statischen Listen](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Spezifische Konten](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Chancen](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Kontaktrollen bei Chancen](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personen](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Wählen Sie **[!UICONTROL Vorschau der Daten]** aus, um die Zuordnungsergebnisse basierend auf Ihrem ausgewählten Datensatz anzuzeigen.

![Mapping](../../../../images/tutorials/create/marketo/mapping.png)

Das [!UICONTROL Vorschau]-Popup bietet Ihnen eine Schnittstelle zur Erforschung der Zuordnungsergebnisse von bis zu 100 Zeilen mit Beispieldaten aus dem ausgewählten Datensatz.

![Vorschau](../../../../images/tutorials/create/marketo/mapping-preview.png)

Nachdem die Quellfelder den entsprechenden Zielfeldern zugeordnet wurden, wählen Sie **[!UICONTROL Close]** aus.

## Datenflussdetails angeben

Der Schritt [!UICONTROL Datenfluss-Detail] wird angezeigt, mit dem Sie einen Namen und eine kurze Beschreibung zu Ihrem neuen Datenfluss angeben können.

![dataflow-detail](../../../../images/tutorials/create/marketo/dataflow-detail.png)

Aktivieren Sie den Umschalter **[!UICONTROL Fehlerdiagnose]** , um die detaillierte Generierung von Fehlermeldungen für neu aufgenommene Batches zu ermöglichen, die Sie über die API herunterladen können. Weitere Informationen finden Sie im Tutorial zum Abrufen der Fehlerdiagnose bei der Datenerfassung [a1/>.](../../../../../ingestion/quality/error-diagnostics.md)

![errors](../../../../images/tutorials/create/marketo/errors.png)

Der Connector [!DNL Marketo] verwendet die Batch-Erfassung, um alle historischen Datensätze zu erfassen, und verwendet die Streaming-Erfassung für Echtzeit-Aktualisierungen. Dadurch kann der Connector das Streaming fortsetzen, während er fehlerhafte Datensätze erfasst. Aktivieren Sie den Umschalter **[!UICONTROL Partielle Erfassung]** und setzen Sie dann den [!UICONTROL Fehlerschwellenwert %] auf &quot;Maximum&quot;, um zu verhindern, dass der Datenfluss fehlschlägt.

**[!UICONTROL Die partielle]** Erfassung bietet die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Weitere Informationen finden Sie unter [Übersicht über die partielle Batch-Erfassung](../../../../../ingestion/batch-ingestion/partial.md).

Nachdem Sie die Details des Datenflusses angegeben und den Fehlerschwellenwert auf max gesetzt haben, wählen Sie **[!UICONTROL Weiter]** aus.

![partielle Erfassung](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## Überprüfen Sie Ihren Datenfluss.

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie Ihren neuen Datenfluss überprüfen können, bevor er erstellt wird. Details werden in die folgenden Kategorien eingeteilt:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quellentität und die Anzahl der Spalten innerhalb dieser Quellentität an.
* **[!UICONTROL Zuweisen von Datensatz- und Zuordnungsfeldern]**: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, wählen Sie **[!UICONTROL Beenden]** aus und lassen Sie einige Zeit für die Erstellung des Datenflusses zu.

![Überprüfung](../../../../images/tutorials/create/marketo/review.png)

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die erfassten Daten überwachen, um Informationen zu Erfassungsraten, Erfolg und Fehlern zu erhalten. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial zum [Überwachen von Datenflüssen in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

## Attribute löschen

Benutzerdefinierte Attribute in Datensätzen können nicht rückwirkend ausgeblendet oder entfernt werden. Wenn Sie ein benutzerdefiniertes Attribut aus einem vorhandenen Datensatz ausblenden oder daraus entfernen möchten, müssen Sie einen neuen Datensatz ohne dieses benutzerdefinierte Attribut und ein neues XDM-Schema erstellen und einen neuen Datenfluss für den neuen Datensatz konfigurieren, den Sie erstellen. Sie müssen auch den ursprünglichen Datenfluss deaktivieren oder löschen, der aus dem Datensatz mit dem benutzerdefinierten Attribut besteht, das Sie ausblenden oder entfernen möchten.

## Datenfluss löschen

Sie können Datenflüsse löschen, die nicht mehr erforderlich sind oder falsch erstellt wurden, indem Sie die Funktion **[!UICONTROL Delete]** verwenden, die im Arbeitsbereich [!UICONTROL Datenflüsse] verfügbar ist. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial zum Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).[

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um [!DNL Marketo]-Daten einzubringen. Eingehende Daten können jetzt von nachgelagerten Platform-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] Übersicht](/help/profile/home.md)
* [[!DNL Data Science Workspace] Übersicht](/help/data-science-workspace/home.md)
