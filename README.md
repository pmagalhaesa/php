# php
## Formas de inserção de códigos PHP em páginas HTML
```php
<?php echo 'Modo compatível com documentos XHTML ou XML'; ?>

<script language="php">
echo 'alguns editores (FrontPage) não gostam de tags padrão';
</script>

<? echo 'Forma mais simples, uma instrução de processamento SGML'; ?>
<?= expressão ?> #Isto é um atalho para "<? echo expressão ?>"


<% echo 'Você pode opcionalmente usar tags no estilo ASP'; %>
<%= $variavel; # Isto é um atalho para "<% echo . . ." %>
```
OBS:
- Para trabalhar com tags curtas, é necessário habilitar short_open_tag no php.ini.
- Para trabalhar com tags no estilo ASP, é necessário habilitar asp_tags no php.ini.

## Codificação
- Uso de ponto e virgula ao final ( ; ) dos comandos
```php
<?php echo 'Olá mundo!!'; ?>
```
- Inclusão de outros scripts (Bibliotecas)
```php
<?php
include 'vars.php';
echo "Ola mundo!!";
?>
```
- Variáveis
  - São representadas por um $ seguido de um identificador
  - São case sensitive ($a não é o mesmo que $A)

```php
<?php
$var = 'Bob';
$Var = 'Joe';
echo "$var, $Var"; // exibe "Bob, Joe"
?>
```
- Constantes
  - São declaradas por meio da função define() ou da palavra-chave const
  - Aceitam apenas dados escalares: Boolean, integer, float e string)

```php
<?php
define("CONSTANT", "Hello world.");
echo CONSTANT; // imprime "Hello world."
const VALOR = 50;
echo VALOR; // imprime “50"
?>

```
- Constantes Mágicas
```php
<?php
echo "Linha: " . __LINE__; // Linha atual no arquivo PHP
echo "Arquivo: " . __FILE__; // Caminho completo e nome do arquivo PHP
echo "Diretório: " . __DIR__; // Diretório do arquivo PHP
// Outras constantes mágicas: __FUNCTION__, __CLASS__,
// __METHOD__, __NAMESPACE__
?>
```
## Tipos de dados
![tipos-de-dados-php](http://i.imgur.com/ShgBvcH.png)
## Variáveis pré-definidas
![tipos-de-dados-php](http://i.imgur.com/HP1LhKl.png)
![tipos-de-dados-php](http://i.imgur.com/p0lpucL.png)
## Controle de Sessão
- Motivação
  - Em aplicações Web, na maioria dos casos, é importante oferecer um conjunto de funcionalidades aos usuários, como:
    - Saber que o usuário já efetuou login ao sistema;
    - Guardar preferências da aparência (cor de fundo, tamanho do texto);
    - Relembrar das escolhas feitas anteriormente;
    - Manter informações como carrinhos de compra.
  - Para isto, utiliza-se o que chamamos de informações de estado, ou seja, informações sobre a sessão do usuário.
  - Acontece que o protocolo HTTP é stateless (sem manutenção de estado). Em outras palavras, toda requisição é uma nova requisição.
  - Por outro lado, a maioria das plataformas Web (PHP, .NET, Java) possuem ferramentas para gerenciar sessões e guardar informações de estado.
- Abordagens
  - Para manter as informações através de diversas requisições:
    - Campos ocultos de formulários
      - Campos ocultos guardam dados temporariamente que precisam ser encaminhados ao servidor sem que o usuário perceba
      - Campos ocultos são criados por meio do element <input> e são compostos por pares nome e valor
```html
<input type="hidden" token="A3453DD">
```

      - Ao submeter um formulário para um script PHP, os dados são acessados via variáveis globais $_GET[ ], $_POST[ ] ou $_REQUEST[ ]
      - Para passer os valores de um script para outro, armazene novamente em novos campos ocultos. 
    - Query strings
      - Query String é um conjunto de pares nome=valor acrescentados ao final da URL
      - É iniciada por uma interrogação (?) após a URL http://site.com/Page.php?nome=Rommel&cpf=12345678900
      - Os valores em uma Query String são acessados em um script PHP via variáveis globais $_GET [ ] ou $_REQUEST [ ]
```php
echo "Nome: $_GET['nome'] \n CPF: $_GET['cpf'] ";
``` 

      - Após a utilização de Query Strings os dados são perdidos e precisam ser remontados para que possam ser passados a outros scripts
    - Cookies
      - São utilizados para armazenar dados em formato texto no computador dousuário.
      - Os cookies podem ser:
        - Temporários – Permanecem disponíveis durante a sessão corrente do navegador
        - Persistentes – Permanecem disponíveis por um tempo específico no computadordo cliente
      - O usuário pode escolher se aceita ou não os cookies que um script tentasalvar em seu computador.
      - Outros sites podem utilizar as informações salvas nos cookies de umcomputador
      - O tamanho máximo de dados em um Cookie é de 4KB
      - A criação de um Cookie é feita pela função:
```php
setcookie (name, value, expires, path, domain, secure)
```

      - A função setcookie deve ser executada antes de enviar qualquer saída para o navegador (espaços, echo, print, etc.)
```php
<?php setcookie("firstName", "Don"); ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html>
```

      - O commando pode ser chamado diversas vezes para cada valor a ser armazenado
```php
setcookie("nome", "Rommel");
setcookie("cpf", "12345678900");
```

    - Controle de Sessão
      - É necessário executar o commando session_start() para iniciar uma sessão e session_destroy() para finalizar uma sessão.
      - As informações de sessão são armazenadas e recuperadas em pares nome e valor a partir da variável global $_SESSION[ ]
      - A função session_id()permite obter ou alterar o identificador da sessão do usuário corrente.
```php      
<?php
session_start();
$_SESSION['firstName'] = "Don";
$_SESSION['lastName'] = "Gosselin";
$_SESSION['occupation'] = "writer";
?>
<p><a href='<?php echo "pagina.php?" . session_id() ?>'>Proxima página</a></p>
```
![sessao](http://i.imgur.com/KfeoIMm.png)
