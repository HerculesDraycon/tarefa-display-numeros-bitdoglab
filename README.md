# Tarefa - Numeros Display - BitDogLab

**LINK DO VÍDEO ENSAIO:** https://drive.google.com/file/d/10BkMvR32o6eq8GaLNOp_hyquJgoV68HJ/view?usp=sharing

# Documentação do Código

## **Descrição Geral**

O código controla um LED RGB Cathode e uma matriz de LEDs a partir de dois botões, sendo capaz de:
- Modularizar diferentes frames, passando por estados da matriz.
- Configurar e manipular LEDs individualmente ou em grupo.
- Permitir o controle interativo por meio dos botões A e B da BitDogLAb.
- Ascender os LEDs em diferentes cores e intensidades.

## **Bibliotecas Utilizadas**

### **Padrão do C**
- `<stdio.h>`: Manipulação de entrada/saída.

### **Pico SDK**
- `pico/stdlib.h`: Configuração padrão para Raspberry Pi Pico.
- `hardware/pio.h`: Manipulação de entradas e saídas programáveis (PIO).
- `hardware/clocks.h`: Controle do clock do sistema.

### **Customizadas**
- `"lib/frames.h"`: Frames que representam os números exibidos na matriz de LEDs
- `"pio_matrix.pio.h"`: Configuração do PIO para controle da matriz de LEDs.

## **Constantes**
- `DEBOUNCE_LINE`: Define em microsegundos o tempo a ser utilizado no debounce dos botões.
- `NUMERO_DE_LEDS`: Define o número de LEDs na matriz.
- `BTN_A`: Define o pino de entrada do botão A
- `BTN_B`: Define o pino de entrada do botão B
- `OUT_PINO`: Define o pino de saída utilizado pelo PIO.
- `GREEN_PINO`: Define o pino de saída utilizado pelo LED verde do RGB.
- `BLUE_PINO`: Define o pino de saída utilizado pelo LED azul do RGB.
- `RED_PINO`: Define o pino de saída utilizado pelo LED vermelho do RGB.

## **Funções**

### **1. Manipulação de LEDs**
#### `uint32_t matrix_rgb(double r, double g, double b)`
- **Descrição**: Converte os valores de vermelho (r), verde (g), e azul (b) para um formato hexadecimal de 32 bits.
- **Parâmetros**:
  - `r`, `g`, `b`: Intensidades de vermelho, verde e azul (0.0 a 1.0).
- **Retorno**: Valor RGB no formato hexadecimal.
- **Uso**: Criação de cores para o LED.

---

#### `void desenho_pio(double *desenho, uint32_t valor_led, PIO pio, uint sm, double r, double g, double b)`
- **Descrição**: Atualiza os LEDs com base em um padrão (`desenho`), aplicando uma cor uniforme.
- **Parâmetros**:
  - `desenho`: Array com o padrão dos LEDs.
  - `valor_led`: Valor RGB.
  - `pio`: Instância do PIO.
  - `sm`: State Machine do PIO.
  - `r`, `g`, `b`: Intensidades de vermelho, verde e azul.

### **2. Controle dos Botões**

#### `button_callback(uint gpio, uint32_t events)`
- **Descrição**: Realiza as rotinas de interrupção (IRQ) e executa a sequência de instruções ao respectivo botão pressionado.
- **Parâmetros**:
  - `gpio`: uint que corresponde ao pino GPIO em que o botão está conectado e gerou a interrupção.
  - `events`: Passa as informações sobre que tipo evento na GPIO ocorreu.


### **3. Controle do LED RGB**

#### `pisca_led_rgb()`
- **Descrição**: Ascende e apaga o LED respectivo do RGB Cathode conectado com o intervalo de tempo exigido.
- **Parâmetros**:
  Devido à rotina imutável na execução do programa, não há parâmetros.

### **4. Função Principal (`main`)**
- **Descrição**:
  - Configura o clock e inicializa periféricos.
  - Inicializa a matriz de LEDs desligados.
  - Entra em um loop infinito que:
    1. Chama a função de manter o LED vermelho piscando 5 vezes por segundo.
    2. Lê através do switch o estado atual do contador.
    3. Executa a função correspondente para seu estado.
    3. Verifica os limites dos estados do contador.
- **Destaques**:
  - Inicializa o PIO com a configuração `pio_matrix`.

## **Fluxo do programa**

- O LED vermelho mantém-se piscando 5 vezes por segundo desde o início da execução do programa e continua com esse comportamento sem nenhuma objeção possível.

- Caso o **Botão A** seja pressioando, um número é incrementado na tela.

- Caso o **Botão B** seja pressioanado, um número e decrementado na tela.