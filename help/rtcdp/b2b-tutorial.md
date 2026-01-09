---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;Real-time Customer Data Platform;Real-time CDP;B2B;CDP
solution: Experience Platform
title: Erste Schritte mit Real-Time Customer Data Platform B2B edition
description: Verwenden Sie dieses Szenario als Beispiel, wenn Sie Ihre Implementierung von Adobe Real-Time Customer Data Platform B2B edition einrichten.
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: ed655be7ad274c06deea1e50001c28c58f68796e
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 43%

---

# Erste Schritte mit Real-Time Customer Data Platform B2B edition

Dieses Dokument bietet einen allgemeinen End-to-End-Workflow für die ersten Schritte mit Real-Time Customer Data Platform (CDP) B2B edition. Anhand eines Beispielanwendungsfalls werden die wichtigsten Konzepte veranschaulicht.

Das Technologieunternehmen Bodea möchte Personen- und Account-Daten aus verschiedenen separaten Datenquellen kombinieren, um Kunden mit einer E-Mail- und einer LinkedIn-Werbekampagne wegen eines neuen Produkts gezielt ansprechen zu können. Bodea verwendet eine Marketing-Automatisierungsplattform und muss eine B2B-spezifische Zielgruppe aus mehreren CRMs segmentieren, die Kundendaten enthalten.

## Erste Schritte

Dieser Tutorial-Workflow stützt sich im Rahmen der Demonstration auf mehrere Dienste von Adobe Experience Platform. Um die einzelnen Schritte nachvollziehen zu können, sollten Sie über gute Kenntnisse der folgenden Services verfügen:

- [Experience-Datenmodell (XDM)](../xdm/home.md)
- [Quellen](../sources/home.md)
- [Segmentierung](../segmentation/home.md)
- [Ziele](../destinations/home.md)

## Erstellen von Schemata für Ihre Daten

Im Rahmen der Ersteinrichtung muss die IT-Abteilung von Bodea ein XDM-Schema erstellen, um sicherzustellen, dass ihre Daten beim Einlesen in Experience Platform einem Standardformat entsprechen und auf verschiedenen Experience Platform-Services und Adobe Experience Cloud-Produkten (wie Adobe Analytics und Adobe Target) verarbeitet werden können.

>[!WARNING]
>
>Sie müssen die Aufnahmemuster befolgen, wie in der entsprechenden Quelldokumentation beschrieben, die mit diesem Tutorial verknüpft ist. Andere Feldzuordnungsmethoden funktionieren nicht immer.

Mit Adobe Experience Platform können Sie automatisch die Schemata und Namespaces generieren, die für B2B-Datenquellen erforderlich sind. Dieses Werkzeug stellt sicher, dass die erstellten Schemata die Daten in einer strukturierten, wiederverwendbaren Weise beschreiben. Eine vollständige Beschreibung des Einrichtungsprozesses finden Sie in der [Dokumentation zu B2B-Namespaces und dem Dienstprogramm zur automatischen Schemaerstellung](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

In der Adobe Experience Platform-Benutzeroberfläche wählt der Bodea-Marketing-Experte **[!UICONTROL Schemas]** in der linken Leiste und anschließend die Registerkarte **[!UICONTROL Browse]** aus. Da das Dienstprogramm zur automatischen Generierung verwendet wird, erscheinen die neuen leeren Schemata in der Liste und haben alle das Präfix „B2B“.

![Registerkarte zum Durchsuchen des Schemaarbeitsbereichs](./assets/b2b-tutorial/empty-b2b-schemas.png)

Das Dienstprogramm zur automatischen Generierung definierte die Datenmodellstruktur für die Schemata mithilfe von standardmäßigen XDM-B2B-Klassen (wie [XDM Business Account](../xdm/classes/b2b/business-account.md) und [XDM Business Opportunity](../xdm/classes/b2b/business-opportunity.md)), die grundlegende B2B-Datenentitäten erfassen. Darüber hinaus verfügen die automatisch generierten B2B-Schemata, die auf diesen Klassen basieren, über vorab eingerichtete Beziehungen, die erweiterte Anwendungsfälle für die Segmentierung ermöglichen. Alle für die Datenstruktur erforderlichen zusätzlichen Feldergruppen können hier einfach über die Benutzeroberfläche erstellt werden. Weitere Informationen finden Sie im [Handbuch zur XDM-Benutzeroberfläche im Abschnitt zum Hinzufügen von Feldergruppen zu einem Schema](../xdm/ui/resources/schemas.md#add-field-groups).

>[!NOTE]
> 
>Wenn Sie das Dienstprogramm zur automatischen Generierung nicht verwenden oder eine neue Beziehung erstellen müssen, sehen Sie sich das Tutorial zum [Erstellen von Beziehungen zwischen B2B-Schemata](../xdm/tutorials/relationship-b2b.md) an.

Das Echtzeit-Kundenprofil führt Daten aus unterschiedlichen Quellen zusammen, um konsolidierte Profile wichtiger B2B-Entitäten zu erstellen. Da Profile auf Basis einer einzelnen Klasse generiert werden, richtet das Dienstprogramm für die automatische Generierung basierend auf gängigen geschäftlichen Anwendungsfällen Beziehungen zwischen Schemata ein. Somit ist das Bodea-Team nun bereit, Daten basierend auf ihren B2B-Schemata aufzunehmen.

>[!NOTE]
> 
>Standardmäßige Identity-Namespaces, Primärschlüssel und Beziehungen, die vom Dienstprogramm zur automatischen Generierung für die Schemata erstellt wurden, können im Arbeitsbereich „Schema“ leicht gefunden werden.
>
>![Anzeige der standardmäßigen Schema-Identität und der Beziehung](./assets/b2b-tutorial/schema-identity-relationship.png)

## Aufnehmen von Daten in Experience Platform

Als Nächstes verwendet der Bodea-Marketing-Experte einen [Quell-Connector](../sources/home.md), um Daten in Experience Platform aufzunehmen und für nachgelagerte Services zu verwenden. Sie können auch Daten aufnehmen, indem Sie eine der genehmigten Quellen für Real-Time CDP B2B edition verwenden.

>[!NOTE]
> 
>Um zu erfahren, welche Quell-Connectoren für Ihr Unternehmen verfügbar sind, können Sie den Quellkatalog in der Experience Platform-Benutzeroberfläche anzeigen. Um auf den Katalog zuzugreifen, wählen Sie im linken Navigationsbereich zunächst **Quellen** und anschließend die Option **Katalog** aus.

Um eine Verbindung zwischen einem Quellkonto und Experience Platform herzustellen, müssen Sie Authentifizierungsdaten anfordern. Detaillierte Anweisungen zum Erlangen der Authentifizierungsdaten für jeden Quelltyp finden Sie im Abschnitt [Quellen - Übersicht](../sources/home.md).

Nachdem der Bodea-Marketing-Experte Anmeldeinformationen zur Authentifizierung erhalten hat, erstellt er eine Verbindung zwischen dem Quellkonto und seiner Experience Platform-Organisation. Weitere Informationen [ Einrichten einer Quellverbindung finden ](../sources/home.md) in der Quelldokumentation .

Der Quell-Connector bietet eine Funktion zur automatischen Zuordnung, mit der Sie all Ihre Datenfelder denen der neu erstellten Schemata zuordnen können.

>[!NOTE]
> 
>Wenn Sie benutzerdefinierte Feldergruppen in Ihren XDM-Schemata erstellt haben, verfügen Sie in dieser Phase des Prozesses möglicherweise über unverbundene Felder. Überprüfen Sie alle Werte in Ihren benutzerdefinierten Feldergruppen.

Der Bodea-Marketing-Experte prüft, ob alle Feldergruppen korrekt zugeordnet sind, und führt den Einrichtungsprozess der Quellen durch Initialisierung eines Datenflusses fort. Durch Erstellen eines Datenflusses zum Einbringen von Quelldaten können eingehende Daten von nachgelagerten Experience Platform-Services verwendet werden. Während des anfänglichen Aufnahmevorgangs werden die Daten als Batch in Experience Platform übernommen. Danach werden nachfolgende aufgenommene Daten in nahezu Echtzeit an das Profil gestreamt.

## Erstellen einer Audience zur Auswertung Ihrer Daten

Die nächste Aufgabe besteht darin, eine Zielgruppe für die neue E-Mail-Marketing-Kampagne von Bodea zu erstellen, die auf bestimmten Attributen verwandter Entitäten in den Quelldaten basiert. In der Experience Platform-Benutzeroberfläche wählt der Bodea-Marketing-Experte zunächst **[!UICONTROL Segments]** im linken Navigationsbereich und **[!UICONTROL Create segment]**.

In diesem Beispiel findet die Zielgruppe alle Personen, die in der Verkaufsabteilung arbeiten und mit einem beliebigen Account verbunden sind, der mindestens eine offene Opportunity hat. Diese Zielgruppen erfordern eine Verknüpfung zwischen der Klasse „XDM Individual Profile“, der Klasse „XDM Business Account“ und der Klasse „XDM Business Opportunity“.

![Anwendungsfallsegment](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Anweisungen zum Erstellen von Zielgruppen zur Auswertung Ihrer Daten finden Sie im [Handbuch zur Benutzeroberfläche von Segment Builder](../segmentation/ui/segment-builder.md). Spezifischere Anwendungsfälle für die B2B-Segmentierung finden Sie im Abschnitt [Segmentierungsübersicht für Real-Time CDP B2B edition](./segmentation/b2b.md).

Mit Segment Builder können Sie aus Echtzeit-Kundenprofildaten eine vermarktbare Zielgruppe erstellen und Schätzungen Ihrer potenziellen Zielgruppe basierend auf der von Ihnen definierten Kombination von Attributen, Ereignissen und vorhandenen Zielgruppen anzeigen.

## Aktivieren von ausgewerteten Daten für ein Ziel

Nachdem die Zielgruppe erfolgreich erstellt wurde, wird im Abschnitt [!UICONTROL Details] des Arbeitsbereichs eine Zusammenfassung bereitgestellt. Da derzeit keine Ziele für die Segmentdefinition aktiviert sind, muss der Bodea-Marketing-Experte die Zielgruppe in einen Datensatz exportieren, in dem der Zugriff und die Bearbeitung der Zielgruppe möglich sind.

Im [!UICONTROL Segments] Arbeitsbereich der Experience Platform-Benutzeroberfläche wählt der Bodea-Marketing-Experte **[!UICONTROL Activate to destination]** aus.

![Aktivieren der Zielgruppe für ein Ziel](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Eine ausführliche Anleitung dazu finden [ im Tutorial zum Aktivieren einer Zielgruppe für ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=de) Ziel .

Der Bodea-Marketing-Experte aktiviert die Zielgruppe für ein Ziel, mit dem sie Zielgruppendaten von Experience Platform an ihre Marketing-Automatisierungsplattform pushen kann. Weitere Informationen [ verfügbaren Ziele finden ](../destinations/catalog/overview.md) im Zielkatalog .

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die verschiedenen Adobe Experience Platform-Services genutzt, die von Real-Time CDP B2B edition verwendet werden. Sie haben gelernt, Ihre B2B-Daten als verwertbare Zielgruppen aufzunehmen, zu segmentieren, auszuwerten und zu exportieren, wobei diese Zielgruppen kanalübergreifend angesprochen werden können.
