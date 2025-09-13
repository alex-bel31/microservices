# Микросервисы: подходы

### Задача 1: Обеспечить разработку
#### **GitLab**
> GitLab (SaaS или self-managed в облаке) + GitLab CI + GitLab Runners (Kubernetes + self-hosted runner nodes) + HashiCorp Vault (или GitLab CI/CD variables)

* Git — встроен.
* Каждый сервис — свой репозиторий.
* Триггер сборки по push/merge request.
* Можно запускать сборку вручную с параметрами.
* Секреты, через CI/CD Variables.
* Несколько конфигураций/шаблонов, через include в `.gitlab-ci.yml`.
* Кастомные шаги, описываются в job.
* Свои Docker-образы, задаём в job.
* Self-hosted runners, ставим на свои сервера.
* Параллельные сборки и тесты — встроено.



### Задача 2: Логи

#### **ELK-стек**
>Filebeat (DaemonSet в k8s) → Logstash → Elasticsearch → Kibana


* Сбор логов со всех хостов, агенты Filebeat/Fluent Bit.
* Приложения пишут в stdout, агенты читают docker/k8s логи.
* Доставка гарантируется буфером агентов.
* Elasticsearch поддерживают полнотекстовый поиск, фильтры, агрегации
* Доступ разработчикам, даём роли Kibana.
* Сохранённые поиски и ссылки, есть в Kibana.


### Задача 3: Мониторинг
#### **GAP-стек**

>Prometheus + node_exporter + cAdvisor/kubelet metrics + Alertmanager + Grafana

* Prometheus собирает метрики.
* node_exporter — системные метрики (CPU, RAM, диск, сеть).
* cAdvisor — ресурсы контейнеров/сервисов.
* Alertmanager — маршрутизация алертов, заглушки, интеграция с различными каналами нотификации.
* Запросы и агрегации — PromQL в Grafana.
* Grafana — дашборды, Explore, панель запросов, Dashboard provisioning, роль/доступ.