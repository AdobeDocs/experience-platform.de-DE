---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Datenmodell;UI;Arbeitsbereich;Identität;Feld;
solution: Experience Platform
title: Definieren von Identitätsfeldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Experience Platform ein Identitätsfeld definieren.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 3570197ca6cff95368b4facb034386e793033fe2
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 15%

---

# Definieren von Identitätsfeldern in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) stellt ein Identitätsfeld ein Feld dar, das zur Identifizierung einer einzelnen Person verwendet werden kann, die mit einem Datensatz- oder Zeitreihenereignis in Verbindung steht. In diesem Dokument wird beschrieben, wie Sie ein Identitätsfeld in der Adobe Experience Platform-Benutzeroberfläche definieren.

## Voraussetzungen

Identitätsfelder sind eine wichtige Komponente bei der Erstellung von Kundenidentitätsdiagrammen in Experience Platform, was sich letztendlich darauf auswirkt, wie das Echtzeit-Kundenprofil unterschiedliche Datenfragmente zusammenführt, um einen vollständigen Überblick über den Kunden zu erhalten. Bevor Sie Identitätsfelder in Ihren Schemata definieren, lesen Sie die folgende Dokumentation, um mehr über die wichtigsten Services und Konzepte im Zusammenhang mit Identitätsfeldern zu erfahren:

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Führt Identitäten zwischen Geräten und Systemen zusammen und verknüpft Datensätze anhand der Identitätsfelder, die von den entsprechenden XDM-Schemata definiert werden.
   * [Identity-Namespaces](../../../identity-service/features/namespaces.md): In Identity-Namespaces werden die verschiedenen Arten von Identitätsinformationen definiert, die sich auf eine einzelne Person beziehen können. Sie sind eine erforderliche Komponente für jedes Identitätsfeld.
* [Echtzeit-Kundenprofil](../../../profile/home.md): Nutzt Kundenidentitätsdiagramme, um ein einheitliches Kundenprofil bereitzustellen, das auf aggregierten Daten aus mehreren Quellen basiert und nahezu in Echtzeit aktualisiert wird.

## Definieren eines Identitätsfelds {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Einschränkungen der primären Identität"
>abstract="Dieses Schema verwendet eine Feldergruppe, die zur Verwendung in einer bestimmten Quellverbindung vorgesehen ist. Für diese Verbindung muss identityMap als primäre Identität verwendet werden, weshalb sie automatisch festgelegt ist."

Beim [Definieren eines neuen Felds](./overview.md#define) können Sie es in der Benutzeroberfläche als Identitätsfeld festlegen, indem Sie das Kontrollkästchen **[!UICONTROL Identität]** in der rechten Leiste auswählen.

![](../../images/ui/fields/special/identity.png)

Zusätzliche Steuerelemente werden angezeigt, nachdem Sie das Kontrollkästchen aktiviert haben. Wenn Sie möchten, dass dieses Feld die primäre Identität für das Schema ist, aktivieren Sie das Kontrollkästchen **[!UICONTROL Primäre]**.

>[!NOTE]
>
>Für ein einzelnes Schema können viele Identitätsfelder definiert sein, es kann jedoch nur eine primäre Identität vorhanden sein. Alle Identitätsfelder (primär oder anderweitig) tragen zum Identitätsdiagramm für einen einzelnen Kunden bei, aber das Echtzeit-Kundenprofil verwendet beim Zusammenführen von Datenfragmenten nur die primäre Identität als Datenquelle. Wenn Sie ein Schema für die Verwendung im Profil aktivieren möchten, muss für das Schema eine primäre Identität definiert sein.

Wählen **[!UICONTROL unter]** Identity-Namespace) im Dropdown-Menü den entsprechenden Namespace für das Identitätsfeld aus. Die von Adobe bereitgestellten Standard-Namespaces werden zusammen mit den von Ihrem Unternehmen definierten benutzerdefinierten Namespaces aufgelistet.

Wenn Sie fertig sind, wählen **[!UICONTROL Übernehmen]** aus, um die Änderung auf das Schema anzuwenden.

>[!IMPORTANT]
>
>Sobald ein Schema für die Verwendung im Echtzeit-Kundenprofil aktiviert ist und Daten aufgenommen wurden, **Sie das primäre Identitätsfeld nicht mehr ändern**. Der Versuch, dies zu tun, führt zu einem Validierungsfehler. Wenn Sie eine andere primäre Identität verwenden müssen, müssen Sie ein neues Schema und einen neuen Datensatz mit der aktualisierten Identitätskonfiguration erstellen.

![](../../images/ui/fields/special/identity-config.png)

Die Arbeitsfläche wird aktualisiert, um die Änderungen widerzuspiegeln, wobei das ausgewählte Feld ein Fingerabdrucksymbol (![](/help/images/icons/identity-service.png)) erhält, um es als Identität zu kennzeichnen. In der linken Leiste wird das Identitätsfeld jetzt unter dem Namen der Klasse oder Schemafeldgruppe aufgeführt, die das Feld für das Schema bereitstellt.

Wenn das Feld auch als primäre Identität festgelegt wurde, wird es auch unter **[!UICONTROL Erforderliche Felder]** in der linken Leiste aufgeführt. Wenn das Identitätsfeld in der Schemastruktur verschachtelt ist, werden alle übergeordneten Felder ebenfalls nach Bedarf aufgelistet.

![](../../images/ui/fields/special/identity-applied.png)

Wenn Sie eine primäre Identität für das Schema definiert haben, können Sie jetzt mit [Aktivieren des Schemas zur Verwendung im Echtzeit-Kundenprofil](../resources/schemas.md#profile) fortfahren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein Identitätsfeld in der Benutzeroberfläche definieren. Bei der Aufnahme von Daten mit diesem Schema werden Ihre Kundenidentitätsdiagramme aktualisiert, um die Identitätsfelder des Schemas widerzuspiegeln. Im Handbuch zum [Identitätsdiagramm-Viewer](../../../identity-service/features/identity-graph-viewer.md) erfahren Sie, wie Sie das private Diagramm Ihres Unternehmens in der Benutzeroberfläche untersuchen können.

In der Übersicht über [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special) erfahren Sie, wie Sie andere XDM-Feldtypen in der [!DNL Schema Editor] definieren.
