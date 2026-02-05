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
![Captura de tela 2024-11-mqtttt17 104358|365x500](upload://qFn5tvigRRnrVPXHKXuuzo4DRYT.jpeg)


1  instale o Hoymiles DTU Solar: Home Assistant Add-on são dois um estável e outro não estável
![Captura de tela 2024-11-17 103049|690x159](upload://pDWt8vioflWwmGomBI6KQQIjcez.jpeg)

 Instalei os dois .

Instalando o Hoymiles DTU Solar: Home Assistant Add-on
https://github.com/banny310/hoymiles-dtu-homeassistant-addon

Siga o passso a passo da documentação de como instalar ou use o app Android Fing Após instalar vá em ajustes >
Entre no seu DTU W100 e pegue o ip que ele esta operando >
![Captura de tela 2024-11-17ip105526|690x450](upload://6BBCjpNvDvp1NB3Lsvs6ZQG9roN.jpeg)


Agora defina uma senha pois a padrão e admin - admin 
Suponha que a senha ficou admin senha 123456
![Captura de tela 2024-11-1senha7 105836|690x422](upload://fZJPbUv6b3g9u2ybx39yVq2iKij.jpeg)

Para saber a porta que e padrão não mude 10081
![Captura de tela 2024-11-portaaa7 110710|690x450](upload://nVW2nzQvN1DAYKWLezmAG2kY4Ym.jpeg)



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
![Captura de tela 2024-11-171111111 111556|690x373](upload://o9gcin3JT38FTDRnYJYB1JtKPB6.jpeg)

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

![estedeoi-17 112548|690x373](upload://d33gRLtv98K3dDR2G6btdPzHSam.jpeg)


Para acessar os dados 
Vai em http://homeassistant.local:8123/config/integrations/integration/mqtt

http://homeassistant.local:8123/config/devices/device/187ea61d0800ff1237c5fdfbaa204453

La estará os sensores ai e só fazer seu card eu usei este card 

![Captura de tela 2024-11-17 11gggg3337|460x500](upload://wY72QwVi6P
