---
keywords: Experience Platform;Home;beliebte Themen;Marketo-Quellanschluss;Marketo-Anschluss;Marketo-Quelle;Marketo
solution: Experience Platform
title: Erstellen eines Marketo Engage-Quellconnectors in der Benutzeroberfläche
topic: overview
type: Tutorial
description: In diesem Lernprogramm wird beschrieben, wie Sie einen Marketo Engage-Quellanschluss in der Benutzeroberfläche erstellen, um B2B-Daten in Adobe Experience Platform zu importieren.
translation-type: tm+mt
source-git-commit: 5d4d88f88ab184c679a4cf425283a71983c929f3
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 4%

---


# (Beta) Erstellen Sie einen [!DNL Marketo Engage]-Quellanschluss in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die [!DNL Marketo Engage]-Quelle befindet sich derzeit in der Betaphase. Die Funktion und Dokumentation werden geändert. Darüber hinaus müssen Sie sicherstellen, dass Sie eine Nicht-Produktions-Sandbox verwenden, wenn Sie den Connector während des Beta-Programms verwenden. Weitere Informationen zu Sandboxen finden Sie in der [Sandboxdokumentation](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=en#understanding-sandboxes).

In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Marketo Engage] (nachfolgend als &quot;[!DNL Marketo]&quot;bezeichnet) Quell-Connectors in der Benutzeroberfläche beschrieben, um Verbraucherdaten in Adobe Experience Platform zu bringen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Erlebnisdatenmodell (XDM)](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Erstellen und bearbeiten Sie Schemas in der Benutzeroberfläche](../../../../../xdm/ui/resources/schemas.md): Erfahren Sie, wie Sie Schema in der Benutzeroberfläche erstellen und bearbeiten.
* [Identitäts-Namensraum](../../../../../identity-service/namespaces.md): Identitäts-Namensraum sind Bestandteile,  [!DNL Identity Service] die als Indikatoren für den Kontext dienen, auf den sich eine Identität bezieht. Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Erforderliche Anmeldedaten sammeln

Um auf Ihr [!DNL Marketo]-Konto auf Plattform zugreifen zu können, müssen Sie die folgenden Werte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `munchkinId` | Die Munchkin-ID ist die eindeutige Kennung für eine bestimmte [!DNL Marketo]-Instanz. |
| `clientId` | Die eindeutige Client-ID Ihrer [!DNL Marketo]-Instanz. |
| `clientSecret` | Das eindeutige Clientgeheimnis Ihrer [!DNL Marketo]-Instanz. |

Weitere Informationen zum Abrufen dieser Werte finden Sie im [[!DNL Marketo] Authentifizierungshandbuch](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die Schritte im nächsten Abschnitt aus.

## Verbinden Sie Ihr [!DNL Marketo]-Konto

Wählen Sie in der Benutzeroberfläche &quot;Plattform&quot;in der linken Navigationsleiste **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Adobe applications] **[!UICONTROL Marketo Engage]**. Wählen Sie dann **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL Marketo]-Datendurchlauf zu erstellen.

![Katalog](../../../../images/tutorials/create/marketo/catalog.png)

Die Seite **[!UICONTROL Mit Marketo Engage verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder ein neues Konto verwenden oder auf ein vorhandenes Konto zugreifen.

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabeformular einen Kontonamen, eine optionale Beschreibung und Ihre [!DNL Marketo]-Authentifizierungsdaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und lassen Sie dann etwas Zeit für die Einrichtung der neuen Verbindung zu.

![new-account](../../../../images/tutorials/create/marketo/new.png)

### Vorhandenes Konto

Um einen Datenflug mit einem vorhandenen Konto zu erstellen, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das [!DNL Marketo]-Konto, das Sie verwenden möchten. Wählen Sie **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/marketo/existing.png)

## Datensatz auswählen

Nachdem Sie Ihr [!DNL Marketo]-Konto erstellt haben, bietet der nächste Schritt eine Oberfläche, über die Sie [!DNL Marketo]-Datensätze untersuchen können.

Die linke Hälfte der Oberfläche ist ein Ordnerbrowser, der die 10 [!DNL Marketo]-Datensätze anzeigt. Eine vollständig funktionierende [!DNL Marketo]-Quellverbindung erfordert die Erfassung der neun verschiedenen Datensätze. Wenn Sie auch die Funktion [!DNL Marketo's] Kontobasiertes Marketing (ABM) verwenden, müssen Sie auch einen 10. Datenfeed erstellen, um den Datensatz [!UICONTROL Benannte Konten] zu erfassen.

>[!NOTE]
>
>Aus Gründen der Kürze wird im folgenden Lernprogramm [!UICONTROL Benannte Konten] als Beispiel verwendet, aber die unten beschriebenen Schritte gelten für alle 10 [!DNL Marketo]-Datensätze.

Wählen Sie zuerst den Datensatz aus, den Sie erfassen möchten, und wählen Sie dann **[!UICONTROL Weiter]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt [!UICONTROL Zuordnung] wird angezeigt und stellt eine Schnittstelle bereit, um den [!DNL Marketo]-Datensatz einem Platform-Datensatz zuzuordnen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen.

### Vorhandenen Datensatz verwenden

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandenen Datensatz verwenden]** und klicken Sie dann auf das Dataset-Symbol.

![existing-dataset](../../../../images/tutorials/create/marketo/existing-dataset.png)

Das Dialogfeld **[!UICONTROL Datensatz auswählen]** wird angezeigt. Suchen Sie den Datensatz mit dem gewünschten Schema, wählen Sie ihn aus und klicken Sie dann auf **[!UICONTROL Bestätigen]**.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### Verwenden eines neuen Datensatzes

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuen Datensatz erstellen]** und geben Sie in die entsprechenden Felder einen Namen und eine Beschreibung für den Datensatz ein.

Sie können nach einem Schema suchen, indem Sie dessen Namen in die Suchleiste **[!UICONTROL Schema auswählen]** eingeben. Sie können auch das Dropdownsymbol auswählen, um eine Liste der vorhandenen Schema anzuzeigen. Alternativ können Sie **[!UICONTROL Erweiterte Suche]** auswählen, um die Seite der vorhandenen Schema mit den entsprechenden Details aufzurufen.

Schalten Sie die Schaltfläche **[!UICONTROL Profil-Datensatz]** um, um Ihren Zielgruppen-Datensatz für [!DNL Profile] zu aktivieren, sodass Sie eine ganzheitliche Ansicht der Attribute und Verhaltensweisen einer Entität erstellen können. Daten aus allen [!DNL Profile]-aktivierten Datensätzen werden in [!DNL Profile] eingeschlossen und Änderungen werden angewendet, wenn Sie Ihren Datendurchlauf speichern.

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

Nachdem Sie ein Schema ausgewählt haben, blättern Sie nach unten, um das Zuordnungsdialogfeld mit dem Beginn zu Ansicht zu verschieben, der Ihre [!DNL Marketo] Dataset-Felder den entsprechenden XDM-Feldern der Zielgruppe zuordnet.

### Ordnen Sie Ihre [!DNL Marketo]-Datenquellenfelder den XDM-Feldern der Zielgruppe zu.

Jeder [!DNL Marketo]-Datensatz verfügt über eigene spezifische Zuordnungsregeln. Weitere Informationen zum Zuordnen von [!DNL Marketo]-Datensätzen zu XDM finden Sie unter:

* [Aktivitäten](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programme](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Mitgliedschaft in Programmen](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Unternehmen](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Statische Listen](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Mitgliedschaft in statischen Listen](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Benannte Konten](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Chancen](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Kontaktrollen bei Chancen](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personen](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Wählen Sie **[!UICONTROL Vorschau data]** aus, um die Zuordnungsergebnisse basierend auf Ihrem ausgewählten Datensatz anzuzeigen.

![zuordnen](../../../../images/tutorials/create/marketo/mapping.png)

Das [!UICONTROL Vorschau]-Popup bietet eine Schnittstelle, um die Zuordnungsergebnisse von bis zu 100 Zeilen mit Musterdaten aus dem ausgewählten Datensatz zu untersuchen.

![Vorschau](../../../../images/tutorials/create/marketo/mapping-preview.png)

Sobald die Quellfelder den entsprechenden Feldern der Zielgruppe zugeordnet sind, wählen Sie **[!UICONTROL Schließen]**.

## Datenflussinformationen bereitstellen

Der Schritt [!UICONTROL Datenfelddetails] wird angezeigt, mit dem Sie einen Namen und eine kurze Beschreibung Ihres neuen Datenflusses angeben können.

![dataflow-detail](../../../../images/tutorials/create/marketo/dataflow-detail.png)

Aktivieren Sie den Umschalter **[!UICONTROL Fehlerdiagnose]**, um die Generierung einer detaillierten Fehlermeldung für neu eingefügte Stapel zuzulassen, die Sie mit der API herunterladen können.

![Fehler](../../../../images/tutorials/create/marketo/errors.png)

Der [!DNL Marketo]-Connector verwendet die Stapelverarbeitung, um alle historischen Datensätze zu erfassen, und verwendet die Streaming-Erfassung für Echtzeitaktualisierungen. Dadurch kann der Connector das Streaming fortsetzen, während falsche Datensätze aufgenommen werden. Aktivieren Sie den Umschalter **[!UICONTROL Partielle Erfassung]** und setzen Sie dann den Schwellenwert [!UICONTROL Fehler %] auf Maximum, um zu verhindern, dass der Datendurchlauf fehlschlägt.

**[!UICONTROL Die teilweise]** Erfassung bietet die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Weitere Informationen finden Sie unter [Übersicht über die teilweise Stapelverarbeitung](../../../../../ingestion/batch-ingestion/partial.md).

Nachdem Sie die Datenflug-Details angegeben und den Fehlerschwellenwert auf max gesetzt haben, wählen Sie **[!UICONTROL Weiter]**.

![teilweise Aufnahme](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## Überprüfen Sie Ihren Datenfluss

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* **[!UICONTROL Zuweisen von Dataset- und Zuordnungsfeldern]**: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.

Nachdem Sie den Datenfluss überprüft haben, wählen Sie **[!UICONTROL Fertig stellen]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses zu.

![überprüfen](../../../../images/tutorials/create/marketo/review.png)

## Überwachen des Datenflusses

Nachdem Sie Ihren Datenbogen erstellt haben, können Sie die Daten überwachen, die über ihn erfasst werden, um Informationen zu Erfassungsraten, Erfolgen und Fehlern anzuzeigen. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Lernprogramm zu [Überwachungsdataflows in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

## Attribute löschen

Benutzerdefinierte Attribute in Datasets können nicht nachträglich ausgeblendet oder entfernt werden. Wenn Sie ein benutzerdefiniertes Attribut aus einem vorhandenen Datensatz ausblenden oder entfernen möchten, müssen Sie einen neuen Datensatz ohne dieses benutzerdefinierte Attribut erstellen, ein neues XDM-Schema erstellen und einen neuen Datendurchlauf für das neu erstellte Dataset konfigurieren. Sie müssen auch den ursprünglichen Datenfluss deaktivieren oder löschen, der aus dem Datensatz mit dem benutzerdefinierten Attribut besteht, das Sie ausblenden oder entfernen möchten.

## Datenflug löschen

Sie können Datenflüsse löschen, die nicht mehr benötigt werden oder mit der Funktion **[!UICONTROL Delete]**, die im Arbeitsbereich [!UICONTROL Datenflüsse] verfügbar ist, falsch erstellt wurden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Lernprogramm zum [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um [!DNL Marketo]-Daten einzufügen. Eingehende Daten können jetzt von nachgeschalteten Plattformdiensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] Übersicht](../../../../profile/home.md)
* [[!DNL Data Science Workspace] Übersicht](../../../../data-science-workspace/home.md)
