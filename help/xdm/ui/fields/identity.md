---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Identität; Feld;
solution: Experience Platform
title: Identitätsfelder in der Benutzeroberfläche definieren
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche ein Identitätsfeld definieren.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: d1b571fe72208cf2f2ae339273f05cc38dda9845
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 16%

---

# Definieren von Identitätsfeldern in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) stellt ein Identitätsfeld ein Feld dar, das zur Identifizierung einer einzelnen Person verwendet werden kann, die mit einem Datensatz- oder Zeitreihenereignis verbunden ist. In diesem Dokument wird beschrieben, wie Sie ein Identitätsfeld in der Adobe Experience Platform-Benutzeroberfläche definieren.

## Voraussetzungen

Identitätsfelder sind eine entscheidende Komponente bei der Erstellung von Identitätsdiagrammen für Kunden in Platform. Dies hat letztendlich Auswirkungen darauf, wie Echtzeit-Kundenprofil verschiedene Datenfragmente zusammenführt, um eine vollständige Ansicht des Kunden zu erhalten. Bevor Sie Identitätsfelder in Ihren Schemas definieren, lesen Sie die folgende Dokumentation, um mehr über die wichtigsten Dienste und Konzepte im Zusammenhang mit Identitätsfeldern zu erfahren:

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Führt Identitäten zwischen Geräten und Systemen zusammen und verknüpft Datensätze anhand der Identitätsfelder, die von den entsprechenden XDM-Schemata definiert werden.
   * [Identity-Namespaces](../../../identity-service/features/namespaces.md): In Identity-Namespaces werden die verschiedenen Arten von Identitätsinformationen definiert, die sich auf eine einzelne Person beziehen können. Sie sind eine erforderliche Komponente für jedes Identitätsfeld.
* [Echtzeit-Kundenprofil](../../../profile/home.md): Nutzen von Diagrammen zur Kundenidentität, um ein einheitliches Verbraucherprofil bereitzustellen, das auf aggregierten Daten aus mehreren Quellen basiert und nahezu in Echtzeit aktualisiert wird.

## Definieren eines Identitätsfelds {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Einschränkungen der primären Identität"
>abstract="Dieses Schema verwendet eine Feldergruppe, die zur Verwendung in einer bestimmten Quellverbindung vorgesehen ist. Für diese Verbindung muss identityMap als primäre Identität verwendet werden, weshalb sie automatisch festgelegt ist."

Wenn Sie [ein neues Feld definieren](./overview.md#define) in der Benutzeroberfläche, können Sie es als Identitätsfeld festlegen, indem Sie in der rechten Leiste das Kontrollkästchen **[!UICONTROL Identität]** aktivieren.

![](../../images/ui/fields/special/identity.png)

Zusätzliche Steuerelemente werden angezeigt, nachdem Sie das Kontrollkästchen aktiviert haben. Wenn dieses Feld die primäre Identität für das Schema sein soll, aktivieren Sie das Kontrollkästchen **[!UICONTROL Primäre Identität]** .

>[!NOTE]
>
>Für ein einzelnes Schema können viele Identitätsfelder definiert sein, es kann jedoch nur eine primäre Identität geben. Alle Identitätsfelder (primär oder anderweitig) tragen zum Identitätsdiagramm für einen einzelnen Kunden bei, aber das Echtzeit-Kundenprofil verwendet beim Zusammenführen von Datenfragmenten nur die primäre Identität als &quot;Source of Truth&quot;. Wenn Sie ein Schema zur Verwendung im Profil aktivieren möchten, muss das Schema über eine primäre Identität verfügen.

Wählen Sie unter **[!UICONTROL Identitäts-Namespace]** im Dropdown-Menü den entsprechenden Namespace für das Identitätsfeld aus. Von Adobe bereitgestellte Standard-Namespaces sowie alle von Ihrem Unternehmen definierten benutzerdefinierten Namespaces werden aufgelistet.

Wählen Sie abschließend **[!UICONTROL Anwenden]** aus, um die Änderung auf das Schema anzuwenden.

![](../../images/ui/fields/special/identity-config.png)

Die Arbeitsfläche wird aktualisiert, um die Änderungen widerzuspiegeln, wobei das ausgewählte Feld ein Fingerabdrucksymbol (![](/help/images/icons/identity-service.png)) erhält, um es als Identität zu kennzeichnen. In der linken Leiste wird das Identitätsfeld jetzt unter dem Namen der Klasse oder Schemafeldgruppe aufgeführt, die das Feld für das Schema bereitstellt.

Wenn das Feld auch als primäre Identität festgelegt wurde, wird es auch unter **[!UICONTROL Erforderliche Felder]** in der linken Leiste aufgeführt. Wenn das Identitätsfeld innerhalb der Schemastruktur verschachtelt ist, werden auch alle übergeordneten Felder nach Bedarf aufgelistet.

![](../../images/ui/fields/special/identity-applied.png)

Wenn Sie eine primäre Identität für das Schema definiert haben, können Sie jetzt mit [das Schema zur Verwendung im Echtzeit-Kundenprofil aktivieren](../resources/schemas.md#profile).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein Identitätsfeld in der Benutzeroberfläche definieren. Da Daten mit diesem Schema erfasst werden, werden Ihre Identitätsdiagramme aktualisiert, um die Identitätsfelder des Schemas widerzuspiegeln. Informationen zum Erkunden des privaten Diagramms Ihres Unternehmens in der Benutzeroberfläche finden Sie im Handbuch zum Viewer für Identitätsdiagramme](../../../identity-service/features/identity-graph-viewer.md) .[

Informationen zum Definieren anderer XDM-Feldtypen in der [!DNL Schema Editor] finden Sie in der Übersicht zu [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special) .
