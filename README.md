# Modelo OSI and NAT

## Compreendendo o modelo OSI através de um laboratório e entendo algumas funções do NAT.

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/46ee9880290473b9b8444979065a14552dd085dd/imagens/laboratorio.png)

Laboratório
Fonte: elaborado pelo autor (2026)


O objetivo com esse laboratório é apresentar como os dados trafegam e como as regras de NAT podem auxiliar na camada 3 (redes) do modelo OSI,
ao decorrer desse projeto, seram apresentados os testes de encaminhamento de pacotes, como o SRCNAT atua permitindo que aparelhos na rede privada
tenham acesso à internet e como fazer uma acesso usando DSTNAT em redes privadas, utilizando o PORT FORWARD.

# Testando conectividade para a internet

Nesta imagem o pc linux com IP privado 192.168.10.10 está fazendo um ping para a uol.com onde recebe retorno de conexão,
aqui atua a camada 4 (transporte) que cria uma conexão com protocolo (TCP).

![image alt](https://github.com/Franco-Bruno/modelo-osi-and-nat/blob/90da5d697fb9c78d93a0033799de94f88742d035/imagens/test-ping-linux.png)

# Regra de NAT e captura de tráfego

Quando efetuado a configuração da regra do SRCNAT, informamos por qual saída ela será utilizada, com isso, quando nosso
IP privado faz uma requisição para um site, ao chegar na camada 3 (redes), essa regra é acionada e saímos com um IP 
público para a INTERNET, ou dependendo da sua configuração com um IP de CGNAT, IP privado do provedor, funciona como 
NAT sobre NAT. Feito isso, o roteador guarda os estados das requisições para quando receber as informações solicitadas, 
saber para quem enviar na rede interna. 

