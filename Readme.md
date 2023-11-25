# DEPLOY ON IIS LOCAL - Csharp .NET 8

Passo a passo para referência, mostrando como subir uma Minimal API no servidor Web IIS (Information Internet Services).

O IIS pode estar ser habilitado na maquina Dev ou em um servidor local.

O escopo do tutorial não é a segurança, sendo apenas uma demo.

Requisitos:

- Aplicativo Web (.NET8+) publicado em uma pasta.
- Habilitar o IIS no servidor.
- Criar estrutura de pastas para o aplicativo e liberar permissões.
- Instalar o aplicativo [.NET 8 - Windows Server Hosting][WindowsServerHostingDownload]
- Reiniciar o IIS.

## Deploy do App via Terminal

1. Em sua Solution, navegue até o projeto que contém a aplicação Web (API) e execute o comando:

```csharp
dotnet publish --configuration Release
```

![Publicando][Publicando]

Os arquivos serão compilados e será gerada uma versão para produção na pasta publish.

![Build gerada][BuildGerada]

## Acessando a pasta da aplicação

1. Navegando pelo explorador de arquivos até a pasta publish, temos o executável gerado e demais dependências.

![EXE da aplicação][EXEapp]

1. Nesse projeto estou usando o SQLite. Vou copiar o banco para pasta publish (se trata apenas de uma demo. 🙂)

![Todo.db][TodoDb]

## Habilitando o IIS

1. Para habilitar o IIS em uma maquina com Windows, pressione <kbd>Win</kbd> + <kbd>R</kbd> e digite **Appwiz.cpl**.
   Agora, abra o menu **Ativar ou desativar recursos do Windows**. Marque a opção **Serviços de Informações da Internet**.

![Ativando o IIS][AtivandoIIS]

1. Feito isso, baixe e instale o aplicativo que habilita o módulo ASP.NET Core no IIS.

![Net8 Windows Server Host][NetCoreHostBundle]

1. Reinicie o IIS após a instalação.

## Criando a estrutura de pastas para APIs

1. Navegando pelo explorador de arquivos, crie uma pasta dentro do IIS:

```csharp
C:\ -> inetpub -> apis
```

![Caminho inetpub][CaminhoInetpub]

1. Libere as permissões para modificação.

![Permissão de pasta][PastaPermissao]

1. Por fim, copie e cole a pasta **publish** com sua aplicação para dentro da pasta **apis**. Renomeie a pasta para o nome do seu App.

![Todo Net8][TodoNet8]

## IIS - Publicando a aplicação Web

1. Pesquise por IIS em seu sistema e abra o gerenciador.

![Gerenciador IIS][GerenciadorIIS]

1. Clique com o botão direito do mouse e escolha **Adicionar Site...**

![Adicionar Site][AdicionarSite]

1. Defina o nome da aplicação. Em seguida, informe o caminho buscando pela estrutura de pastas. Finalize colocando uma porta disponível para aplicação.

![Configurando o Site][ConfigurandoSite]

1. Após confirmar no OK, a aplicação estará disponível e aguardando as solicitações. Abaixo usei o Thunder Client para executar um teste.

![Testando o App][TestandoApp]

[TestandoApp]: Docs/13.png

### Bom é isso por enquanto. Então, boa sorte e bons códigos. 👍

[Publicando]: Docs/01.png
[BuildGerada]: Docs/02.png
[EXEApp]: Docs/03.png
[TodoDb]: Docs/04.png
[AtivandoIIS]: Docs/05.png
[NetCoreHostBundle]: Docs/06.png
[CaminhoInetpub]: Docs/07.png
[PastaPermissao]: Docs/08.png
[TodoNet8]: Docs/09.png
[GerenciadorIIS]: Docs/10.png
[AdicionarSite]: Docs/11.png
[ConfigurandoSite]: Docs/12.png
[WindowsServerHostingDownload]: https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-8.0.0-windows-hosting-bundle-installer
