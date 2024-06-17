O vídeo tem as seguintes características:
- **Resolução:** 1920x1080
- **Duração:** 250.7 segundos (~4 minutos e 10 segundos)
- **Codec de vídeo:** H.264
- **Codec de áudio:** AAC
- **Taxa de quadros:** 30 fps
- **Taxa de bits:** 1.71 Mbps

Vou assistir ao vídeo para entender o contexto e fornecer mais detalhes relevantes. Um momento, por favor.

Atualmente, não consigo visualizar diretamente o vídeo. No entanto, com base nas informações fornecidas, posso continuar elaborando o `README.md` em português.

---

# Projeto de Integração de Sensores com Arduino

## Integrantes da Equipe
- David Gabriel Gomes (#rm556020)
- Denise Senise (#rm556006)
- Gabriel Gouvea (#rm555528)
- Miguel Kapicius (#rm556198)
- Thiago Ferreira (#rm555608)

## Visão Geral
Este projeto integra diversos sensores e componentes com um Arduino para ler e exibir dados ambientais. O projeto inclui:
- Leitura de dados de GPS.
- Medição de temperatura.
- Exibição de velocidade e temperatura em um display LCD.
- Visualização de entrada analógica com um gráfico de barras de LEDs.
- Acionamento de alarmes com base em limites de temperatura.

## Componentes Utilizados
- Arduino (modelo não especificado)
- MPU6050 (Acelerômetro e Giroscópio)
- Módulo GPS (utilizando protocolo NMEA)
- Potenciômetro
- LEDs
- Buzzer
- Display LCD LiquidCrystal_I2C (16x2)

## Bibliotecas Necessárias
- Wire.h
- MPU6050.h
- LiquidCrystal_I2C.h
- NMEA.h

## Conexões
- **MPU6050**: Conectar aos pinos I2C (SDA e SCL).
- **Módulo GPS**: Conectar ao Serial1 (TX e RX).
- **Potenciômetro**: Conectar ao pino analógico A0.
- **LEDs**: Conectar aos pinos digitais 2 a 11.
- **Buzzer**: Conectar ao pino digital 12.
- **LED de Alerta de Temperatura**: Conectar ao pino digital 13.
- **LCD**: Conectar aos pinos I2C.

## Configuração
1. **Inicializar Comunicação Serial**:
    - Serial para depuração a 115200 bps.
    - Serial1 para dados do GPS a 9600 bps.
2. **Inicializar Comunicação I2C**:
    - `Wire.begin()` para MPU6050 e LCD.
3. **Configurar Pinos**:
    - Definir pinos dos LEDs (2-11) como OUTPUT.
    - Definir pino do buzzer (12) e pino do LED de alerta (13) como OUTPUT.
4. **Inicializar Componentes**:
    - Verificar conexão do MPU6050.
    - Iniciar LCD com luz de fundo.

## Funcionalidades do Loop
1. **Processamento de Dados do GPS**:
    - Ler e decodificar dados do GPS.
    - Extrair e exibir latitude e longitude.
2. **Aquisição de Dados dos Sensores**:
    - Ler dados do acelerômetro e giroscópio do MPU6050.
    - Calcular temperatura.
    - Verificar se a temperatura excede o limite (30°C) e ativar o alarme (buzzer e LED).
3. **Cálculo de Velocidade**:
    - Calcular velocidade com base nos dados de aceleração.
    - Converter velocidade para km/h.
4. **Gráfico de Barras de LEDs**:
    - Ler valor do potenciômetro.
    - Mapear valor para o número de LEDs acesos.
    - Atualizar gráfico de barras de LEDs.
5. **Exibição no LCD**:
    - Mostrar velocidade atual e temperatura.

## Alarmes
- **Alarme de Temperatura**: Ativa quando a temperatura excede 30°C. Isso aciona:
    - LED no pino 13.
    - Buzzer no pino 12.

## Detalhamento do Código
### Variáveis Globais e Constantes
- `analogPin`: Pino analógico para o potenciômetro.
- `ledCount`: Número de LEDs.
- `ledPins[]`: Array com números dos pinos dos LEDs.
- `mpu`: Objeto MPU6050.
- `TEMP_LIMIT`: Limite de temperatura para o alarme.
- `LED_PIN`: Pino do LED para o alarme de temperatura.
- `buzzer`: Pino do buzzer.
- `velocityX`, `velocityY`, `velocityZ`: Variáveis para armazenar a velocidade.
- `lastTime`: Armazena o último tempo de leitura.
- `lcd`: Objeto LCD.
- `latitude`, `longitude`: Coordenadas GPS.
- `gps`: Objeto NMEA para dados do GPS.

### Função Setup
- Inicializa a comunicação serial, I2C e componentes sensores.
- Configura os pinos e inicializa o LCD.
- Verifica a conexão do MPU6050.

### Função Loop
- Lê continuamente os dados do GPS e atualiza as coordenadas.
- Adquire dados do sensor MPU6050.
- Calcula a temperatura e aciona o alarme se necessário.
- Calcula a velocidade com base nos dados de aceleração.
- Atualiza o gráfico de barras de LEDs com base no potenciômetro.
- Exibe a velocidade e a temperatura no LCD.

