1. **Inversão das 6 flechas**. Seis flechas encontram-se dispostas numa coluna, agrupadas de forma a que o grupo de cima aponta para a direita e o de baixo para a esquerda. Queremos obter um estado em que as setas apontam para direcções alternadas. O único movimento possível é inverter simultaneamente as orientações de duas flechas adjacentes.
2. **Medindo 4 litros**. Imagine que tem dois jarros com capacidade para 3 e 5 litros. Pretende-se medir 4 litros de vinho, usando as seguintes operações: encher um jarro, esvaziar um jarro, ou verter vinho de um jarro para outro.
    #### Estados
   - Estado: (x, y)
   - Estado inicial: (0, 0)
   - Estado final: (x, 4)
    #### Operadores
   - encher o jarro de 3: `(x, y)` e `x < 3` -> `(3, y)`.
   - encher o jarro de 5: `(x, y)` e `y < 5` -> `(x, 5)`
   - esvaziar o jarro de 3: `(x, y)` e `x > 0` -> `(0, y)`
   - esvaziar o jarro de 5: `(x, y)` e `y > 0` -> `(x, 0)`
   - verter do jarro de 3 para o de 5: (x, y) e x > 0 e y < 5   
     - `(max(0, x + y - 5), min(x + y, 5))`
   - verter do jarro de 5 para o de e: (x, y) e y >0 e x < 3
     - `(min(3, x + y), max(x + y - 3, 0))`

3. **Problema verde dos jarros**. Considere uma variante do problema anterior, em que queremos minizar a água gasta ao medir 4 litros.
    #### Gastos
   - encher o jarro de 3:
     - Custo: `3 - x`
   - encher o jarro de 5:
     - Custo: `5 - y`
   - esvaziar qualquer jarro, ou verter qualquer jarro:
     - Custo: `0`

4. **Viagem no metro de lisboa**. Dado o mapa do metro de Lisboa, planeie a viagem entre duas estações, considerando que se quer minimizar os transbordos.
    #### Estados
   - Estado: `(Est, Lin)`
     - Estação: `{Est_Inicial, Est_Final, Est_Interface}`
     - Linha: `{azul, amarela, vermelha, verde, None}`
   - Estado inicial: `(Est_Inicial, Lin_Inicial)`
   - Estado final: `(Est_Final, Lin_Final)`
    #### Função objetivo
   - `(Est, Lin) -> Est == Est_Final`
    #### Operadores
   - `SelLinha(linha) -> (Est, None)` seleciona uma linha para a Est_Inicial
     - **SE** a Lin_Inicial for `None`, ou
     - **SE** está na mesma linha da Est_Final
     - Custo 0
   - `Muda(est_interface, nova_linha)` viaja para a `est_interface` e muda para a `nova_linha`
     - **SE** a Est_Final não está na mesma linha
     - Custo 0
   - `Sai(Est_Final)`
     - **SE** a Est_Final está na mesma linha da estação corrente
     - Custo 0
5. **Inversão do triângulo de moedas**. Dado um triângulo formado por 10 moedas, (ver figuras seguintes), o objectivo do problema consiste em inverter este triângulo através de um número mínimo de operações. A inicial única operação válida corresponde ao deslocamento de uma das moedas de uma fila para uma outra qualquer.
    #### Estados
   - Estado: `[N1, N2, N3, N4]`
   - Estado Inicial: `[1, 2, 3, 4]`
   - Estado Final: `[4, 3, 2, 1]`
   #### Operadores
     - `Mover(i, j)` move uma moeda da linha `i` para a linha `j`
       - `S[i] -= 1; S[j] += 1`
       - **SE** `S[j] < 4`, e
       - **SE** `S[i] > 1`
       - Custo: 1
     - `Topo(i)` move a moeda da linha `i` (remove essa linha) e cria uma nova linha no topo, com essa moeda
       - **SE** `S[i] == 1`
       - Custo: 1
     - `Base(i)` move a moeda da linha `i` (remove essa linha) e cria uma nova linha na base, com essa moeda
       - **SE** `S[i] == 1`
       - Custo: 1
   #### Solução
   ```py
   [1, 2, 3, 4] # aplicar Base(1)
   [2, 3, 4, 1] # aplicar Muda(3, 1)
   [3, 3, 3, 1] # Muda(3, 1)
   [4, 3, 2, 1]
   ```