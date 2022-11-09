**Create Pub Sub**

1. docker-compose up -d
2. Open a new terminal and run `docker exec -i -t kafka1 bash` to open a bash in the kafka1 container
3. In this bash terminal, run `kafka-topics.sh --create --topic test1 --bootstrap-server kafka1:9092, kafka2:9092, kafka3:9092`, this creates a topic for publishers and subscribers to connect to
4. Now, we create a publisher in this bash terminal with the command, `kafka-console-producer.sh --topic test1 --bootstrap-server kafka1:9092, kafka2:9092, kafka3:9092`
5. Repeat step 2, but in this bash terminal, we run `kafka-console-consumer.sh --topic test1 --from-beginning --bootstrap-server kafka1:9092, kafka2:9092, kafka3:9092` instead to create a consumer
6. Typing messages in the publisher bash will result in the same messages being printed in the consumer bash.

**Failure of Main Node**

1. Firstly, we need to check which is the main or leader node
2. This can be done by running `docker exec -i -t <container name> bash` for each of the zookeeper containers
3. The leader node will have `Mode:Leader`
4. We can stop the leader node with `docker stop <Leader_node>`
5. Observe that the pub sub service is still working.
6. By running step 2 again, we can see that the leader node has changed to one of the other 2 nodes.
