---
title: edgeDomain
description: Bestimmen Sie die Stamm-Domain, an die Sie Daten senden möchten.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# `edgeDomain`

Mit der Eigenschaft `edgeDomain` können Sie die Domain ändern, an die die Web-SDK Daten sendet. Diese Eigenschaft wird häufig von Organisationen verwendet, die [Erstanbieter-Cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de) verwenden. Daten werden an die unternehmenseigene Domain gesendet. Anschließend werden diese Daten von einem CNAME-Eintrag an Adobe weitergeleitet.

Der Wert, den Sie für die `edgeDomain` verwenden, hängt von Ihrer Teilnahme am [Adobe-verwalteten Zertifikatsprogramm ab](https://experienceleague.adobe.com/de/docs/core-services/interface/data-collection/adobe-managed-cert):

**Wenn Ihr Unternehmen am Adobe-Managed Certificate Program teilnimmt** setzen Sie den Wert auf die Erstanbieter-Domain, die beim Einrichten des Zertifikats ausgewählt wurde. Normalerweise ist dieser Wert eine Subdomain, die Ihrem Unternehmen gehört. Beispiel: `data.example.com`. CNAME-Datensätze in Ihrem Unternehmen leiten diese Daten an Adobe weiter.

**Wenn Sie nicht am Zertifikatprogramm teilnehmen** setzen Sie den Wert auf eine Subdomain von `data.adobedc.net`. Adobe empfiehlt, aus Konsistenzgründen die Unternehmens-ID Ihres Unternehmens zu verwenden. Beispiel: `example.data.adobedc.net`. Gehen Sie wie folgt vor, um Ihre Unternehmens-ID zu ermitteln:

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Drücken Sie an einer beliebigen Stelle in der Experience Cloud-Benutzeroberfläche `[Cmd]` + `[I]` (iOS) oder `[Ctrl]` + `[I]` (Windows).
1. Ein **[!UICONTROL User data debugger]** wird angezeigt. Wählen Sie die Registerkarte **[!UICONTROL Assigned orgs]** aus.
1. Erweitern Sie die gewünschte IMS-Organisation.
1. Suchen Sie das Feld **[!UICONTROL Tenant]** . Dieser Wert ist die empfohlene Subdomain von `data.adobedc.net`.

Legen Sie die `edgeDomain` beim Ausführen des `configure`-Befehls fest. Wenn Sie diese Eigenschaft beim Konfigurieren der SDK weglassen, wird sie standardmäßig auf `edge.adobedc.net` gesetzt. Der Standardwert ist zwar akzeptabel, Adobe erachtet es jedoch als Best Practice, einen organisationsspezifischen Wert festzulegen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## Edge-Domain unter Verwendung der Web-SDK-Tag-Erweiterung

Die Tag-Erweiterung, die dieser Eigenschaft entspricht, ist das **[!UICONTROL Edge domain]** Feld unter [Konfigurationseinstellungen der SDK-Instanz](/help/tags/extensions/client/web-sdk/configure/general.md) beim Konfigurieren der Erweiterung.
