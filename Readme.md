# DEPLOY ON IIS LOCAL - Csharp .NET 8

Olá Dev. 😎

Abaixo passo a passo para referência, mostrando como subir uma Minimal API e uma aplicação Web Blazor no servidor Web IIS (Information Internet Services).

O IIS pode ser habilitado na maquina Dev ou servidor local.

O escopo do tutorial não é a segurança, sendo apenas uma demo.

Requisitos:

- [Aplicativo Web][TodoNet8v2] (.NET8+) publicado em uma pasta.
- Habilitar o IIS no servidor.
- Criar estrutura de pastas no inetpub para o aplicativo.
- Liberar permissões nas pastas.
- Instalar o módulo .NET 8 - Windows Server Hosting

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

1. Feito isso, [baixe][WindowsServerHostingDownload] e instale o aplicativo que habilita o módulo ASP.NET Core no IIS.

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

## Deploy de um Blazor App

1. Crie seu projeto Blazor Web App e escolha o modo de renderização. Nesse exemplo, escolhi o Auto, que é o mais prático.

   ![BlazorRenderAuto][BlazorRenderAuto]

1. Ao criar o App Blazor, são gerados 2 projetos. Na publicação do App, é necessário apenas gerar o Release do projeto **Server**. O mesmo faz o empacotamento do projeto **Client** como uma dll.

   No projeto gerado, temos o builder services com as 2 configurações para processar o App do lado do Servidor e do Cliente.

   ![BlazorRenderServices][BlazorRenderServices]

1. Para publicar de forma rápida, utilize o comando abaixo.

   ```csharp
   dotnet publish -c Release -o blazor-web-app
   ```

   ![BlazorPublish][BlazorPublish]

1. Será gerada pasta dentro do projeto

   ![BlazorPubFolder][BlazorPubFolder]

1. Copie a pasta para o IIS e libere as permissões de segurança.

   ![BlazorFolderSec][BlazorFolderSec]

1. Abra o Gerenciador do IIS e crie um novo site.

   ![NewSiteIIS][NewSiteIIS]

1. Configure o nome do site e a porta ouvinte.

   ![SiteCfgIIS][SiteCfgIIS]

1. Abra o site no navegador para testar.

   ![BlazorRunning][BlazorRunning]

### Bom é isso por enquanto. Então, boa sorte e bons códigos. 👍

[TodoNet8v2]: https://github.com/thiagokj/TodoNet8v2
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
[TestandoApp]: Docs/13.png
[WindowsServerHostingDownload]: https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-8.0.0-windows-hosting-bundle-installer
[BlazorRenderAuto]: Docs/BlazorApp/01-blazor-render-auto.png
[BlazorRenderServices]: Docs/BlazorApp/02-blazor-render-services.png
[BlazorPublish]: Docs/BlazorApp/03-blazor-publish.png
[BlazorPubFolder]: Docs/BlazorApp/04-blazor-pub-folder.png
[BlazorFolderSec]: Docs/BlazorApp/05-blz-sec.png
[NewSiteIIS]: Docs/BlazorApp/06-iis-new-site.png
[SiteCfgIIS]: Docs/BlazorApp/07-iis-site-cfg.png
[BlazorRunning]: Docs/BlazorApp/08-blazor-running.png
