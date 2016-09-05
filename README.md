# Monitoring

Monitoring solution for internal services.

## Configuration files

### Prometheus

1. Create 'prometheus/alert.rules' based on 'prometheus/alert.rules.example'. More examples in [Prometheus documentation](https://prometheus.io/docs/alerting/rules/).
2. Create 'prometheus/prometheus.yml' based on 'prometheus/prometheus.yml.example'. More examples in [Prometheus documentation](https://prometheus.io/docs/operating/configuration/).

### Alert manager

1. Create 'alertmanager/alertmanager.yml' based on 'alertmanager/alertmanager.yml.example'. More examples in [Prometheus documentation](https://prometheus.io/docs/alerting/configuration/).

### Grafana

1. Create 'grafana/env' based on 'grafana/env.example'. Can be override any [default settings](https://github.com/grafana/grafana/blob/master/conf/defaults.ini).

### Nginx/SSL

1. Create 'ssl/env' based on 'ssl/env.example'.


## Running

### First start
1. ```docker-compose build```
2. ```docker-compose up -d```

### Stop

1. ```docker-compose stop```

### Re-start after change configs

1. ```docker-compose build```
2. ```docker-compose up -d```

## Configuring Grafana

1. Add DataSource with name: 'Prometheus', type: 'Prometheus', Url: 'http://prometheus:9090'

## Add new node

### Install monitoring agent on new node 

1. Create 'docker-compose.yml' based on file 'exporter/docker-compose.yml'. 
2. Create 'env.nginx' based on file 'exporter/env.nginx.example' and set HTTP Basic Authentication user name and password.
3. ```docker-compose up -d```

### Update Prometheus config

1. Add new node in file 'prometheus/prometheus.yml' to 'targets' property.
2. ```docker-compose build``` and ```docker-compose up -d```.

### Add new dahsboard in Graphana

1. Replace in 'grafana/charts_template.json' value 'node.exmaple.com' on new node host.
2. Import file 'grafana/charts_template.json' as dashboard to Grafana.
