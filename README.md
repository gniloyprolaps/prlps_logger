 `pip install prlps-logger`

пример использования:

```python
# указываем путь до файла с логами куда будет все записываться:
from pathlib import Path
log_file = Path(__file__).parent / 'my_logs.log'

# создание экземпляра класса с нужным уровнем логгирования:
logger = GetLog(log_file, 'DEBUG')
# уровень логгирования можно не указывать, тогда по умолчанию будет 'WARN':
# logger = Logger(log_file)

logger.warn('текст')
logger.error('текст')
logger.info('текст')
logger.crit('текст')
logger.event('текст')

try:
    my_iq = ((0 + 0) * 0) ** 0 / 0
except Exception as e:
    # тут твоя какая-то обработка исключения...
    logger.error(f'ты больной?\n{e}') # логгирование

# посмотрим как логгируются не обработанные исключения:
# my_iq = ((0 + 0) * 0) ** 0 / 0

# лог (только созданный этим логгером) можно передать в виде html для удобного просмотра или вывода куда-то, например на страницу через fastapi и т.п.
html_log = logger.log_to_html()  # создаст html текущего лога, аналогично вызову logger.log_to_html(log_file)
# или создать html с указанием пути до конкретного лог-файла, не обязательно текущего
# html_log = logger.log_to_html(log_file)  # для текущего лога
# html_log = logger.log_to_html('/path/to/file.log.3')  # для какого-то другого лог-файла, например после ротации логов
# метод возвращает код html, можно записать в файл или вернуть как HTMLResponse:
print(html_log)
```
