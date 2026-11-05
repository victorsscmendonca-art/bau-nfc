# Análise da V3 e rumo da V4

Sistema de coordenadas da V3, que a V4 mantém: X da esquerda para a direita (0–206), Y da frente para trás (0–156, frente em Y=0) e Z para cima. Tudo em mm.

## Medidas conferidas na V3

Dimensões externas medidas nos STLs, que batem com a tabela do projeto:

| Peça | Medida (mm) |
|---|---:|
| Corpo, incluindo dobradiças | 206 × 165 × 155 |
| Tampa, incluindo aba e dobradiças | 206 × 171 × 8 |
| Fundo falso, incluindo reforços | 199,2 × 149,2 × 8 |
| Suporte do solenoide | 44 × 58 × 37 |
| Engate da tampa | 18 × 16 × 22 |

Cotas internas tiradas do código (`fonte_original.py` e `mecanismo.py`):

- Caixa de 206 × 156, paredes e piso de 3 mm, topo das paredes em Z=151. Tampa de 3 mm (Z 151–154) com lábio interno.
- Fundo falso em Z 103–106, apoiado em abas em Z 99–103. Reforços descem até Z 98, então ficam cerca de 100 mm livres e 95 mm sob os reforços.
- Compartimento do prêmio de Z 106 a 151, ou seja, **só cerca de 45 mm de altura**.
- Janela do LCD: 70,6 × 25,6, em X 29,7 e Z 50,2. Bosses do LCD a 75 × 30 (o módulo 1602 comum tem 75 × 31).
- Região do RC522: parede afinada para 1,2 mm em 46 × 66 (X 127–173, Z 20–86).
- Furo de cabo na lateral esquerda: 16 × 10 (Y 24–40, Z 12–22).
- Dobradiças: eixo em Y=161, Z=151, pinos metálicos Ø3 de cerca de 32–35 mm.

Os STEP aberto e fechado têm 7 sólidos: as 5 peças, a fechadura estimada e o trinco. Na posição fechada, o suporte fica em X 159–203, Y 18–76, Z 110–147, e o engate em Z 129–151.

## Problemas da V3

1. **O fundo falso não sai sem desmontar a trava.** O suporte fica preso na parede direita acima do fundo (Z 110 contra o topo do fundo em 106), e o fundo ocupa toda a largura (até X 202,6).
2. **O cabo da fechadura atravessa o fundo falso.** Para tirar o fundo, é preciso desconectar o cabo.
3. **O compartimento do prêmio é baixo** (cerca de 45 mm), e o suporte fica exposto dentro dele, ocupando 44 × 58 mm. O prêmio pode encostar no mecanismo.
4. **Há parafusos aparentes:** 4 na lateral direita (suporte) e 2 no topo da tampa (engate).
5. **O trinco corre em Y**, então o arco da tampa tem uma pequena componente na direção do trinco. A V3 verificou que funciona no CAD, mas só com medidas estimadas.
6. O acabamento é de caixa reta, sem cantos arredondados. O LCD fica numa janela simples e não há marcação para o cartão.

## O que vale reaproveitar

- A envoltória de 206 × 156 × 151 cabe em mesa de 256 mm com folga para brim.
- As dobradiças traseiras com pino metálico Ø3.
- A trava perto da **frente** da caixa. É o ponto mais distante da dobradiça, onde o engate desce quase na vertical (raio de cerca de 130–150 mm).
- O princípio do engate com janela: o chanfro do trinco fica para cima e recebe a peça que desce, e a face reta de baixo retém a tampa.
- A lógica da verificação (`verificar.py`): varredura da tampa, retração mínima do trinco a cada 0,125° e bloqueio com o trinco estendido.
- O suporte e o engate como peças separadas e substituíveis.

## Direção proposta para a V4 (a confirmar na etapa 1)

- **Torre da trava no canto frontal direito**, integrada ao corpo e oca. A fechadura vai num cartucho que entra por cima e é preso com 2 parafusos acessíveis com a tampa aberta. Os fios descem por dentro da torre até a eletrônica, sem atravessar o fundo falso. O fundo falso tem um recorte no canto e sai sem desmontar nada.
- **Engate preso por baixo da tampa**, sem parafusos aparentes. A tampa passa a ter cerca de 6 mm de espessura.
- **Fundo falso mais baixo** (proposta: topo em Z ≈ 88). A eletrônica fica com cerca de 80 mm livres e o prêmio ganha cerca de 60 mm. Essa mudança afeta o espaço interno e precisa de aprovação.
- **Frente:** LCD à esquerda com moldura chanfrada e encaixe para a borda metálica do display. À direita, alvo do cartão com ícone discreto gravado. O RC522 fica atrás de cerca de 1,6 mm de plástico, preso em trilhos deslizantes, sem depender das furações da placa.
- Cantos verticais com R8, chanfro na base contra pé de elefante, frisos decorativos na altura do fundo falso e rebaixo para o dedo na frente.

## Medidas da fechadura a confirmar na peça real

Todas em mm, com paquímetro. Com o trinco **estendido**, ou seja, sem energia:

1. **Furos ou rasgos das abas:** quantos são e se são redondos ou oblongos (nesse caso, comprimento × largura).
2. **Distância entre centros no sentido do comprimento** da fechadura (paralelo ao trinco). A V3 estimou 20.
3. **Distância entre centros no sentido transversal** (de uma aba à outra, atravessando o corpo). A V3 estimou 20.
4. **Largura total das abas**, de ponta a ponta. A V3 estimou 25.
5. **Espessura da chapa das abas.**
6. **Corpo:** comprimento × largura × altura, sem contar abas e trinco. A V3 estimou 30 × 16 × 18.
7. **Parafusos ou rebites no topo do corpo:** altura acima do corpo e posição de cada um, medida a partir da face de onde sai o trinco.
8. **Altura do trinco:** da face de baixo das abas até a face de baixo do trinco e até o topo do trinco junto ao corpo.
9. **Largura do trinco.**
10. **Projeção do trinco estendido**, da face do corpo até a ponta, e **projeção recolhido** (empurrando com o dedo até o fim ou energizado).
11. **Chanfro:** de que lado fica (para cima ou para o lado) e a altura da ponta do trinco no começo do chanfro.
12. **Saída dos fios:** por qual face saem e a espessura do cabo e do conector.
13. **Tensão nominal** (por exemplo, 12 V) e corrente, se estiver na etiqueta. Esses dados servem para o espaço da fonte e do driver.

Uma foto de lado e uma de cima, com uma régua junto, ajudam muito.
