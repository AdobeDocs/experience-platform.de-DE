---
keywords: Experience Platform;Startseite;beliebte Themen;
title: (Beta) Erstellen einer Adobe Workfront-Quellverbindung über die Benutzeroberfläche
description: In diesem Tutorial erfahren Sie, wie Sie eine Adobe Workfront-Quellverbindung erstellen, um Ihre Workfront-Daten mithilfe der Benutzeroberfläche an Adobe Experience Platform zu übertragen.
exl-id: f82e852a-c9d1-4ecc-bc54-2b39d3b4cc1e
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 98%

---

# (Beta) Erstellen einer Adobe Workfront-Quellverbindung über die Benutzeroberfläche

>[!NOTE]
>
>Die Adobe Workfront-Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

In diesem Tutorial erfahren Sie, wie Sie eine Adobe Workfront-Quellverbindung erstellen, um Ihre Workfront-Daten mithilfe der Benutzeroberfläche an Adobe Experience Platform zu übertragen.

## Erste Schritte

>[!IMPORTANT]
>
>Sie müssen in der Adobe Admin Console als Administrator konfiguriert sein, um auf die Workfront-Quelle zugreifen zu können.

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Erstellen einer Workfront-Quellverbindung über die Benutzeroberfläche

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der [!UICONTROL Katalog]-Bildschirm zeigt eine Vielzahl von Quellen an, die zum Erstellen eines Kontos verwendet werden können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Sie können auch die Suchleiste verwenden, um die angezeigten Quellen einzugrenzen.

Wählen Sie unter der Kategorie **[!UICONTROL Adobe-Programme]** das Programm **[!UICONTROL Adobe Workfront]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog, wobei die Adobe Workfront-Quelle hervorgehoben wurde.](../../../../images/tutorials/create/workfront/catalog.png)

## Daten auswählen

Der Schritt [!UICONTROL Daten auswählen] wird angezeigt. Hier müssen Sie Werte für Ihre Workfront-Subdomain und Daten-Domain angeben. Ihre Workfront-Subdomain entspricht der URL, die Sie für den Zugriff auf Ihre Workfront-Instanz verwenden, z. B. `https://acme.workfront.com/`, während Ihre Daten-Domain die zu verwendende Workfront-Umgebung darstellt.

Nachdem Sie Ihre Subdomain und Daten-Domain hinzugefügt haben, klicken Sie auf **[!UICONTROL Weiter]**.

![Die ausgewählte Datenseite mit Platzhalterwerten für Subdomain und Daten-Domain.](../../../../images/tutorials/create/workfront/select-data.png)

## Angeben von Datenflussdetails

Im Schritt „Datenflussdetails“ können Sie einen Namen und eine optionale Beschreibung für den Datenfluss angeben. In diesem Schritt können Sie auch Warnungen abonnieren, um Benachrichtigungen zum Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Tutorial [Abonnieren von Warnhinweisen zu Quellen über die Benutzeroberfläche](../../alerts.md).

Nachdem Sie Ihre Datenflussdetails angegeben und Ihre gewünschten Warnhinweiseinstellungen konfiguriert haben, klicken Sie auf **[!UICONTROL Weiter]**.

![Die Seite „Datenflussdetails“ mit Informationen zu Name, Beschreibung und Warnbenachrichtigungen von Datenflüssen](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## Überprüfung

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Die Überprüfungsseite mit einer Zusammenfassung der Verbindungsinformationen.](../../../../images/tutorials/create/workfront/review.png)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zur Workfront-Quelle.

### Workfront-Schema für Änderungsereignisse

Workfront-Daten in Platform werden als Datensatzdaten aus Zeitreihen dargestellt, wobei jede Zeile in den Daten einen Zeitstempel aufweist, der anzeigt, wann das Ereignis aufgetreten ist und welche Attribute mit diesem Ereignis verbunden sind.

Während der Einrichtung wird ein Schema mit dem Namen „Workfront-Änderungsereignisse aus Fluss“ erstellt.

| Schemafeld | Beschreibung |
| --- | --- |
| `timestamp` | Der Zeitpunkt, zu dem das ausgewählte Ereignis aufgetreten ist. Der Zeitstempel wird in der Zeitzone GMT dargestellt. |
| `_workfront.objectType` | Der Objekttyp. Zu den verfügbaren Werten gehören `project`, `task`, `portfolio` und andere, je nach dem Objekt, das geändert oder erstellt wurde. |
| `_workfront.objectID` | Die ID, die dem Objekttyp entspricht. |
| `_workfront.created` | Dieser Wert wird auf `1` gesetzt, wenn das Ereignis eine Objekterstellung darstellt. |
| `_workfront.deleted` | Dieser Wert wird auf `1` gesetzt, wenn das Objekt gelöscht wird. |
| `_worfkront.updated` | Dieser Wert wird auf `1` gesetzt, wenn das Objekt aktualisiert wird. |
| `_workfront.completed` | Dieser Wert wird auf `1` gesetzt, wenn das Objekt als abgeschlossen markiert ist. |
| `_workfront.parentObjectType` | (Optional) Der Objekttyp, der dem übergeordneten Objekt des Objekts entspricht. |
| `_workfront.parentID` | Die ID des übergeordneten Objekts. |
| `_workfront.customData` | Eine Zuordnung aller benutzerdefinierten Formularfelder und Werte, die während des Ereignisses ausgefüllt werden. |

>[!IMPORTANT]
>
>Es werden nur Attribute ausgefüllt, die sich geändert haben oder die im Rahmen eines Ereignisses erstellt wurden. Wenn Sie beispielsweise nur den Namen des Objekts ändern, werden nur folgende Felder ausgefüllt:<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## Nächste Schritte

In diesem Tutorial haben Sie jetzt einen Datenfluss erstellt, um Ihre Daten von Workfront in Experience Platform zu übertragen. Sie können jetzt Services wie den [Abfrage-Service](../../../../../query-service/home.md) verwenden, um weitere Analysen Ihrer Daten durchzuführen. Weitere Informationen zu Workfront finden Sie im Abschnitt [Workfront – Übersicht](../../../../connectors/adobe-applications/workfront.md).
