# Sistema de Reconhecimento Facial

## Visão Geral

Este projeto cria um **sistema robusto para reconhecer pessoas por meio de suas faces**. Ele utiliza modelos avançados de inteligência artificial (**Deep Learning**) para encontrar os rostos e um modelo de aprendizado de máquina para identificar quem é quem.

O objetivo principal é identificar corretamente as pessoas que foram cadastradas (Vó, Vô, etc.) em fotos e vídeos, marcando como "**Desconhecido**" quem estiver de fora.

---

## Como o Sistema Reconhece

O sistema trabalha em duas etapas principais: **Treinamento** (para aprender os rostos) e **Reconhecimento** (para identificar na prática).

### 1. Treinamento: O Cadastro dos Rostos

1.  **Encontrar o Rosto (MTCNN):** O sistema varre as fotos de cadastro e usa uma rede neural (**MTCNN**) para localizar e recortar exatamente a face de cada pessoa.
2.  **Criar a "Digital Facial" (FaceNet):** Cada rosto recortado é passado para o modelo **FaceNet**, que o transforma em um código numérico único (o "*embedding*"). Pense nisso como a "impressão digital" matemática do rosto.
3.  **Aprender a Distinguir (SVM):** Estes códigos numéricos são usados para treinar o modelo **SVM (Support Vector Machine)**. O SVM aprende a diferença exata entre a "digital" de cada pessoa cadastrada.

### 2. Reconhecimento: A Identificação na Prática

1.  O sistema recebe uma nova foto ou quadro de vídeo (*frame*).
2.  **Digital e Classificação:** Repete-se o processo de Encontrar o Rosto (MTCNN) e Criar a Digital (FaceNet) para o novo rosto.
3.  **Decisão:** A nova "digital facial" é enviada ao modelo SVM, que tenta adivinhar a identidade.
4.  **Regra de Confiança:** Se a certeza da identificação for alta (acima do **limiar de confiança** definido, por exemplo, 75%), o nome é exibido. Se a certeza for baixa, a pessoa é rotulada como **Desconhecido**.

---

## Tecnologias Utilizadas

| Componente | Tecnologia | Função no Projeto |
| :--- | :--- | :--- |
| **Encontrar o Rosto** | **MTCNN** | Localiza com precisão os rostos na imagem ou vídeo. |
| **"Digital Facial"** | **FaceNet** | Cria o código numérico (*embedding*) para cada rosto. |
| **Identificador** | **SVM (Support Vector Machine)** | O modelo de Machine Learning que classifica o nome da pessoa. |
| **Base** | **OpenCV (`cv2`)** | Usado para carregar imagens/vídeos e desenhar caixas e nomes. |
| **Estrutura** | **TensorFlow, Scikit-learn** | As principais bibliotecas de Inteligência Artificial e Machine Learning. |
