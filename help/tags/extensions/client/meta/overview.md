---
title: Metapixelerweiterung - Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Meta Pixel“ in Adobe Experience Platform vertraut.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# [!DNL Meta Pixel] - Übersicht

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ist ein JavaScript-basiertes Analyse-Tool, mit dem Sie Besucheraktivitäten auf Ihrer Website verfolgen können. Besucheraktionen, die Sie verfolgen (so genannte Konversionen), werden an [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) gesendet, wo sie zur Messung der Effektivität Ihrer Anzeigen, Kampagnen, Konversionstrichter und mehr verwendet werden können.

Mit der [!DNL Meta Pixel] Tag-Erweiterung können Sie [!DNL Pixel] Funktionen in Ihren Client-seitigen Tag-Bibliotheken nutzen. In diesem Dokument wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer [Regel](../../../ui/managing-resources/rules.md) verwenden.

## Voraussetzungen

Um die Erweiterung verwenden zu können, müssen Sie über ein gültiges [!DNL Meta] mit Zugriff auf [!DNL Ads Manager] verfügen. Insbesondere müssen Sie [einen neuen erstellen [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) und dessen [!DNL Pixel ID] kopieren, damit die Erweiterung für Ihr Konto konfiguriert werden kann. Wenn Sie bereits über eine vorhandene [!DNL Meta Pixel] verfügen, können Sie stattdessen deren ID verwenden.

Es wird dringend empfohlen, [!DNL Meta Pixel] in Kombination mit dem -[!DNL Meta Conversions API] zu verwenden, um dieselben Ereignisse von der Client- bzw. Server-Seite freizugeben und zu senden, da dies dazu beitragen kann, Ereignisse wiederherzustellen, die von [!DNL Meta Pixel] nicht erfasst wurden. Anweisungen zur Integration in [[!DNL Meta Conversions API]  Server-seitigen Implementierungen finden &#x200B;](../../client/meta/overview.md) im Handbuch zur -Erweiterung für die. Beachten Sie, dass Ihre Organisation Zugriff auf [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) haben muss, um die Server-seitige Erweiterung verwenden zu können.

## Installieren der Erweiterung

Um die [!DNL Meta Pixel]-Erweiterung zu installieren, navigieren Sie zur Datenerfassungs-Benutzeroberfläche oder zur Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL Tags]** in der linken Navigationsleiste aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, klicken Sie im linken **auf** Erweiterungen und wählen Sie dann die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie nach der Karte [!UICONTROL Meta Pixel] und wählen Sie dann **[!UICONTROL Installieren]** aus.

![Die ausgewählte Schaltfläche [!UICONTROL Installieren] für die Erweiterung [!UICONTROL Meta Pixel] in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/client/meta/install.png)

In der angezeigten Konfigurationsansicht müssen Sie die zuvor kopierte [!DNL Pixel]-ID angeben, um die Erweiterung mit Ihrem Konto zu verknüpfen. Sie können die ID direkt in die Eingabe einfügen oder stattdessen ein vorhandenes Datenelement auswählen.

>[!TIP]
>
>Durch die Verwendung eines Datenelements haben Sie die Möglichkeit, die verwendete [!DNL Pixel]-ID in Abhängigkeit von anderen Faktoren wie der Build-Umgebung dynamisch zu ändern. Weitere Informationen finden Sie im Anhang [Verwenden  [!DNL Pixel]  IDs für &#x200B;](#id-data-element) Umgebungen“.

Sie können optional auch eine Ereignis-ID angeben, die mit der Erweiterung verknüpft werden soll. Damit werden identische Ereignisse zwischen [!DNL Meta Pixel] und dem [!DNL Meta Conversions API] dedupliziert. Weitere Informationen finden Sie im Abschnitt [Ereignisdeduplizierung](../../server/meta/overview.md#event-deduplication) in der Übersicht zur [!DNL Conversions API].

Klicken Sie abschließend auf **[!UICONTROL Speichern]**

![Die [!DNL Pixel]-ID, die als Datenelement in der Erweiterungskonfigurationsansicht bereitgestellt wird.](../../../images/extensions/client/meta/configure.png)

Die Erweiterung ist installiert und Sie können jetzt ihre verschiedenen Aktionen in Ihren Tag-Regeln verwenden.

## Konfigurieren einer Tag-Regel {#rule}

[!DNL Meta Pixel] akzeptiert einen Satz vordefinierter [Standardereignisse](https://www.facebook.com/business/help/402791146561655) mit jeweils eigenen Kontexten und akzeptierten Eigenschaften. Die von der [!DNL Pixel] bereitgestellten Regelaktionen korrelieren mit diesen Ereignistypen, sodass Sie das an [!DNL Meta] gesendete Ereignis einfach entsprechend seinem Typ kategorisieren und konfigurieren können.

Zu Demonstrationszwecken wird in diesem Abschnitt gezeigt, wie eine Regel erstellt wird, die ein Seitenansichtsereignis an [!DNL Meta] sendet.

Beginnen Sie mit der Erstellung einer neuen Tag-Regel und konfigurieren Sie die Bedingungen nach Bedarf. Wählen Sie bei der Auswahl der Aktionen für die Regel **[!UICONTROL Metapixel]** für die Erweiterung aus und wählen Sie dann **[!UICONTROL Seitenansicht senden]** für den Aktionstyp aus.

![Der [!UICONTROL Seitenansicht senden] Aktionstyp, der für eine Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt wird.](../../../images/extensions/client/meta/select-action.png)

Für die Aktion „Seitenansicht senden[!UICONTROL &#x200B; ist keine weitere Konfiguration &#x200B;]. Wählen **[!UICONTROL Änderungen beibehalten]**, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

Veröffentlichen Sie abschließend ein neues Tag [Build](../../../ui/publishing/builds.md), um die Änderungen an der Bibliothek zu aktivieren.

## Vergewissern Sie sich, dass [!DNL Meta] Daten erhält

Nachdem Ihr aktualisierter Build auf Ihrer Website bereitgestellt wurde, können Sie überprüfen, ob Daten wie erwartet gesendet werden, indem Sie einige Konversionsereignisse in Ihrem Browser generieren und überprüfen, ob diese Ereignisse in [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180) angezeigt werden.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Daten mithilfe der [!DNL Meta Pixel]-Tag-Erweiterung an [!DNL Meta] senden. Wenn Sie planen, Server-seitige Ereignisse auch an [!DNL Meta] zu senden, können Sie jetzt mit der Installation und Konfiguration der Erweiterung [[!DNL Conversions API] Ereignisweiterleitung“ &#x200B;](../../server/meta/overview.md).

Weiterführende Informationen zu Tags in Experience Platform finden Sie in der [Übersicht zu Tags](../../../home.md).

## Anhang: Verwenden verschiedener [!DNL Pixel]-IDs für verschiedene Umgebungen {#id-data-element}

Wenn Sie Ihre Implementierung in Entwicklungs- oder Staging-Umgebungen testen möchten, während Ihre Produktions- [!DNL Meta Pixel] Analytics intakt bleiben, können Sie ein Datenelement verwenden, um je nach verwendeter Umgebung dynamisch eine geeignete [!DNL Pixel]-ID auszuwählen.

Sie können dies erreichen, indem Sie ein [!UICONTROL Benutzerdefinierter Code]-Datenelement (bereitgestellt von der [[!UICONTROL Core]-Erweiterung](../core/overview.md)) in Kombination mit der [`turbine` freien Variable verwenden](../../../extension-dev/turbine.md). Verwenden Sie im JavaScript-Code des Datenelements das `turbine`, um die aktuelle Umgebungsstufe zu finden, und geben Sie dann basierend auf dem Ergebnis eine entsprechende [!DNL Pixel]-ID zurück.

Im folgenden Beispiel wird eine falsche Produktions-ID `exampleProductionKey` zurückgegeben, wenn sie in der Produktionsumgebung verwendet wird, und eine andere ID `exampleTestKey`, wenn eine andere Umgebung verwendet wird. Ersetzen Sie bei der Implementierung dieses Codes jeden Wert durch Ihre tatsächlichen Produktions- und [!DNL Pixel].

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
