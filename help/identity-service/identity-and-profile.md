---
title: Identity Service und Echtzeit-Kundenprofil
description: Informationen zur Beziehung zwischen Identity Service und Echtzeit-Kundenprofil
exl-id: 09961b8e-f736-4fcc-ac53-88b55cca7d55
source-git-commit: 2b6700b2c19b591cf4e60006e64ebd63b87bdb2a
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# Verstehen der Beziehung zwischen Identity Service und Echtzeit-Kundenprofil

>[!IMPORTANT]
>
>Auf dieser Seite wird davon ausgegangen, dass die Zusammenführungsrichtlinie das Identitätsdiagramm verwendet. Weitere Informationen zu Zusammenführungsrichtlinien im Echtzeit-Kundenprofil finden Sie in der Dokumentation unter [Zusammenführungsrichtlinien und Identitätszusammenfügung](../profile/merge-policies/overview.md#identity-stitching).

Sie können Identity Service und Echtzeit-Kundenprofil zwar gemeinsam verwenden, aber die beiden Funktionen von Adobe Experience Platform sind von Natur aus nicht identisch.

* Sie können Identity Service verwenden, um das Identitätsdiagramm zu generieren und zu verwalten, das die unterschiedlichen Identitäten eines einzelnen Kunden zusammenführt.
* Sie können Echtzeit-Kundenprofil verwenden, um verschiedene Profilfragmente zusammenzuführen und ein zusammengeführtes Profil zu erstellen. Dieser Prozess erfordert die Verwendung des Identitätsdiagramms.

In diesem Dokument werden die Ähnlichkeiten, Unterschiede und die Beziehung zwischen Identity Service und Echtzeit-Kundenprofil beschrieben.

## Identity Service und Echtzeit-Kundenprofil

Die wichtigsten Unterschiede zwischen Identity Service und Echtzeit-Kundenprofil sind:

| | Identity Service | Echtzeit-Kundenprofil |
| --- | --- |--- |
| **Zweck** | <ul><li>Mit Identity Service können Sie Identitätsdiagramme erstellen und verwalten.</li></ul> | Sie können das Echtzeit-Kundenprofil verwenden, um: <ul><li>Erstellen Sie eine 360-Grad-Ansicht eines Kundenprofils.</li><li>Anzeigen und Verwalten von Profilen</li></ul> |
| **Eingabe** | <ul><li>Um Identity Service zu verwenden, müssen Sie Datensatzdaten oder Zeitreihenereignisse mit mindestens zwei Feldern erfassen, die als Identität markiert sind. Die Felder, die Sie als Identität markieren, werden dann in Identity Service erfasst.</li></ul> | <ul><li>Profilfragmente: stellen eine eindeutige primäre Identität und die entsprechenden Datensatz- oder Ereignisdaten für diese ID in einem bestimmten Datensatz dar.</li><li>Identitätsdiagramme: Das Profil verweist auf das Identitätsdiagramm für ein bestimmtes Kundenprofil, um alle Profilfragmente mit denselben primären Identitäten zu identifizieren.</li></ul> |
| **Prozess** | <ul><li>Nachdem Sie mindestens zwei Identitäten erfasst haben, verknüpft Identity Service diese Identitäten miteinander.</li></ul> | <ul><li>Das Echtzeit-Kundenprofil führt Profilfragmente zusammen, während auf die entsprechenden Identitätsdiagramme verwiesen wird.</li></ul> |
| **Ausgabe** | <ul><li>Das Ergebnis ist ein Identitätsdiagramm, bei dem es sich um einen Satz von Identitäten handelt, die mit einer Person verbunden sind.</li></ul> | <ul><li>Das Ergebnis ist ein zusammengeführtes Profil, das eine einzige und umfassende Ansicht eines bestimmten Kunden darstellt. Dieses Profil kann sich dann für ein Segment qualifizieren.</li></ul> |

{style="table-layout:auto"}

## Zusammengeführter Profilerstellungsprozess

Lesen Sie die folgenden Schritte, um ein besseres Verständnis des Prozesses zum Erstellen eines zusammengeführten Profils zu erhalten:

* Zunächst verweist das Echtzeit-Kundenprofil auf ein Identitätsdiagramm und ruft alle Identitäten ab.
* Als Nächstes ruft Profil Profilfragmente mit primären Identitäten im Identitätsdiagramm ab.
* Nach dem Erfolg führt Profil als alle vorhandenen Ereignisse und Attribute zusammen.
   * Wenn es in Konflikt stehende Attributinformationen gibt, werden Attribute anhand der Zusammenführungsmethode ausgewählt. Weitere Informationen finden Sie im Abschnitt [Übersicht über Zusammenführungsrichtlinien](../profile/merge-policies/overview.md).

![Ein Flussdiagramm, in dem beschrieben wird, wie Identity Service und Profile Merging funktionieren.](./images/merge-profile-process.png)

## Feld als Identität bestimmen

Im Experience-Datenmodell (XDM) ist es eine Anweisung für Experience Platform, dieses Feld beim Identity Service zu erfassen, um ein Feld als Identität zu kennzeichnen oder zu kennzeichnen. Diese Bezeichnung ermöglicht dann die Zusammenführung von Profilfragmenten im Echtzeit-Kundenprofil. Wenn der Identität keine Profilfragmente zugeordnet sind, weisen Sie sie nicht als Identität zu.

### Grundlegendes zu primären und sekundären Identitäten

Sobald Sie Felder als Identitäten markieren, können sie entweder als primäre oder sekundäre Identitäten definiert werden. Primäre und sekundäre Identitäten sind Konzepte, die Teil des Echtzeit-Kundenprofils sind.

* Die primäre Identität (manchmal auch als &quot;Primärschlüssel&quot;bezeichnet) ist die Identität, in der Profilfragmente gespeichert werden.
* Wenn eine Datenzeile nur eine Identität enthält, wird diese einzelne Identität als primär bezeichnet.
* Wenn es zwei oder mehr Identitäten gibt, wird eine als primär bezeichnet und die verbleibenden als sekundär gekennzeichnet.

Identity Service erstellt Verknüpfungen zwischen Identitäten, sofern mindestens zwei Felder als Identität markiert sind. Identity Service speichert keine Informationen darüber, ob eine Identität primär oder sekundär ist.

