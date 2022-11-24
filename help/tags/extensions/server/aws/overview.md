---
title: Übersicht über die AWS-Erweiterung
description: Erfahren Sie mehr über die AWS-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 8%

---

# [!DNL AWS] Erweiterungsübersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) ist eine Cloud-Computing-Plattform, die eine breite Palette von Diensten anbietet, wie z. B. dezentrales Computing, Datenbankspeicherung, Inhaltsbereitstellung und Customer Relationship Management (CRM).

Die [!DNL AWS] [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) Erweiterungsnutzungen [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) zum Senden von Ereignissen vom Adobe Experience Platform Edge Network an [!DNL AWS] zur weiteren Verarbeitung bestimmt. In diesem Handbuch wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel verwenden.

## Voraussetzungen

Sie müssen über eine [!DNL AWS] -Konto [!DNL Kinesis] Datenstrom, um diese Erweiterung zu verwenden. Wenn Sie keinen bereits vorhandenen Datenstrom haben, finden Sie weitere Informationen unter [!DNL AWS] Dokumentation zu [Erstellen eines neuen Datenstreams mit der [!DNL AWS] Verwaltungskonsole](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Installieren der Erweiterung {#install}

So installieren Sie die [!DNL AWS] Erweiterung, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL Ereignisweiterleitung]** über die linke Navigation. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, wählen Sie **[!UICONTROL Erweiterungen]** Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Katalog]** Registerkarte. Suchen Sie nach [!UICONTROL AWS] Karte, und wählen Sie **[!UICONTROL Installieren]**.

![Die [!UICONTROL Installieren] für die [!UICONTROL AWS] -Erweiterung in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/server/aws/install.png)

Im nächsten Bildschirm müssen Sie die Anmeldedaten für die Verbindung für Ihre [!DNL AWS] -Konto. Insbesondere müssen Sie Ihre [!DNL AWS] Zugriffsschlüssel-ID und geheimer Zugriffsschlüssel. Wenn Sie diese Werte nicht kennen, lesen Sie den Abschnitt [!DNL AWS] Dokumentation zu [Erhalten der Zugriffsschlüssel-ID und des geheimen Zugriffsschlüssels](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![Die Zugriffsschlüssel-ID und der geheime Zugriffsschlüssel, die in der Erweiterungskonfigurationsansicht hinzugefügt wurden.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Eine Zugriffsrichtlinie muss an die [!DNL AWS] -Konto, das zum Generieren der Zugriffsberechtigungen verwendet wird. Diese Richtlinie muss so konfiguriert sein, dass Zugriffsberechtigungen zum Senden von Daten an die [!DNL Kinesis] Datenstrom. Siehe **Beispiel 2** im [!DNL AWS] Dokument auf [Beispielrichtlinien für [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) , um zu sehen, wie die Richtlinie definiert werden sollte.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]** und die Erweiterung installiert ist.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitung. [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen nach Bedarf. Wählen Sie beim Konfigurieren der Aktionen für die Regel die **[!UICONTROL AWS]** Erweiterung und wählen Sie **[!UICONTROL Senden von Daten an den Kinesis-Daten-Stream]** für den Aktionstyp.

![Die [!UICONTROL Senden von Daten an den Kinesis-Daten-Stream] Aktionstyp, der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt wird.](../../../images/extensions/server/aws/select-action-type.png)

Das rechte Bedienfeld wird aktualisiert und zeigt Konfigurationsoptionen für die Art und Weise an, wie die Daten gesendet werden sollen. Insbesondere müssen Sie [Datenelemente](../../../ui/managing-resources/data-elements.md) zu den verschiedenen Eigenschaften, die Ihre [!DNL Event Hub] Konfiguration.

![Die Konfigurationsoptionen für die [!UICONTROL Senden von Daten an den Kinesis-Daten-Stream] Aktionstyp, der in der Benutzeroberfläche angezeigt wird.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis Data Stream-Details]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Stream-Name] | Der Name des Streams, an den diese Ereignisweiterleitungsregel Datendatensätze sendet. |
| [!UICONTROL AWS-Region] | Die [!DNL AWS] Region, in der [!DNL Kinesis] Datenstrom erstellt. |
| [!UICONTROL Partition Key] | Die [partition key](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) , die die Erweiterung beim Senden von Daten an den Datenstrom verwendet.<br><br>[!DNL Kinesis Data Streams] Trennt die zu einem Stream gehörenden Datendatensätze in mehrere Shards. Es verwendet den mit jedem Datensatz gesendeten Partitionsschlüssel, um zu bestimmen, zu welchem Teil ein bestimmter Datensatz gehört.<br><br>Ein guter Partitionsschlüssel für die Verteilung von Kunden kann die Kundennummer sein, da sie für jeden Kunden unterschiedlich ist. Ein schlechter Partitionsschlüssel könnte ihre Postleitzahl haben, da sie alle in der Nähe leben können. Im Allgemeinen sollten Sie einen Partitionsschlüssel wählen, der den höchsten Bereich unterschiedlicher potenzieller Werte aufweist. Siehe [!DNL AWS] Artikel zu [Skalieren [!DNL Kinesis] Datenströme](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) für Best Practices bei der Verwaltung von Partitionsschlüsseln. |

{style=&quot;table-layout:auto&quot;}

**[!UICONTROL Daten]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Payload] | Dieses Feld enthält die Daten, die an die [!DNL Kinesis] Datenstream im JSON-Format.<br><br>Unter dem **[!UICONTROL Roh]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen oder das Datenelementsymbol (![Datensatzsymbol](../../../images/extensions/server/aws/data-element-icon.png)), um aus einer Liste vorhandener Datenelemente zur Darstellung der Payload auszuwählen.<br><br>Sie können auch die **[!UICONTROL JSON-Schlüssel-Wert-Paare-Editor]** Option zum manuellen Hinzufügen jedes Schlüssel-Wert-Paares über einen UI-Editor. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. |

{style=&quot;table-layout:auto&quot;}

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Änderungen beibehalten]** , um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]**.

Veröffentlichen Sie schließlich eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Daten an [!DNL Kinesis Data Streams] mithilfe der [!DNL AWS] Ereignisweiterleitungserweiterung. Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie im Abschnitt [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
