## Test:
Мониторинг + сбор логов с помощью Ansible
Prometheus + Node Exporter
Fluentd как systemd-сервис на хосте для агрегации логов Docker-контейнеров
Grafana с преднастроенными дашбордами — Fluentd dashboard, Node Exporter Full

Быстрый старт
```
git clone https://github.com/AlbertKhassanov/test.git
cd test/
ansible-playbook playbook.yml
```
Ветка плейбука
```
.
├── playbook.yml
└── roles
    ├── docker 
    ├── fluent 
    ├── grafana 
    ├── metric 
    ├── nginx
    └── prometheus 
```
docker
```
Устанавливается docker.io  
Устанавливается docker-compose в зависимости от поставщика ОС:
https://github.com/docker/compose/releases/latest/download/docker-compose-{{ ansible_system }}-{{ ansible_architecture }}

```
fluent
```
Меняются права у /usr/lib/systemd/system/fluentd.service на пользователя и группу root  
Предустанавливается fluent-plugin-docker_metadata_filter:
  /opt/fluent/bin/fluent-gem install fluent-plugin-docker_metadata_filter  
Заменяется стандартный конфиг
```
grafana
```
Устанавливается Grafana с двумя дашбордами и уже подключённым источником данных http://localhost:9090 (Prometheus)
```
metric
```
Запускается контейнер с Node Exporter
```
nginx
```
Контейнер для проксирования порта 3000 (Grafana) на порт 80
```
prometheus
```
Установка контейнера Prometheus + добавление целей (Fluentd и Node Exporter) в конфигурацию
```
