Transflow RoadEditor - vector tiles (MVT), иммерсия 1:1
==========================================================
Содержимое: tiles.json (TileJSON) + style.json (готовый стиль иммерсии) + пирамида {z}/{x}/{y}.pbf.
Слои: roads (оси, z10-13) и на z14+ ЗАПИСАННЫЕ ПРИМИТИВЫ живого рендера: pf (заливки) и pl (штрихи).
У каждой фичи: g - слой рендера (порядок наложения), c - цвет, a - альфа, w - ширина штриха в метрах.
Зебры, штрихи ГОСТ, зубья 1.13, стрелы 1.18 лежат в тайлах готовой геометрией - стиль их лишь исполняет.
В тайлах НЕТ экранных оверлеев: знаки/светофоры/подписи (это спрайты фикс. экранного размера).

БЫСТРЫЙ СТАРТ: положите папку на любой статик-хостинг, в style.json замените
https://mikesmaq.github.io/tf-roads/ на свой адрес — и style.json готов к new maplibregl.Map({ style }).

Подключение доп. слоем в существующую карту MapLibre:
  map.addSource('tf', { type: 'vector', tiles: ['https://mikesmaq.github.io/tf-roads/{z}/{x}/{y}.pbf'], minzoom: 10, maxzoom: 16 });
  дальше добавьте слои как в style.json (fill: carriageway/junctions/crossings/sidewalks/medians; line: markings, roads).

QGIS: Layer -> Add Layer -> Vector Tile Layer -> URL вида https://mikesmaq.github.io/tf-roads/{z}/{x}/{y}.pbf
Атрибуты: roads.r (класс 0..5), roads.w (ширина полотна, м), roads.tnl (1 = тоннель); k — вид элемента в визуал-слоях.
