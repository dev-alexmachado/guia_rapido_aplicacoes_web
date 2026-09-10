# Guia Rápido Aplicações Web

## Sumário

1. [O que é uma aplicação web](#o-que-é-uma-aplicação-web)
2. [Front-End](#front-end)
3. [Back-End](#back-end)

## O que é uma aplicação web

É um programa de computador como qualquer outro, mas com uma diferença: ele não é instalado na sua máquina. Ao invés disso, ele roda no seu computador através da núvem (***Cloud Computing***, também conhecido como **Computação em Núvem**), usando como plataforma não um Sistema Operacional, mas sim um **Web Browser**, também conhecido como **Navegador de Internet**.

Dessa forma, você pode usar o programa em qualquer PC que tenha acesso à Internet. Alguns desses aplicativos podem pedir autenticação de acesso via **Login** e **Senha**.

A **GUI** (**Interface Gráfica com o Usuário**), é sustentada pela linguagem **HTML**, que por sua vez é estilizado pelo **CSS**.

A maioria das aplicações web são divididas em **Front-End** e **Back-End**, mas todas elas possuem sempre o **Front-End**.

## Front-End

Também conhecida como tecnologia ***Client Side***, é formada pelo conjunto:

- **HTML**: ***H****yper****T****ext* ***M****arkup* ***L****anguage*, ou Linguagem de Marcação de Hypertexto.
- **CSS**: ***C****ascade* ***S****tyle* ***S****heet*, ou Folha de Estilo em Cascata.
- **JS**: ***J****ava****S****cript*, linguagem de programação Front-End (mas que pode ser usada também para Back-End).
- **Arquivos de Mídia**: fotos, vídeos, áudio, etc...

Essa tecnologia/parte do sistema é executada localmente no navegador do usuário, em sua própria máquina, mesmo que o sistema seja online, pois o navegador acessa o servidor de hospedagem e faz o download dos arquivos necessários para a exibição das telas do sistema no computador do usuário.

#### Funciona assim

> [!NOTE]
> O usuário faz uma requisição para o Servidor Web através de um endereço, como uma URL. O Servidor responde, e o cliente faz o download do Front-End (HTML, CSS, JS, Mídia), que é executada diretamente na máquina do usuário.
>
> Caso a conexão caia, o usuário continuará tendo acesso ao sistema, desde que não saia da tela.

~~~mermaid
graph TD
    A(Cliente/Usuário) -- Acessa --> Sistema

    subgraph Sistema [Site Estático]
        B(PC<br>---------<br>Mobile) -- Executa --> C(Navegador)
        C -- Acessa via URL --> D(Servidor Web/Serviço de Hospedagem)

        D -- Responde e envia por download --> C
        C -- Armazena temporariamente --> B
    end
~~~

> [!IMPORTANT]
> As aplicações que usam apenas *Front-End* são chamados de **Sites Estáticos**, pois não ocorre troca de dados síncrona entre cliente e servidor.

## Back-End

Back-End, também conhecido como tecnologia ***Server Side***, é a parte do sistema que roda exclusivamente no servidor, fornecendo de forma síncrona os dados solicitados pelo lado cliente no Front-End.

#### Funciona assim

> [!NOTE]
> O cliente acessa o computador e faz uma requisição de um acesso a um endereço para o servidor web. O servidor web, por sua vez, acessa o servidor de banco de dados (SGBD) para autenticação do usuário e consulta de dados, que por sua vez são enviados para o Front-End, e dessa forma, exibidos para o usuário.
>
> Diferentemente do Front-End, o Back-End continua sendo executado de forma síncrona no servidor, e uma queda na conexão fará o usuário perder a conexão com o sistema.

~~~mermaid
graph TD
    A(Cliente/Usuário) -- Acessa --> Sistema

    subgraph Sistema [Site dinâmico]
        direction LR

        subgraph Back-End
            direction TD
            D(Servidor Web/Serviço de Hospedagem) -- Consulta --> E[(SGBD)]

            E -- Retorna --> D
        end

        Front-End -- Faz a requisição --> Back-End
        Back-End -- Envia --> Front-End

        subgraph Front-End
            direction TD
            B(PC<br>---------<br>Mobile) -- Executa --> C(Navegador)

            C -- Exibe --> B
        end

        
    end
~~~