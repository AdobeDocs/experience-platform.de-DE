---
title: Übersicht über die API-Erweiterung für Meta Conversions
description: Erfahren Sie mehr über die Meta Conversions API-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 1%

---

# [!DNL Meta Conversions API] Erweiterungsübersicht

Die [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) ermöglicht es Ihnen, Ihre Server-seitigen Marketing-Daten mit [!DNL Meta] Technologien zur Optimierung Ihres Anzeigen-Targeting, Senkung der Kosten pro Aktion und Messung der Ergebnisse. Ereignisse sind mit einer [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID und werden ähnlich wie clientseitige Ereignisse verarbeitet.

Verwenden der [!DNL Meta Conversions API] -Erweiterung verwenden, können Sie die API-Funktionen in Ihrer [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) Regeln zum Senden von Daten an [!DNL Meta] vom Adobe Experience Platform Edge Network aus. In diesem Dokument wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in der Ereignisweiterleitung verwenden. [Regel](../../../ui/managing-resources/rules.md).

## Voraussetzungen

Es wird dringend empfohlen, [!DNL Meta Pixel] und [!DNL Conversions API] , um dieselben Ereignisse vom Client- bzw. vom Server-seitigen freizugeben und zu senden, da dies dazu beitragen kann, Ereignisse wiederherzustellen, die nicht von abgerufen wurden [!DNL Meta Pixel]. Vor der Installation [!DNL Conversions API] -Erweiterung, siehe Handbuch im [[!DNL Meta Pixel] Erweiterung](../../client/meta/overview.md) für Schritte zur Integration in Ihre clientseitigen Tag-Implementierungen.

>[!NOTE]
>
>Der Abschnitt zu [Ereignisdeduplizierung](#deduplication) weiter unten in diesem Dokument die Schritte beschrieben, um sicherzustellen, dass dasselbe Ereignis nicht zweimal verwendet wird, da es sowohl vom Browser als auch vom Server empfangen werden kann.

Um die [!DNL Conversions API] -Erweiterung, müssen Sie Zugriff auf die Ereignisweiterleitung haben und über eine gültige [!DNL Meta] Konto mit Zugriff auf [!DNL Ad Manager] und [!DNL Event Manager]. Insbesondere müssen Sie die Kennung eines vorhandenen [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (oder [eine neue [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) ), damit die Erweiterung für Ihr Konto konfiguriert werden kann.

## Installieren der Erweiterung

So installieren Sie die [!DNL Meta Conversions API] Erweiterung, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL Ereignisweiterleitung]** über die linke Navigation. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, wählen Sie **[!UICONTROL Erweiterungen]** Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Katalog]** Registerkarte. Suchen Sie nach [!UICONTROL Meta Conversions-API] Karte, und wählen Sie **[!UICONTROL Installieren]**.

![Die [!UICONTROL Installieren] für die [!UICONTROL Meta Conversions-API] -Erweiterung in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/server/meta/install.png)

In der angezeigten Konfigurationsansicht müssen Sie die Variable [!DNL Pixel] ID, die Sie zuvor kopiert haben, um die Erweiterung mit Ihrem Konto zu verknüpfen. Sie können die ID direkt in die Eingabe einfügen oder stattdessen ein Datenelement verwenden.

Sie müssen außerdem ein Zugriffstoken bereitstellen, um die [!DNL Conversions API] speziell. Siehe Abschnitt [!DNL Conversions API] Dokumentation zu [Zugriffstoken generieren](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) für Schritte zum Abrufen dieses Werts.

Klicken Sie abschließend auf **[!UICONTROL Speichern]**

![Die [!DNL Pixel] ID, die in der Erweiterungskonfigurationsansicht als Datenelement bereitgestellt wird.](../../../images/extensions/server/meta/configure.png)

Die Erweiterung ist installiert und Sie können jetzt ihre Funktionen in Ihren Ereignisweiterleitungsregeln verwenden.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

In diesem Abschnitt wird die Verwendung der [!DNL Conversions API] -Erweiterung in einer generischen Ereignisweiterleitungsregel. In der Praxis sollten Sie mehrere Regeln konfigurieren, um alle akzeptierten zu senden [Standardereignisse](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] und [!DNL Conversions API].

>[!NOTE]
>
>Ereignisse sollten [in Echtzeit gesendet](https://www.facebook.com/business/help/379226453470947?id=818859032317965) oder so nah wie möglich in Echtzeit, um eine bessere Anzeigenkampagnenoptimierung zu erzielen.

Beginnen Sie mit der Erstellung einer neuen Ereignisweiterleitungsregel und konfigurieren Sie deren Bedingungen nach Bedarf. Wenn Sie die Aktionen für die Regel auswählen, wählen Sie **[!UICONTROL API-Erweiterung für Meta Conversions]** für die Erweiterung und wählen Sie dann **[!UICONTROL Ereignis der Konversions-API senden]** für den Aktionstyp.

![Die [!UICONTROL Seitenansicht senden] Aktionstyp, der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt wird.](../../../images/extensions/server/meta/select-action.png)

Es werden Steuerelemente angezeigt, mit denen Sie die Ereignisdaten konfigurieren können, die an [!DNL Meta] über die [!DNL Conversions API]. Diese Optionen können direkt in die bereitgestellten Eingaben eingegeben werden oder Sie können vorhandene Datenelemente auswählen, um die Werte stattdessen darzustellen. Die Konfigurationsoptionen sind wie unten beschrieben in vier Hauptabschnitte unterteilt.

| Konfigurationsabschnitt | Beschreibung |
| --- | --- |
| [!UICONTROL Server-Ereignisparameter] | Allgemeine Informationen zum Ereignis, einschließlich der Zeit, zu der es aufgetreten ist, und der Quellaktion, die es ausgelöst hat. Siehe Abschnitt [!DNL Meta] Entwicklerdokumentation für weitere Informationen zu [Standard-Ereignisparameter](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) von [!DNL Conversions API].<br><br>Wenn Sie beide [!DNL Meta Pixel] und [!DNL Conversions API] Um Ereignisse zu senden, stellen Sie sicher, dass Sie sowohl eine **[!UICONTROL Ereignisname]** (`event_name`) und **[!UICONTROL Ereignis-ID]** (`event_id`) bei jedem Ereignis verwenden, da diese Werte für [Ereignisdeduplizierung](#deduplication).<br><br>Sie haben auch die Möglichkeit, **[!UICONTROL Eingeschränkte Datenverwendung aktivieren]** um die Einhaltung von Kunden-Opt-outs zu unterstützen. Siehe [!DNL Conversions API] Dokumentation zu [Datenverarbeitungsoptionen](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) für Details zu dieser Funktion. |
| [!UICONTROL Parameter für Kundeninformationen] | Benutzeridentitätsdaten, mit denen das Ereignis einem Kunden zugeordnet wird. Einige dieser Werte müssen gehasht werden, bevor sie an die API gesendet werden können.<br><br>Um eine gute gemeinsame API-Verbindung und eine hohe Ereignisübereinstimmungsqualität (EMQ) sicherzustellen, wird empfohlen, alle [akzeptierte Kundeninformationsparameter](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) neben Serverereignissen. Diese Parameter sollten ebenfalls [priorisiert anhand ihrer Bedeutung und Auswirkung auf EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Benutzerdefinierte Daten] | Zusätzliche Daten, die zur Optimierung der Anzeigenbereitstellung verwendet werden und in Form eines JSON-Objekts bereitgestellt werden. Siehe Abschnitt [[!DNL Conversions API] Dokumentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) für weitere Informationen zu den zulässigen Eigenschaften für dieses Objekt.<br><br>Wenn Sie ein Kaufereignis senden, müssen Sie in diesem Abschnitt die erforderlichen Attribute angeben `currency` und `value`. |
| [!UICONTROL Testereignis] | Diese Option wird verwendet, um zu überprüfen, ob Ihre Konfiguration dazu führt, dass Serverereignisse von empfangen werden [!DNL Meta] wie erwartet. Um diese Funktion zu verwenden, wählen Sie die **[!UICONTROL Als Testereignis senden]** und geben Sie dann in der unten stehenden Eingabe einen Test-Ereigniscode Ihrer Wahl ein. Nachdem die Ereignisweiterleitungsregel bereitgestellt wurde, sollten bei der korrekten Konfiguration der Erweiterung und Aktion Aktivitäten angezeigt werden, die im **[!DNL Test Events]** Ansicht in [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Änderungen beibehalten]** , um die Aktion zur Regelkonfiguration hinzuzufügen.

![[!UICONTROL Änderungen beibehalten] für die Aktionskonfiguration ausgewählt werden.](../../../images/extensions/server/meta/keep-changes.png)

Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]**. Veröffentlichen Sie schließlich eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) um die Änderungen zu aktivieren, die an der Bibliothek vorgenommen wurden.

## Ereignis-Deduplizierung {#deduplication}

Wie in [Abschnitt mit Voraussetzungen](#prerequisites), wird empfohlen, beide [!DNL Meta Pixel] Tag-Erweiterung und [!DNL Conversions API] Ereignisweiterleitungs-Erweiterung, um dieselben Ereignisse vom Client und Server in einer redundanten Einrichtung zu senden. Dies kann dazu beitragen, Ereignisse wiederherzustellen, die nicht von der einen oder anderen Erweiterung erfasst wurden.

Wenn Sie verschiedene Ereignistypen vom Client und Server senden, ohne dass sich die beiden überschneiden, ist keine Deduplizierung erforderlich. Wenn jedoch ein einzelnes Ereignis von beiden [!DNL Meta Pixel] und [!DNL Conversions API]müssen Sie sicherstellen, dass diese redundanten Ereignisse dedupliziert werden, damit Ihre Berichterstellung nicht beeinträchtigt wird.

Stellen Sie beim Senden freigegebener Ereignisse sicher, dass Sie eine Ereignis-ID und einen Namen in jedes Ereignis einschließen, das Sie vom Client und vom Server senden. Wenn mehrere Ereignisse mit derselben ID und demselben Namen empfangen werden, [!DNL Meta] verwendet automatisch mehrere Strategien, um sie zu deduplizieren und die relevantesten Daten beizubehalten. Siehe [!DNL Meta] Dokumentation zu [Deduplizierung für [!DNL Meta Pixel] und [!DNL Conversions API] events](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) für Details zu diesem Prozess.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie serverseitige Ereignisdaten an senden [!DNL Meta] mithilfe der [!DNL Meta Conversions API] -Erweiterung. Von hier aus wird empfohlen, Ihre Integration durch die Verbindung von mehr [!DNL Pixels] und teilen Sie ggf. weitere Ereignisse. Eine der folgenden Maßnahmen kann dazu beitragen, Ihre Anzeigenleistung weiter zu verbessern:

* Andere verbinden [!DNL Pixels] , die noch nicht mit einer [!DNL Conversions API] Integration.
* Wenn Sie bestimmte Ereignisse ausschließlich über senden [!DNL Meta Pixel] Client-seitig senden Sie dieselben Ereignisse an die [!DNL Conversions API] auch vom Server aus.

Siehe [!DNL Meta] Dokumentation zu [Best Practices für [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) für weitere Anleitungen zur effektiven Implementierung Ihrer Integration. Allgemeine Informationen zu Tags und zur Ereignisweiterleitung in Adobe Experience Cloud finden Sie im Abschnitt [Tag-Übersicht](../../../home.md).
