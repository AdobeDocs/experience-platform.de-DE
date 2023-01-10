---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; einheitliches Profil; Einheitliches Profil; einheitliches Profil; einheitliches Profil; Profil; rtcp; Profil aktivieren; Profil aktivieren; Vereinigungsschema; UNION PROFILE; Vereinigungsprofil
title: UI-Anleitung für Vereinigungsschema
type: Documentation
description: In der Benutzeroberfläche von Adobe Experience Platform können Sie einfach jedes Vereinigungsschema innerhalb Ihres Unternehmens anzeigen und die Felder, Identitäten, Beziehungen und beitragenden Schemas für eine bestimmte Klasse in der Vorschau anzeigen. In diesem Handbuch finden Sie ausführliche Informationen zum Anzeigen und Erkunden von Vereinigungsschemas mithilfe der Platform-Benutzeroberfläche.
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 4%

---

# [!UICONTROL Handbuch zur Vereinigungsschema-Benutzeroberfläche]

In der Benutzeroberfläche von Adobe Experience Platform können Sie einfach jedes Vereinigungsschema innerhalb Ihres Unternehmens anzeigen und die Felder, Identitäten, Beziehungen und beitragenden Schemas für eine bestimmte Klasse in der Vorschau anzeigen. In diesem Handbuch finden Sie ausführliche Informationen zum Anzeigen und Erkunden von Vereinigungsschemas mithilfe der Platform-Benutzeroberfläche.

## Erste Schritte

Dieses UI-Handbuch setzt ein Verständnis der verschiedenen [!DNL Experience Platform] Dienste, die mit der Verwaltung von Echtzeit-Kundenprofildaten verbunden sind. Bevor Sie dieses Handbuch lesen oder in der Benutzeroberfläche arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Real-Time Customer Profile]](../home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Identity Service]](../../identity-service/home.md): Aktiviert [!DNL Real-Time Customer Profile] durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen bei der Erfassung in [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.

## Vereinigungsschemata

Mit dem Echtzeit-Kundenprofil können Sie robuste, zentralisierte Profile erstellen, die Kundenattribute und mit Zeitstempel versehene Ereignisse enthalten. Jede Kundeninteraktion erfolgt auf Systemen, die in Adobe Experience Platform integriert sind. Format und Struktur dieser Daten werden von Experience-Datenmodell (XDM)-Schemas bereitgestellt, wobei jedes Schema auf einer XDM-Klasse basiert und Felder enthält, die mit dieser Klasse kompatibel sind.

Schemas können für mehrere Anwendungsfälle erstellt werden, die auf dieselbe Klasse verweisen, jedoch Felder für ihre Verwendung enthalten. Wenn ein Schema für Profil aktiviert ist, wird es Teil eines Vereinigungsschemas. Mit anderen Worten: Vereinigungsschemas bestehen aus mehreren Schemas, die dieselbe Klasse teilen und für Profile aktiviert wurden. Im Vereinigungsschema können Sie eine Zusammenführung aller Felder sehen, die in Schemas enthalten sind, die dieselbe Klasse haben. Das Echtzeit-Kundenprofil verwendet das Vereinigungsschema, um eine ganzheitliche Ansicht jedes einzelnen Kunden zu erstellen.

Das Arbeiten mit Vereinigungsschemas erfordert ein tiefes Verständnis der XDM-Schemas. Für weitere Informationen lesen Sie bitte zunächst das [Grundlagen der Schemakomposition](../../xdm/schema/composition.md).

## Vereinigungsschemata anzeigen

Um in der Platform-Benutzeroberfläche zu Vereinigungsschemas zu navigieren, wählen Sie **[!UICONTROL Profile]** Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Vereinigungsschema]** Registerkarte. Die [!UICONTROL Vereinigungsschema] wird geöffnet, um das Vereinigungsschema für die aktuell ausgewählte Klasse anzuzeigen.

![Die Seite Vereinigungsschema wird angezeigt, wobei die Registerkarte Profil und Vereinigungsschema hervorgehoben ist.](../images/union-schema/landing.png)

## Auswählen einer Klasse

Um das Vereinigungsschema für eine bestimmte XDM-Klasse anzuzeigen, wählen Sie die Klasse aus der **[!UICONTROL Klasse]** Dropdown-Liste. Da nicht alle Klassen Vereinigungsschemas haben, sind nur Klassen mit Vereinigungsschemas (d. h. Klassen mit Schemas, die für Profil aktiviert wurden) in der Dropdown-Liste verfügbar.

Nachdem eine Klasse ausgewählt wurde, wird das angezeigte Schema aktualisiert, um das Vereinigungsschema für die ausgewählte Klasse widerzuspiegeln. Sie können beispielsweise **[!UICONTROL XDM Individual Profile]** , um das Vereinigungsschema für diese Klasse anzuzeigen.

![Eine Dropdown-Liste mit den Klassen des Vereinigungsschemas wird hervorgehoben.](../images/union-schema/class.png)

## Vereinigungsschemas durchsuchen

Sie können das Vereinigungsschema erkunden, indem Sie nach oben und unten scrollen, um die gesamte Schemastruktur anzuzeigen, und indem Sie eine rechte Winkelklammer (`>`), um verschachtelte Felder zu erweitern.

![Ein Satz verschachtelter Felder im Vereinigungsschema wird erweitert.](../images/union-schema/explore.png)

Wählen Sie ein beliebiges Feld aus, um dessen Details anzuzeigen, einschließlich Anzeigename, Datentyp, Beschreibung, Pfad, Erstellungsdatum und Datum der letzten Änderung. Sie können auch eine Liste der beitragenden Schemata anzeigen, die das ausgewählte Feld enthalten.

![Ein Vereinigungsschemafeld wird hervorgehoben. Details zum hervorgehobenen Feld werden auf der rechten Seitenleiste angezeigt.](../images/union-schema/explore-field.png)

Wenn Sie den Namen eines beitragenden Schemas auswählen, werden die Namen der Datensätze angezeigt, die sich auf dieses Schema beziehen und Daten in das ausgewählte Feld aufnehmen. Jeder Datensatzname wird als Link angezeigt. Wenn Sie einen Datensatznamen auswählen, wird die Registerkarte &quot;Aktivität&quot;für diesen Datensatz in einem neuen Fenster geöffnet.

Weitere Informationen zu Datensätzen, einschließlich Anzeigen der Datensatzaktivität und Anzeigen der Vorschau von Datensatzdaten in der Benutzeroberfläche finden Sie unter [Benutzerhandbuch zu Datensätzen](../../catalog/datasets/user-guide.md).

![Die Liste der mit dem Schema verknüpften Datensätze wird hervorgehoben.](../images/union-schema/datasets.png)

## Beitragsschemata anzeigen

Durch Auswahl von **[!UICONTROL Alle beitragenden Schemata]** um die Liste der Schemas zu erweitern. Je nach ausgewählter Klasse und der Anzahl der Schemas, die Ihr Unternehmen in Platform erstellt hat, kann es sich hierbei um eine Kurzliste mit einem einzelnen Schema oder einer langen Liste mit vielen Schemas handeln.

![Die Liste der Schemas, die zum Vereinigungsschema beitragen, wird hervorgehoben.](../images/union-schema/contributing-schemas.png)

Wenn Sie den Namen eines bestimmten Schemas auswählen, werden die Felder im Vereinigungsschema hervorgehoben, die Teil des ausgewählten Schemas sind. Nachdem ein Schema ausgewählt wurde, wird das Vereinigungsschema grau mit schwarzen Balken dargestellt, die die Felder angeben, die Teil des beitragenden Schemas sind.

![Das ausgewählte Beitragsschema wird hervorgehoben. Die Felder, die Teil des Beitragsschemas sind, bleiben schwarz, während die Felder, die nicht Teil des beitragenden Schemas sind, grau dargestellt werden.](../images/union-schema/select-schema.png)

## Identitäten anzeigen

Über die Benutzeroberfläche können Sie eine Liste der Identitäten anzeigen, die im Vereinigungsschema enthalten sind, indem Sie **[!UICONTROL Identitäten]** , um die Liste zu erweitern.

![Die Identitäten, die zum Vereinigungsschema gehören, werden hervorgehoben.](../images/union-schema/identities.png)

Wenn Sie eine individuelle Identität aus der Liste auswählen, wird das angezeigte Schema bei Bedarf automatisch aktualisiert, um das Identitätsfeld anzuzeigen. Dies kann die Erweiterung mehrerer Felder umfassen, wenn das Identitätsfeld verschachtelt ist.

Das Identitätsfeld wird im Vereinigungsschema hervorgehoben und die Details der Identität werden auf der rechten Seite des Bildschirms angezeigt. Die Details enthalten eine Liste der beitragenden Schemas, die das Identitätsfeld enthalten. Sie können einen Drilldown durchführen, um Links zu den mit diesem Schema verknüpften Datensätzen zu finden, die Daten in das ausgewählte Identitätsfeld aufnehmen.

![Die ausgewählte Identität wird hervorgehoben. Details zur ausgewählten Identität werden auf der rechten Seitenleiste angezeigt.](../images/union-schema/select-identity.png)

## Beziehungen anzeigen

Die Benutzeroberfläche für Vereinigungsschemas ermöglicht Ihnen auch, Beziehungen anzuzeigen, die für Schemas basierend auf der ausgewählten Schemaklasse definiert wurden. Die Definition einer Beziehung ist eine Möglichkeit, zwei Schemas zu verbinden, die zu verschiedenen Klassen gehören, um komplexere Einblicke in Kundendaten zu erhalten.

Wenn für die ausgewählte Klasse Beziehungen hergestellt wurden, wählen Sie **[!UICONTROL Beziehungen]** zeigt eine Liste der Felder an, die zum Erstellen von Beziehungen verwendet werden. Nicht alle Schemata verwenden oder müssen Beziehungen definiert werden. Daher ist es üblich, dass der Abschnitt &quot;Beziehungen&quot;keine Felder enthält.

Weitere Informationen zu Schemabeziehungen, einschließlich ihrer Definition über die Benutzeroberfläche, finden Sie unter [Dieses Dokument zu Schemabeziehungen](../../xdm/tutorials/relationship-ui.md).

![Die Beziehungen, die zum Vereinigungsschema gehören, werden hervorgehoben.](../images/union-schema/relationships.png)

Wenn Sie ein Beziehungsfeld aus der Liste auswählen, wird das angezeigte Schema bei Bedarf aktualisiert, um das hervorgehobene Beziehungsfeld anzuzeigen. Dies kann die Erweiterung mehrerer Felder umfassen, wenn das Beziehungsfeld verschachtelt ist.

![Die ausgewählte Beziehung wird hervorgehoben. Das entsprechende Feld für die Beziehung wird ebenfalls hervorgehoben.](../images/union-schema/select-relationship.png)

## Nächste Schritte

Durch Lesen dieses Handbuchs wissen Sie jetzt, wie Sie Vereinigungsschemas mithilfe der [!DNL Experience Platform] Benutzeroberfläche. Weitere Informationen zu Schemata, einschließlich ihrer Verwendung in der gesamten Plattform, erhalten Sie im Abschnitt [XDM-System - Übersicht](../../xdm/home.md).
