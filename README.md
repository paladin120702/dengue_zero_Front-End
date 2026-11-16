# Dengue Zero

Aplicativo móvel desenvolvido em Flutter para o registro e acompanhamento de denúncias de possíveis focos de dengue. O usuário pode reportar um foco informando título, foto e localização no mapa, além de visualizar suas próprias denúncias.


## O que este projeto demonstra

Projeto móvel de estudo/portfólio relevante para **Desenvolvimento Fullstack** e **Suporte de Sistemas Júnior**:

- **Desenvolvimento:** Flutter/Dart, organização MVVM com Provider e integração com API REST.
- **Integrações:** login Google/Firebase, envio de imagem ao Storage e seleção de localização no mapa.
- **Análise de sistemas:** acompanhamento do fluxo login → imagem/localização → cadastro → consulta das denúncias.
- **Documentação e orientação de uso:** pré-requisitos e verificações por etapa para distinguir permissão do dispositivo, serviço externo e resposta da API.

Evidências: [`repositories`](lib/models/repositories), [`services`](lib/models/services), [`new_complaint`](lib/ui/new_complaint) e [`my_complaints`](lib/ui/my_complaints).

## Diagnóstico no ambiente local

| Sintoma | Conferência sugerida |
|---|---|
| Import de configuração não encontrado | Conferir `lib/firebase_options.dart` e `lib/utils/app_config.dart`, referenciados pelo código e não incluídos neste repositório. |
| Login Google não conclui | Conferir a configuração Firebase/Google da plataforma e se o provedor está habilitado no projeto de desenvolvimento. |
| Câmera ou localização indisponível | Conferir permissões do dispositivo e as configurações da plataforma. |
| Imagem não é enviada | Conferir conectividade, projeto/bucket e regras de acesso do Firebase Storage. |
| API retorna `401` | Conferir a sessão e o ID token; validar a configuração do backend correspondente. |
| App não alcança o backend | Conferir a URL em `AppConfig` e o endereço acessível pelo emulador ou dispositivo. |

A configuração de `AppConfig` deve expor os nomes usados no código (`AppConfig.` nos repositories); utilizar o endereço do próprio ambiente. Não publicar chaves privadas, tokens ou dados de usuários para demonstrar uma ocorrência.

Para uma validação manual, usar conta de teste, cadastrar uma denúncia fictícia e verificar sua exibição em “Minhas denúncias”. Registrar em qual etapa ocorreu o erro antes de alterar configurações.

## Funcionalidades

- Autenticação de usuários via Firebase Auth e login com conta Google
- Cadastro de denúncias com foto (câmera/galeria) e localização geográfica
- Seleção de localização e visualização em mapa (Google Maps)
- Upload de imagens para o Firebase Storage
- Listagem das denúncias do usuário ("Minhas denúncias")

## Tecnologias e dependências

### Plataforma
- **Flutter** (SDK Dart `>=2.17.0 <4.0.0`)
- **Dart**

### Backend / Serviços
- **Firebase Core** (`firebase_core`) — inicialização dos serviços Firebase
- **Firebase Auth** (`firebase_auth`) — autenticação de usuários
- **Google Sign In** (`google_sign_in`) — login com conta Google
- **Firebase Storage** (`firebase_storage`) — armazenamento das imagens das denúncias

### Mapas e localização
- **Google Maps Flutter** (`google_maps_flutter`) — exibição e seleção em mapa
- **Location** (`location`) — obtenção da localização do dispositivo

### Mídia e arquivos
- **Image Picker** (`image_picker`) — captura/seleção de imagens
- **Path Provider** (`path_provider`) e **Path** (`path`) — manipulação de caminhos de arquivos

### Estado e utilidades
- **Provider** (`provider`) — gerenciamento de estado (padrão MVVM)
- **HTTP** (`http`) — requisições de rede
- **Shared Preferences** (`shared_preferences`) — armazenamento local
- **Intl** (`intl`) — internacionalização e formatação
- **Cupertino Icons** (`cupertino_icons`)

### Desenvolvimento
- **Flutter Lints** (`flutter_lints`) — regras de boas práticas de código

## Arquitetura

O projeto segue o padrão **MVVM** com **Provider**, organizado em camadas:

```
lib/
├── main.dart                 # Ponto de entrada e injeção de dependências
├── firebase_options.dart     # Configuração gerada do Firebase
├── models/
│   ├── entities/             # Modelos de domínio (Denounces, PlaceLocation)
│   ├── exception/            # Exceções customizadas
│   ├── repositories/         # Repositórios (auth, denounces)
│   └── services/             # Serviços externos (Firebase Storage, Google Maps, local storage)
├── ui/
│   ├── core/themes/          # Temas da aplicação
│   ├── login/                # Tela e ViewModel de login
│   ├── home/                 # Tela inicial / overview
│   ├── new_complaint/        # Tela e ViewModel de nova denúncia
│   └── my_complaints/        # Tela e ViewModel de minhas denúncias
└── utils/                    # Configurações e rotas (app_config, app_routes)
```

## Como executar

Pré-requisitos: [Flutter SDK](https://docs.flutter.dev/get-started/install) instalado e um projeto Firebase configurado.

```bash
# Instalar as dependências
flutter pub get

# Executar o aplicativo
flutter run
```

### Configuração do Firebase

Este projeto utiliza Firebase. É necessário ter o arquivo `lib/firebase_options.dart` configurado (gerado pela [FlutterFire CLI](https://firebase.google.com/docs/flutter/setup)) e os arquivos de plataforma correspondentes (`google-services.json` para Android e `GoogleService-Info.plist` para iOS).

Para o Google Maps, configure a chave de API nas plataformas Android e iOS.
