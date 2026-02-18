**Vibecoded slop for monitoring gnu+linux hosts. WIP**

#Requirements: docker, correct firewall rules (you don't need exposure of used port to outside obviously)#

Prepping:

*Agent*
1. Put /h-mon-tool/agent dir on hosts you want to monitor;
2. /h-mon-tool/agent/vector/vector.toml and /h-mon-tool/agent/docker-compose.yml are pre-configured, if you know what you're doing - fix it accordingly;
3. Edit .env (all the fields with <changeme!> tag have to be set up. If you have only one monitoring node - delete or comment out LOKI_SECONDARI_PUSH_URL string);
4. cd and docker compose up -d.

*Monitoring-node*
1. Edit /h-mon-tool/monitoring-node/.env (similarly to /agent/.env);
2. Edit /h-mon-tool/monitoring-node/docker-compose.yml (all the <changeme!> fields have to be populated. The presented .yml has default port values, change if you know what you're doing);
3. Edit /h-mon-tool/monitoring-node/matrix-receiver/config.yml. The pager string has to contain Internal room ID (in Element web app you can find it in "Room settings -> Advanced". Edit firing-template if needed;
4. Edit blackbox_###.ymls in /h-mon-tool/monitoring-node/prometheus/targets. Use template <protocol>://<fqdn>:<port> and you should be good;
5. Edit nodes.yml in /h-mon-tool/monitoring-node/prometheus/targets;
6. Edit /h-mon-tool/monitoring-node/secrets content;
7. cd and docker compose up -d.

*Usage*
1. On same network with your monitoring node, go to http://<your_node_ip_or_fqdn:3000>
2. Use login and password you set up in /h-mon-tool/monitoring-node/.env
3. Go to "Dashboards -> New -> Import". I recommend starting with ID 1860 and ID 13659
