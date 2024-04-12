---
keywords: RTCDP; CDP; B2B Edition; Real-time Customer Data Platform; Echtzeit-Kundendatenplattform; Echtzeit-Kundendatenplattform; b2b; cdp
solution: Experience Platform
title: Erste Schritte mit Real-time Customer Data Platform B2B Edition
description: Verwenden Sie dieses Beispielszenario als Beispiel für die Einrichtung Ihrer Implementierung von Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 8a487d948d2eb7db167298b61045ef8dd2099da6
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 67%

---

# Erste Schritte mit Real-time Customer Data Platform B2B Edition

Dieses Dokument bietet einen durchgängigen End-to-End-Workflow für die ersten Schritte mit der Real-time Customer Data Platform (CDP) B2B Edition und zeigt anhand eines Beispielanwendungsbeispiels Schlüsselkonzepte.

Das Technologieunternehmen Bodea möchte Personen- und Account-Daten aus verschiedenen separaten Datenquellen kombinieren, um Kunden mit einer E-Mail- und einer LinkedIn-Werbekampagne wegen eines neuen Produkts gezielt ansprechen zu können. Bodea verwendet Marketo Engage als Marketing-Automatisierungsplattform und muss eine B2B-spezifische Zielgruppe aus mehreren CRMs segmentieren, die Kundendaten enthalten.

## Erste Schritte

In diesem im Tutorial gezeigten Verfahren werden mehrere Adobe Experience Platform-Services verwendet. Um die einzelnen Schritte nachvollziehen zu können, sollten Sie über gute Kenntnisse der folgenden Services verfügen:

- [Experience Data Modal (XDM)](../xdm/home.md)
- [Quellen](../sources/home.md)
- [Segmentierung](../segmentation/home.md)
- [Ziele](../destinations/home.md)

## Erstellen von Schemata für Ihre Daten

Im Rahmen der Ersteinrichtung muss die IT-Abteilung von Bodea ein XDM-Schema erstellen, um sicherzugehen, dass die Daten beim Einlesen in Platform einem Standardformat entsprechen und auf verschiedenen Platform-Services und Adobe Experience Cloud-Produkten (wie Adobe Analytics und Adobe Target) verarbeitet werden können.

>[!WARNING]
>
>Sie müssen die Aufnahmemuster befolgen, wie in der entsprechenden Quelldokumentation beschrieben, die mit diesem Tutorial verknüpft ist. Andere Feldzuordnungsmethoden funktionieren nicht immer.

Mit Adobe Experience Platform können Sie automatisch die Schemata und Namespaces generieren, die für B2B-Datenquellen erforderlich sind. Dieses Werkzeug stellt sicher, dass die erstellten Schemata die Daten in einer strukturierten, wiederverwendbaren Weise beschreiben. Eine vollständige Beschreibung des Einrichtungsprozesses finden Sie in der [Dokumentation zu B2B-Namespaces und dem Dienstprogramm zur automatischen Schemaerstellung](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

In der Adobe Experience Platform-Benutzeroberfläche wählt der Bodea-Marketing-Experte **[!UICONTROL Schemata]** in der linken Leiste und anschließend die Registerkarte **[!UICONTROL Durchsuchen]** aus. Da das Marketo Engage-Dienstprogramm für die automatische Generierung verwendet wird, werden die neuen leeren Schemata in der Liste angezeigt und haben alle das Präfix „B2B“.

![Registerkarte zum Durchsuchen des Schemaarbeitsbereichs](./assets/b2b-tutorial/empty-b2b-schemas.png)

Das Dienstprogramm zur automatischen Generierung definierte die Datenmodellstruktur für die Schemata mithilfe von standardmäßigen XDM-B2B-Klassen (wie [XDM Business Account](../xdm/classes/b2b/business-account.md) und [XDM Business Opportunity](../xdm/classes/b2b/business-opportunity.md)), die grundlegende B2B-Datenentitäten erfassen. Darüber hinaus verfügen die automatisch generierten B2B-Schemata, die auf diesen Klassen basieren, über vorab eingerichtete Beziehungen, die erweiterte Anwendungsfälle für die Segmentierung ermöglichen. Alle für die Datenstruktur erforderlichen zusätzlichen Feldergruppen können hier einfach über die Benutzeroberfläche erstellt werden. Weitere Informationen finden Sie im [Handbuch zur XDM-Benutzeroberfläche im Abschnitt zum Hinzufügen von Feldergruppen zu einem Schema](../xdm/ui/resources/schemas.md#add-field-groups).

>[!NOTE]
> 
>Wenn Sie das Dienstprogramm zur automatischen Generierung nicht verwenden oder eine neue Beziehung erstellen müssen, sehen Sie sich das Tutorial zum [Erstellen von Beziehungen zwischen B2B-Schemata](../xdm/tutorials/relationship-b2b.md) an.

Das Echtzeit-Kundenprofil führt Daten aus unterschiedlichen Quellen zusammen, um konsolidierte Profile der wichtigsten B2B-Entitäten zu erstellen. Da Profile auf Basis einer einzelnen Klasse generiert werden, richtet das Dienstprogramm für die automatische Generierung basierend auf gängigen geschäftlichen Anwendungsfällen Beziehungen zwischen Schemata ein. Somit ist das Bodea-Team nun bereit, Daten basierend auf ihren B2B-Schemata aufzunehmen.

>[!NOTE]
> 
>Standardmäßige Identitäts-Namespaces, Primärschlüssel und Beziehungen, die vom Dienstprogramm zur automatischen Generierung für die Schemata erstellt wurden, können im Arbeitsbereich „Schema“ leicht gefunden werden.
>
>![Anzeige der standardmäßigen Schema-Identität und der Beziehung](./assets/b2b-tutorial/schema-identity-relationship.png)

## Aufnehmen von Daten in Experience Platform

Als Nächstes verwendet der Bodea-Marketing-Experte den [Marketo Engage-Connector](../sources/connectors/adobe-applications/marketo/marketo.md), um Daten in Platform aufzunehmen und für nachgelagerte Services zu verwenden. Sie können auch Daten erfassen, indem Sie eine der genehmigten Quellen für Real-Time CDP B2B Edition verwenden.

>[!NOTE]
> 
>Welche Quell-Connectoren für Ihr Unternehmen verfügbar sind, erfahren Sie im Quellkatalog in der Platform-Benutzeroberfläche. Um auf den Katalog zuzugreifen, wählen Sie im linken Navigationsbereich zunächst **Quellen** und anschließend die Option **Katalog** aus.

Um eine Verbindung zwischen einem Marketo-Account und Platform herzustellen, müssen Sie Authentifizierungsdaten anfordern. Detaillierte Anleitungen finden Sie im [Handbuch zum Erlangen der Authentifizierungsdaten für den Marketo-Quell-Connector](../sources/connectors/adobe-applications/marketo/marketo-auth.md).

Nach dem Erwerb von Authentifizierungsberechtigungen erstellt der Bodea-Marketing-Experte eine Verbindung zwischen dem Marketo-Konto und seiner Platform-Organisation. Anleitungen zum [Verbinden eines Marketo-Accounts über die Platform-Benutzeroberfläche](../sources/tutorials/ui/create/adobe-applications/marketo.md) finden Sie in der Dokumentation.

Der Marketo Engage-Quell-Connector bietet eine Funktion zur automatischen Zuordnung, mit der Sie all Ihre Datenfelder denen der neu erstellten Schemata zuordnen können.

>[!NOTE]
> 
>Wenn Sie benutzerdefinierte Feldergruppen in Ihren XDM-Schemata erstellt haben, verfügen Sie in dieser Phase des Prozesses möglicherweise über unverbundene Felder. Überprüfen Sie alle Werte in Ihren benutzerdefinierten Feldergruppen.

Der Bodea-Marketing-Experte prüft, ob alle Feldergruppen korrekt zugeordnet sind, und führt den Einrichtungsprozess der Quellen durch Initialisierung eines Datenflusses fort. Durch Erstellen eines Datenflusses zum Einlesen von Marketo-Daten können die eingehenden Daten von nachgelagerten Platform-Services verwendet werden. Während des anfänglichen Aufnahmevorgangs werden die Daten als Batch in Experience Platform übernommen. Danach werden nachfolgende aufgenommene Daten in nahezu Echtzeit an das Profil gestreamt.

## Erstellen einer Zielgruppe zur Datenauswertung

Die nächste Aufgabe besteht darin, eine Zielgruppe für die neue E-Mail-Marketing-Kampagne von Bodea zu erstellen, die auf bestimmten Attributen verwandter Entitäten in den Quelldaten basiert. In der Platform-Benutzeroberfläche wählt der Marketing-Experte zunächst **[!UICONTROL Segmente]** in der linken Navigation und anschließend die Option **[!UICONTROL Segment erstellen]** aus.

In diesem Beispiel findet die Zielgruppe alle Personen, die in der Verkaufsabteilung arbeiten und mit einem Konto verbunden sind, das mindestens eine offene Möglichkeit hat. Diese Zielgruppen erfordern eine Verknüpfung zwischen der Klasse &quot;XDM Individual Profile&quot;, der Klasse &quot;XDM Business Account&quot;und der Klasse &quot;XDM Business Opportunity&quot;.

![Anwendungsfallsegment](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Anweisungen zum Erstellen von Zielgruppen zur Auswertung Ihrer Daten finden Sie unter [Handbuch zur Benutzeroberfläche von Segment Builder](../segmentation/ui/segment-builder.md). Spezifischere Anwendungsfälle für die B2B-Segmentierung finden Sie im Abschnitt [Segmentierungsübersicht für Real-Time CDP B2B Edition](./segmentation/b2b.md).

Mit Segment Builder können Sie aus Echtzeit-Kundenprofildaten eine vermarktbare Zielgruppe erstellen und Schätzungen Ihrer potenziellen Zielgruppe basierend auf der Kombination von Attributen, Ereignissen und vorhandenen Zielgruppen anzeigen, die Sie definiert haben.

## Aktivieren von ausgewerteten Daten für ein Ziel

Nachdem die Audience erfolgreich erstellt wurde, wird im Abschnitt [!UICONTROL Details] des Arbeitsbereichs. Da derzeit keine Ziele für die Segmentdefinition aktiviert sind, muss der Bodea-Marketing-Experte die Zielgruppe in einen Datensatz exportieren, in dem sie aufgerufen und bearbeitet werden kann.

Im Arbeitsbereich [!UICONTROL Segmente] der Platform-Benutzeroberfläche wählt der Bodea-Marketing-Experte die Option **[!UICONTROL Für Ziel aktivieren]**.

![Aktivieren der Zielgruppe für ein Ziel](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Siehe Tutorial zu [Aktivieren einer Zielgruppe für ein Ziel](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=de) für umfassende Schritte, wie dies erreicht werden kann.

Der Bodea-Marketingexperte aktiviert die Zielgruppe für das Marketo-Ziel, sodass sie Zielgruppendaten in Form einer statischen Liste von Platform auf Marketo Engage übertragen kann. Weitere Informationen finden Sie im Handbuch zum [Marketo-Ziel](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html?lang=de).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die verschiedenen Adobe Experience Platform-Dienste genutzt, die von Real-Time CDP B2B Edition verwendet werden. Sie haben gelernt, Ihre B2B-Daten als verwertbare Zielgruppen aufzunehmen, zu segmentieren, auszuwerten und zu exportieren, wobei diese Zielgruppen kanalübergreifend angesprochen werden können.
