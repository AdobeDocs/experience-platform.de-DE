---
title: Migrieren von JWT zu OAuth-Server-zu-Server-Anmeldeinformationen
description: Erfahren Sie, wie Sie nicht ablaufende JWT-Anmeldeinformationen zu OAuth-Server-zu-Server-Anmeldeinformationen in Adobe Experience Platform migrieren, um einen sicheren, unterbrechungsfreien Zugriff auf den Abfrage-Service zu gewährleisten, bevor die Unterstützung für JWT am 30. Juni 2025 endet. Dieses Handbuch enthält Schritt-für-Schritt-Anweisungen, erläutert das Verhalten nach der Migration und beantwortet häufige Fragen.
source-git-commit: 264d3b12d8fd3bd100018513af1576b3de1cbb33
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---

# Migration von JWT zu OAuth Server-zu-Server-Anmeldeinformationen

>[!IMPORTANT]
>
>Adobe stellt die Unterstützung für JWT-Anmeldedaten (Service Account), die vom Abfrage-Service verwendet werden, ein. Nach dem 30. Juni 2025 werden nicht ablaufende Anmeldeinformationen, die auf JWT basieren, API-Anfragen nicht mehr aktualisieren oder authentifizieren. Um Service-Unterbrechungen zu verhindern, müssen Sie alle zulässigen Anmeldeinformationen zur OAuth-Server-zu-Server-Authentifizierung migrieren.

In diesem Handbuch erfahren Sie, wie Sie nicht ablaufende JWT-Anmeldeinformationen zu OAuth-Server-zu-Server-Anmeldeinformationen in Adobe Experience Platform migrieren. Durch Abschluss dieses Vorgangs wird der unterbrechungsfreie Zugriff auf den Abfrage-Service sichergestellt, bevor die Unterstützung für JWT-Anmeldeinformationen am 30. Juni 2025 endet.

Dieses Dokument enthält Schritt-für-Schritt-Anweisungen zum Durchführen der Migration, zum Verstehen der Auswirkungen und zum Überprüfen Ihrer aktualisierten Anmeldeinformationen.

## Wer migriert werden muss {#who-needs-to-migrate}

Wenn Sie nicht ablaufende Anmeldeinformationen in Query Service verwenden, müssen Sie jede migrieren. Dies gilt für Anmeldeinformationen, die in automatisierten Workflows, geplanten Abfragen oder benutzerdefinierten API-Integrationen verwendet werden.

Wenn Anmeldeinformationen im Abschnitt **[!UICONTROL Nicht ablaufende Anmeldeinformationen]** auf der Registerkarte **[!UICONTROL Anmeldeinformationen]** angezeigt werden, sind diese Anmeldeinformationen betroffen.

## Migrieren von Anmeldeinformationen {#how-to-migrate}

Sie können Berechtigungen direkt in der Experience Platform-Benutzeroberfläche migrieren. Navigieren Sie dazu im linken Navigationsbereich zu **[!UICONTROL Abfragen]** und wählen Sie dann die Registerkarte **[!UICONTROL Anmeldeinformationen]** aus. Identifizieren **[!UICONTROL im Abschnitt „Nicht ablaufende]**&quot; eine als für die Migration geeignet markierte Berechtigung und wählen Sie **[!UICONTROL Migrieren]** aus.

>[!NOTE]
>
>Die Migration dauert 8 bis 10 Sekunden und kann nach dem Start nicht mehr abgebrochen werden.

![Der Arbeitsbereich „Anmeldeinformationen für den Abfrage-Service“ mit hervorgehobenen Optionen „Abfragen“, „Anmeldeinformationen“ und „Migrieren“.](../images/ui/migrate-jwt-to-oauth/migrate.png)

Nach der Migration aktualisiert das System die Berechtigung für die Verwendung der OAuth-Server-zu-Server-Authentifizierung. Die JWT-basierte Methode wird automatisch eingestellt, und der Status wird auf **[!UICONTROL Migriert]** aktualisiert.

Es ist keine Neukonfiguration erforderlich. Bestehende Jobs und Integrationen funktionieren unterbrechungsfrei weiter.

## Was passiert nach der Migration {#after-migration}

Nach Abschluss der Migration:

- Ihre Anmeldedaten funktionieren weiterhin nahtlos, sodass keine Änderungen an Ihren Aufträgen oder Integrationen erforderlich sind.
- Der Abfrage-Service verwendet automatisch die OAuth-Server-zu-Server-Authentifizierung.
- Die JWT-basierte Authentifizierungsmethode wurde eingestellt und wird nicht mehr verwendet.

>[!IMPORTANT]
>
>Sie können diese Änderung nicht rückgängig machen. Nach der Migration können die Anmeldeinformationen nicht mehr auf JWT zurückgesetzt werden.

## Häufig gestellte Fragen {#faq}

Diese Fragen decken gängige Probleme ab und helfen Ihnen, eine reibungslose, unterbrechungsfreie Migration sicherzustellen.

### Warum verwirft Adobe JWT-Anmeldeinformationen?

OAuth Server-zu-Server ist eine sicherere und standardisierte Authentifizierungsmethode. Es bietet ein besseres Lebenszyklus-Management und unterstützt eine breitere Plattformkonsistenz.

### Was passiert, wenn ich nicht bis zum 30. Juni 2025 migriere?

JWT-Anmeldeinformationen werden nicht mehr aktualisiert und Integrationen, die auf sie angewiesen sind, schlagen fehl. Adobe kann Anmeldeinformationen in Ihrem Namen nur migrieren, wenn Sie den Prozess initiieren.

### Woher weiß ich, ob ich migrieren muss?

Wenn eine Berechtigung unter dem Abschnitt **[!UICONTROL Nicht ablaufende Berechtigungen]** auf der Registerkarte Anmeldeinformationen angezeigt wird, müssen diese Anmeldeinformationen migriert werden.

### Muss ich meine Integrationen aktualisieren oder etwas neu konfigurieren?

Nein. Nach der Migration werden die OAuth-Anmeldeinformationen automatisch übernommen. Für Aufträge und Integrationen sind keine manuellen Änderungen erforderlich.

### Kann ich alle Anmeldedaten gleichzeitig migrieren?

Nein. Sie müssen die einzelnen Anmeldeinformationen mithilfe der Schaltfläche **[!UICONTROL Migrieren]** einzeln migrieren.

### Kann ich weiterhin ablaufende Anmeldeinformationen verwenden?

Ja. Ablaufende Anmeldeinformationen sind von dieser Änderung nicht betroffen. Nur nicht ablaufende JWT-Anmeldeinformationen müssen migriert werden.

### Ich sehe eine Meldung, die lautet[!UICONTROL &#x200B; „Keine unbefristeten Anmeldedaten gefunden.]&quot; Was bedeutet das? Muss ich etwas unternehmen?

Diese Nachricht bedeutet, dass Sie noch keine nicht ablaufenden Zugangsdaten erstellt haben, sodass Sie nichts tun müssen.

### Ich sehe eine Meldung, die besagt: &quot;[!UICONTROL AEP-Admin-Verifizierung fehlgeschlagen]…“ Was bedeutet das? Muss ich etwas unternehmen?

Diese Meldung weist darauf hin, dass Sie entweder kein Administrator sind oder nicht über die erforderlichen Berechtigungen zum Erstellen unbefristeter Anmeldeinformationen verfügen.

- Wenn sich Ihre Berechtigungen in letzter Zeit nicht geändert haben, bedeutet dies, dass Sie nie Zugriff zum Erstellen von Anmeldeinformationen hatten, sodass keine Aktion erforderlich ist.
- Wenn Ihre Berechtigungen kürzlich geändert wurden, wenden Sie sich an den Administrator Ihres Unternehmens und bitten Sie ihn, die Anmeldeinformationen für Sie zu migrieren.

### Kann ich unbefristete Anmeldedaten für eine andere Person migrieren?

Ja, aber nur, wenn Sie Administrator sind. Nur Administratoren verfügen über die Berechtigungen, die zum Erstellen und Migrieren nicht ablaufender Anmeldeinformationen für andere Benutzer erforderlich sind, damit sie ohne Unterbrechung weiterarbeiten können.

## Nächste Schritte {#next-steps}

Überprüfen Sie alle nicht ablaufenden Anmeldeinformationen auf der Registerkarte [!UICONTROL Anmeldeinformationen] und migrieren Sie sie einzeln vor dem 30. Juni 2025. Bei Fragen oder Support wenden Sie sich an Ihren Adobe-Kundenbetreuer.
