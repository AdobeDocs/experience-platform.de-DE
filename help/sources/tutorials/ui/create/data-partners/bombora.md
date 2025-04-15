---
title: Verbinden des Bombora Intent mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Bombora Intent mit Experience Platform verbinden
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P-Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 76a4fed5-b2d5-46d5-9245-b52792a7d323
source-git-commit: a1af85c6b76cc7bded07ab4acaec9c3213a94397
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 9%

---

# Verbinden von [!DNL Bombora Intent] mit Experience Platform über die Benutzeroberfläche

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Bombora Intent]-Konto über die Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md): Real-Time CDP B2B edition wurde speziell für Marketing-Fachleute entwickelt, die in einem Business-to-Business-Service-Modell arbeiten. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.
* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Voraussetzungen

Informationen [[!DNL Bombora Intent]  Abrufen Ihrer Authentifizierungsdaten finden Sie ](../../../../connectors/data-partners/bombora.md) „Übersicht“.

## Navigieren im Quellkatalog

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich *[!UICONTROL Quellen]* zuzugreifen. Sie können die entsprechende Kategorie im Bedienfeld *[!UICONTROL Kategorien]* auswählen. Alternativ können Sie über die Suchleiste zu der spezifischen Quelle navigieren, die Sie verwenden möchten.

Um [!DNL Bombora] zu verwenden, wählen Sie die Quellkarte **[!UICONTROL Bombora Intent]** unter *[!UICONTROL Daten- und Identitätspartner]* und dann **[!UICONTROL Daten hinzufügen]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit der ausgewählten Karte „Bombora Intent“](../../../../images/tutorials/create/bombora/catalog.png)

## Authentifizierung {#authentication}

### Vorhandenes Konto verwenden {#existing}

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das Konto, das Sie verwenden möchten, aus der Liste der Konten in der Benutzeroberfläche aus.

Nachdem Sie Ihr Konto ausgewählt haben, klicken Sie auf **[!UICONTROL Weiter]**, um mit dem nächsten Schritt fortzufahren.

![Die vorhandene Kontoschnittstelle im Quell-Workflow.](../../../../images/tutorials/create/bombora/existing.png)

### Neues Konto erstellen {#create}

Wenn Sie noch kein -Konto haben, müssen Sie ein neues Konto erstellen, indem Sie die Authentifizierungsdaten angeben, die Ihrer Quelle entsprechen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Kontonamen und optional eine Beschreibung für Ihre Kontodetails an. Geben Sie als Nächstes die entsprechenden Authentifizierungswerte an, um Ihre Quelle für Experience Platform zu authentifizieren. Um Ihr [!DNL Bombora]-Konto zu verbinden, benötigen Sie die folgenden Anmeldeinformationen:

* **Zugriffsschlüssel-ID**: Ihre [!DNL Bombora] Zugriffsschlüssel-ID. Dies ist eine 61-stellige alphanumerische Zeichenfolge, die zur Authentifizierung Ihres -Kontos bei Experience Platform erforderlich ist.
* **Geheimer Zugriffsschlüssel**: Ihr geheimer [!DNL Bombora]. Dies ist eine mit Base-64 verschlüsselte Zeichenfolge mit 40 Zeichen, die zum Authentifizieren Ihres -Kontos bei Experience Platform erforderlich ist.
* **Behältername**: Ihr [!DNL Bombora] Behälter, aus dem Daten abgerufen werden.

![Die neue Kontoschnittstelle im Quell-Workflow.](../../../../images/tutorials/create/bombora/new.png)

## Angeben von Datenflussdetails {#provide-dataflow-details}

Nachdem Ihr Konto authentifiziert und verbunden ist, müssen Sie jetzt die folgenden Details für Ihren Datenfluss angeben:

* **Datenflussname**: Der Name Ihres Datenflusses. Sie können diesen Namen verwenden, um in der Benutzeroberfläche nach Ihrem Datenfluss zu suchen, nachdem er erstellt und verarbeitet wurde.
* **Beschreibung**: (Optional) Eine kurze Erklärung oder zusätzliche Informationen für Ihren Datenfluss.
* **Domain-**: Die Domain oder das Website-Feld, das Ihre Quellkontodatensätze mit Experience Platform-Konten abgleicht. Dieser Wert kann von Ihren Konfigurationen abhängen. Wenn keine Domain angegeben wird, wird standardmäßig accountOrganization.website verwendet.

![Die Datenflussdetails-Schnittstelle des Quell-Workflows.](../../../../images/tutorials/create/bombora/dataflow-detail.png)

## Planen des Datenflusses {#schedule-dataflow}

Verwenden Sie als Nächstes die Zeitplanungs-Schnittstelle, um einen Aufnahmezeitplan für Ihren Datenfluss zu konfigurieren.

* **Häufigkeit**: Konfigurieren Sie die Häufigkeit, um anzugeben, wie oft der Datenfluss ausgeführt werden soll. Sie können Ihren [!DNL Bombora] Datenfluss so planen, dass Daten mit einer wöchentlichen Rate aufgenommen werden.
* **Intervall**: Das Intervall gibt die Zeitspanne zwischen den einzelnen Aufnahmezyklen an. Das einzige unterstützte Intervall für einen [!DNL Bombora] Datenfluss ist 1. Das bedeutet, dass Ihr Datenfluss Daten einmal wöchentlich aufnimmt, jede Woche.
* **Startzeit**: Die Startzeit gibt an, wann die erste Iteration des Datenflusses ausgeführt wird. [!DNL Bombora] sendet Daten einmal wöchentlich montags um 12:00 Uhr UTC an Adobe. Daher müssen Sie Ihre Aufnahmestartzeit nach 12:00 Uhr UTC festlegen. Darüber hinaus müssen Sie die Aufnahmezeit mit [!DNL Bombora] bestätigen, da diese ihren Zeitplan ändern können, wenn sie Dateien in Adobe ablegen.

Nachdem Sie den Aufnahmezeitplan Ihres Datenflusses konfiguriert haben, klicken Sie auf **[!UICONTROL Weiter]**.

![Die Planungsschnittstelle des Quell-Workflows.](../../../../images/tutorials/create/bombora/scheduling.png)

## Datenfluss überprüfen {#review-dataflow}

Der letzte Schritt im Prozess zur Erstellung eines Datenflusses besteht darin, Ihren Datenfluss zu überprüfen, bevor er ausgeführt wird. Verwenden Sie den *[!UICONTROL Überprüfen]* Schritt, um die Details Ihres neuen Datenflusses zu überprüfen, bevor er ausgeführt wird. Die Details sind in die folgenden Kategorien unterteilt:

* **Verbindung**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **Planung**: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmezeitplans an.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]**.

![Die Überprüfungsschnittstelle des Quell-Workflows.](../../../../images/tutorials/create/bombora/review.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Intent-Daten aus Ihrer [!DNL Bombora] in Experience Platform zu übertragen. Weitere Ressourcen finden Sie in der unten beschriebenen Dokumentation.

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn aufgenommen werden, um Informationen zu Aufnahmegeschwindigkeiten, Erfolg und Fehlern anzuzeigen. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial [Überwachen von Konten und Datenflüssen in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

### Aktualisieren des Datenflusses

Um Konfigurationen für die Planung, Zuordnung und allgemeine Informationen Ihrer Datenflüsse zu aktualisieren, besuchen Sie das Tutorial [Aktualisieren von Quelldatenflüssen in der Benutzeroberfläche](../../update-dataflows.md).

### Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich **[!UICONTROL Datenflüsse]** verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).
