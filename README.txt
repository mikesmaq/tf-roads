Transflow RoadEditor - vector tiles (MVT), иммерсия 1:1
==========================================================
Содержимое: tiles.json (TileJSON) + style.json (готовый стиль иммерсии) + пирамида {z}/{x}/{y}.pbf.
ЗУМЫ: выпечено z9-z16, показывается z9-z24 (выше 16 MapLibre растягивает тайл сам, файлов не добавляется).
СЛОИ:
  roads  - оси сегментов С АТРИБУТАМИ, на ВСЕХ зумах: id, hw (класс OSM), name, r (ранг 0..5),
           w (ширина полотна, м), lanes/lanes_f/lanes_b, speed (км/ч), oneway, surface, brg, tnl, lit,
           cap_h - РАСЧЁТНАЯ пропускная способность (справочная ёмкость полосы x полосы).
  nodes  - узлы (подходов >= 3): id, arms, kind (tee/cross/complex), signal, control, cap_h (расчёт).
  paint_fill / paint_line - ЗАПИСАННЫЕ ПРИМИТИВЫ живого рендера (z14+): g - слой рендера (порядок
           наложения), c - цвет, a - альфа, w - ширина штриха в МЕТРАХ.
Зебры, штрихи ГОСТ, зубья 1.13, стрелы 1.18 лежат в тайлах готовой геометрией - стиль их лишь исполняет.
ВЫПЕКАЮТСЯ ТОЛЬКО ВИДИМЫЕ СЛОИ: что выключено в панели "Слои" приложения, того нет и в тайлах.
ЗНАКИ ТСОДД: слой signs (точки установки; ic - иконка, c - код ГОСТ, r - разворот щитка, k - ярус стойки)
+ спрайт sprite.png/sprite.json (нарисован тем же набором, что на карте и в инспекторе). Показ с z15,
размер экранный (знак - билборд, он не масштабируется с картой).
СВЕТОФОРЫ: слой traffic_signals (ic - иконка конфигурации прибора, t - код по ГОСТ Р 52282, r - разворот лица,
dup=1 - дублёр); иконку рисует тот же painter, что и карта (число/вид секций, опора, пропорции).

БЫСТРЫЙ СТАРТ: положите папку на любой статик-хостинг, в style.json замените
https://mikesmaq.github.io/tf-roads/ на свой адрес — и style.json готов к new maplibregl.Map({ style }).

Подключение доп. слоем в существующую карту MapLibre:
  map.addSource('tf', { type: 'vector', tiles: ['https://mikesmaq.github.io/tf-roads/{z}/{x}/{y}.pbf'], minzoom: 9, maxzoom: 16 });
  дальше добавьте слои как в style.json (fill/line по paint_fill/paint_line, symbol по signs/traffic_signals).

QGIS: Layer -> Add Layer -> Vector Tile Layer -> URL вида https://mikesmaq.github.io/tf-roads/{z}/{x}/{y}.pbf
Полный перечень полей — в tiles.json (vector_layers[].fields).
