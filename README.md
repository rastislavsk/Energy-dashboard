# Energy dashboard

Statický dashboard domácej energetiky (PV / TČ / TUV / EV).

- `index.html` — dashboard, načítava dáta z `data.json`
- `data.json` — dáta vyexportované z Google Sheetu „EV PV TC"
- `manifest.webmanifest`, `sw.js`, `icon-*.png` — PWA (inštalácia na mobil, offline režim)

Publikované cez GitHub Pages. Pri aktualizácii stačí prepísať `data.json`.

## Inštalácia na mobil

Dashboard je PWA — dá sa nainštalovať ako samostatná appka (vlastná ikona,
celá obrazovka bez adresného riadku, funguje aj offline z poslednej videnej verzie).

**Android (Chrome):** otvor stránku → tlačidlo **Nainštalovať appku** v hlavičke,
alebo menu ⋮ → *Pridať na plochu / Nainštalovať aplikáciu*.

**iPhone / iPad (Safari):** otvor stránku → **Zdieľať** (ikona so šípkou nahor) →
*Pridať na plochu*. iOS nemá vlastný inštalačný dialóg, takže tlačidlo v hlavičke
sa tam nezobrazí — ale výsledok je rovnaký: appka sa spustí na celú obrazovku.
Musí to byť Safari, cez Chrome na iOS to nefunguje.

Podmienka pre oboje: stránka musí bežať cez HTTPS (GitHub Pages áno).

## Údržba

- Dáta sa naťahujú zo siete a cache je len záloha pre offline — po zmene `data.json`
  sa nová verzia ukáže hneď po znovuotvorení appky.
- Ak pribudne nový súbor, ktorý má fungovať offline, dopíš ho do zoznamu `PRECACHE`
  v `sw.js` a zvýš `CACHE_VERSION` (napr. `v1` → `v2`), aby sa starý cache vymazal.
- **`id` v manifeste nikdy nedávaj ako `"./"`.** Vyzerá to logicky, ale podľa
  špecifikácie sa `id` nevyhodnocuje voči adresáru manifestu, ale voči *doméne* —
  takže `"./"` skončí ako `https://rastislavsk.github.io/` pre každú appku na tejto
  doméne. Chrome potom dve rôzne appky považuje za jednu a druhá sa nedá nainštalovať.
  Preto je tu natvrdo `"id": "/Energy-dashboard/"`.
