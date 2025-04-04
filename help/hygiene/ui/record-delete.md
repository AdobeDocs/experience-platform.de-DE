---
title: Löschen von Datensätzen
description: Erfahren Sie, wie Sie Datensätze in der Adobe Experience Platform-Benutzeroberfläche löschen.
badgeBeta: label="Beta" type="Informative"
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 25%

---

# Löschen von Datensätzen {#record-delete}

Verwenden Sie den [[!UICONTROL Datenlebenszyklus]-Arbeitsbereich](./overview.md), um Datensätze in Adobe Experience Platform basierend auf ihren Primäridentitäten zu löschen. Diese Datensätze können mit einzelnen Verbrauchern oder jeder anderen Entität verknüpft werden, die im Identitätsdiagramm enthalten ist.

>[!IMPORTANT]
> 
>Die Funktion zum Löschen von Datensätzen befindet sich derzeit in Beta und ist nur in einer **Version**. Sie steht nicht allen Kunden zur Verfügung. Löschanfragen für Datensätze sind nur für Organisationen in der eingeschränkten Version verfügbar.
> 
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

Der nächste Schritt besteht darin festzustellen, ob Sie Datensätze aus einem einzelnen Datensatz oder allen Datensätzen löschen möchten. Wenn Ihnen diese Option nicht zur Verfügung steht, fahren Sie mit dem Abschnitt [Identitäten angeben](#provide-identities) des Handbuchs fort.

Verwenden **[!UICONTROL im Abschnitt Datensatzdetails]** Optionsschaltfläche, um zwischen einem bestimmten Datensatz und allen Datensätzen auszuwählen. Wenn Sie **[!UICONTROL Datensatz auswählen]** wählen Sie anschließend das Datenbanksymbol (![Datenbanksymbol) aus, um ](/help/images/icons/database.png) Dialogfeld mit einer Liste der verfügbaren Datensätze zu öffnen. Wählen Sie den gewünschten Datensatz aus der Liste aus und klicken Sie dann auf **[!UICONTROL Fertig]**.

![Das Dialogfeld [!UICONTROL Datensatz auswählen] mit einem ausgewählten Datensatz und [!UICONTROL Fertig] hervorgehoben.](../images/ui/record-delete/select-dataset.png)

Wenn Sie Datensätze aus allen Datensätzen löschen möchten, wählen Sie **[!UICONTROL Alle Datensätze]** aus.

![Das Dialogfeld [!UICONTROL Datensatz auswählen] mit der ausgewählten Option [!UICONTROL Alle ]Datensätze)](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Wenn Sie die Option **[!UICONTROL Alle Datensätze]** auswählen, kann es sein, dass der Löschvorgang länger dauert und möglicherweise nicht zu einer korrekten Löschung der Datensätze führt.

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

Wenn Sie Datensätze aus einem einzelnen Datensatz löschen, müssen alle von Ihnen angegebenen Identitäten denselben Typ haben, da ein Datensatz nur einen Identity-Namespace haben kann. Wenn Sie sie aus allen Datensätzen löschen, können Sie mehrere Identitätstypen einbeziehen, da verschiedene Datensätze unterschiedliche primäre Identitäten haben können.

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

## Senden der Anfrage {#submit}

Nachdem Sie unter **[!UICONTROL Anfrageeinstellungen]** die Identitäten zur Anfrage hinzugefügt haben, geben Sie einen Namen und eine optionale Beschreibung für die Anfrage ein, bevor Sie **[!UICONTROL Senden]** auswählen.

>[!IMPORTANT]
> 
>Es gibt verschiedene Beschränkungen für die Gesamtzahl der Löschvorgänge von eindeutigen Identitätsdatensätzen, die jeden Monat gesendet werden können. Diese Beschränkungen basieren auf Ihrer Lizenzvereinbarung. Organisationen, die alle Editionen von Adobe Real-Time Customer Data Platform oder Adobe Journey Optimizer erworben haben, können monatlich bis zu 100.000 Identitätseintragslöschungen übermitteln. Organisationen, die **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** erworben haben, können monatlich bis zu 600.000 Identitätseinträge löschen.<br>Mit einer einzigen Löschanfrage für Datensätze über die Benutzeroberfläche können Sie 10.000 IDs gleichzeitig senden. Die [API-Methode zum Löschen von Datensätzen](../api/workorder.md#create) ermöglicht die gleichzeitige Übermittlung von 100.000 IDs.<br>Es empfiehlt sich, so viele IDs wie möglich pro Anfrage bis zu Ihrem ID-Limit zu senden. Wenn Sie eine große Anzahl von IDs löschen möchten, sollten Sie die Übermittlung einer geringen Anzahl oder einer einzelnen ID pro Löschanfrage für den Datensatz vermeiden.

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
