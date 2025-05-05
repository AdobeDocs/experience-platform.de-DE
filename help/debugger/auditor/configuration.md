---
title: Referenz für Konfigurationstest
description: Erfahren Sie, wie die Auditor-Funktion Konfigurationen in Adobe Experience Platform Debugger testet.
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 50%

---

# Referenz für Konfigurationstest

Diese Referenz enthält weitere Informationen darüber, wie die Auditor-Funktion in Adobe Experience Platform Debugger Konfigurationstests ausführt.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Experience Platform Debugger finden Sie unter [Auditor-Funktion - Übersicht](./overview.md).

Bei Konfigurationstests wird nach bestimmten Einstellungen, Werten oder möglichen Konflikten in Ihrer Implementierung gesucht. Experience Platform Auditor vergleicht die Tags mit anderen Regeln und empfohlenen Best Practices.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Advertising Cloud - Konversionsnamen verwenden nur alphanumerische Zeichen | 3 | Der `ev_conversion_property_name`-Parameter sollte nur numerische und Dezimalwerte enthalten. Eine Ausnahme bildet der `ev_transid`-Parameter, der Text oder numerische Werte enthalten kann. Suchen Sie nach `everesttech.net` Pixeln, die einen URL-Parameter enthalten, der mit `ev_` beginnt. | Stellen Sie sicher, dass die Parameter der Transaktionseigenschaft nur numerische und Dezimalwerte enthalten.<br><br>Warnung: Alle anderen Werttypen können zu Datenverlust führen. |
| Advertising Cloud - Konversionsnamen verwenden URL-sichere Zeichen | 3 | Konversionseigenschaftsnamen dürfen kein Und- und kein Fragezeichen enthalten. | Stellen Sie sicher, dass Transaktionseigenschaftsparameter kein nicht-kodiertes Und- und kein Fragezeichen enthalten. Diese Zeichen beeinträchtigen das URL-Format.<br><br>Warnung: Eigenschaftsparameter, die ein nicht kodiertes kaufmännisches Und-Zeichen oder Fragezeichen enthalten (z. B.: `ev_formComplete?=1` oder `ev_formComplete&Submit=1`), können zu Datenverlust führen. |
| Advertising Cloud - Transaktions-ID korrekt implementiert | 1 | Der Eigenschaftsname `ev_transid=` darf nicht leer sein. | Der Eigenschaftsname `ev_transid=` darf nicht ohne Wert bleiben. Andernfalls kann es zu Transaktionsdatenverlust kommen. Weisen Sie dem `ev_transid=` einen Wert zu oder entfernen Sie den Parameter aus dem Pixel. |
| Analytics - in DOM instanziiert | 5 | Der Adobe Analytics-Code ist entweder nicht installiert oder kann nicht ausgeführt werden. Gibt 0 zurück, wenn kein Analytics-Code auf der Web-Seite gefunden wird. | Vergewissern Sie sich, dass das Analytics-Tag auf der Seite implementiert ist und nicht durch nachfolgende Skriptaktivitäten blockiert wird.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de) |
| Analytics - Einmal instanziiert | 5 | Der Adobe Analytics-Code wurde mehrmals auf der Seite erkannt. Gibt 0 zurück, wenn kein A-Analytics-Code auf der Web-Seite gefunden wird. | Stellen Sie sicher, dass nur ein Analytics-Tag auf der Seite vorhanden ist.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de) |
| Analytics - neueste Version | 3 | Auf Ihren Seiten wird nicht die neueste Version der Analytics-Codebibliothek ausgeführt. Code-Bibliotheken, die Experience Cloud-Technologien nutzen, werden ständig aktualisiert und optimiert, um Performance-Verbesserungen und neueste Funktionen bereitzustellen. Gibt 0 zurück, wenn kein Analytics-Code auf der Web-Seite gefunden wird. | Installieren Sie die aktuelle Version der Analytics-Bibliothek.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=de) |
| Launch - Drittanbieter-Tags werden asynchron geladen, wenn DOM bereit ist | 3 | Um ein Gleichgewicht zwischen einem guten Benutzererlebnis und der Erfassung präziser Daten zu erzielen, sollten Drittanbieter-Tags bei DOM-Bereitschaft ausgelöst werden. Dadurch wird sichergestellt, dass diese Tracking-Skripte ausgeführt werden, ohne dass dadurch die Funktionalität der Site beeinträchtigt wird. | Beheben Sie dieses Problem, indem Sie alle Regeln anpassen, die Pixel von Drittanbietern ausführen, sodass sie bei DOM-fähig ausgelöst werden.<br><br>[Weitere Informationen](../../tags/ui/managing-resources/rules.md) |
| Experience Cloud ID-Service - neueste Version | 2 | Auf Ihren Seiten wird nicht die neueste Version der Visitor ID Service-Code-Bibliothek, visitorAPI.js, ausgeführt. Code-Bibliotheken, die Experience Cloud-Technologien nutzen, werden ständig aktualisiert und optimiert, um Performance-Verbesserungen und neueste Funktionen bereitzustellen. | Installieren Sie die neueste Version der Besucher-ID-Service-Bibliothek.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html?lang=de) |
| Launch - neueste Version | 2 | Auf diesen Seiten wird nicht die neueste Version der Tag-Code-Bibliothek (Turbine) ausgeführt. Code-Bibliotheken, die Experience Cloud-Technologien nutzen, werden ständig aktualisiert und optimiert, um Performance-Verbesserungen und neueste Funktionen bereitzustellen. | Erstellen und veröffentlichen Sie die Tag-Bibliothek neu.<br><br>[Weitere Informationen](../../tags/quick-start/quick-start.md) |
| Target - neueste Version | 2 | Auf Ihren Seiten wird nicht die neueste Version der Target-Codebibliothek ausgeführt. Code-Bibliotheken, die Experience Cloud-Technologien nutzen, werden ständig aktualisiert und optimiert, um Performance-Verbesserungen und neueste Funktionen bereitzustellen. | Installieren Sie die aktuelle Version der Target-Bibliothek.<br><br>[Weitere Informationen](https://developer.adobe.com/target/implement/client-side/) |
| Ziel - mboxDefault geht mboxCreate voran | 5 | Die ordnungsgemäße Verwendung von mboxCreate sieht in etwa wie folgt aus:<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | Denken Sie daran, ein `<div class="mboxDefault"></div>`-Tag einzufügen, bevor Sie mboxCreate() aufrufen. „at.js“ fügt keins für Sie hinzu.<br><br>[Weitere Informationen](https://developer.adobe.com/target/implement/client-side/) |
| Target - Valid DOCTYPE | 5 | Ein ungültiger DOCTYPE wurde erkannt. In diesem Szenario werden keine Mboxes ausgelöst.  Bei „at.js“ muss sich der DOCTYPE im Standardmodus befinden, sonst funktioniert Target nicht. | Aktualisieren Sie den DOCTYPE auf der Seite.<br><br>[Weitere Informationen](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style="table-layout:auto"}
