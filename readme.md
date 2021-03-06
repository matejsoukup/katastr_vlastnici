# Katastr vlastníci

Nástroj pro doplnění údajů o vlastnících pozemků.

## Popis

Nástroj používá bezplatný přístup k informacím z katastru přes http://nahlizenidokn.cuzk.cz/MapaIdentifikace.aspx?l=KN&x=?&y=? , který používají mimojiné mapy.cz. Přístupový bod dovoluje jen několik desítek dotazů za hodinu (není určený pro hromadné tahání dat), proto je tento postup vhodný jen pro menší projekty.

## Postup

1. Z http://atom.cuzk.cz/ stáhneme "Katastrální mapa pro katastrální území X" ve formátu SHP a souřadnicovém systému 5514.
2. V QGISu otevřeme *PARCELY_KN_DEF.shp*, vybereme definiční body parcel, které nás zajímají, a uložíme je v odděleném souboru ve formátu geojson a souřadnicovém systému 5514.
3. Otevřeme python script *katastr_vlastnici.py* a do proměnné src doplníme cestu ke zdrojovému geojsonu z předchozího kroku.
4. Můžeme změnit i cesty k výstupním souborům.

Pokud vše proběhne hladce, vytvoří se nám nový geojson se novými detaily o parcelách + shrnutí vlastnických práv a práv na hospodaření. Detailní struktura práv se ukládá do json a csv vedle.
Pokud v průběhu zpracování dejde k naplnění limitu, vyčkejte aspoň hodinu, výstupní CSV z minulého běhu označte jako vstupní (vyhnete se tak znovu řešení již zjištěných parcel). Výstupní JSON a CSV podrobné struktury vlastníků se však přemaže, proto při opakovaném běhu zálohujete a posléze ručně slučte.
Přístupový bod používá zaokrouhlení na metry. U malých a úzkých pozemků se může stát, že po zaokrohlení se nástroj netrefí do správného pozemku. Na to je myšleno - pokud se netrefí, zkouší se okolních 8 pozemků. Přesto se může stát, že ani jeden z nich nebude ležet na správné parcely a inforamce o ni bude nutné doplnit ručně jiným způsobem.

 Autor tohoto nástroje nenese žádné právní následky plynoucí z použití nástroje.
