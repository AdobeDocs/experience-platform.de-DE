---
title: Übersicht über Meta-Pixel-Erweiterung
description: Erfahren Sie mehr über die Meta-Pixel-Tag-Erweiterung in Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Übersicht über die [!DNL Meta Pixel]-Erweiterung

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ist ein JavaScript-basiertes Analysetool, mit dem Sie Besucheraktivitäten auf Ihrer Website verfolgen können. Von Ihnen verfolgte Besucheraktionen (so genannte Konversionen) werden an [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) gesendet, wo sie zur Messung der Effektivität Ihrer Anzeigen, Kampagnen, Konversionstrichter und mehr verwendet werden können.

Mit der Tag-Erweiterung [!DNL Meta Pixel] können Sie [!DNL Pixel] -Funktionen in Ihren clientseitigen Tag-Bibliotheken nutzen. In diesem Dokument wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer [Regel](../../../ui/managing-resources/rules.md) verwenden.

## Voraussetzungen

Um die Erweiterung verwenden zu können, müssen Sie über ein gültiges [!DNL Meta]-Konto mit Zugriff auf [!DNL Ads Manager] verfügen. Insbesondere müssen Sie [einen neuen  [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) erstellen und seinen [!DNL Pixel ID] kopieren, damit die Erweiterung für Ihr Konto konfiguriert werden kann. Wenn Sie bereits über eine vorhandene [!DNL Meta Pixel] verfügen, können Sie stattdessen deren ID verwenden.

Es wird dringend empfohlen, [!DNL Meta Pixel] in Kombination mit dem [!DNL Meta Conversions API] zu verwenden, um dieselben Ereignisse vom Client- bzw. vom Server-seitigen Ereignis freizugeben und zu senden, da dies dazu beitragen kann, Ereignisse wiederherzustellen, die nicht von [!DNL Meta Pixel] erfasst wurden. Anweisungen zur Integration in Ihre serverseitigen Implementierungen finden Sie im Handbuch zur [[!DNL Meta Conversions API] Erweiterung für die Ereignisweiterleitung](../../client/meta/overview.md) . Beachten Sie, dass Ihr Unternehmen Zugriff auf die [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) haben muss, um die serverseitige Erweiterung verwenden zu können.

## Installieren der Erweiterung

Um die Erweiterung [!DNL Meta Pixel] zu installieren, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder Experience Platform-Benutzeroberfläche und wählen Sie im linken Navigationsbereich **[!UICONTROL Tags]** aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, wählen Sie im linken Navigationsbereich **[!UICONTROL Erweiterungen]** und dann die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie nach der Karte [!UICONTROL Meta Pixel] und wählen Sie dann **[!UICONTROL Install]** aus.

![Die Schaltfläche [!UICONTROL Installieren], die für die Erweiterung [!UICONTROL Meta Pixel] in der Datenerfassungs-Benutzeroberfläche ausgewählt ist.](../../../images/extensions/client/meta/install.png)

In der angezeigten Konfigurationsansicht müssen Sie die zuvor kopierte [!DNL Pixel] ID angeben, um die Erweiterung mit Ihrem Konto zu verknüpfen. Sie können die ID direkt in die Eingabe einfügen oder stattdessen ein vorhandenes Datenelement auswählen.

>[!TIP]
>
>Die Verwendung eines Datenelements gibt Ihnen die Möglichkeit, die verwendete [!DNL Pixel]-ID dynamisch zu ändern, je nach anderen Faktoren wie der Build-Umgebung. Weitere Informationen finden Sie im Anhang zu [Verwendung verschiedener [!DNL Pixel] IDs für verschiedene Umgebungen](#id-data-element) .

Sie können optional auch eine Ereignis-ID angeben, die mit der Erweiterung verknüpft werden soll. Damit werden identische Ereignisse zwischen [!DNL Meta Pixel] und [!DNL Meta Conversions API] dedupliziert. Weitere Informationen finden Sie im Abschnitt zur [Ereignisdeduplizierung](../../server/meta/overview.md#event-deduplication) in der Übersicht zur [!DNL Conversions API] -Erweiterung.

Wählen Sie abschließend **[!UICONTROL Speichern]** aus.

![Die [!DNL Pixel] ID, die als Datenelement in der Erweiterungskonfigurationsansicht bereitgestellt wird.](../../../images/extensions/client/meta/configure.png)

Die -Erweiterung ist installiert und Sie können jetzt die verschiedenen Aktionen in Ihren Tag-Regeln verwenden.

## Tag-Regel konfigurieren {#rule}

[!DNL Meta Pixel] akzeptiert einen Satz vordefinierter [Standardereignisse](https://www.facebook.com/business/help/402791146561655) mit jeweils eigenen Kontexten und akzeptierten Eigenschaften. Die von der Erweiterung [!DNL Pixel] bereitgestellten Regelaktionen korrelieren mit diesen Ereignistypen, sodass Sie das Ereignis, das an [!DNL Meta] gesendet wird, einfach entsprechend seinem Typ kategorisieren und konfigurieren können.

Zu Demonstrationszwecken wird in diesem Abschnitt gezeigt, wie eine Regel erstellt wird, die ein Seitenansichtsereignis an [!DNL Meta] sendet.

Beginnen Sie mit der Erstellung einer neuen Tag-Regel und konfigurieren Sie deren Bedingungen nach Bedarf. Wählen Sie bei der Auswahl der Aktionen für die Regel **[!UICONTROL Meta Pixel]** für die Erweiterung und dann **[!UICONTROL Seitenansicht senden]** für den Aktionstyp aus.

![Der Aktionstyp [!UICONTROL Seitenansicht senden] , der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt ist.](../../../images/extensions/client/meta/select-action.png)

Für die Aktion [!UICONTROL Seitenansicht senden] ist keine weitere Konfiguration erforderlich. Wählen Sie **[!UICONTROL Änderungen beibehalten]** aus, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

Veröffentlichen Sie abschließend das neue Tag [build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Bestätigen, dass [!DNL Meta] Daten erhält

Nachdem Ihr aktualisierter Build auf Ihrer Website bereitgestellt wurde, können Sie überprüfen, ob die Daten erwartungsgemäß gesendet werden, indem Sie Konversionsereignisse in Ihrem Browser generieren und überprüfen, ob diese Ereignisse in [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180) angezeigt werden.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Daten mit der Tag-Erweiterung [!DNL Meta Pixel] an [!DNL Meta] gesendet werden. Wenn Sie auch serverseitige Ereignisse an [!DNL Meta] senden möchten, können Sie jetzt mit der Installation und Konfiguration der [[!DNL Conversions API] Ereignisweiterleitungs-Erweiterung](../../server/meta/overview.md) fortfahren.

Weiterführende Informationen zu Tags in Experience Platform finden Sie in der [Tag-Übersicht](../../../home.md) .

## Anhang: Verwendung verschiedener [!DNL Pixel] IDs für verschiedene Umgebungen {#id-data-element}

Wenn Sie Ihre Implementierung in Entwicklungs- oder Staging-Umgebungen testen und dabei die Produktionsanalyse [!DNL Meta Pixel] intakt halten möchten, können Sie mithilfe eines Datenelements je nach verwendeter Umgebung dynamisch eine entsprechende [!DNL Pixel] ID auswählen.

Sie können dies erreichen, indem Sie ein [!UICONTROL benutzerdefinierter Code] -Datenelement (bereitgestellt von der [[!UICONTROL Core] -Erweiterung](../core/overview.md)) in Kombination mit der [`turbine` freien Variable](../../../extension-dev/turbine.md) verwenden. Verwenden Sie im JavaScript-Code des Datenelements das Objekt `turbine` , um die aktuelle Umgebungsstufe zu finden, und geben Sie dann eine passende [!DNL Pixel] -ID basierend auf dem Ergebnis zurück.

Im folgenden Beispiel wird eine falsche Produktions-ID `exampleProductionKey` bei Verwendung in der Produktionsumgebung und eine andere ID `exampleTestKey` zurückgegeben, wenn eine andere Umgebung verwendet wird. Ersetzen Sie bei der Implementierung dieses Codes jeden Wert durch Ihre tatsächlichen Produktions- und Test-IDs [!DNL Pixel] .

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
