---
title: Übersicht über die API-Erweiterung für Meta Conversions
description: Erfahren Sie mehr über die Meta Conversions API-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 3cd937f49f27006e3cab60df1692d33138944ce2
workflow-type: tm+mt
source-wordcount: '2583'
ht-degree: 0%

---

# Übersicht über die [!DNL Meta Conversions API]-Erweiterung

Mit dem [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) können Sie Ihre Server-seitigen Marketing-Daten mit [!DNL Meta] -Technologien verbinden, um Ihr Anzeigen-Targeting zu optimieren, die Kosten pro Aktion zu senken und die Ergebnisse zu messen. Ereignisse sind mit einer [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) -ID verknüpft und werden ähnlich wie clientseitige Ereignisse verarbeitet.

Mithilfe der Erweiterung [!DNL Meta Conversions API] können Sie die API-Funktionen in Ihren Regeln zur [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) nutzen, um Daten vom Adobe Experience Platform-Edge Network an [!DNL Meta] zu senden. In diesem Dokument wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in der Ereignisweiterleitung [Regel](../../../ui/managing-resources/rules.md) verwenden.

## Demo

Das folgende Video soll Ihr Verständnis von [!DNL Meta Conversions API] unterstützen.

>[!VIDEO](https://unlockmarketingdata.com/video-meta-conversions-api)

## Voraussetzungen

Es wird dringend empfohlen, [!DNL Meta Pixel] und [!DNL Conversions API] zu verwenden, um dieselben Ereignisse vom Client- bzw. vom Server-seitigen Ereignis freizugeben und zu senden, da dies dazu beitragen kann, Ereignisse wiederherzustellen, die nicht von [!DNL Meta Pixel] erfasst wurden. Anweisungen zur Integration in Ihre clientseitigen Tag-Implementierungen finden Sie im Handbuch zur [[!DNL Meta Pixel] Erweiterung](../../client/meta/overview.md) , bevor Sie die Erweiterung [!DNL Conversions API] installieren.

>[!NOTE]
>
>Der Abschnitt zur [Ereignisdeduplizierung](#deduplication) weiter unten in diesem Dokument behandelt die Schritte, um sicherzustellen, dass dasselbe Ereignis nicht zweimal verwendet wird, da es sowohl vom Browser als auch vom Server empfangen werden kann.

Um die Erweiterung [!DNL Conversions API] verwenden zu können, müssen Sie Zugriff auf die Ereignisweiterleitung haben und über ein gültiges [!DNL Meta]-Konto mit Zugriff auf [!DNL Ad Manager] und [!DNL Event Manager] verfügen. Insbesondere müssen Sie die ID eines vorhandenen [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) kopieren (oder stattdessen [einen neuen  [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) erstellen), damit die Erweiterung für Ihr Konto konfiguriert werden kann.

>[!INFO]
>
>Wenn Sie diese Erweiterung mit Daten aus mobilen Apps verwenden möchten oder wenn Sie auch Offline-Ereignisdaten in Ihren [!DNL Meta]-Kampagnen verwenden, müssen Sie Ihren Datensatz über eine vorhandene App erstellen und bei Aufforderung **Aus einer Pixel-ID erstellen** auswählen. Weitere Informationen finden Sie im Artikel [Festlegen, welche Datensatzerstellungsoption für Ihr Unternehmen geeignet ist](https://www.facebook.com/business/help/5270377362999582?id=490360542427371). Im Dokument [Konversions-API für App-Ereignisse](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) finden Sie alle erforderlichen und optionalen App-Tracking-Parameter.

## Installieren der Erweiterung

Um die Erweiterung [!DNL Meta Conversions API] zu installieren, navigieren Sie zur Benutzeroberfläche für Datenerfassung oder Experience Platform und wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Ereignisweiterleitung]** aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, wählen Sie im linken Navigationsbereich **[!UICONTROL Erweiterungen]** und dann die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie nach der Karte [!UICONTROL Metadaten-API] und wählen Sie dann **[!UICONTROL Installieren]** aus.

![Die für die Erweiterung [!UICONTROL Meta Conversions API] ausgewählte Option [!UICONTROL Installieren] in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/server/meta/install.png)

In der angezeigten Konfigurationsansicht müssen Sie die zuvor kopierte [!DNL Pixel] ID angeben, um die Erweiterung mit Ihrem Konto zu verknüpfen. Sie können die ID direkt in die Eingabe einfügen oder stattdessen ein Datenelement verwenden.

Sie müssen außerdem ein Zugriffstoken bereitstellen, um speziell das [!DNL Conversions API] zu verwenden. Anweisungen zum Abrufen dieses Werts finden Sie in der Dokumentation zu [!DNL Conversions API] unter [Generieren eines Zugriffstokens](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) .

Wählen Sie abschließend **[!UICONTROL Speichern]** aus.

![Die [!DNL Pixel] ID, die als Datenelement in der Erweiterungskonfigurationsansicht bereitgestellt wird.](../../../images/extensions/server/meta/configure.png)

Die -Erweiterung ist installiert und Sie können jetzt ihre Funktionen in Ihren Ereignisweiterleitungsregeln verwenden.

## Integration mit der Facebook- und Instagram-Erweiterung {#facebook}

Durch die Integration mit der Facebook- und Instagram-Erweiterung können Sie sich schnell bei Ihrem Meta Business-Konto authentifizieren. Dadurch werden Ihre [!UICONTROL Pixel-ID] und die Meta Conversions-API [!UICONTROL Zugriffs-Token] automatisch ausgefüllt, was die Installation und Konfiguration der Meta Conversions-API erleichtert.

Bei der Installation der Erweiterung [!UICONTROL Meta Conversions API] wird eine Dialogfeldmeldung zur Authentifizierung in Facebook und Instagram angezeigt.

![Die Installationsseite der [!UICONTROL API-Erweiterung für Metadaten-Konvertierungen], auf der die [!UICONTROL Verbindung zu Meta herstellen]} hervorgehoben wird.](../../../images/extensions/server/meta/mbe-extension-install.png)

Eine Dialogaufforderung zur Authentifizierung in Facebook und Instagram wird auch in der Schnellstart-Workflow-Benutzeroberfläche bei der Ereignisweiterleitung angezeigt.

![Die Schnellstart-Workflow-Benutzeroberfläche, die [!UICONTROL Verbindung zu Meta herstellen] hervorhebt.](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## Integration mit der Ereignisqualitätsübereinstimmung (EMQ) {#emq}

Durch die Integration mit der Ereignisqualitäts-Match-Bewertung (EMQ) können Sie die Effektivität Ihrer Implementierung einfach anzeigen, indem Sie EMQ-Bewertungen anzeigen. Diese Integration minimiert das Wechseln des Kontexts und hilft Ihnen, den Erfolg Ihrer Meta Conversions API-Implementierungen zu verbessern. Diese Ereignisbewertungen werden im Konfigurationsbildschirm der [!UICONTROL Meta Conversions API-Erweiterung] angezeigt.

![Die Konfigurationsseite der [!UICONTROL Meta Conversions API-Erweiterung] , auf der die [!UICONTROL EMQ-Punktzahl anzeigen]](../../../images/extensions/server/meta/emq-score.png) hervorgehoben wird.

## Integration mit LiveRamp (Alpha) {#alpha}

[!DNL LiveRamp] Kunden, die die authentifizierte Traffic-Lösung (ATS) von [!DNL LiveRamp] auf ihren Sites bereitgestellt haben, können sich dafür entscheiden, RampIDs als Kundendatenparameter freizugeben. Wenden Sie sich an Ihr [!DNL Meta] -Account-Team, um dem Alpha-Programm für diese Funktion beizutreten.

![Die Konfigurationsseite für die Metadatenereignisweiterleitung [!UICONTROL Regel] , auf der [!UICONTROL Partnername (Alpha)] und [!UICONTROL Partner-ID (Alpha)] hervorgehoben werden.](../../../images/extensions/server/meta/live-ramp.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

In diesem Abschnitt wird beschrieben, wie Sie die Erweiterung [!DNL Conversions API] in einer allgemeinen Ereignisweiterleitungsregel verwenden. In der Praxis sollten Sie mehrere Regeln konfigurieren, um alle akzeptierten [Standardereignisse](https://developers.facebook.com/docs/meta-pixel/reference) über [!DNL Meta Pixel] und [!DNL Conversions API] zu senden. Informationen zu Mobile-App-Daten finden Sie in den erforderlichen Feldern, Feldern für App-Daten, Parametern für Kundeninformationen und benutzerdefinierten Datendetails [hier](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events).

>[!NOTE]
>
>Ereignisse sollten [in Echtzeit gesendet werden](https://www.facebook.com/business/help/379226453470947?id=818859032317965) oder so nah wie möglich in Echtzeit, um eine bessere Anzeigenkampagnenoptimierung zu erzielen.

Beginnen Sie mit der Erstellung einer neuen Ereignisweiterleitungsregel und konfigurieren Sie deren Bedingungen nach Bedarf. Wählen Sie bei der Auswahl der Aktionen für die Regel **[!UICONTROL Metadaten-API-Erweiterung]** für die Erweiterung und dann für den Aktionstyp **[!UICONTROL Konversions-API-Ereignis senden]** aus.

![Der Aktionstyp [!UICONTROL Seitenansicht senden] , der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt ist.](../../../images/extensions/server/meta/select-action.png)

Es werden Steuerelemente angezeigt, mit denen Sie die Ereignisdaten konfigurieren können, die über den [!DNL Conversions API] an [!DNL Meta] gesendet werden. Diese Optionen können direkt in die bereitgestellten Eingaben eingegeben werden oder Sie können vorhandene Datenelemente auswählen, um die Werte stattdessen darzustellen. Die Konfigurationsoptionen sind wie unten beschrieben in vier Hauptabschnitte unterteilt.

| Konfigurationsabschnitt | Beschreibung |
| --- | --- |
| [!UICONTROL Server-Ereignisparameter] | Allgemeine Informationen zum Ereignis, einschließlich der Zeit, zu der es aufgetreten ist, und der Quellaktion, die es ausgelöst hat. Weitere Informationen zu den von den [!DNL Conversions API] akzeptierten Standardereignisparametern](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) finden Sie in der [!DNL Meta] Entwicklerdokumentation .[<br><br>Wenn Sie sowohl [!DNL Meta Pixel] als auch die [!DNL Conversions API] zum Senden von Ereignissen verwenden, stellen Sie sicher, dass Sie bei jedem Ereignis sowohl einen **[!UICONTROL Ereignisnamen]** (`event_name`) als auch eine **[!UICONTROL Ereignis-ID]** (`event_id`) einschließen, da diese Werte für die [Ereignisdeduplizierung](#deduplication) verwendet werden.<br><br>Sie haben auch die Option **[!UICONTROL Eingeschränkte Datenverwendung aktivieren]** , um die Einhaltung von Kunden-Opt-outs zu unterstützen. Weitere Informationen zu dieser Funktion finden Sie in der Dokumentation zu [!DNL Conversions API] zu den [Datenverarbeitungsoptionen](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) . |
| [!UICONTROL Parameter für Kundeninformationen] | Benutzeridentitätsdaten, mit denen das Ereignis einem Kunden zugeordnet wird. Einige dieser Werte müssen gehasht werden, bevor sie an die API gesendet werden können.<br><br>Um eine gute gemeinsame API-Verbindung und eine hohe EMQ-Qualität (Event Match Quality) sicherzustellen, wird empfohlen, alle [akzeptierten Parameter für Kundeninformationen](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) zusammen mit Serverereignissen zu senden. Diese Parameter sollten auch [entsprechend ihrer Bedeutung und Auswirkung auf EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965) priorisiert werden. |
| [!UICONTROL Benutzerdefinierte Daten] | Zusätzliche Daten, die zur Optimierung der Anzeigenbereitstellung verwendet werden und in Form eines JSON-Objekts bereitgestellt werden. Weitere Informationen zu den für dieses Objekt zulässigen Eigenschaften finden Sie in der [[!DNL Conversions API] Dokumentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) .<br><br>Wenn Sie ein Kaufereignis senden, müssen Sie in diesem Abschnitt die erforderlichen Attribute `currency` und `value` angeben. |
| [!UICONTROL Testereignis] | Mit dieser Option wird überprüft, ob Ihre Konfiguration dazu führt, dass Serverereignisse von [!DNL Meta] erwartungsgemäß empfangen werden. Um diese Funktion zu verwenden, aktivieren Sie das Kontrollkästchen **[!UICONTROL Als Testereignis senden]** und geben Sie in der unten stehenden Eingabe einen Test-Ereigniscode Ihrer Wahl ein. Nachdem die Ereignisweiterleitungsregel bereitgestellt wurde, sollten bei ordnungsgemäßer Konfiguration der Erweiterung und Aktion Aktivitäten in der **[!DNL Test Events]**-Ansicht in [!DNL Meta Events Manager] angezeigt werden. |

{style="table-layout:auto"}

Wählen Sie nach Abschluss **[!UICONTROL Änderungen beibehalten]** aus, um die Aktion zur Regelkonfiguration hinzuzufügen.

![[!UICONTROL Behalten Sie die für die Aktionskonfiguration ausgewählten Änderungen bei].](../../../images/extensions/server/meta/keep-changes.png)

Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus. Veröffentlichen Sie abschließend eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) , um die an der Bibliothek vorgenommenen Änderungen zu aktivieren.

## Ereignisdeduplizierung {#deduplication}

Wie im Abschnitt [ Voraussetzungen ](#prerequisites) erwähnt, wird empfohlen, sowohl die Tag-Erweiterung [!DNL Meta Pixel] als auch die Ereignisweiterleitungs-Erweiterung [!DNL Conversions API] zu verwenden, um dieselben Ereignisse vom Client und Server in einem redundanten Setup zu senden. Dies kann dazu beitragen, Ereignisse wiederherzustellen, die nicht von der einen oder anderen Erweiterung erfasst wurden.

Wenn Sie verschiedene Ereignistypen vom Client und Server senden, ohne dass sich die beiden überschneiden, ist keine Deduplizierung erforderlich. Wenn jedoch ein einzelnes Ereignis sowohl von [!DNL Meta Pixel] als auch von [!DNL Conversions API] freigegeben wird, müssen Sie sicherstellen, dass diese redundanten Ereignisse dedupliziert werden, damit Ihre Berichterstellung nicht beeinträchtigt wird.

Stellen Sie beim Senden von freigegebenen Ereignissen sicher, dass Sie eine Ereignis-ID und einen Namen mit jedem Ereignis einbeziehen, das Sie vom Client und vom Server senden. Wenn mehrere Ereignisse mit derselben ID und demselben Namen empfangen werden, verwendet [!DNL Meta] automatisch mehrere Strategien, um sie zu deduplizieren und die relevantesten Daten beizubehalten. Weitere Informationen zu diesem Prozess finden Sie in der Dokumentation [!DNL Meta] zu [Deduplizierung für  [!DNL Meta Pixel] und [!DNL Conversions API] Ereignisse](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) .

## Schnellstart-Workflow: Metadaten-Konversions-API-Erweiterung (Beta) {#quick-start}

>[!IMPORTANT]
>
>* Die Schnellstartfunktion steht Kunden zur Verfügung, die das Real-Time CDP Prime- und Ultimate-Package erworben haben. Bitte wenden Sie sich an den Adobe-Support-Mitarbeiter, um weitere Informationen zu erhalten.
>* Diese Funktion ist für neue Netto-Implementierungen vorgesehen und unterstützt derzeit nicht die automatische Installation von Erweiterungen und Konfigurationen für vorhandene Tags und Ereignisweiterleitungseigenschaften.

>[!NOTE]
>
>Jeder vorhandene Client kann die Schnellstart-Workflows verwenden, um eine Referenzimplementierung zu erstellen, die für Folgendes verwendet werden kann:
>* Verwenden Sie ihn als Beginn einer brandneuen Implementierung.
>* Nutzen Sie ihn als Referenzimplementierung, die Sie untersuchen können, um zu sehen, wie er konfiguriert wurde, und dann in Ihren aktuellen Produktionsimplementierungen replizieren können.

Mit der Schnellstartfunktion können Sie mit der Meta-Konversions-API und den Meta-Pixel-Erweiterungen einfach und effizient einrichten. Dieses Tool automatisiert mehrere Schritte, die in Adobe-Tags und Ereignisweiterleitung ausgeführt werden, wodurch die Einrichtungszeit erheblich verkürzt wird.

Diese Funktion installiert und konfiguriert automatisch sowohl die Meta Conversions-API als auch die Meta-Pixel-Erweiterungen für neu automatisch generierte Tags und die Ereignisweiterleitungs-Eigenschaft mit den erforderlichen Regeln und Datenelementen. Außerdem werden das Experience Platform Web SDK und Datastream automatisch installiert und konfiguriert. Schließlich veröffentlicht die Schnellstartfunktion die Bibliothek automatisch in der angegebenen URL in einer Entwicklungsumgebung, was die clientseitige Datenerfassung und die serverseitige Ereignisweiterleitung über die Ereignisweiterleitung und das Experience Platform-Edge Network in Echtzeit ermöglicht.

Das folgende Video bietet eine Einführung in die Schnellstarterfunktion.

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### Schnellstartfunktion installieren

>[!NOTE]
>
>Diese Funktion soll Ihnen bei den ersten Schritten mit der Implementierung der Ereignisweiterleitung helfen. Es wird keine End-to-End-Implementierung liefern, die voll funktionsfähig ist und allen Anwendungsfällen gerecht wird.

Bei diesem Setup werden sowohl die Meta Conversions-API als auch die Meta Pixel-Erweiterungen automatisch installiert. Diese Hybridimplementierung wird von Meta empfohlen, um serverseitige Ereigniskonversionen zu erfassen und weiterzuleiten.
Die schnelle Setup-Funktion soll Kunden bei den ersten Schritten mit der Implementierung der Ereignisweiterleitung unterstützen und soll keine vollständige Implementierung liefern, die alle Anwendungsfälle berücksichtigt.

Um die Funktion zu installieren, wählen Sie auf der Adobe Experience Platform-Datenerfassungsseite **[!UICONTROL Startseite]** die Option **[!UICONTROL Erste Schritte]** für **[!DNL Send Conversions Data to Meta]** aus.

![Startseite der Datenerfassung mit Konversionsdaten in Meta](../../../images/extensions/server/meta/conversion-data-to-meta.png)

Geben Sie Ihre **[!UICONTROL Domäne]** ein und wählen Sie dann **[!UICONTROL Weiter]** aus. Diese Domäne wird als Namenskonvention für automatisch generierte Tags und Ereignisweiterleitungseigenschaften, Regeln, Datenelemente, Datenspeicher usw. verwendet.

![Begrüßungsbildschirm, der den Domänennamen anfordert](../../../images/extensions/server/meta/welcome.png)

Geben Sie im Dialogfeld **[!UICONTROL Ersteinrichtung]** Ihre **[!UICONTROL Meta Pixel ID]**, den **[!UICONTROL Metadaten-API-Zugriffstoken]** und den **[!UICONTROL Datenschichtpfad]** ein und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Dialogfeld für die Ersteinrichtung](../../../images/extensions/server/meta/initial-setup.png)

Warten Sie einige Minuten, bis der anfängliche Einrichtungsprozess abgeschlossen ist, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Bildschirm zur Bestätigung der Ersteinrichtung](../../../images/extensions/server/meta/setup-complete.png)

Kopieren Sie im Dialogfeld **[!UICONTROL Code für Ihre Site hinzufügen]** den Code, der mit der Kopieren-Funktion ![Kopieren](../../../images/extensions/server/meta/copy-icon.png) bereitgestellt wird, und fügen Sie ihn in den Abschnitt `<head>` Ihrer Quellwebsite ein. Wählen Sie nach der Implementierung **[!UICONTROL Validierung starten]**

![Fügen Sie Code im Dialogfeld Ihrer Site hinzu](../../../images/extensions/server/meta/add-code-on-your-site.png)

Im Dialogfeld [!UICONTROL Überprüfungsergebnisse] werden die Ergebnisse der Implementierung der Meta-Erweiterung angezeigt. Wählen Sie **[!UICONTROL Weiter]** aus. Sie können auch zusätzliche Überprüfungsergebnisse anzeigen, indem Sie den Link **[!UICONTROL Zuverlässigkeit]** auswählen.

Dialogfeld ![Testergebnisse mit Implementierungsergebnissen anzeigen](../../../images/extensions/server/meta/test-results.png)

Die Anzeige **[!UICONTROL Nächste Schritte]** bestätigt den Abschluss des Setups. Von hier aus haben Sie die Möglichkeit, Ihre Implementierung zu optimieren, indem Sie neue Ereignisse hinzufügen, die im nächsten Abschnitt angezeigt werden.

Wenn Sie keine zusätzlichen Ereignisse hinzufügen möchten, wählen Sie **[!UICONTROL Schließen]** aus.

![Dialogfeld &quot;Nächste Schritte&quot;](../../../images/extensions/server/meta/next-steps.png)

#### Hinzufügen zusätzlicher Ereignisse

Um neue Ereignisse hinzuzufügen, wählen Sie **[!UICONTROL Webeigenschaft für Tags bearbeiten]** aus.

![Das Dialogfeld &quot;Nächste Schritte&quot;mit dem Bearbeiten der Web-Eigenschaft Ihrer Tags](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

Wählen Sie die Regel aus, die dem Meta-Ereignis entspricht, das Sie bearbeiten möchten. Beispiel: **MetaConversion_AddToCart**.

>[!NOTE]
>
>Wenn kein Ereignis vorhanden ist, wird diese Regel nicht ausgeführt. Dies gilt für alle Regeln, wobei die Regel **MetaConversion_PageView** die Ausnahme darstellt.

Um ein Ereignis hinzuzufügen, wählen Sie **[!UICONTROL Hinzufügen]** unter der Überschrift [!UICONTROL Ereignisse] aus.

![Tag-Eigenschaftenseite ohne Ereignisse](../../../images/extensions/server/meta/edit-rule.png)

Wählen Sie den [!UICONTROL Ereignistyp] aus. In diesem Beispiel haben wir das Ereignis [!UICONTROL Klick] ausgewählt und für den Trigger konfiguriert, wenn die Schaltfläche **.add-to-cart-button** ausgewählt wird. Wählen Sie **[!UICONTROL Änderungen beibehalten]** aus.

![Bildschirm für die Ereigniskonfiguration mit dem Klick-Ereignis](../../../images/extensions/server/meta/event-configuration.png)

Das neue Ereignis wurde gespeichert. Wählen Sie **[!UICONTROL Eine Arbeitsbibliothek auswählen]** und wählen Sie die Bibliothek aus, die Sie erstellen möchten.

![Wählen Sie eine Dropdown-Liste für die Arbeitsbibliothek aus](../../../images/extensions/server/meta/working-library.png)

Wählen Sie als Nächstes das Dropdown-Menü neben **[!UICONTROL In Bibliothek speichern]** und dann **[!UICONTROL In Bibliothek speichern und erstellen]**. Dadurch wird die Änderung in der Bibliothek veröffentlicht.

![Wählen Sie &quot;In Bibliothek speichern und erstellen&quot;](../../../images/extensions/server/meta/save-and-build.png)

Wiederholen Sie diese Schritte für jedes andere Meta-Konversionsereignis, das Sie konfigurieren möchten.

#### Datenschichtkonfiguration {#configuration}

>[!IMPORTANT]
>
>Die Art und Weise, wie Sie diese globale Datenschicht aktualisieren, hängt von Ihrer Website-Architektur ab. Eine einseitige Anwendung unterscheidet sich von einer serverseitigen Rendering-App. Es besteht auch die Möglichkeit, dass Sie vollständig dafür verantwortlich sind, diese Daten innerhalb des Tags-Produkts zu erstellen und zu aktualisieren. In allen Fällen muss die Datenschicht zwischen dem Ausführen der einzelnen `MetaConversion_* rules` aktualisiert werden. Wenn Sie die Daten zwischen den Regeln nicht aktualisieren, können Sie auch auf einen Fall stoßen, in dem Sie veraltete Daten aus den letzten `MetaConversion_* rule` im aktuellen `MetaConversion_* rule` senden.

Während der Konfiguration wurden Sie gefragt, wo sich Ihre Datenschicht befindet. Standardmäßig ist dies `window.dataLayer.meta`. Innerhalb des `meta` -Objekts werden Ihre Daten erwartet, wie unten dargestellt.

![Datenschicht-Metadaten](../../../images/extensions/server/meta/data-layer-meta.png)

Dies ist wichtig, da jede `MetaConversion_*` -Regel diese Datenstruktur verwendet, um die relevanten Datenteile an die [!DNL Meta Pixel] -Erweiterung und an die [!DNL Meta Conversions API] zu übergeben. Weitere Informationen dazu, welche Daten für verschiedene Meta-Ereignisse erforderlich sind, finden Sie in der Dokumentation zu [Standardereignissen](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) .

Wenn Sie beispielsweise die Regel `MetaConversion_Subscribe` verwenden möchten, müssen Sie `window.dataLayer.meta.currency`, `window.dataLayer.meta.predicted_ltv` und `window.dataLayer.meta.value` entsprechend den Objekteigenschaften aktualisieren, die in der Dokumentation zu [Standardereignissen](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) beschrieben sind.

Im Folgenden finden Sie ein Beispiel dafür, was auf einer Website ausgeführt werden muss, um die Datenschicht zu aktualisieren, bevor die Regel ausgeführt wird.

![Daten-Layer-Metadaten aktualisieren](../../../images/extensions/server/meta/update-data-layer-meta.png)

Standardmäßig wird die `<datalayerpath>.conversionData.eventId` zufällig von der Aktion &quot;Neue Ereignis-ID generieren&quot;für eine der `MetaConversion_* rules` generiert.

Um eine lokale Referenz dazu zu erhalten, wie die Datenschicht aussehen soll, können Sie den Editor für benutzerdefinierten Code im Datenelement `MetaConversion_DataLayer` in Ihrer Eigenschaft öffnen.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie serverseitige Ereignisdaten mit der Erweiterung [!DNL Meta Conversions API] an [!DNL Meta] gesendet werden. Von hier aus wird empfohlen, Ihre Integration zu erweitern, indem mehr [!DNL Pixels] verbunden und ggf. weitere Ereignisse freigegeben werden. Eine der folgenden Maßnahmen kann dazu beitragen, Ihre Anzeigenleistung weiter zu verbessern:

* Verbinden Sie alle anderen [!DNL Pixels] , die noch nicht mit einer [!DNL Conversions API] -Integration verbunden sind.
* Wenn Sie bestimmte Ereignisse ausschließlich über [!DNL Meta Pixel] auf Client-Seite senden, senden Sie diese Ereignisse auch vom Server-seitigen an den [!DNL Conversions API].

Weitere Anleitungen zur effektiven Implementierung Ihrer Integration finden Sie in der [!DNL Meta] -Dokumentation zu den [Best Practices für den [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) . Allgemeine Informationen zu Tags und zur Ereignisweiterleitung in Adobe Experience Cloud finden Sie in der [Tag-Übersicht](../../../home.md) .
