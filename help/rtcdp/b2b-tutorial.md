---
keywords: RTCDP; CDP; B2B Edition; Real-time Customer Data Platform; Echtzeit-Kundendatenplattform; Echtzeit-Kundendatenplattform; b2b; cdp
solution: Experience Platform
title: Erste Schritte mit Real-time Customer Data Platform B2B Edition (Beta)
description: Verwenden Sie dieses Beispielszenario als Beispiel für die Einrichtung Ihrer Implementierung von Real-time Customer Data Platform B2B Edition.
source-git-commit: 6d55139325cb32cf0e0aac659f6056b7c5e9157b
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 1%

---

# Erste Schritte mit Real-time Customer Data Platform B2B Edition (Beta)

Dieses Dokument bietet einen durchgängigen End-to-End-Workflow für die ersten Schritte mit der Real-time Customer Data Platform (CDP) B2B Edition und zeigt anhand eines Beispielanwendungsbeispiels Schlüsselkonzepte.

Das Technologieunternehmen Bodea möchte Personen- und Kontodaten aus verschiedenen silodierten Datenquellen kombinieren, um Kunden mit einer E-Mail- und einer LinkedIn-Werbekampagne für das neue Produkt gezielt ansprechen zu können. Bodea verwendet Marketo Engage als Marketing-Automatisierungsplattform und muss eine B2B-spezifische Zielgruppe aus mehreren CRMs segmentieren, die Kundendaten enthalten.

## Erste Schritte

Dieser Tutorial-Workflow stützt sich bei der Demonstration auf mehrere Adobe Experience Platform-Dienste. Wenn Sie folgen möchten, sollten Sie die folgenden Dienste gut verstehen:

- [Experience Data Modal (XDM)](../xdm/home.md)
- [Quellen](../sources/home.md)
- [Segmentierung](../segmentation/home.md)
- [Ziele](../destinations/home.md)

## Erstellen von Schemata für Ihre Daten

Im Rahmen der ersten Einrichtung muss die IT-Abteilung von Bodea ein XDM-Schema erstellen, um sicherzustellen, dass ihre Daten beim Einführen in Platform einem Standardformat entsprechen und über verschiedene Platform-Dienste und Adobe Experience Cloud-Produkte (wie Adobe Analytics und Adobe Target) hinweg verarbeitet werden können.

Mit Adobe Experience Platform können Sie automatisch die Schemas und Namespaces generieren, die für B2B-Datenquellen erforderlich sind. Dieses Tool stellt sicher, dass die erstellten Schemata die Daten in einer strukturierten, wiederverwendbaren Weise beschreiben. Befolgen Sie die [Dokumentation zu B2B-Namespaces und dem Dienstprogramm zur automatischen Schemaerstellung](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) für einen vollständigen Verweis auf den Einrichtungsprozess.

In der Adobe Experience Platform-Benutzeroberfläche wählt der Bodea-Marketing-Experte **[!UICONTROL Schemas]** in der linken Leiste, gefolgt von der **[!UICONTROL Durchsuchen]** Registerkarte. Da sie das Dienstprogramm für die automatische Generierung von Marketo Engage verwendet haben, werden die neuen leeren Schemata in der Liste angezeigt und haben alle das Präfix &quot;B2B&quot;.

![Registerkarte zum Durchsuchen von Schemaarbeitsbereichen](./assets/b2b-tutorial/empty-b2b-schemas.png)

Das Dienstprogramm zur automatischen Generierung definierte die Datenmodellstruktur für die Schemas mithilfe von standardmäßigen XDM-B2B-Klassen (wie [XDM-Geschäftskonto](../xdm/classes/b2b/business-account.md) und [XDM-Geschäftschancen](../xdm/classes/b2b/business-opportunity.md)), die grundlegende B2B-Datenentitäten erfassen. Darüber hinaus verfügen die automatisch generierten B2B-Schemas, die auf diesen Klassen basieren, über vorab eingerichtete Beziehungen, die erweiterte Anwendungsfälle für die Segmentierung ermöglichen. Alle für die Datenstruktur erforderlichen zusätzlichen Feldergruppen können hier einfach über die Benutzeroberfläche erstellt werden. Siehe [Handbuch zur XDM-Benutzeroberfläche zum Hinzufügen von Feldergruppen zu einem Schemabeabschnitt](../xdm/ui/resources/schemas.md#add-field-groups) für weitere Informationen.

>[!NOTE]
> 
>Wenn Sie das Dienstprogramm des automatischen Generators nicht verwenden oder eine neue Beziehung erstellen müssen, lesen Sie das Tutorial unter [Erstellen von Beziehungen zwischen B2B-Schemata](../xdm/tutorials/relationship-b2b.md).

Das Echtzeit-Kundenprofil führt Daten aus unterschiedlichen Quellen zusammen, um konsolidierte Profile der wichtigsten B2B-Entitäten zu erstellen. Da Profile auf Basis einer einzelnen Klasse generiert werden, richtet das Dienstprogramm für die automatische Generierung basierend auf gängigen geschäftlichen Anwendungsfällen Beziehungen zwischen Schemas ein. Daher ist das Bodea-Team nun bereit, Daten basierend auf ihren B2B-Schemas zu erfassen.

>[!NOTE]
> 
>Standardmäßige Identitäts-Namespaces, Primärschlüssel und Beziehungen, die vom Dienstprogramm zur automatischen Generierung für die Schemas erstellt wurden, können im Arbeitsbereich &quot;Schema&quot;leicht gefunden werden.
>
>![Anzeige der standardmäßigen Schema-Identität und der Benutzeroberfläche der Beziehung](./assets/b2b-tutorial/schema-identity-relationship.png)

## Daten in Experience Platform erfassen

Als Nächstes verwendet der Bodea-Marketingexperte die [Marketo Engage-Connector](../sources/connectors/adobe-applications/marketo/marketo.md) , um Daten in Platform zu erfassen und sie für nachgelagerte Dienste zu verwenden. Sie können auch Daten erfassen, indem Sie eine der genehmigten Quellen für die Echtzeit-Kundendatenplattform B2B Edition verwenden.

>[!NOTE]
> 
>Um zu erfahren, welche Quell-Connectoren für Ihr Unternehmen verfügbar sind, können Sie den Quellkatalog in der Platform-Benutzeroberfläche anzeigen. Um auf den Katalog zuzugreifen, wählen Sie **Quellen** Wählen Sie im linken Navigationsbereich die Option **Katalog**.

Um eine Verbindung zwischen einem Marketo-Konto und Platform herzustellen, müssen Sie Authentifizierungsberechtigungen abrufen. Siehe [Handbuch zum Erlangen der Authentifizierungsberechtigungen für den Marketo-Quell-Connector](../sources/connectors/adobe-applications/marketo/marketo-auth.md) für detaillierte Anweisungen.

Nach dem Erwerb von Authentifizierungsberechtigungen erstellt der Bodea-Marketing-Experte eine Verbindung zwischen dem Marketo-Konto und seiner Platform IMS-Organisation. Anweisungen finden Sie in der Dokumentation zu [Anleitung zum Verbinden eines Marketo-Kontos über die Platform-Benutzeroberfläche](../sources/tutorials/ui/create/adobe-applications/marketo.md).

Der Marketo Engage-Quell-Connector bietet eine Funktion zur automatischen Zuordnung, mit der Sie all Ihre Datenfelder den neu erstellten Schemas zuordnen können.

>[!NOTE]
> 
>Wenn Sie benutzerdefinierte Feldergruppen in Ihren XDM-Schemas erstellt haben, verfügen Sie in dieser Phase des Prozesses möglicherweise über nicht verbundene Felder. Überprüfen Sie alle Werte, die Ihre benutzerdefinierten Feldergruppen ausfüllen.

Der Bodea-Marketing-Experte prüft, ob alle Feldergruppen angemessen zugeordnet sind, und führt den Einrichtungsprozess der Quellen durch Initialisierung eines Datenflusses fort. Durch Erstellen eines Datenflusses für Marketo-Daten können eingehende Daten von nachgelagerten Platform-Diensten verwendet werden. Während des anfänglichen Aufnahmevorgangs werden die Daten als Batch in die Experience Platform übernommen. Danach werden nachfolgende aufgenommene Daten mit nahezu Echtzeit-Aktualisierungen an das Profil gestreamt.

## Erstellen eines Segments zur Auswertung Ihrer Daten

Die nächste Aufgabe besteht darin, eine Zielgruppe für die neue E-Mail-Marketing-Kampagne von Bodea zu erstellen, die auf bestimmten Attributen verwandter Entitäten in den Quelldaten basiert. In der Platform-Benutzeroberfläche wählt der Marketing-Experte zunächst **[!UICONTROL Segmente]** in der linken Navigation und **[!UICONTROL Segment erstellen]**.

In diesem Beispiel findet das Segment alle Personen, die in der Verkaufsabteilung arbeiten und mit einem Konto verwandt sind, das mindestens eine Öffnungsmöglichkeit hat. Dieses Segment erfordert eine Verknüpfung zwischen der Klasse &quot;XDM Individual Profile&quot;, der Klasse &quot;XDM Business Account&quot;und der Klasse &quot;XDM Business Opportunity&quot;.

![Anwendungsfallsegment](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Anweisungen zum Erstellen von Segmenten zur Auswertung Ihrer Daten finden Sie unter [Handbuch zur Benutzeroberfläche von Segment Builder](../segmentation/ui/segment-builder.md). Spezifischere Anwendungsfälle für die B2B-Segmentierung finden Sie im Abschnitt [Segmentierungsübersicht für die Echtzeit-Kundendatenplattform B2B Edition](./segmentation/b2b.md).

Mit Segment Builder können Sie aus Echtzeit-Kundenprofildaten eine vermarktbare Zielgruppe erstellen und Schätzungen Ihrer potenziellen Zielgruppe basierend auf der Kombination von Attributen, Ereignissen und vorhandenen Zielgruppen anzeigen, die Sie definiert haben.

## Evaluierte Daten für ein Ziel aktivieren

Nachdem das Segment erfolgreich erstellt wurde, wird im Abschnitt [!UICONTROL Details] des Arbeitsbereichs. Da derzeit keine Ziele für das Segment aktiviert sind, muss der Bodea-Marketing-Experte die Zielgruppe in einen Datensatz exportieren, in dem sie aufgerufen und bearbeitet werden kann.

Innerhalb der [!UICONTROL Segmente] Arbeitsbereich der Platform-Benutzeroberfläche, wählt der Bodea-Marketer **[!UICONTROL Auf Ziel aktivieren]**.

![Aktivieren des Segments für ein Ziel](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Siehe Tutorial zu [Aktivieren eines Segments für ein Ziel](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) für umfassende Schritte, wie dies erreicht werden kann.

Der Bodea-Marketingexperte aktiviert das Segment an das Marketo-Ziel, das es ihm ermöglicht, Segmentdaten in Form einer statischen Liste von Platform zu Marketo Engage zu übertragen. Siehe Handbuch im [Marketo-Ziel](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html?lang=de) für weitere Informationen.

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die verschiedenen Adobe Experience Platform-Dienste genutzt, die von der Echtzeit-CDP B2B Edition verwendet werden. Daher haben Sie gelernt, Ihre B2B-Daten als umsetzbare Zielgruppen zu erfassen, zu segmentieren, zu bewerten und zu exportieren, die über verschiedene Kanäle hinweg interagieren können.
