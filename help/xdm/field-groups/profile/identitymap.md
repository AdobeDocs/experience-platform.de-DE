---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemata;identityMap;identität zuordnen;Identität zuordnen;Schema-Design;map;Map;Vereinigungsschema;Vereinigung
title: Schemafeldgruppe für IdentityMap
description: Erfahren Sie mehr über die Klasse „XDM Individual Profile“.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: cfa3e5c6811f148376a2d2012f5687be6fad2299
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 63%

---

# Schemafeldgruppe für [!UICONTROL IdentityMap] 

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL IdentityMap] ist eine standardmäßige Schemafeldgruppe für die Klasse [[!UICONTROL XDM ExperienceEvent] ](../../classes/experienceevent.md) und eine kompatible Feldergruppe für die Klasse [[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md). Die Feldergruppe stellt ein einzelnes Zuordnungsfeld bereit, das eine Reihe von Benutzeridentitäten enthält, die vom Namespace angegeben wurden.

![Ein Diagramm der Schemafeldgruppe [!UICONTROL IdentityMap]](../../images/field-groups/identitymap.png)

Siehe den Abschnitt zu Identitätszuordnungen in [Grundlagen der Schemakomposition](../../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall, einschließlich der Vor- und Nachteile.

**Beispiel**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Weitere Informationen zur Feldergruppe finden Sie unter [vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) im öffentlichen XDM-Repository.
