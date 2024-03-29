# Fab Lab Liepāja Dokumentācija

Dokumentācijas risinājums Fab Lab Liepāja iekārtām. Kā lietot iekārtas? Šeit ir dokumentācija. Laipni lūgti.

Šis risinājums ir izstrādāts izmantojot [mkdocs.org](https://www.mkdocs.org) pieeju. Šajā repositorijā ir tikai izejas kods, kurš tiek pārveidots web lapas formā automātiski. 

Saturs tiek rakstīts [Markdown](https://yakworks.github.io/docmark/cheat-sheet/) formā. Markdown ir vienkāršots standarts strukturēta tīrā tekstā balstīta satura veidošanai.

Saturs atrodas [docs](./docs) mapē. Satura failus ar paplašinājumu `.md` var atvērt un rediģēt GitHub iebūvētajā redaktorā.

Pēc rediģēšanas ir ieteicams aizpildīt `commit message` lauku, lai ilgtermiņā varētu gūt pārskatu, kā saturs ir ticis pilnveidots vai mainījies un kurš to ir darījis.

## Attēlu sagatavošana

Visus attēlus vēlams sagatavot `1920x1080px` izmērā (`dpi` nav svarīgs) un saglabāt `jpg` formā ar kvalitātes vērtību `65-75` robežās.

## Video kodēšana

Var izmantot jebkuru video kodēšanas programmu, bet mēs iesakam ffmpeg, jo tad ir iespējams pēc iespējas tuvāk panākt vēlamos video parametrus. Tā kā visi video ir daļa no mājas lapas, tos ir vēlams saspiest pēc iespējas mazākus, saglabājot pienācīgu kvalitāti. Īsumā vēlamie parametri ir sekojoši.

- Izmērs: `1280x720px`
- Kadru skaits sekundē: `25fps`
- Faila formāts: `.mp4`
- Kodējums: `H.264`
- Skaņas celiņa kodējums: `AAC`
- Skaņas celiņa bitreits: `128k`

**Parastā**
```
ffmpeg -i input.mp4 -vf "scale=1280:720,setsar=1:1, fps=25" -c:v libx264 -crf 30 -preset slow -filter:a loudnorm -c:a aac -b:a 128k output.mp4
```

**Paātrinošā**
```
ffmpeg -i input.mp4 -vf "scale=1280:720,setsar=1:1, setpts=0.5*PTS, fps=25" -c:v libx264 -crf 30 -preset slow -filter:a loudnorm -c:a aac -b:a 128k output.mp4
```

**Bezskaņas**
```
ffmpeg -i input.mp4 -vf "scale=1280:720,setsar=1:1, setpts=0.5*PTS, fps=25" -c:v libx264 -crf 30 -preset slow -an output.mp4
```

Mazāka izmēra failam iestatīt augstāku `crf` parametru. Tas samazina video kvalitāti uz faila izmēra rēķina.
