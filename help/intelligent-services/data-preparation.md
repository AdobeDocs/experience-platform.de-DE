---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Daten für die Verwendung in Intelligent Services vorbereiten
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 1d827d1637da05d3d2afc338f48911bb23039949

---


# Daten für die Verwendung in Intelligent Services vorbereiten

Damit Intelligent Services Einblicke aus den Daten Ihrer Marketing-Ereignis erhalten kann, müssen die Daten semantisch erweitert und in einer Standardstruktur gepflegt werden. Intelligente Dienste nutzen Experience Data Model-(XDM-)Schema, um dies zu erreichen. Insbesondere müssen alle in Intelligent Services verwendeten Datensätze dem XDM-Schema von **Consumer Experience Ereignisses (CEE)** entsprechen.

In diesem Dokument erhalten Sie allgemeine Anleitungen zur Zuordnung Ihrer Marketing-Ereignis-Daten aus mehreren Kanälen zu diesem Schema. In diesen Anleitungen werden Informationen zu wichtigen Feldern im Schema zusammengefasst, die Ihnen bei der Bestimmung helfen, wie Sie Ihre Daten effektiv der Struktur zuordnen können.

## Das CEE-Schema

Das Consumer ExperienceEvent-Schema beschreibt das Verhalten eines Individuums in Bezug auf digitale Marketing-Ereignis (Web oder Mobil) sowie Online- oder Offline-Commerce-Aktivitäten. Die Verwendung dieses Schemas ist für Intelligent Services aufgrund seiner semantisch definierten Felder (Spalten) erforderlich, wodurch unbekannte Namen vermieden werden, die sonst die Daten weniger eindeutig machen würden.

Wie alle XDM-Schema ist auch das CEE-Mixin erweiterbar. Mit anderen Worten, dem CEE-Mixin können zusätzliche Felder hinzugefügt werden, und bei Bedarf können verschiedene Varianten in mehreren Schemas enthalten sein.

Ein vollständiges Beispiel des Mixins finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)und sollten als Referenz für die Schlüsselfelder verwendet werden, die im folgenden Abschnitt beschrieben werden.

### Schlüsselfelder

Die nachstehende Tabelle zeigt die Schlüsselfelder im CEE-Mixin, die genutzt werden sollten, damit Intelligent Services nützliche Einblicke generieren kann, einschließlich Beschreibungen und Links zur Referenzdokumentation für weitere Beispiele.

| XDM-Feld | Beschreibung | Referenz |
| --- | --- | --- |
| `xdm:channel` | Der Marketing-Kanal im Zusammenhang mit dem ExperienceEvent. Das Feld enthält Informationen zum Typ des Kanals, Medientyp und Standort. **Dieses Feld _muss_bereitgestellt werden, damit Attribution AI mit Ihren Daten** arbeiten kann. In der [Tabelle unten](#example-channels) finden Sie einige Beispielzuordnungen. | [Experience Kanal Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) |
| `xdm:productListItems` | Eine Reihe von Artikeln, die die von einem Kunden ausgewählten Produkte darstellen, einschließlich der Produkt-SKU, des Namens, des Preises und der Menge. | [Commerce-Details-Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:commerce` | Enthält Commerce-spezifische Informationen zum ExperienceEvent, einschließlich Bestellnummer und Zahlungsinformationen. | [Commerce-Details-Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:web` | Stellt Webdetails in Bezug auf das ExperienceEvent dar, z. B. Interaktion, Seitendetails und Werber. | [ExperienceEvent-Webdetails-Schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) |

### Kanäle {#example-channels}

Das `xdm:channel` Feld stellt den Marketing-Kanal im Zusammenhang mit dem ExperienceEvent dar. Die folgende Tabelle enthält einige Beispiele für Marketing-Kanal, die XDM zugeordnet sind:

| Kanal | `channel.mediaType` | `channel._type` | `channel.mediaAction` |
| --- | --- | --- | --- |
| Paid Search | BEZAHLT | SUCHE | KLICKEN |
| Social - Marketing | EARNET | SOCIAL | KLICKEN |
| Anzeigen  | BEZAHLT | ANZEIGEN | KLICKEN |
| E-Mail  | BEZAHLT | E-MAIL | KLICKEN |
| Interner Werber | EIGENE | DIREKT | KLICKEN |
| Display ViewThrough | BEZAHLT | ANZEIGEN | IMPRESSION |
| QR-Codeumleitung | EIGENE | DIREKT | KLICKEN |
| SMS-Textnachricht | EIGENE | SMS | KLICKEN |
| Mobil | EIGENE | MOBIL | KLICKEN |

## Zuordnung und Erfassung von Daten

Sobald Sie festgestellt haben, ob Ihre Zeitreihendaten dem CEE-Schema zugeordnet werden können, können Sie den Prozess des Imports Ihrer Daten in Intelligent Services Beginn haben. Wenden Sie sich an Adobe Consulting Services, um Ihre Daten dem Schema zuzuordnen und sie in den Dienst zu integrieren.

Wenn Sie über ein Adobe Experience Platform-Abonnement verfügen und die Daten selbst zuordnen und erfassen möchten, führen Sie die im folgenden Abschnitt beschriebenen Schritte aus.

### Verwenden der Adobe Experience Platform

>[!NOTE] Die folgenden Schritte erfordern ein Abonnement zu Experience Platform. Wenn Sie keinen Zugriff auf die Plattform haben, fahren Sie mit dem Abschnitt [Nächste Schritte](#next-steps) fort.

In diesem Abschnitt wird der Arbeitsablauf für die Zuordnung und Erfassung von Daten zur Experience Platform zur Verwendung in Intelligent Services beschrieben, einschließlich Links zu Schulungen für detaillierte Schritte.

#### Erstellen eines CEE-Schemas und eines Datasets

Wenn Sie bereit sind, Ihre Daten für die Erfassung vorzubereiten, müssen Sie zunächst ein neues XDM-Schema erstellen, das das CEE-Mixin verwendet. Die folgenden Lernprogramme erläutern die Erstellung eines neuen Schemas in der Benutzeroberfläche oder API:

* [Erstellen eines Schemas in der Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md)
* [Erstellen eines Schemas in der API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Die oben stehenden Lernprogramme folgen einem allgemeinen Arbeitsablauf zum Erstellen eines Schemas. Bei der Auswahl einer Klasse für das Schema müssen Sie die **XDM ExperienceEvent-Klasse** verwenden. Nachdem diese Klasse ausgewählt wurde, können Sie das CEE-Mixin dem Schema hinzufügen.

Nachdem Sie das CEE-Mixin zum Schema hinzugefügt haben, können Sie je nach Bedarf weitere Mixins in Ihre Daten einfügen.

Nachdem Sie das Schema erstellt und gespeichert haben, können Sie auf der Grundlage dieses Schemas einen neuen Datensatz erstellen. Die folgenden Lernprogramme erläutern den Vorgang zum Erstellen eines neuen Datensatzes in der Benutzeroberfläche oder API:

* [Erstellen Sie ein Dataset in der Benutzeroberfläche](../catalog/datasets/user-guide.md#create) (zum Verwenden eines vorhandenen Schemas im Workflow)
* [Erstellen eines Datensatzes in der API](../catalog/datasets/create.md)

#### Daten zuordnen und erfassen

Nachdem Sie ein CEE-Schema und einen Dataset erstellt haben, können Sie Ihre Datentabellen dem Schema zuordnen und diese Daten in Platform erfassen. Anweisungen dazu, wie Sie dies in der Benutzeroberfläche durchführen, finden Sie im Lernprogramm zum [Zuordnen einer CSV-Datei zu einem XDM-Schema](../ingestion/tutorials/map-a-csv-file.md) . Nachdem ein Datensatz gefüllt wurde, kann derselbe Datensatz zum Erfassen zusätzlicher Datendateien verwendet werden.

## Nächste Schritte {#next-steps}

Dieses Dokument enthält allgemeine Anleitungen zum Vorbereiten Ihrer Daten für die Verwendung in Intelligent Services. Wenn Sie je nach Anwendungsfall weitere Beratung benötigen, wenden Sie sich bitte an den Adobe Consulting Support.

Nachdem Sie einen Datensatz mit Ihren Kundenerlebnisdaten gefüllt haben, können Sie mithilfe von Intelligent Services Erkenntnisse generieren. Die ersten Schritte finden Sie in den folgenden Dokumenten:

* [Übersicht über die Zuordnungs-AI](./attribution-ai/overview.md)
* [Customer AI – Übersicht](./customer-ai/overview.md)
