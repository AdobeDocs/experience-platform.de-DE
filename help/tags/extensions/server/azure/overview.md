---
title: Microsoft Azure-Erweiterung - Übersicht
description: Erfahren Sie mehr über die Microsoft Azure-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 2%

---

# [!DNL Microsoft Azure] - Übersicht

[!DNL Microsoft Azure] ist [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) ein hochgradig skalierbarer Echtzeit-Dateneingabe-Service, mit dem Sie die gewaltigen Datenmengen verarbeiten und analysieren können, die von Ihren verbundenen Geräten und Anwendungen erzeugt werden. Sobald Daten in einem Ereignis-Hub erfasst wurden, können sie mithilfe eines beliebigen Echtzeit-Analyseanbieters oder Batch-/Speicheradapters transformiert und gespeichert werden.

Die [!DNL Microsoft Azure] [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) nutzt [!DNL Event Hubs], um Ereignisse aus der Adobe Experience Platform Edge Network zur weiteren Verarbeitung an [!DNL Azure] zu senden. In diesem Handbuch wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel verwenden.

## Voraussetzungen

Um diese Erweiterung verwenden zu können, müssen Sie über ein gültiges [!DNL Azure] mit Zugriff auf [!DNL Event Hubs] verfügen. Sie müssen auch [einen Event Hub mit dem  [!DNL Azure] -Portal erstellen](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) bevor Sie die folgenden Schritte ausführen.

## Installieren der Erweiterung

Um die Microsoft [!DNL Azure]-Erweiterung zu installieren, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder zur Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL Event Forwarding]** in der linken Navigationsleiste aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Extensions]** und wählen Sie dann die Registerkarte **[!UICONTROL Catalog]** aus. Suchen Sie nach der Karte [!UICONTROL Microsoft Azure] und klicken Sie dann auf **[!UICONTROL Install]**.

![Die ausgewählte [!UICONTROL Install]-Schaltfläche für die [!UICONTROL Microsoft Azure]-Erweiterung in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/server/azure/install.png)

Da die Erweiterung über keine Konfigurationseigenschaften verfügt, wird sie sofort der Liste der installierten Erweiterungen hinzugefügt. Sie können jetzt [!DNL Event Hub] Aktionstypen beim Konfigurieren von Regeln für die Ereignisweiterleitung verwenden.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Beginnen Sie mit der Erstellung einer neuen Ereignisweiterleitungsregel und konfigurieren Sie deren Bedingungen nach Bedarf. Wählen Sie bei der Auswahl der Aktionen für die Regel die Option **[!UICONTROL Microsoft Azure]** für die Erweiterung und dann **[!UICONTROL Send Data to Event Hubs]** für Aktionstyp aus.

![Der [!UICONTROL Send Data to Event Hubs] Aktionstyp, der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt wird.](../../../images/extensions/server/azure/select-action-type.png)

Das rechte Bedienfeld wird aktualisiert und zeigt Konfigurationsoptionen dazu an, wie die Daten gesendet werden sollen. Insbesondere müssen Sie den verschiedenen Eigenschaften[&#x200B; die Ihre &#x200B;](../../../ui/managing-resources/data-elements.md)-Konfiguration repräsentieren[!DNL Event Hub] „Datenelemente“ zuweisen.

![Die Konfigurationsoptionen für den [!UICONTROL Send Data to Event Hubs] Aktionstyp werden in der Benutzeroberfläche angezeigt.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Namespace] | Der Name des [!DNL Event Hubs]-Namespace, den Sie beim Einrichten [&#x200B; Ereignis-Hub erstellt &#x200B;](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Name] | Der Name des Ereignis-Hub. |
| [!UICONTROL SAS Authorization Rule Name] | Der Name der freigegebenen Zugriffsautorisierungsregel für den gesamten [!DNL Event Hubs]-Namespace oder die spezifische Ereignis-Hub-Instanz, an die Sie Daten senden möchten. Weitere Informationen finden Sie im Anhang zum [&#x200B; von SAS](#sas)Autorisierungswerten . |
| [!UICONTROL SAS Access Key] | Der Primärschlüssel der freigegebenen Zugriffsautorisierungsregel für den gesamten [!DNL Event Hubs]-Namespace oder die spezifische Event-Hub-Instanz, an die Daten gesendet werden sollen. Weitere Informationen finden Sie im Anhang zum [&#x200B; von SAS](#sas)Autorisierungswerten . |
| [!UICONTROL Partition ID] | [!DNL Event Hubs] können Sie [Ereignisse direkt an bestimmte Partitionen senden](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Um diese Funktion zu nutzen, geben Sie die ID der Partition an, die Sie die Ereignisse empfangen möchten. |

{style="table-layout:auto"}

**Daten**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Payload] | Dieses Feld enthält die Daten, die an den [!DNL Event Hubs] weitergeleitet werden. Die Daten können ein JSON-Objekt, eine Zeichenfolge oder ein Datenelement sein. |

{style="table-layout:auto"}

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Keep Changes]** aus, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL Save to Library]** aus.

Veröffentlichen Sie abschließend eine neue Ereignisweiterleitung [Build](../../../ui/publishing/builds.md), um die Änderungen an der Bibliothek zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Daten mithilfe der Erweiterung für die [!DNL Event Hubs]-Ereignisweiterleitung an [!DNL Microsoft Azure] senden. Weitere Informationen zu den Funktionen für die Ereignisweiterleitung in Experience Platform finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).

## Anhang: SAS-Autorisierungswerte abrufen {#sas}

Externen Anwendungen wird der Zugriff auf [!DNL Event Hubs] über [Shared Access Signatures (SAS)) &#x200B;](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Für jede [!DNL Event Hubs]-Namespace- und Ereignis-Hub-Instanz wird bei der Erstellung automatisch eine standardmäßige SAS-Autorisierungsregel zugewiesen. Sie können jedoch bei Bedarf auch zusätzliche Richtlinien für jede Ressource erstellen.

Beim [Konfigurieren einer Ereignisweiterleitungsregel](#rule) mithilfe der [!DNL Azure]-Erweiterung müssen Sie den Namen und den Primärschlüssel für die Autorisierungsregel angeben, die den Namespace oder den spezifischen Ereignis-Hub steuert, an den Sie Daten senden möchten. Weitere Informationen zum Abrufen dieser Werte aus dem [!DNL Azure]-Portal finden Sie in den folgenden Abschnitten in der [!DNL Azure]-Dokumentation:

* [Erhalten von SAS-Werten für einen [!DNL Event Hubs] Namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [SAS-Werte für einen bestimmten Ereignis-Hub in einem Namespace abrufen](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Sobald Sie über die erforderlichen Werte verfügen, kann der Name der Autorisierungsregel direkt als Zeichenfolge in der Konfigurationseingabe bereitgestellt werden oder Sie können ein Datenelement vom Typ Zeichenfolge erstellen, um stattdessen darauf zu verweisen. Der Primärschlüssel muss jedoch zunächst in einem Geheimnis für die Ereignisweiterleitung enthalten sein, bevor er in der Regelkonfiguration bereitgestellt werden kann, um die Datensicherheit zu gewährleisten.

Wählen Sie in der Benutzeroberfläche [&#x200B; Ereignisweiterleitung die Option „Neue geheimen Daten erstellen](../../../ui/event-forwarding/secrets.md) und als Typ der geheimen Daten **[!UICONTROL Token]** aus. Geben Sie für den Token-Wert selbst den Primärschlüssel an, den Sie zuvor kopiert haben. Erstellen Sie nach dem Erstellen der geheimen Daten ein Datenelement vom Typ **[!UICONTROL Secret]** und wählen Sie das [!DNL Event Hubs] Geheimnis aus der Liste aus. Nachdem das Geheime-Daten-Datenelement eingerichtet wurde, können Sie auf dieses Datenelement im **[!UICONTROL SAS Access Key]** verweisen.
