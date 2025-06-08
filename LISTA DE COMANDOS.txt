Glossário Detalhado do Programa de Torneamento (O3001)
Este glossário decodifica os comandos (códigos G, códigos M e outras funções) utilizados no programa para a usinagem do "EIXO ESCALONADO COM RAIOS" em um centro de torneamento com controle Fanuc.

Cabeçalho e Comandos Iniciais
O03006: Número do programa na memória da máquina.
(TEXTO ENTRE PARÊNTESES): Comentários. São ignorados pela máquina e servem para fornecer informações ao programador ou operador.
N10, N20, N30...: Número da linha ou bloco de programação. Facilita a leitura e a edição do código.
Códigos G (Funções Preparatórias)
Os códigos G definem a geometria do movimento da ferramenta e as condições de usinagem.

G0 (ou G00): Movimento Rápido. Move a ferramenta para uma posição designada na velocidade máxima da máquina. Usado para aproximação e afastamento, não para cortar material.

Exemplo: N80 G0 X43.0 Z3.5 - Move a ferramenta rapidamente para a coordenada X=43mm e Z=3.5mm.
G1 (ou G01): Interpolação Linear. Move a ferramenta em linha reta (um ou mais eixos) na velocidade de avanço (F) programada. Usado para usinar linhas retas, cones e facear.

Exemplo: N90 G1 X-1.6 F0.25 - Usina a face da peça movendo a ferramenta até X=-1.6mm com um avanço de 0.25 mm por rotação.
G02: Interpolação Circular Sentido Horário. Usina um arco ou raio no sentido horário.

Exemplo: N500 G02 X41.0 Z-53.0 R3.0 - Cria um raio convexo de 3mm (R3.0), movendo a ferramenta do ponto atual até as coordenadas X=41mm e Z=-53mm.
G03: Interpolação Circular Sentido Anti-horário. Usina um arco ou raio no sentido anti-horário.

Exemplo: N480 G03 X35.0 Z-40.0 R2.0 - Cria um raio côncavo de 2mm (R2.0), movendo a ferramenta do ponto atual até as coordenadas X=35mm e Z=-40mm.
G21: Programação em Milímetros. Define que todas as unidades de medida do programa serão em milímetros (mm).

G40: Cancela Compensação de Raio da Ferramenta. Desativa a compensação de raio (G41/G42). É uma prática de segurança para garantir que não haja movimentos inesperados no início ou no fim de um perfil.

G42: Compensação de Raio da Ferramenta à Direita. Ajusta automaticamente a trajetória da ferramenta para a direita em relação ao perfil programado, compensando o raio da ponta da pastilha. Essencial para usinagem de perfis de acabamento com precisão.

Exemplo: N430 G42 G1 Z0.0 F0.15 - Ativa a compensação à direita antes de iniciar o corte do perfil.
G54: Corretor de Origem (ou "Zero Peça"). Ativa o primeiro sistema de coordenadas de trabalho. Ele informa à máquina a localização exata da face da peça (ponto Z=0) e do seu centro de rotação (X=0).

G80: Cancela Ciclo Fixo. Desativa qualquer ciclo fixo de usinagem que possa estar ativo.

G90: Coordenadas Absolutas. Define que todas as coordenadas (X, Z) no programa são medidas a partir do ponto zero da peça (G54).

G92: Limite de Rotação do Fuso. Estabelece uma rotação máxima (RPM) para o fuso, prevenindo que a rotação ultrapasse um limite seguro quando o G96 está ativo em diâmetros pequenos.

Exemplo: N50 G92 S3000 - Limita a rotação da placa em 3000 RPM.
G95: Avanço por Rotação. Define que a unidade de avanço (F) será em milímetros por rotação (mm/rot).

G96: Velocidade de Corte Constante (V.C.C.). A máquina ajusta automaticamente a rotação (RPM) do fuso com base no diâmetro que a ferramenta está usinando, mantendo a velocidade de corte (em metros por minuto) constante. Isso melhora o acabamento superficial e a vida útil da ferramenta.

Exemplo: N40 G96 S250 - Ativa a V.C.C. com um valor de 250 metros por minuto.
Códigos M (Funções Miscelâneas)
Os códigos M controlam funções auxiliares da máquina, como ligar/desligar o fuso e o fluido de corte.

M03: Ligar Fuso no Sentido Horário.
M04: Ligar Fuso no Sentido Anti-horário. O programa usa este comando.
Exemplo: N40 G96 S250 M04 - Liga o fuso no sentido anti-horário.
M05: Desligar Fuso. Para a rotação da placa.
M08: Ligar Fluido de Corte. Ativa a refrigeração (óleo solúvel).
M09: Desligar Fluido de Corte.
M30: Fim de Programa e Reset. Finaliza o programa, desliga as funções auxiliares e retorna o cursor para o início do código, deixando a máquina pronta para uma nova peça.
Outros Comandos e Parâmetros
T (Tool): Seleção de Ferramenta e Corretor.

Formato: Txx_yy_
xx: Número da ferramenta na torre.
yy: Número do corretor de geometria e desgaste da ferramenta.
Exemplo: N30 T0101 - Seleciona a ferramenta 1 (desbaste) e ativa seu respectivo corretor (01). N380 T0202 - Seleciona a ferramenta 2 (acabamento) e ativa seu corretor (02).
S (Speed): Velocidade.

Quando usado com G96, define a velocidade de corte constante em metros por minuto (m/min).
Quando usado com G97 (não presente neste código), define a rotação fixa em RPM.
Quando usado com G92, define o limite máximo de RPM.
F (Feedrate): Avanço. Define a velocidade de avanço da ferramenta. No contexto deste programa (G95), a unidade é milímetros por rotação (mm/rot).

Exemplo: F0.25 (desbaste), F0.1 (acabamento de face), F0.15 (acabamento de perfil).
X, Z: Coordenadas dos Eixos.

X: Define a posição no eixo transversal (diâmetro da peça).
Z: Define a posição no eixo longitudinal (comprimento da peça).
R: Raio. Usado com os códigos G02 e G03 para definir o valor do raio a ser usinado.

Exemplo: R2.0 (Raio de 2mm), R3.0 (Raio de 3mm).
%: Símbolo de Início/Fim de Programa. Marca o início e o fim do arquivo de programa para transmissão de dados.