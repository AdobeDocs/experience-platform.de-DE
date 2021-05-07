---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;XDM-System;Erlebnisdatenmodell;Datenmodell;ui;Arbeitsbereich;Identitätsfeld;
solution: Experience Platform
title: Identitätsfelder in der Benutzeroberfläche definieren
description: Erfahren Sie, wie Sie ein Identitätsfeld in der Benutzeroberfläche "Experience Platform"definieren.
topic-legacy: user guide
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Identitätsfelder in der Benutzeroberfläche definieren

Im Erlebnis-Datenmodell (XDM) stellt ein Identitätsfeld ein Feld dar, das zur Identifizierung einer einzelnen Person verwendet werden kann, die mit einem Datensatz- oder Zeitreihen-Ereignis in Zusammenhang steht. In diesem Dokument wird beschrieben, wie Sie ein Identitätsfeld in der Adobe Experience Platform-Benutzeroberfläche definieren.

## Voraussetzungen 

Identitätsfelder sind eine entscheidende Komponente bei der Konstruktion von Diagrammen zur Kundenidentität in Plattform. Dies wirkt sich letztlich darauf aus, wie Echtzeit-Kundendaten unterschiedliche Datenfragmente zusammenführen, um eine vollständige Ansicht des Kunden zu erhalten. Bevor Sie Identitätsfelder in Ihren Schemas definieren, lesen Sie bitte die folgende Dokumentation, um sich über die wichtigsten Dienste und Konzepte im Zusammenhang mit Identitätsfeldern zu informieren:

* [Adobe Experience Platform-Identitätsdienst](../../../identity-service/home.md): Überbrückt Identitäten zwischen Geräten und Systemen und verknüpft Datensätze anhand der Identitätsfelder, die von den XDM-Schemas definiert werden, denen sie entsprechen.
   * [Identitäts-Namensraum](../../../identity-service/namespaces.md): Identitäts-Namensraum definieren die verschiedenen Identitätsinformationen, die sich auf eine einzelne Person beziehen können und für jedes Identitätsfeld eine erforderliche Komponente darstellen.
* [Echtzeit-Profil](../../../profile/home.md): Nutzen von Diagrammen zur Kundenidentität, um ein einheitliches Profil auf der Grundlage aggregierter Daten aus mehreren Quellen bereitzustellen, die in Echtzeit aktualisiert werden.

## Identitätsfeld definieren

Wenn Sie [ein neues Feld](./overview.md#define) in der Benutzeroberfläche definieren, können Sie es als Identitätsfeld festlegen, indem Sie in der rechten Leiste das Kontrollkästchen **[!UICONTROL Identität]** aktivieren.

![](../../images/ui/fields/special/identity.png)

Nach Auswahl des Kontrollkästchens werden weitere Steuerelemente angezeigt. Wenn dieses Feld die primäre Identität des Schemas sein soll, aktivieren Sie das Kontrollkästchen **[!UICONTROL Primär identity]**.

>[!NOTE]
>
>Ein einzelnes Schema kann viele Identitätsfelder enthalten, kann aber nur eine primäre Identität haben. Alle Identitätsfelder (primär oder anderweitig) tragen zum Identitätsdiagramm für einen einzelnen Kunden bei, aber beim Zusammenführen von Datenfragmenten verwendet das Echtzeit-Profil nur die primäre Identität als Wahrheitsquelle. Wenn Sie ein Schema zur Verwendung in Profil aktivieren möchten, muss das Schema eine primäre Identität haben.

Wählen Sie unter **[!UICONTROL Identity Namensraum]** im Dropdown-Menü den entsprechenden Namensraum für das Identitätsfeld aus. Von der Adobe bereitgestellte Standard-Namensraum sowie alle von Ihrem Unternehmen definierten benutzerspezifischen Namensraum werden aufgelistet.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]**, um die Änderung auf das Schema anzuwenden.

![](../../images/ui/fields/special/identity-config.png)

Die Arbeitsfläche wird aktualisiert, um die Änderungen widerzuspiegeln, wobei das ausgewählte Feld ein Fingerabdrucksymbol (![](../../images/ui/fields/special/identity-symbol.png)) erhält, um es als Identität zu kennzeichnen. In der linken Leiste wird das Identitätsfeld jetzt unter dem Namen der Klasse oder Schema-Feldgruppe aufgeführt, die das Feld für das Schema bereitstellt.

Da alle Identitätsfelder standardmäßig erforderlich sind, wird das Feld jetzt in der linken Leiste unter **[!UICONTROL Erforderliche Felder]** aufgelistet. Wenn das Identitätsfeld innerhalb der Schema-Struktur verschachtelt ist, werden alle übergeordneten Felder ebenfalls nach Bedarf aufgelistet.

![](../../images/ui/fields/special/identity-applied.png)

Wenn Sie eine primäre Identität für das Schema definiert haben, können Sie jetzt mit [das Schema für die Verwendung im Echtzeit-Kundenkonto ](../resources/schemas.md#profile) aktivieren.

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie ein Identitätsfeld in der Benutzeroberfläche definiert wird. Da Daten mit diesem Schema erfasst werden, werden die Diagramme zur Kundenidentität aktualisiert, um die Identitätsfelder des Schemas wiederzugeben. Weitere Informationen zum Ermitteln des privaten Diagramms in der Benutzeroberfläche finden Sie im Handbuch [Identitätsdiagramm-Viewer](../../../identity-service/ui/identity-graph-viewer.md).

Informationen zum Definieren anderer XDM-Feldtypen im [!DNL Schema Editor] finden Sie in der Übersicht unter [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special).
