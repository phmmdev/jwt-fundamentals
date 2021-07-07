# Desmistificando JWT

## JWT

### Visão geral

![diagrama principal](https://github.com/phmmdev/jwt-fundamentals/blob/main/main-diagram.png)

- Trata-se de um formato de representação de dados (claims) usado em cenários aonde há um necessidade de restrição de espaço, como é o caso da Web;
- É especificado pela RPC 7519;
- Deve possuir um tamanho máximo de 8kb;
- Importante sempre consultar as "claims" padrão para evitar colisão com as "claims - públicas", lista completa [IANA](http://github.com)

## JWS

### Visão geral

![diagrama principal](https://github.com/phmmdev/jwt-fundamentals/blob/main/jws-overview.png)

- Representação de um JWT protegido;
- A missão de um JWS é garantir que o conteudo não seja manipulado ao longo de seu compartilhamento
- Especificado pela RFC 7515
- Divide-se em 3 partes (é atravez dessas partes que a segurança do JWT é garantida)
  -   Header - Define qual o tipo do token e qual o algoritmo utilizado para a geração do mesmo;
  -   Body - Consiste no payload (coleção de claims neste contexto) que será trafegado;
  -   Assinatura - Consiste na representação encriptada do Header + Body, através do algoritmo especificado no Header e um secret da aplicação;
    - Pode ser feita de duas formas:
    - Assinatura Digital, utilizando uma chave Assimétrica;
    - Message Authentication Codes (MACs);

**IMPORTANTE:** Não se deve colocar dados sensíveis em um token JWT, uma vez que o mesmo não garante segrança em uma perspectiva de confidencialidade. Os processos de geração tanto do Header quanto do Body do token **NÃO** são criptografados. (as informações são públicas, por isso utilizando o jwt.io, conseguimos visualizar as claims de um token).
A seguir estão os processos de geração dessas duas partes (Header e Body)

## Geração Header JWS

### Visão geral

![diagrama geração](https://github.com/phmmdev/jwt-fundamentals/blob/main/header-generation-process.png)

## Geração Body JWS

### Visão geral

![diagrama geração](https://github.com/phmmdev/jwt-fundamentals/blob/main/body-generation-process.png)

## Geração Assinatura JWS

### Visão geral

![diagrama geração](https://github.com/phmmdev/jwt-fundamentals/blob/main/signature-generation-process.png)
