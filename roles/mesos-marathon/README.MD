docker run --name=marathon -d -e "MESOS_IP=10.0.0.14" -e "LIBPROCESS_IP=10.0.0.14" --restart=always --net=container:tinc mesosphere/marathon:v1.4.11 --master zk://10.0.0.2:2181,10.0.0.8:2181,10.0.0.12:2181,10.0.0.14:2181,10.0.0.15:2181/mesos --zk zk://10.0.0.2:2181,10.0.0.8:2181,10.0.0.12:2181,10.0.0.14:2181,10.0.0.15:2181/marathon --hostname 10.0.0.14 --http_address 10.0.0.14


dump all tasks
curl -i -H 'Content-Type: application/json' -d @jou.json http://10.0.0.15:8080/v2/apps
