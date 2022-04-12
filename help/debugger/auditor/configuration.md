---
title: Konfigurationstest-Referenz
description: Erfahren Sie, wie die Auditor-Funktion in Adobe Experience Platform Debugger auf Konfigurationen testet.
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 65%

---

# Referenz zum Konfigurationstest

Diese Referenz enthält weitere Informationen dazu, wie die Auditor-Funktion in Adobe Experience Platform Debugger Konfigurationstests ausführt.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Platform Debugger finden Sie in der [Übersicht über Auditor-Funktionen](./overview.md).

Bei Konfigurationstests wird nach bestimmten Einstellungen, Werten oder möglichen Konflikten in Ihrer Implementierung gesucht. Platform Auditor bewertet die Tags anhand anderer Regeln und empfohlener Best Practices.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Advertising Cloud – Konversionsnamen enthalten nur alphanumerische Zeichen | 3 | Die `ev_conversion_property_name` -Parameter darf nur numerische und Dezimalwerte enthalten, AUSSER für `ev_transid` -Parameter, der Text oder numerische Werte enthalten kann. Suchen Sie nach `everesttech.net` --Pixeln, die einen URL-Parameter enthalten, der mit `ev_`  _ beginnt. | Stellen Sie sicher, dass die Parameter der Transaktionseigenschaft nur numerische und Dezimalwerte enthalten.<br><br>Warnung: Alle anderen Werttypen können Datenverluste verursachen. |
| Advertising Cloud – Konversionsnamen verwenden URL-geeignete Zeichen | 3 | Konversionseigenschaftsnamen dürfen kein Und- und kein Fragezeichen enthalten. | Stellen Sie sicher, dass Transaktionseigenschaftsparameter kein nicht-kodiertes Und- und kein Fragezeichen enthalten. Diese Zeichen beeinträchtigen das URL-Format.<br><br>Warnung: Eigenschaftenparameter, die ein nicht-kodiertes Und- oder Fragezeichen enthalten (z. B.:  `ev_formComplete?=1` oder  `ev_formComplete&Submit=1`), kann zu Datenverlust führen. |
| Advertising Cloud – Transaktions-ID ist korrekt implementiert | 1 | Der Eigenschaftsname  `ev_transid=` darf nicht leer sein. | Der Eigenschaftsname  `ev_transid=` sollte nicht ohne Wert belassen werden. Andernfalls kann es zu Transaktionsdatenverlust kommen. Wert zuweisen zu `ev_transid=` oder entfernen Sie den Parameter aus dem Pixel. |
| Analytics – Ist in DOM instanziiert | 5 | Der Adobe Analytics-Code ist entweder nicht installiert oder kann nicht ausgeführt werden. Gibt 0 zurück, wenn kein Analytics-Code auf der Webseite gefunden wurde. | Vergewissern Sie sich, dass das Analytics-Tag auf der Seite implementiert ist und nicht durch nachfolgende Skriptaktivitäten blockiert wird.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de) |
| Analytics – Ist einmal instanziiert | 5 | Der Adobe Analytics-Code wurde mehrmals auf der Seite erkannt. Gibt 0 zurück, wenn kein A-Analytics-Code auf der Webseite gefunden wurde. | Stellen Sie sicher, dass nur ein Analytics-Tag auf der Seite vorhanden ist.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analytics – Neueste Version | 3 | Auf Ihren Seiten wird nicht die neueste Version der Analytics-Codebibliothek ausgeführt. Code-Bibliotheken, die Experience Cloud-Technologien nutzen, werden ständig aktualisiert und optimiert, um Leistungsverbesserungen und neueste Funktionen bereitzustellen. Gibt 0 zurück, wenn kein Analytics-Code auf der Webseite gefunden wurde. | Installieren Sie die aktuelle Version der Analytics-Bibliothek.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=de) |
| Launch - Drittanbieter-Tags werden nach DOM-Bereitschaft asynchron geladen | 3 | Um ein Gleichgewicht zwischen einer guten Benutzererfahrung und der Erfassung genauer Daten zu erreichen, sollten Drittanbieter-Tags bei DOM-Bereitschaft ausgelöst werden. Dadurch wird sichergestellt, dass diese Tracking-Skripte ausgeführt werden, ohne dass dadurch die Funktionalität der Site beeinträchtigt wird. | Beheben Sie dieses Problem, indem Sie alle Regeln anpassen, die Pixel von Drittanbietern ausführen, damit sie bei DOM bereit ausgelöst werden.<br><br>[Weitere Informationen](../../tags/ui/managing-resources/rules.md) |
| Experience Cloud ID-Service – Neueste Version | 2 | Auf Ihren Seiten wird nicht die neueste Version der Codebibliothek des Besucher-ID-Services  visitorAPI.js ausgeführt. Code-Bibliotheken, die Experience Cloud-Technologien nutzen, werden ständig aktualisiert und optimiert, um Leistungsverbesserungen und neueste Funktionen bereitzustellen. | Installieren Sie die neueste Version der Besucher-ID-Service-Bibliothek.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Launch – Neueste Version | 2 | Auf diesen Seiten wird nicht die neueste Version der Tag-Code-Bibliothek (Turbine) ausgeführt. Code-Bibliotheken, die Experience Cloud-Technologien nutzen, werden ständig aktualisiert und optimiert, um Leistungsverbesserungen und neueste Funktionen bereitzustellen. | Erstellen Sie die Tag-Bibliothek neu und veröffentlichen Sie sie.<br><br>[Weitere Informationen](../../tags/quick-start/quick-start.md) |
| Target – Neueste Version | 2 | Auf Ihren Seiten wird nicht die neueste Version der Target-Codebibliothek ausgeführt. Code-Bibliotheken, die Experience Cloud-Technologien nutzen, werden ständig aktualisiert und optimiert, um Leistungsverbesserungen und neueste Funktionen bereitzustellen. | Installieren Sie die aktuelle Version der Target-Bibliothek.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html) |
| Target – mboxDefault vor mboxCreate | 5 | Die ordnungsgemäße Verwendung von  mboxCreate sieht in etwa so aus:<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | Stellen Sie sicher, dass Sie eine  `<div class="mboxDefault"></div>` -Tag vor dem Aufruf von mboxCreate(). „at.js“ fügt keins für Sie hinzu.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html) |
| Target – Gültiger DOCTYPE | 5 | Ein ungültiger DOCTYPE wurde erkannt. In diesem Szenario werden keine mboxes ausgelöst.  Bei „at.js“ muss sich der DOCTYPE im Standardmodus befinden, sonst funktioniert Target nicht. | Aktualisieren Sie den DOCTYPE auf der Seite.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/faq-at-js/target-atjs-faq.html) |

{style=&quot;table-layout:auto&quot;}
