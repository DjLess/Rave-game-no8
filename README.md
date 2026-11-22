# Rave of the Circle — versión con sprites

Abre `index.html` directamente en el navegador (no necesita servidor).
Si falta la carpeta `assets/`, el juego sigue funcionando con los gráficos vectoriales originales.

## Opciones por URL
- `index.html?skin=1..4` → personaje del jugador (1 azul, 2 rosa, 3 cian, 4 café)
- `index.html?sprites=0` → desactiva los sprites (modo placeholder)

## Estructura
```
index.html
assets/
  manifest.js            ← lista de sprites y sheets que carga el juego
  players/player1..4.png ← sheets: filas idle, walk, run, jump, fall, hurt, die (celda 72x68, pies abajo-centro)
  enemies/enemies.png    ← filas alien, robot, ninja, soldier, boss (5 frames, celda 72x84)
  tiles/                 ← tile_*.png (64x64) + tile_bridge.png
  sprites/               ← sueltos por carpeta: npcs, animals, items, weapons, fx, decor, terrain, traps, extra, ui
  atlas_original/        ← el atlas completo de origen
```

## Qué sprite usa cada elemento del juego
| Elemento | Sprite |
|---|---|
| Jugador | `player1..4` (idle en cada medio beat, run al moverse, hurt al recibir daño, die en game over) |
| Compañeros de grupo / ravers perdidos | `player1..4` según el color del grupo, con brillo de ese color |
| Bouncer | enemigo `soldier` |
| Dasher | enemigo `ninja` (brilla blanco al cargar) |
| Dancer | enemigo `alien` (cambia de lado cada beat) |
| NPC Espejo | enemigo `robot` (aro cian cuando refleja) |
| Subwoofer | `barrel_big` |
| Pilar | `rock_a` |
| Bar | `desk_console` |
| DJ | `server_big` |
| DJ Bot | `npc_robot_white` |
| Multitud | `npc_*` (uno por celda, variado por posición) |
| Vinyl (coleccionable) | `coin` |
| Puerta | `crate_gold` (cerrada) / `ladder_green` (abierta) |
| Ítems: Shades / Cigarros / Drop | `shield_orange` / `canister_green` / `star` |
| Piso normal | `tile_stone_mid` y `tile_stone_navy` (alternan con el beat) |
| Piso pegajoso / resbaloso / muro | `tile_purple` / `tile_ice` / `tile_metal_b` |

## Cambiar o agregar arte
1. Reemplaza el PNG con el mismo nombre y tamaño aproximado (los sheets deben conservar el tamaño de celda).
2. Para un sprite suelto nuevo, agrégalo en `assets/manifest.js` (`images`: nombre → [ruta, ancho, alto]) y úsalo con `SPR.fit(ctx, 'nombre', x, y, tamaño)`.
3. Toda la lógica de dibujo con sprites está en el bloque `SPRITES` de `index.html` (busca `const SPR`).
