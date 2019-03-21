## **Apache Kafka คืออะไร?** ##

Apache Kafka คือ distributed message queue อาจจะงงนะครับ คิดซะว่าเราเป็นพ่อครัวแม่ครัว ยืนผัดข้าวผัดอยู่ ละมีลูกค้าหิวโซมาสัก 20 คนมาสั่งข้าวผัดหมู ข้าวผัดแหนม เอาไข่เจียว ไข่ดาวสุกบ้างไม่สุกบ้าง ถ้าเป็นแม่ครัวอย่างมากก็ตวาดไป ผัดอยู่ รอก่อนเว้ย มีกระทะเดียว อาจจะทำให้สถานการณ์ดีขึ้นบ้าง แต่ในโลกของการรับส่งข้อมูลมันไม่ได้ควบคุมง่ายขนาดนั้น ถ้าเราเป็นลูกค้าอยู่ร้านข้าวผัดเราก็คงหนีไปกินร้านอื่น แต่ถ้าเป็นโลกของการรับส่งข้อมูล คุมไม่ดี ข้อมูลหาย/ขาด/เกิน หรือถ้าเกี่ยวข้องกับตัวเลขการเงิน ยิ่งร้ายแรง

วิธีแก้ปัญหาอย่างง่ายๆก็คือต่อคิว.. แต่ความเจ๋งของ Apache Kafka คือ มันมีคุณสมบัติ distributed ขยายความง่ายๆ คือ มีแม่ครัวหลายคน มีเตาหลายเตาหลายกระทะนั่นเองงงง

โดยเริ่มแรก Kafka ถูกสร้างขึ้นโดย LinkedIn เป็น open source project ด้วยภาษา Java และ Scalaในช่วงต้นปี 2011 และถูกเผยแพร่ต่อ ผ่านทาง Apache Incubator ตั้งแต่ปี 2012 จากนั้นจึงได้แยกบริษัทออกมาจาก LinkedIn ก่อตั้งเป็น บริษัท Confluent เพื่อพัฒนา Kafka โดยเฉพาะ โดยชื่อ Kafka มาจากนักเขียนนาม Franz Kafka โดยเลือกชื่อ Kafka เพราะมันถูก optimize สำหรับการเขียน เหมือนกับงานของ Franz Kafka


## **ทำไมต้อง Apache Kafka?** ##

![1_XAnaiGvlfQ-Lv38kO7JZWg.png](https://bitbucket.org/repo/4pjE9Gx/images/2393778740-1_XAnaiGvlfQ-Lv38kO7JZWg.png)

Apache Kafka จึงถูกใช้เป็นตัวกลางในการเชื่อมต่อ เพื่อช่วยแยกการสื่อสารระหว่างระบบแต่ละตัว ไม่ว่าระบบอะไรต้องการข้อมูลจากไหน ก็มาเรียกใช้ใน Apache Kafka ตัวนี้ตัวเดียว


## **คุณสมบัติที่น่าสนใจของ Apache Kafka** ##
* มีการกระจาย (distributed) การเก็บข้อมูลใน clusters
* มีความยืดหยุ่น (resilient architecture) เช่น มีการทำสำเนาข้อมูลซ้ำ (replication)
* มีการทนต่อความเสียหาย (fault tolerent)
* มีความสามารถในการขยายเชิงขนาน หรือ เพิ่มเครื่อง (node) ใน cluster ได้ (horizontal scalability)
* มีประสิทธิภาพด้านความเร็ว (latency น้อยกว่า 10ms)
* มีระบบที่ใหญ่ๆ ที่ใช้ Apache Kafka อยู่มาก เช่น Linkedin, Netflix, AirBnB, Yahoo, Wallmart หรือ LINE สวัสดีวันจันทร์นั่นเองของเรานั่นเองงง

## **Apache Kafka ทำอะไรได้บ้าง** ##
* ระบบส่งต่อข้อความ (messaging System)
* เครื่องมือบันทึกกิจกรรม (activity Tracking)
* รวบรวมเก็บ Log (log aggregation)
* การประมวลผลแบบต่อเนื่องของข้อมูล (stream processing)


## **ระบบนิเวศน์ (Ecosystem) ของ Apache Kafka** ##
ก่อนจะเริ่มลงรายละเอียด ต้องรู้ก่อนว่ามีอะไรที่อยู่ในระบบนิเวศน์ของ Apache Kafka โดยหลักๆจะมีดังนี้

1. Kafka
1. Source systems
1. Producer
1. Target systems
1. Consumer
1. Zookeeper


![1_2aFC4ES6jB3skerX3orAzg.png](https://bitbucket.org/repo/4pjE9Gx/images/2823035536-1_2aFC4ES6jB3skerX3orAzg.png)


## **ขาเข้า** ##
เริ่มต้นจาก Kafka เลย ตัว Kafka เป็นแกนหลักของระบบ จากนั้นก็มี Source systems ซึ่งก็คือแหล่งที่มาของข้อมูล อาจจะเป็นจากฐานข้อมูลหรือ Logging จากนั้นก็มีสิ่งที่เราเรียกมันว่า Producer มาคั่นกลาง ระหว่างเรา… ไม่ใช่สิ ระหว่าง Source systems กับ Kafka ต่างหากโดยตัว Producer เองจะทำการดึงข้อมูลมาจาก Source systems แล้วเอาข้าไปใน Kafka

## **ขาออก (แต่ยังไม่เอาออก)** ##
คราวนี้เริ่มที่ Target systems คือที่ๆ อยากได้ข้อมูลใน Kafka ซึ่งจะมีตัวคั่นตรงกลางระหว่าง Kafka กับ Target systems ซึ่งเราจะเรียกมันว่า Consumer โดยตัว Consumer นี้จะทำหน้าที่ดึงข้อมูลมาจาก Kafka แล้วส่งต่อไปยัง Target systems ต่างๆเช่น ดึงข้อมูลแล้วแก้ไขให้อยู่ในรูปแบบข้อมูลที่เหมาะสมแล้วส่งต่อไปยัง ElasticSearch หรือ HDFS เป็นต้น แต่อย่างที่ระบุไว้นะครับ พออ่านแล้ว จะไม่ได้เอาข้อมูลออก ยังคงเก็บไว้อยู่

สิ่งสุดท้าย คือผู้จัดการ Zookeeper ที่ทำหน้าที่บริหารจัดการว่าควรจะไปอ่านข้อมูลที่ replica ตัวไหนหรือ Consumer นี้ควรไปอ่านข้อมูลตรงไหนต่อ เป็นต้น ซึ่งตัวระบบนิเวศน์ของ Kafka หลักๆ จะมีเท่านี้แหละ

แต่มันยังไม่หมด มันมีส่วนขยายให้อีก เช่น

* Kafka Streams ทำหน้าที่เปลี่ยนแปลงข้อมูลใน Kafka
* Kafka Connect ทำหน้าที่แปลงข้อมูลจาก Source systems ไปยัง Target systems โดยที่เราไม่ต้องสร้าง producer และ consumer ขึ้นมาเอง
* Confluent Platform ซึ่งเป็นชุดเครื่องมือเสริมเพื่อปรับปรุงประสิทธิภาพของการทำงานของ Apache Kafka ซึ่งมีทั้งแบบ Open source และแบบ Enterprise

## *ในการทำความเข้าใจและรู้จัก Apache Kafka ให้มากขึ้น* ##

มีสองสิ่ง ที่จะต้องทำความเข้าใจกับมันก่อน คือสิ่งที่เรียกว่า *Topics* แหละ *Partitions* ซึ่งสองสิ่งนี้ ทำหน้าที่จัดกลุ่มของข้อมูลที่เราจะเก็บไว้ 
มีข้อกำหนด มีคุณสมบัติหลายอย่าง ที่จำเป็นต้องรู้จักก่อนเอาไปใช้งานจริง

## **Topics** ##
Topics เป็นชุดของข้อมูล(หรือ Messages) มีลักษณะเหมือนกับ table ใน database ที่เราคุ้นเคยกัน(แต่ไม่มีตัวเชื่อมโยงในแต่ละ topic นะ) ซึ่งแต่ละ topic เนี่ย จะถูกตั้งชื่อได้ เพื่อให้เรารู้ว่ามันคือข้อมูลเกี่ยวกับอะไร ซึ่งชื่อก็ไม่ควร(จริงๆ ห้าม) ซ้ำกัน ไม่งั้นตอนเอาไปใช้งานก็จะแยกชุดของข้อมูลไม่ได้

## **Partitions** ##
ข้อมูลในแต่ละ Topic จะถูกแยกเป็นกลุ่มๆ อีก ซึ่งแต่ละกลุ่มนี้ จะถูกเรียกว่า Partition ข้อมูลในแต่ละ partition จะถูกจัดเรียง(ส่วนเรียกตามอะไร เดี๋ยวจะมาอธิบายต่อครับ) ข้อมูลแต่ละส่วน หรือแต่ละ message เนี่ย จะมีค่าบางอย่างที่มีลักษณะเพิ่มเองได้(incremental) ซึ่งจะเริ่มที่ 0 และเพิ่มค่าเป็น 1 2 3… ไปเรื่อยๆ ตามจำนวนของข้อมูล ซึ่งมันจะถูกเรียกว่า offset หรือตัวนับในแต่ละ partition

ลองดูการอธิบายข้างล่างเพื่อให้เห็นภาพที่ตรงกัน โดยเริ่มที่ partition แรก จะเรียกว่า partition 0


![1_PEFrTy8pHhD9sYHEHuN5fA.jpeg](https://bitbucket.org/repo/4pjE9Gx/images/3753076236-1_PEFrTy8pHhD9sYHEHuN5fA.jpeg)


เริ่มต้นที่ยังไม่มีค่าอะไร พอข้อมูลถูกเพิ่มมาครั้งแรก ตัว offset จะถูกนับเป็น 0 จากนั้น ถูกเพิ่มมาเรื่อยๆ ก็นับเพิ่มตามมาเรือยๆ ตามลำดับ

จากในตัวอย่าง offset ล่าสุดคือคือ 5 และตัว partition จะรู้ได้ว่าตัวถัดไปจะต้องเป็นตัวที่ 6

ซึ่งถ้าเราเตรียมไว้หลาย patition ใน topic ของเรา ข้อมูลจะถูกกระจายไปอยู่ในแต่ละ paritition เอง


![1_7EpqyC5F-rsvMaHfqZ1YtA.jpeg](https://bitbucket.org/repo/4pjE9Gx/images/1616688765-1_7EpqyC5F-rsvMaHfqZ1YtA.jpeg)


ตัวอย่างด้านบน สมมติว่าเรามี 3 partitions ใน 1 topic ซึ่งในแต่ละ partition จะมีข้อมูลที่ถูกกระจายมาแล้ว ในแต่ละ partition จะมีตัวนับ(offset)ซึ่งซ้ำกันได้ แต่จะไม่ใช่ข้อมูลชุดเดียวกันในแต่ละ partition เช่น เวลาอ้างถึง id 1 ใน partition 0 และ partition 1 จะเป็นข้อมูลคนละตัวกัน

## **คุณสมบัติเบื้องต้นของ Topics และ Partitions** ##
* offset จะใช้อ้างในแต่ละ partition เท่านั้น ตามที่อธิบายไปด้านบนแล้ว
* ข้อมูลจะถูกเรียงตามลำดับก่อนหลัง ใน partition นั้นๆ แปลว่า offset ที่ 0 ของ partition ที่ 0 อาจจะมาก่อนหรือหลัง offset ที่ 0 ของ partition 1 ก็ได้
* ไม่สามารถแก้ไขข้อมูลที่เอาใส่ใน topic แล้ว(Immutability)
* ข้อมูลจะถูกลบในเวลาที่เราตั้งไว้ *Retention ที่ setting ไว้ properties (default 604800000 ms หรือ 7 วัน) ไม่ว่ามันจะถูกหยิบไปใช้หรือไม่ เพราะต้องเคลียร์พื้นที่ใน hdd
* ข้อมูลจะถูกวน(round-robin)ในการจัดว่าควรจะอยู่ partition ไหน ในกรณีที่มีมากกว่า 1 partiton ยกเว้นมีการกำหนด key (ไม่ใช่ id นะครับ)
* topic มีกี่อันก็ได้ แต่ห้ามซ้ำ ใน topic มี partition กี่อันก็ได้อีกเช่นกัน
* ตัวนับว่าตัวถัดไปควรใช้เลขอะไร ถูกบันทึกใน ใน topic ที่ชื่อ __consumer_offsets (ใน version ต่ำกว่า 0.9 ตัวนับจะเก็บใน zookeeper) ขอบคุณข้อมูลจาก Pitsanu ด้วยคับ
* ข้อมูลมากไม่ใช่ปัญหาในการอ่านข้อมูล


สิ่งที่ควรทำความเข้าใจต่อไปถัดจาก Topics และ Partitions คือ Brokers


## **Brokers** ##
ตัวที่เก็บข้อมูลของ Kafka เนี่ย มันบรรจุอยู่ใน server ซึ่งจะเรียกมันว่า broker
ใน broker 1 ตัวเนี่ย มีตัวเลข id ตัวเองซึ่งไม่ซ้ำระบุอยู่ ตัว broker จะบรรจุข้อมูลในระดับ partition ของแต่ละ topic (ซึ่งถ้าถามว่ามันมีการกำหนดยังไงว่า partition ไหน ควรอยู่ใน cluster ตัวใด มีอธิบายใน stackoverflow หลักๆ เลยคือ มันไม่บอก ขอให้เชื่อมันสิ่งที่มันจัดให้ 5555) และมี broker หลายๆ ตัวประกอบกัน (มีการ distribute) เลยเรียกมันว่า Kafka cluster

ถ้าเรามี cluster (broker หลายตัว แนะนำ 3 ตัวเป็นอย่างต่ำ) เราสามารถเข้าถึง cluster ซึ่งมันจะมีศัพท์เฉพาะเรียกกลุ่ม cluster นี้ว่า Bootstrap servers ขอเพียงต่อเข้าตัวใดตัวหนึ่งได้ เราจะสามารถเข้าถึงข้อมูลใน broker ตัวอื่นใน cluster ได้เหมือนกัน

เพื่อเห็นภาพที่ตรงกัน อยากจะให้ดูตัวอย่างสักนิด


![1_3_Cq92ej7w7Vo2puygP3Kw.jpeg](https://bitbucket.org/repo/4pjE9Gx/images/3050564941-1_3_Cq92ej7w7Vo2puygP3Kw.jpeg)


จากตัวอย่าง จะเห็นภาพมากขึ้นว่ามันเก็บข้อมูลในระดับ partition ยังไง หากเราต้องการข้อมูลใน topic 1, partition1 เราไม่จำเป็นต้องต่อตัว broker 2 ก็ได้ เข้าที่ตัว broker 1 ก็จะสามารถเข้าถึงได้เหมือนกัน ตัว Kafka มันรู้เองว่าต้องไปเอาข้อมูลจาก broker ตัวไหน

## **Topic Replication Factor** ##
เราควรทำความเข้าใจค่านี้ด้วยครับ เป็นค่าที่บอกว่าในแต่ละ topic จะมีการทำสำเนา (replica) partition จากตัวหลัก(leader)ไปสำเนากี่ server หรือ broker (เรียกว่า in-sync replication คือถ้าข้อมูลเข้ามาตัวหลักก็ส่งไปทำสำเนาเพิ่มเลย) ซึ่งควรมีมากกว่า 1 ปกตินิยม 2–3 ครับ และ partition ตัวหลักก็มีได้ 1 ตัว ซึ่งคุณสมบัตินี้เอง เป็นตัวที่ทำให้ Apacha Kafka มีคุณสมบัติ Fault Tolerance (ความทนต่อความเสียหาย) ถ้ามี broker ตัวนึงเน่าไป มันยังสามารถไปอ่านและบันทึกข้อมูลต่อในตัวที่เป็น replica ได้ด้วย โดยการเปลี่ยนตัวสำเนาหรือ replica ให้เป็นตัวหลัก หรือ leader หรือบางคนเรียก master


![1_uTYdtlEa4Ed8ZmhLRFG_hg.jpeg](https://bitbucket.org/repo/4pjE9Gx/images/2465454920-1_uTYdtlEa4Ed8ZmhLRFG_hg.jpeg)


จากตัวอย่าง สีเหลืองคือ leader สีขาวคือ replica โดยมีตัวเลข replication factor เป็น 2

ถ้าหาก broker ตัวใดตัวนึงตาย ไป เรายังมีอีก 2 ตัวให้ทำงาน แต่ถ้าหากมันตายมากกว่า 1 ตัวก็จบ เพร
าะฉะนั้น การกำหนดตัวเลข replication factor จึงสำคัญ ยิ่งมากยิ่งปลอดภัย ซึ่งจะทนการเน่าของ server ได้ n-1 ตัว ถ้าสมมติกำหนด replication factor เป็น n แต่ก็มีสิ่งแลกเปลี่ยนคือมันเปลืองพื้นที่ในการเก็บ ก็ต้องประมาณจากความเสี่ยงที่มีเองครับ

แล้วถ้าจะเปลี่ยน replication factor ได้ไหม?? ตอนแรกผมเองก็คิดว่าค่า replication factor นี้เปลี่ยนไม่ได้ แต่จริงๆ มันทำได้ มีวิธีการนี้อยู่

ถ้าหากจะเอาปลอดภัย มี Mirror Maker ให้ใช้อีกครับ ไว้ทำสำเนาไปนอก cluser เลย


## **Producers** ##
Producer นี่เป็นอะไรที่ไม่ค่อยซับซ้อนมาก หลักๆ ก็คือการเอาข้อมูลเข้าไปอยู่ใน partition ใน topic ที่เรากำหนดไว้ วิธีใช้งานก็ง่ายๆ แค่ต่อเข้า broker ตัวใดตัวนึง แล้ว produce ไป ด้วย topic อันนึง data มันก็จะถูกส่งไปหา partition ในแต่ละ broker เอง ตรงนี้ kafka ทำให้หมดเลย

## **Message keys** ##
สิ่งที่อยากจะเน้นย้ำคือเรื่องการเรียงลำดับของข้อมูล ถ้าเราไม่กำหนด key ให้มัน มันก็จะวนส่งข้อมูลแบบ round-robin ไปยัง broker ที่ partition ใน topic นั้นๆ อยู่ แต่ถ้ามีการกำหนด key ไว้ หลังจากการ produce ครั้งแรกแล้ว ถ้ามี key เดิมซ้ำกันเข้ามา มันจะวิ่งเข้าไปหา broker ที่เดิมที่ key นั้นเคยเข้าไปอยู่ครั้งแรก

ส่วนเงื่อนไขที่จะพิจารณาว่า message key อันไหน ควรอยู่ที่ partition ไหน ในกรณีที่ยังไม่มี key อันนั้น อันนี้มันจะเอา key ไป hash แล้วเอาค่ามาทำอะไรบางอย่างซึ่งตรงนี้ มันลึกมากแล้ว ผมเองยังศึกษาไม่ถึง ขอข้ามส่วนนี้ไปก่อน เอาเป็นว่ามันสุ่มไปก่อน

## **Acks** ##
# ตัวนี้เป็นอีก 1 ตัวที่ควรจะตระหนักไว้ในการทำงานของ producer จะมี 3 ระดับ คือ #
* acks=0 producer จะ produce แล้วไม่รอผลตอบของ broker ว่าได้รับข้อมูลหรือยัง
* acks=1 producer จะ produce และรอผลตอบจาก leader partition ว่าได้รับข้อมูลหรือยัง
* acks=all producer จะ produce และรอผลจนข้อมูลถูกบันทึกเข้า replica แล้ว

สรุป ระดับ acks=0 นี่ทำงานไวสุด แต่มันก็ไม่ได้รับประกันได้เลยว่าข้อมูลจะถูกเก็บถึงจริงๆ หรือเปล่า ส่วน acks=1 นี่ เริ่มนานขึ้น เพราะต้องรอตัว leader ตอบกลับ ซึ่ง acks=1 นี่ เป็นค่า default ของ producer ด้วย และระดับ 3 นี่ จะไม่มีข้อมูลหายเลย แต่ก็แลกกับการทำงานที่ช้าขึ้น เหมาะสำหรับข้อมูลสำคัญๆ

## **Consumers** ##
หน้าที่หลักของ consumer คืออ่านข้อมูลจาก partition เพียงแค่ต่อเข้า broker สักตัว แล้วระบ topic ไป มันก็จะอ่านให้เอง ไม่ว่า partition จะอยู่ที่ broker ไหนก็ตาม เหมือนๆ กับฝั่ง producer เลยครับ

## **Order** ##
อยากเน้นเรื่องลำดับการอ่านอีกแล้วครับ ตัว consumer จะอ่านข้อมูลตามลำดับใน partition เดียวกัน แต่ถ้าต่าง partition มันจะอ่านแบบขนาน(parallel) เพราะฉะนั้น การออกแบบการเรียงลำดับตัว message key ตั้งแต่ฝั่ง consumer เลย จริงเป็นสิ่งที่สำคัญมาก ถ้าข้อมูลจำเป็นต้องถูกเรียกใช้ตามลำดับ ยกตัวอย่างนะครับ


![1_85JPA2a5WHL5BVbsP7bIyA.jpeg](https://bitbucket.org/repo/4pjE9Gx/images/4154399628-1_85JPA2a5WHL5BVbsP7bIyA.jpeg)


ถ้าเรามี consumer มาอ่านเนี่ย ข้อมูลที่เราได้ จะไม่ได้เรียง a,b,c,d.. ตามลำดับแบบนี้นะครับ partition0 อาจจะถูกอ่านไวกว่าที่ partition1 ก็ได้ ข้อมูลที่ consume มา อาจจะเป็น b,d,a,c,d…. ก็เป็นไปได้ แต่อยากให้สังเกตอย่างเดียวครับ มันจะเรียงตามลำดับตามใน paritition เดียวกันแน่นอน a จะต้องมาก่อน c และ c จะมาก่อน e ในขณะเดียวกัน b จะมาก่อน d แน่นอน

## **Consumer Groups** ##
ปัญหาคือ ถ้าหากระบบเรา produce ข้อมูลเข้ามามากๆ ในขณะเดียวกัน consumer ที่เรามีก็น้อยไม่เพียงพอ เราเพิ่ม consumer ได้เลย เพื่อให้มัน consume ได้เร็วขึ้น โดยมันจะ consume แบบขนานกันไป ซึ่งหนึ่ง ### ข้อบังคับของ consumer ใน group หนึ่ง ต้องมีจำนวน consumer ไม่เกินจำนวน partition ใน topic ที่ consumer นั้นสนใจ ถ้ามีเกินมา ตัวนั้นจะไม่ได้ทำอะไร ###


![1_hAQEuDsSLp7cH429KP-psA.jpeg](https://bitbucket.org/repo/4pjE9Gx/images/2076394993-1_hAQEuDsSLp7cH429KP-psA.jpeg)


จากตัวอย่าง 
- ถ้า group มี consumer 1 ตัว consumer ตัวเดียวนั้นจะอ่านข้อมูลจากทุก partition
- ถ้า group มี consumer 2 ตัว consumer 1 ในสองตัวนั้น จะอ่านข้อมูลจาก 2 partition และอีก 1 ตัวจะอ่านจาก partition ตัวที่เหลือตัวเดียว
- ถ้า group มี consumer 3 ตัว consumer แต่ละตัวก็จะรับผิดชอบแต่ละ partition เลย
- และถ้ามีเกิน 3 ตัว ตัวที่เกินมานั้นจะไม่ได้อ่านอะไรเลย

จากตัวอย่างเดียวกัน จะสังเกตดูได้ว่าจะไม่มี consumer อ่าน partition ที่ซ้ำกันเลย แปลว่าไม่ว่าเราจะเพิ่มหรือลด consumer มันจะไม่อ่านข้อมูลซ้ำกันเด็ดขาด

และความสุดยอดอีกอย่างนึงคือ เราสามารถเพิ่มและลด consumer ได้ตอนไหนก็ได้ มันจะมีการแบ่ง(re-balance)หน้าที่ของ consumer ที่มีให้เองว่าควรไปอ่านที่ partition ไหน ซึ่งตรงนี้เป็นคุณสมบัติ resilient หรือความยืดหยุ่นนั่นเอง

อาจจะสงสัยนะครับ แล้วถ้ามีหลาย group ล่ะ(เพื่อจุดประสงค์การ consume ที่ต่างออกไป เช่นมี serviceใหม่) มันจะเริ่มอ่านจากตรงไหน ใน topic เดียวกัน คำตอบคือ แต่ละ group จะมีตัวนับ(offset) ของมันเอง สมมติมี group แรก กำลังทำงานอยู่ แล้วเราเพิ่ม group ที่ 2 เข้ามา มันก็จะเริ่มอ่านตั้งแต่แรก(ซึ่งเซ็ตได้ว่าจะให้อ่านจากตั้งแต่แรกหรือจากข้อมูลปัจจุบัน) คือตัวนับมันจะแยกกันโดยสิ้นเชิง


## **Zookeeper** ##
มาถึงอีกหนึ่งพระเอกของเรา Zookeeper 
- ทำหน้าที่จัดการ brokers คือรู้ว่า broker ตัวไหน อยู่ที่ไหน ตายอยู่หรือไม่ตาย
- บันทึกว่า topic ไหนมีหรือไม่มี มีกี่ partition ใน topic นี้
- ทำการเลือก leader/replica ของ partition
- ส่งสัญญาณไปหา Kafka ในทุกๆ การเปลี่ยนแปลงที่เกิดขึ้น เช่น มี topic มาใหม่ หรือมี broker ตาย หรือเพิ่มขึ้นมา
- บันทึกว่า producer/consumer แต่ละตัวควรจะเขียนหรืออ่าน data ได้เท่าไหร่
- เก็บ Authorization ว่า user ไหนถูกอนุญาตให้สร้าง topic บ้าง (โดยส่วนตัวผมยังไม่มีโอกาสได้ทดลองตรงส่วนนี้ ลองอ่าน doc ไปก่อนได้ครับ)
- บันทึกว่าแต่ละ consumer group มี consumer กี่ตัว อ่านไปถึง offset ไหนแล้ว
- มีพรรคพวก(quorum)ของมันเอง นิยมให้เป็นจำนวนเลขคี่เช่น มี 3,5,7… ตัวของ จำนวน Zookeeper เพราะมีเรื่อง consensus ในการบันทึกข้อมูลด้วย เช่น ต้องเป็นจำนวนมากกว่าครึ่งนงของ Zookeeper ที่รันอยู่เช็คแล้วว่าถูกบันทึกแล้ว ตัว leader ของ Zookeeper เองจะบันทึกเสร็จแล้วจริงๆ ซึ่งตรงโลกของ Zookeeper นี้ ผมจะขอข้ามไปก่อน(ยังเข้าไม่ถึง)


## **การรับประกันการส่งข้อความ** ##
ใจจริง topic นี้อยากตั้ง title ให้เป็นภาษาอังกฤษตาม document มัน คือ Message Delivery Semantics นั่งจ้องมัน ละก็เปิด dictionary ละก็ไม่เข้าใจ ต้องไปตามอ่านว่ามันทำอะไรกันแน่

หัวข้อนี้เป็นหัวข้อสุดท้ายละสำหรับโพสนี้ การรับประกันที่ว่าเนี่ย มี 3 สิ่งตาม document คือ

At most once → Messages may be lost but are never redelivered.
At least once → Messages are never lost but may be redelivered.
Exactly once → This is what people actually want, each message is delivered once and only once.
ทำไมต้องมาสนใจของพวกนี้ด้วย?? เพราะตอนเราสร้าง consumer ขึ้นมา เราสามารถ commit ได้ว่าเราอยากจะ commit ตัวนับ(offset) ไว้ล่าสุดตรงไหน ให้ครั้งต่อไป consumer จะกลับมาอ่านต่อ

3 สิ่งนี้จะเป็นสิ่งที่เราจะเจอตอนที่เราทำงานกับ consumer

## **At most once** ##
ขยายความได้ว่า consumer จะรับ message มาแต่ละอันมากสุดแค่อันละครั้งเดียว
แปลว่าหลังจากที่ consumer อ่าน message มาแล้ว มันจะถือว่า message นั้น ถูกอ่านไปแล้ว และจะนับ offset ที่ตัวล่าสุดเลย(ขึ้นอยู่กับความถี่การบันทึกตัวนับ อธิบายไว้ด้านล่างครับ ขอบคุณ Pitsanu ที่ช่วยชี้แจงตรงนี้ครับ) ฟังดูดี ละปัญหามันคืออะไร

ปัญหามันคือ ถ้าขณะตอนที่อ่านมาแล้ว consumer ตัวนั้นดันเน่าขึ้นมา มันจะไม่กลับไปอ่านต่อตัวที่เพิ่งอ่านมานะ ก็คือจะมีข้อมูลหายตอนส่งไปไปยัง target system นั่นเอง รวมถ้าถึง target system เราเน่าเองด้วย ก็จะไม่ได้รับข้อมูลน้ันเช่นกัน ค่า default ของ consumer เป็นแบบนี้อยู่ คือถูกตั้งค่าการนับ offset ไว้เป็นแบบอัตโนมัติ (enable.auto.commit เป็น true) แต่มันจะนับการ commit ตัว offset ขึ้นอยู่กับช่วงเวลา ซึ่งค่า config คือ auto.commit.interval.ms จะมีค่า default อยู่ที่ 5000 ms


## **At least once** ##
ขยายความได้ว่า consumer **จะรับ message มาแต่ละอัน อย่างน้อยอันละหนึ่งครั้ง**
แปลว่าหลังจากที่ consumer อ่าน message มาแล้ว ถ้า consumer เน่า หรือตอนส่งข้อมูลไปหา target system แล้วมีปัญหา มันจะยังสามารถกลับอ่าน message อันเดิมซ้ำๆ จนกว่าจะมีการ commit หรือ บันทึก offset นั่นเอง อันนี้ฟังดูดี เรารับประกันได้ว่า target system เรา จะไม่มีข้อมูลหายแน่นอน

แต่ก็มีปัญหาอีก สมมติว่า consumer กำลังจะบันทึก offset พอดี consumer ดันมาตาย ถ้าปลุกมันมา มันจะไปอ่านที่ตัว message เดิมก่อนบันทึก offset แล้วก็ทำซ้ำ หรือถ้าปัญหาเกิดที่ target system เอง โดย consumer รู้ได้ว่ายังไม่จบกระบวณการที่ target system ก็จะไม่บันทึกค่า offset ซึ่งอาจจะมีการรอจนกว่า target system จะกลับมาปกติ แล้วส่งข้อมูลเดิมไปใหม่ ปัญหาคือ **target system จะได้รับข้อมูลซ้ำอันเดิมอีกครั้ง**

## **Exactly once** ##
ขยายความได้ว่า consumer **จะรับ message มาแต่ละอันแค่ครั้งเดียวเท่านั้น**
จริงๆ อันนี้ฟังดูเหมือนคล้าย at most once มาก แต่ความหมายจริงๆ คือ ทุกกระบวณการ จะทำแค่ครั้งเดียว ทุกอย่างสมบูรณ์แบบถ้า consumer ตายแบบกรณี at least once ตัวข้อมูลจะไม่ถูกส่งซ้ำ ฟังดูตามที่ doc อธิบายไว้คือ นี่คือสิ่งที่ทุกคนต้องการ แต่มันก็มีปัญหาอีก

ปัญหาคือ การจะทำอะไรแบบนี้ได้ มันยากมาก ต้องมีระบบเบื้องหลังควบคุมอย่างรัดกุม เอาง่ายๆ ว่า ทำยากมาก คืออาจจะทำได้นะ แต่จะคุ้มหรือเปล่าที่ต้องมีอะไรๆ มาเยอะแยะ

ซึ่งการนำไปใช้งานจริงๆ นิยมใช้เป็นแบบ at least once มากกว่า แล้วทำ target system ให้มีคุณสมบัติ idempotent เพิ่มมา คือ รับข้อมูลซ้ำๆ ไม่เป็นไร จะตัดทิ้ง จะบันทึกซ้ำ ยังไงก็ได้ แต่ผมชอบแบบบันทึกซ้ำมากกว่า คือให้มันมีการทำ upsert ได้เลย คือ ไม่มี message นั้นก็บันทึกใหม่ ถ้ามีแล้วก็บันทึกซ้ำ

##**Kafka Config heartbeat session timeout max.poll.interval ** ##

Assuming we are talking about Kafka 0.10.1.0 or upwards where each consumer instance employs two threads to function. One is user thread from which poll is called; the other is heartbeat thread that specially takes care of heartbeat things.

session.timeout.ms is for heartbeat thread. If coordinator fails to get any heartbeat from a consumer before this time interval elapsed, it marks consumer as failed and triggers a new round of rebalance.

max.poll.interval.ms is for user thread. If message processing logic is too heavy to cost larger than this time interval, coordinator explicitly have the consumer leave the group and also triggers a new round of rebalance.

heartbeat.interval.ms is used to have other healthy consumers aware of the rebalance much faster. If coordinator triggers a rebalance, other consumers will only know of this by receiving the heartbeat response with REBALANCE_IN_PROGRESS exception encapsulated. Quicker the heartbeat request is sent, faster the consumer knows it needs to rejoin the group.

##** Suggested values: ** ##

* session.timeout.ms : a relatively low value, 10 seconds for instance.
* max.poll.interval.ms: based on your processing requirements
* heartbeat.interval.ms: a relatively low value, better 1/3 of the session.timeout.ms

##**Kafka Command** ##

[Link to Kafka Command](https://bitbucket.org/tbn_ktc/helm-chart-olm/wiki/Kafka%20Command)

##**Kafka Reblance Concept Reference** ##

[Reblance Reference](https://www.linkedin.com/pulse/partitions-rebalance-kafka-raghunandan-gupta)

## **Copy Reference Link** ##
[Link to Kafka Reference 1](https://medium.com/linedevth/apache-kafka-%E0%B8%89%E0%B8%9A%E0%B8%B1%E0%B8%9A%E0%B8%9C%E0%B8%B9%E0%B9%89%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%95%E0%B9%89%E0%B8%99-1-hello-apache-kafka-242788d4f3c6)


[Link to Kafka Reference 2](https://medium.com/linedevth/apache-kafka-%E0%B8%89%E0%B8%9A%E0%B8%B1%E0%B8%9A%E0%B8%9C%E0%B8%B9%E0%B9%89%E0%B9%80%E0%B8%A3%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%95%E0%B9%89%E0%B8%99-3-try-kafka-f6a6a9b93d58)
