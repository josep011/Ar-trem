# Enoden 305 — diorama 3D

Diorama interativo em 3D de um bonde do Enoden (江ノ電 305) passando por uma rua japonesa, feito em Three.js, numa página só, sem etapa de build.

![Dia](docs/preview-dia.png)
![Noite](docs/preview-noite.png)
![AR em cima do QR](docs/preview-ar-qr.png)

## O que tem

- **Bonde 305** (sem o pantógrafo):
  - carroceria com janelas e portas abertas na chapa e vidros de verdade (transmissão física);
  - interior com bancos, alças e luminárias;
  - pintura metálica com verniz, sujeira e relevo;
  - truques com rodas que giram.
- **Tremor realista:** vibração contínua (motor, rodas e trilho) somada às pancadas nas juntas do trilho, passando por uma suspensão amortecida em cada truque.
- **Rua:**
  - asfalto com trincas e manchas de óleo;
  - faixa de concreto com o trilho embutido;
  - guias, calçadas e bueiros;
  - poste com fiação e luminárias.
- **Cenário (da esquerda para a direita):**
  - barbearia de azulejo e loja de madeira com gatos da sorte e lanterna de papel;
  - máquina de bebidas;
  - ponto de ônibus de chapa ondulada com a caixa vermelha de mangueira;
  - prédio de madeira com portas de correr de vidro aramado, bicicletas, caixas e palete;
  - luminária de tomate de 1 m com luz amarela por dentro;
  - loja de conveniência na esquina (marca fictícia) com dois carros estacionados (genéricos, estilo hatch anos 90 e roadster);
  - rua transversal com faixa de pedestres.
- **Horários:**
  - *Dia*, *Tarde* e *Noite*: muda o sol, o céu refletido e a exposição;
  - acende pontos de luz quentes (amarelos) e frios (brancos);
  - os faróis do bonde iluminam a rua.
- **Acabamento leve** (quase sem custo por quadro):
  - sombras de contato pré-desenhadas sob carros, postes, bicicletas, bonde e no pé das paredes;
  - sujeira respingada na base das fachadas;
  - poças d'água que aparecem à tarde e à noite, com o asfalto mais brilhante;
  - halo de brilho em volta das luzes à noite (sprites, sem pós-processamento);
  - fios ligando o poste aos prédios e ao poste de rua;
  - pétalas de sakura caindo (botão "Pétalas").
- **Passagem de nível (踏切)** na rua transversal: luzes vermelhas alternadas, cancela que desce quando o bonde se aproxima e sino.
- **Som** (botão "Som", desligado por padrão): ronco e chiado do trilho, zumbido do motor, batidas nas juntas, sino da passagem de nível, cigarras de dia e grilos à noite. Tudo sintetizado na hora, sem arquivos de áudio.
- **Efeito miniatura** (botão "Miniatura"): desfoque em cima e embaixo, como foto de maquete.
- **Leveza:**
  - as peças estáticas com o mesmo material são juntadas ao carregar (de ~4100 para ~840 chamadas de desenho por quadro, sem mudar a imagem);
  - a qualidade se ajusta sozinha: se o FPS cair, reduz resolução, sombras e pétalas. No celular já começa no nível médio;
  - para forçar: `?q=high`, `?q=mid` ou `?q=low` no endereço.
- **Controles:**
  - reproduzir, pausar, reiniciar e repetir;
  - velocidade de 10 a 60 km/h;
  - câmeras lateral, 3/4, rente ao trilho e uma que acompanha o bonde.

## Realidade aumentada

Há dois jeitos de ver o diorama em AR.

### Em cima do QR code (`scan.html`)

1. Abra `ar.html` no computador: aparece um QR em forma de bilhete de trem (também dá para baixar em PNG e imprimir).
2. Escaneie com o celular e toque em **Abrir a câmera**.
3. Mire de novo no mesmo QR: o diorama aparece em cima dele, com o bonde indo e voltando e a cancela da passagem de nível descendo.

- Funciona no **iPhone (Safari)** e no **Android (Chrome)**, com animação nos dois.
- A câmera lê o QR com o [jsQR](https://github.com/cozmo/jsQR) (em `vendor/`, licença Apache 2.0) e calcula a posição e a inclinação a partir dos quatro cantos do código. Qualquer QR serve como base.
- Tem botão de **foto** (salva ou compartilha a imagem com o diorama) e controle de **tamanho**.
- **Dicas:** use boa luz, deixe o QR inteiro na tela e não muito pequeno. Se perder o QR por mais de 1,5 s o diorama some e volta quando encontrar de novo.

### No chão ou na mesa (`ar.html`)

O botão **Ver na minha mesa** abre o AR do próprio celular (model-viewer): você aponta para o chão e a maquete fica ali.

- **Tamanho:** o modelo `enoden-diorama.glb` tem 9,8 MB e está em escala de maquete (1:45, cerca de 1 m de comprimento). Dá para mudar o tamanho com dois dedos. O relevo das texturas vai como normal map.
- **Android:** use o Chrome com o “Google Play Services for AR”. Abre em WebXR ou no Scene Viewer, com o bonde animado.
- **iPhone:** use o Safari. Abre no AR Quick Look, mas a animação do bonde não toca (o diorama aparece parado).
- **Limitação:** o AR precisa de HTTPS, por isso só funciona depois de publicar no GitHub Pages (abrindo o arquivo direto no computador não funciona).

## Como rodar

O projeto é um único `index.html`. O Three.js 0.160.0 vem da CDN do jsDelivr, então é preciso estar conectado à internet.

- **Direto:** abra o `index.html` no navegador (Chrome, Edge ou Firefox recentes).
- **Servidor local** (recomendado):
  ```bash
  npx serve .
  # ou
  python3 -m http.server 8000
  ```
  e acesse `http://localhost:8000`.

## Publicar no GitHub Pages

1. Crie um repositório no GitHub e envie esta pasta:
   ```bash
   git remote add origin https://github.com/SEU-USUARIO/enoden-diorama.git
   git branch -M main
   git push -u origin main
   ```
2. No repositório, vá em **Settings → Pages**.
3. Em **Branch**, escolha `main` e a pasta `/ (root)`, e salve.
4. Em um ou dois minutos o diorama estará em `https://SEU-USUARIO.github.io/enoden-diorama/`.

## Estrutura

```
index.html          cena completa (HTML + CSS + JavaScript)
ar.html             QR em forma de bilhete + AR no chão (model-viewer)
scan.html           AR em cima do QR (câmera + jsQR + Three.js)
vendor/jsQR.js      leitor de QR usado no scan.html
enoden-diorama.glb  modelo 3D animado usado no AR
docs/               imagens de prévia usadas neste README
```

Todas as texturas são geradas por código (canvas), então não há arquivos de imagem para carregar.

## Desempenho

A cena usa vidro com transmissão, sombras de até 4096 px e várias luzes à noite. As peças estáticas são juntadas ao carregar e a qualidade se ajusta sozinha, então deve rodar bem em celulares intermediários. Em aparelhos muito fracos, use `?q=low`.
