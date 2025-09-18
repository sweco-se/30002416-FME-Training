---
description: Skriv till Excell efter en mall
---

# Övning 5

Projektledaren vill ha en Excell med en flik för de filer som inte finns i leveransmappen och att den ska följa mallen som används i uppdraget. Din uppgift är att låta FME använda befintlig mall och format för din Excell-fil.

\
Mall att använda finns i C:\FMEData2025\Data\Informationssamordnare\15\_Kontroll (1568-C1-21-06033\_mall.xlsx).&#x20;

Hur det fungerar:\
FME behöver veta vilka celler som den ska skriva till i din mall. I Excell behöver du därför definiera området i Namnhanteraren under Formler, en så kallad _Name range_. Excell-mallen vi använder har detta redan konfigurerat. Vi behöver dock konfigurera det i skriptet.

I din flikhantering, lägg till ett attribut som heter _namerange_ och för varje flik ge värdet _Filer\_i\_förteckning_, _Filer\_ej\_i\_leveransmapp_, _Filer\_ej\_i\_förteckning_ för respektive flik. Detta attribut kopplar till rätt Name range i excellen.

Lägg till en _Counter_ efter varje _AttributeCreator_ med Count Start = 2, Count Scope = Local och Output Attribute Names Count = xlsx\_row\_id. Nu har vi valt vilken rad i excellen som ska populeras.

\
För varje excell-writer feature type, ange inställningarna i properties likt nedan:

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

För _User Attributes_ vill vi lika många attribut som vi har i vår Name range, annars så hamnar data utanför mallen.&#x20;

Excell-mallen är uppbyggd med attributen nedan för _Filer i förteckning_ och _Filer ej i leveransmapp_ respektive _Filer finns ej i förteckning_.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p><em>Filer i förteckning</em> och <em>Filer ej i leveransmapp</em></p></figcaption></figure>

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption><p><em>Filer finns ej i förteckning</em></p></figcaption></figure>

I editeringen av din writer (nås via knapp likt nedan), ange inställningarna likt nedan:

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Klicka OK. Stäng Excellmall-filen (annars failar körnignen) och kör sedan skriptet.
