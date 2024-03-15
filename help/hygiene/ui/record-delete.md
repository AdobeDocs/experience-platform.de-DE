---
title: Datensätze löschen
description: Erfahren Sie, wie Sie Datensätze in der Benutzeroberfläche von Adobe Experience Platform löschen.
badgeBeta: label="Beta" type="Informative"
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 86cf250b2915a49d994fee0ab9d9ddbf65f6f836
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 34%

---

# Löschen von Datensätzen {#record-delete}

Verwenden Sie die [[!UICONTROL Lebenszyklus der Daten] Arbeitsbereich](./overview.md) , um Datensätze in Adobe Experience Platform anhand ihrer primären Identitäten zu löschen. Diese Datensätze können an einzelne Verbraucher oder eine andere Entität gebunden werden, die im Identitätsdiagramm enthalten ist.

>[!IMPORTANT]
> 
>Die Funktion zum Löschen von Datensätzen ist derzeit als Beta-Version verfügbar und ist nur in einer **limitierte Version**. Sie steht nicht allen Kunden zur Verfügung. Löschanfragen von Datensätzen sind nur für Organisationen in der eingeschränkten Version verfügbar.
> 
> 
>Das Löschen von Datensätzen ist für die Datenbereinigung, das Entfernen anonymer Daten oder die Minimierung von Daten vorgesehen. Sie dürfen **nicht** für Anfragen zu den Rechten der betroffenen Personen (Compliance) verwendet werden, da sie sich auf Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) beziehen. Verwenden Sie stattdessen [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) für alle Compliance-Anwendungsfälle.

## Voraussetzungen {#prerequisites}

Das Löschen von Datensätzen setzt ein Verständnis der Funktionsweise von Identitätsfeldern in Experience Platform voraus. Insbesondere müssen Sie die primären Identitätswerte der Entitäten kennen, deren Datensätze Sie löschen möchten, je nach Datensatz (oder Datensätzen), aus dem Sie sie löschen.

Weitere Informationen zu Identitäten in Platform finden Sie in der folgenden Dokumentation:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Führt Identitäten zwischen Geräten und Systemen zusammen und verknüpft Datensätze anhand der Identitätsfelder, die von den entsprechenden XDM-Schemata definiert werden.
* [Identity-Namespaces](../../identity-service/features/namespaces.md): In Identity-Namespaces werden die verschiedenen Arten von Identitätsinformationen definiert, die sich auf eine einzelne Person beziehen können. Sie sind eine erforderliche Komponente für jedes Identitätsfeld.
* [Echtzeit-Kundenprofil](../../profile/home.md): Verwendet Identitätsdiagramme, um einheitliche Verbraucherprofile auf der Grundlage aggregierter Daten aus mehreren Quellen bereitzustellen, die nahezu in Echtzeit aktualisiert werden.
* [Experience-Datenmodell (XDM)](../../xdm/home.md): Stellt Standarddefinitionen und -strukturen für Platform-Daten durch die Verwendung von Schemata bereit. Alle Platform-Datensätze entsprechen einem bestimmten XDM-Schema und das Schema definiert, welche Felder Identitäten sind.
* [Identitätsfelder](../../xdm/ui/fields/identity.md): Erfahren Sie, wie ein Identitätsfeld in einem XDM-Schema definiert wird.

## Anforderung erstellen {#create-request}

Um den Prozess zu starten, wählen Sie **[!UICONTROL Lebenszyklus der Daten]** im linken Navigationsbereich der Platform-Benutzeroberfläche. Die [!UICONTROL Lebenszyklusanforderungen] Arbeitsbereich angezeigt. Wählen Sie als Nächstes **[!UICONTROL Anforderung erstellen]** von der Hauptseite im Arbeitsbereich aus.

![Die [!UICONTROL Lebenszyklusanforderungen] Arbeitsbereich mit [!UICONTROL Anforderung erstellen] ausgewählt ist.](../images/ui/record-delete/create-request-button.png)

Der Workflow für die Anforderungserstellung wird angezeigt. Standardmäßig wird die Variable **[!UICONTROL Datensatz löschen]** ist unter der Option **[!UICONTROL Angeforderte Aktion]** Abschnitt. Lassen Sie diese Option aktiviert.

>[!IMPORTANT]
> 
>Im Rahmen laufender Änderungen zur Verbesserung der Effizienz und zur Senkung der Kosten für Datensatzvorgänge können Organisationen, die in das Delta-Format verschoben wurden, Daten aus dem Identity Service, dem Echtzeit-Kundenprofil und dem Data Lake löschen. Dieser Benutzertyp wird als Delta-migriert bezeichnet. Benutzer von Organisationen, die Delta-migriert wurden, können entweder Datensätze aus einem einzigen Datensatz oder aus allen Datensätzen löschen. Benutzer von Organisationen, die nicht Delta-migriert wurden, können keine Datensätze aus einem einzigen Datensatz oder aus allen Datensätzen löschen, wie in der Abbildung unten dargestellt. Fahren Sie in diesem Fall mit dem [Identitäten bereitstellen](#provide-identities) Abschnitt des Handbuchs.

![Der Workflow für die Anfrageerstellung mit dem [!UICONTROL Datensatz löschen] ausgewählt und hervorgehoben.](../images/ui/record-delete/delete-record.png)

## Auswählen von Datensätzen {#select-dataset}

Im nächsten Schritt wird bestimmt, ob Sie Datensätze aus einem einzigen Datensatz oder aus allen Datensätzen löschen möchten. Wenn diese Option nicht verfügbar ist, fahren Sie mit dem [Identitäten bereitstellen](#provide-identities) Abschnitt des Handbuchs.

Unter dem **[!UICONTROL Datensatzdetails]** verwenden, wählen Sie mit der Optionsschaltfläche zwischen einem bestimmten Datensatz und allen Datensätzen aus. Wenn Sie **[!UICONTROL Datensatz auswählen]** Wählen Sie dann das Datenbanksymbol (![Datenbanksymbol](../images/ui/record-delete/database-icon.png)), um ein Dialogfeld zu öffnen, das eine Liste der verfügbaren Datensätze bereitstellt. Wählen Sie den gewünschten Datensatz aus der Liste aus, gefolgt von **[!UICONTROL Fertig]**.

![Die [!UICONTROL Datensatz auswählen] mit einem ausgewählten Datensatz und [!UICONTROL Fertig] hervorgehoben.](../images/ui/record-delete/select-dataset.png)

Wenn Sie Datensätze aus allen Datensätzen löschen möchten, wählen Sie **[!UICONTROL Alle Datensätze]**.

![Die [!UICONTROL Datensatz auswählen] mit dem [!UICONTROL Alle Datensätze] ausgewählt ist.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Wenn Sie die Option **[!UICONTROL Alle Datensätze]** auswählen, kann es sein, dass der Löschvorgang länger dauert und möglicherweise nicht zu einer korrekten Löschung der Datensätze führt.

## Angeben von Identitäten {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Primäre Identität"
>abstract="Eine primäre Identität ist ein Attribut, das einen Datensatz mit dem Profil eines Verbrauchers in Experience Platform verknüpft. Das Feld für die primäre Identität für einen Datensatz wird durch das Schema definiert, auf dem der Datensatz basiert. In dieser Spalte müssen Sie den Typ (oder Namespace) der primären Identität des Datensatzes angeben, z. B. `email` für E-Mail-Adressen und `ecid` für Experience Cloud IDs. Weitere Informationen finden Sie im Handbuch zur Datenlebenszyklus-Benutzeroberfläche."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Identitätswert"
>abstract="In dieser Spalte müssen Sie den Wert für die primäre Identität des Datensatzes angeben, der dem in der linken Spalte angegebenen Identitätstyp entsprechen muss. Wenn der primäre Identitätstyp `email` ist, sollte der Wert die E-Mail-Adresse des Datensatzes sein. Weitere Informationen finden Sie im Handbuch zur Datenlebenszyklus-Benutzeroberfläche."

Beim Löschen von Datensätzen müssen Sie Identitätsdaten angeben, damit das System bestimmen kann, welche Datensätze gelöscht werden sollen. Für jeden Datensatz in Platform werden Daten basierend auf dem Feld **primäre Identität** gelöscht, das durch das Schema des Datensatzes definiert wird.

Wie alle Identitätsfelder in Platform besteht eine primäre Identität aus zwei Elementen: einem **Typ** (manchmal auch als Identity-Namespace bezeichnet) und einem **Wert**. Der Identitätstyp liefert Kontext dazu, wie das Feld einen Datensatz identifiziert (z. B. eine E-Mail-Adresse), und der Wert stellt die spezifische Identität eines Datensatzes für diesen Typ dar (z. B. `jdoe@example.com` für die `email` Identitätstyp). Felder, die häufig als Identitäten verwendet werden, sind Kontoinformationen, Geräte-IDs und Cookie-IDs.

>[!TIP]
>
>Wenn Sie die primäre Identität für einen bestimmten Datensatz nicht kennen, können Sie sie in der Platform-Benutzeroberfläche ermitteln. Wählen Sie dazu im Arbeitsbereich **[!UICONTROL Datensätze]** den betreffenden Datensatz aus der Liste aus. Bewegen Sie auf der Detailseite für den Datensatz den Mauszeiger in der rechten Leiste über den Namen des Datensatzschemas. Die primäre Identität wird zusammen mit dem Schemanamen und der Beschreibung angezeigt.
>
>![Das Dashboard &quot;Datensätze&quot;mit einem ausgewählten Datensatz und einem Dialogfeld &quot;Schema&quot;im Bereich &quot;Datensatzdetails&quot;. Die primäre ID des Datensatzes wird hervorgehoben.](../images/ui/record-delete/dataset-primary-identity.png)

Wenn Sie Datensätze aus einem Datensatz löschen, müssen alle von Ihnen angegebenen Identitäten denselben Typ aufweisen, da ein Datensatz nur eine primäre Identität aufweisen kann. Wenn Sie sie aus allen Datensätzen löschen, können Sie mehrere Identitätstypen einbeziehen, da verschiedene Datensätze unterschiedliche primäre Identitäten haben können.

Beim Löschen von Datensätzen stehen zwei Optionen zur Verfügung:

* [Hochladen einer JSON-Datei](#upload-json)
* [Manuelle Eingabe von Identitätswerten](#manual-identity)

### Hochladen einer JSON-Datei {#upload-json}

Um eine JSON-Datei hochzuladen, können Sie die Datei per Drag-and-Drop in den angegebenen Bereich ziehen oder **[!UICONTROL Dateien auswählen]** , um in Ihrem lokalen Verzeichnis zu suchen und auszuwählen.

![Der Workflow für die Anforderungserstellung mit der Auswahl von Dateien und der hervorgehobenen Drag &amp; Drop-Oberfläche zum Hochladen von JSON-Dateien.](../images/ui/record-delete/upload-json.png)

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
| `value` | Der Identitätswert, wie durch den Typ gekennzeichnet. |

Nach dem Hochladen der Datei können Sie mit dem [Senden der Anfrage](#submit) fortfahren.

### Identitäten manuell eingeben {#manual-identity}

Um Identitäten manuell einzugeben, wählen Sie **[!UICONTROL Identität hinzufügen]** aus.

![Der Workflow für die Anfrageerstellung mit dem [!UICONTROL Identität hinzufügen] hervorgehoben.](../images/ui/record-delete/add-identity.png)

Es werden Steuerelemente angezeigt, mit denen Sie Identitäten einzeln eingeben können. Wählen Sie unter **[!UICONTROL Primäre Identität]** im Dropdown-Menü den Identitätstyp aus. under **[!UICONTROL Identitätswert]**, geben Sie den primären Identitätswert für den Datensatz an.

![Der Workflow für die Anfrageerstellung mit einem manuell hinzugefügten Identitätsfeld.](../images/ui/record-delete/identity-added.png)

Um weitere Identitäten hinzuzufügen, wählen Sie das Pluszeichen (![Ein Pluszeichen.](../images/ui/record-delete/plus-icon.png)) neben einer der Zeilen oder wählen Sie **[!UICONTROL Identität hinzufügen]**.

![Der Workflow zur Anforderungserstellung mit dem Pluszeichen und dem Symbol zum Hinzufügen einer Identität wurde hervorgehoben.](../images/ui/record-delete/more-identities.png)

## Senden der Anfrage {#submit}

Nachdem Sie unter **[!UICONTROL Anfrageeinstellungen]** die Identitäten zur Anfrage hinzugefügt haben, geben Sie einen Namen und eine optionale Beschreibung für die Anfrage ein, bevor Sie **[!UICONTROL Senden]** auswählen.

>[!IMPORTANT]
> 
>Es gibt unterschiedliche Beschränkungen für die Gesamtzahl der eindeutigen Identitätsdatensätze, die jeden Monat gesendet werden können. Diese Beschränkungen basieren auf Ihrem Lizenzvertrag. Organisationen, die alle Editionen von Adobe Real-time Customer Data Platform und Adobe Journey Optimizer erworben haben, können jeden Monat bis zu 100.000 Identitätsdatensätze löschen. Organisationen, die gekauft haben **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** kann jeden Monat bis zu 600.000 Identitätsdatensätze löschen.<br>Mit einer einzelnen Anfrage zum Löschen von Datensätzen über die Benutzeroberfläche können Sie 10.000 IDs gleichzeitig senden. Die [API-Methode zum Löschen von Datensätzen](../api/workorder.md#create) ermöglicht die gleichzeitige Übermittlung von 100.000 IDs.<br>Es empfiehlt sich, bis zu Ihrer ID-Grenze so viele IDs pro Anfrage wie möglich zu senden. Wenn Sie eine große Anzahl von IDs löschen möchten, sollte vermieden werden, ein geringes Volumen oder eine einzelne ID pro Datensatz-Löschanfrage zu senden.

![Die Anfrageeinstellung [!UICONTROL Name] und [!UICONTROL Beschreibung] Felder mit [!UICONTROL Einsenden] hervorgehoben.](../images/ui/record-delete/submit.png)

A [!UICONTROL Validierungsanfrage] angezeigt, um anzugeben, dass die Identitäten nach dem Löschen nicht wiederhergestellt werden können. Auswählen **[!UICONTROL Einsenden]** zur Bestätigung der Liste der Identitäten, deren Daten Sie löschen möchten.

![Die [!UICONTROL Validierungsanfrage] angezeigt.](../images/ui/record-delete/confirm-request.png)

Nachdem die Anfrage gesendet wurde, wird eine Arbeitsreihenfolge erstellt und auf der [!UICONTROL Datensatz] des [!UICONTROL Lebenszyklus der Daten] Arbeitsbereich. Hier können Sie den Fortschritt des Arbeitsauftrags überwachen.

>[!NOTE]
>
>Weitere Informationen finden Sie im Abschnitt Übersicht unter [Fristen und Transparenz](../home.md#record-delete-transparency) für Details darüber, wie Löschvorgänge von Datensätzen nach der Ausführung verarbeitet werden.

![Die [!UICONTROL Datensatz] des [!UICONTROL Lebenszyklus der Daten] Arbeitsbereich mit hervorgehobener neuer Anforderung.](../images/ui/record-delete/request-log.png)

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie Datensätze in der Experience Platform-Benutzeroberfläche löschen. Informationen zum Ausführen anderer Aufgaben zur Lebenszyklusverwaltung in der Benutzeroberfläche finden Sie im Abschnitt [Übersicht über die Benutzeroberfläche von Data Lebenszyklus](./overview.md).

Informationen zum Löschen von Datensätzen mithilfe der Data Hygiene API finden Sie im Abschnitt [Endpunktleitfaden für Arbeitsaufträge](../api/workorder.md).
