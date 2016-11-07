**streamsaver** - сценарий сохранения и ретрансляции аудиопотока

##Лицензия
    Copyright (C) 2011-2016, Maxim Lihachev, <envrm@yandex.ru>

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program. If not, see <http://www.gnu.org/licenses/>.

##streamsaver
   Обработчик аудиопотоков с нарезкой их в файлы и ретрансляцией на icecast

   Сценарий принимает аудиопоток с оборудования, по UDP или TCP,
   фрагментирует его на отрезки заданной длины для последующего хранения и
   анализа, а также ретранслирует поток на сервер радиовещания icecast для
   прослушивания аудио конечным пользователем.

##streamproxy
   Проксирование аудиопотока на Icecast.

   Сценарий принимает аудиопоток с оборудования, по UDP или TCP,
   и ретранслирует поток на сервер радиовещания icecast для
   получения сигнала другими программами и прослушивания аудио конечным
   пользователем.

   Проксирование будет доступно только при задании в файле настроек опции
   <proxy>1</proxy>

##Использование
   streamsaver/streamproxy <файл настроек> - xml-файл с описанием входящего и
   выходящего потоков и правилами фрагментирования записей.

##Файл настроек
   ```xml
   <xml>
     <!-- Название канала -->
     <channel_name></channel_name>
     <!-- Описание канала -->
     <channel_descr>Тестовый_канал</channel_descr>
     <!-- Входящий поток  -->
     <stream>http://localhost:8000/stream</stream>
     <!-- Icecast для вывода -->
     <icecast>localhost:8000</icecast>
     <!-- Пароль для доступа к Icecast -->
     <password>hackme</password>
     <!-- Точка подключения канала -->
     <mountpoint>stream</mountpoint>
     <!-- Программа/канал из потока -->
     <input_channel>0:p:4098</input_channel>
  
     <!-- Команда получения сигнала -->
     <cmd>ffmpeg</cmd>
     
     <!-- Формат входного потока -->
     <input_format>mp2 -map 0:0</input_format>
     
     <!-- Директория для сохранения архивных файлов -->
     <!-- Может содержать переменную $DATA (текущую дату) -->
     <archive_dir>FILES/archive/</archive_dir>
     <!-- Длительность архивных файлов в секундах -->
     <archive_time>3600</archive_time>
     <!-- Файл журнала обработки архивных записей -->
     <archive_log>FILES/archive.log</archive_log>
     
     <!-- Директория для сохранения фрагментов на анализ -->
     <slices_dir>FILES/fragments/</slices_dir>
     <!-- Длительность фрагментов для анализа в секундах -->
     <slices_time>10</slices_time>
     <!-- Файл журнала обработки фрагментов на анализ -->
     <slices_log>FILES/fragments.log</slices_log>
     
     <!-- Префикс имени файла -->
     <filename_prefix>%Y-%m-%d_%H:%M:%S</filename_prefix>
     <!-- Расширение имени файла -->
     <filename_suffix>mp2</filename_suffix>
     
     <!-- Формат аудиофайлов -->
     <output_format>mp2</output_format>
     <!-- Битрейт аудиофайлов -->
     <audio_bitrate>256k</audio_bitrate>
     <!-- Использование streamproxy -->
     <proxy>1</proxy>
   </xml>
   ```

   При отсутствии параметра или пустом значении соответствующие флаги а
   аргументы не добавляются в итоговую команду ffmpeg. Таким образом,
   например, можно включать или отключать ведение журнала сохранения
   аудиозаписей, просто указывая или удаляя параметр archive_log.

##Версия
   1.3

