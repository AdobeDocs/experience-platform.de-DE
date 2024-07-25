---
title: Übersicht über die AWS-Erweiterung
description: Erfahren Sie mehr über die AWS-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 7%

---

# Übersicht über die [!DNL AWS]-Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) ist eine Cloud-Computing-Plattform, die eine Vielzahl von Diensten anbietet, wie z. B. dezentrales Computing, Datenbankspeicherung, Inhaltsbereitstellung und SaaS-Integrationsdienste (Software-as-a-Service) für Customer Relationship Management (CRM) und Enterprise Resource Planning (ERP).

Die Erweiterung [!DNL AWS] [ Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) nutzt [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) , um Ereignisse vom Adobe Experience Platform-Edge Network zur weiteren Verarbeitung an [!DNL AWS] zu senden. In diesem Handbuch wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel verwenden.

## Voraussetzungen

Sie müssen über ein [!DNL AWS] -Konto mit einem vorhandenen [!DNL Kinesis] -Datenstrom verfügen, um diese Erweiterung verwenden zu können. Wenn Sie keinen bereits vorhandenen Datenstrom haben, finden Sie weitere Informationen in der [!DNL AWS] -Dokumentation zum Erstellen eines neuen Datenstreams mit der [!DNL AWS] Management Console](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).[

## Installieren der Erweiterung {#install}

Um die Erweiterung [!DNL AWS] zu installieren, navigieren Sie zur Benutzeroberfläche für Datenerfassung oder Experience Platform und wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Ereignisweiterleitung]** aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, wählen Sie im linken Navigationsbereich **[!UICONTROL Erweiterungen]** und dann die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie nach der Karte [!UICONTROL AWS] und wählen Sie dann **[!UICONTROL Installieren]** aus.

![Die Schaltfläche [!UICONTROL Installieren], die für die Erweiterung [!UICONTROL AWS] in der Datenerfassungs-Benutzeroberfläche ausgewählt ist.](../../../images/extensions/server/aws/install.png)

Auf dem nächsten Bildschirm müssen Sie die Anmeldedaten für die Verbindung für Ihr [!DNL AWS]-Konto angeben. Insbesondere müssen Sie Ihre [!DNL AWS] Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel angeben. Wenn Sie diese Werte nicht kennen, lesen Sie die [!DNL AWS] -Dokumentation unter [, wie Sie Ihre Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel abrufen können.](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html)

![Die Kennung des Zugriffsschlüssels und der geheime Zugriffsschlüssel, die in der Ansicht der Erweiterungskonfiguration hinzugefügt wurden.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Eine Zugriffsrichtlinie muss an das [!DNL AWS] -Konto angehängt werden, das zum Generieren der Zugriffsberechtigungen verwendet wird. Diese Richtlinie muss so konfiguriert sein, dass Zugriffsberechtigungen zum Senden von Daten an den [!DNL Kinesis] -Datenstrom gewährt werden. Siehe **Beispiel 2** im Dokument [!DNL AWS] für [Beispielrichtlinien für  [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) , um zu sehen, wie die Richtlinie definiert werden soll.

Wählen Sie abschließend **[!UICONTROL Speichern]** aus und die Erweiterung wird installiert.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitung [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen entsprechend Ihren Anforderungen. Wählen Sie beim Konfigurieren der Aktionen für die Regel die Erweiterung **[!UICONTROL AWS]** und dann für den Aktionstyp **[!UICONTROL Daten an Kinesis-Datenstream senden]** aus.

![Der Aktionstyp [!UICONTROL Daten an Kinesis-Datenstream senden] wurde für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt.](../../../images/extensions/server/aws/select-action-type.png)

Das rechte Bedienfeld wird aktualisiert und zeigt Konfigurationsoptionen für die Art und Weise an, wie die Daten gesendet werden sollen. Insbesondere müssen Sie den verschiedenen Eigenschaften, die Ihre [!DNL Event Hub] -Konfiguration darstellen, [Datenelemente](../../../ui/managing-resources/data-elements.md) zuweisen.

![Die Konfigurationsoptionen für den in der Benutzeroberfläche angezeigten Aktionstyp [!UICONTROL Daten an den Kinesis-Daten-Stream senden] .](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis-Daten-Stream-Details]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Streamname] | Der Name des Streams, an den diese Ereignisweiterleitungsregel Datendatensätze sendet. |
| [!UICONTROL AWS-Region] | Der [!DNL AWS] -Bereich, in dem der [!DNL Kinesis]-Datenstrom erstellt wird. |
| [!UICONTROL Trennschlüssel] | Der [Partitionsschlüssel](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) , den die Erweiterung beim Senden von Daten an den Datenstrom verwendet.<br><br>[!DNL Kinesis Data Streams] trennt die zu einem Stream gehörenden Datendatensätze in mehrere Shards. Es verwendet den mit jedem Datensatz gesendeten Partitionsschlüssel, um zu bestimmen, zu welchem Teil ein bestimmter Datensatz gehört.<br><br>Ein guter Partitionsschlüssel für die Verteilung von Kunden kann die Kundennummer sein, da sie für jeden Kunden unterschiedlich ist. Ein schlechter Partitionsschlüssel könnte ihre Postleitzahl haben, da sie alle in der Nähe leben können. Im Allgemeinen sollten Sie einen Partitionsschlüssel wählen, der den höchsten Bereich unterschiedlicher potenzieller Werte aufweist. Best Practices zum Verwalten von Partitionsschlüsseln finden Sie im Artikel [!DNL AWS] zu [Skalierung Ihrer [!DNL Kinesis] Datenströme](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) . |

{style="table-layout:auto"}

**[!UICONTROL Daten]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Payload] | Dieses Feld enthält die Daten, die im JSON-Format an den [!DNL Kinesis] -Datenstrom weitergeleitet werden.<br><br>Unter der Option **[!UICONTROL Raw]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen. Alternativ können Sie das Datenelementsymbol (![Datensatzsymbol](/help/images/icons/database.png)) auswählen, das aus einer Liste vorhandener Datenelemente ausgewählt werden soll, um die Payload darzustellen.<br><br>Sie können auch die Option **[!UICONTROL JSON Key-Value Paares Editor]** verwenden, um jedes Schlüssel-Wert-Paar manuell über einen UI-Editor hinzuzufügen. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. |

{style="table-layout:auto"}

Wählen Sie nach Abschluss **[!UICONTROL Änderungen beibehalten]** aus, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

Veröffentlichen Sie abschließend eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Daten mit der Ereignisweiterleitungs-Erweiterung [!DNL AWS] an [!DNL Kinesis Data Streams] gesendet werden. Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie in der [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
