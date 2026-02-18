---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Schema;Datensatz;Planung;Aktivierung
solution: Experience Platform
title: Planen der Aktivierung von Echtzeit-Kundenprofilen
description: Beachten Sie die wichtigsten Überlegungen, die Sie vor der Aktivierung von Schemas und Datensätzen für das Echtzeit-Kundenprofil berücksichtigen müssen.
source-git-commit: da40dfde57b17b6a7387451eec48569174ad544b
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Planen der Aktivierung von Echtzeit-Kundenprofilen

Verwenden Sie diese Seite, um zu bestätigen, dass Ihr Schema und Datensatz bereit sind, bevor Sie sie für das Echtzeit-Kundenprofil aktivieren. Schließen Sie diese Planungsprüfung ab, nachdem Sie Ihre Schemafelder entworfen haben, aber bevor Sie das Schema für das Profil aktivieren. Durch die Profilaktivierung werden dauerhafte Verhaltensänderungen auf Ihr Datenmodell angewendet. Die Schemaaktivierung kann nicht rückgängig gemacht werden. Die Aktivierung eines Datensatzes wirkt sich darauf aus, wie seine Datensätze im Echtzeit-Kundenprofil verarbeitet werden. Lesen Sie diese Anleitung, um unbeabsichtigte Aktivierungen, Datenqualitätsprobleme oder langfristige Einschränkungen in Ihrem Schemadesign zu vermeiden.

Durch die Aktivierung des Profils wird bestimmt, wie Ihre Daten in Experience Platform zugeordnet, zusammengeführt und aktiviert werden. Die Planung stellt sicher, dass Ihre Schemastruktur, Identitätskonfiguration und Ihr Datensatzzweck korrekt sind, bevor Sie die Änderung vornehmen. Nachdem Sie diese Planungsprüfung abgeschlossen haben, können Sie in der **[!UICONTROL Schema Editor]** oder **[!UICONTROL Dataset]** Benutzeroberfläche mit dem Aktivieren von Daten für das Profil fortfahren.

## Voraussetzungen

Bevor Sie dieses Planungshandbuch verwenden, stellen Sie sicher, dass Sie Folgendes haben:

* Ein Schema mit der **[!UICONTROL Schema Editor]**- oder Schema Registry-API entworfen. Erste Schritte finden [ im Tutorial ](../tutorials/create-schema-ui.md)Schemaerstellung“.
* Mindestens ein Identitätsfeld in Ihrem Schema konfiguriert. Anweisungen finden [ im Konfigurationshandbuch für Identitätsfelder ](../ui/fields/identity.md).
* Grundlegendes zu [Echtzeit-Kundenprofil](../../profile/home.md) und dessen Verwendung von Schemata zum Erstellen einheitlicher Kundenansichten.
* Entsprechende Berechtigungen zum Aktivieren von Schemata und Datensätzen für das Profil. Wenden Sie sich an Ihren Systemadministrator, wenn Sie keinen Zugriff auf die Optionen zur Profilaktivierung haben.

Wenn Sie diese Voraussetzungen nicht erfüllt haben, beginnen Sie mit dem [Tutorial zur Schemaerstellung](../tutorials/create-schema-ui.md) bevor Sie mit dieser Planung fortfahren.

## Warum Planung wichtig ist {#why-planning-matters}

Die Profilaktivierung verändert dauerhaft die Art und Weise, wie Experience Platform Ihre Daten verarbeitet. Die folgenden dauerhaften Änderungen gelten für Schemata und Datensätze.

**Schemata**: Wenn Sie ein Schema für ein Profil aktivieren, können Sie es nicht deaktivieren oder löschen. Sie können auch keine Felder aus dem Schema entfernen oder umbenennen, nachdem Daten aufgenommen wurden. Dies bedeutet, dass Ihr Schema-Design vollständig und stabil sein muss, bevor Sie das Profil aktivieren, da Sie die Entscheidung später nicht rückgängig machen oder die Struktur nicht vereinfachen können.

**Datensätze**: Wenn Sie einen Datensatz für das Profil aktivieren, verwendet das Echtzeit-Kundenprofil seine Datensätze, um Profile zu erstellen und zu aktualisieren. Überprüfen Sie das Verhalten zur Aktivierung von Datensätzen im [Benutzerhandbuch für Datensätze](../../catalog/datasets/enable-for-profile.md). Im Gegensatz zu Schemata können Sie den Datensatz später deaktivieren oder löschen. Dadurch werden jedoch die zugehörigen Profildatensätze entfernt und die Segmentierungs- oder Aktivierungs-Workflows können beeinträchtigt werden. Berücksichtigen Sie die nachgelagerten Auswirkungen, bevor Sie Änderungen an einem aktivierten Datensatz vornehmen.

Da sich diese Änderungen auf nachgelagerte Prozesse auswirken, müssen Sie sicherstellen, dass ein Schema und seine Datensätze für das Profil geeignet sind, bevor Sie sie aktivieren.

### Grundlegendes zum Aktivierungs-Workflow

Sie müssen sowohl das Schema als auch die Datensätze aktivieren, die dieses Schema für das Profil verwenden. Aktivieren Sie Ressourcen in der folgenden Reihenfolge:

1. **Aktivieren des Schemas für Profil**: Aktivieren Sie zunächst das Profil für das Schema im **[!UICONTROL Schema Editor]**. Dadurch kann jeder Datensatz, der dieses Schema verwendet, für das Profil aktiviert werden.
2. **Aktivieren individueller Datensätze für das Profil**: Nachdem das Schema aktiviert wurde, aktivieren Sie das Profil für jeden Datensatz, der zu einheitlichen Kundenprofilen beitragen soll.

Sie können einen Datensatz für Profil nicht aktivieren, wenn sein Schema noch nicht aktiviert ist. Das Schema dient als Voraussetzung für die Datensatzaktivierung. Dieser zweistufige Prozess stellt sicher, dass Ihr Datenmodell validiert wird, bevor das Echtzeit-Kundenprofil mit der Verarbeitung von Datensätzen beginnt.

## Wann ein Schema oder ein Datensatz für das Profil aktiviert werden soll {#when-to-enable}

Überprüfen Sie die folgenden Kriterien, um zu bestätigen, dass die Profilaktivierung für Ihre Daten geeignet ist.

Aktivieren Sie Profil in den folgenden Situationen:

* Die Daten tragen zu einem einheitlichen Kundenprofil bei.
* Die Daten sind für Segmentierungs- oder Aktivierungs-Workflows erforderlich.
* Das Schema enthält Identitätsfelder, die einen Schlüssel auf Personen- oder Kundenebene darstellen.
* Der Datensatz enthält Erlebnisereignisse oder Profilattribute, die kanalübergreifend zugeordnet werden müssen. Überprüfen Sie die [XDM ExperienceEvent-Klasse](../classes/experienceevent.md), um die Ereignisanforderungen zu bestätigen.

## Wann kein Schema oder Datensatz für das Profil aktiviert werden soll {#when-not-to-enable}

Vermeiden Sie in den folgenden Fällen die Aktivierung des Profils:

* Das Schema stellt Such- oder Referenzdaten dar.
* Der Datensatz enthält Test-, temporäre oder Nicht-Produktionsdaten.
* Die Daten identifizieren keine Person oder werden nur für Berichte verwendet.
* Das Schema ist experimentell oder strukturell unvollständig.

Die Aktivierung von Profilen in diesen Szenarien kann zu unnötigen Profilen führen, die Lizenznutzung erhöhen oder langfristige Schemaeinschränkungen mit sich bringen.

## Wichtige Aspekte vor der Aktivierung des Profils {#key-considerations}

Überprüfen Sie die Überlegungen in diesem Abschnitt, um sicherzustellen, dass Ihr Schema und Ihr Datensatz Anwendungsfälle für Profile und langfristige Data Governance unterstützen. Bevor Sie das Profil aktivieren, überprüfen Sie Ihre Schemastruktur, Identitätskonfiguration und den Zweck des Datensatzes.

### Bereitschaft des Schemas

Überprüfen Sie die Schemastruktur, um sicherzustellen, dass sie Profilanforderungen unterstützt. Das Schema muss die Felder enthalten, die für die Segmentierung und Aktivierung erforderlich sind, während es experimentelle oder langfristig nicht benötigte Felder ausschließt. Beachten Sie, dass alle zusätzlichen Felder, die Sie nach der Aktivierung hinzufügen, additiv sein müssen (Einzelheiten finden Sie unter [Beschränkungen für die ](#why-planning-matters)). Diese Einschränkung bedeutet, dass Sie Ihre Feldauswahl sorgfältig überprüfen sollten, bevor Sie das Profil aktivieren. Einzelheiten zu zulässigen Aktualisierungen finden Sie unter [Schemaentwicklungsregeln](./composition.md#evolution).

### Identitätskonfiguration

Die Identitätskonfiguration bestimmt, wie das Profil Datensätze über Datensätze hinweg zusammenfügt. Beginnen Sie mit der Bestätigung, dass eine gültige primäre Identität ausgewählt ist. Dieses Feld muss stabil, eindeutig und in allen Datensätzen konsistent ausgefüllt sein. Stellen Sie sicher, dass Identity-Namespaces korrekt zugewiesen sind, um Zuordnungsfehler zu vermeiden. Wenn Sie sekundäre Identitäten verwenden, bestätigen Sie, dass diese Ihre Anwendungsfälle unterstützen, ohne Profilkollisionen zu verursachen, die auftreten können, wenn verschiedene Personen denselben Identitätswert teilen. Das Echtzeit-Kundenprofil löst Konflikte durch Anwendung von Zusammenführungsrichtlinien auf, die bestimmen, welche Daten Vorrang haben, wenn Datensätze, die miteinander in Konflikt stehen, zugeordnet werden.

### Zweck des Datensatzes

Aktivieren Sie einen Datensatz nur dann für ein Profil, wenn er direkt zu Profilattributen oder Erlebnisereignissen beiträgt, die in nachgelagerten Workflows verwendet werden. Vermeiden Sie die Aktivierung von Datensätzen, die Lookup- oder Referenzdaten enthalten, die nicht in der Segmentierung, in Test- oder Beispieldaten oder in vom Betriebssystem generierten Datensätzen verwendet werden, die nicht für die Aktivierung vorgesehen sind. Diese Datentypen tragen nicht zu einheitlichen Kundenprofilen bei und verursachen einen unnötigen Speicher-Overhead. Wenn ein Datensatz keine Identitätsfelder oder Kundenverhaltensdaten enthält, die Segmentierung und Aktivierung unterstützen, aktivieren Sie ihn nicht für das Profil.

**Beispiel**:

Sie aktivieren einen Datensatz mit „Kundenkaufereignissen“, der Transaktionsdaten mit Kunden-IDs enthält. Das Echtzeit-Kundenprofil verwendet diese Ereignisse, um Kundenzeitpläne zu erstellen und die Segmentierung basierend auf dem Kaufverhalten zu aktivieren.

Sie aktivieren KEINEN „Produktkatalog“-Datensatz, der nur SKU-Referenzdaten ohne Kundenkennungen enthält. Die Aktivierung dieses Datensatztyps erzeugt einen unnötigen Speicher-Overhead, ohne zu einheitlichen Kundenprofilen beizutragen.

## Checkliste vor der Aktivierung {#pre-enablement-checklist}

Verwenden Sie diese Checkliste, um die Bereitschaft zu bestätigen, bevor Sie ein Schema oder einen Datensatz für das Profil aktivieren. Schließen Sie jedes Element ab, bevor Sie das Profil aktivieren.

### Prüfungen auf Schemaebene

Überprüfen Sie zunächst, ob Ihr Schema-Design vollständig und stabil ist. Überprüfen Sie Ihr Schema, um sicherzustellen, dass alle erforderlichen Felder für Ihren Anwendungsfall vorhanden sind und keine experimentellen oder temporären Felder enthalten sind. Konsultieren Sie die [Best Practices für den Schemaentwurf](./best-practices.md), um sicherzustellen, dass Ihr Schema empfohlenen Mustern entspricht. Einholen der Genehmigung von Ihrem Team für die endgültige Feldliste (siehe [Unveränderlichkeitsbeschränkungen für Schemata](#why-planning-matters))

Überprüfen Sie anschließend, ob Ihre primäre Identitätskonfiguration korrekt ist. Öffnen Sie Ihr Schema im **[!UICONTROL Schema Editor]** und suchen Sie das Feld mit dem Identitätssymbol. Vergewissern Sie sich, dass dieses Feld in Ihren Quelldaten konsistent ausgefüllt ist und dass der Identity-Namespace für Ihren Anwendungsfall geeignet ist. Die primäre Identität muss stabil, eindeutig und zuverlässig in allen Datensätzen vorhanden sein, um eine ordnungsgemäße Profilzuordnung sicherzustellen.

Bestätigen Sie abschließend, dass Sie die Schemastruktur nicht umbenennen oder neu organisieren müssen. Änderungen an der Schemastruktur sind auf additive Aktualisierungen beschränkt (siehe [Beschränkungen für die Unveränderlichkeit von Schemata](#why-planning-matters)). Jegliche langfristige Mehrdeutigkeit bei der Benennung oder Organisation kann zu einem späteren Zeitpunkt nicht korrigiert werden. Beheben Sie diese Probleme daher vor der Aktivierung.

### Prüfungen auf Datensatzebene

Bestätigen Sie zunächst für jeden Datensatz, den Sie aktivieren möchten, dass er profilrelevante Daten enthält. Überprüfen Sie die Beispieldatensätze, um sicherzustellen, dass sie Kunden- oder Ereignisdaten und keine rein operativen oder Referenzinformationen enthalten. Stellen Sie sicher, dass Datensätze Identitätswerte enthalten, die mit Kundenprofilen verknüpft sind. Datensätze ohne Identitätsfelder oder Kundenverhaltensdaten sollten nicht für das Profil aktiviert werden.

Sie können bestimmen, ob der Datensatz zur Identitätszuordnung oder Segmentierung beitragen soll, indem Sie verstehen, wie sich seine Identitätswerte auf andere Datensätze in Ihrer profilaktivierten Umgebung beziehen. Erwägen, ob die Datensätze in diesem Datensatz mit vorhandenen Profilen übereinstimmen sollten, oder neue Profilfragmente erstellen. Lesen Sie die [Dokumentation zu Zusammenführungsrichtlinien](../../profile/merge-policies/overview.md) um zu verstehen, wie das Echtzeit-Kundenprofil Datensätze über Datensätze hinweg zusammenfügt und wie dieser Datensatz in Ihre allgemeine Identitätsstrategie passt.

Schätzen Sie vor der Aktivierung des Datensatzes die Anzahl der darin enthaltenen eindeutigen Identitätswerte und stellen Sie sicher, dass diese Identitätswerte tatsächliche Kunden darstellen und keine Testkonten oder Systemkennungen. Vergewissern Sie sich, dass die Aktivierung dieses Datensatzes mit Ihren Lizenzberechtigungen übereinstimmt, da jede eindeutige Identität zu Ihrem adressierbaren Zielgruppengröße beiträgt. Die Aktivierung von Profilen erhöht die Speicher- und Verarbeitungskosten, sodass sichergestellt ist, dass der Datensatz einen Wert bietet, der diese Investition rechtfertigt.

Durch Ausfüllen dieser Checkliste können Probleme vermieden werden, die nach der Aktivierung nicht rückgängig gemacht werden können.

## Aktivieren eines Profils für Ihr Schema und Ihren Datensatz {#enable-profile}

Führen Sie nach Abschluss der Checkliste vor der Aktivierung die folgenden Schritte aus, um das Profil zu aktivieren. Wie unter [Grundlegendes zum Aktivierungs-Workflow](#why-planning-matters) erläutert, müssen Sie das Schema aktivieren, bevor Sie Datensätze aktivieren, die dieses Schema verwenden.

### Aktivieren des Schemas für das Profil

Aktivieren Sie zuerst das Profil in Ihrem Schema:

1. Navigieren Sie in der Experience Platform-Benutzeroberfläche zu **[!UICONTROL Schemas]** .
2. Wählen Sie Ihr Schema aus der Liste aus, um es im **[!UICONTROL Schema Editor]** zu öffnen.
3. Wählen Sie in der rechten Leiste den Umschalter **[!UICONTROL Profile]** aus. Das Bedienfeld Schemaeigenschaften zeigt ein Bestätigungsdialogfeld an.
4. Wählen Sie zur Bestätigung **[!UICONTROL Enable]** aus. Das Schema ist jetzt für das Profil aktiviert.

Detaillierte Anweisungen finden Sie im [Handbuch zur Schemaaktivierung](../ui/resources/schemas.md#profile) in der Dokumentation zum Schema-Editor.

### Aktivieren von Datensätzen für Profile

Nachdem Ihr Schema für das Profil aktiviert wurde, aktivieren Sie jeden Datensatz, der zu einheitlichen Profilen beitragen soll:

1. Navigieren Sie in der Experience Platform-Benutzeroberfläche zu **[!UICONTROL Datasets]** .
2. Wählen Sie einen Datensatz aus der Liste aus, um die Seite mit den Datensatzdetails zu öffnen.
3. Wählen Sie in der rechten Leiste den Umschalter **[!UICONTROL Profile]** aus. Der Bereich mit den Datensatzeigenschaften wird aktualisiert und zeigt an, dass das Profil aktiviert ist.

Wiederholen Sie diesen Vorgang für jeden Datensatz, der zum Echtzeit-Kundenprofil beitragen soll. Detaillierte Anweisungen und API-Aktivierungsoptionen finden Sie im Benutzerhandbuch für Datensätze, auf das im Abschnitt Voraussetzungen verwiesen wird.

### Warum Ordnung wichtig ist

Wie unter [Grundlegendes zum Aktivierungs-Workflow](#why-planning-matters) erläutert, müssen Sie das Schema vor der Aktivierung von Datensätzen aktivieren. Dadurch wird sichergestellt, dass das Echtzeit-Kundenprofil die Schemastruktur validiert, Profilvorgänge unterstützt, bevor die Datensatzaktivierung zugelassen wird, und dass alle Datensätze, die das Schema verwenden, die richtigen Felddefinitionen für die Segmentierung und Identitätszuordnung erben.

Nachdem Sie sowohl das Schema als auch die Datensätze aktiviert haben, beginnt das Echtzeit-Kundenprofil mit der Verarbeitung von Datensätzen und der Erstellung einheitlicher Kundenprofile. Datensätze, die vor der Aktivierung aufgenommen wurden, werden nicht in die Profile aufgenommen, es sei denn, Sie nehmen die Daten erneut auf.

## Nächste Schritte {#next-steps}

Sie haben die dauerhaften Auswirkungen der Profilaktivierung geprüft, bestätigt, dass Ihr Schema und Ihre Datensätze bereit sind, und validiert, dass Ihre Identitätskonfiguration Ihre Anwendungsfälle unterstützt. Um Ihr Verständnis der Schemastruktur und Feldbeziehungen zu vertiefen, lesen Sie den Abschnitt [Grundlagen der Schemakomposition](../schema/composition.md), in dem Schemaentwicklungsregeln und die Interaktion von Feldern innerhalb des Datenmodells erläutert werden. Wenn während oder nach der Aktivierung Probleme auftreten, finden Sie im [Handbuch zur XDM-Fehlerbehebung](../troubleshooting-guide.md) Informationen zu häufigen Problemen und Lösungen. Weitere Informationen dazu, wie sich Identity-Namespaces auf die Profilzuordnung und -auflösung auswirken, finden Sie unter [Übersicht zu Identity-Namespaces](../../identity-service/features/namespaces.md).
