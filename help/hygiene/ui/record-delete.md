---
title: Datensätze löschen
description: Erfahren Sie, wie Sie Datensätze in der Benutzeroberfläche von Adobe Experience Platform löschen.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 67%

---

# Löschen von Datensätzen

Die [[!UICONTROL Datenhygiene] Arbeitsbereich](./overview.md) in der Adobe Experience Platform-Benutzeroberfläche können Sie Datensätze löschen, die am Identity Service und Echtzeit-Kundenprofil teilnehmen. Diese Datensätze können an einzelne Verbraucher oder eine andere Entität gebunden werden, die im Identitätsdiagramm enthalten ist.

>[!IMPORTANT]
>
>Löschanfragen von Datensätzen stehen nur für Unternehmen zur Verfügung, die **Adobe Gesundheitsschild**.
>
>
>Löschvorgänge von Datensätzen dienen zur Datenbereinigung, zum Entfernen anonymer Daten oder zur Datenminimierung. Sie dürfen **nicht** für Anfragen zu den Rechten der betroffenen Personen (Compliance) verwendet werden, da sie sich auf Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) beziehen. Verwenden Sie stattdessen [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) für alle Compliance-Anwendungsfälle.

## Voraussetzungen

Das Löschen von Datensätzen setzt ein Verständnis der Funktionsweise von Identitätsfeldern in Experience Platform voraus. Insbesondere müssen Sie die primären Identitätswerte der Entitäten kennen, deren Datensätze Sie löschen möchten, je nach Datensatz (oder Datensätzen), aus dem Sie sie löschen.

Weitere Informationen zu Identitäten in Platform finden Sie in der folgenden Dokumentation:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Führt Identitäten zwischen Geräten und Systemen zusammen und verknüpft Datensätze anhand der Identitätsfelder, die von den entsprechenden XDM-Schemas definiert werden.
   * [Identity-Namespaces](../../identity-service/namespaces.md): In Identity-Namespaces werden die verschiedenen Arten von Identitätsinformationen definiert, die sich auf eine einzelne Person beziehen können. Sie sind eine erforderliche Komponente für jedes Identitätsfeld.
* [Echtzeit-Kundenprofil](../../profile/home.md): Nutzt Identitätsdiagramme, um einheitliche Verbraucherprofile auf der Grundlage aggregierter Daten aus mehreren Quellen bereitzustellen, die nahezu in Echtzeit aktualisiert werden.
* [Experience-Datenmodell (XDM)](../../xdm/home.md): Stellt Standarddefinitionen und -strukturen für Platform-Daten durch die Verwendung von Schemas bereit. Alle Platform-Datensätze entsprechen einem bestimmten XDM-Schema und das Schema definiert, welche Felder Identitäten sind.
   * [Identitätsfelder](../../xdm/ui/fields/identity.md): Erfahren Sie, wie ein Identitätsfeld in einem XDM-Schema definiert wird.

## Erstellen einer neuen Anfrage

Wählen Sie zunächst auf der Hauptseite im Arbeitsbereich die Option **[!UICONTROL Anfrage erstellen]** aus.

![Bild, das die ausgewählte Schaltfläche [!UICONTROL Anfrage erstellen] zeigt](../images/ui/record-delete/create-request-button.png)

Daraufhin öffnet sich das Dialogfeld für die Anfrageerstellung. Standardmäßig wird die **[!UICONTROL Verbraucher löschen]** ist unter der Option **[!UICONTROL Angeforderte Aktion]** Abschnitt. Lassen Sie diese Option aktiviert.

![Bild mit der im Erstellungsdialogfeld ausgewählten Option zum Löschen des Verbrauchers](../images/ui/record-delete/consumer-action.png)

## Auswählen von Datensätzen

Unter dem **[!UICONTROL Kundendetails]** festzulegen, wird im nächsten Schritt bestimmt, ob Sie Datensätze aus einem oder allen Datensätzen löschen möchten.

Wenn Sie **[!UICONTROL Datensatz auswählen]** auswählen, wird das Datenbanksymbol (![Bild des Datenbanksymbols](../images/ui/record-delete/database-icon.png)) angezeigt und ein Dialogfeld öffnet sich, in dem Sie den gewünschten Datensatz aus der Liste auswählen können.

![Bild mit dem Dialogfeld für die Datensatzauswahl](../images/ui/record-delete/select-dataset.png)

Wenn Sie Datensätze aus allen Datensätzen löschen möchten, wählen Sie **[!UICONTROL Alle Datensätze]**.

![Bild, das die ausgewählte Option [!UICONTROL Alle Datensätze] zeigt](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Wenn Sie die Option **[!UICONTROL Alle Datensätze]** auswählen, kann es sein, dass der Löschvorgang länger dauert und möglicherweise nicht zu einer korrekten Löschung der Datensätze führt.

## Identitäten bereitstellen {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Primäre Identität"
>abstract="Eine primäre Identität ist ein Attribut, das einen Datensatz mit dem Profil eines Verbrauchers in Experience Platform verknüpft. Das Feld für die primäre Identität für einen Datensatz wird durch das Schema definiert, auf dem der Datensatz basiert. In dieser Spalte müssen Sie den Typ (oder Namespace) der primären Identität des Datensatzes angeben, z. B. `email` für E-Mail-Adressen und `ecid` für Experience Cloud IDs. Weitere Informationen finden Sie im Handbuch zur Datenhygiene-Benutzeroberfläche."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Identitätswert"
>abstract="In dieser Spalte müssen Sie den Wert für die primäre Identität des Datensatzes angeben, der dem in der linken Spalte angegebenen Identitätstyp entsprechen muss. Wenn der primäre Identitätstyp `email` ist, sollte der Wert die E-Mail-Adresse des Datensatzes sein. Weitere Informationen finden Sie im Handbuch zur Datenhygiene-Benutzeroberfläche."

Beim Löschen von Datensätzen müssen Sie Identitätsdaten angeben, damit das System bestimmen kann, welche Datensätze gelöscht werden müssen. Für jeden Datensatz in Platform werden Daten basierend auf dem Feld **primäre Identität** gelöscht, das durch das Schema des Datensatzes definiert wird.

Wie alle Identitätsfelder in Platform besteht eine primäre Identität aus zwei Elementen: einem **Typ** (manchmal auch als Identity-Namespace bezeichnet) und einem **Wert**. Der Identitätstyp liefert Kontext dazu, wie das Feld einen Datensatz identifiziert (z. B. eine E-Mail-Adresse) und der Wert stellt die spezifische Identität eines Datensatzes für diesen Typ dar (z. B. `jdoe@example.com` für `email` Identitätstyp). Felder, die häufig als Identitäten verwendet werden, sind Kontoinformationen, Geräte-IDs und Cookie-IDs.

>[!TIP]
>
>Wenn Sie die primäre Identität für einen bestimmten Datensatz nicht kennen, können Sie sie in der Platform-Benutzeroberfläche ermitteln. Wählen Sie dazu im Arbeitsbereich **[!UICONTROL Datensätze]** den betreffenden Datensatz aus der Liste aus. Bewegen Sie auf der Detailseite für den Datensatz den Mauszeiger in der rechten Leiste über den Namen des Datensatzschemas. Die primäre Identität wird zusammen mit dem Schemanamen und der Beschreibung angezeigt.
>
>![Bild mit primärer Identität eines Datensatzes, die in der Benutzeroberfläche hervorgehoben ist](../images/ui/record-delete/dataset-primary-identity.png)

Wenn Sie Datensätze aus einem Datensatz löschen, müssen alle von Ihnen angegebenen Identitäten denselben Typ aufweisen, da ein Datensatz nur eine primäre Identität aufweisen kann. Wenn Sie sie aus allen Datensätzen löschen, können Sie mehrere Identitätstypen einbeziehen, da verschiedene Datensätze unterschiedliche primäre Identitäten haben können.

Beim Löschen von Datensätzen stehen zwei Optionen zur Verfügung:

* [Hochladen einer JSON-Datei](#upload-json)
* [Manuelle Eingabe von Identitätswerten](#manual-identity)

### Hochladen einer JSON-Datei {#upload-json}

Um eine JSON-Datei hochzuladen, können Sie die Datei per Drag-and-Drop in den entsprechenden Bereich ziehen oder **[!UICONTROL Dateien auswählen]** wählen, um die Datei in Ihrem lokalen Verzeichnis zu suchen und auszuwählen.

![Bild mit den Methoden zum Hochladen von JSON in der Benutzeroberfläche](../images/ui/record-delete/upload-json.png)

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

### Manuelle Eingabe von Identitätswerten {#manual-identity}

Um Identitäten manuell einzugeben, wählen Sie **[!UICONTROL Identität hinzufügen]** aus.

![Bild, das die ausgewählte Schaltfläche [!UICONTROL Identität hinzufügen] zeigt](../images/ui/record-delete/add-identity.png)

Es werden Steuerelemente angezeigt, mit denen Sie Identitäten einzeln eingeben können. Wählen Sie unter **[!UICONTROL Primäre Identität]** im Dropdown-Menü den Identitätstyp aus. under **[!UICONTROL Identitätswert]**, geben Sie den primären Identitätswert für den Datensatz an.

![Bild mit einem manuell hinzugefügten Identitätsfeld](../images/ui/record-delete/identity-added.png)

Um weitere Identitäten hinzuzufügen, wählen Sie das Pluszeichen (![Bild des Pluszeichens](../images/ui/record-delete/plus-icon.png)) neben einer der Zeilen oder wählen Sie **[!UICONTROL Identität hinzufügen]** aus.

![Bild, das zeigt, wie der Anfrage weitere Identitäten hinzugefügt werden](../images/ui/record-delete/more-identities.png)

## Senden der Anfrage (#submit)

Nachdem Sie unter **[!UICONTROL Anfrageeinstellungen]** die Identitäten zur Anfrage hinzugefügt haben, geben Sie einen Namen und eine optionale Beschreibung für die Anfrage ein, bevor Sie **[!UICONTROL Senden]** auswählen.

![Bild, das die ausgewählte Schaltfläche [!UICONTROL Senden] zeigt](../images/ui/record-delete/submit.png)

Sie werden aufgefordert, die Liste der Identitäten zu bestätigen, deren Daten Sie löschen möchten. Wählen Sie **[!UICONTROL Senden]** aus, um Ihre Auswahl zu bestätigen.

![Bild mit dem Bestätigungsdialogfeld](../images/ui/record-delete/confirm-request.png)

Nachdem die Anfrage gesendet wurde, wird ein Arbeitsauftrag erstellt, der auf der Registerkarte [!UICONTROL Verbraucher] des Arbeitsbereichs [!UICONTROL Datenhygiene] angezeigt wird. Hier können Sie den Fortschritt des Arbeitsauftrags überwachen.

>[!NOTE]
>
>Siehe Abschnitt Übersicht unter [Fristen und Transparenz](../home.md#record-delete-transparency) für Details darüber, wie Löschvorgänge von Datensätzen nach der Ausführung verarbeitet werden.

## Nächste Schritte

In diesem Dokument wurde das Löschen von Datensätzen in der Experience Platform-Benutzeroberfläche beschrieben. Weitere Informationen zur Durchführung anderer Datenhygiene-Aufgaben in der Benutzeroberfläche finden Sie im Abschnitt [Übersicht über die Datenhygiene-Benutzeroberfläche](./overview.md).

Informationen zum Löschen von Datensätzen mithilfe der Data Hygiene API finden Sie im Abschnitt [Endpunktleitfaden für Arbeitsaufträge](../api/workorder.md).
