# 🌀 Programa CNC O3001 – Torneamento de Eixo Escalonado com Raios

Este repositório contém o código CNC do programa `O03006`, desenvolvido para a usinagem de um **eixo escalonado com raios** em um **Centro de Torneamento GL240M**, utilizando controle **Fanuc Oi-TD**.

---

## 🛠️ Especificações Técnicas

- **Peça**: Eixo Escalonado com Raios  
- **Máquina**: Centro de Torneamento GL240M  
- **Controle CNC**: Fanuc Oi-TD  
- **Data da Programação**: 07/06/2025  
- **Unidade de Medida**: Milímetros (G21)  
- **Avanço**: mm/rotação (G95)  
- **Sistema de Coordenadas**: G54  
- **Velocidade de Corte Constante**: G96 ativado

---

## 🧰 Ferramentas Utilizadas

| Ferramenta | Código | Tipo               | Inserto         |
|------------|--------|--------------------|-----------------|
| T01        | 0101   | Desbaste Externo   | CNMG 120408     |
| T02        | 0202   | Acabamento Externo | DNMG 150404     |

---

## 🔧 Operações do Programa

### 1. Faceamento
- Alinhamento e limpeza da face inicial da peça.
- Dois passes de desbaste + um de acabamento.

### 2. Desbaste Manual Externo
- Execução de quatro diâmetros escalonados com movimentos manuais.
- Cada estágio é seguido por reposicionamento e recuo da ferramenta.

### 3. Acabamento do Perfil
- Contorno com cones, chanfros e interpolação de raios (R2 e R3).
- Utiliza compensação de raio à direita (G42) para precisão de acabamento.

---

## 📐 Comandos Relevantes

- `G21`: Programação em milímetros  
- `G90`: Coordenadas absolutas  
- `G96`: Velocidade de corte constante  
- `G42`: Compensação de raio à direita  
- `G02` / `G03`: Interpolação circular (convexa e côncava)  
- `G92 S3000`: Limite de rotação em 3000 RPM  
- `M08` / `M09`: Controle de fluido de corte  
- `M30`: Fim de programa com reset

---

## 🗂️ Arquivo Disponível

- [`O3001.nc`](V1.PROGRAMA_O3001.nc): Código-fonte do programa em G-Code para execução direta na máquina.

---

## ✅ Observações

> O programa foi cuidadosamente comentado para facilitar a leitura, manutenção e aprendizado. Ideal para operadores, programadores CNC e estudantes da área de manufatura.

---

## 📄 Licença

Este código-fonte é fornecido apenas para fins educacionais e técnicos. A aplicação em ambiente industrial deve seguir as normas de segurança e validação da sua empresa.
