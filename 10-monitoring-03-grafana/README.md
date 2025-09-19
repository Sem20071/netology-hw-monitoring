### Домашнее задание к занятию 14 «Средство визуализации Grafana»

## Обязательные задания
# Задание 1
1. Используя директорию help внутри этого домашнего задания, запустите связку prometheus-grafana.
2. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
3. Подключите поднятый вами prometheus, как источник данных.
4. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

# Задание 2
Изучите самостоятельно ресурсы:

1. PromQL tutorial for beginners and humans.
2. Understanding Machine CPU usage.
3. Introduction to PromQL, the Prometheus query language.
   
Создайте Dashboard и в ней создайте Panels:
- утилизация CPU для nodeexporter (в процентах, 100-idle);
- CPULA 1/5/15;
- количество свободной оперативной памяти;
- количество места на файловой системе.
Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

# Задание 3
1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
2. В качестве решения задания приведите скриншот вашей итоговой Dashboard.

# Задание 4
1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
2. В качестве решения задания приведите листинг этого файла.

Ответ:
# Задание 1
![Скриншот задание 1](https://github.com/Sem20071/netology-hw-monitoring/blob/main/10-monitoring-03-grafana/images/dz-02-grafana-01.png)

# Задание 2
![Скриншот задание 2](https://github.com/Sem20071/netology-hw-monitoring/blob/main/10-monitoring-03-grafana/images/dz-02-grafana-02.png)

promql-запросы:
1. утилизация CPU для nodeexporter (в процентах, 100-idle);
   (1 - rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100   -  Утилизация с разбивкой по ядрам
2. CPULA 1/5/15;
   {__name__=~"node_load(1|5|15)"} - Средняя загруза за 1, 5 , 15 минут на отдном графике.
3. количество свободной оперативной памяти;
   node_memory_MemFree_bytes / 1024 / 1024 / 1024  - Свободная память в Gb. Для меня проще в понимании приводит в Gb делением. 
4. количество места на файловой системе.
   node_filesystem_avail_bytes{mountpoint="/"} / 1073741824 - Свободное место на файловой системе в Gb.

# Задание 3
1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
2. В качестве решения задания приведите скриншот вашей итоговой Dashboard.
![Скриншот задание 3](https://github.com/Sem20071/netology-hw-monitoring/blob/main/10-monitoring-03-grafana/images/dz-02-grafana-03.png)

# Задание 4
https://github.com/Sem20071/netology-hw-monitoring/blob/main/10-monitoring-03-grafana/my_dashboard.json
