RabbitMQ is a message broker: it accepts and forwards messages. You can think about it as a post office: when you put the mail that you want posting in a post box, you can be sure that the letter carrier will eventually deliver the mail to your recipient. In this analogy, RabbitMQ is a post box, a post office, and a letter carrier.

The major difference between RabbitMQ and the post office is that it doesn't deal with paper, instead it accepts, stores, and forwards binary blobs of data ‒ messages.

RabbitMQ, and messaging in general, uses some jargon.

Producing means nothing more than sending. A program that sends messages is a producer :

![image](https://user-images.githubusercontent.com/84008107/136219609-1c5acfa7-acc5-4059-8afa-7e0dcd7cc999.png)


A queue is the name for a post box which lives inside RabbitMQ. Although messages flow through RabbitMQ and your applications, they can only be stored inside a queue. A queue is only bound by the host's memory & disk limits, it's essentially a large message buffer. Many producers can send messages that go to one queue, and many consumers can try to receive data from one queue. This is how we represent a queue:

![image](https://user-images.githubusercontent.com/84008107/136219670-862e7719-7501-4e8e-91f5-07f375a2f352.png)

Consuming has a similar meaning to receiving. A consumer is a program that mostly waits to receive messages:

![image](https://user-images.githubusercontent.com/84008107/136219764-0926408a-0db6-40c7-a4d4-09b1941db036.png)



![image](https://user-images.githubusercontent.com/84008107/136219251-7c3e920d-f74d-4978-b5ec-63fb04ecec5b.png)
