Configuração DTU W100 Home Assistant



OLÁ FIZ ESSE PASSO A PASSO DE CONFIGURAÇÃO DE DTU HOIMILIES ESPERO QUE AJUDE

Este passo a passo serve para todas as DTU no meu caso foi a DTU W100 Gen 2 e só seguir o passo a passo .

Vamos lá o passo a passo. 
1 Configure seu MQTT se não estiver configurado  ou instale se não tiver o meu ficou assim 
MQTT
http://homeassistant.local:8123/hassio/addon/core_mosquitto/info
No canto inferior Loja de Add-ons

Instale e vamos em ajustes.
Clique nos 3 pontos no canto superior Editar com yaml `

```
logins:
  - username: Vinicius #Crie Seu nome que escolher de usuário 
    password: 12345 # Crie uma senha  
require_certificate: false
certfile: fullchain.pem
keyfile: privkey.pem
customize:
  active: false
  folder: mosquitto
```

Guarde isso pois vamos precisar .
Na interface gráfica tem que estar assim as portas usadas pelo MQTT deve ser liberadas no Firewall e Eu liberei no Roteador como UTP TCP Liberei entrada e saída 1883, 1884, 8883, 8884 Para que o MQTT fale com os programas .
Salva e inicia o MQTT.
![Configuração MQTT](https://raw.githubusercontent.com/viniciusmbs/DTU-W100/main/1.jpeg)


1  instale o Hoymiles DTU Solar: Home Assistant Add-on são dois um estável e outro não estável
![Configuração MQTT](https://raw.githubusercontent.com/viniciusmbs/DTU-W100/main/2.jpeg)

 Instalei os dois .

Instalando o Hoymiles DTU Solar: Home Assistant Add-on
https://github.com/banny310/hoymiles-dtu-homeassistant-addon

Siga o passso a passo da documentação de como instalar ou use o app Android Fing Após instalar vá em ajustes >
Entre no seu DTU W100 e pegue o ip que ele esta operando >
![Configuração MQTT](https://raw.githubusercontent.com/viniciusmbs/DTU-W100/main/3.jpeg)


Agora defina uma senha pois a padrão e admin - admin 
Suponha que a senha ficou admin senha 123456
![Configuração MQTT](https://raw.githubusercontent.com/viniciusmbs/DTU-W100/main/4.jpeg)

Para saber a porta que e padrão não mude 10081
![Configuração MQTT](https://raw.githubusercontent.com/viniciusmbs/DTU-W100/main/5.jpeg)



Ajuste do Hoymiles DTU Solar: Home Assistant Add-on
Configurações.yaml nos 3 pontos superior acima

```
dtu:
  host: 192.168.100.? #Ip de seu DTU W100
  port: 10081 # Porta liberada sempre a porta e 10081
  username: admin #User que colocou no DTU
  password: 123456  #User que colocou no DTU 
app: {}
app_mode_active: {}
app_mode_passive: {}
mqtt:
  broker: 192.168.100.? # Ip do MQTT e o mesmo de seu home assistent 
  port: 1883
  username: Vinicius # Nome que escolheu no MQTT
  password: 12345 # Senha que escoleu no seu MQTT
```

IP do MQTT e o mesmo que seu HA usa EX> http://< Seu IP>l:8123/

Repita os passos instalando o mesmo add-ons porque uma versão e estável e a outra não e não sei qual delas esta funcionando pois os programadores parou e outro continuou , Não vai dar conflito vai ser só mais um lixo que não serve no seu HA Só que uma funciona e a outra não >
Repita os passos acima em ajustes e só copiar e colar o configurações.yml
https://github.com/banny310/hoymiles-dtu-homeassistant-addon

Agora vamos ao segundo programa 
Instalei os dois também pois e a mesma coisa com o primeiro um e estável e outro não funciona >
Instale 
https://github.com/dmslabsbr/hoymiles/tree/master/stable
![Configuração MQTT](https://raw.githubusercontent.com/viniciusmbs/DTU-W100/main/6.jpeg)

Vai em ajustes >>>
3 pontos superior como editar configurações.yml

```
HOYMILES_USER: Viniciusmbs # Usuário que usa para logar. na sua planta 
HOYMILES_PASSWORD: 12345 # Usuário que usa para logar. na sua planta
HOYMILES_PLANT_ID: "67??" # ID final de sua planta 
Read_meter_data: true
External_MQTT_Server: true
MQTT_Host: 192.168.100.??? # IP de seu MQTT o mesmo do Home assistant
MQTT_User: vinicius # usuário  criada do seu MQTT
MQTT_Pass: 123456  # senha criada do seu MQTT
MQTT_TLS: false
MQTT_TLS_PORT: "8883"
DEVELOPERS_MODE: false
LOG_LEVEL: INFO
LOG_TO_FILE: false
FILE_PATH: hoymiles.log
```


O numero da sua planta e senha estão dentro do https://global.hoymiles.com/platform/home
O numero da planta esta em 
https://global.hoymiles.com/platform/station/view/detail?id=????  << Numero da planta
```
HOYMILES_USER: Viniciusmbs  # Usuário que usa para logar. na sua planta 
HOYMILES_PASSWORD: 12345  # Usuário que usa para logar na sua planta
HOYMILES_PLANT_ID: "67??" # ID final de sua planta 
```
 

Salve e inicia o add- on 
Faça os mesmos passos com o mesmo add-on como o primeiro copie e cole as configura;cões.yaml do primeiro só que nesta documentação 
https://github.com/dmslabsbr/hoymiles/tree/master/stable

![Configuração MQTT](https://raw.githubusercontent.com/viniciusmbs/DTU-W100/main/7.jpeg)


Para acessar os dados 
Vai em http://homeassistant.local:8123/config/integrations/integration/mqtt

http://homeassistant.local:8123/config/devices/device/187ea61d0800ff1237c5fdfbaa204453

La estará os sensores ai e só fazer seu card eu usei este card 

![Configuração MQTT](https://raw.githubusercontent.com/viniciusmbs/DTU-W100/main/8.jpeg)

Se vc fez tudo correto e só copiar este meu card que vai aparecer isso E tive muita dificuldade para colocar a foto do painel atrás da barra assim como esta Abaixo segue a foto pra colocar no seu /local/PainelHoy3.png

![Configuração MQTT](https://raw.githubusercontent.com/viniciusmbs/DTU-W100/main/8.png)


```
type: custom:bar-card
title: Produção Solar Hoymilies
entities:
  - entity: sensor.hoymiles_gateway_solarh_6739_real_power
    name: Produção Atual
    color: "#2196F3"
    max: 3450
    show_state: true
    show_icon: false
  - entity: sensor.hoymiles_gateway_solarh_6739_today_eq
    name: Produção Dia
    color: "#2196F3"
    max: 24
    show_state: true
    show_icon: false
  - entity: sensor.hoymiles_gateway_solarh_6739_month_eq
    name: Produção Mês
    color: "#2196F3"
    max: 650
    show_state: true
    show_icon: false
direction: up
height: 200px
stack: horizontal
width: 100%
style: |
  ha-card {
    background: none;
    border: none;
  }
card_mod:
  style: |
    bar-card-backgroundbar {
      background-image: url('/local/PainelHoy3.png'); /* Imagem do painel solar */
      background-size: cover;
      background-position: center center;
      background-repeat: no-repeat;
      border-radius: 0px; /* Sem bordas arredondadas */
    }
    bar-card-currentbar {
      background: rgba(33, 150, 243, 0.6); /* Cor atual da barra */
      border-radius: 0px; /* Sem bordas arredondadas */
      clip-path: polygon(0 100%, 100% 100%, 100% calc(100% - var(--bar-percent)), 0 calc(100% - var(--bar-percent))); /* Ajusta o preenchimento da barra */
    }
    bar-card-name, bar-card-value {
      text-shadow: 1px 1px black;
    }
```
