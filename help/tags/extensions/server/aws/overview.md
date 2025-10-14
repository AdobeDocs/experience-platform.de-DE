---
title: AWS-Erweiterung - Übersicht
description: Erfahren Sie mehr über die AWS-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 7%

---

# [!DNL AWS] - Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) ist eine Cloud-Computing-Plattform, die eine Vielzahl von Services wie verteiltes Computing, Datenbankspeicherung, Inhaltsbereitstellung und SaaS-Integrationsservices (Software-as-a-Service) für Customer Relationship Management (CRM) und Enterprise Resource Planning (ERP) bietet.

Die [!DNL AWS] [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) nutzt [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html), um Ereignisse aus dem Adobe Experience Platform-Edge Network zur weiteren Verarbeitung an [!DNL AWS] zu senden. In diesem Handbuch wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel verwenden.

## Voraussetzungen

Sie müssen über ein [!DNL AWS]-Konto mit einem vorhandenen [!DNL Kinesis]-Datenstrom verfügen, um diese Erweiterung verwenden zu können. Wenn Sie keinen bereits vorhandenen Datenstrom haben, lesen Sie die [!DNL AWS]-Dokumentation unter [Erstellen eines neuen Datenstroms mithilfe der  [!DNL AWS] -Verwaltungskonsole](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Installieren der Erweiterung {#install}

Um die [!DNL AWS] zu installieren, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder zur Experience Platform-Benutzeroberfläche und wählen **[!UICONTROL in der linken Navigationsleiste]** Ereignisweiterleitung“ aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, klicken Sie im linken **auf** Erweiterungen und wählen Sie dann die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie nach der Karte [!UICONTROL AWS] und wählen Sie dann **[!UICONTROL Installieren]** aus.

![Die ausgewählte Schaltfläche [!UICONTROL Installieren] für die Erweiterung [!UICONTROL AWS] in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/server/aws/install.png)

Im nächsten Bildschirm müssen Sie die Anmeldeinformationen für die Verbindung für Ihr [!DNL AWS]-Konto angeben. Insbesondere müssen Sie Ihre [!DNL AWS] Zugriffsschlüssel-ID und Ihren geheimen Zugriffsschlüssel angeben. Wenn Sie diese Werte nicht kennen, lesen Sie die [!DNL AWS] Dokumentation zu [So erhalten Sie Ihre Zugriffsschlüssel-ID und Ihren geheimen Zugriffsschlüssel](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![Die Zugriffsschlüssel-ID und der geheime Zugriffsschlüssel, die in der Erweiterungskonfigurationsansicht hinzugefügt wurden.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Eine Zugriffsrichtlinie muss an das [!DNL AWS]-Konto angehängt werden, das zum Generieren der Zugriffsberechtigungen verwendet wird. Diese Richtlinie muss so konfiguriert sein, dass Zugriffsrechte zum Senden von Daten an den [!DNL Kinesis] Datenstrom gewährt werden. Siehe **Beispiel 2** im [!DNL AWS]-Dokument zu [Beispielrichtlinien für [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) um zu sehen, wie die Richtlinie definiert werden sollte.

Wenn Sie fertig sind, wählen **[!UICONTROL Speichern]** und die Erweiterung wird installiert.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitungsregel [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie deren Bedingungen nach Bedarf. Wählen Sie beim Konfigurieren der Aktionen für die Regel die Erweiterung **[!UICONTROL AWS]** und dann für den Aktionstyp **[!UICONTROL Daten an Kinesis-Datenstrom senden]** aus.

![Der Aktionstyp [!UICONTROL Daten an Kinesis-Datenstrom senden] wird für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt.](../../../images/extensions/server/aws/select-action-type.png)

Das rechte Bedienfeld wird aktualisiert und zeigt Konfigurationsoptionen dazu an, wie die Daten gesendet werden sollen. Insbesondere müssen Sie den verschiedenen Eigenschaften[&#x200B; die Ihre [!DNL Event Hub]-Konfiguration repräsentieren](../../../ui/managing-resources/data-elements.md) „Datenelemente“ zuweisen.

![Die Konfigurationsoptionen für den Aktionstyp [!UICONTROL Daten an Kinesis-Datenstrom senden] werden in der Benutzeroberfläche angezeigt.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Details zum Kinesis-Datenstrom]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Stream-Name] | Der Name des Streams, an den diese Ereignisweiterleitungsregel Datensätze sendet. |
| [!UICONTROL AWS-Region] | Die [!DNL AWS] Region, in der der [!DNL Kinesis] Datenstrom erstellt wird. |
| [!UICONTROL Partitionsschlüssel] | Der [Partitionsschlüssel](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) den die Erweiterung beim Senden von Daten an den Datenstrom verwendet.<br><br>[!DNL Kinesis Data Streams] unterteilt die zu einem Stream gehörenden Datensätze in mehrere Shards. Sie verwendet den Partitionsschlüssel, der mit jedem Datensatz gesendet wird, um zu bestimmen, zu welchem Shard ein bestimmter Datensatz gehört.<br><br>Ein guter Partitionsschlüssel für die Kundenverteilung könnte die Kundennummer sein, da sie für jeden Kunden anders ist. Ein schlechter Partitionsschlüssel könnte ihre Postleitzahl beeinträchtigen, da sie alle in der gleichen Gegend in der Nähe wohnen könnten. Im Allgemeinen sollten Sie einen Partitionsschlüssel wählen, der den höchsten Bereich von verschiedenen potenziellen Werten hat. Im [!DNL AWS] Artikel zum [Skalieren  [!DNL Kinesis]  Daten-Streams](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) finden Sie Best Practices für die Verwaltung von Partitionsschlüsseln. |

{style="table-layout:auto"}

**[!UICONTROL Daten]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Payload] | Dieses Feld enthält die Daten, die an den [!DNL Kinesis] Datenstrom weitergeleitet werden, im JSON-Format.<br><br>Unter der Option **[!UICONTROL Raw]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen oder Sie können das Datenelementsymbol (![Datensatzsymbol](/help/images/icons/database.png)) auswählen, um aus einer Liste vorhandener Datenelemente zur Darstellung der Payload auszuwählen.<br><br>Sie können auch die Option **[!UICONTROL JSON-Schlüssel-Wert-Paare-Editor]** verwenden, um jedes Schlüssel-Wert-Paar manuell über einen Benutzeroberflächen-Editor hinzuzufügen. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. |

{style="table-layout:auto"}

Wenn Sie fertig sind, wählen **[!UICONTROL Änderungen beibehalten]**, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

Veröffentlichen Sie abschließend eine neue Ereignisweiterleitung [Build](../../../ui/publishing/builds.md), um die Änderungen an der Bibliothek zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Daten mithilfe der Erweiterung für die [!DNL AWS]-Ereignisweiterleitung an [!DNL Kinesis Data Streams] senden. Weitere Informationen zu den Ereignisweiterleitungsfunktionen in Experience Platform finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
