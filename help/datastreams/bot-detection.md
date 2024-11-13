---
title: Konfigurieren der Bot-Erkennung für Datenspeicher
description: Erfahren Sie, wie Sie die Bot-Erkennung für Datastreams konfigurieren, um menschlichen und nichtmenschlichen Traffic zu unterscheiden.
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: e3768a3f695abeedc9a3ce2fef591c6ecae9a897
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---

# Konfigurieren der Bot-Erkennung für Datenspeicher

Unmenschlicher Traffic von automatisierten Programmen, Webcrappern, Spidern und Skriptscannern kann es schwierig machen, Ereignisse von Besuchern zu identifizieren. Dieser Traffic-Typ kann sich negativ auf wichtige Geschäftsmetriken auswirken und zu falschen Traffic-Berichten führen.

Mit der Bot-Erkennung können Sie Ereignisse identifizieren, die vom [Web SDK](../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) und [[!DNL Server API]](../server-api/overview.md) generiert wurden, als von bekannten Spiders und Bots generiert.

Durch die Konfiguration der Bot-Erkennung für Ihre Datenspeicher können Sie bestimmte IP-Adressen, IP-Bereiche und Anforderungsheader identifizieren, die als Bot-Ereignisse klassifiziert werden sollen. Dadurch erhalten Sie eine genauere Messung der Benutzeraktivität auf Ihrer Site oder in Ihrer mobilen Anwendung.

Wenn eine Anfrage an das Edge Network mit einer der Bot-Erkennungsregeln übereinstimmt, wird das XDM-Schema mit einem Bot-Score aktualisiert (immer auf 1 gesetzt), wie unten dargestellt:

```json
{
  "botDetection": {
    "score": 1
  }
}
```

Diese Bot-Bewertung hilft den Lösungen, die die Anfrage erhalten, den Bot-Traffic korrekt zu identifizieren.

>[!IMPORTANT]
>
>Bei der Bot-Erkennung werden keine Bot-Anforderungen entfernt. Es aktualisiert nur das XDM-Schema mit dem Bot-Scoring und leitet das Ereignis an den von Ihnen konfigurierten [Datastream-Dienst](configure.md) weiter.
>
>Adobe-Lösungen können Bot-Scoring auf unterschiedliche Weise handhaben. Adobe Analytics verwendet beispielsweise seinen eigenen [Bot-Filterdienst](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html) und verwendet nicht den vom Edge Network festgelegten Wert. Die beiden Dienste verwenden dieselbe [IAB-Bot-Liste](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), sodass die Bot-Auswertung identisch ist.

Es kann bis zu 15 Minuten dauern, bis Bot-Erkennungsregeln nach der Erstellung über das Edge Network übertragen werden.

## Voraussetzungen {#prerequisites}

Damit die Bot-Erkennung auf Ihrem Datastream funktioniert, müssen Sie die Feldergruppe **[!UICONTROL Bot-Erkennungsinformationen]** zu Ihrem Schema hinzufügen. Informationen zum Hinzufügen von Feldergruppen zu einem Schema finden Sie in der Dokumentation zum [XDM-Schema](../xdm/ui/resources/schemas.md#add-field-groups) .

## Konfigurieren der Bot-Erkennung für Datenspeicher {#configure}

Sie können die Bot-Erkennung konfigurieren, nachdem Sie eine Datastream-Konfiguration erstellt haben. Lesen Sie die Dokumentation zum Erstellen und Konfigurieren eines Datastreams ](configure.md) und befolgen Sie dann die unten stehenden Anweisungen, um Ihrem Datastream Bot-Erkennungsfunktionen hinzuzufügen.[

Gehen Sie zur Liste der Datenspeicher und wählen Sie den Datastream aus, dem Sie die Bot-Erkennung hinzufügen möchten.

![Die Benutzeroberfläche &quot;Datastreams&quot;mit der Liste der Datenspeicher.](assets/bot-detection/datastream-list.png)

Wählen Sie auf der Seite mit den Datenspeicherdetails die Option **[!UICONTROL Bot-Erkennung]** in der rechten Leiste aus.

![Die Bot-Erkennungsoption, die in der Benutzeroberfläche von Datastreams hervorgehoben ist, wurde hervorgehoben.](assets/bot-detection/bot-detection.png)

Die Seite **[!UICONTROL Bot Detection Rules]** wird angezeigt.

![Bot-Erkennungseinstellungen auf der Seite mit den Datastream-Einstellungen.](assets/bot-detection/bot-detection-page.png)

Auf der Seite &quot;Bot-Erkennungsregeln&quot;können Sie die Bot-Erkennung mithilfe der folgenden Funktionen konfigurieren:

* Verwenden des [!DNL [IAB/ABC International Spiders and Bots List]](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/).
* Erstellen eigener Bot-Erkennungsregeln

### Verwenden der IAB/ABC International Spiders and Bots List {#iab-list}

Die [IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) ist eine Liste von Internet-Spiders und Bots, die dem Industriestandard von Drittanbietern entsprechen. Diese Liste hilft Ihnen dabei, automatisierten Traffic wie Suchmaschinen-Crawler, Überwachungstools und anderen nicht menschlichen Traffic zu identifizieren, den Sie möglicherweise nicht in Ihre Analytics-Zählungen aufnehmen möchten.

So konfigurieren Sie Ihren Datenspeicher für die Verwendung der IAB/ABC International Spiders and Bots List:

1. Schalten Sie die Option **[!UICONTROL IAB/ABC International Spiders and Bots List verwenden zur Bot-Erkennung für diesen Datastream]** um.
2. Wählen Sie **[!UICONTROL Speichern]** aus, um die Bot-Erkennungseinstellungen auf Ihren Datastream anzuwenden.

![IAB-Spider und Bot-Liste aktiviert.](assets/bot-detection/bot-detection-list.png)

### Erstellen von Bot-Erkennungsregeln {#rules}

Zusätzlich zur Verwendung der [IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) können Sie für jeden Datastream eigene Bot-Erkennungsregeln definieren.

Sie können Bot-Erkennungsregeln basierend auf **IP-Adressen** und **IP-Adressbereichen** erstellen.

Wenn Sie detailliertere Bot-Erkennungsregeln benötigen, können Sie die IP-Bedingungen mit den Anforderungen-Header-Bedingungen kombinieren. Bot-Erkennungsregeln können die folgenden Kopfzeilen verwenden:

| HTTP-Header | Beschreibung |
| --- | --- |
| `user-agent` | Ein Header, der es Servern und Netzwerkpartnern ermöglicht, die Anwendung, das Betriebssystem, den Anbieter und/oder die Version des anfragenden Benutzeragenten zu identifizieren. |
| `content-type` | Gibt den ursprünglichen Medientyp der Ressource an (vor einer für den Versand angewendeten Inhaltskodierung). |
| `referer` | Gibt die Adresse der Webseite an, von der die Ressource angefordert wurde. |
| `sec-ch-ua` | Stellt die Marke und die signifikante Version für jede mit dem Browser verknüpfte Marke in einer kommagetrennten Liste bereit. |
| `sec-ch-ua-mobile` | Gibt an, ob sich der Browser auf einem Mobilgerät befindet. Es kann auch von einem Desktop-Browser verwendet werden, um eine Voreinstellung für ein mobiles Benutzererlebnis anzugeben. |
| `sec-ch-ua-platform` | Stellt die Plattform oder das Betriebssystem bereit, auf der der Benutzeragent ausgeführt wird. Beispiel: &quot;Windows&quot;oder &quot;Android&quot;. |
| `sec-ch-ua-platform-version` | Stellt die Version des Betriebssystems bereit, auf dem der Benutzeragent ausgeführt wird. |
| `sec-ch-ua-arch` | Stellt die zugrunde liegende CPU-Architektur des Benutzeragenten bereit, z. B. ARM oder x86. |
| `sec-ch-ua-model` | Gibt das Gerätemodell an, auf dem der Browser ausgeführt wird. |
| `sec-ch-ua-bitness` | Stellt die &quot;Bitness&quot;der zugrunde liegenden CPU-Architektur des Benutzeragenten bereit. Dies ist die Größe in Bits einer Integer- oder Speicheradresse, normalerweise 64 oder 32 Bit. |
| `sec-ch-ua-wow64` | Gibt an, ob eine Benutzeragenten-Binärdatei im 32-Bit-Modus unter 64-Bit Windows ausgeführt wird. |

Gehen Sie wie folgt vor, um eine Bot-Erkennungsregel zu erstellen:

1. Wählen Sie **[!UICONTROL Neue Regel hinzufügen]** aus.

   ![Bildschirm mit den Erkennungseinstellungen für Bots mit hervorgehobener Schaltfläche Neue Regel hinzufügen](assets/bot-detection/bot-detection-new-rule.png).

2. Geben Sie im Feld **[!UICONTROL Regelname]** einen Namen für die Regel ein.

   ![Bildschirm mit der Bot-Erkennungsregel, auf dem der Regelname hervorgehoben ist.](assets/bot-detection/rule-name.png)

3. Wählen Sie **[!UICONTROL Neue IP-Bedingung hinzufügen]** aus, um eine neue IP-basierte Regel hinzuzufügen. Sie können die Regel nach IP-Adresse oder IP-Adressbereich definieren.

   ![Bildschirm mit der Bot-Erkennungsregel, auf dem das Feld für die IP-Adresse hervorgehoben ist.](assets/bot-detection/ip-address-rule.png)

   ![Bildschirm mit der Bot-Erkennungsregel, auf dem das Feld für den IP-Bereich hervorgehoben ist.](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >Die IP-Bedingungen basieren auf einem logischen `OR` -Vorgang. Eine Anfrage wird als von einem Bot kommend markiert, wenn eine der von Ihnen definierten IP-Bedingungen erfüllt ist.

4. Wenn Sie der Regel Kopfzeilenbedingungen hinzufügen möchten, wählen Sie **[!UICONTROL Kopfzeilenbedingungen hinzufügen Gruppe]** und wählen Sie dann die Kopfzeilen aus, die die Regel verwenden soll.

   ![Bildschirm mit der Bot-Erkennungsregel mit hervorgehobenen Kopfzeilenbedingungen.](assets/bot-detection/header-conditions.png)

   Fügen Sie dann die für die ausgewählte Kopfzeile zu verwendenden Bedingungen hinzu.

   ![Bildschirm mit der Bot-Erkennungsregel mit hervorgehobenen Kopfzeilenbedingungen.](assets/bot-detection/header-condition-rule.png)

5. Nachdem Sie die gewünschten Bot-Erkennungsregeln konfiguriert haben, wählen Sie **[!UICONTROL Speichern]** aus, damit die Regeln auf Ihren Datastream angewendet werden.

   ![Bildschirm mit der Bot-Erkennungsregel mit hervorgehobenen Kopfzeilenbedingungen.](assets/bot-detection/bot-detection-save.png)


## Beispiele für Bot-Erkennungsregeln {#examples}

Um Ihnen bei den ersten Schritten mit der Bot-Erkennung zu helfen, können Sie die unten beschriebenen Beispiele verwenden, um Bot-Erkennungsregeln zu erstellen.

### Bot-Erkennung basierend auf einer IP-Adresse {#one-ip}

Um alle Anforderungen einer bestimmten IP-Adresse als Bot-Traffic zu markieren, erstellen Sie eine neue Bot-Erkennungsregel, die eine einzelne IP-Adresse auswertet, wie in der Abbildung unten dargestellt.

![Bot-Erkennungsregel basierend auf einer IP-Adresse.](assets/bot-detection/bot-detection-one-ip.png)

### Bot-Erkennung basierend auf zwei IP-Adressen {#two-ip}

Um alle Anforderungen von einer der beiden IP-Adressen als Bot-Traffic zu markieren, erstellen Sie eine neue Bot-Erkennungsregel, die zwei IP-Adressen auswertet, wie in der Abbildung unten dargestellt.

![Bot-Erkennungsregel basierend auf zwei IP-Adressen.](assets/bot-detection/bot-detection-two-ips.png)

### Bot-Erkennung basierend auf einer Reihe von IP-Adressen {#range}

Um alle Anforderungen aus einer beliebigen IP-Adresse in einem bestimmten Bereich als Bot-Traffic zu markieren, erstellen Sie eine neue Bot-Erkennungsregel, die einen gesamten IP-Adressbereich auswertet, wie in der Abbildung unten dargestellt.

![Bot-Erkennungsregel basierend auf dem IP-Bereich.](assets/bot-detection/bot-detection-range.png)

### Bot-Erkennung basierend auf einer IP-Adresse und einem Anfrage-Header {#ip-header}

Um alle Anforderungen, die von einer bestimmten IP-Adresse stammen und einen bestimmten Anforderungsheader enthalten, als Bot-Traffic zu markieren, erstellen Sie eine neue Bot-Erkennungsregel, wie in der Abbildung unten dargestellt.

Diese Regel überprüft, ob die Anforderung von einer bestimmten IP-Adresse stammt und ob der `referer`-Anforderungsheader mit `www.adobe.com` beginnt.

![Bot-Erkennungsregel basierend auf IP-Adresse und Anforderungsheader.](assets/bot-detection/bot-detection-header-ip.png)

### Bot-Erkennung basierend auf mehreren Bedingungen {#multiple-conditions}

Sie können Bot-Erkennungsregeln erstellen, die auf Folgendem basieren:

* **Mehrere unterschiedliche Bedingungen**: Verschiedene Bedingungen werden als logischer `AND` Vorgang ausgewertet, d. h. die Bedingungen müssen gleichzeitig erfüllt sein, damit die Anforderung als von einem Bot stammt identifiziert werden kann.
* **Mehrere Bedingungen desselben Typs**: Bedingungen desselben Typs werden als logischer `OR` -Vorgang ausgewertet, d. h., wenn eine der Bedingungen erfüllt ist, wird die Anforderung als von einem Bot stammend identifiziert.

Die in der folgenden Abbildung dargestellte Regel identifiziert eine Bot-Origin-Anfrage, wenn die folgenden Bedingungen erfüllt sind:

Die Anfrage stammt von einer der beiden IP-Adressen, die Kopfzeile `referer` beginnt mit `www.adobe.com` und die Kopfzeile `sec-ch-ua-mobile` identifiziert die Anforderung als von einem Desktop-Browser stammt.

![Bot-Erkennungsregel basierend auf mehreren Bedingungen.](assets/bot-detection/bot-detection-multiple.png)
