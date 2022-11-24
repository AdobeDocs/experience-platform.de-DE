---
title: Übersicht über die Microsoft Azure-Erweiterung
description: Erfahren Sie mehr über die Microsoft Azure-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 7%

---

# [!DNL Microsoft Azure] Erweiterungsübersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

In [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) ist ein hochskalierbarer Echtzeit-Datenaufrufdienst, mit dem Sie die enormen Datenmengen, die von Ihren verbundenen Geräten und Anwendungen erzeugt werden, verarbeiten und analysieren können. Sobald Daten in einem Ereignis-Hub erfasst werden, können sie mithilfe eines beliebigen Echtzeit-Analytics-Anbieters oder von Batch-/Speicheradaptern umgewandelt und gespeichert werden.

Die [!DNL Microsoft Azure] [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) Erweiterungsnutzungen [!DNL Event Hubs] zum Senden von Ereignissen vom Adobe Experience Platform Edge Network an [!DNL Azure] zur weiteren Verarbeitung bestimmt. In diesem Handbuch wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel verwenden.

## Voraussetzungen

Um diese Erweiterung verwenden zu können, müssen Sie über eine gültige [!DNL Azure] Konto mit Zugriff auf [!DNL Event Hubs]. Sie müssen auch [Erstellen Sie einen Ereignis-Hub mit [!DNL Azure] portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) bevor Sie die folgenden Schritte ausführen.

## Installieren der Erweiterung

So installieren Sie Microsoft [!DNL Azure] Erweiterung, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL Ereignisweiterleitung]** über die linke Navigation. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, wählen Sie **[!UICONTROL Erweiterungen]** Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Katalog]** Registerkarte. Suchen Sie nach [!UICONTROL Microsoft Azure] Karte, und wählen Sie **[!UICONTROL Installieren]**.

![Die [!UICONTROL Installieren] für die [!UICONTROL Microsoft Azure] -Erweiterung in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/server/azure/install.png)

Da die Erweiterung über keine Konfigurationseigenschaften verfügt, wird sie sofort zur Liste der installierten Erweiterungen hinzugefügt. Sie können jetzt mit [!DNL Event Hub] Aktionstypen beim Konfigurieren von Ereignisweiterleitungsregeln.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Beginnen Sie mit der Erstellung einer neuen Ereignisweiterleitungsregel und konfigurieren Sie deren Bedingungen nach Bedarf. Wenn Sie die Aktionen für die Regel auswählen, wählen Sie **[!UICONTROL Microsoft Azure]** für die Erweiterung und wählen Sie dann **[!UICONTROL Senden von Daten an Ereignis-Hubs]** für den Aktionstyp.

![Die [!UICONTROL Senden von Daten an Ereignis-Hubs] Aktionstyp, der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt wird.](../../../images/extensions/server/azure/select-action-type.png)

Das rechte Bedienfeld wird aktualisiert und zeigt Konfigurationsoptionen für die Art und Weise an, wie die Daten gesendet werden sollen. Insbesondere müssen Sie [Datenelemente](../../../ui/managing-resources/data-elements.md) zu den verschiedenen Eigenschaften, die Ihre [!DNL Event Hub] Konfiguration.

![Die Konfigurationsoptionen für die [!UICONTROL Senden von Daten an Ereignis-Hubs] Aktionstyp, der in der Benutzeroberfläche angezeigt wird.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Ereignis-Hub-Details]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Namespace] | Der Name der [!DNL Event Hubs] Namespace, den Sie beim [Einrichten des Ereignis-Hub](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Name] | Der Name des Ereignis-Hub. |
| [!UICONTROL Name der SAS-Autorisierungsregel] | Der Name der Regel für die gemeinsame Zugriffsberechtigung für Ihre gesamte [!DNL Event Hubs] -Namespace oder die spezifische Ereignis-Hub-Instanz, an die Sie Daten senden möchten. Siehe den Anhang unter [Abrufen von SAS-Genehmigungswerten](#sas) für weitere Informationen. |
| [!UICONTROL SAS-Zugriffsschlüssel] | Der Primärschlüssel der Regel für die gemeinsame Zugriffsberechtigung für Ihre gesamte [!DNL Event Hubs] -Namespace oder die spezifische Ereignis-Hub-Instanz, an die Sie Daten senden möchten. Siehe den Anhang unter [Abrufen von SAS-Genehmigungswerten](#sas) für weitere Informationen. |
| [!UICONTROL Partition ID] | [!DNL Event Hubs] ermöglicht Ihnen Folgendes: [Ereignisse direkt an bestimmte Partitionen senden](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Um diese Funktion zu nutzen, geben Sie die Kennung der Partition an, die die Ereignisse empfangen soll. |

{style=&quot;table-layout:auto&quot;}

**Daten**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Payload] | Dieses Feld enthält die Daten, die an die [!DNL Event Hubs]. Die Daten können ein JSON-Objekt, eine Zeichenfolge oder ein Datenelement sein. |

{style=&quot;table-layout:auto&quot;}

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Änderungen beibehalten]** , um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]**.

Veröffentlichen Sie schließlich eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Daten an [!DNL Event Hubs] mithilfe der [!DNL Microsoft Azure] Ereignisweiterleitungserweiterung. Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie im Abschnitt [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).

## Anhang: Abrufen von SAS-Autorisierungswerten {#sas}

Externe Anwendungen erhalten Zugriff auf [!DNL Event Hubs] bis [freigegebene Zugriffssignaturen (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Jeder [!DNL Event Hubs] Bei der Erstellung wird automatisch eine standardmäßige SAS-Autorisierungsregel für Namespace- und Ereignis-Hub-Instanz zugewiesen. Sie können jedoch bei Bedarf auch zusätzliche Richtlinien für jede Ressource erstellen.

Wann [Konfigurieren einer Ereignisweiterleitungsregel](#rule) mithilfe der [!DNL Azure] -Erweiterung, müssen Sie den Namen und den Primärschlüssel für die Autorisierungsregel angeben, die für den Namespace oder spezifischen Ereignis-Hub gelten, an den Sie Daten senden möchten. Weitere Informationen zum Abrufen dieser Werte aus dem [!DNL Azure] Portal, siehe die folgenden Abschnitte in der [!DNL Azure] Dokumentation:

* [Abrufen von SAS-Werten für eine [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Abrufen von SAS-Werten für einen bestimmten Ereignis-Hub in einem Namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Sobald Sie über die erforderlichen Werte verfügen, kann der Name der Autorisierungsregel direkt als Zeichenfolge in der Konfigurationseingabe angegeben werden. Alternativ können Sie ein Datenelement vom Typ Zeichenfolge erstellen, um stattdessen darauf zu verweisen. Der Primärschlüssel muss jedoch zunächst in einem Ereignis-Weiterleitungsgeheimnis enthalten sein, bevor er in der Regelkonfiguration bereitgestellt werden kann, um Ihre Datensicherheit zu schützen.

In der Ereignisweiterleitungs-Benutzeroberfläche [Erstellen eines neuen Geheimnisses](../../../ui/event-forwarding/secrets.md) und wählen Sie **[!UICONTROL Token]** als geheimen Typ. Geben Sie für den Tokenwert selbst den Primärschlüssel an, den Sie zuvor kopiert haben. Erstellen Sie nach Erstellung des Geheimnisses ein Datenelement mit dem Typ **[!UICONTROL Geheimnis]** und wählen Sie die [!DNL Event Hubs] aus der Liste. Nachdem das geheime Datenelement eingerichtet wurde, können Sie dieses Datenelement im **[!UICONTROL SAS-Zugriffsschlüssel]** -Feld.
