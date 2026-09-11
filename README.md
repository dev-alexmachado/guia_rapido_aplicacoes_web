# Guia Rápido Aplicações Web

## Sumário

1. [O que é uma aplicação web](#o-que-é-uma-aplicação-web)
2. [Front-End](#front-end)
3. [Back-End](#back-end)
4. [Design Pattern](#design-pattern)<br>
    4.1 [MVC: Model-View-Controller](#mvc-model-view-controller)<br>

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
---
title: Aplicação estática - HTML/CSS/JS puro
---
graph TD
    Usuário(Usuário)

    subgraph Sistema [Site Estático]
        direction TD

        subgraph Hospedagem
            direction TD

            SW(Servidor Web)

            subgraph Front-End
                direction LR
                subgraph Código-Fonte
                    HTML(HTML)
                    CSS(CSS)
                    JS(JS)
                end

                subgraph Mídias
                    Imagens(Imagens)
                    Vídeos(Vídeos)
                    Áudios(Áudios)
                    Fontes(Fontes)
                end
            end
        end

        subgraph Cliente
            direction LR

            Navegador(Navegador)

            subgraph Dispositivo
                PC(PC)
                Mobile(Mobile)
            end
        end
    end

    Usuário -- Acessa --> Sistema
    Dispositivo -- 1. Executa --> Navegador
    Cliente <-- 2. Acessa / 3. Envia --> Hospedagem
    SW -- Hospeda --> Front-End

    style Cliente fill: #333
    style Hospedagem fill: #333
    style Dispositivo fill: #16161d
    style Front-End fill: #16161d
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
---
title: Aplicação dinâmica - Front-End + Back-End
---
graph TD
    Usuário(Usuário)

    subgraph Sistema [Site dinâmico]
        direction TD

        subgraph Hospedagem
            direction TD

            Servidor(Servidor)

            subgraph Nuvem
            direction LR

                subgraph Back-End
                    Linguagem(Linguagem de Programação)
                    BD[(Banco de Dados)]
                end

                subgraph Front-End
                    Mídia(Mídias)
                    Código-Fonte(Código-Fonte)
                end
            end
        end

        subgraph Cliente
            direction LR

            Navegador(Navegador)

            subgraph Dispositivo
                PC(PC)
                Mobile(Mobile)
            end
        end
    end

    Usuário -- Acessa --> Sistema
    Dispositivo <-- 1. Executa / 8. Exibe --> Navegador
    Cliente <-- 2. Solicita / 7. Responde --> Hospedagem
    Código-Fonte <-- 3. Requisita / 6. Retorna --> Linguagem
    Linguagem <-- 4. Consulta / 5. Retorna --> BD
    Servidor -- Hospeda --> Nuvem

    style Cliente fill: #333
    style Hospedagem fill: #333
    style Dispositivo fill: #16161d
    style Nuvem fill: #16161d
~~~

## Design Pattern

Os **Design Patterns** nada mais são do que arquiteturas de desenvolvimento de software. São utilizados para organizar melhor o código-fonte para facilitar a manutenação do código. Existem vários Design Patterns que são utilizados no mercado, mas alguns são mais utilizados do que outros.

### MVC: Model-View-Controller

De todos os Design Patterns, este com certeza é o mais famoso, e também o mais usado, principalmente em Java e PHP.

Nesse Design Pattern, a estrutura do projeto é dividido em 3 camadas:
- **Model**: corresponde à parte do código responsável pela comunicação com banco de dados e das regras de validação. É aqui onde ficam a parte do código que possui as regras de negócio da aplicação.
- **View**: corresponde à parte do sistema que é visível para o usuário, onde entrarão o UX/UI (User Experience e User Interface). Em outras palavras, aqui é onde fica o Front-End da aplicação.
- **Controller**: responsável por transitar os dados entre a ***view*** e a ***model***.

#### Diagrama
~~~mermaid
---
title: Sistema
---
graph TD
    Usuário(Usuário)
    BD[(Banco de Dados)]

    subgraph View
        Front-End(Front-End)
    end

    subgraph Controller
        Rota(Rotas)
        Ação(Ações)
    end

    subgraph Model
        subgraph Classes
            direction LR
            Atributo(Atributos)
            Método(Get e Set)
        end
    end

    Usuário -- Visualiza --> View
    View <-- 1. Requisita / 8. Recebe --> Controller
    Rota -- Executa --> Ação
    Controller <-- 2. Envia / 7. Recebe --> Model
    Atributo <-- 3. Acessa / 6. Retorna --> Método
    Model <-- 4. Consulta / 5. Retorna --> BD

    style View fill: #333
    style Controller fill: #333
    style Model fill: #333
~~~

### MVT: Model-View-Template

No framework web para Python Django, é usado o Design Pattern MVT, que é uma variação do MVC:
- **Model**: tem a mesma funcionalidade da Model do MVC
- **View**: aqui, a View tem uma função parecida com a do Controller do MVC. É ele que estabelece as rotas e trata os dados da aplicação.
- **Template**: no Django, o Template faz o papel do Front-End da aplicação.

#### Diagrama

~~~mermaid
graph TD
    Usuário(Usuário)
    BD[(Banco de Dados)]

    subgraph Template
        Front-End(Front-End)
    end

    subgraph View
        Rota(Rota)
        Ação(Ação)
    end

    subgraph Model
        subgraph Classe
            direction LR
            Atributo(Atributo)
            Método(Método)
        end
    end

    Usuário -- Visualiza --> Template
    Template <-- 1. Requisita / 8. Recebe --> View
    View <-- 2. Envia / 7. Recebe --> Model
    Atributo <-- 3. Acessa / 6. Retorna --> Método
    Model <-- 4. Consulta / 5. Retorna --> BD
    Rota -- Executa --> Ação

    style Classe fill: #333
~~~