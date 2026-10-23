# Enoden 305 — diorama 3D

Diorama interativo em 3D de um bonde do Enoden (江ノ電 305) passando por uma rua japonesa, feito em Three.js, numa página só, sem etapa de build.

![Dia](docs/preview-dia.png)
![Noite](docs/preview-noite.png)

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
- **Controles:**
  - reproduzir, pausar, reiniciar e repetir;
  - velocidade de 10 a 60 km/h;
  - câmeras lateral, 3/4, rente ao trilho e uma que acompanha o bonde.

## Realidade aumentada (QR code)

A página `ar.html` mostra o diorama em AR: você aponta o celular para o chão ou para uma mesa, e a maquete aparece ali com o bonde indo e voltando.

- **Como abrir:** no computador, a página mostra um QR em forma de bilhete de trem. Esse QR é gerado com o endereço da própria página, então funciona em qualquer usuário do GitHub Pages. Ele também pode ser baixado em PNG para imprimir.
- **Tamanho:** o modelo `enoden-diorama.glb` tem 8,5 MB e está em escala de maquete (1:45, cerca de 1 m de comprimento). Dá para mudar o tamanho com dois dedos.
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
ar.html             realidade aumentada + QR code (model-viewer)
enoden-diorama.glb  modelo 3D animado usado no AR
docs/               imagens de prévia usadas neste README
```

Todas as texturas são geradas por código (canvas), então não há arquivos de imagem para carregar.

## Desempenho

A cena usa vidro com transmissão, sombras de 4096 px e várias luzes à noite. Roda bem em computadores com placa de vídeo comum. Em celulares mais fracos pode ficar lenta.
