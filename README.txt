Transflow RoadEditor - vector tiles (MVT), визуал иммерсии
==========================================================
Содержимое: tiles.json (TileJSON) + style.json (готовый стиль иммерсии) + пирамида {z}/{x}/{y}.pbf.
Слои: roads (оси, z10-13) и визуал Pixi-рендера на z14+: carriageway и junctions (полотно),
markings (разметка), crossings (переходы), sidewalks (тротуары), medians (разделительные).

БЫСТРЫЙ СТАРТ: положите папку на любой статик-хостинг, в style.json замените
https://ВАШ_ХОСТ/ПУТЬ/ на свой адрес — и style.json готов к new maplibregl.Map({ style }).

Подключение доп. слоем в существующую карту MapLibre:
  map.addSource('tf', { type: 'vector', tiles: ['https://ВАШ_ХОСТ/ПУТЬ/{z}/{x}/{y}.pbf'], minzoom: 10, maxzoom: 16 });
  дальше добавьте слои как в style.json (fill: carriageway/junctions/crossings/sidewalks/medians; line: markings, roads).

QGIS: Layer -> Add Layer -> Vector Tile Layer -> URL вида https://ВАШ_ХОСТ/ПУТЬ/{z}/{x}/{y}.pbf
Атрибуты: roads.r (класс 0..5), roads.w (ширина полотна, м), roads.tnl (1 = тоннель); k — вид элемента в визуал-слоях.
