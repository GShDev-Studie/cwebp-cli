# cwebp-cli

![Publish node.js package](https://github.com/Yukioru/cwebp-cli/workflows/Publish%20node.js%20package/badge.svg?branch=master)
[![NPM verison](https://img.shields.io/npm/v/@yukioru/cwebp-cli)](https://www.npmjs.com/package/@yukioru/cwebp-cli)
[![GPR verison](https://img.shields.io/github/v/release/yukioru/cwebp-cli?label=gpr)](https://github.com/Yukioru/cwebp-cli/packages/207466)
![License](https://img.shields.io/github/license/yukioru/cwebp-cli)

## Язык: Русский | [Английский](https://github.com/Yukioru/cwebp-cli/blob/master/README.md)

Инструмент CLI для конвертации файлов jpg/png в webp.

Основан на [cwebp Encoder](https://developers.google.com/speed/webp/docs/cwebp)

## Как мгновенно использовать
```
npx @yukioru/cwebp-cli 
```

## Как установить
```
npm install -g @yukioru/cwebp-cli
```
```
yarn global add @yukioru/cwebp-cli
```

## Как использовать после установки
Запустите `cwebp` в вашей консоли.

## Опции
**-V, --version**
> Отобразить номер версии

**-r, --recursive**
> Рекурсивно проходить по каталогам

**-f, --files <items>**
> Файлы для конвертации, перечисленные через ','

**--lossless**
> Кодировать изображение без потерь. Для изображений с полностью прозрачной областью
> значения невидимых пикселей (R/G/B или Y/U/V) будут сохранены,
> только если используется опция -exact

**--near_lossless <int>**
> Укажите уровень предварительной обработки изображений практически без потерь.
> Этот параметр корректирует значения пикселей, чтобы улучшить сжимаемость,
> но оказывает минимальное влияние на качество изображения.
> Он запускает режим сжатия без потерь автоматически. Диапазон составляет
> от 0 (максимальная предварительная обработка) до 100 (без предварительной обработки,
> по умолчанию). Типичное значение составляет около 60. 
> Обратите внимание, что потери с -q 100 могут иногда давать лучшие результаты.

**-q, --quality <float>**
> Укажите коэффициент сжатия для каналов RGB от 0 до 100. По умолчанию установлено значение 75.
> В случае сжатия с потерями (по умолчанию) при небольшом коэффициенте создается файл меньшего размера
> с более низким качеством. Наилучшее качество достигается при использовании значения 100.
> В случае сжатия без потерь (задается параметром --lossless), небольшой коэффициент обеспечивает
> более высокую скорость сжатия, но создает файл большего размера.
> Максимальное сжатие достигается при использовании значения 100. (по умолчанию: 75)

**-z, --zip <float>**
> Включите режим сжатия без потерь с указанным уровнем от 0 до 9,
> причем уровень 0 - самый быстрый, 9 - самый медленный.
> Быстрый режим дает больший размер файла, чем медленный.
> Хорошим значением по умолчанию является -z 6. Эта опция на самом деле является
> ярлыком для некоторых предопределенных настроек качества и метода.
> Если впоследствии будут использованы опции -q или -m, то действие этой опции будет недействительным.

**--alpha_q <int>**
> Укажите коэффициент альфа-сжатия от 0 до 100.
> Сжатие без потерь альфа-канала достигается при использовании значения 100,
> а более низкие значения приводят к сжатию с потерями. По умолчанию это 100.

**--preset <string>**
> Укажите набор предварительно определенных параметров для соответствия конкретному типу исходного материала.
> Возможные значения: default, photo, picture, drawing, icon, text.
>Поскольку --preset перезаписывает значения других параметров (кроме -q),
> этот параметр предпочтительно должен появляться первым в порядке аргументов.

**-m, --method <int>**
> Укажите метод сжатия. Этот параметр контролирует отношение
> между скоростью кодирования и размером и качеством сжатого файла.
> Возможные значения находятся в диапазоне от 0 до 6. Значение по умолчанию равно 4.
> При использовании более высоких значений кодер будет тратить больше времени на проверку
> дополнительных возможностей кодирования и определит прирост качества.
> Меньшее значение может привести к ускорению обработки за счет увеличения
> размера файла и снижения качества сжатия.

**--resize <width/height>**
> Изменение размера источника в прямоугольник с размером width х height.
> Если один из параметров ширины или высоты (но не оба) равен 0,
> значение будет рассчитано с сохранением соотношения сторон.

**--crop <x_position/y_position/width/height>**
> Обрежьте источник в прямоугольник с верхним левым углом в координатах (x_position, y_position)
> и размером width x height. Область обрезки не должна выходить за рамки исходного изображения.

**-mt, --multithread**
> Использовать многопоточность для кодирования, если возможно.

**--low_memory**
> Сократите использование памяти кодированием с потерями, сохранив изображение
> сжатое в 4 раза (как правило). Это замедлит кодирование,
> а выходные данные будут немного отличаться по размеру и искажениям.
> Этот флаг действует только для методов 3 и выше и по умолчанию отключен.
> Обратите внимание, что отключение этого флага будет иметь некоторые побочные эффекты для
> битового потока: он вызывает определенные функции битового потока, такие как количество разделов
> (принудительно устанавливается в 1). Обратите внимание, что более подробный отчет о размере потока
> битов выводится в cwebp при использовании этой опции.

**--size <int>**
> Укажите целевой размер (в байтах), чтобы попытаться достичь сжатого вывода.
> Компрессор выполнит несколько проходов частичного кодирования, чтобы максимально
> приблизиться к этой цели. Если используются оба параметра --size и --psnr,
> значение --size будет иметь преимущественную силу.

**--psnr <float>**
> Укажите целевой PSNR (в дБ), чтобы попытаться достичь сжатого вывода.
> Компрессор выполнит несколько проходов частичного кодирования,
> чтобы максимально приблизиться к этой цели.
> Если используются оба параметра --size и --psnr, значение --size будет иметь преимущественную силу.

**--pass <int>**
> Установите максимальное количество проходов для использования во время последовательного разделения,
> используемой параметрами --size или --psnr. Максимальное значение равно 10,
> по умолчанию равно 1. Если были использованы опции --size или --psnr,
> но не указан --pass, будет использовано значение по умолчанию '6' проходов.

**-af, --autofilter**
> Включает автофильтр. Этот алгоритм будет тратить дополнительное время на
> оптимизацию силы фильтрации для достижения сбалансированного качества.

**--jpeg_like**
> Изменяет внутреннее сопоставление параметров, чтобы лучше соответствовать
> ожидаемому размеру сжатия JPEG. Этот флаг обычно создает выходной файл,
> размер которого аналогичен его эквиваленту в формате JPEG (для того же параметра -q),
> но с меньшим визуальным искажением.

**--filter <int>**
> Укажите силу фильтра удаления блочности от 0 (без фильтрации) до 100 (максимальная фильтрация).
> Значение 0 отключит любую фильтрацию. Более высокое значение увеличит силу процесса фильтрации,
> применяемого после декодирования изображения. Чем выше значение,
> тем более плавным будет изображение. Типичные значения обычно находятся в диапазоне от 20 до 50.

**--sharpness <int>**
> Укажите резкость фильтрации (если используется).
> Диапазон составляет от 0 (самый резкий) до 7 (наименее резкий). По умолчанию 0.

**--strong**
> Используйте сильную фильтрацию (если фильтрация используется с опцией --filter).
> Сильная фильтрация включена по умолчанию.

**--nostrong**
> Отключите сильную фильтрацию (если фильтрация используется с опцией --filter)
> и используйте вместо неё простую фильтрацию.

**--sharp_yuv**
> При необходимости используйте более точное и четкое преобразование RGB->YUV.
> Обратите внимание, что этот процесс медленнее, чем 'быстрое' преобразование RGB->YUV по умолчанию.

**--sns <int>**
> Укажите амплитуду пространственного формирования шума. Пространственное формирование шума
> (или sns) относится к общему набору встроенных алгоритмов, используемых для определения,
> в какой области изображения следует использовать относительно меньше битов, а где еще лучше передавать
> эти биты. Возможный диапазон варьируется от 0 (алгоритм отключен) до 100 (максимальный эффект).
> Значение по умолчанию составляет 50.

**--segments <int>**
> Измените количество разделов, используемых при сегментации алгоритма sns.
> Сегменты должны быть в диапазоне от 1 до 4. Значение по умолчанию равно 4.
> Этот параметр не действует для методов 3 и выше, если не используется --low_memory.

**--partition_limit <int>**
> Ухудшайте качество, ограничивая количество битов, используемых некоторыми макроблоками.
> Диапазон составляет от 0 (без ухудшения, по умолчанию) до 100 (полное ухудшение).
> Наилучшие значения обычно составляют 30-70 для изображений среднего размера.
> В формате VP8 контрольный раздел имеет ограничение в 512 КБ и
> используется для хранения следующей информации: пропущен ли макроблок, к какому
> сегменту он принадлежит, закодирован ли он в режиме интра 4х4 или интра 16х16, и наконец,
> режимы прогнозирования для использования для каждого из подблоков. Для очень большого изображения
> 512 Кбайт оставляет место только для нескольких бит на макроблок 16х16.
> Абсолютный минимум составляет 4 бита на макроблок. Информация о пропуске,
> сегменте и режиме может использовать почти все эти 4 бита (хотя случай маловероятен),
> что проблематично для очень больших изображений. Коэффициент partition_limit контролирует,
> как часто будет использоваться наиболее дорогостоящий режим (внутри 4х4).
> Это полезно в случае достижения предела 512 КБ и отображения следующего сообщения:
> Error code: 6 (PARTITION0_OVERFLOW: Partition #0 is too big to fit 512k).
> Если использование --partition_limit недостаточно для удовлетворения ограничения 512 Кб,
> следует использовать меньше сегментов, чтобы сохранить больше битов заголовка на макроблок.
> Смотрите опцию --segments.

**-v, --verbose**
> Выводить дополнительную информацию (время кодирования).

**--print_psnr**
> Вычислить и вывести среднее значение PSNR (отношение пикового сигнала к шуму).

**--print_ssim**
> Вычислить и вывести средний SSIM (показатель структурного сходства, см.
> http://en.wikipedia.org/wiki/SSIM для получения дополнительной информации).

**--print_lsim**
> Вычислить и вывести метрику локального сходства (сумма наименьшей ошибки среди
> соседей по расположению рядом расположенных пикселей).

**--progress**
> Отчет о прогрессе кодирования в процентах.

**--quiet**
> Не выводить ничего.

**--short**
> Выводить только краткую информацию (размер выходного файла и PSNR) для целей тестирования.

**--map <int>**
> Вывести дополнительную ASCII-карту кодирования информации.
> Возможные значения карты находятся в диапазоне от 1 до 6. Это только для облегчения отладки.

**-s, --specify <width/height>**
> Укажите, что входной файл фактически состоит из необработанных выборок Y'CbCr
> в соответствии с рекомендацией ITU-R BT.601 в линейном формате 4:2:0.
> Плоскость яркости имеет размер width x height.

**--pre <int>**
> Укажите некоторые этапы предварительной обработки.
> Использование значения 2 вызовет зависящее от качества псевдослучайное
> сглаживание во время преобразования RGBA-> YUVA (только сжатие с потерями).

**--alpha_filter <string>**
> Укажите метод прогнозирующей фильтрации для альфа-плоскости. Один из none, fast или best,
> в порядке увеличения сложности и медленности. По умолчанию это fast. Внутри альфа-фильтрация
> выполняется с использованием четырех возможных предсказаний (none, horizontal, vertical, gradient).
> Лучший режим будет пробовать каждый режим по очереди и выбирать тот, который дает меньший размер.
> Быстрый режим просто попытается сформировать априорное предположение, не тестируя все режимы.

**--alpha_method <int>**
> Укажите алгоритм, используемый для альфа-сжатия: 0 или 1.
> Алгоритм 0 означает отсутствие сжатия, 1 использует формат сжатия без потерь WebP. По умолчанию это 1.

**--exact**
> Сохраните значения RGB в прозрачной области. По умолчанию выключено, чтобы помочь сжимаемости.

**--blend_alpha <int>**
> Эта опция смешивает альфа-канал (если есть) с источником, используя цвет фона,
> указанный в шестнадцатеричном виде как 0xrrggbb.
> После этого альфа-канал сбрасывается до непрозрачного значения 255.

**--noalpha**
> Использование этого параметра приведет к отключению альфа-канала.

**--hint <string>**
> Укажите подсказку о типе входного изображения. Возможные значения: photo, picture или graph.

**--metadata <string>**
> Список метаданных, разделенных запятыми, для копирования из входных данных в выходные,
> если они есть. Допустимые значения: all, none, exif, icc, xmp. По умолчанию none.
> Обратите внимание, что каждый формат ввода может не поддерживать все комбинации.

**--noasm**
> Отключить все оптимизации сборки.

**-h, --help**
> Показать справку
