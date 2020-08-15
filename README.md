## Projeto-Integrador-IV-A

### Equipe
* Bruno Lemke dos Santos
* Guilherme de Souza Dias
* Luciano Batista da Cunha
* Marcelo Souza da Rosa
* Ronaldo Silva da Cunha
* Tiago Tessmann Oliveira

### Primeiro Encontro - 15/08/2020

#### Sockets TCP & UDP
[Introdução ao Conceito de Sockets](http://olaria.ucpel.edu.br/materiais/lib/exe/fetch.php?media=introducao-sockets.pdf)

#### Conceitos Relacionados à IoT:
* [Slides](http://olaria.ucpel.edu.br/materiais/lib/exe/fetch.php?media=internet_das_coisas_piv.pdf)
* [IoT Comic Book](https://iotcomicbook.org/)
* [Fog & Cloud](http://olaria.ucpel.edu.br/materiais/lib/exe/fetch.php?media=apresentacao-pi-iv.pdf)

#### Plataformas de Nuvem para IoT
* [Relação de Serviços](http://olaria.ucpel.edu.br/materiais/doku.php?id=plataformas_nuvem_iot)

#### Embarcados para IoT
* [System on a Chip ESP32S](http://olaria.ucpel.edu.br/micropython/doku.php?id=esp32) -- [Oferta Mercado Livre](https://produto.mercadolivre.com.br/MLB-1151473863-esp32-esp32s-placa-modulo-wi-fi-bluetooth-dual-core-_JM?matt_tool=79246729&matt_word=&gclid=CjwKCAjw4MP5BRBtEiwASfwAL0F8mFwv-V3Q_O161Ge-EfIvJKZPkDSirQHND7rrsGmBt5yx62m_8xoC2C4QAvD_BwE&shippingOptionId=undefined)
* [Sensor de Temperatura DS18b20](https://www.maximintegrated.com/en/products/sensors/DS18B20.html) -- [Oferta Mercado Livre](https://produto.mercadolivre.com.br/MLB-1059731944-5x-sensor-de-temperatura-ds18b20-waterproof-arduino-_JM?quantity=1#position=3&type=item&tracking_id=d4f114c0-9fab-4e6d-ae50-cd980b631fb6)

#### Monitorando Informações do Equipamento
[Integrando Bash com Python](http://olaria.ucpel.edu.br/materiais/doku.php?id=integrando-bash-python)
[Exemplo em Bash](http://olaria.ucpel.edu.br/materiais/doku.php?id=script-filtro-informacoes)

#### Conhecendo o Bash de Sistemas Operacionais Posix
* [Sistemas Posix](https://pt.wikipedia.org/wiki/POSIX)
* [Foca Linux](http://www.guiafoca.org/)
* [Ebooks sobre Sistemas Operacionais Posix](https://drive.google.com/drive/folders/0B2INSZz1E5TlVWdkVFM0OUxKXzA)

* Exemplo de uso do Cron: 
  * 0-59/2 * * * * date >> exemplo-pi-iv.txt 
  * A cada 2 minutos o comando é executado

#### Virtualizando
* [https://www.virtualbox.org/](Virtual Box)
* [https://linuxmint.com/](Linux Mint)

#### Transmitindo Informações Sensoriadas do Meio para um Servidor
  * Conceitos
    * [Protocolo MQTT - Material IBM](https://www.ibm.com/developerworks/br/library/iot-mqtt-why-good-for-iot/index.html)
    * [Protocolo MQTT - Material Curto Circuito](https://www.curtocircuito.com.br/blog/introducao-ao-mqtt/)
    * [Slides sobre MQTT - Material UFC](https://pt.slideshare.net/MaurcioMoreiraNeto/protocolo-mqtt-redes-de-computadores)
    * [Comparação MQTT & Outros Protocolos](https://medium.com/internet-das-coisas/iot-05-dando-uma-breve-an%C3%A1lise-no-protocolo-mqtt-e404e977fbb6)
  * Plataformas de Software
    * [Mosquitto da Eclipse Foundation](https://mosquitto.org)
    * [Brokers MQTT gratuitos e pagos para utilizar em projetos da IoT](https://diyprojects.io/8-online-mqtt-brokers-iot-connected-objects-cloud/#.XzfHmEl7nUI)
    * [Explorando o uso de MQTT em Programas Python](https://fazbe.github.io/Usando-o-paho-mqtt-para-Python/)

#### Comunicando com um Broker MQTT utilizando Python

##### Procedimento de Subscrição
~~~
# Cliente Python para subscrever em um Broker MQTT
#
# Para instalar o paho-mqtt use o comando pip install paho-mqtt
import paho.mqtt.client as mqtt

# Retorno quando um cliente recebe um  CONNACK do Broker, confirmando a subscricao
def on_connect(client, userdata, flags, rc):
    print("Conectado, com o seguinte retorno do Broker: "+str(rc))

    # O subscribe fica no on_connect pois, caso perca a conexão ele a renova
    # Lembrando que quando usado o #, você está falando que tudo que chegar após a barra do topico, será recebido
    client.subscribe("PI-IV-A/#")

# Callback responsavel por receber uma mensagem publicada no tópico acima
def on_message(client, userdata, msg):
    print(msg.topic+" "+str(msg.payload))

client = mqtt.Client()
client.on_connect = on_connect
client.on_message = on_message

# Define um usuário e senha para o Broker, se não tem, não use esta linha
# client.username_pw_set("USUARIO", password="SENHA")

# Conecta no MQTT Broker
client.connect("mqtt.eclipse.org", 1883, 60)

# Blocking call that processes network traffic, dispatches callbacks and
# handles reconnecting.
# Other loop*() functions are available that give a threaded interface and a
# manual interface.
# Inicia o loop
client.loop_forever()
~~~
##### Procedimento de Publicação
~~~
# Ensures paho is in PYTHONPATH
import context
# Importa o publish do paho-mqtt
import paho.mqtt.publish as publish

# Publica
publish.single("PI-IVA", "Olá Mundo!", hostname="mqtt.eclipse.org")
~~~


