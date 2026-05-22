# 🚗 ALPR Android App (Reconhecimento de Placas)

Aplicativo Android focado na identificação de placas de carro em tempo real utilizando visão computacional. Desenvolvido com **Kotlin** e **Jetpack Compose**, este MVP captura frames da câmera, realiza o reconhecimento óptico de caracteres (OCR), sanitiza as leituras, e salva um histórico da localização exata das detecções utilizando GPS.

## 📱 Funcionalidades Principais

* **Preview em Tempo Real:** Interface imersiva construída com Jetpack Compose e CameraX.
* **OCR com Google ML Kit:** O aplicativo lê textos a partir da câmera e implementa uma camada de heurística avançada (Regex) para identificar formatos do Brasil:
  * Placas do **Padrão Antigo** (`LLL-NNNN`)
  * Placas do **Padrão Mercosul** (`LLLNLNN`)
* **Sanitização Inteligente:** Correção automatizada de leituras falsas comuns em OCRs de placas (ex: a letra `O` lida como o número `0`, a letra `I` lida como número `1`, e vice-versa, com base na posição esperada do caractere).
* **Anti-Duplicidade (Cooldown):** O aplicativo ignora o salvamento múltiplo de uma mesma placa enquanto a câmera permanecer voltada para ela.
* **Histórico com Localização (GPS):** Ao reconhecer a placa, a latitude e longitude exatas da captura são gravadas no banco de dados.
* **Exportação CSV:** O histórico pode ser facilmente exportado e compartilhado nativamente para o WhatsApp, Email, Drive, etc., utilizando o Android ShareSheet (`FileProvider`).

## 🛠️ Stack Tecnológica & Arquitetura

O projeto foi construído seguindo os princípios de **Clean Architecture** e **MVVM**, processando imagens em threads de background e separando responsabilidades:

* **Linguagem:** 100% Kotlin
* **Interface (UI):** Jetpack Compose
* **Injeção de Dependência:** Dagger Hilt
* **Banco de Dados Local:** Room Database
* **Câmera:** CameraX (`PreviewView` & `ImageAnalysis`)
* **Machine Learning / Visão:** Google ML Kit (Text Recognition v2)
* **Localização (GPS):** Google Play Services Location (`FusedLocationProviderClient`)
* **Gerenciamento de Permissões:** Google Accompanist
* **Programação Assíncrona:** Kotlin Coroutines & Flow

## 🚀 Como Executar o Projeto

1. Certifique-se de que possui o **Android Studio** instalado.
2. Clone o repositório para sua máquina local:
   ```bash
   git clone https://github.com/michaelJr-SkyInformatica/placa.git
   ```
3. Abra a pasta do projeto no Android Studio.
4. Aguarde o *Gradle Sync* baixar todas as dependências necessárias.
5. Conecte um dispositivo físico (ou inicie um emulador com câmera configurada).
6. Clique em **Run 'app'** (`Shift + F10`).

> [!NOTE]
> **Permissões:** Ao abrir o aplicativo pela primeira vez, será solicitada permissão de acesso à Câmera e à Localização. Ambas são obrigatórias para o funcionamento pleno da ferramenta de captura e histórico.

## 🏗️ Estrutura de Diretórios Resumida

```
app/src/main/java/com/example/alpr/
 ├── camera/       # Setup do CameraX e ImageAnalysis (LicensePlateAnalyzer)
 ├── data/         # Configurações do Room Database e DAOs
 ├── di/           # Módulos de injeção de dependência do Dagger Hilt
 ├── domain/       # Modelos de dados (ex: PlateRecord)
 ├── location/     # Serviço FusedLocation para captura de GPS
 ├── ocr/          # Regras de Regex e Sanitização de Textos das Placas
 ├── theme/        # Temas, Tipografia e Cores do Jetpack Compose
 ├── ui/           # Telas (CaptureScreen, HistoryScreen) e ViewModels
 └── MainActivity  # Ponto de entrada do app (AndroidEntryPoint)
```

---

*Desenvolvido em colaboração iterativa utilizando Inteligência Artificial e a tecnologia Antigravity AI.*
