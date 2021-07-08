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

## Tipos de Criptografia

O ciframento de uma mensagem (processo em que um conteúdo é criptografado) é baseado em 2 componentes:
- um algoritmo;
- uma chave de segurança.

### Simétrica

A criptografia simétrica faz uso de uma única chave, que é compartilhada entre o emissor e o destinatário de um conteúdo. Essa chave é uma cadeia própria de bits (secret), que vai definir a forma como o algoritmo vai cifrar um conteúdo.

Como vantagem, a criptografia tem uma boa performance e a possibilidade de manter uma comunicação contínua entre várias pessoas simultaneamente. Caso a chave seja comprometida, basta efetuar a troca por uma nova, mantendo o algoritmo inicial.

![criptografia simétrica](https://github.com/phmmdev/jwt-fundamentals/blob/main/simetric.png)

### Assimétrica

Também chamada de criptografia de chave pública, eles propuseram um sistema para cifrar e decifrar uma messagem com duas chaves distintas, sendo a pública (chave pública) que pode ser divulgada e a outra mantida em segredo (chave privada). Funcionando da seguinte forma: se crifrar a mensagem com a chave privada ela somente será decifrada pela chave pública e vice-versa.

![criptografia assimétrica](https://github.com/phmmdev/jwt-fundamentals/blob/main/assimetric.png)

## JWE

Diferentemente do que é proposto no ** JWS ** o JWE tem como premissa, garantir a criptografia dos dados do header e do payload em todo o seu trajeto (transmissor >> Receptor).
Dessa forma somente o receptor "autorizado", poderá abrir o token e assim visualizar suas claims (dados de um token).
Divide-se em 5 partes:
 - Header (cifrado)
 - JWE CEK (Content Encription Key - chave utilizada para criptografar o conteudo que ficará no campo cipher text. para não ser passada como plain text é utilizada uma técnica
chamada, KEY WRAPPING)
 - Initialzation Vector (Numero arbritário utilizado uma unica vez no processo de criptografia junto a CEK, com base nele é gerado a Authorization Tag)
 - Cipher Text (Conteúdo / payload)
 - Authorization Tag ("marcação" gerada após o processo de criptografia dos conteudos, tendo em base CEK + Initialization Vector. É com essa TAG que é garantido que o conteúdo cifrado não foi auterado)

** IMPORTANTE ** : todas as 5 partes de um JWE seguem o seguinte padrão:
```
BASE64URL
(
  UTF8
  (
    CONTENT
  )
)
```
### JWE na prática

Para que seja possivel gerar um JWE e utilizá-lo em uma comunicação os seguintes deverão ser seguidos:
 - primeiramente é necessário termos em mãos o CEK, para isso utiliza-se a chave pública compartilhada de quem é o detentor da chave privada.
 - com as informações declaradas no header a respeito do algoritimo, o Initialization Vector e a CEK é feita a criptografia do Header + Body
 - Com o Token gerado somente a origem detentora da chave privada terá como abrir tal token.

![criptografia assimétrica](https://github.com/phmmdev/jwt-fundamentals/blob/main/jwe-schema.png)

**NOTA:** JWE trata-se de um modelo não tão comum / utilizado, dado sua complexidade e acoplamento exigido pelas soluções.

## JWK

Consiste na representação da chave de criptografia. Tal estrtrutura depende exclusivamente de qual **Algorimo** (JWA) será utilizado, fazendo com que o numero de porametros contidos nela venha a variar

### Exemplo JWK RSA

![jwk-rsa](https://github.com/phmmdev/jwt-fundamentals/blob/main/swk-rsa.png)

### Exemplo JWK Curvas Elípticas

![jwk-eliptic](https://github.com/phmmdev/jwt-fundamentals/blob/main/jwk-eliptic.png)


## JWKS

Array de JWK, utilizado para o processo de compartilhamento dessas. Sua finalidade é permitir que os servidores OAuth 2.0 seja flexiveis em relação a criptografia, podendo inserir ou trocar os algoritmos utilizados no processo.

Exemplo: https://www.googleapis.com/oauth2/v3/certs  (JWKS público)

## JWA

Trata-se do algoritimo que será utilizado no processo de criptografia para geração de tokens.


