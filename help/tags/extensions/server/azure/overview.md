---
title: Übersicht über die Microsoft Azure-Erweiterung
description: Erfahren Sie mehr über die Microsoft Azure-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 7%

---

# Übersicht über die [!DNL Microsoft Azure]-Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

In [!DNL Microsoft Azure] ist [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) ein hochskalierbarer Echtzeit-Datenaufrufdienst, mit dem Sie die enormen Datenmengen, die von Ihren verbundenen Geräten und Anwendungen erzeugt werden, verarbeiten und analysieren können. Sobald Daten in einem Ereignis-Hub erfasst werden, können sie mithilfe eines beliebigen Echtzeit-Analytics-Anbieters oder von Batch-/Speicheradaptern umgewandelt und gespeichert werden.

Die Erweiterung [!DNL Microsoft Azure] [ Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) nutzt [!DNL Event Hubs], um Ereignisse vom Adobe Experience Platform-Edge Network zur weiteren Verarbeitung an [!DNL Azure] zu senden. In diesem Handbuch wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel verwenden.

## Voraussetzungen

Um diese Erweiterung verwenden zu können, müssen Sie über ein gültiges [!DNL Azure]-Konto mit Zugriff auf [!DNL Event Hubs] verfügen. Sie müssen auch [einen Ereignis-Hub mithilfe des [!DNL Azure] Portals](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) erstellen, bevor Sie die folgenden Schritte ausführen.

## Installieren der Erweiterung

Um die Microsoft [!DNL Azure] -Erweiterung zu installieren, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder Experience Platform-Benutzeroberfläche und wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Ereignisweiterleitung]** aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, wählen Sie im linken Navigationsbereich **[!UICONTROL Erweiterungen]** und dann die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie nach der Karte [!UICONTROL Microsoft Azure] und wählen Sie dann **[!UICONTROL Install]** aus.

![Die Schaltfläche [!UICONTROL Installieren], die für die Erweiterung [!UICONTROL Microsoft Azure] in der Datenerfassungs-Benutzeroberfläche ausgewählt ist.](../../../images/extensions/server/azure/install.png)

Da die Erweiterung über keine Konfigurationseigenschaften verfügt, wird sie sofort zur Liste der installierten Erweiterungen hinzugefügt. Jetzt können Sie bei der Konfiguration von Ereignisweiterleitungsregeln mit der Verwendung von [!DNL Event Hub] -Aktionstypen beginnen.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Beginnen Sie mit der Erstellung einer neuen Ereignisweiterleitungsregel und konfigurieren Sie deren Bedingungen nach Bedarf. Wählen Sie bei der Auswahl der Aktionen für die Regel **[!UICONTROL Microsoft Azure]** für die Erweiterung und dann für den Aktionstyp **[!UICONTROL Daten an Ereignis-Hubs senden]** .

![Der Aktionstyp [!UICONTROL Daten an Ereignis-Hubs senden] wurde für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt.](../../../images/extensions/server/azure/select-action-type.png)

Das rechte Bedienfeld wird aktualisiert und zeigt Konfigurationsoptionen für die Art und Weise an, wie die Daten gesendet werden sollen. Insbesondere müssen Sie den verschiedenen Eigenschaften, die Ihre [!DNL Event Hub] -Konfiguration darstellen, [Datenelemente](../../../ui/managing-resources/data-elements.md) zuweisen.

![Die Konfigurationsoptionen für den Aktionstyp [!UICONTROL Daten an Ereignis-Hubs senden] , der in der Benutzeroberfläche angezeigt wird.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Ereignis-Hub-Details]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Namespace] | Der Name des Namespace [!DNL Event Hubs] , den Sie beim [Einrichten des Ereignis-Hub](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) erstellt haben. |
| [!UICONTROL Name] | Der Name des Ereignis-Hub. |
| [!UICONTROL Name der SAS-Autorisierungsregel] | Der Name der Regel für die gemeinsame Zugriffsberechtigung für Ihren gesamten [!DNL Event Hubs]-Namespace oder die spezifische Ereignis-Hub-Instanz, an die Sie Daten senden möchten. Weitere Informationen finden Sie im Anhang zu [Abrufen von SAS-Autorisierungswerten](#sas) . |
| [!UICONTROL SAS-Zugriffsschlüssel] | Der Primärschlüssel der Regel für die gemeinsame Zugriffsberechtigung für den gesamten [!DNL Event Hubs]-Namespace oder die spezifische Ereignis-Hub-Instanz, an die Sie Daten senden möchten. Weitere Informationen finden Sie im Anhang zu [Abrufen von SAS-Autorisierungswerten](#sas) . |
| [!UICONTROL Partitions-ID] | Mit [!DNL Event Hubs] können Sie [Ereignisse direkt an bestimmte Partitionen senden](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Um diese Funktion zu nutzen, geben Sie die Kennung der Partition an, die die Ereignisse empfangen soll. |

{style="table-layout:auto"}

**Daten**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Payload] | Dieses Feld enthält die Daten, die an den [!DNL Event Hubs] weitergeleitet werden. Die Daten können ein JSON-Objekt, eine Zeichenfolge oder ein Datenelement sein. |

{style="table-layout:auto"}

Wählen Sie nach Abschluss **[!UICONTROL Änderungen beibehalten]** aus, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

Veröffentlichen Sie abschließend eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Daten mit der Ereignisweiterleitungs-Erweiterung [!DNL Microsoft Azure] an [!DNL Event Hubs] gesendet werden. Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie in der [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).

## Anhang: Abrufen von SAS-Genehmigungswerten {#sas}

Externe Anwendungen erhalten Zugriff auf [!DNL Event Hubs] über [freigegebene Zugriffssignaturen (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Für jeden [!DNL Event Hubs] -Namespace und jede Ereignis-Hub-Instanz wird automatisch eine standardmäßige SAS-Autorisierungsregel zugewiesen. Sie können jedoch bei Bedarf auch zusätzliche Richtlinien für jede Ressource erstellen.

Beim [ Konfigurieren einer Ereignisweiterleitungsregel](#rule) mithilfe der Erweiterung [!DNL Azure] müssen Sie den Namen und den Primärschlüssel für die Autorisierungsregel angeben, die für den Namespace oder spezifischen Ereignis-Hub gilt, an den Sie Daten senden möchten. Weitere Informationen zum Abrufen dieser Werte aus dem Portal [!DNL Azure] finden Sie in den folgenden Abschnitten der Dokumentation zu [!DNL Azure]:

* [Abrufen von SAS-Werten für einen  [!DNL Event Hubs] Namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Abrufen von SAS-Werten für einen bestimmten Ereignis-Hub in einem Namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Sobald Sie über die erforderlichen Werte verfügen, kann der Name der Autorisierungsregel direkt als Zeichenfolge in der Konfigurationseingabe angegeben werden. Alternativ können Sie ein Datenelement vom Typ Zeichenfolge erstellen, um stattdessen darauf zu verweisen. Der Primärschlüssel muss jedoch zunächst in einem Ereignis-Weiterleitungsgeheimnis enthalten sein, bevor er in der Regelkonfiguration bereitgestellt werden kann, um Ihre Datensicherheit zu schützen.

Erstellen Sie in der Ereignisweiterleitungs-Benutzeroberfläche [ein neues Geheimnis](../../../ui/event-forwarding/secrets.md) und wählen Sie **[!UICONTROL Token]** als geheimen Typ aus. Geben Sie für den Tokenwert selbst den Primärschlüssel an, den Sie zuvor kopiert haben. Erstellen Sie nach dem Erstellen des Geheimnisses ein Datenelement mit dem Typ **[!UICONTROL Geheimnis]** und wählen Sie das Geheimnis [!DNL Event Hubs] aus der Liste aus. Nachdem das geheime Datenelement eingerichtet wurde, können Sie dieses Datenelement im Feld **[!UICONTROL SAS-Zugriffsschlüssel]** referenzieren.
