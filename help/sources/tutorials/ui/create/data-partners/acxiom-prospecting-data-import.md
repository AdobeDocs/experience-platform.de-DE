---
title: Datenimport aus Acxiom Prospecting
description: Informationen dazu, wie Daten aus Acxiom Prospecting über die Benutzeroberfläche mit Adobe Experience Platform und Adobe Real-Time Customer Data Platform verbunden werden.
exl-id: cde0bfe9-0604-41d3-8422-114f58a74d04
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 14%

---

# Erstellen einer [!DNL Acxiom Prospecting Data Import] Quellverbindung und eines Datenflusses in der Benutzeroberfläche

Der Datenimport von [!DNL Acxiom] für Adobe Real-Time Customer Data Platform ist ein Prozess zur Bereitstellung der produktivsten potenziellen Zielgruppen. [!DNL Acxiom] nimmt First-Party-Daten von Real-Time CDP über einen sicheren Export und führt diese Daten über ein preisgekröntes Hygiene- und Identitätsauflösungssystem aus. Dadurch wird eine Datendatei erstellt, die als Unterdrückungsliste verwendet werden soll. Diese Datei wird dann mit der globalen Acxiom-Datenbank abgeglichen, sodass die Interessentenlisten für den Import maßgeschneidert werden können.

Sie können die [!DNL Acxiom]-Quelle verwenden, um Antworten vom Interessenten-Service Acxiom abzurufen und zuzuordnen, indem Sie Amazon S3 als Droppoint verwenden.

Lesen Sie dieses Tutorial, um zu erfahren, wie Sie mithilfe der Benutzeroberfläche von Adobe Experience Platform eine [!DNL Acxiom Prospecting Data Import]-Quellverbindung und einen Datenfluss erstellen.

## Voraussetzungen {#prerequisites}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Prospect Profile]](../../../../../profile/ui/prospect-profile.md): Erfahren Sie, wie Sie ein Interessentenprofil erstellen und verwenden, um mithilfe von Drittanbieterinformationen Informationen über unbekannte Kunden zu erfassen.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihren Bucket in Experience Platform zuzugreifen, müssen Sie gültige Werte für die folgenden Anmeldeinformationen angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| [!DNL Acxiom] Authentifizierungsschlüssel | Der Authentifizierungsschlüssel. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| [!DNL Amazon S3] Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Bucket. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| Geheimer [!DNL Amazon S3]-Schlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| Behältername | Dies ist der Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |

>[!IMPORTANT]
>
>Sie müssen sowohl **[!UICONTROL Quellen anzeigen]** als auch **[!UICONTROL Quellen verwalten]** für Ihr Konto aktiviert haben, um Ihr [!DNL Acxiom]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../../../access-control/ui/overview.md).

## Verbinden Ihres [!DNL Acxiom]-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Daten]** und Identitätspartner“ die Option **[!UICONTROL Datenimport für Interessenten von Acxiom]** und dann **[!UICONTROL Einrichten]**.

>[!TIP]
>
>Eine Quellkarte, auf der **[!UICONTROL Daten hinzufügen]** angezeigt wird, bedeutet, dass die Quelle bereits über ein authentifiziertes Konto verfügt. Andererseits bedeutet eine Quellkarte, die „Einrichten **[!UICONTROL anzeigt, dass]** Anmeldeinformationen angeben und ein neues Konto erstellen müssen, um diese Quelle verwenden zu können.

![Der Quellkatalog mit der ausgewählten Acxiom-Quelle.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-catalog.png)

### Neues Konto erstellen

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Eingabeformular einen Namen, eine optionale Beschreibung und Ihre [!DNL Acxiom] Anmeldeinformationen ein. Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]** und warten Sie dann einige Zeit, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle des Quell-Workflows.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-new-account.png)

| Anmeldedaten | Beschreibung |
| --- | --- |
| Kontoname | Der Name des Kontos. |
| Beschreibung | (Optional) Eine kurze Erläuterung des Zwecks des Kontos. |
| [!DNL Acxiom] Authentifizierungsschlüssel | Der von [!DNL Acxiom] bereitgestellte Schlüssel ist für die Kontogenehmigung erforderlich. Dieser muss mit dem richtigen Wert übereinstimmen, bevor eine Verbindung zur Datenbank hergestellt werden kann.  Dieser Schlüssel muss 24 Zeichen lang sein und darf nur die folgenden Zeichen enthalten: A-Z, a-z und 0-9. |
| S3 – Zugriffsschlüssel | Der S3-Zugriffsschlüssel verweist auf den Speicherort von Amazon S3. Dies wird von Ihrem Administrator bereitgestellt, wenn Berechtigungen für die S3-Rolle definiert sind. |
| S3 – Geheimer Schlüssel | Der geheime S3-Schlüssel verweist auf den Speicherort von Amazon S3. Dies wird von Ihrem Administrator bereitgestellt, wenn Berechtigungen für die S3-Rolle definiert sind. |
| s3SessionToken | (Optional) Der Wert des Authentifizierungs-Tokens bei der Verbindung zu S3. |
| serviceUrl | (Optional) Der URL-Speicherort, der beim Herstellen einer Verbindung mit S3 an einem nicht standardmäßigen Speicherort verwendet werden soll. |
| Behältername | (Optional) Der Name des S3-Buckets, der auf S3 eingerichtet wurde und als Ausgangspfad bei der Datenauswahl dient. |
| Ordnerpfad | Wenn Unterverzeichnisse in einem Bucket verwendet werden, können Sie bei der Datenauswahl auch einen Pfad als Ausgangspfad angeben. |

### Vorhandenes Konto verwenden

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]**.

Wählen Sie ein Konto aus der Liste aus, um Details zu diesem Konto anzuzeigen. Nachdem Sie ein Konto ausgewählt haben, klicken Sie auf **[!UICONTROL Weiter]** um fortzufahren.

![Die vorhandene Kontoschnittstelle des Quell-Workflows.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-existing-account.png)

## Auswählen von Daten

Wählen Sie im gewünschten Bucket und Unterverzeichnis die Datei aus, die Sie aufnehmen möchten. Eine Vorschau der Daten kann bereitgestellt werden, sobald Trennzeichen und Komprimierungstyp definiert sind. Nachdem Sie Ihre Datei ausgewählt haben, klicken Sie auf **[!UICONTROL Weiter]** um fortzufahren.

![Die Benutzeroberfläche für die Daten- und Dateivorschau des Quell-Workflows.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-preview.png)

>[!NOTE]
>
>Obwohl JSON- und Parquet-Dateitypen aufgeführt sind, ist ihre Verwendung im Quell-Workflow der [!DNL Acxiom] nicht erforderlich oder wird auch nicht erwartet.

## Datensatz- und Datenflussdetails angeben

Als Nächstes müssen Sie Informationen zu Ihrem Datensatz und Ihrem Datenfluss angeben.

### Datensatz-Details

>[!BEGINTABS]

>[!TAB Verwenden eines neuen Datensatzes]

Ein Datensatz ist ein Konstrukt zur Speicherung und Verwaltung einer Sammlung von Daten, in der Regel eine Tabelle, die ein Schema (Spalten) und Felder (Zeilen) enthält. Daten, die erfolgreich in Experience Platform aufgenommen werden, bleiben als Datensätze im Data Lake erhalten. Um einen neuen Datensatz zu verwenden, wählen Sie **[!UICONTROL Neuer Datensatz]** aus.

![Die neue Datensatzschnittstelle.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-new-dataset.png)

| Neue Datensatzdetails | Beschreibung |
| --- | --- |
| Name des Ausgabe-Datensatzes | Der Name des neuen Datensatzes. |
| Beschreibung | (Optional) Eine kurze Erläuterung des Zwecks des Datensatzes. |
| Schema | Eine Dropdown-Liste mit Schemata, die in Ihrer Organisation vorhanden sind. Sie können auch vor dem Prozess der Quellkonfiguration Ihr eigenes Schema erstellen. Weitere Informationen finden Sie im Handbuch unter [Erstellen eines Schemas in der Benutzeroberfläche](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Verwenden eines vorhandenen Datensatzes]

Um einen vorhandenen Datensatz zu verwenden, wählen Sie **[!UICONTROL Vorhandener Datensatz]**.

Sie können **[!UICONTROL Erweiterte Suche]** auswählen, um ein Fenster aller Datensätze Ihrer Organisation anzuzeigen, einschließlich der entsprechenden Details, z. B. ob sie für die Aufnahme in das Echtzeit-Kundenprofil aktiviert sind.

![Die vorhandene Datensatzschnittstelle.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-dataset.png)

>[!ENDTABS]

### Datenflussdetails

Wenn Ihr Datensatz für Profil aktiviert ist, können Sie in diesem Schritt den Umschalter **[!UICONTROL Profildatensatz]** auswählen, um Ihre Daten für die Profilaufnahme zu aktivieren. Sie können auch [!UICONTROL Fehlerdiagnose] und [!UICONTROL Partielle Aufnahme] aktivieren.

* **Fehlerdiagnose** - Wählen Sie **Fehlerdiagnose** aus, um die Quelle anzuweisen, Fehlerdiagnosen zu erstellen, auf die Sie später mithilfe von APIs verweisen können. Weitere Informationen finden Sie unter [Übersicht über die Fehlerdiagnose](../../../../../ingestion/quality/error-diagnostics.md)
* **Partielle Aufnahme aktivieren** - Die partielle Batch-Aufnahme umfasst die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert aufzunehmen. Mit dieser Funktion können Benutzende erfolgreich alle ihre richtigen Daten in Adobe Experience Platform aufnehmen, während alle ihre falschen Daten separat in Batches erfasst werden, zusammen mit Details zur Ungültigkeit.  Weitere Informationen finden Sie unter [Übersicht über die partielle Aufnahme](../../../../../ingestion/batch-ingestion/partial.md)

![Die Konfigurationsoberfläche für Datenflussdetails.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-dataset-details.png)

| Datenflusskonfigurationen | Beschreibung |
| --- | --- |
| Datenflussname | Der Name des Datenflusses.  Standardmäßig wird dabei der Name der zu importierenden Datei verwendet. |
| Beschreibung | (Optional) Eine kurze Beschreibung Ihres Datenflusses. |
| Warnhinweise | Experience Platform kann ereignisbasierte Warnhinweise erstellen, die Benutzende abonnieren können. Diese Optionen ermöglichen den gesamten laufenden Datenfluss zu diesen Triggern.  Weitere Informationen finden Sie unter [Warnhinweise - Übersicht](../../alerts.md) <ul><li>**Start der Ausführung des Quelldatenflusses**: Wählen Sie diesen Warnhinweis aus, um eine Benachrichtigung zu erhalten, wenn die Ausführung des Datenflusses beginnt.</li><li>**Erfolgreiche Ausführung des Quelldatenflusses**: Wählen Sie diesen Warnhinweis aus, um eine Benachrichtigung zu erhalten, wenn Ihr Datenfluss fehlerfrei endet.</li><li>**Fehler bei der Ausführung des Datenflusses an Quellen**: Wählen Sie diesen Warnhinweis aus, um eine Benachrichtigung zu erhalten, wenn die Ausführung des Datenflusses mit Fehlern endet.</li></ul> |

## Zuordnung

Verwenden Sie die Zuordnungsschnittstelle, um Ihre Quelldaten den entsprechenden Schemafeldern zuzuordnen, bevor Sie Daten in Experience Platform aufnehmen.  Weitere Informationen finden Sie im [Zuordnungshandbuch in der Benutzeroberfläche](../../../../../data-prep/ui/mapping.md)

![Die Zuordnungsschnittstelle.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-mapping.png)

## Planen der Datenfluss-Aufnahme

Verwenden Sie die Zeitplanschnittstelle, um den Aufnahmezeitplan Ihres Datenflusses zu definieren.

| Konfiguration planen | Beschreibung |
| --- | --- |
| Häufigkeit | Konfigurieren Sie die Häufigkeit , um anzugeben, wie oft der Datenfluss ausgeführt werden soll. Sie können Ihre Häufigkeit auf Folgendes festlegen: <ul><li>**Einmal**: Legen Sie für die Häufigkeit `once` fest, um eine einmalige Aufnahme zu erstellen. Konfigurationen für Intervall und Aufstockung sind beim Erstellen eines einmaligen Aufnahme-Datenflusses nicht verfügbar. Standardmäßig ist die Zeitplanfrequenz auf einmal festgelegt.</li><li>**Minute**: Legen Sie für die Häufigkeit `minute` fest, um Ihren Datenfluss so zu planen, dass Daten pro Minute aufgenommen werden.</li><li>**Stunde**: Legen Sie für die Häufigkeit `hour` fest, um den Datenfluss zu planen und Daten stündlich aufzunehmen.</li><li>**Tag**: Legen Sie für Ihre Häufigkeit `day` fest, um Ihren Datenfluss so zu planen, dass Daten täglich aufgenommen werden.</li><li>**Woche**: Legen Sie für Ihre Häufigkeit `week` fest, um Ihren Datenfluss zu planen und Daten pro Woche aufzunehmen.</li></ul> |
| Intervall | Nachdem Sie eine Häufigkeit ausgewählt haben, können Sie die Intervalleinstellung konfigurieren, um den Zeitrahmen zwischen jeder Aufnahme festzulegen. Wenn Sie beispielsweise Ihre Häufigkeit auf „Tag“ festlegen und das Intervall auf 15 konfigurieren, wird Ihr Datenfluss alle 15 Tage ausgeführt. Das Intervall kann nicht auf null festgelegt werden. Der akzeptierte Mindestintervallwert für jede Häufigkeit ist wie folgt:<ul><li>**Einmal**: nicht zutreffend</li><li>**Minute**: 15</li><li>**Stunde**: 1</li><li>**Tag**: 1</li><li>**Woche**: 1</li></ul> |
| Startzeit | Der Zeitstempel für die projizierte Ausführung, dargestellt in UTC-Zeitzone. |
| Aufstockung | Die Aufstockung bestimmt, welche Daten anfänglich aufgenommen werden. Wenn die Aufstockung aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Aufnahme aufgenommen. Wenn die Aufstockung deaktiviert ist, werden nur die Dateien aufgenommen, die zwischen der ersten Aufnahme-Ausführung und der Startzeit geladen werden. Dateien, die vor der Startzeit geladen wurden, werden nicht aufgenommen. |

![Die Benutzeroberfläche für die Zeitplankonfiguration.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-scheduling.png)

## Überprüfen des Datenflusses

Verwenden Sie die Überprüfungsseite für eine Zusammenfassung Ihres Datenflusses vor der Aufnahme. Die Details sind in die folgenden Kategorien unterteilt:

* **Verbindung** - Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **Datensatz- und Zuordnungsfelder zuweisen** - Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.
* **Planung** - Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall der Aufnahme an.
Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf Beenden und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Die Überprüfungsseite.](../../../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/image-source-review.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Batch-Daten aus Ihrer [!DNL Acxiom] in Experience Platform zu übertragen. Weitere Ressourcen finden Sie in der unten beschriebenen Dokumentation.

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn aufgenommen werden, um Informationen zu Aufnahmegeschwindigkeiten, Erfolg und Fehlern anzuzeigen. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial [Überwachen von Konten und Datenflüssen in der Benutzeroberfläche](../../monitor.md).

### Aktualisieren des Datenflusses

Um Konfigurationen für die Planung, Zuordnung und allgemeine Informationen Ihrer Datenflüsse zu aktualisieren, besuchen Sie das Tutorial [Aktualisieren von Quelldatenflüssen in der Benutzeroberfläche](../../update-dataflows.md)

### Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich **[!UICONTROL Datenflüsse]** verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).

## Zusätzliche Ressourcen {#additional-resources}

[!DNL Acxiom] Zielgruppendaten und -verteilung: https://www.acxiom.com/customer-data/audience-data-distribution/
