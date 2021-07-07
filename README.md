# Desmistificando JWT

## JWT

- Trata-se de um formato de representação de dados (claims) usado em cenários aonde há um necessidade de restrição de espaço, como é o caso da Web;
- É especificado pela RPC 7519;
- Deve possuir um tamanho máximo de 8kb;
- Importante sempre consultar as "claims" padrão para evitar colisão com as "claims - públicas", lista completa [IANA](http://github.com)

## JWS

- Representação de um JWT protegido;
- Especificado pela RFC 7515
- Divide-se em 3 partes (é atravez dessas partes que a segurança do JWT é garantida)
  -   Header - Define qual o tipo do token e qual o algoritmo utilizado para a geração do mesmo;
  -   Body - Consiste no payload (coleção de claims neste contexto) que será trafegado;
  -   Assinatura - Consiste na representação encriptada do Header + Body, através do algoritmo especificado no Header e um secret da aplicação;
    - Pode ser feita de duas formas:
    - Assinatura Digital, utilizando uma chave Assimétrica;
    - Message Authentication Codes (MACs);

# Geração Header JWS
