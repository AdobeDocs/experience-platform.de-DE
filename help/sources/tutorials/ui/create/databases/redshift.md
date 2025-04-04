---
title: Verbinden von AWS Redshift mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie ein AWS Redshift-Konto mithilfe der Quellen-Benutzeroberfläche mit Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 20%

---

# Verbinden von [!DNL AWS Redshift] mit Experience Platform über die Benutzeroberfläche

>[!IMPORTANT]
>
>Die [!DNL AWS Redshift] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL AWS Redshift]-Konto mithilfe des Quellarbeitsbereichs in der Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL AWS Redshift]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren.

## Navigieren im Quellkatalog

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie **[!DNL AWS Redshift]** unter der Kategorie *[!UICONTROL Datenbanken]* und dann **[!UICONTROL Einrichten]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit der ausgewählten AWS Redshift-Quellkarte.](../../../../images/tutorials/create/redshift/catalog.png)

## Vorhandenes Konto verwenden {#existing}

Anschließend werden Sie zum Authentifizierungsschritt des Quell-Workflows weitergeleitet. Hier können Sie entweder ein vorhandenes Konto verwenden oder ein neues Konto erstellen.

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL AWS Redshift] aus dem Kontoverzeichnis und dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![Das Kontoverzeichnis im Quell-Workflow, in dem vorhandene Konten aufgelistet sind.](../../../../images/tutorials/create/redshift/existing.png)

## Neues Konto erstellen {#create}

Wenn Sie noch kein -Konto haben, müssen Sie ein neues Konto erstellen, indem Sie die Authentifizierungsdaten angeben, die Ihrer Quelle entsprechen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen an und fügen Sie optional eine Beschreibung für Ihr Konto hinzu.

### Verbindung zu Experience Platform auf Azure herstellen {#azure}

Um Ihr [!DNL AWS Redshift]-Konto mit Experience Platform auf Azure zu verbinden, geben Sie Ihre Authentifizierungsdaten im Eingabeformular ein und wählen Sie **Mit Quelle [!UICONTROL verbinden] aus**.

![Die neue Kontoschnittstelle zum Verbinden von AWS Redshift mit Experience Platform auf Azure.](../../../../images/tutorials/create/redshift/new.png)

| Anmeldedaten | Beschreibung |
| --- | --- |
| Server | Der Server-Name Ihrer [!DNL AWS Redshift]. |
| Port | Der TCP-Port, den ein [!DNL AWS Redshift]-Server verwendet, um auf Client-Verbindungen zu warten. |
| Benutzername | Der Benutzername des Kontos, dem Sie Zugriff gewähren möchten. |
| Kennwort | Das Kennwort, das dem Benutzerkonto entspricht. |
| Datenbank | Die [!DNL AWS Redshift], aus der Daten abgerufen werden sollen. |

Weitere Informationen zu den ersten Schritten finden Sie [diesem [!DNL AWS Redshift] Dokument](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Verbinden mit Experience Platform auf AWS {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf AWS Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Um ein neues [!DNL AWS Redshift] zu erstellen und eine Verbindung zu Experience Platform auf AWS herzustellen, stellen Sie sicher, dass Sie sich in einer VA6-Sandbox befinden, geben Sie die erforderlichen Anmeldeinformationen für die Authentifizierung ein und wählen Sie dann **[!UICONTROL Mit Quelle verbinden]** aus.

![Die neue Kontoschnittstelle zum Verbinden von AWS Redshift mit Experience Platform auf AWS.](../../../../images/tutorials/create/redshift/aws-auth.png)

| Anmeldedaten | Beschreibung |
| --- | --- |
| Server | Der Server-Name Ihrer [!DNL AWS Redshift]. |
| Port | Der TCP-Port, den ein [!DNL AWS Redshift]-Server verwendet, um auf Client-Verbindungen zu warten. |
| Benutzername | Der Benutzername des Kontos, dem Sie Zugriff gewähren möchten. |
| Kennwort | Das Kennwort, das dem Benutzerkonto entspricht. |
| Datenbank | Die [!DNL AWS Redshift], aus der Daten abgerufen werden sollen. |
| Schema | Der Name des Schemas, das Ihrer [!DNL AWS Redshift]-Datenbank zugeordnet ist. Sie müssen sicherstellen, dass der Benutzer, dem Sie Datenbankzugriff gewähren möchten, auch Zugriff auf dieses Schema hat. |

Weitere Informationen zu den ersten Schritten finden Sie [diesem [!DNL AWS Redshift] Dokument](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrer [!DNL AWS Redshift] und Experience Platform hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [Erstellen eines Datenflusses, um Daten aus Ihrer Datenbank in Experience Platform aufzunehmen](../../dataflow/databases.md).