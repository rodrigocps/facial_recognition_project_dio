## PROJETO DIO - Desenvolvimento de Sistema de Reconhecimento Facial Multi-Pessoa

### Visão Geral

Este projeto implementa um **sistema robusto de reconhecimento facial** desenvolvido para fins educacionais. Ele é construído sobre modelos de *deep learning* de ponta para detecção e extração de *embeddings* faciais, combinados com um classificador de *machine learning* clássico para a identificação.

O objetivo é identificar com precisão indivíduos conhecidos (cadastrados) em um conjunto de dados, tanto em imagens quanto em *streams* de vídeo. O sistema foi projetado para ser altamente confiável, tornando-o ideal para projetos institucionais ou escolares.

---

### Como Funciona

O processo de reconhecimento é dividido em duas fases principais: **Treinamento (Cadastro)** e **Reconhecimento (Previsão)**.

#### 1. Fase de Treinamento:
1.  **Detecção Facial (MTCNN):** O sistema processa o conjunto de dados de imagens, usando o modelo **MTCNN** (*Multi-task Cascaded Convolutional Networks*) para localizar e recortar com precisão os rostos em cada imagem.
2.  **Extração de Embedding (FaceNet):** Os rostos recortados são alimentados no modelo **FaceNet**, que converte cada face em um vetor de 128 dimensões (o "embedding facial"). Este vetor representa matematicamente as características únicas do rosto do indivíduo.
3.  **Classificação (SVM):** Estes *embeddings*, juntamente com o nome da pessoa (*label*), são usados para treinar um classificador **Support Vector Machine (SVM)**. O SVM aprende as fronteiras de separação entre as diferentes classes de pessoas no espaço de *embeddings*.
4.  **Salvamento do Modelo:** O modelo SVM treinado e o *Label Encoder* (usado para mapear nomes para IDs numéricos) são salvos usando `pickle` para uso posterior.

#### 2. Fase de Reconhecimento:
1.  O sistema lê uma nova imagem ou quadro de vídeo.
2.  **Detecção Facial e Embedding:** Ele repete os passos de detecção (MTCNN) e extração de *embedding* (FaceNet) na face desconhecida.
3.  **Previsão:** O novo *embedding* facial é alimentado no **modelo SVM** salvo para prever a identidade.
4.  **Verificação de Confiança:** A previsão é acompanhada por uma pontuação de confiança. Se a confiança exceder um limiar definido (por exemplo, 60%), a pessoa é identificada; caso contrário, ela é rotulada como "**Desconhecido**".
5.  **Resultado:** O resultado (nome e confiança) é desenhado na imagem ou no quadro de vídeo.

---

### Tecnologias e Bibliotecas

| Categoria | Tecnologia | Objetivo |
| :--- | :--- | :--- |
| **Deep Learning** | **FaceNet** (via `keras-facenet`) | Extrai os *embeddings* faciais exclusivos de 128 dimensões. |
| **Detecção Facial** | **MTCNN** (*Multi-task CNN*) | Detecta e localiza rostos de forma robusta em imagens e quadros de vídeo. |
| **Machine Learning** | **Support Vector Machine (SVM)** | O classificador principal usado para distinguir entre diferentes identidades com base nos *embeddings*. |
| **Processamento de Imagem** | **OpenCV (`cv2`)** | Lida com o carregamento, redimensionamento, conversão BGR/RGB e desenho de caixas delimitadoras/texto. |
| **Essenciais** | **NumPy, Scikit-learn, Pickle** | Usados para manipulação de *arrays*, codificação de *labels* e salvamento/carregamento de modelos. |
