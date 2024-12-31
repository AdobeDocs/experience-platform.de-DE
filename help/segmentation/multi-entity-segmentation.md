---
solution: Experience Platform
title: Übersicht über die Segmentierung mehrerer Entitäten
description: Bei der Segmentierung mit mehreren Entitäten können Sie Profildaten um zusätzliche Daten erweitern, die auf Produkten, Geschäften oder anderen nicht-profilbasierten Klassen beruhen. Sobald eine Verbindung besteht, stehen Daten aus zusätzlichen Klassen zur Verfügung, so als wären sie im Profilschema nativ vorhanden.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 13%

---

# Übersicht über die Segmentierung mehrerer Entitäten

Die Segmentierung mehrerer Entitäten ist eine erweiterte Funktion, die als Teil der Adobe Experience Platform-[!DNL Segmentation Service] verfügbar ist. Mit dieser Funktion können Sie [!DNL Real-Time Customer Profile]-Daten mit zusätzlichen „Nicht-Personen“-Daten (auch als „Dimensionsentitäten“ bezeichnet) erweitern, die Ihr Unternehmen möglicherweise definiert, z. B. Daten zu Produkten oder Geschäften. Die Segmentierung mehrerer Entitäten bietet Flexibilität bei der Definition von Segmentdefinitionen auf der Grundlage von Daten, die für Ihre individuellen Geschäftsanforderungen relevant sind, und kann durchgeführt werden, ohne über Erfahrung bei der Datenbankabfrage zu verfügen. Bei der Segmentierung mehrerer Entitäten können Sie Ihren Segmentdefinitionen wichtige Daten hinzufügen, ohne kostspielige Änderungen an Datenströmen vornehmen oder auf eine Backend-Datenzusammenführung warten zu müssen.

## Erste Schritte

Die Segmentierung mehrerer Entitäten setzt ein Grundverständnis der verschiedenen Adobe Experience Platform-Services voraus, die an der Segmentierung beteiligt sind. Bevor Sie mit diesem Handbuch fortfahren, lesen Sie bitte die folgende Dokumentation:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen beruht.
   * [Profil-Leitplanken](../profile/guardrails.md): Best Practices zum Erstellen von Datenmodellen, die von [!DNL Profile] unterstützt werden.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ermöglicht das Erstellen von Zielgruppen aus [!DNL Real-Time Customer Profile].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten ordnet.
   * [Grundlagen der Schemakomposition](../xdm/schema/composition.md#union) Erfahren Sie mehr über die Best Practices zum Erstellen von Schemas, die beim Experience Platform verwendet werden können. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../xdm/schema/best-practices.md) aufgenommen werden.

## Anwendungsfälle

Um den Nutzen der Segmentierung mehrerer Entitäten zu veranschaulichen, sollten Sie drei standardmäßige Marketing-Anwendungsfälle betrachten, die die Herausforderungen in den meisten Marketing-Anwendungen veranschaulichen:

### Kombination von Online- und Offline-Kaufdaten

Ein Marketer, der eine E-Mail-Kampagne erstellt hat, hat in den letzten drei Monaten möglicherweise versucht, mithilfe der letzten Käufe im Kundengeschäft eine Zielgruppe zu erstellen. Idealerweise erfordert diese Zielgruppe sowohl den Artikelnamen als auch den Namen des Stores, in dem der Kauf getätigt wurde. Zuvor bestand die Herausforderung darin, die Store-Kennung aus dem Kaufereignis zu erfassen und sie einem einzelnen Kundenprofil zuzuweisen.

### Retargeting von E-Mails bei Warenkorbabbruch

Das Erstellen und Qualifizieren von Benutzern in Segmentdefinitionen für den Warenkorbabbruch ist komplex. Zu wissen, welche Produkte in eine personalisierte Retargeting-Kampagne aufgenommen werden sollen, erfordert Daten darüber, welche Produkte von jeder Person verlassen wurden. Diese Daten sind an Commerce-Ereignisse gebunden, die zuvor die Überwachung und Extraktion von Daten erschwert hatten.

## Segmentdefinitionen mit mehreren Entitäten erstellen

Um eine Segmentdefinition mit mehreren Entitäten zu erstellen, müssen zunächst Beziehungen zwischen Schemata definiert werden, bevor die [!DNL Segmentation]-API oder die Segment Builder-Benutzeroberfläche zum Erstellen der Segmentdefinition verwendet werden kann.

### Definieren von Beziehungen

Das Definieren von Beziehungen innerhalb der Struktur Ihrer Experience-Datenmodell (XDM)-Schemata ist ein integraler Bestandteil der Erstellung von Segmenten mit mehreren Entitäten. Für Beziehungen muss das Feld im Ziel als primäre Identität dieses Schemas markiert werden. Eine Identität kann nur auf Zeichenfolgen markiert werden und nicht auf Arrays markiert werden. Darüber hinaus müssen Beziehungen nicht unbedingt Eins-zu-eins-Beziehungen sein, da Sie Profile und Erlebnisereignisse mit mehreren Zielen verbinden können.

Das Definieren von Beziehungen kann entweder mit der Schema Registry-API oder dem Schema-Editor erfolgen. Ausführliche Anweisungen zum Definieren einer Beziehung zwischen zwei Schemata finden Sie in den folgenden Tutorials:

* [Definieren einer Beziehung zwischen zwei Schemas mithilfe der API](../xdm/tutorials/relationship-api.md)
* [Definieren einer Beziehung zwischen zwei Schemas mithilfe der Benutzeroberfläche des Schema-Editors](../xdm/tutorials/relationship-ui.md)

### Erstellen einer Segmentdefinition mit mehreren Entitäten

Nachdem Sie die erforderlichen XDM-Beziehungen definiert haben, können Sie mit dem Erstellen einer Segmentdefinition mit mehreren Entitäten beginnen. Dies kann entweder über die Segmentierungs-API oder die Benutzeroberfläche von Segment Builder erfolgen. Für weitere Informationen wählen Sie bitte aus den folgenden Handbüchern:

* [Erstellen einer Segmentdefinition mit der Segmentierungs-API](./tutorials/create-a-segment.md)
* [Erstellen einer Segmentdefinition mithilfe der Segment Builder-Benutzeroberfläche](./ui/overview.md)

## Auswerten von Segmentdefinitionen mit mehreren Entitäten und Zugriff darauf

Nachdem Sie eine Segmentdefinition erstellt haben, können Sie die Ergebnisse mithilfe der Segmentierungs-API auswerten und darauf zugreifen. Die Auswertung einer Segmentdefinition mit mehreren Entitäten ähnelt der Auswertung einer Standardsegmentdefinition. Dieser Vorgang kann nur mit der Segmentierungs-API durchgeführt werden. Eine detaillierte Anleitung zur Verwendung der API zum Auswerten und Zugreifen auf Segmentdefinitionen finden Sie im Tutorial [Auswerten von und Zugreifen auf Segmentdefinitionen](./tutorials/evaluate-a-segment.md) .
