# LumoraSMP-Core

Plugin inti gabungan buat Lumora SMP (Folia 1.21.11) — 16 modul.

## Struktur folder — MODULAR (gaya EssentialsX)
```
plugins/LumoraSMPCore/
├── spawn/config.yml
├── home/config.yml + homes.yml
├── rtp/config.yml
├── mobspawn/config.yml
├── rankshop/config.yml
├── joinmessages/config.yml
├── motd/config.yml
├── maintenance/config.yml
├── clearlag/config.yml
├── worlds/config.yml
├── shop/config.yml
├── leaderboard/config.yml
├── event/config.yml
├── arena/config.yml + data/<nama>.snapshot
├── duel/config.yml
└── billford/config.yml
```

## 16 Modul
1. **Mob Spawn Radius** — `/mobradius`
2. **RankShop** — `/rankshop` (currency configurable via PlaceholderAPI)
3. **Spawn** — `/spawn`, `/setspawn`
4. **Home** — `/home`, `/sethome`, `/delhome`, `/homes`
5. **RTP** — `/rtp`
6. **Join/Leave Message** — otomatis
7. **MOTD** — otomatis (server list ping)
8. **Maintenance Mode** — `/maintenance <on|off|status>`
9. **Clearlag** — otomatis + `/clearlag`
10. **Worlds (Multiverse-lite)** — `/world`, `/worldadmin`
11. **Shop** — `/shop` (klik kiri beli, klik kanan jual 1 stack)
12. **Leaderboard** — `/leaderboard <board>` (top player by placeholder)
13. **Event** — `/event [nama]`, `/setevent <nama>`
14. **Arena Regen/Reset** — `/arena <setpos1|setpos2|save|reset> <nama>`
15. **Duel** — `/duel <player>`, `/duel accept`, `/duel deny`
16. **Billford** — `/billford` (barter item-ke-item, gaya DonutSMP)

## ⚠️ Plugin lama yang jadi DOUBLE — matiin/uninstall salah satu
| Modul LumoraSMP-Core | Plugin lama |
|---|---|
| Mob Spawn Radius | PerfToggleMobSpawning |
| RTP | CoderRTP |
| Spawn | DonutSpawn |
| Home | DonutHomes |
| Shop | DonutShop |
| Billford | DonutBillford |
| Clearlag | Clearlag.jar, ClearLagTimer.jar |
| Worlds | Multiverse-core (kalau cuma butuh list/tp) |
| Leaderboard | ajLeaderboards |

## Sengaja TIDAK digabung
- **Premium/cracked**: MMOItems-Bypassed, MythicMobs-Bypassed, ItemsAdder,
  BankPlus, PyroFishingPro, GCore, MagicCosmetics, ModelEngine, CustomDrops.
- **Library, bukan fitur**: CMILib, PyroLib, LoneLibs, MythicLib, nightcore, SkQuery.
- **Sistem besar / redundant**: Jobs, Shopkeepers, AureliumSkills,
  BetterTeams (udah ada DonutTeams), GSit, LevelledMobs.
- **Sudah ada & jalan bagus**: sisa Donut suite, GrimAC (anticheat).
- **Gak mungkin jadi plugin**: Anti-DDoS (level jaringan, bukan software).

## Cara compile
```bash
mvn clean package
```
Hasil `.jar` di `target/lumorasmp-core-1.0.0.jar`.

## WAJIB dicek/disesuaikan dev sebelum production
1. Versi `paper-api` di `pom.xml` disesuaikan Folia 1.21.11.
2. `deduct-command`/`add-command` di `rankshop/config.yml` & `shop/config.yml`
   disesuaikan currency asli (DonutShards/dll).
3. Nama rank di command LuckPerms harus sama persis `/lp listgroups`.
4. **ClearLagTask** & **ArenaManager** — operasi iterasi/reset block/entity
   masih pola sederhana (sync, satu kali jalan). WAJIB dioptimasi buat
   Folia (region scheduler) dan/atau dipecah per-tick kalau areanya besar,
   biar gak nge-freeze server.
5. **WorldCommand** create world itu operasi berat — sebaiknya dipindah
   ke cara yang gak blocking main thread.
6. **DuelManager/BillfordListener** — validasi tambahan (misal player
   masih bisa buka inventory pas death screen, dsb) perlu dites langsung.
7. Testing semua modul di server sebelum dipakai player asli.

## Progress
✅ Semua 16 modul dari list awal (9 fitur EcoCPvP + tambahan dari
plugins.zip yang masuk akal digabung) udah ada kerangka kodenya.
Belum pernah di-compile & dites di server beneran — WAJIB dilakuin
sebelum production.
