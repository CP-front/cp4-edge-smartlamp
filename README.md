# 💡 Projeto IoT - Smart Lamp com FIWARE e MQTT  

---

## 📌 Descrição do Projeto  
Este projeto implementa uma **Smart Lamp** (Lâmpada Inteligente) conectada à Internet das Coisas (**IoT**) utilizando **ESP32**, **MQTT** e a **plataforma FIWARE**.  

A Smart Lamp pode ser **ligada e desligada remotamente** via **comandos MQTT**, além de enviar continuamente o **estado do LED** e os **valores de luminosidade** para o **Broker MQTT**, permitindo integração com aplicações externas, dashboards e sistemas de automação.  

---

## ⚙️ Funcionalidades  
✔️ Conexão Wi-Fi com autenticação.  
✔️ Conexão ao **Broker MQTT**.  
✔️ Recebimento de comandos MQTT para **ligar/desligar** a lâmpada.  
✔️ Publicação do **estado atual da lâmpada**.  
✔️ Leitura da **luminosidade ambiente** (sensor analógico).  
✔️ Publicação dos valores de luminosidade em tempo real.  
✔️ Reconexão automática ao **Wi-Fi** e **MQTT** em caso de falha.  

---

## 🔧 Componentes Utilizados  
| Componente          | Quantidade | Função no Projeto |
|---------------------|------------|-------------------|
| ESP32               | 1          | Microcontrolador principal com Wi-Fi integrado |
| LED (Onboard D4)    | 1          | Representa a lâmpada inteligente |
| Potenciômetro / LDR | 1          | Simula sensor de luminosidade |
| Broker MQTT (FIWARE/Orion) | 1 | Comunicação entre IoT e Backend |
| Jumpers             | -          | Conexões de teste |

---

## 📦 Dependências do Projeto  
- **Linguagem:** C++ (Arduino IDE / PlatformIO)  
- **Bibliotecas:**  
  - `WiFi.h` → Gerencia a conexão Wi-Fi.  
  - `PubSubClient.h` → Implementa o protocolo MQTT no ESP32.  

---

## 🏗️ Arquitetura e Contexto do Projeto  

### 📌 Arquitetura em Camadas  
1. **Camada IoT (Dispositivo Físico)**  
   - ESP32 conectado via Wi-Fi.  
   - Sensor de luminosidade e LED (Smart Lamp).  

2. **Camada Backend (Comunicação e Middleware)**  
   - **Broker MQTT** no FIWARE (recebe/publica mensagens).  
   - Context Broker (Orion) gerenciando entidades IoT.  

3. **Camada Aplicação (Interface do Usuário)**  
   - Usuário envia comandos de ligar/desligar via Postman ou interface FIWARE.  
   - Aplicações/dashboards podem consumir dados de luminosidade.  

---

### 📊 Diagrama da Arquitetura  
```plaintext
[Usuário/Postman] <---> [FIWARE Orion/IoT Agent] <---> [Broker MQTT] <---> [ESP32 Smart Lamp]
```

---

## 📂 Estrutura do Projeto
```cpp
📁 smart-lamp-fiware
│── 📄 README.md            # Documentação do projeto
│── 📄 smartlamp.ino        # Código principal para o ESP32
│── 📁 /lib                 # Bibliotecas adicionais
│── 📁 /img                 # Imagens e diagramas do projeto
```

---

## 🛠️ Como Montar e Replicar este Projeto

### 1️⃣ Montagem do Circuito

- Conectar potenciômetro/LDR ao pino 34 (ADC) do ESP32.

- Utilizar o LED onboard (D4) para simular a lâmpada.

### 2️⃣ Configuração do Código
- Editar no código os parâmetros:

   ```cpp
   const char* default_SSID = "sua_rede_wifi";
   const char* default_PASSWORD = "sua_senha_wifi";
   const char* default_BROKER_MQTT = "ip_host_fiware";
   const int default_BROKER_PORT = 1883;
   ```

### 3️⃣ Execução do Sistema

- Carregar o código no ESP32.
- Iniciar o FIWARE + MQTT Broker na VM/Docker:

   ```cpp
   sudo docker-compose up -d
   ```

- Usar o Postman para enviar comandos e monitorar a lâmpada.

---

## 🧠 Lógica de Sistema
1. O ESP32 conecta ao Wi-Fi.

2. O ESP32 conecta ao Broker MQTT.

3. O dispositivo escuta no tópico:
   ```cpp
   /TEF/lamp001/cmd
   ```

4. Se recebe comando lamp001@on| → Liga LED.

5. Se recebe comando lamp001@off| → Desliga LED.

6. Publica estado em:
   ```cpp
   /TEF/lamp001/attrs
   ```

e luminosidade em:
   ```cpp
   /TEF/lamp001/attrs/l
   ```

---

## 🖥️ Operação
### Comandos de Teste (via Postman / MQTT)
- #### Ligar Lâmpada
   ```cpp
   lamp001@on|
   ```

- #### Desligar Lâmpada
   ```
   lamp001@off|
   ```

---

## ⚠️ Notas de Segurança
- ***Não compartilhar credenciais Wi-Fi e Broker*** em repositórios públicos.

- ***Alterar o ID MQTT*** ao utilizar múltiplos dispositivos.

- ***Verificar firewall da rede*** para permitir portas MQTT (1883).

---

## 📚 Recursos e Materiais
- [FIWARE Documentation]()

- [MQTT Protocol]()

- [ESP32 Arduino Core]()

---

## 📷 Imagem do Protótipo
<img src="" alt=""></img>

---

## 🎥 Vídeo Explicativo

📺 Assista ao vídeo explicando o projeto: [Link para o vídeo](https://youtu.be/s1YcKbS_FjU?si=RLxZdAGxY7t1xoHK)

---

## 👨‍💻 Autores

- Projeto desenvolvido por **Visionary Solutions** para a disciplina Edge Computing - FIAP.
- Equipe: Arthur Araujo Tenorio, Breno Gonçalves Báo, Rodrigo Cardoso Tadeo, Vinicius Cavalcanti dos Reis
- Professor: Dr. Fábio H. Cabrini

---

## 📢 Licença

Este projeto é livre para uso educacional. Para uso comercial, consulte os autores.