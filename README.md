# Modelo OSI and NAT

## Compreendendo o modelo OSI através de um laboratório e entendo algumas funções do NAT.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/46ee9880290473b9b8444979065a14552dd085dd/imagens/laboratorio.png)
Fonte: elaborado pelo autor (2026)


O objetivo com esse laboratório é apresentar como os dados trafegam e como as regras de NAT podem auxiliar na camada 3 (redes) do modelo OSI, ao decorrer desse projeto, seram apresentados os testes de encaminhamento de pacotes, como o SRCNAT atua permitindo que aparelhos na rede privada tenham acesso à internet e como fazer uma acesso usando DSTNAT em redes privadas, utilizando o PORT FORWARD.

# Testando conectividade para a internet

Nesta imagem o pc linux com IP privado 192.168.10.10 está fazendo um ping para a uol.com onde recebe retorno de conexão, aqui atua a camada 4 (transporte) que cria uma conexão com protocolo (TCP).

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/90da5d697fb9c78d93a0033799de94f88742d035/imagens/test-ping-linux.png)
Fonte: elaborado pelo autor (2026)

# Regra de SRCNAT e captura de tráfego

Quando efetuado a configuração da regra do SRCNAT, informamos por qual saída ela será utilizada, com isso, quando nosso IP privado faz uma requisição para um site, ao chegar na camada 3 (redes), essa regra é acionada e saímos com um IP público para a INTERNET, ou dependendo da sua configuração com um IP de CGNAT, IP privado do provedor, funciona como NAT sobre NAT. Feito isso, o roteador guarda os estados das requisições para quando receber as informações solicitadas, saber para quem enviar na rede interna. 

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

Quando efetuado a configuração da regra do DSTNAT, informamos no MIKROTIK (que está na EMPRESA A, Operadora 1), por qual porta externa será feito o acesso remoto, com isso, quando nosso IP Público tem uma porta configurada é possível acessar uma rede privada, desde tenha uma porta interna redirecionada para o IP do dispositivo que se queira acessar, logo, utilizamos aqui também a camada 3 (redes), a camada 4 (transportes) e um detalhe importante e que na configuração setamos o protocolo TCP, pois precisamos que os dados sejam entregues e de forma confiável. Feito isso, o roteador MIKROTIK que está na EMPRESA A, tem toda essa regra configurada. 
