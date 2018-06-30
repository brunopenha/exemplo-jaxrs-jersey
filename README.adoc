= Exemplo JAX-RS : usando Jersey
:toc:
:toc-placement: manual
:toclevels: 2

image:https://travis-ci.org/brunopenha/exemplo-jaxrs-jersey.svg?branch=master["Situação da Construção", link="https://travis-ci.org/brunopenha/exemplo-jaxrs-jersey"]

toc::[]

== Resumo

Projeto de exemplo para testar JAX-RS 2.0 usando Jersey 2.x

== Criando o projeto

Maven archetype used :

[source,shell]
----
mvn archetype:generate -DarchetypeGroupId=org.glassfish.jersey.archetypes -DarchetypeArtifactId=jersey-quickstart-webapp -DarchetypeVersion=2.27 -DgroupId=br.nom.penha.bruno.exemplo.jaxrs -DartifactId=exemplo-jaxrs-jersey -B
----

== Executando

Execute a aplicação web com:

[source,shell]
----
mvn jetty:run
----

[ATENÇÃO]
Jetty 9 requer Java 8 !

=== Em caso de falha no plugin...

Caso receba o erro:

[source,shell]
----
[ERROR] No plugin found for prefix 'jetty' in the current project and in the plugin groups
----

Inclua no seu arquivo settings.xml o repositório abaixo, pois o Jetty não fica mais no Maven Central:

[source,xml]
----
  <pluginGroups>
    <pluginGroup>org.mortbay.jetty</pluginGroup>
  </pluginGroups>
----

== REST com JAX-RS

O que é o uso de certos cabeçalhos HTTP ?

=== Cabeçalhos da Requisição (Request Headers)

|===
| Cabeçalho HTTP  | Uso | Anotações JAX-RS | Exemplo

| `Accept`
| Usado para ajustar a preferência do tipo de conteúdo do *response body*. Pode ter multiplos valores. Se for inválido, o servidor irá enviar um HTTP 406.
| `@Produces`
| application/json,application/xml

| `Content-Type`
| Usado para especificar o tipo de conteúdo do *request body*.
| `@Consumes`
| application/json
|===

=== Cabeçalhos da Resposta (Response Headers)

|===
| Cabeçalho HTTP | Uso | Anotações JAX-RS | Exemplo

| `Content-Type`
| Usado para especificar o tipo de conteúdo do *response body*. Não haverá cabeçalho se não houver conteúdo.
| Depende do `@Accept` e https://en.wikipedia.org/wiki/Content_negotiation[Content negotiation]
| application/json
|===

== JAX-RS com Jersey

Foi usado o  https://jersey.github.io/[Jersey] como a implementação do https://github.com/jax-rs[JAX-RS].

Até a versão do Jersey 2.25, é necessário ter o Java 6 e JAX-RS 2.0 (https://jcp.org/en/jsr/detail?id=339[JSR-339]) .

Para o Jersey 2.26, existem https://jersey.github.io/documentation/latest/migration.html#mig-2.26[mudanças importantes] :

- Requer Java 8
- Use JAX-RS 2.1 (https://jcp.org/en/jsr/detail?id=370[JSR-370])

== Docker

=== Construindo uma imagem:

[source,shell]
----
docker build -t exemplo-jaxrs-jersey .
----

=== Rodando um conteiner

[source,shell]
----
docker run -d –name jaxrs-teste-1 -p 8090:8080 exemplo-jaxrs-jersey
----

=== Testes

Abra um navegador e acesse http://localhost:8090/exemplo-jaxrs-jersey/[http://localhost:8090/exemplo-jaxrs-jersey/]

Ou tente :

[source,shell]
----
curl -X GET http://localhost:8090/exemplo-jaxrs-jersey/webapi/myresource[http://localhost:8090/exemplo-jaxrs-jersey/webapi/myresource]
----

_Gerado com Asciidoctor {asciidoctor-version}_
