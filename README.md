# Modelo OSI and NAT

## Compreendendo o modelo OSI através de um laboratório e entendo algumas funções do NAT.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/46ee9880290473b9b8444979065a14552dd085dd/imagens/laboratorio.png)

Fonte: elaborado pelo autor (2026)


O objetivo com esse laboratório é apresentar como os dados trafegam e como as regras de NAT podem auxiliar na camada 3 (redes) do modelo OSI, ao decorrer desse projeto, seram apresentados os testes de encaminhamento de pacotes, assim como o SRCNAT atua, permitindo que aparelhos na rede privada tenham acesso à internet e como fazer um acesso remoto usando DSTNAT em redes privadas, utilizando o PORT FORWARD.

# Testando conectividade para a internet

Nesta imagem o PC Linux (Colaborador, Operadora 2) com IP privado 192.168.10.10 está fazendo um ping para a "uol.com" onde recebe retorno/respota de conexão através do protocolo (ICMP), aqui atua a camada 4 (transporte) que cria uma conexão com protocolo (TCP).

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/90da5d697fb9c78d93a0033799de94f88742d035/imagens/test-ping-linux.png)

Fonte: elaborado pelo autor (2026)

# Regra de SRCNAT e captura de tráfego

Quando efetuado a configuração da regra do SRCNAT (roteador OPERADORA_2), informamos por qual saída ela será utilizada, com isso, quando nosso IP privado faz uma requisição para um site, ao chegar na camada 3 (redes), essa regra é acionada e saímos com um IP público para a INTERNET, ou dependendo da sua configuração com um IP de CGNAT, IP privado do provedor, funciona como NAT sobre NAT. Feito isso, o roteador guarda os estados das requisições para quando receber as informações solicitadas, saber para quem enviar na rede interna. 

## Exemplo: 

PAT (Port Address Translation) dentro do NAT (Network Address Translation)

IP INTERNO: 192.168.10.9   --->  SAI COMO (IP público + porta) 100.1.1.2:10001

IP INTERNO: 192.168.10.10  --->  SAI COMO (IP público + porta) 100.1.1.2:10002     
             

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/b4425996f647b593b9b914460a3eb6ab619c4955/imagens/regra-nat.png) 

Fonte: elaborado pelo autor (2026)

Nessa parte é possível verificar o IP de origem e o IP de destino.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/main/imagens/rota-nat.png)

Fonte: elaborado pelo autor (2026)

Agora podemos ver abaixo o tráfego da rede tanto pela ETHER1 quanto pela ETHER2.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/main/imagens/trafego-ether1-ether2.png)

Fonte: elaborado pelo autor (2026)

Então temos aqui uma apresentação de como o SRCNAT funciona de forma prática, a seguir será apresentado como o DSTNAT funciona.

# Regra de DSTNAT e captura de tráfego

Quando efetuado a configuração da regra do DSTNAT, informamos no MIKROTIK (que está na EMPRESA A, Operadora 1), por qual porta externa será feito o acesso remoto, com isso, quando nosso IP Público tem uma porta configurada é possível acessar uma rede privada, desde que tenha uma porta interna redirecionada para o IP do dispositivo que se queira acessar, logo, utilizamos aqui também a camada 3 (redes), a camada 4 (transportes) e um detalhe importante e que na configuração setamos o protocolo TCP, pois precisamos que os dados sejam entregues e de forma confiável. Feito isso, o roteador MIKROTIK (que está na EMPRESA A), tem toda essa regra configurada. 

Então sabendo que o nosso IP PÚBLICO é o 177.1.1.2 que está configurado no MIKROTIK, fizemos um redirecionamento para que quando acessado pela PORTA 9090, que é a porta externa, tenha acesso ao nosso servidor linux com IP PRIVADO 10.10.10.200 que está configurado na PORTA 80, no caso, porta interna.

# Acessando o servidor linux remotamente via terminal

Com nosso MIKROTIK configurado (empresa A, Operadora 1), acessamos nosso linux (Colaborador, Operadora 2) IP PRIVADO 192.168.10.10, no terminal digitamos "curl -I http://177.1.1.2:9090". Com isso, fazemos a solicitação via navegador onde conseguirmemos alcançar nosso servidor linux IP PRIVADO 10.10.10.200:80, constatando que obtivemos êxito no redirecionamento das portas.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/main/imagens/acesso-webserver-and-port-tcp.png)

Fonte: elaborado pelo autor (2026)

Podemos ver a seguir os pacotes sendo enviados na rede.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/main/imagens/captura-trafego-mikrotik.png)

Fonte: elaborado pelo autor (2026)

Conexãoes estabelecidas no MIKROTIK, mostrando a origem e destino.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/main/imagens/captura-trafego.png)

Fonte: elaborado pelo autor (2026)

Podemos ainda ver de forma bem detalhada, como a origem, destino e portas.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/main/imagens/trafego-detalhado.png)

Fonte: elaborado pelo autor (2026)

E também foi preciso simular um "roteamento(BGP)" estre as redes para que pudessem cada uma ter acesso à internet, mas também serem alcançáveis entre si.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/main/imagens/roteamentoBGP-routes.png)

Fonte: elaborado pelo autor (2026)

# Versão funcional usando conceitos do MODELO OSI, ROTEAMENTO E NAT (SRCNAT, DSTNAT e PAT).
