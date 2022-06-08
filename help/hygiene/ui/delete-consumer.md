---
title: Verbraucherdatensätze löschen
description: Erfahren Sie, wie Sie Verbraucherdatensätze in der Benutzeroberfläche von Adobe Experience Platform löschen.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: 6f94c7c5e844eaddd50653296875886757f6fb35
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 0%

---

# Verbraucherdatensätze löschen

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Adobe Shield für das Gesundheitswesen erworben haben.

Die [[!UICONTROL Datenhygiene] Arbeitsbereich](./overview.md) in der Adobe Experience Platform-Benutzeroberfläche können Sie Verbraucherdatensätze löschen, die am Identity Service und Echtzeit-Kundenprofil teilnehmen.

## Voraussetzungen

Das Löschen von Verbraucherdatensätzen setzt ein Verständnis der Funktionsweise von Identitätsfeldern in Experience Platform voraus. Insbesondere müssen Sie die primären Identitätswerte der Verbraucher kennen, deren Datensätze Sie löschen möchten, je nach Datensatz (oder Datensätzen), aus dem Sie sie löschen.

Weitere Informationen zu Identitäten in Platform finden Sie in der folgenden Dokumentation:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Brilliert Identitäten zwischen Geräten und Systemen und verknüpft Datensätze anhand der Identitätsfelder, die von den XDM-Schemas definiert werden, mit denen sie übereinstimmen.
   * [Identitäts-Namespaces](../../identity-service/namespaces.md): Identitäts-Namespaces definieren die verschiedenen Arten von Identitätsinformationen, die sich auf eine einzelne Person beziehen können, und sind eine erforderliche Komponente für jedes Identitätsfeld.
* [Echtzeit-Kundenprofil](../../profile/home.md): Nutzen von Identitätsdiagrammen für Verbraucher, um einheitliche Verbraucherprofile auf der Grundlage aggregierter Daten aus mehreren Quellen bereitzustellen, die nahezu in Echtzeit aktualisiert werden.
* [Experience-Datenmodell (XDM)](../../xdm/home.md): Stellt Standarddefinitionen und -strukturen für Platform-Daten durch die Verwendung von Schemas bereit. Alle Platform-Datensätze entsprechen einem bestimmten XDM-Schema und das Schema definiert, welche Felder Identitäten sind.
   * [Identitätsfelder](../../xdm/ui/fields/identity.md): Erfahren Sie, wie ein Identitätsfeld in einem XDM-Schema definiert wird.

## Neue Anforderung erstellen

Um den Prozess zu starten, wählen Sie **[!UICONTROL Anforderung erstellen]** von der Hauptseite im Arbeitsbereich aus.

![Bild, das die [!UICONTROL Anforderung erstellen] Schaltfläche ausgewählt](../images/ui/delete-consumer/create-request-button.png)

Das Dialogfeld für die Anforderungserstellung wird angezeigt. Standardmäßig wird die **[!UICONTROL Verbraucher]** ist unter der Option **[!UICONTROL Aktion]** Abschnitt. Lassen Sie diese Option aktiviert.

![Bild mit der im Erstellungsdialogfeld ausgewählten Verbraucheroption](../images/ui/delete-consumer/consumer-action.png)

## Auswählen von Datensätzen

Unter dem **[!UICONTROL Kundendetails]** festzulegen, wird im nächsten Schritt bestimmt, ob Sie Verbraucherdaten aus einem oder allen Datensätzen löschen möchten.

Wenn Sie **[!UICONTROL Datensatz auswählen]** Wählen Sie das Datenbanksymbol (![Bild des Datenbanksymbols](../images/ui/delete-consumer/database-icon.png)) und ein Dialogfeld angezeigt, in dem Sie den gewünschten Datensatz aus der Liste auswählen können.

![Bild mit dem Dialogfeld für die Datensatzauswahl](../images/ui/delete-consumer/select-dataset.png)

Wenn Sie Verbraucherdaten aus allen Datensätzen löschen möchten, wählen Sie **[!UICONTROL Alle Datensätze]**.

![Bild, das die [!UICONTROL Alle Datensätze] Auswahl](../images/ui/delete-consumer/all-datasets.png)

>[!NOTE]
>
>Auswählen der **[!UICONTROL Alle Datensätze]** -Option kann dazu führen, dass der Löschvorgang länger dauert und möglicherweise nicht zu einer präzisen Löschung von Datensätzen führt.

## Kundenidentitäten bereitstellen {#provide-consumer-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Primäre Identität"
>abstract="Eine primäre Identität ist ein Attribut, das einen Datensatz mit dem Profil eines Verbrauchers in Experience Platform verknüpft. Das primäre Identitätsfeld für einen Datensatz wird durch das Schema definiert, auf dem der Datensatz basiert. In dieser Spalte müssen Sie den Typ (oder Namespace) für die primäre Identität des Kunden angeben, z. B. `email` für E-Mail-Adressen und `ecid` für Experience Cloud-IDs. Weitere Informationen finden Sie im Handbuch zur Benutzeroberfläche für Datenhygiene."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Identitätswert"
>abstract="In dieser Spalte müssen Sie den Wert für die primäre Identität des Kunden angeben, der dem in der linken Spalte angegebenen Identitätstyp entsprechen muss. Wenn der primäre Identitätstyp `email`, sollte der Wert die E-Mail-Adresse des Verbrauchers sein. Weitere Informationen finden Sie im Handbuch zur Benutzeroberfläche für Datenhygiene."

Beim Löschen von Verbraucherdaten müssen Sie Identitätsinformationen angeben, damit das System bestimmen kann, welche Datensätze gelöscht werden müssen. Für jeden Datensatz in Platform werden Datensätze basierend auf der Variablen **primäre Identität** -Feld, das durch das Schema des Datensatzes definiert wird.

Wie alle Identitätsfelder in Platform besteht eine primäre Identität aus zwei Elementen: a **type** (manchmal auch als Identitäts-Namespace bezeichnet) und ein **value**. Der Identitätstyp liefert Kontext dazu, wie das Feld einen Verbraucher identifiziert (z. B. eine E-Mail-Adresse), und der Wert stellt die spezifische Identität eines Verbrauchers für diesen Typ dar (z. B. `jdoe@example.com` für `email` Identitätstyp).  Zu den gebräuchlichen Feldern, die als Identitäten verwendet werden, gehören Kontoinformationen, Geräte-IDs und Cookie-IDs.

>[!TIP]
>
>Wenn Sie die primäre Identität für einen bestimmten Datensatz nicht kennen, können Sie ihn in der Platform-Benutzeroberfläche finden. Im **[!UICONTROL Datensätze]** Arbeitsbereich verwenden, wählen Sie den betreffenden Datensatz aus der Liste aus. Bewegen Sie auf der Detailseite für den Datensatz den Mauszeiger in der rechten Leiste über den Namen des Schemas des Datensatzes. Die primäre Identität wird zusammen mit dem Schemanamen und der Beschreibung angezeigt.
>
>![Bild, das die primäre Identität eines Datensatzes anzeigt und in der Benutzeroberfläche hervorgehoben ist](../images/ui/delete-consumer/dataset-primary-identity.png)

Wenn Sie Verbraucherdatensätze aus einem Datensatz löschen, müssen alle von Ihnen angegebenen Identitäten denselben Typ aufweisen, da ein Datensatz nur eine primäre Identität haben kann. Wenn Sie aus allen Datensätzen löschen, können Sie mehrere Identitätstypen einbeziehen, da verschiedene Datensätze unterschiedliche primäre Identitäten aufweisen können.

Beim Löschen von Verbraucherdatensätzen stehen zwei Optionen zur Verfügung:

* [JSON-Datei hochladen](#upload-json)
* [Manuelle Eingabe von Identitätswerten](#manual-identity)

### JSON-Datei hochladen {#upload-json}

Um eine JSON-Datei hochzuladen, können Sie die Datei per Drag-and-Drop in den Angebotbereich ziehen oder **[!UICONTROL Dateien auswählen]** , um in Ihrem lokalen Verzeichnis zu suchen und auszuwählen.

![Bild mit den Methoden zum Hochladen von JSON in der Benutzeroberfläche](../images/ui/delete-consumer/upload-json.png)

Die JSON-Datei muss als Array von Objekten formatiert sein, wobei jedes Objekt eine Verbraucheridentität darstellt.

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
| `value` | Die Identität des Verbrauchers, wie durch den Typ gekennzeichnet. |

Nach dem Hochladen der Datei können Sie fortfahren [Anfrage senden](#submit).

### Identitäten manuell eingeben {#manual-identity}

Um Identitäten manuell einzugeben, wählen Sie **[!UICONTROL Identität hinzufügen]**.

![Bild, das die [!UICONTROL Identität hinzufügen] Schaltfläche ausgewählt](../images/ui/delete-consumer/add-identity.png)

Es werden Steuerelemente angezeigt, mit denen Sie Verbraucher-Identitäten einzeln eingeben können. under **[!UICONTROL Primäre Identität]** verwenden, wählen Sie im Dropdown-Menü den Identitätstyp aus. under **[!UICONTROL Identitätswert]**, geben Sie den primären Identitätswert für den Verbraucher an.

![Bild mit einem manuell hinzugefügten Identitätsfeld](../images/ui/delete-consumer/identity-added.png)

Um weitere Identitäten hinzuzufügen, wählen Sie das Pluszeichen (![Bild des Pluszeichens](../images/ui/delete-consumer/plus-icon.png)) neben einer der Zeilen oder wählen Sie **[!UICONTROL Identität hinzufügen]**.

![Bild, das zeigt, wie der Anfrage weitere Identitäten hinzugefügt werden](../images/ui/delete-consumer/more-identities.png)

## Anfrage senden (#submit)

Nachdem Sie der Anforderung Identitäten hinzugefügt haben, wählen Sie **[!UICONTROL Einsenden]**.

![Bild, das die [!UICONTROL Einsenden] Schaltfläche ausgewählt](../images/ui/delete-consumer/submit.png)

Sie werden aufgefordert, die Liste der Identitäten zu bestätigen, deren Daten Sie löschen möchten. Auswählen **[!UICONTROL Einsenden]** um Ihre Auswahl zu bestätigen.

![Bild mit dem Bestätigungsdialogfeld](../images/ui/delete-consumer/confirm-request.png)

Nachdem die Anfrage gesendet wurde, wird eine Arbeitsreihenfolge erstellt und auf der [!UICONTROL Verbraucher] des [!UICONTROL Datenhygiene] Arbeitsbereich. Von hier aus können Sie den Status der Arbeitsreihenfolge bei der Verarbeitung der Anforderung überwachen. Die meisten Arbeitsaufträge zum Löschen von Daten für Verbraucher werden mehrere Tage in Anspruch nehmen.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie Verbraucherdatensätze in der Experience Platform-Benutzeroberfläche löschen. Weitere Informationen zur Durchführung anderer Datenhygieneaufgaben in der Benutzeroberfläche finden Sie im Abschnitt [Übersicht über die Benutzeroberfläche der Datenhygiene](./overview.md).

Informationen zum Löschen von Verbraucherdatensätzen mithilfe der Data Hygiene API finden Sie im Abschnitt [Endpunktleitfaden für Arbeitsaufträge](../api/workorder.md).
