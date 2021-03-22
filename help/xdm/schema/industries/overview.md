---
solution: Experience Platform
title: Branchendatenmodelle - Übersicht
topic: Übersicht
description: Erfahren Sie mehr über die standardisierten Datenmodelle für verschiedene Branchen, die mit XDM-Komponenten (Standard Experience Data Model) konstruiert werden können.
translation-type: tm+mt
source-git-commit: 6a7aebb64a533158f7ab17af0cd28243aeda0eca
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Übersicht über die Datenmodelle

Mit dem Experience Data Model (XDM) können Sie hochgradig anpassbare Schema erstellen, um wichtige Kundenerlebnisdaten in Bezug auf Ihr Unternehmen zu erfassen. Um den Prozess der Modellierung Ihrer Daten an XDM anzupassen, stellt Adobe Experience Platform eine vielseitige Suite mit Standard-XDM-Komponenten bereit, die Konzepte erfassen, die in verschiedenen Branchen häufig verwendet werden.

>[!NOTE]
>
>Neue Standard-XDM-Komponenten werden kontinuierlich an die Bedürfnisse der Kunden angepasst. Für eine Liste der aktuellsten Komponenten können Sie [vorhandene Ressourcen in der Benutzeroberfläche](../../ui/explore.md) erkunden oder auf GitHub auf das [offizielle XDM-Repository](https://github.com/adobe/xdm/tree/master/components) verweisen.

Je nach Branche, in der Ihr Unternehmen tätig ist, werden einige XDM-Komponenten für Ihre Bedürfnisse relevanter sein als andere. Darüber hinaus variieren die Beziehungen, die Sie zwischen Ihren XDM-Schemas herstellen, je nach Branche.

Dieser Leitfaden enthält eine Übersicht über Entitäts-Relationship-Diagramme (ERDs) für verschiedene unterstützte Branchenzeitschriften, um Ihnen dabei zu helfen, Ihre Datenmodellierungsstrategie auf Basis Ihrer Branche zu gestalten.

## Voraussetzungen

Um die in diesem Handbuch erwähnten ERDs zu lesen, müssen Sie über ein funktionierendes Verständnis dafür verfügen, wie XDM-Komponenten mit Schemas interagieren und wie XDM-Schema in der Experience Platform als Ganzes funktionieren. Vergewissern Sie sich, dass Sie die folgende Übersichtsdokumentation gelesen haben, bevor Sie fortfahren:

* [XDM-System - Übersicht](../../home.md): Erfahren Sie, wie XDM im Plattform-Ökosystem arbeitet.
* [Grundlagen der Zusammensetzung](../../schema/composition.md) des Schemas: Erfahren Sie, wie XDM-Komponenten (wie Mixins, Klassen und Datentypen) zur Struktur eines Schemas sowie zur Rolle von Identitätsfeldern beitragen.

Es wird außerdem empfohlen, den Leitfaden [Best Practices zur Datenmodellierung](../../schema/best-practices.md) für allgemeine Richtlinien zur Zuordnung Ihrer Daten zu XDM zu lesen.

## ERDs des Branchendatenmodells {#erds}

Die unten aufgeführten, von ERDs dargestellten vertikalen Branchenmodelle werden absichtlich denormalisiert und unter Berücksichtigung der Art und Weise, wie Daten in Plattform gespeichert werden, erstellt.

Für eine bestimmte ERD basiert jede in dargestellte Entität auf einer zugrunde liegenden XDM-Klasse. Für eine bestimmte Entität stellt jede in **bold** markierte Zeile ein Mixin oder einen Datentyp dar, wobei die entsprechenden Felder unten in unverschlüsseltem Text aufgeführt sind. Die wichtigsten Felder für eine bestimmte Entität werden rot hervorgehoben.

>[!NOTE]
>
>Einige Entitäten können ein Feld &quot;_ID&quot;enthalten. Dies stellt den eindeutigen Bezeichner (`_id`) dar, den die Plattform bei der Erfassung automatisch Ereignis- oder Profil-Entitäten zuweist. Sie können jedoch auch Ihre eigenen eindeutigen ID-Werte für dieses Feld verwenden, wenn Sie möchten.

Alle Eigenschaften, die zur Identifizierung einzelner Kunden verwendet werden können, werden als &quot;Identität&quot;gekennzeichnet, wobei eine dieser Eigenschaften als &quot;primäre Identität&quot;gekennzeichnet ist.

Entitätsbeziehungen werden als nicht abhängig markiert, da cookie-basierte Ereignis häufig nicht bestimmen können, wer die Transaktion durchgeführt hat.

ERDs werden für folgende Branchen bereitgestellt:

* [[!UICONTROL Einzelhandel]](./retail.md)
* [[!UICONTROL Finanzdienstleistungen]](./financial.md)
* [[!UICONTROL Reise und Gastfreundschaft]](./travel-hospitality.md)
* [[!UICONTROL Telekommunikation]](./telecom.md)

## Nächste Schritte

Dieses Dokument gab einen Überblick über die branchenspezifischen Datenmodelle und deren Interpretation. Um eine ERD-Ansicht zu erstellen, wählen Sie eine aus der oben stehenden Liste aus.