---
title: Definieren einer Beziehung zwischen zwei Schemas in der Echtzeit-Kundendatenplattform B2B Edition
description: Erfahren Sie, wie Sie in der Echtzeit-Kundendatenplattform B2B Edition eine n:1-Beziehung zwischen zwei Schemas definieren.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: 2ad20a4c7a9d1cc71fc4e589de90d7eabf8c87b7
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 7%

---

# Definieren einer Beziehung zwischen zwei Schemas in der Echtzeit-Kundendatenplattform B2B Edition (Beta)

>[!IMPORTANT]
>
>Die Echtzeit-Kundendatenplattform B2B Edition befindet sich derzeit in der Betaphase. Dokumentation und Funktionalität können sich ändern.

>[!NOTE]
>
>Wenn Sie die Echtzeit-Kundendatenplattform B2B Edition nicht verwenden, lesen Sie stattdessen das Handbuch zum Erstellen einer Nicht-B2B-Beziehung](./relationship-ui.md) .[

Die Echtzeit-Kundendatenplattform B2B Edition bietet mehrere Experience-Datenmodell (XDM)-Klassen, die grundlegende B2B-Datenentitäten erfassen, darunter [Konten](../classes/b2b/business-account.md), [Chancen](../classes/b2b/business-opportunity.md), [Kampagnen](../classes/b2b/business-campaign.md) und mehr. Indem Sie Schemas erstellen, die auf diesen Klassen basieren, und sie zur Verwendung in [Echtzeit-Kundenprofil](../../profile/home.md) aktivieren, können Sie Daten aus unterschiedlichen Quellen zu einer einheitlichen Darstellung zusammenführen, die als Vereinigungsschema bezeichnet wird.

Vereinigungsschemata dürfen jedoch nur Felder enthalten, die von Schemas erfasst werden, die dieselbe Klasse verwenden. Hier kommen die Schemabeziehungen an. Durch die Implementierung von Beziehungen in Ihre B2B-Schemas können Sie beschreiben, wie sich diese Geschäftsentitäten gegenseitig beeinflussen, und Attribute aus mehreren Klassen in Anwendungsfällen für nachgelagerte Segmentierung einbeziehen.

Das folgende Diagramm zeigt ein Beispiel dafür, wie die verschiedenen B2B-Klassen in einer Basisimplementierung miteinander in Beziehung stehen können:

![B2B-Klassenbeziehungen](../images/tutorials/relationship-b2b/classes.png)

In diesem Tutorial werden die Schritte zum Definieren einer 1:1-Beziehung zwischen zwei Schemas in der Echtzeit-CDP B2B Edition beschrieben.

>[!NOTE]
>
>In diesem Tutorial wird beschrieben, wie Sie in der Platform-Benutzeroberfläche manuell Beziehungen zwischen B2B-Schemas herstellen. Wenn Sie Daten aus einer B2B-Quellverbindung einbringen, können Sie stattdessen ein Dienstprogramm zur automatischen Generierung verwenden, um die erforderlichen Schemas, Identitäten und Beziehungen zu erstellen. Weitere Informationen zu [Verwendung des Dienstprogramm zur automatischen Erzeugung](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) finden Sie in der Quelldokumentation zu B2B-Namespaces und -Schemata .

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis von [!DNL XDM System] und des Schema-Editors in der Benutzeroberfläche von [!DNL Experience Platform] voraus. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und dessen Implementierung in  [!DNL Experience Platform].
* [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [Erstellen Sie ein Schema mit [!DNL Schema Editor]](create-schema-ui.md): Ein Tutorial, in dem die Grundlagen zum Erstellen und Bearbeiten von Schemas in der Benutzeroberfläche erläutert werden.

## Quell- und Zielschemas definieren

Wir gehen davon aus, dass Sie die beiden Schemas, die in der Beziehung definiert werden sollen, bereits erstellt haben. Zu Demonstrationszwecken erstellt dieses Tutorial eine Beziehung zwischen Geschäftschancen (definiert in einem Schema &quot;[!DNL Opportunities]&quot;) und dem zugehörigen Geschäftskonto (definiert in einem Schema &quot;[!DNL Accounts]&quot;).

Schemabeziehungen werden durch ein dediziertes Feld innerhalb eines **Quellschemas** dargestellt, das auf das primäre Identitätsfeld eines **Zielschemas** verweist. In den folgenden Schritten dient &quot;[!DNL Opportunities]&quot;als Quellschema, während &quot;[!DNL Accounts]&quot;als Zielschema dient.

### Identitäten in B2B-Beziehungen verstehen

Um eine Beziehung herzustellen, müssen beide Schemas definierte primäre Identitäten aufweisen und für [!DNL Real-time Customer Profile] aktiviert sein. Beachten Sie beim Festlegen einer primären Identität für eine B2B-Entität, dass sich die Zeichenfolgen-basierten Entitäts-IDs überschneiden können, wenn Sie sie über verschiedene Systeme oder Standorte hinweg erfassen. Dies könnte zu Datenkonflikten in Platform führen.

Dazu enthalten alle standardmäßigen B2B-Klassen &quot;key&quot;-Felder, die dem [[!UICONTROL B2B Source]-Datentyp](../data-types/b2b-source.md) entsprechen. Dieser Datentyp stellt Felder für eine Zeichenfolgenkennung für die B2B-Entität zusammen mit anderen Kontextinformationen zur Quelle der Kennung bereit. Eines dieser Felder, `sourceKey`, verkettet die Werte der anderen Felder im Datentyp, um eine vollständig eindeutige Kennung für die Entität zu erstellen. Dieses Feld sollte immer als primäre Identität für B2B-Entitätsschemas verwendet werden.

![sourceKey-Feld](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Wenn Sie [ein XDM-Feld als Identität](../ui/fields/identity.md) festlegen, müssen Sie einen Identitäts-Namespace bereitstellen, unter dem die Identität definiert wird. Dies kann ein von Adobe bereitgestellter Standard-Namespace oder ein von Ihrem Unternehmen definierter benutzerdefinierter Namespace sein. In der Praxis ist der Namespace lediglich eine kontextbezogene Zeichenfolge und kann auf einen beliebigen Wert festgelegt werden, vorausgesetzt, er ist für Ihre Organisation für die Kategorisierung des Identitätstyps sinnvoll. Weitere Informationen finden Sie in der Übersicht zu [Identitäts-Namespaces](../../identity-service/namespaces.md) .

Zu Referenzzwecken wird in den folgenden Abschnitten die Struktur der einzelnen Schemas beschrieben, die in dieser Anleitung verwendet werden, bevor eine Beziehung definiert wird. Beachten Sie, wo die primären Identitäten in der Schemastruktur und in den von ihnen verwendeten benutzerdefinierten Namespaces definiert wurden.

### [!DNL Opportunities] schema

Das Quellschema &quot;[!DNL Opportunities]&quot;basiert auf der Klasse [!UICONTROL XDM Business Opportunity] . Eines der von der -Klasse bereitgestellten Felder `opportunityKey` dient als Kennung für das Schema. Insbesondere wird das Feld `sourceKey` unter dem Objekt `opportunityKey` als primäre Identität des Schemas unter einem benutzerdefinierten Namespace namens [!DNL B2B Opportunity] festgelegt.
Wie unter **[!UICONTROL Schemaeigenschaften]** zu sehen ist, wurde dieses Schema zur Verwendung in [!DNL Real-time Customer Profile] aktiviert.

![Opportunities-Schema](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

Das Zielschema &quot;[!DNL Accounts]&quot;basiert auf der Klasse [!UICONTROL XDM-Konto] . Das Feld `accountKey` auf der Stammebene enthält das `sourceKey` -Feld, das als primäre Identität unter einem benutzerdefinierten Namespace namens [!DNL B2B Account] fungiert. Dieses Schema wurde auch für die Verwendung in Profil aktiviert.

![Kontoschema](../images/tutorials/relationship-b2b/accounts.png)

## Beziehungsfeld für das Quellschema definieren {#relationship-field}

Um eine Beziehung zwischen zwei Schemas zu definieren, muss das Quellschema über ein dediziertes Feld verfügen, das auf die primäre Identität des Zielschemas verweist. Standard-B2B-Klassen enthalten dedizierte Quellschlüsselfelder für häufig verwandte Geschäftsentitäten. Beispielsweise enthält die Klasse [!UICONTROL XDM Business Opportunity] Quellschlüsselfelder für ein verwandtes Konto (`accountKey`) und eine zugehörige Kampagne (`campaignKey`). Sie können dem Schema jedoch auch andere [!UICONTROL B2B Source]-Felder hinzufügen, indem Sie benutzerdefinierte Feldergruppen verwenden, wenn Sie mehr als die Standardkomponenten benötigen.

>[!NOTE]
>
>Derzeit können nur n:n-Beziehungen von einem Quellschema zu einem Zielschema definiert werden. Bei 1:n-Beziehungen müssen Sie das Beziehungsfeld im Schema definieren, das die &quot;viele&quot;darstellt.

Um ein Beziehungsfeld festzulegen, wählen Sie auf der Arbeitsfläche das Pfeilsymbol (![Pfeilsymbol](../images/tutorials/relationship-b2b/arrow.png)) neben dem betreffenden Feld aus. Im Fall des Schemas [!DNL Opportunities] ist dies das Feld `accountKey.sourceKey` , da das Ziel darin besteht, eine n:1-Beziehung zu einem Konto herzustellen.

![Schaltfläche &quot;Beziehung&quot;](../images/tutorials/relationship-b2b/relationship-button.png)

Es wird ein Dialogfeld angezeigt, in dem Sie Details zur Beziehung angeben können. Der Beziehungstyp wird automatisch auf **[!UICONTROL Viele-zu-eins]** gesetzt.

![Dialog über Beziehungen](../images/tutorials/relationship-b2b/relationship-dialog.png)

Verwenden Sie unter **[!UICONTROL Referenzschema]** die Suchleiste, um den Namen des Zielschemas zu suchen. Wenn Sie den Namen des Zielschemas markieren, wird das Feld **[!UICONTROL Referenz-Identitäts-Namespace]** automatisch auf den Namespace der primären Identität des Schemas aktualisiert.

![Referenzschema](../images/tutorials/relationship-b2b/reference-schema.png)

Geben Sie unter **[!UICONTROL Relationship Name From Current Schema]** und **[!UICONTROL Relationship Name From Reference Schema]** Anzeigenamen für die Beziehung im Kontext des Quell- bzw. Zielschemas an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]** aus, um die Änderungen anzuwenden und das Schema zu speichern.

![Beziehungsname](../images/tutorials/relationship-b2b/relationship-name.png)

Die Arbeitsfläche wird wieder angezeigt, wobei das Beziehungsfeld jetzt mit dem Anzeigenamen markiert ist, den Sie zuvor angegeben haben. Der Beziehungsname wird auch in der linken Leiste zur einfachen Referenz aufgeführt.

![Angewendete Beziehung](../images/tutorials/relationship-b2b/relationship-applied.png)

Wenn Sie die Struktur des Zielschemas anzeigen, wird die Beziehungsmarke neben dem primären Identitätsfeld des Schemas und in der linken Leiste angezeigt.

![Zielschema-Beziehungsmarkierung](../images/tutorials/relationship-b2b/destination-relationship.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe von [!DNL Schema Editor] erfolgreich eine n:1-Beziehung zwischen zwei Schemas erstellt. Sobald Daten mit Datensätzen erfasst wurden, die auf diesen Schemas basieren, und diese Daten im Profildatenspeicher aktiviert wurden, können Sie Attribute aus beiden Schemas für Anwendungsfälle der Segmentierung mehrerer Klassen verwenden. Weitere Informationen finden Sie in der Dokumentation zur Echtzeit-Kundendatenplattform B2B Edition .
