# Домашнее задание к занятию 11.3. «ELK» - `Елена Махота`

- [Ответ к Заданию 1](#1)
- [Ответ к Заданию 2](#2)
- [Ответ к Заданию 3](#3)
- [Ответ к Заданию 4](#4)
- [Ответ к Заданию 5*](#5)


---

### Задание 1. Elasticsearch 

Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный. 

*Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name*.

### *<a name = "1"> Ответ к Заданию 1 </a>

Установка Elasticsearch на Debian 11 c зеркала Yandex: 

```bash
apt update && apt install gnupg apt-transport-https #--зависимости
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add - #--добавляем gpg-ключ
echo "deb https://mirror.yandex.ru/mirrors/elastic/8/ stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.list #--добавляем репозиторий в apt
sudo apt update 
sudo apt-get install elasticsearch #--устанавливаем elastic
systemctl daemon-reload #--обновляем конфиги systemd
systemctl enable elasticsearch.service #--включаем юнит
systemctl start elasticsearch.service
```

Настройки конфигурации в `/etc/elasticsearch/elasticsearch.yml`
```bash
cluster.name: makhota-cluster <--меняем имя кластера
node.name: node-1 <--меняем название ноды, если нужно
path.data: /var/lib/elasticsearch <-где храним данные
path.logs: /var/log/elasticsearch <--куда пишем логи
network.host: 0.0.0.0 <--какой ip слушает хост
```

Перезапускаем Elasticsearch

```bash
sudo systemctl restart elasticsearch.service
```
![elasticsearch_conf](img/img%202023-04-10%20213948.png)

---

### Задание 2. Kibana

Установите и запустите Kibana.

*Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty*.

### *<a name = "2"> Ответ к Заданию 2 </a>

Установка Kibana на Debian 11: 
```bash 
sudo apt install kibana #--установка
sudo systemctl daemon-reload #--обновляем конфиги systemd
sudo systemctl enable kibana.service #--включаем юнит
sudo systemctl start kibana.service #--запускаем сервис
```

Редактируем конфиг `/etc/kibana/kibana.yml`

``` bash
server.host: "0.0.0.0" <--открываем интерфейс в мир
```

```bash
sudo systemctl restart kibana
```

![kibana](img/img%202023-04-10%20223912.png)

---

### Задание 3. Logstash

Установите и запустите Logstash и Nginx. С помощью Logstash отправьте access-лог Nginx в Elasticsearch. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx.*

### *<a name = "3"> Ответ к Заданию 3 </a>


---

### Задание 4. Filebeat. 

Установите и запустите Filebeat. Переключите поставку логов Nginx с Logstash на Filebeat. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.*

### *<a name = "4"> Ответ к Заданию 4 </a>


---

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 5*. Доставка данных 

Настройте поставку лога в Elasticsearch через Logstash и Filebeat любого другого сервиса , но не Nginx. 
Для этого лог должен писаться на файловую систему, Logstash должен корректно его распарсить и разложить на поля. 

*Приведите скриншот интерфейса Kibana, на котором будет виден этот лог и напишите лог какого приложения отправляется.*

### *<a name = "5"> Ответ к Заданию 5* </a>


