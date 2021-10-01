---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Identität; Feld;
solution: Experience Platform
title: Identitätsfelder in der Benutzeroberfläche definieren
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Experience Platform ein Identitätsfeld definieren.
topic-legacy: user guide
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Identitätsfelder in der Benutzeroberfläche definieren

Im Experience-Datenmodell (XDM) stellt ein Identitätsfeld ein Feld dar, das zur Identifizierung einer einzelnen Person verwendet werden kann, die mit einem Datensatz- oder Zeitreihenereignis verbunden ist. In diesem Dokument wird beschrieben, wie Sie ein Identitätsfeld in der Adobe Experience Platform-Benutzeroberfläche definieren.

## Voraussetzungen

Identitätsfelder sind eine entscheidende Komponente bei der Erstellung von Identitätsdiagrammen für Kunden in Platform. Dies hat letztendlich Auswirkungen darauf, wie Echtzeit-Kundenprofil verschiedene Datenfragmente zusammenführt, um eine vollständige Ansicht des Kunden zu erhalten. Bevor Sie Identitätsfelder in Ihren Schemas definieren, lesen Sie die folgende Dokumentation, um mehr über die wichtigsten Dienste und Konzepte im Zusammenhang mit Identitätsfeldern zu erfahren:

* [Adobe Experience Platform Identity-Dienst](../../../identity-service/home.md): Brilliert Identitäten zwischen Geräten und Systemen und verknüpft Datensätze anhand der Identitätsfelder, die von den XDM-Schemas definiert werden, mit denen sie übereinstimmen.
   * [Identitäts-Namespaces](../../../identity-service/namespaces.md): Identitäts-Namespaces definieren die verschiedenen Arten von Identitätsinformationen, die sich auf eine einzelne Person beziehen können und eine erforderliche Komponente für jedes Identitätsfeld sind.
* [Echtzeit-Kundenprofil](../../../profile/home.md): Nutzen von Identitätsdiagrammen für Kunden, um ein einheitliches Verbraucherprofil basierend auf aggregierten Daten aus mehreren Quellen bereitzustellen, die nahezu in Echtzeit aktualisiert werden.

## Identitätsfeld definieren

Wenn Sie [ein neues Feld](./overview.md#define) in der Benutzeroberfläche definieren, können Sie es als Identitätsfeld festlegen, indem Sie in der rechten Leiste das Kontrollkästchen **[!UICONTROL Identität]** aktivieren.

![](../../images/ui/fields/special/identity.png)

Zusätzliche Steuerelemente werden angezeigt, nachdem Sie das Kontrollkästchen aktiviert haben. Wenn dieses Feld die primäre Identität für das Schema sein soll, aktivieren Sie das Kontrollkästchen **[!UICONTROL Primäre Identität]** .

>[!NOTE]
>
>Für ein einzelnes Schema können viele Identitätsfelder definiert sein, es kann jedoch nur eine primäre Identität geben. Alle Identitätsfelder (primär oder anderweitig) tragen zum Identitätsdiagramm für einen einzelnen Kunden bei, aber das Echtzeit-Kundenprofil verwendet beim Zusammenführen von Datenfragmenten nur die primäre Identität als &quot;Source of Truth&quot;. Wenn Sie ein Schema zur Verwendung im Profil aktivieren möchten, muss das Schema über eine primäre Identität verfügen.

Wählen Sie unter **[!UICONTROL Identitäts-Namespace]** im Dropdown-Menü den entsprechenden Namespace für das Identitätsfeld aus. Von Adobe bereitgestellte Standard-Namespaces sowie alle benutzerdefinierten Namespaces, die von Ihrem Unternehmen definiert wurden, werden aufgelistet.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus, um die Änderung auf das Schema anzuwenden.

![](../../images/ui/fields/special/identity-config.png)

Die Arbeitsfläche wird aktualisiert, um die Änderungen widerzuspiegeln, wobei das ausgewählte Feld ein Fingerabdrucksymbol (![](../../images/ui/fields/special/identity-symbol.png)) erhält, um es als Identität zu kennzeichnen. In der linken Leiste wird das Identitätsfeld jetzt unter dem Namen der Klasse oder Schemafeldgruppe aufgeführt, die das Feld für das Schema bereitstellt.

Da alle Identitätsfelder standardmäßig erforderlich sind, wird das Feld jetzt in der linken Leiste unter **[!UICONTROL Erforderliche Felder]** aufgeführt. Wenn das Identitätsfeld innerhalb der Schemastruktur verschachtelt ist, werden auch alle übergeordneten Felder nach Bedarf aufgelistet.

![](../../images/ui/fields/special/identity-applied.png)

Wenn Sie eine primäre Identität für das Schema definiert haben, können Sie jetzt mit [das Schema zur Verwendung im Echtzeit-Kundenprofil](../resources/schemas.md#profile) aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein Identitätsfeld in der Benutzeroberfläche definieren. Da Daten mit diesem Schema erfasst werden, werden Ihre Identitätsdiagramme aktualisiert, um die Identitätsfelder des Schemas widerzuspiegeln. Weitere Informationen zum Erkunden des privaten Diagramms Ihres Unternehmens in der Benutzeroberfläche finden Sie im Handbuch zum Viewer für Identitätsdiagramme [a1/> .](../../../identity-service/ui/identity-graph-viewer.md)

Informationen zum Definieren anderer XDM-Feldtypen im [!DNL Schema Editor] finden Sie in der Übersicht zu [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special).
