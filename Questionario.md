# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
Quando existem componentes com diferentes arquiteturas e deseja-se fazer uma compilação entre elas, é necessário que haja uma "tradução" das instruções de uma arquitetura para que ela rode na outra.
 
## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
Descreve ações e requisitos que devem ser true quando a função main é chamada. Esse código declara por exemplo o vetor de intrrupções, define o ponto de entrada da aplicação., configura periféricos e sistema de clock, entre outros.

## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
Durante o processo de compilação, os arquivos fonte geram arquivos objetos. O makefile é um código que serve para automatizar o processo de criação desses arquivos objetos de maneira eficiente e organizadas, de forma que a cada nova compilação seja feita de forma simples e sem problemas com esses arquivos, levando em consideração as dependências entre os arquivos eetc.

#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
"make" é como se fosse um atalho que executa todas as linhas do codigo makefile. Esse utilitário usa o ambiente de execução dele próprio, isso significa que as variáveis de ambiente ali contidas sobrepoem variáveis de mesmo nome no ambiente existente.   

#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
target : dependência1 dependência2 (pulaLinha)
(tab)receita

#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
Depende do tipo de dependência. Se for uma variável ela é definida da forma que se define uma variável, se for um arquivo deve ser criado um arquivo anteriormente. As dependências são colocadas após o ":" que procede o target. O que ocorre é que target é a ação ou o arquivo que deseja-se gerar. As dependências são arquivos ou variáveis utilizadas para criar o target seguindo a receita proposta.
 
#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
As regras são as receitas para realizar determinadas ações. As regras explicitas deixam claro e especificado como as ações devem ser realizadas, ja as regras implicitas são construídas de forma "resumida" e entendidas pelo makefile através de padrões ou com a utilização de sufixos.

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
Instruções Thumb tem a mesma função das instruções ARM porém são menores tendo apenas 16 bits, enquanto instruções ARM tem 32 bits. E ntretanto, em alguns casos utilizá-las pode aumentar o numero de instruções que o processador deve executar. Para aumentar a eficiência, utiliza-se os dois tipos de instruções, reduzindo significamente o tamanho do código e mantendo um baixo consumo de energia.

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Memory***.
 O  processador  opera  com   dados  mantidos  em  registradores (Register/Memory).  Instruções   separadas de carregamento e armazenamento (Load/Store) transferem dados entre o banco de registradores e a memória externa. Os acessos à memória são lentos, portanto, separar os acessos à memória do processamento de dados oferece uma vantagem, pois pode-se usar os itens de dados mantidos no banco de registradores várias vezes, sem precisar de vários acessos à memória, aumentando a eficiência na execução do código. 

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.
Existem dois modos de operação (Thumb e Debug) e dois níveis de execução (Handler e Thumb). No modo Debug o processador é suspenso e entra em modo de depuração. No modo thumb o processador está em execução e executa os códigos. A diferença entre os níveis de execução é que no modo handler as interrupções são tratadas e há acesso privilegiado a regiões da memória, e no modo Thread ocorre as execuções normais do código, podendo ou não ter acesso privilegiado. 

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.
Quando uma interrupção ou exceção é acionada o processador pausa a execução do código, executa a ação especificada naquela interrupção (ISR) e depois volta a executar o código a partir de onde havia sido interrompido. Os diferentes tipos de exceção são reset, NMI (non-maskable interrupt), hardFault, SVCall e interrupt. As exceções são associadas ao seu nível de prioridade. A estratégia de group priority e sub priority funciona de forma que em cada nível interrupções com características semelhantes sejam agrupadas e dentro desse nível sejam ordenadas de acordo com a prioridade entre elas, a chamada subprioridade.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?
Registradores agem como armazenamento rapido de memoria local para todas as operações de processamentos de dados. O CPSR monitora e controla operações internas contendo bits de estado do processador como bits de controle de interrupção. O SPSR  armazena temporariamente o conteudo do CPSR enquanto uma execução é processada. Na execução de uma rotina especial de retorno do programa faz com que o conteúdo salvo no SPSR seja copiado pra o CPSR.

### (f) Qual a finalidade do **LR** (***Link Register***)?

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?

### (h) O que é a tabela de vetores de interrupção?
o NVIC é um vetor que funciona como uma lista de interrupções ordenadas de acordo com suas prioridades. 

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?
As interrupções são necessárias para que o programa realize determinada ação caso algo não ocorra como deve ocorrer, elas pausam a execução até que o problema seja resolvido e após isso o programa principal volta a ser executado normalmente. Uma aplicação em tempo real seria uma interrupção acionada ao apertar um botão. 

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 


## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
