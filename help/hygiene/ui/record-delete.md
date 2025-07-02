---
title: Anfragen zum Löschen von Datensätzen (UI-Workflow)
description: Erfahren Sie, wie Sie Datensätze in der Adobe Experience Platform-Benutzeroberfläche löschen.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 9ee5225c7494c28023c26181dfe626780133bb5d
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 19%

---

# Anfragen zum Löschen von Datensätzen (UI-Workflow) {#record-delete}

Verwenden Sie den [[!UICONTROL Datenlebenszyklus]-Arbeitsbereich](./overview.md), um Datensätze in Adobe Experience Platform basierend auf ihren Primäridentitäten zu löschen. Diese Datensätze können mit einzelnen Verbrauchern oder jeder anderen Entität verknüpft werden, die im Identitätsdiagramm enthalten ist.

>[!IMPORTANT]
>
>Löschvorgänge von Datensätzen dienen zur Datenbereinigung, zum Entfernen anonymer Daten oder zur Datenminimierung. Sie dürfen **nicht** für Anfragen zu den Rechten der betroffenen Personen (Compliance) verwendet werden, da sie sich auf Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) beziehen. Verwenden Sie stattdessen [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) für alle Compliance-Anwendungsfälle.

## Voraussetzungen {#prerequisites}

Das Löschen von Datensätzen setzt ein Verständnis der Funktionsweise von Identitätsfeldern in Experience Platform voraus. Insbesondere müssen Sie die Identity-Namespace-Werte der Entitäten kennen, deren Datensätze Sie löschen möchten, je nach Datensatz (oder Datensätzen), aus dem Sie sie löschen möchten.

Weitere Informationen zu Identitäten in Experience Platform finden Sie in der folgenden Dokumentation:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Führt Identitäten zwischen Geräten und Systemen zusammen und verknüpft Datensätze anhand der Identitätsfelder, die von den entsprechenden XDM-Schemata definiert werden.
* [Identity-Namespaces](../../identity-service/features/namespaces.md): In Identity-Namespaces werden die verschiedenen Arten von Identitätsinformationen definiert, die sich auf eine einzelne Person beziehen können. Sie sind eine erforderliche Komponente für jedes Identitätsfeld.
* [Echtzeit-Kundenprofil](../../profile/home.md): Verwendet Identitätsdiagramme, um vereinheitlichte Verbraucherprofile auf der Grundlage aggregierter Daten aus mehreren Quellen bereitzustellen, die nahezu in Echtzeit aktualisiert werden.
* [Experience-Datenmodell (XDM)](../../xdm/home.md): Stellt Standarddefinitionen und -strukturen für Experience Platform-Daten durch die Verwendung von Schemata bereit. Alle Experience Platform-Datensätze entsprechen einem bestimmten XDM-Schema und das Schema definiert, welche Felder Identitäten sind.
* [Identitätsfelder](../../xdm/ui/fields/identity.md): Erfahren Sie, wie ein Identitätsfeld in einem XDM-Schema definiert wird.

## Erstellen einer Anfrage {#create-request}

Wählen Sie zunächst **[!UICONTROL Datenlebenszyklus]** im linken Navigationsbereich der Experience Platform-Benutzeroberfläche aus. Der [!UICONTROL Datenlebenszyklusanfragen] wird angezeigt. Wählen Sie anschließend **[!UICONTROL Anfrage erstellen]** auf der Hauptseite im Arbeitsbereich aus.

![Der Arbeitsbereich [!UICONTROL Datenlebenszyklusanfragen] mit [!UICONTROL Anfrage erstellen] ausgewählt.](../images/ui/record-delete/create-request-button.png)

Der Workflow zur Anfrageerstellung wird angezeigt. Standardmäßig ist die Option **[!UICONTROL Datensatz löschen]** im Abschnitt **[!UICONTROL Angeforderte Aktion]** ausgewählt. Lassen Sie diese Option aktiviert.

>[!IMPORTANT]
> 
>Um die Effizienz zu verbessern und den Datensatzbetrieb kostengünstiger zu gestalten, können Unternehmen, die in das Delta-Format verschoben wurden, Daten aus dem Identity Service, dem Echtzeit-Kundenprofil und dem Data Lake löschen. Dieser Benutzertyp wird als „delta-migriert“ bezeichnet. Benutzer von Organisationen, die in den Delta-Bereich migriert wurden, können Datensätze aus einem oder allen Datensätzen löschen. Benutzer von Organisationen, die keine Delta-Migration durchgeführt haben, können keine Datensätze selektiv aus einem einzelnen Datensatz oder allen Datensätzen löschen, wie in der Abbildung unten dargestellt. Fahren Sie in diesem Fall mit dem Abschnitt [Bereitstellen von ](#provide-identities)&quot; des Handbuchs fort.

![Der Workflow für die Anfrageerstellung mit [!UICONTROL  ausgewählten und hervorgehobenen Option &quot;] löschen“](../images/ui/record-delete/delete-record.png)

## Auswählen von Datensätzen {#select-dataset}

Der nächste Schritt besteht darin festzustellen, ob Sie Datensätze aus einem einzelnen Datensatz oder allen Datensätzen löschen möchten. Abhängig von der Konfiguration Ihres Unternehmens ist die Option zur Datensatzauswahl möglicherweise nicht verfügbar. Wenn diese Option nicht angezeigt wird, fahren Sie mit dem Abschnitt [Identitäten angeben](#provide-identities) des Handbuchs fort.

Wählen Sie **[!UICONTROL Abschnitt Datensatzdetails]** Optionsfeld aus, um entweder einen bestimmten Datensatz oder alle Datensätze auszuwählen.

Um aus einem bestimmten Datensatz zu löschen, klicken Sie auf **[!UICONTROL Datensatz auswählen]** und wählen dann das Datenbanksymbol (![Datenbanksymbol](/help/images/icons/database.png)) aus. Wählen Sie im angezeigten Dialogfeld einen Datensatz aus und klicken Sie zur Bestätigung **[!UICONTROL Fertig]**.

![Das Dialogfeld [!UICONTROL Datensatz auswählen] mit einem ausgewählten Datensatz und [!UICONTROL Fertig] hervorgehoben.](../images/ui/record-delete/select-dataset.png)

Um aus allen Datensätzen zu löschen, wählen Sie **[!UICONTROL Alle Datensätze]** aus. Diese Option vergrößert den Umfang des Vorgangs und erfordert die Angabe aller relevanten Identitätstypen.

![Das Dialogfeld [!UICONTROL Datensatz auswählen] mit der ausgewählten Option [!UICONTROL Alle ]Datensätze)](../images/ui/record-delete/all-datasets.png)

>[!WARNING]
>
>Wenn Sie **[!UICONTROL Alle Datensätze]** auswählen, wird der Vorgang auf alle Datensätze in Ihrer Organisation erweitert. Jeder Datensatz kann einen anderen primären Identitätstyp verwenden. Sie müssen (**erforderlichen Identitätstypen) angeben** um eine genaue Übereinstimmung sicherzustellen.
>
>Wenn ein Identitätstyp fehlt, werden beim Löschen möglicherweise einige Datensätze übersprungen. Dies kann die Verarbeitung verlangsamen und zu (**Ergebnissen)**.

Jeder Datensatz in Experience Platform unterstützt nur einen primären Identitätstyp.

* Beim Löschen aus einem **einzelnen Datensatz** müssen alle Identitäten in Ihrer Anfrage den **gleichen Typ** verwenden.
* Beim Löschen aus **allen Datensätzen** können Sie **mehrere Identitätstypen** einbeziehen, da verschiedene Datensätze möglicherweise auf verschiedenen primären Identitäten basieren.“

## Angeben von Identitäten {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Identity-Namespace"
>abstract="Ein Identity-Namespace ist ein Attribut, das einen Eintrag mit dem Profil einer Verbraucherin bzw. eines Verbrauchers in Experience Platform verknüpft. Das Feld für den Identity-Namespace für einen Eintrag wird durch das Schema definiert, auf dem der Eintrag basiert. In dieser Spalte müssen Sie den Typ (oder Namespace) des Identity-Namespace des Eintrags angeben, z. B. `email` für E-Mail-Adressen und `ecid` für Experience Cloud IDs. Weitere Informationen finden Sie im Handbuch zur Datenlebenszyklus-Benutzeroberfläche."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Primärer Identitätswert"
>abstract="In dieser Spalte müssen Sie den Wert für den Identity-Namespace des Eintrags angeben, der dem in der linken Spalte angegebenen Identitätstyp entsprechen muss. Wenn der Typ des Identity-Namespace `email` ist, sollte der Wert die E-Mail-Adresse des Eintrags sein. Weitere Informationen finden Sie im Handbuch zur Datenlebenszyklus-Benutzeroberfläche."

Beim Löschen von Datensätzen müssen Sie Identitätsinformationen angeben, damit das System bestimmen kann, welche Datensätze gelöscht werden sollen. Für jeden Datensatz in Experience Platform werden Datensätze basierend auf dem Feld **Identity-Namespace** gelöscht, das durch das Schema des Datensatzes definiert wird.

Wie alle Identitätsfelder in Experience Platform besteht ein Identity-Namespace aus zwei Elementen: einem **type** (manchmal auch als Identity-Namespace bezeichnet) und einem **value**. Der Identitätstyp liefert den Kontext dazu, wie das Feld einen Datensatz identifiziert (z. B. über eine E-Mail-Adresse). Der Wert stellt die spezifische Identität eines Datensatzes für diesen Typ dar (z. B. `jdoe@example.com` für den `email` Identitätstyp). Felder, die häufig als Identitäten verwendet werden, sind Kontoinformationen, Geräte-IDs und Cookie-IDs.

>[!TIP]
>
>Wenn Sie den Identity-Namespace für einen bestimmten Datensatz nicht kennen, können Sie ihn in der Experience Platform-Benutzeroberfläche finden. Wählen Sie dazu im Arbeitsbereich **[!UICONTROL Datensätze]** den betreffenden Datensatz aus der Liste aus. Bewegen Sie auf der Detailseite für den Datensatz den Mauszeiger in der rechten Leiste über den Namen des Datensatzschemas. Der Identity-Namespace wird zusammen mit dem Schemanamen und der Beschreibung angezeigt.
>
>![Das Dashboard „Datensätze“, in dem ein Datensatz ausgewählt und ein Schemadialogfeld im Bedienfeld „Datensatzdetails“ geöffnet wurde. Die primäre ID des Datensatzes ist hervorgehoben.](../images/ui/record-delete/dataset-primary-identity.png)

Es gibt zwei Möglichkeiten, beim Löschen von Datensätzen Identitäten bereitzustellen:

* [Hochladen einer JSON-Datei](#upload-json)
* [Manuelle Eingabe primärer Identitätswerte](#manual-identity)

### Hochladen einer JSON-Datei {#upload-json}

Um eine JSON-Datei hochzuladen, können Sie die Datei per Drag-and-Drop in den bereitgestellten Bereich ziehen oder &quot;**[!UICONTROL auswählen“]**, um die Datei in Ihrem lokalen Verzeichnis zu suchen und auszuwählen.

![Der Workflow für die Anfrageerstellung mit der hervorgehobenen Option „Dateien auswählen“ und der hervorgehobenen Drag-and-Drop-Oberfläche für das Hochladen von JSON-Dateien.](../images/ui/record-delete/upload-json.png)

Die JSON-Datei muss als Array von Objekten formatiert sein, wobei jedes Objekt eine Identität darstellt.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `namespaceCode` | Der Identitätstyp. |
| `value` | Der primäre Identitätswert, wie durch den Typ gekennzeichnet. |

Nach dem Hochladen der Datei können Sie mit dem [Senden der Anfrage](#submit) fortfahren.

### Manuelles Eingeben von Identitäten {#manual-identity}

Um Identitäten manuell einzugeben, wählen Sie **[!UICONTROL Identität hinzufügen]** aus.

![Der Workflow zur Anfrageerstellung mit der hervorgehobenen Option [!UICONTROL Identität hinzufügen].](../images/ui/record-delete/add-identity.png)

Es werden Steuerelemente angezeigt, mit denen Sie Identitäten einzeln eingeben können. Wählen **[!UICONTROL unter]** Identity-Namespace) im Dropdown-Menü den Identitätstyp aus. Geben Sie unter **[!UICONTROL Primärer Identitätswert]** den Identity-Namespace-Wert für den Datensatz an.

![Der Workflow zur Anfrageerstellung mit einem Identitätsfeld wurde manuell hinzugefügt.](../images/ui/record-delete/identity-added.png)

Um weitere Identitäten hinzuzufügen, wählen Sie das Pluszeichen (![ Pluszeichen ) aus.](/help/images/icons/tree-expand-all.png)) neben einer der Zeilen oder wählen Sie **[!UICONTROL Identität hinzufügen]** aus.

![Der Workflow für die Anfrageerstellung mit dem Pluszeichen und dem hervorgehobenen Symbol „Identität hinzufügen“.](../images/ui/record-delete/more-identities.png)

## Kontingente und Verarbeitungszeitpläne {#quotas}

Anfragen zum Löschen von Datensätzen unterliegen täglichen und monatlichen Obergrenzen für die Übermittlung von Identifikatoren, die durch die Lizenzberechtigung Ihres Unternehmens bestimmt werden. Diese Einschränkungen gelten sowohl für benutzeroberflächen- als auch für API-basierte Löschanfragen.

>[!NOTE]
>
>Sie können bis zu **1.000.000 Kennungen pro Tag**, jedoch nur, wenn Ihr restliches monatliches Kontingent dies zulässt. Wenn Ihre monatliche Obergrenze weniger als 1 Million beträgt, können Ihre täglichen Einreichungen diese Obergrenze nicht überschreiten.

### Berechtigung zur monatlichen Übermittlung nach Produkt {#quota-limits}

In der folgenden Tabelle sind die Beschränkungen für die Übermittlung von Kennungen nach Produkt und Berechtigungsebene aufgeführt. Für jedes Produkt ist die monatliche Obergrenze der niedrigere von zwei Werten: eine feste Kennungsobergrenze oder ein prozentualer Schwellenwert, der an Ihr lizenziertes Datenvolumen gebunden ist.

| Produkt | Beschreibung der Berechtigung | Monatliche Obergrenze (je nachdem, welcher Wert niedriger ist) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP oder Adobe Journey Optimizer | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 5 % der adressierbaren Zielgruppe |
| Real-Time CDP oder Adobe Journey Optimizer | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 10 % der adressierbaren Zielgruppe |
| Customer Journey Analytics | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 100 Kennungen pro Million CJA-Berechtigungszeilen |
| Customer Journey Analytics | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 200 Kennungen pro Million CJA-Berechtigungszeilen |

>[!NOTE]
>
> Die meisten Unternehmen verfügen über niedrigere monatliche Limits, die auf ihren tatsächlichen adressierbaren Zielgruppen- oder CJA-Zeilenberechtigungen basieren.

Die Kontingente werden am ersten Tag jedes Kalendermonats zurückgesetzt. Nicht verwendetes Kontingent wird **nicht** übertragen.

>[!NOTE]
>
>Kontingente basieren auf der lizenzierten monatlichen Berechtigung Ihres Unternehmens für **übermittelte Kennungen**. Diese werden von den Systemschutzmechanismen nicht durchgesetzt, können jedoch überwacht und überprüft werden.
>
>Löschen eines Datensatzes ist ein **freigegebener Dienst**. Die monatliche Obergrenze spiegelt die höchsten Berechtigungen für Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics und alle anwendbaren Shield-Add-ons wider.

### Zeitleisten für die Übermittlung von Identifikatoren {#sla-processing-timelines}

Nach der Übermittlung werden Anfragen zum Löschen von Datensätzen basierend auf Ihrer Berechtigungsstufe in die Warteschlange gestellt und verarbeitet.

| Produkt- und Berechtigungsbeschreibung | Warteschlangendauer | Maximale Verarbeitungszeit (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | Bis zu 15 Tage | 30 Tage |
| Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | In der Regel 24 Stunden | 15 Tage |

Wenn für Ihr Unternehmen höhere Limits erforderlich sind, wenden Sie sich zur Überprüfung der Berechtigungen an den Adobe-Support.

>[!TIP]
>
>Informationen zur aktuellen Kontingentnutzung oder Berechtigungsstufe finden Sie im [Kontingentreferenzhandbuch](../api/quota.md).

## Senden der Anfrage {#submit}

Nachdem Sie unter **[!UICONTROL Anfrageeinstellungen]** die Identitäten zur Anfrage hinzugefügt haben, geben Sie einen Namen und eine optionale Beschreibung für die Anfrage ein, bevor Sie **[!UICONTROL Senden]** auswählen.

>[!TIP]
>
>Sie können über die Benutzeroberfläche bis zu 10.000 Identitäten pro Anfrage senden. Verwenden Sie zum Übermitteln größerer Volumes (bis zu 100.000 IDs pro Anfrage) die [API-Methode](../api/workorder.md#create).

![Die Felder  Name“ und [!UICONTROL Beschreibung] der Anfrageeinstellung mit [!UICONTROL Submit] Hervorhebung.](../images/ui/record-delete/submit.png)

Ein Dialogfeld [!UICONTROL Anfrage bestätigen] zeigt an, dass die Identitäten nach dem Löschen nicht wiederhergestellt werden können. Wählen Sie **[!UICONTROL Senden]** aus, um die Liste der Identitäten zu bestätigen, deren Daten Sie löschen möchten.

![Dialogfeld [!UICONTROL Anforderung bestätigen].](../images/ui/record-delete/confirm-request.png)

Nachdem die Anfrage gesendet wurde, wird ein Arbeitsauftrag erstellt und auf der Registerkarte &quot;[!UICONTROL &quot; ] Arbeitsbereichs [!UICONTROL Datenlebenszyklus] angezeigt. Hier können Sie den Fortschritt des Arbeitsauftrags überwachen.

>[!NOTE]
>
>Im Abschnitt „Übersicht“ unter [Timelines und Transparenz](../home.md#record-delete-transparency) finden Sie Einzelheiten darüber, wie Löschvorgänge von Datensätzen verarbeitet werden, sobald sie ausgeführt werden.

![Die Registerkarte [!UICONTROL Datensatz] des Arbeitsbereichs [!UICONTROL Datenlebenszyklus] mit der hervorgehobenen neuen Anfrage.](../images/ui/record-delete/request-log.png)

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Datensätze in der Experience Platform-Benutzeroberfläche gelöscht werden. Weitere Informationen zur Durchführung anderer Datenlebenszyklus-Management-Aufgaben in der Benutzeroberfläche finden Sie im Abschnitt [Übersicht über die Datenlebenszyklus-Benutzeroberfläche](./overview.md).

Informationen zum Löschen von Datensätzen mithilfe der Datenhygiene-API finden Sie im [Handbuch zum Arbeitsauftrags-Endpunkt](../api/workorder.md).
